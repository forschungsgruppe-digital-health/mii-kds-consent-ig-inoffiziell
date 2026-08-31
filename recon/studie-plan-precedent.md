# Migration plan — MII KDS Modul Forschungsvorhaben/Studie → mii-kds-module-template

**Status: PLAN ONLY — nothing has been executed.** Drafted 2026-08-31 from a five-track recon
(toolkit, source repo, rendered guides, target template, prior migrations), all measured the same day.

| Coordinate | Value |
|---|---|
| Source repo | `medizininformatik-initiative/kerndatensatzmodul-studie`, master @`6cc63c5` (2026-08-31) |
| Source IG | `simplifier.net/guide/miiigmodulstudieen2027ballot` (EN v2027 ballot, live) + in-repo guide trees |
| Migration toolkit | FGDH `agent-skills` **v0.25.0** (@`5c0cc0c`): `mii-ig-migration` (stable) + `fhir-ig-analysis` (Gate-0/verify instrument) |
| Target template | `medizininformatik-initiative/mii-kds-module-template` — **v0.13.2 required** (see D-2) + `ig-template-mii-kds` v1.3.4 by URL |
| Direct precedent | `kerndatensatz-dokument` PR #36 (skill v0.25.0, template v0.13.1, DE-first, draft; decisions owner-closed, awaiting Gate-D / MII-side review) |
| Prior Studie evidence | FGDH sandbox try-run PR #1 (2026-08-19, skill v0.15.1/template v0.11.0, preview live) |

---

## 1. Executive summary

