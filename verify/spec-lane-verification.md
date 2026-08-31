# SPEC lane — adversarial verification of `plan/consent-migration-plan.md` against mii-ig-migration @ v0.25.0

**Date:** 2026-08-31 · **Basis:** clone `recon/agent-skills` at tag `v0.25.0` (`git describe --tags` → `v0.25.0`, HEAD `5c0cc0c`), skill `skills/mii-ig-migration/` (SKILL.md 497 lines, migration-spec.md 2924 lines, expected-steps.tsv 31 data rows). All line references below re-read from the clone in this session (MEASURED).

## Method

Line-by-line comparison of the plan's procedure (§3 decision queue + §4 execution plan + §5 risks) against SKILL.md, migration-spec.md, expected-steps.tsv, codes.md, provenance.md, migration-report-template.md, template-pages.tsv, template-artifacts.tsv, and the argparse/flag surfaces of `verify-migration.py`, `guide-harvest.sh`, `page-structure-advice.py`, `comparison-table.py`, `qa-checklist.py`, `license-align.py`, `migration-log.sh`, `derived-scan.py`, `prepost-delta.py`, `first-run-bootstrap.sh` (template clone).

## Checks that PASSED (no findings; spot-verified, not exhaustive list)

- **Ledger arithmetic**: expected-steps.tsv has exactly 31 data rows (lines 25–55); for Consent every condition except `5.1c simplifier-discover` ("no rendered-IG URL was supplied") holds → the plan's "all 31 rows minus exactly one conditional" is correct, and every one of the other 30 rows is placed in a plan phase with the exact `step action` slug from the tsv (verified row-by-row: `1 preflight-analysis`, `pre.2`, `pre.5`, `5.1`, `2.1 ×3`, `5.1d`, `5.1b.2 ×2`, `5.1b.3 ×3`, `5.1b.5`, `5.2 ×4`, `5.3`, `5.4`, `5.4a-d`, `5.5`, `5.6 ×2`, `5.6a`, `7`, `11`).
- **Order**: Gate 0 → identity → 2b goFSH → 2c harvest → skeleton → transfer/Gate A → narrative/Gate B → bilingual/Gate C → build/QA → verify/report/PR matches SKILL steps 1, 2, 2b, 2c, 3–9; gates A/B/C/D after steps 4/5/6/pre-merge (SKILL.md:466-471).
- **No-vendored-template doctrine** (spec:1442-1453, CHANGELOG.md:3-8): plan 5.2 keeps the ig.ini URL line, deletes `ig-template/` + the three sync files, records BOTH `5.2 skeleton-vendored ref=… commit=…` and `5.2 template-reference url=… release=…`; `commit=a2390dea` for v0.13.2 verified in the template clone (`git rev-parse v0.13.2` → `a2390dea`).
- **Manifest stamping**: template-pages.tsv/template-artifacts.tsv stamped `v0.11.1`/pkg `1.3.2`, read 2026-08-20 (file headers lines 9-10 / 31-33); `manifest_stale` at verify-migration.py:1034-1046 downgrades **C5c** (line 1155-1162) and **R4** (line 2550-2558) exactly as the plan says; re-stamp is the file's own sanctioned procedure ("Update this file when the template's page set changes…", template-pages.tsv:36-38).
- **Page-map generate–review–consume** (SKILL.md:295-300, 454, 460; spec §9e/§9f; expected-steps row 5.4c): plan 7.2 + R11 state the overwrite trap and the consume-only-the-map contract correctly, incl. v2 columns and menu budgets (≤33/≤10/≤8/depth 2, hub ≤250 words, branch 4a — spec:2197).
- **Harvest contract** (SKILL.md 2c:240-256; spec:1405-1412): route ① gated human download (spec:1328-1355 verbatim match), route ② discovered-never-constructed slugs, `?version=` pinning, depth-scanned `preview-content`, 18/18/0 + 14/4 reference measurement, `silent-partial-success:`/`generated-view-lossy:` tokens, manifest at `migration-log/guide-harvest.tsv` auto-discovered by the advice run (page-structure-advice.py:960-970) — all as the plan states. (The plan's `--out migration-log/harvest` deviates from the documented example path but is harmless: the manifest path is fixed and the file column resolves — guide-harvest.sh:167, page-structure-advice.py:1061-1067. Not a finding.)
- **Derived-scan marker form** (derived-scan.py:28-31, closed kind set, NO-BOX + bilingual-twin failures; spec:2112): plan 7.5 correct.
- **Prepost-delta census-mode exception** (prepost-delta.py:45-53; SKILL.md step 7): plan 9.3 correct, incl. source-first ordering and equal-packageId trigger.
- **Report generators**: `qa-checklist.py` and `comparison-table.py` exist with the flags the plan names — `--preview-url`/`--source-guide-url` ARE comparison-table flags (comparison-table.py:204-205) and the plan correctly says the verifier has no `--source-guide-url` (verify-migration.py argparse:3456-3483).
- **license-align 5.2** (license-align.py:19-34 contract row 1; spec:1460-1476): byte-faithful copy, `license-replaced:` + FIX row, exit-1 cases to Gate A — plan 5.5 + D-1 correct.
- **goFSH block** (SKILL.md:134-234; spec:755-767): `-t json-and-xml` trap 1-of-20@exit-0, 19 XML + 1 JSON, 41→5→0, `--expected-nonzero` on `sushi-after`, minted ids → ② — plan 3.1 correct.
- **Parent snapshots** (spec:1009-1020, 1106-1116): 21 SDs/0 snapshots both versions, four carry options named exactly, never-hand-rolled rule, upstream escalation — plan D-4/R2 substance correct (but see SPEC-3 on the F2 characterization).
- **`--template-latest` axis** (spec:2033-2041): module-template tag, not ig-template release — plan 10.2 states it correctly.
- **Translation-marker wording** (spec:2046-2049): `machine translation of source page <name> (de)` — plan 8.2 verbatim correct; DE-first inversion of the `gen-page-title-po` invocation (seed `menu-titles-en.txt`, lang `en`, output under `input/translations/en/`) is the correct mirror of SKILL.md:322-328; the `translation-sources` footgun is quoted correctly (SKILL.md:334-335).
- **Branch scheme** (spec:1844-1850), **sibling-skill check** (spec:1767-1833; `/tree/<ref>` vs `@` pin — template `skills/RETIRED.md:41-45` verified), **codes** L1/L2/L3/F2/F3/P1-P5/C5c/R4 all exist with the meanings used (codes.md:61-88), **tier G never identity** (spec:297; provenance.md:54), **§9b CapabilityStatement suggestion incl. `{% lang-fragment %}`** (spec:2279, 2309), **M9 measured >0-keeps + `artifacts.other` placement rows** (spec:1988-2007), **first-run-bootstrap REMOVE list** (first-run-bootstrap.sh:~174: release-please.yml, notify-zulip.yml, release-demo.yml, both JSONs, CHANGELOG.md — matches plan 5.3).

## FINDINGS

### SPEC-1 (MINOR) — the run-of-record verifier command is invalid: `--expected-nonzero` is not a `verify-migration.py` flag

Plan §4 Phase 10.2 writes:

> `verify-migration.py --expected-nonzero --target . --source <pinned-source> …`

MEASURED: `verify-migration.py`'s argparse (lines 3456-3483) defines no `--expected-nonzero`; `parse_args` (line 3484) rejects unknown flags, so the command exits 2 on usage error before checking anything. `--expected-nonzero` belongs to the `migration-log.sh run` wrapper and **requires a WHY argument** (migration-log.sh:433-434: "`--expected-nonzero needs a reason`"); the sanctioned form is SKILL.md:354-358 / 456-457: `bash "$ML" run 11 verify-migration --emits-runlog --expected-nonzero '<reason>' -- python3 …/verify-migration.py …`. The plan knows the wrapper elsewhere (its own bracketed `[11 verify-migration]` row), so this is a transcription defect — but it is the plan's one full verifier invocation.

**Fix:** rewrite 10.2 as the ML-wrapped call with a reason string; keep all the (correct) verifier flags on the python side.

### SPEC-2 (MAJOR) — the plan plans a `publisher` decision the spec has already decided the other way (template ≥ v1.1 chrome exception, spec:343-350)

Plan Phase 2.1 treats `publisher` as the open tier-P/R gap to be "closed with a `decision:` line" at Gate A ("publisher (profiles have none; terminology says 'MII Task Force Consent Umsetzung' vs JSON CS 'Medizininformatik-Initiative' … Gate-A remainder measured to `publisher` alone"), and Gate A in Phase 6.2 lists "publisher (the tier-P gap)". D-5's "keep everything verbatim" reinforces carrying source values.

MEASURED: migration-spec.md:343-350 — "**One deliberate exception (template ≥ v1.1): `publisher` is template CHROME, not module identity.** The template sets `publisher: NUM-DIZ` … **Do NOT carry a source publisher over it**; the module's content identity (artifact copyright labels, prose attribution) is untouched. … under template ≥ v1.1 that carry is reverted (§9a). Update the stale publisher unit in the IG-level `.po` by hand: the title-catalogue generator is non-destructive and preserves the old unit verbatim." The target here is module-template v0.13.2 / ig-template v1.3.4 — well past v1.1; the template scaffold ships `publisher:` NUM-DIZ (template clone sushi-config.yaml:108-114). The provenance history confirms this was learned on the 2026-08-15 Dokument re-migration (provenance.md, 2026-08-15 entry: "§2.2's source-wins rule collided with the ≥ v1.1 publisher chrome … §2.2 now records the publisher exception").

Consequence of the plan as written: it manufactures a Gate-A "publisher" decision for the owners whose outcome, if carried into sushi-config, violates §2.2; and Phase 8 omits the spec-mandated hand-update of the stale publisher `.po` unit. The recovered publisher evidence (TFCU vs MII strings) is Gate-A *content-attribution* evidence only.

**Fix:** in Phase 2.1/6.2 and D-5, replace the "publisher gap → Gate-A decision" item with: `sushi-config publisher` stays the template's NUM-DIZ chrome (spec §2.2 exception, template ≥ v1.1); record the recovered source publisher strings as content-attribution/identity-ledger evidence; add the `.po` publisher-unit hand-update to Phase 8.

### SPEC-3 (MINOR) — the F2 run-of-record finding is mischaracterized as "pin-vs-cache-name", with a remedy that cannot deliver "must not recur"

Plan D-4: "F2 pin-vs-cache-name findings (the run-of-record's `2.0.3-snapshots` vs `2.0.3` DIVERGIERT — provenance.md:102) must not recur: the cache entry name must equal the declared pin." (repeated in R2: "cache name == pin").

MEASURED: F2 is "dependency versions are pinned exactly as the source pinned them" (codes.md:71); the run-of-record finding was **target sushi-config pin `2.0.3-snapshots` against the SOURCE pin `2.0.3`** (provenance.md:94 — the F2 made-real entry; the :102 run-of-record line only counts it) — a target-pin-vs-source-pin divergence, not a pin-vs-cache-name one. The cache entry name already equaled the declared pin on that run (`parent-snapshots.sh … --install` creates exactly `<id>#<version>-snapshots`, SKILL.md:224-226), so the plan's remedy changes nothing. And under ANY §5.1b.5 repin option the F2 divergence recurs **by construction** — spec:1098-1099 instructs "Point the FSH project at the rebuild — `de.einwilligungsmanagement: 2.0.2-snapshots`", which can never equal the source pin. The spec's treatment is a recorded Gate-A carry decision and a triaged DIVERGIERT, not prevention. The one real F2 hygiene point available is different: pin the *source's* parent version (`2.0.2-snapshots`, not `2.0.3-snapshots`, if D-2 = tag 2026.0.0 — spec §2.1.1 source-evidence-wins, spec:1016-1017).

**Fix:** reword D-4/R2: expect and pre-triage the F2 DIVERGIERT on the `-snapshots` repin as the recorded Gate-A carry decision; the guard worth stating is "repin suffixes the SOURCE-pinned version" (2.0.2-snapshots under a 2026.0.0 baseline), and cite provenance.md:94.

### SPEC-4 (MINOR) — the spec-mandated first-run bootstrap run is silently replaced by manual removals

Plan Phase 5.1/5.3 scaffolds from v0.13.2 and applies the removal list "(bootstrap list, first-run-bootstrap.sh:174)" by hand; the plan never runs — or records a decision not to run — the bootstrap itself.

MEASURED: SKILL.md:258-260 — "scaffold from the template checked out in Preconditions 3 **and run its first-run bootstrap**"; identically spec:1435-1437. The template's script is dry-run by default and `--apply` also performs branch setup/protection (first-run-bootstrap.sh:8-20), which is arguably wrong for an in-place migration branch on the MII repo — but that is exactly why the deviation must be *recorded*, not silent: the plan otherwise deviates from an explicit spec step while reproducing only part (b) of its effect (the plan's manual list does match the script's REMOVE line, verified).

**Fix:** add to Phase 5.3: run `first-run-bootstrap.sh` in dry-run to print the authoritative list at the checked-out ref, apply the removals from that output, and record a `decision:` line that `--apply` was not used (branch setup out of scope for a migration branch).

## Verdict

The plan is an unusually faithful rendering of skill v0.25.0 — every ledger row, gate, guardrail, doctrine (no-vendor, manifest re-stamp, page-map contract, harvest contract, derived markers, prepost-delta, generators) is present, correctly named, and correctly ordered; 40+ spot-checked line citations into SKILL.md/migration-spec.md/scripts all resolve to the claimed content. Four defects survive verification: one wrong command line (SPEC-1), one genuinely wrong decision route that contradicts the spec's ≥ v1.1 publisher-chrome exception (SPEC-2, the only MAJOR), one mischaracterized check with an ineffective remedy (SPEC-3), and one silently skipped spec step (SPEC-4). No BLOCKER: nothing in the plan violates the read-only policy, fabricates, or would corrupt identity/canonicals if executed as written.
