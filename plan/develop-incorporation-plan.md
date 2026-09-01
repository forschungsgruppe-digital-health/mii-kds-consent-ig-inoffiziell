# Plan: incorporate `develop` into the Consent migration branch

**Status: PLAN ONLY — no integration executed** (user instruction 2026-09-01).
Target when GO: branch `migration/2027.0.0-ballot.rc1-template-v0.13.2` (PR
medizininformatik-initiative/kerndatensatzmodul-consent#131).
Delta measured: `792f9f3e` (tag 2026.0.0, the migrated baseline) → `source/develop`
tip **`744f7ba`** (2026-08-21, Bialke; unchanged since — same tip the plan of
2026-08-31 recorded). 18 commits, **7 files**, +232/−158.

## 1. The delta, file by file (measured)

| # | File | Change | Commits |
|---|---|---|---|
| Δ1 | `ressourcen-profile/Profile_MII_Consent_Einwilligung.xml` | **Re-parented**: `baseDefinition` core `Consent` → `http://fhir.de/ConsentManagement/StructureDefinition/Consent` (HL7-D profile). `Consent.category` **min 2 → 0**. Slice `loinc` → **renamed `consentCategory`**; slice `mii` kept (version-modules pattern); **new slices `resultType`** (required binding `…/ValueSet/ResultType`) **and `templateType`** (extensible binding `…/ValueSet/TemplateType`), each with min-1 coding/system/code + mustSupport. `version` 1.0.9 → 1.1.0, date 2026-08-21 | 401133b, 5b22e17, 6542cc3/5a5fd5c/744f7ba |
| Δ2 | 3 examples (`Einwilligung`, `Einwilligung_2`, `ResultType_ConsentStatus`) | Category system `…/CodeSystem/mii-cs-consent-consent_category` → **`…/CodeSystem/mii-cs-consent-version-modules`** — **this is the D-9 dangling-CS fix** | 128f146, 539e2f8, 1d9e79c |
| Δ3 | `terminologie/codesystems/CodeSystem-MiiConsentPolicyCodeSystem.xml` | ~19 display corrections: ACRIBIS labels de-comma'd + "(ACRIBIS)" suffix, "(PROM)" suffixes, SNID display/typo/module-name fixes ("verabeiten"→"verarbeiten", `Z4_Rekontaktierung_FU` → sprechend), deprecated-codes formatting. **CS `version` stays 1.1.0 and `count` stays 101 — both upstream misses** | dbdbabc…bc05772, 37e524d, e742208, 3885622/4d44dbe |
| Δ4 | `terminologie/codesystems/CodeSystem-MiiConsentVersionModuleCodeSystem.json` | +1 concept `…24.2.4055` "Version 1.7.2 Vertretende" (+ child property on 184) | afce23a |
| Δ5 | `terminologie/codesystems/CodeSystem-MiiConsentPolicy.md` | The **hand-maintained markdown mirror**: 252-line churn — display renames + ~~strikethrough~~ for deprecated policies | 37e524d + display commits |

Overlap check vs. our applied QA fixes: develop does **not** touch example displays
(0 display lines in Δ2) and its Δ3 display changes hit Z2–Z5 module codes the
examples don't use → **no conflict with the 2026-08-31 display harmonization**;
our `count 101→124` fix **stands** (develop still wrong at 101 — upstream note).

## 2. Impact map onto the migrated structure

| Δ | Migrated target | Action |
|---|---|---|
| Δ1 | `input/fsh/profiles/MII_PR_Consent_Einwilligung.fsh` | Port via **targeted goFSH re-derivation** (route A below). Ripples: SUSHI parent becomes the **snapshot-less HL7-D profile** (covered — our `-snapshots` cache entry has `profile-ConsentManagement-Consent` verified); `^version` stays harmonized `2027.0.0-ballot.rc1` (record develop's 1.1.0 in the ledger); `^date` → 2026-08-21 (carry) |
| Δ2 | `input/fsh/instances/{34150a23,5143266b,Example-MII-Consent-ResultType-document}.fsh` | Trivial: swap the category system alias/URL (3 lines). **Also decide for the D-14 example `89f494a3`** (registry-only; develop can't fix what it doesn't have — apply the same swap for consistency, recorded) |
| Δ3 | `input/fsh/codesystems/MII_CS_Consent_Policy.fsh` | Port displays via goFSH re-derivation or scripted display-map patch. Keep OUR `^count = 124`. Then **re-run the example↔CS display check** (expect no drift; Δ3 codes unused by examples) |
| Δ4 | `input/fsh/codesystems/MIIConsentVersionModuleCodeSystem.fsh` | Port +1 concept + property (goFSH re-derivation preferred — nested-concept FSH is fiddly by hand) |
| Δ5 | `input/pagecontent/code-systems.md` (policy table) + EN mirror | Transfer develop's regenerated mirror table — **re-normalized** (the table-shatter gotcha: join rows, no blank lines) and with the strikethrough formatting; also refresh the 3 renamed-display rows in any prose |
| all | `input/pagecontent/changes.md` + EN | New changelog section for the incorporation — **must carry a BREAKING entry** per the page's own rule: `category` min 2→0 + slice rename + re-parent change instance-validation semantics |
| all | intro-note `StructureDefinition-e0e166b4…-intro.md` + EN | The transferred 2026.0.0 narrative now describes the OLD slicing ("min 2", loinc slice, "2..*" cardinality prose). **The Simplifier guide has no updated version** → either (a) minimally annotate the affected table rows as superseded-by-develop (DERIVED:summary markers), or (b) leave verbatim + a prominent Gate-B note. Recommend (a) for the 3 directly-false rows; full narrative rework = owner content work |

## 3. Mechanics (when GO)

1. **Pin the delta**: record `744f7ba` as the incorporation source; per-resource commit shas in the ledger (`bash $ML claim`-style info lines).
2. **Route A — targeted goFSH re-derivation** (preferred for Δ1/Δ3/Δ4): run
   `npx gofsh@2.6.1` on a scratch copy of ONLY the changed source files (with
   `-d de.einwilligungsmanagement@2.0.3 -d hl7.fhir.r4.core@4.0.1`,
   `-t json-and-xml`), postprocess, then **FSH-diff against our tree** and port
   hunks — preserves the proven pipeline semantics and catches XML→FSH subtleties
   (nested concepts, slicing) that hand-editing gets wrong. Δ2 = 3-line hand edit.
3. **Parent pin decision (owner-facing)**: develop's rc-4 package pins
   `de.einwilligungsmanagement` **2.0.3**; the re-parent makes the parent profile
   load-bearing. Recommend moving to **`2.0.3-snapshots`** (sandbox-measured:
   21/21 differentials generate on 2.0.3, better than 2.0.2's 18/21):
   `scripts/generate-parent-snapshots.sh` PARENT_VERSION → 2.0.3 + sushi-config
   pin + F2 ledger note. Fallback: stay on 2.0.2-snapshots (profile exists there
   too) if the owners want the released-pin story.
4. **Version/identity bookkeeping**: all resource versions stay harmonized at
   `2027.0.0-ballot.rc1` (develop's 1.0.9→1.1.0 recorded as superseded);
   **REVISE every "content-identical to release 2026.0.0" claim** (README,
   changes.md sections, report summary, PR body) to
   "release 2026.0.0 **+ the develop delta up to 744f7ba** (unreleased
   2026.0.1-rc line)".
5. **Rebuild + measure**: expect the **4 `category:mii` slice errors and the
   dangling-canonical class to disappear** (D-9 resolved by Δ2); watch for NEW
   classes from the re-parent (HL7-D profile constraints now validate the
   examples — e.g. resultType required binding) and from `consentCategory`'s
   fixed values. Compare per element path against qa-target (33).
6. **Re-verify**: verify-migration — C1/F-checks compare against the pinned tag
   worktree, so Δ-changed resources will read DIVERGIERT; **adjudicate each
   against its develop commit sha** (same pattern as the re-version) or pass a
   second `--source` measurement at `744f7ba` for the affected rows. prepost:
   artifact counts unchanged; re-run for the record.
7. **Report + PR**: new report section "Develop incorporation (744f7ba)" with
   the Δ-table + adjudications; PR comment; decision-queue updates (D-9 →
   RESOLVED-by-incorporation, parent-pin decision, breaking-change entry).
8. Commit shape: one commit per Δ-group (profile / examples / terminology /
   narrative) or a single `feat(migration)!:` — recommend **one commit**
   `feat(migration)!: incorporate develop @744f7ba (2026.0.1-rc line)` with the
   BREAKING footer, matching the re-version precedent.

## 4. Open questions for the owners (ask before or at Gate A)

1. Is `develop@744f7ba` the intended content basis for the **2027 ballot RC**,
   or should the RC stay at released 2026.0.0? (The rc-4 package suggests yes.)
2. `category` min 2→0 + re-parent + slice rename are **breaking** vs 2026.0.0 —
   confirm the changelog framing and implementer guidance.
3. Upstream misses to fix on develop regardless: CS `count` still 101 (actual
   124/125 with Δ4), CS `version` not bumped despite display changes, and the
   packaging drop of `CodeSystem-MiiConsentVersionModuleCodeSystem` from rc-4
   **conflicts with Δ2** (examples now REQUIRE that CS — it must ship).
4. Narrative: the Simplifier guide was never updated for these changes — who
   rewrites the profile prose (intro-note) for the new slicing?

## 5. Effort & risk

~2–4 h mechanics + one rebuild cycle. Main risks: re-parent QA surface
(unknown constraint interactions with the HL7-D parent — mitigated by the
element-path QA diff), and narrative drift (mitigated by the minimal-annotation
route). Everything else is small, measured, and reversible per commit.