Studie is a **small, clean, well-understood migration**: shape A (SUSHI project), 60 resources
(7 profiles, 14 extensions, 1 logical model, 2 VS, 2 CS, 1 CapabilityStatement,
15 SearchParameters — the measured evidence for keeping the search-parameters page at M9 —
1 IG resource, 17 example instances), SUSHI 0 errors, all profile
parents are core R4 (no snapshot generation), narrative fully in-repo (no guide harvest), a
CapabilityStatement already exists, the bare canonical `…/fhir/modul-studie` passes the template's
M5 check unchanged, and — uniquely among the migrations so far — **human-authored English
translations already exist** (the owner's 2027-EN guide tree), so the DE-first bilingual setup needs
no machine translation and Gate C shrinks to a correspondence review.

The dominant constraint is **not technical but coordination**: the module owner
(Margaux Gatrio / BIH Charité, module lead Matthias Löbe / IMISE, © TMF) merged **eight PRs on
2026-08-31 alone** (#58 plus the narrative wave #59–#65), actively building the 2027-ballot guides
on the *legacy Simplifier toolchain*. There is a three-way version contradiction (tree 2026.0.1 /
registry 2026.0.2 / guides 2027.0.0), no machine-readable licence, and the official Release-2027
wiki lists **two Claude-skill options**: MII's own `mii-ig-publisher-migration` skill
(`mii-kerndatensatz-dev`) and an FGDH sandbox demonstrator (`mii-kds-sample-ig-inoffiziell`) built
with the FGDH toolkit.

**Recommended sequencing (Dokument pattern):** do not race the owner. Contact the owners first
(§3, D-0), let them cut their 2027 ballot RC tag on the legacy path, then migrate **that immutable
tag** in place on an owner-sanctioned branch — exactly how `kerndatensatz-dokument` PR #36 was
produced on 2026-08-30. If owner sanction is not obtained promptly, run a fresh sandbox migration on
the current toolkit (the August sandbox is stale by two toolkit generations) as a demonstrator and
hand the result over.

---

## 2. Measured starting position (evidence-based, 2026-08-31)

### 2.1 Source repo — shape A hybrid, quiet FSH, churning narrative

- **Shape A** (SUSHI/Simplifier hybrid): `sushi-config.yaml` + `input/fsh/` (17 files) + committed
  `fsh-generated/` (60 JSONs) + three Simplifier guide trees at repo root. No `ig.ini` on master
  (one exists only on branch `tech-test-2026-07-23`). ⇒ no goFSH (step 2b skipped), no narrative
  harvest (step 2c skipped — narrative lives in-repo).
- **Conformance content is stable**: since the August try-run pin (`1394b43`) the only conformance
  FSH delta is PR #58 adding `Context: ResearchStudy` to 8 extensions. Additionally, 19ab7b1 moved
  the 3-line SUSHI stub `input/fsh/pagecontent/index.md` → `input/pagecontent/index.md` — it must
  appear in the page-map universe and the Phase 4.2 path-list expectations (superseded by the DE
  tree's `Index.page.md`).
- **Narrative is churning**: the 2026-08-31 wave (PRs #59–#65) created
  `ImplementationGuide-2027.x.x-DE/` (≈ verbatim copy of the 2026 tree; 2 files differ) and
  `ImplementationGuide-2027.x.x-EN/` (full human EN translation; 26 files differ vs DE). Each tree:
  22 pages, 21 images, 5 `toc.yaml`, own `guide.yaml`. Only 2 of the 21 images are referenced by
  the 2027 pages (`UML_Forschungsvorhaben_2026.png`, `Warning.jpg`) plus one remote CC badge — the
  other 19 are orphan candidates; transfer-all vs referenced-only is a page-map decision measured
  at Gate 0.
- **Identity**: canonical `https://www.medizininformatik-initiative.de/fhir/modul-studie` (bare
  space — passes M5, which since template v0.11.2 accepts bare/ext/core; the M5 comment even lists
  studie in the bare-space set); id `mii-ig-studie`; name `MII_IG_Medizinisches_Forschungsvorhaben`;
  packageId `de.medizininformatikinitiative.kerndatensatz.studie`; **no title**, **no license**,
  version 2026.0.1, releaseLabel `ci-build`, `language: de-DE`.
- **Version contradiction (3-way)**: tree = 2026.0.1 everywhere (sushi-config, package.json,
  `rulesets/version.fsh`, `qc/custom.rules.yaml`) · Simplifier registry `latest` = **2026.0.2**
  (+2026.0.2-rc1; no corresponding git commit/tag — package content not reconstructible from git) ·
  both 2027 guide.yaml files = **2027.0.0** ("Version 2027 Ballot - IG"). The 2027 version exists
  ONLY in guide metadata so far — and the contradiction has a **4th member**: the authoritative
  DE-2027 tree's own Index publication table still reads *Version 2026.0.1 / Datum 09.01.2026*
  (byte-identical to the 2026 tree; only the EN tree shows 2027.0.0 with a "x.x.x" date
  placeholder).
- **Licence**: nothing machine-readable (no LICENSE file, no `license:` key, GitHub API
  `license: null`; `rulesets/license-terms.fsh` is a literal `// ToDo` stub). CC-BY-4.0 is
  recoverable only from guide prose (`Index.page.md`: "© 2019+ TMF e. V. … CC BY 4.0", now also on
  the live EN ballot guide). ⇒ `license-align.py` will exit 1 (`license-missing:`) → hard Gate-A
  owner decision (Dokument D-1 analog).
- **Dependencies**: fixed pins only — `kerndatensatz.meta 2026.0.0`, `hl7.fhir.r4.core 4.0.1`, and
  the **old-style `hl7.fhir.extensions.r5: 4.0.1`** pseudo-package (SUSHI warns; materializes as
  `hl7.fhir.uv.xver-r5.r4#0.1.0`). Churn hazard: the owner hand-deleted the xver dependsOn from the
  committed generated IG (19ab7b1), SUSHI regenerates it, and the CI bot has already re-added it on
  the unmerged `translations` branch — the migration must resolve this properly (D-6).
- **Canonical census**: 11 out-of-space canonicals (unchanged since the August pin; the try-run's
  qa-derived mismatch count was 12 — a counting-method difference, no canonical disappeared) — 7×
  deliberate R5-backport
  extension canonicals `http://hl7.org/fhir/5.0/StructureDefinition/extension-…` + 2 CS + 2 VS at
  `http://example.org/…`. All handled via `special-url` in the try-run (qa 42 → 17). Plus
  `example.com` system URIs in instances (link-check fodder, not canonicals).
- **CI**: meta reusable validation workflows adopted (`ci_dotnet_validation` +
  `ci_java_validation @master`), `advisor.json` + `qc/custom.rules.yaml` present, master CI green.
- **QA baseline provenance**: no qa.txt on master. gh-pages carries a full IG Publisher v2.2.11
  build of the **tech-test branch** (2026-07-23): err=783/warn=662/broken=396 — real but built from
  a different toolchain config and a stale commit; **not a usable acceptance baseline**. Spec §9c
  allows build-or-fetch; fetch is ruled out here (the only rendered qa is that stale tech-test
  build), so Gate 0 builds the pinned source — via `hl7fhir/ig-publisher-base` Docker as operator
  practice (local macOS Ruby cannot run Jekyll; the skill itself mandates no Docker).

### 2.2 Rendered guides (Simplifier)

- `miiigmodulstudieen2027ballot` (EN v2027): **live and fully rendered**; publication table shows
  Version 2027.0.0, Status Active, **Date "x.x.x" placeholder**; Release Notes end at v2026.0.1
  (stale for 2027); nav keeps German lead terms on the 8 profile pages ("Dokument
  (DocumentReference)" …). Profile pages embed Simplifier-proprietary widgets
  (`{{tree:…, diff|snapshot}}` treetables, FQL query tables, `{{render:}}`, `{{pagelink:}}`,
  `{{index:root}}`) that have **no IG-Publisher equivalent** — the skill's fql-scan/crosswalk
  handles the re-expression (structure-tabs include etc.).
- `miiigmodulstudiede2027ballot` (DE v2027): key exists but **broken** ("Could not determine guide
  folder") — the DE 2027 content has never been render-validated on Simplifier.
- `miiigmodulstudie2026ballot` (DE v2026): renders fully (the published 2026 guide).
- **Live defects**: 14 files across the two 2027 trees still `{{pagelink:}}`/`{{render:}}` into
  `ImplementationGuide-2026.x.x/…`; at least one pagelink visibly renders "Page not found." in the
  live EN guide. Additionally (outside that census): each tree's `FHIR-Profile/Index.page.md`
  renders `Warning.jpg` from the **foreign** Simplifier project `ImplementationGuide-Common`
  (crosswalk to the tree-local `images/Warning.jpg`), and the Datensatz page's LogicalModel FQL
  query targets the retired ext-space canonical `…/fhir/ext/modul-studie/…/LogicalModel/Studie`
  (the real LM is `…/fhir/modul-studie/StructureDefinition/mii-lm-studie-logicalmodel`). The
  page-map-driven link rewrite + fql-scan crosswalk fix all of these as a side effect.
- One orphan page (`FHIR-Profile/FHIR-Profile.page.md`, in all three trees, not in any toc, live by
  direct URL) → needs a page-map row (likely RETIRED-near-duplicate with reason).
- No published guide versions exist (only `current`; explicit `?version=` URLs 404) → **P4
  exception must be pre-agreed** exactly as in Dokument PR #36 (evidence file `guide-versions.html`).
  Narrative comes from the in-repo trees anyway, so this only affects provenance bookkeeping.

### 2.3 Toolkit and template — versions to pin

- **agent-skills v0.25.0**: procedure = Gate 0 preflight → steps 1–9 with Gates A (identity),
  B (narrative), C (language), D (release/merge; "merging is what publishes" — TF-KDS/AG IOP/NSG).
  31 expected run-log rows; `page-map.tsv` generate-review-consume contract; **no vendored
  template** (keep the ig.ini URL line; delete `ig-template/` + sync machinery; record both
  `5.2 skeleton-vendored ref=` and `5.2 template-reference url=… release=…` rows).
- **Template pin — the M6 gate decides it**: released v0.13.1 **rejects prerelease CalVer**
  (`2027.0.0-ballot.rc1` fails M6). The fix (#25, filed from the Dokument migration) sits
  **unreleased on main @3db9de0**; release-please PR #26 ("release 0.13.2", `autorelease: pending`)
  is open. ⇒ For a ballot-versioned migration: **merge PR #26 and pin v0.13.2** (module-template is
  a tier-1 repo — this is an allowed, ordered action) or pin main @3db9de0. Never v0.13.1.
- **ig-template-mii-kds v1.3.4** = current release = main tip; consumed by URL at build time (the
  sanctioned interim form; passes M7).
- **Skill reference-data staleness**: `template-pages.tsv`/`template-artifacts.tsv` are stamped
  v0.11.1/pkg 1.3.2. Page set verified unchanged at HEAD, but verify-migration downgrades C5c/R4 to
  NICHT PRÜFBAR on the stamp mismatch ⇒ **re-measure both manifests at the pinned template version
  and commit them under `migration-log/`** (sanctioned hand edit; Dokument did exactly this:
  `template-pages-v0.13.1.tsv` + `template-artifacts-v1.3.4.tsv`).
- Toolchain pins (from the template's workflows, drift-gated): IG Publisher 2.3.2 (SHA-256
  `07c5760…`), SUSHI 3.20.1, Jekyll 4.4.1, Node 22, Ruby 3.3, temurin 17.

### 2.4 What is LIGHTER than the Dokument migration

| Concern | Dokument PR #36 | Studie |
|---|---|---|
| Narrative source | in-repo, DE only → EN machine-translated (TODO:REVIEW, heavy Gate C) | in-repo, **DE + human EN trees** → Gate C = correspondence review |
| Scale | 12 page-groups, 38 DERIVED markers, 96/21/17 verify | 22 pages ×2 languages, 60 artefacts (Onkologie for contrast: 155 pages, 583 artefacts) |
| Parents/snapshots | — | all parents core R4 → no `parent-snapshots` |
| CapabilityStatement | present | present (no §9b synthesis; render via `{% lang-fragment %}` — try-run-proven) |
| Canonical space | `/ext/` (needed go-publish env fixes) | bare — scaffold default form, M5-listed |
| Known QA residuals | 12 errors, 4 known classes | try-run: 17 errors, all source-inherent (R5-backport VS bindings, Library example narrative) |

---

## 3. Decision queue (before/at execution — nothing here is the agent's call)

**D-0 · Owner contact & venue (BLOCKING FIRST STEP).** Contact Gatrio (BIH), Löbe (IMISE, lead),
plus the other documented addressees — Alexander Zautke (HL7 Deutschland, technische Umsetzung per
README) and Karoline Buckow (the named TMF contact in the guide Index) — via the channel the
Release-2027 wiki itself says is undecided ("Dezidierter Kommunikationskanal?").
Clarify: (a) explicit GO for an in-place migration branch on the MII repo (Dokument precedent;
MII-org policy otherwise keeps the repo read-only for agents); (b) **which toolkit** — the wiki
links MII's own `mii-ig-publisher-migration` skill *and* the FGDH-toolkit-built sandbox
demonstrator; running FGDH tooling uninvited could read as bypassing MII's choice; (c) whether the
2027 ballot ships on Simplifier first (their visible plan) with the IG-Publisher migration
following the RC tag.
*Fallback if no sanction:* fresh FGDH-sandbox migration on the current toolkit as a demonstrator.

**D-1 · Licence (Gate A, owner).** Confirm CC-BY-4.0 (tier-R evidence: guide prose © TMF, both
languages). `license-align` will exit 1 (`license-missing:`) — the template LICENSE must not
default silently. Dokument's owner confirmed the same question in one day. Ideal outcome: owner
also adds a LICENSE file + `license:` key upstream, killing the F-01-class hazard for good.

**D-2 · Template ref (operator).** Merge module-template release PR #26 → pin **v0.13.2**
(preferred; tier-1 action) or pin main @3db9de0. Required because of D-3's prerelease version.

**D-3 · Source pin + target version (owner + operator).** Recommended: wait for the owners' 2027
ballot RC tag (e.g. `v2027.0.0-ballot.rc1`) and migrate that immutable state — the Dokument
pattern. The migration then carries the version bump coherently (sushi-config, `version.fsh` ×2,
package.json, qc predicate — currently all 2026.0.1). Alternatives: pin master @`6cc63c5` and keep
2026.0.1 (front-runs nothing but contradicts the 2027 narrative), or bump to a 2027 prerelease
without an owner tag (front-runs the owners — not recommended). Also surface the registry-2026.0.2
mystery so the owners can reconcile it: no git tag/commit carries that version string, but
2026.0.2 was published ten minutes after the 2026-02-05 merge `44e01c0` — offer that commit as the
probable content basis.

**D-4 · Language model: DE-first (governance).** KDS-Governance v4.0 §4.4 + meta-wiki
"IG Umbau – DE First" (Dokument precedent: the language-direction decision "D3" in PR #36's
comment of 2026-08-30 — note the PR body's decision-table row "D-3" is a *different* decision):
`i18n-default-lang: de`,
`i18n-lang: [en]`, `translation-sources: [input/translations/en]`. Note this **inverts the
template scaffold and the skill text's stated default** — but the skill itself instructs
verifying the language direction against the target's sushi-config.yaml on every run, so DE-first
is a sanctioned, recorded parameter, not a skill deviation; every step-6 recipe path and the
`gen-page-title-po` language argument mirror en↔de accordingly. Authoritative narrative tree = `ImplementationGuide-2027.x.x-DE`; the human EN tree
fills `input/translations/en/`. The 2026 tree is historical (retire set, D-8).

**D-5 · Publisher & branding (Gate A).** Dokument D-6 analog: IG-level publisher NUM-DIZ (template
default), resource-level publisher stays "Medizininformatik Initiative" (module RuleSet). No
`brand.json` ⇒ NUM-DIZ corporate design (only `{"design":"mii"}` would select MII).

**D-6 · Dependency surface (Gate A).** Replace old-style `hl7.fhir.extensions.r5: 4.0.1` with the
explicit `hl7.fhir.uv.xver-r5.r4: 0.1.0` pin (kills the SUSHI warning AND the owner-vs-bot
dependsOn churn; matches template scaffold + kerndatensatz-basis parity); add template machinery
`hl7.fhir.uv.crmi 2.0.0` + direct pins `hl7.terminology.r4 7.3.0`, `hl7.fhir.uv.extensions.r4 5.3.0`
(Dokument D-4 analog; F2 records them as target-only additions). Keep `kerndatensatz.meta 2026.0.0`
unchanged (F2: source pins win).

**D-7 · example.org canonicals (Gate A, owner).** 2 CS + 2 VS keep their source-authored
`example.org` canonicals via `special-url` (try-run-proven, qa 42→17). Flag to the owners as an
upstream fix candidate — mechanical rewriting is forbidden (canonicals are immutable identity).

**D-8 · Retire-after-Gate-D set (owner).** Dokument D-7 analog: the three
`ImplementationGuide-*` trees, `package-lock.json` stub, legacy release workflow pieces the
template replaces. On merge, the Simplifier "current" guides lose their source — an intended
sunset the owners must consciously accept (their DE-2027 guide is broken on Simplifier anyway).

**D-9 · M9 optional pages (Gate A/B, measured).** Try-run outcome as prior: REMOVE
researcher-guidance / operations / metadata; KEEP extensions / search-parameters / value-sets /
code-systems. Re-measure on the pinned source (counts decide, not preference). M11: delete the
Person illustrative example in both languages.

**D-10 · Formal-publication history (Gate D horizon).** `publication-request.json` ships
`"first": true` — but Studie has a long prior publication history: the registry lists 8 versions
(1.0.0-ballot 2023, 1.0.0 = "2024.0.0" static-HTML era on the MII website, 2025.0.0,
2026.0.0-ballot, 2026.0.0, 2026.0.1, 2026.0.2-rc1, 2026.0.2). Decide with the owners whether the
go-publish history
import (`install-history-template.mjs` + `merge-publication-webroot.mjs`) must reconstruct that
history. Not needed for the migration PR itself; blocks the first formal publication.

---

## 4. Execution plan (maps 1:1 onto skill v0.25.0; run-log rows in brackets)

### Phase 0 — Preparation (human + operator)
0.1 D-0 owner contact; obtain GO + toolkit alignment + ballot-tag timing.
0.2 D-2: merge template release PR #26 → v0.13.2.
0.3 Working clone of the source at the agreed pin (D-3) on branch
    `migration/<source-version>-template-v0.13.2`; SSH remote (workflow-file pushes need it).
0.4 Install/verify toolchain: node 22 (nvm), pinned `fsh-sushi`, python3, Docker with
    `hl7fhir/ig-publisher-base` (for local Jekyll-capable builds), `~/.fhir` cache mount. Run
    `sibling-skill-check.sh` here (the §9c preflight depends on `fhir-ig-analysis`; never
    auto-install). Emit the two always-required preamble rows the L2 oracle checks:
    [`pre.2 classify-source-shape`] (shape=A; evidence: sushi-config.yaml + input/fsh, no ig.ini
    on master) and [`pre.5 toolchain`] (the pins above).

### Phase 1 — Gate 0: measure the unmigrated source [`1 preflight-analysis`, `5.1 source-inventory`]
1.1 `ig-stats.py analyze` on the pinned source → `preflight-analysis.json`: licence tiers,
    special-url prediction (expect ≈11), dependency health (old-style xver flagged), M9 counts,
    QA-baseline status.
1.2 **Build the pinned source** in `ig-publisher-base` (tech-test ig.ini as reference config) →
    the real QA acceptance baseline ("no worse than source" is unprovable without it).
1.3 Multi-guide classification (§5.1a): authoritative = 2027-DE · parallel-language = 2027-EN
    (translation seed) · historical = 2026 (retained until Gate D). Record guide-versions evidence
    for the P4 exception (no published Simplifier versions exist).

### Phase 2 — Identity [`2.1 read-identity`; Gate A]
2.1 Claim every field into `identity-claims.tsv`; expected contradictions: version (3-way, D-3),
    licence (absent, D-1), title (absent → template pattern, try-run wording reusable). All
    resolved only by recorded decisions (`decision: … field=` closes L3).

### Phase 3 — Skeleton [`5.2 skeleton-vendored`, `5.2 template-reference`, `5.2 license-align`, `5.2 sushi-skeleton`]
3.1 Scaffold from template v0.13.2 in place: substitute the 15 active placeholders; **rename the
    three placeholder-NAMED files** (`ImplementationGuide-mii-ig-{{MODULE_SLUG}}.md` ×2 + `.po` →
    `…-mii-ig-studie.*`); census placeholders **by exclusion**.
3.2 Do NOT carry over: `release-please.yml`, `notify-zulip.yml`, `release-demo.yml`,
    `release-please-config.json`, `.release-please-manifest.json`, `CHANGELOG.md` (bootstrap
    REMOVE list). Delete template example artefacts (`example-patient` FSH + instance). Remove the
    template's **M8 demo set** (rendering-artifacts page ×2 languages, its `pages:`/menu entries
    ×2, `demo/`, `gen-rendering-demo.py` + `demo-en.md`/`demo-de.md`/`rendering-demo-codes.json`)
    — release-mode convention check fails otherwise.
3.3 **No-vendor doctrine**: keep `ig.ini` URL line; delete `ig-template/`,
    `sync-ig-template.{yml,sh}`, `resolve-ig-template-source.sh`; record both 5.2 rows
    (`ref=v0.13.2 commit=…` and `url=… release=v1.3.4`).
3.4 **DE-first swap** (D-4): invert i18n params; swap `input/pagecontent/` ↔ DE content; rename
    `input/translations/de/` → `…/en/`; swap menus; invert the IG-level `.po`; patch **three**
    files in the same commit — `scripts/language-model-check.sh` (guards EN-default; hard-fails
    `i18n-lang: en` / `input/translations/en` on every push), the hardcoded `translations/de`
    paths in `scripts/convention-check.mjs` (M9/M10/M11 mirror scans), **and
    `scripts/convention-check.test.mjs`** (the push workflow runs `node --test scripts/*.test.mjs`
    FIRST, and its fixtures assert the very `translations/de` strings being patched) — otherwise
    CI is red from the first push. Rewrite `translationinfo` prose. (Dokument-proven.)
3.5 FSH scaffold collision rule: module's `aliases.fsh` wins; skip colliding template rulesets.
    `license-align.py` runs → exits 1 → D-1 owner decision recorded loudly.
3.6 Merge `advisor.json` / `qc/custom.rules.yaml` / `ignoreWarnings.txt` as union (template rules
    with the module's bare canonical; Dokument commit-2 analog). Acceptance: SUSHI clean.

### Phase 4 — Artefact transfer [`5.3 transfer-artefacts`]
4.1 Copy `input/fsh/` structure-preserving (17 files); IDs/URLs byte-unchanged; D-6 dependency
    edits in `sushi-config.yaml` only. Special-URL list (≈11) into the template's `special-url:`
    parameter block in sushi-config.yaml, regenerated per the template's
    `docs/recipes/regenerate-special-url.md` (try-run list as cross-check — never copy another
    module's list).
4.2 Acceptance: `comm -3` path-list proof — empty apart from logged scaffold additions.
4.3 **Gate A review checkpoint** (after step 4, per the skill's gate table): canonical/ID/licence
    preservation + artefact completeness evidence + every recorded decision (D-1, D-3, D-5–D-7,
    D-9) signed by the module maintainer with TF-KDS.

### Phase 5 — Narrative [`5.4 fql-scan`, `5.4a optional-page-decisions`, `5.4b security-privacy-decision`, `5.4c page-routing`, `5.4d derived-scan`; Gate B]
5.1 `fql-scan.sh --strict` over the source trees → inventory of Simplifier directives
    ({{tree}}, FQL, {{render}}, {{pagelink}}, {{index:root}}) with crosswalk targets
    (structure-tabs include, artefact-page links, GENERATED mapping tables).
5.2 `page-structure-advice.py --map` → `page-map.tsv` over the **union universe** = 2027-DE tree
    ∪ source `input/pagecontent/` (the moved `index.md` stub) ∪ on-disk pages no toc lists (the
    `FHIR-Profile.page.md` orphan); template pages are C5 provenance via `template-pages.tsv`,
    not map rows. Expect ≈22 routed rows + RETIRED rows (empty index stubs, the orphan
    near-duplicate). **Human reviews/edits the map; step 5 consumes only the map** — and
    re-running the advice script OVERWRITES the reviewed map, so after any regeneration re-apply
    and re-review the human edits. Per-profile pages → `input/intro-notes/` (>2-profiles rule);
    Suchparameter sections → search-parameters page (try-run map as prior).
5.3 Transfer DE prose **verbatim** (German is the source language); rewrite internal links from
    the map (fixes the 14 stale cross-tree pagelinks, the foreign-project `Warning.jpg` render,
    and the ext-space LM FQL target as side effects); copy images FLAT into `input/images/`
    (case-sensitivity: one `images/` casing) — 21 per tree, only 2 referenced by the 2027 pages:
    decide transfer-all vs referenced-only in the map and record it.
5.4 EN pages: measure DE↔EN page coverage FIRST, then transfer the owner's human translations
    from the 2027-EN tree into `input/translations/en/pagecontent/` (same filenames as their DE
    twins) with a **per-page provenance line citing the exact 2027-EN source path** (the §5.1a →
    translation-harvest contract). No TODO:REVIEW markers needed *because the tree versions
    match* (both guide.yaml 2027.0.0 — record this evidence; the §5.1a stale-tree caveat is
    inapplicable). Any DE page WITHOUT an EN twin is machine-translated + TODO:REVIEW or an
    explicit recorded fallback decision (R3 flags byte-identical "translations").
5.5 M9 decisions (D-9) + M11 example removal, both languages symmetrically. DERIVED markers
    (§9d box form) only where the migration writes bridging text; `derived-scan` clean.
5.6 Known source-content defects surface as Gate-B findings, never silent fixes: stale Release
    Notes (end at 2026.0.1), the EN Date "x.x.x" placeholder, the **DE-2027 Index publication
    table still reading Version 2026.0.1 / Datum 09.01.2026** (the authoritative tree!), the
    Datensatz FQL querying the retired ext-space LM canonical, `LogicalModel.fsh:100` bare
    `contentReference`, the 2025.0.0 deep-link-to-Organization bug. Queue ② items for the owners.

### Phase 6 — Bilingual wiring [`5.5 gen-page-title-po`; Gate C]
6.1 `gen-page-title-po.py` from the SUSHI-generated IG → `input/translations/en/ImplementationGuide-mii-ig-studie.po`
    seeded with the EN menu titles; German `pages:` titles are the msgids (char-for-char).
6.2 Menu: German `input/includes/menu.xml` + English mirror under `translations/en/includes/`.
6.3 Gate C review = DE↔EN correspondence (owner translations transferred, not produced); flag the
    German-led profile-page nav labels ("Dokument (DocumentReference)") as an owner style choice.

### Phase 7 — Build & QA [`5.6 sushi-build`, `5.6 ig-publisher`, `5.6a sibling-skill-check`, `7 prepost-delta`]
7.1 SUSHI 3.20.1 + IG Publisher 2.3.2 (SHA-pinned) via `ig-publisher-base` locally; tx: template
    default (SU-TermServ cert absent → tx.fhir.org fallback; no SCT-2026 pins in Studie, so the
    Ontoserver detour Dokument needed is likely unnecessary — verify in QA).
7.2 Acceptance: qa errors ⊆ source-inherent classes proven at 1.2 (R5-backport VS bindings ≈15
    refs, Library example empty `<a>`), broken links 0. Expect ≈17-error steady state per try-run.
7.3 `ig-stats` postflight + same-module comparison (source first) → identity/published-set/URLs
    **IDENTISCH** required; `prepost-delta.py` exit 0 (any REGRESSION stops the run).

### Phase 8 — Verification & report [`11 verify-migration`; feeds all gates]
8.1 Re-measure `template-pages.tsv`/`template-artifacts.tsv` at v0.13.2 / ig-template 1.3.4 into
    `migration-log/`, **stamp them with the vendored tag** (pages 3rd column /
    `# template_tag: v0.13.2` header) **and point the verifier at them via
    `--template-pages`/`--template-artifacts`** — the script defaults to the skill's own
    references/ and does not auto-discover `migration-log/` (Dokument PR #36 did all three).
    Reported as a sanctioned edit.
8.2 `verify-migration.py` — expect a non-zero exit initially: 1 while any DIVERGIERT is untriaged
    (licence, manifests), 3 once only NICHT PRÜFBAR rows remain; **neither is a pass**. Triage
    every DIVERGIERT to a decision or fix (Dokument finished 96/21/17 with all 21 triaged); generate
    `qa-checklist.md` + `comparison-table.md`; report from the template, protocol section
    generated from `run.log`.

### Phase 9 — PR & gates [step 9; Gates B/C/D]
9.1 Push branch (SSH); **draft PR** onto the discovered base (`master`), report as description;
    preview via the template's branch preview (`gh-pages/branches/migration/...`). Check the
    repo's Pages state first: branch-mode "Deploy from gh-pages" (template default) suffices; only
    a legacy/Actions-mode repo needs the Dokument three-layer fix (Actions mode +
    `PAGES_ACTIONS_ENABLED=true` + github-pages environment branch policy `migration/**`). Studie's
    Pages root currently 404s (gh-pages holds only the tech-test dir) — expect to enable Pages.
9.2 Gate B (module authors) · Gate C (bilingual reviewer — light) · Gate D (TF-KDS/AG IOP/NSG):
    merge = publish; the agent never merges. D-8 retire set + D-10 history question ride Gate D.
    go-publish stays untouched (dry-run emulation optional, Dokument D-8 analog).

---

## 5. Risks & mitigations

| # | Risk | Mitigation |
|---|---|---|
| R1 | **Owner race**: 8 PRs merged on 2026-08-31; any branch cut today goes stale immediately | D-0 first; migrate the owners' immutable ballot tag (D-3), not master; agree a freeze window for the narrative trees |
| R2 | **Toolkit-choice friction**: Release-2027 wiki names MII's own migration skill | D-0 names it explicitly; offer the FGDH run as the Dokument-pattern continuation; both PRs (#36, Onkologie #311) still await ANY owner review — treat as unvalidated expectation |
| R3 | Version ambiguity (2026.0.1 / 2026.0.2 / 2027.0.0) | D-3: one pinned version by owner tag; surface the registry-2026.0.2 gap; M6 needs template ≥ v0.13.2 for prerelease suffixes |
| R4 | Silent relicensing (no machine-readable licence) | license-align exits 1 by design; D-1 owner confirmation before LICENSE is written; push for an upstream LICENSE file |
| R5 | DE-first breaks template CI (language-model-check + hardcoded de-paths + their test fixtures) | Patch all three files in the skeleton commit (Phase 3.4); Dokument-proven |
| R6 | Source-inherent QA errors misread as migration defects | Gate-0 source build = provable baseline; special-url list; triage table pre-seeded from try-run |
| R7 | xver dependsOn churn (owner deletes, bot restores) | D-6 replaces the old-style dep explicitly; owner signs it at Gate A |
| R8 | Verifier noise (C5c/R4 manifest staleness; C4 URL-stripping limitation) | Re-measure manifests (8.1); reuse Dokument's checker-limitation adjudications where they apply |
| R9 | URL-form template reference is unpinned (fetches ig-template main at build time) | Record `release=v1.3.4`; rebuild+re-record if ig-template releases mid-run; endgame = registry package (module-template #1/#2 + ig-template #5/#6, all open) |
| R10 | Broken DE-2027 Simplifier guide masks content errors (never render-validated) | The migration build itself validates the DE tree; report render findings upstream as a courtesy |

---

## 6. Effort & scale estimate

Comparable to or smaller than Dokument (which went source-pin → draft PR in ~1 day of agent time
plus owner-decision latency): 60 artefacts, 22 pages ×2 languages with human EN translations
already present, no goFSH/harvest/snapshots, canonical/M5 clean, decision queue front-loaded
(D-0…D-10). Critical path = **owner responses** (GO, licence, ballot tag), not the mechanics.

## 7. What this plan deliberately does NOT do

- No migration step is executed; no branch, no fork, no issue/comment on any MII repo (org policy:
  MII repos outside the two template repos are read-only for agents; D-0 changes that only for
  this migration and only with explicit owner sanction).
- No version bump, licence write, or dependency change happens before the corresponding decision
  (D-1/D-3/D-6) is recorded with its owner.
- The 2026 guide tree and the live Simplifier guides stay untouched until Gate D's retire set.
