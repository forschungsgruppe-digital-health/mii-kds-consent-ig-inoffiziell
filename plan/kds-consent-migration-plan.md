# Migration plan — MII KDS Modul Consent → mii-kds-module-template

**Status: PLAN ONLY — NOTHING HAS BEEN EXECUTED.** The user explicitly forbade executing this
migration; this document is a decision input. Drafted 2026-08-31 from a five-track recon
(skills toolkit, source repo, rendered guide, target template, ecosystem/ownership context), all
measured the same day. Evidence citations are `recon/<report>.md` plus the underlying file:line
or URL/command each report records. **Revised 2026-08-31 (same day)** after an independent
verification pass: 13 findings applied (fact corrections: link census 160, issue count 40/44,
wiki names the sample-IG repo; spec conformance: verifier invocation via the run-log wrapper,
publisher = NUM-DIZ template chrome, F2 repin semantics, bootstrap dry-run; new risk cover:
in-place access mechanics, evidence persistence + early harvest as Phase 0.0, D-14 registry-only
example, committed QA-baseline method, mirror-update semantics, risk-id/check-code
disambiguation). Verification reports: `verify/verify-fact.md`, `verify/spec-lane-verification.md`,
`verify/risk-lane-findings.md`.

| Coordinate | Value | Evidence |
|---|---|---|
| Source repo | `medizininformatik-initiative/kerndatensatzmodul-consent`, `master` HEAD `792f9f3e` **== tag `2026.0.0`** (`git diff --stat` empty); `develop` 18 commits ahead (last push 2026-08-21, Bialke) | recon/source.md §0 |
| Source IG | `https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0` — 18 pages, all HTTP 200, German-only, the ONLY guide version on Simplifier | recon/guide.md §a/§b |
| Package | `de.medizininformatikinitiative.kerndatensatz.consent`, dist-tags.latest `2026.0.0`; registry additionally holds `2026.0.1-rc-1…rc-4` | recon/source.md §h |
| Migration toolkit | FGDH `agent-skills` **v0.25.0** (tag `5c0cc0c3`, `version.txt`=0.25.0): `mii-ig-migration` (stable) + required sibling `fhir-ig-analysis` | recon/skills.md header, CATALOG.md:13-17 |
| Target template | `mii-kds-module-template` **v0.13.2** (released TODAY 2026-08-31T15:03Z, M6 prerelease fix) + `ig-template-mii-kds` **v1.3.4** by URL | recon/template.md §a/§e |
| Direct precedents | `kerndatensatz-dokument` PR #36 (OPEN, DE-first, owner-interacting — the in-place pattern); Studie plan (same day, plan-only); FGDH sandbox `mii-kds-consent-ig-inoffiziell` PR #3 (2026-08-06, stale) | recon/context.md §c/§f |

---

## 1. Executive summary (headline verdict)

**Recommended route: D-0 owner contact first; on GO, migrate IN PLACE on the MII repo (Dokument
PR #36 pattern). Until/without GO: a FRESH run in the EXISTING FGDH sandbox repo
`mii-kds-consent-ig-inoffiziell` on a new branch — never a continuation of its stale
2026-08-06 branch.** The existing sandbox is evidence-only: template v0.6.0 vendored vs v0.13.2,
EN-primary vs the wiki's DE-first mandate, source base 3 commits behind `develop`, skill
~v0.12/0.13-era vs v0.25.0 which removed template vendoring entirely (recon/context.md §c,
migration-report.md:6,30,500 + agent-skills CHANGELOG.md:3-8). Its `migration-log/`
(identity-claims, D1–D8 decisions, harvest TSVs, parent-snapshot measurements) carries over as
decision input; nothing else does.

**Effort relative to the precedents: mechanically the HEAVIEST of the three, but the smallest in
scale.** Consent exercises nearly every conditional path of skill v0.25.0 — it is the skill's own
measured reference case for shape B, the guide harvest, and parent snapshots (recon/skills.md §b:
migration-spec.md:536-542, 1405-1412; provenance.md:54-56). Unlike Studie (shape A, in-repo
narrative, human EN translations, no snapshots), Consent needs goFSH derivation (measured
41→5→0 SUSHI errors), an 18-page Simplifier harvest (the narrative exists NOWHERE in git —
recon/guide.md §e), parent-snapshot generation for `de.einwilligungsmanagement` (21 SDs, 0
snapshots in both 2.0.2 and 2.0.3 — migration-spec.md:1009-1020), machine translation of 14
German pages to EN under DE-first, and a ~160-link external rewrite surface (census sum 160 —
recon/guide.md §g.5). Countervailing:
only 14 conformance resources + 5 examples, 2-package dependency surface, master==tag baseline,
bare canonical drops into the template unchanged. Estimate: ~1.5–2 agent-days of mechanics plus
owner-decision latency (Dokument went source-pin → draft PR in ~1 day at lower mechanical load).

**Critical path: (1) D-0 owner contact** — unlike Studie there is NO owner momentum to attach to
(zero 2027 branches/guides/packages; `gh api search` for 2027/ballot = 0 hits — recon/source.md
§g, recon/context.md §d), so the GO, the toolkit choice, and the baseline decision carry more
project risk than any technical step; **(2) the parent-snapshot CI answer** — the sandbox proved
a local `-snapshots` cache pin does NOT resolve in CI ("CI preview is disabled for this branch",
sandbox migration-report.md D4 — recon/context.md §c); one of the four §5.1b.5 carry-upstream
options must be picked at Gate A before any CI-verified preview exists.

---

## 2. Measured starting position

### 2.1 Source repo — shape B, raw XML, identity only registry-side

- **Shape B** (raw FHIR resource repository, no scaffolding): 32 files; no FSH, no
  `sushi-config.yaml`, no `ig.ini`, no `input/`, no ImplementationGuide resource, no `.github/`
  at all (recon/source.md §a). 14 conformance resources (3 profiles + 6 SearchParameters +
  3 CS [2 XML + 1 JSON] + 3 VS) + 5 XML examples across five German-named dirs — exactly the
  file set the skill measured its shape-B path on (migration-spec.md:536-542). Third-bucket
  narrative-bearing text files needing a recorded disposition: the 43-line German `README.md`
  (whose own guide link is DEAD, 404 — recon/source.md §h) and
  `terminologie/codesystems/CodeSystem-MiiConsentPolicy.md`, a hand-synced markdown mirror of
  the Policy CS with columns ("Gültigkeit" 5/30/EINMALIG) NOT representable in the CS
  (recon/source.md §i.3) — a parallel source, not a rendering.
- **Identity exists only registry-side**: packageId `de.medizininformatikinitiative.kerndatensatz.consent`
  from the 2026.0.0 tarball; the repo deliberately holds no manifest (stale `package.json`
  deleted 2025-06-13, commit `07e826d`; `.gitignore` ignores `fhirpkg.lock.json`) — recon/source.md
  §a/§b. Tier-P/R identity reads (`package-identity.sh`, `repo-identity.sh`) are therefore
  REQUIRED expected-steps rows (expected-steps.tsv: "no sushi-config.yaml in the source").
- **Canonical space = the BARE MII space** `https://www.medizininformatik-initiative.de/fhir/modul-consent`
  (`Profile_MII_Consent_Einwilligung.xml:4`; unanimous 13/13 per the skill's own measurement,
  migration-spec.md:133-174; wiki Namenskonventionen line 17 agrees — recon/context.md §a).
  Template fit: M5 accepts bare since v0.11.2 (convention-check.mjs:175-190) and
  `go-publish.yml:102` EXPECTED_CANONICAL is already templated to the bare space —
  `MODULE_SLUG=consent` drops in with NO manual canonical edits (recon/template.md §b). MEASURED
  simulation on the v0.13.2 clone with Consent values: **M1–M7 all PASS in release mode** for
  both `2026.0.0` and `2027.0.0-ballot.rc1` (recon/template.md §b).
- **Out-of-space canonicals — 2 of 14**: both XML CodeSystems use `urn:oid:` urls
  (`2.16.840.1.113883.3.1937.777.24.5.2` Answer, `…5.3` Policy —
  `CodeSystem-MiiConsentPolicyCodeSystem.xml:6`), referenced from in-space ValueSets via
  `urn:oid` system (recon/source.md §e) → `special-url` entries, never rewrites.
- **id↔url mismatch on EVERY id-bearing resource**: profiles carry random UUID ids
  (`e0e166b4-…` vs slug `mii-pr-consent-einwilligung`, Profile_MII_Consent_Einwilligung.xml:3-4),
  XML CS/VS carry ART-DECOR `OID--timestamp` ids, all 6 SearchParameters have NO id element,
  only the JSON CS id matches its slug (recon/source.md §e). Guardrail: canonicals/IDs are never
  changed by the migration; goFSH-minted ids for the id-less SPs are a ② Gate-A review item
  (SKILL.md:399-424; gate table).
- **Dangling canonical on the release**: 3 examples reference
  `…/CodeSystem/mii-cs-consent-consent_category` (Example_MII_Consent_Einwilligung.xml:40) which
  is defined NOWHERE in repo or package; the fix exists only on unreleased `develop` (2026-03-19
  commits) — recon/source.md §e. A faithful 2026.0.0 migration reproduces this validation error
  (D-9).
- **Version/registry drift**: registry holds 19 versions incl. registry-only `2025.0.4` and
  `2026.0.1-rc-1…rc-4` (rc-4 = "resync from github branch develop"); rc-4 bumps parent
  `de.einwilligungsmanagement` 2.0.2→2.0.3 AND drops `ImplementationGuide.json` +
  `CodeSystem-MiiConsentVersionModuleCodeSystem.json` from the package vs 2026.0.0; the 2026.0.0
  package ships a 6th example (`Example_MII_Consent_Einwilligung_1.json`) with no XML source in
  git (recon/source.md §h) — disposition decided at D-14, NOT silently dropped. Per-resource versions diverge (1.0.9/1.0.8/1.0.7/1.6.0/1.1.0/0.2.0-draft);
  package version 2026.0.0 exists only on Simplifier (recon/source.md §b). `develop` moved
  2026-08-21 in exactly the `Consent.category` slice area (issue #124 active same day) —
  re-measure the release fingerprint at execution time; do not reuse the sandbox's rc-4 finding
  (recon/context.md §e).
- **Dependencies (published tarball only)**: `hl7.fhir.r4.core 4.0.1` +
  `de.einwilligungsmanagement 2.0.2` (2.0.3 in rc-4). NO basisprofil, no xver/r5-extensions, no
  CRMI, no terminology package (recon/source.md §d).
- **Licence — "file-only CC-BY" CONFIRMED precisely**: `LICENSE` = full CC-BY-4.0 legal code
  (18,658 B, whitespace variant of the creativecommons.org text; GitHub API spdx `CC-BY-4.0`);
  NO `license` field in the published package.json or IG resource; per-resource copyright only
  in `CodeSystem-MiiConsentVersionModuleCodeSystem.json:48` (TMF e.V.) — recon/source.md §c.
  The guide root page states CC BY 4.0 / "© 2019+ TMF e. V." (recon/guide.md §d) — file and
  guide agree; the gap is machine-readable metadata (D-1).
- **QA baseline: none exists** — no qa.txt/html, no CI, no workflows ever; issues #64/#66/#107
  confirm (recon/source.md §f). Gate 0 must build the source baseline itself.
- **People**: Sebastian Stäubert (IMISE Leipzig; 52/98 commits, merged 7 of last 8 PRs, 40 of 44
  open issues — re-measured live 2026-08-31: `gh api search/issues` total_count 44, author
  breakdown 40× SebStaeubert; supersedes recon/context.md §d's stale 30/31 and agrees with
  recon/source.md §g's 44) = primary contact; Martin Bialke (merged release PR #104, authored the last
  develop push; THS Greifswald — INFERENCE from wiki co-publications) = secondary; governance =
  TF Consent Umsetzung (recon/context.md §d). The maintainers already WANT the target shape:
  open issues #36 (FSH), #63 (github statt simplifier), #64/#66 (CI), #101 (JSON unify), #97
  (Policy-CS name) — recon/source.md §g.

### 2.2 Rendered guide (Simplifier) — the single narrative source

- **Exactly 18 addressable pages** (1 root + 3 folder nodes + 14 markdown leaves: 12 `.guide.md`
  + 2 `.page.md`), all fetched HTTP 200; tree from the server-rendered treetable + the IG
  resource, in agreement (recon/guide.md §a). This is the complete harvest universe — and the
  skill has already measured this exact harvest at 18/18/0 (migration-spec.md:1405-1412).
- **Only ONE guide version exists**: 2026.0.0 = default/current (version-less URL
  byte-identical; probes for 2025.x/2026.0.1(-rc)/2027/ballot all 404) — recon/guide.md §b. The
  guide is pinnable to a published version → P4 satisfiable (no Studie-style P4 exception needed).
- **German-only; no EN twin anywhere** (probes + web search; the repo even carries an unused EN
  figure while the guide embeds only the DE one) — recon/guide.md §c. Under DE-first this means
  14 pages of machine-translated EN defaults... inverted: DE default pages verbatim, EN
  translations machine-produced + `TODO:REVIEW`, reviewed at Gate C (see D-3).
- **Status contradiction**: index table `Status: active` vs the IG resource `status: draft`
  (recon/guide.md §g.1) → D-6.
- **4 pages embed rendered conformance resources** (Consent 891 KB, Provenance 188 KB,
  DocumentReference 188 KB, Terminologien 73 KB), classified `artefact-view` by the harvest; the
  renders resolve from project files matching the git layout (recon/guide.md §e). The Consent
  page additionally carries extensive hand-written German sections (Suchparameter, Widerruf
  semantics, komplexe Suchbeispiele) that must survive as narrative.
- **Link-rewrite inventory (census)**: hl7.org 66 (13 plain http), **ig.fhir.de 34**
  (Einwilligungsmanagement IG — the dominant dependency), medizininformatik-initiative.de 26,
  art-decor.org 11 (2 plain http; one RetrieveValueSet service URL with pinned
  `effectiveDate=2021-04-23`), simplifier.net 5 (2 cross-guide `?version=current`), github.com 4,
  ths-greifswald.de 4, plus IHE/BfArM/IOS-Press deep links (recon/guide.md §g.5).
- **Assets to re-host**: 2 content images hot-linked from GitHub **master** (raw.githubusercontent
  `MII-KDS_de_Consent.jpg`; `…UML-Diagramm….png?raw=true` — both track master, not the release
  tag), the MII logo from medizininformatik-initiative.de, the CC-BY button from
  licensebuttons.net, and the guide's custom `MIICustomIGStyle/style.css` (recon/guide.md §g.4/g.11).
  Both content images exist in the repo's `figures/` → copy into `input/images/`.
- **Terminology not self-contained**: the Terminologien page states the ART-DECOR answer-option
  ValueSets "werden zeitnah durch die TFCU in diesem IG eingepflegt" — the migrated IG inherits
  this gap verbatim (Gate-B finding, never a silent fix) — recon/guide.md §g.6.
- **Guides do vanish**: the 2023 predecessor guide (key `IGMIIKDSModulConsent`) was DELETED from
  Simplifier and survives only as a static MII-website mirror (recon/guide.md §b) — the harvest
  is also a preservation act.
- Serial-nr gaps in the tree (9,10,16,20,23,25,29) suggest hidden/deleted nodes — NICHT PRÜFBAR
  anonymously (recon/guide.md §a); the IG resource lists exactly 18 nodes.

### 2.3 Toolkit + template — versions to pin, and the one known compat gap

- **agent-skills v0.25.0**: procedure = 5 preconditions (pre.1 two human URLs, pre.2 shape,
  pre.3 target state, pre.4 placeholder census by exclusion, pre.5 pinned-npx toolchain
  `fsh-sushi@3.20.0` + `gofsh@2.6.1`) + steps 1,2,2b,2c,3–9 with Gates 0/A/B/C/D; 31
  expected-steps ledger rows; page-map generate–review–consume contract; **no vendored template**
  (the v0.25.0 release IS that decision — CHANGELOG.md:3-8; keep the `ig.ini` URL line, delete
  `ig-template/` + sync machinery, record `5.2 skeleton-vendored ref=` AND
  `5.2 template-reference url=… release=` — migration-spec.md:1442-1453) — recon/skills.md §a/§g.
- **Template v0.13.2**: the M6 prerelease gate the Studie plan waited on is FIXED and RELEASED
  (regex `^\d{4}\.\d+\.\d+(-[0-9A-Za-z.-]+)?$` at convention-check.mjs:194; delta v0.13.1→v0.13.2
  = 4 files) — recon/template.md §a. No hard template-level blocker for Consent.
- **Manifest-currency gap (guaranteed tripwire)**: the skill's `template-pages.tsv` /
  `template-artifacts.tsv` are stamped module-template **v0.11.1** / ig-template pkg 1.3.2
  (measured 2026-08-20) — against a v0.13.2 scaffold, C5c and R4 downgrade to NICHT PRÜFBAR
  (`manifest_stale`, verify-migration.py:1034-1046). MEASURED mitigation basis: `gh api compare
  v0.11.1...v0.13.2` = 62 files, ZERO under `input/`, sushi-config untouched — the page set is
  byte-identical, so re-stamping is safe (recon/template.md §g; recon/skills.md §f). Plan:
  re-measure both manifests at v0.13.2/v1.3.4 into `migration-log/` and pass them via
  `--template-pages`/`--template-artifacts` (the Dokument pattern; the Studie plan's Phase 8.1
  is reusable verbatim).
- **Toolchain pins** (template workflows, drift-gated by `toolchain-pins.test.mjs`): IG Publisher
  2.3.2 (SHA-256 `07c57602…`), SUSHI 3.20.1, Jekyll 4.4.1, Ruby 3.3, temurin 17; the Jekyll gem
  SHA in `go-publish.yml:114` is watched by NO test (recon/template.md §d).
- **Parent-snapshot toolchain**: java + pinned `validator_cli.jar` (~187 MB; spec example pins
  6.10.0) fetched only when detected (SKILL.md pre.5; migration-spec.md:997-1120).
- **`--template-latest` axis trap**: it must be the module-template repo tag (P2), never the
  ig-template release (P1) — migration-spec.md:2033-2041 (recon/skills.md §f).

### 2.4 Weight class vs the precedents

| Concern | Dokument PR #36 | Studie (plan) | **Consent** |
|---|---|---|---|
| Shape | A (in-repo narrative) | A (SUSHI project) | **B — goFSH derivation, 41→5→0 measured** (migration-spec.md:953,1099-1104) |
| Narrative source | in-repo DE | in-repo DE + human EN trees | **Simplifier ONLY — 18-page harvest mandatory** (recon/guide.md §e) |
| Parent snapshots | — | — (all core R4) | **`de.einwilligungsmanagement` 21 SDs / 0 snapshots; Gate-A carry decision + CI answer** |
| Gate C load | machine-EN review | correspondence review | **14 machine-translated EN pages (no EN source exists)** |
| Scale | 12 page-groups | 60 artefacts, 22 pages ×2 | **14 conformance + 5 examples, 18 pages — smallest** |
| Canonical | `/ext/` (env fixes) | bare | **bare — zero manual edits** (recon/template.md §b) |
| CapabilityStatement | present | present | **absent → §9b SUGGESTED synthesis, ① queue** (recon/source.md §e: count 0) |
| Baseline ambiguity | owner tag | 3-way version contradiction | **master==tag clean; but develop/rc line already diverged** (D-2) |
| Owner momentum | active, responsive | 8 PRs same day | **none on 2027 — D-0 carries the risk** (recon/context.md §d) |

---

## 3. Decision queue (nothing here is the agent's call)

Per skill doctrine each decision carries: question · who decides · recommendation + rationale ·
what blocks on it. "Owner" = Stäubert/Bialke/TF Consent Umsetzung; "user" = Marcel (operator);
"agent" = execution-time measurement, never judgement.

**D-0 · Owner contact: GO + venue + toolkit + baseline/version timing (BLOCKING FIRST STEP).**
*Question:* (a) explicit GO for a migration and its venue (in-place branch on the MII repo vs the
FGDH sandbox demonstrator); (b) which toolkit — the Release-2027 wiki names BOTH MII's own
`mii-ig-publisher-migration` skill and the FGDH toolkit's **sample-IG reference migration
`mii-kds-sample-ig-inoffiziell`** (wiki Release-2027.md:6-7 — NOT the Consent sandbox
`mii-kds-consent-ig-inoffiziell` used in D-0(a)/Phase 0.2/RISK-1; the wiki nowhere mentions the
Consent sandbox); (c) which source state is migrated and what the target version is
(see D-2); (d) the 2027 ballot schedule, which is NICHT PRÜFBAR from the wiki (recon/context.md §a);
(e) **in-place access mechanics** — HOW the migration branch physically lands on the MII repo:
collaborator write grant to the operator, an owner-pushed branch, or a sanctioned fork-PR
(consent-repo push rights are NICHT PRÜFBAR — recon/context.md §f proves only the Dokument-repo
interaction model, and access is per-repo), plus the in-place venue-enablement state: the repo has
NO `.github/` at all (recon/source.md §a), so Actions/Pages enablement, workflow-file push
transport (SSH — HTTPS tokens fail on workflow files, MEMORY: agent-skills dry run), and branch
protection on the PR base are all unknowns to settle with the owner.
*Who:* owner (Stäubert primary, cc Bialke, TF CU; TMF contact Buckow per the guide Impressum —
recon/guide.md §d).
*Recommendation:* FGDH `mii-ig-migration` v0.25.0 — the MII skill is a one-commit (2026-04-28)
prose doc mandating EN-primary and a floating `fhir2.base.template#current` pin, both
contradicting current DE-first + pinned practice (recon/context.md §b); the Dokument PR #36
precedent shows the FGDH toolkit already runs inside the MII org, DE-first, owner-interacting.
Lead with the owners' own open issues (#36 FSH, #63 github-first, #64/#66 CI) — the migration
IS their backlog.
*Blocks:* everything. Without GO, only the sandbox route proceeds (and any PR against the MII
repo stays out of bounds — this engagement is read-only on both orgs). **Owner GO alone does NOT
create push access**: in-place execution additionally requires the user (Marcel) to explicitly
re-authorize agent writes on `kerndatensatzmodul-consent`, lifting the standing MII read-only
agent policy for this one repo (MEMORY: MII org access policy — all MII repos read-only except
the two template repos); until both the owner mechanics (e) and that re-authorization exist, the
in-place route cannot start.

**D-1 · Licence metadata (Gate A).**
*Question:* the source is file-only CC-BY (LICENSE file present and byte-exact CC-BY-4.0; NO
machine-readable `license` field anywhere — recon/source.md §c). `license-align.py` row 1 copies
the source LICENSE byte-faithfully (exit 0 expected — license-align.py:19-34). But the template
scaffold's `license:` key in sushi-config.yaml ADDS machine-readable licence metadata that never
existed in any published artefact — silently changing published metadata (the F-01
silent-relicensing class from the KDS-Dokument dry run, here in mild form because file and guide
prose agree on CC-BY-4.0).
*Who:* owner confirms; agent never defaults it.
*Recommendation:* set `license: CC-BY-4.0` with the owner's explicit sign-off recorded at Gate A;
tier evidence (file + GitHub spdx + guide prose + TMF copyright) is unanimous, so this should be
a one-line confirmation. Verifier F3 then has full tier evidence.
*Blocks:* Gate A sign-off; the migration report's FIX row.

**D-2 · Source baseline + target version (Gate A; owner + user).**
*Question:* migrate tag `2026.0.0` (== master, immutable, matches dist-tags.latest and the only
guide version) or the `develop`/rc line (18 commits ahead, parent pin 2.0.3, category-slice churn
under active issue #124, package-content changes incl. dropped IG resource + VersionModules CS —
recon/source.md §0/§h)? And which target `version` — the skill's only human identity decision
(migration-spec.md:32-34)?
*Recommendation:* migrate **tag 2026.0.0** with target version `2026.0.0` unless the owners say
a 2026.0.1 final is imminent — the release is the only state where git tag, registry latest, and
guide version AGREE; the rc line is a moving, never-finalized target. Surface the drift table
(rc-4 content diffs, the registry-only 2025.0.4) to the owners as evidence, and offer the
alternative: owners cut 2026.0.1 first, migration follows the new tag (the Dokument pattern).
*Blocks:* Phase 0 pinning; the F2 dependency-pin expectations (2.0.2 vs 2.0.3, see D-4); D-9.

**D-3 · Language direction: DE-first (governance; owner-confirmed).**
*Question:* the wiki mandates "IG Umbau - DE First" (Release-2027.md:9); the skill hard-codes
EN-default and treats a German-only source as machine-translated-EN-default input
(migration-spec.md:396-402); the source guide is German-only (recon/guide.md §c).
*Recommendation:* **DE-first** (`i18n-default-lang: de`), the Dokument PR #36 owner-confirmed
precedent. This is a conscious deviation from skill spec §1/§4.2 — record it as a decision line;
the skill's own instruction is to verify the direction against the target's sushi-config on
every run (SKILL.md:85-87). Consequence 1: the **3-file one-commit CI patch** is mandatory and
OUTSIDE the skill (measured absence — recon/skills.md §i): `scripts/language-model-check.sh`
(pattern :46 `input/translations/en` fires on DE-first config alone), the ~10 hardcoded de-paths
in `scripts/convention-check.mjs` (:235,:238,:271,:309,:361,:385,:424,:427,:435,:437), and
`scripts/convention-check.test.mjs` (:211,:214,:239,:289) — one commit, because
`convention-check.yml` runs `node --test scripts/*.test.mjs` FIRST (:70-71) — recon/template.md §c.
Consequence 2: the 14 German pages become verbatim DE defaults; the EN translations are
machine-produced + `TODO:REVIEW`, reviewed at Gate C.
*Blocks:* Phase 3 skeleton commit; Gate C staffing.

**D-4 · Parent-snapshot carry option (Gate A — "where a migration can quietly break CI").**
*Question:* `de.einwilligungsmanagement` ships 21 StructureDefinitions and 0 snapshots in BOTH
2.0.2 and 2.0.3 (migration-spec.md:1009-1020); SUSHI cannot import 3 profiles without generated
snapshots; the sandbox's local `2.0.3-snapshots` cache pin did NOT resolve in CI (sandbox
migration-report.md D4 — recon/context.md §c). Four §5.1b.5 options: CI prebuild step / vendored
rebuilt parent / internal registry / not repinning (migration-spec.md:1106-1116).
*Who:* user picks the mechanism; owner informed (and the upstream defect — 3 refused
differentials on 2.0.2, 21/21 generating on 2.0.3 per the sandbox — is escalated to the PARENT's
maintainers, never patched; spec §5.1b.5/§12.2).
*Recommendation:* **CI prebuild step** — a workflow step that runs the pinned
`validator_cli.jar snapshot` against the parent before the publisher, committing nothing — the
only option that keeps clean checkouts working without republishing someone else's package. Note
the interaction with D-2: on 2.0.2 the official generator refused 3 of 21 (none blocking
Consent); on 2.0.3 all 21 generate (recon/context.md §c) — if the owners choose the rc/develop
baseline, the parent pin moves to 2.0.3 and the snapshot story improves. F2 semantics under any
§5.1b.5 repin: F2 compares the TARGET pin against the SOURCE pin (codes.md:71), so a
`-snapshots` repin produces an F2 DIVERGIERT **by construction** (run of record: target
`2.0.3-snapshots` vs source pin `2.0.3` — provenance.md:94); expect it and pre-triage it as the
recorded Gate-A carry decision, never as a defect to "fix". The actionable guard is different:
the repin must suffix the SOURCE-pinned parent version — `2.0.2-snapshots` under a 2026.0.0
baseline (the source pins 2.0.2, not dist-tags' 2.0.3 — migration-spec.md:1016-1017,1098-1099).
*Blocks:* any CI preview/build (Phase 7); Gate D (no CI-green preview → no publishable evidence).

**D-5 · Canonical/id policy: keep everything verbatim (Gate A ratification).**
*Question:* UUID/ART-DECOR ids on 9 resources, id-less SearchParameters, 2 `urn:oid` CS
canonicals, name-with-spaces `MII CS Consent Policy` (issue #97) — the template's conventions
(id==slug, clean names) cannot be met without a breaking canonical/id migration.
*Who:* owner (it is an upstream-content decision, not a migration step).
*Recommendation:* **keep verbatim** — guardrail: the migration never changes canonicals or ids
(SKILL.md:399-424). The 2 `urn:oid` canonicals go into `special-url:`; goFSH-minted ids for the
6 id-less SPs are listed as a ② Gate-A review item; the id/name modernization is flagged to the
owners as a FUTURE upstream release (their issues #97/#101 already point there), never done
in-flight.
*Blocks:* Gate A sign-off checklist.

**D-6 · IG status: active vs draft.**
*Question:* the guide index table says `active`, the ImplementationGuide resource says `draft`
(recon/guide.md §g.1).
*Who:* owner. *Recommendation:* `active` (the index table is what the release communicates; the
IG resource is a Simplifier skeleton with nulls — recon/source.md §a). Recorded as an
`identity-contradiction:` closed by a `decision:` line (L3).
*Blocks:* sushi-config `status:`; verifier L3.

**D-7 · Authoritative guide slug.**
*Question:* two live guides resolve (pinned `miiigmodulconsent/MIIIGModulConsent?version=2026.0.0`
and `mii-ig-modul-consent-2026`, both 200; the packaged IG skeleton points at the latter;
README's own link is dead) — which is the harvest/P4 anchor? (recon/source.md §h; sandbox
`simplifier-guides.tsv` knew three keys — recon/context.md §e.)
*Who:* owner confirms; agent proposes.
*Recommendation:* `miiigmodulconsent` @ 2026.0.0 — it is version-pinned, server-rendered,
measured 18/18 harvestable, and is the key the skill's own reference run used
(migration-spec.md:1405-1412). Ask the owners whether the two keys are the same guide under
old/new slug (NICHT PRÜFBAR anonymously).
*Blocks:* pre.1 human input; 5.1d harvest; P4.

**D-8 · Harvest route ①-vs-②: authenticated project download.**
*Question:* route ① (authenticated Simplifier project download — the author's own markdown,
most trustworthy) needs a human with project credentials downloading in their own browser
(never a credential mechanism — migration-spec.md:1328-1355); route ② is the verified anonymous
`guide-harvest.sh` rendering. The two `.page.md` files (Release Notes, Empfehlungen) live only
in the project file store (recon/guide.md §e) — route ① would recover their true source.
*Who:* owner (or any project member: Stäubert/Lang/Bialke/Zautke are admins — recon/guide.md §f)
opt-in; user asks at D-0.
*Recommendation:* ask for the project download at D-0 (one browser action); plan route ② as the
committed default — it is measured clean on this exact guide (18/18/0, 14 narrative + 4
artefact-view, 0 short pages). A harvest-skipped page blocks page-map coverage until re-harvested
or human-retired (spec §9e; CHANGELOG.md:38-43).
*Blocks:* nothing hard (② is sufficient); ① upgrades provenance.

**D-9 · Dangling canonical `mii-cs-consent-consent_category` (Gate A/B).**
*Question:* 3 examples on the 2026.0.0 release reference a CodeSystem defined nowhere; the fix
exists only on unreleased develop (recon/source.md §e). Faithful migration reproduces the
validation error.
*Who:* owner. *Recommendation:* if D-2 = tag 2026.0.0, reproduce faithfully and whitelist the
known error in the QA-delta triage (source-baseline-proven, never silently fixed); offer the
owners the develop cherry-pick as an upstream 2026.0.1 argument. If D-2 = develop/rc, moot.
*Blocks:* QA acceptance criteria (Phase 7).

**D-10 · M9 optional pages, other-bucket placements, TOPIC_NCI_CODE (Gate A/B, measured).**
*Question:* M9 keep/remove per measured artifact counts (>0 keeps — recorded user decision
2026-08-20, migration-spec.md:1988-2007); Consent counts: extensions 0, operations 0,
CapabilityStatement 0 (→ §9b synthesis, ① item), search-parameters 6, value-sets 3,
code-systems 3 (recon/source.md §e). `{{TOPIC_NCI_CODE}}` has NO default and no source
counterpart — an unreplaced value ships a bogus code (sushi-config.yaml:233-237 —
recon/template.md §h); which NCI Thesaurus code(s) Consent declares is NICHT PRÜFBAR from any
source.
*Who:* the M9 decision rule is SPLIT per migration-spec.md:1988-1995 — built-package artifact
counts decide only the five artifact pages (extensions/search-parameters/operations/value-sets/
code-systems; agent measures, human ratifies); **researcher-guidance and metadata are decided
from source NARRATIVE for them, not from counts**; owner/user pick the NCI topic code (an
informed-consent concept — content decision).
*Recommendation:* by counts: KEEP search-parameters (6) / value-sets (3) / code-systems (3),
REMOVE extensions (0) / operations (0) (re-measure at Gate 0). By source narrative: metadata —
no source narrative found → REMOVE; **researcher-guidance — candidate source narrative EXISTS**:
guide page 6.1.5 "Empfehlungen zur praktischen Anwendung" (4,300 B — recon/guide.md §a row 17),
so decide it against that page's page-map row (KEEP-and-fill if the Empfehlungen content routes
there, REMOVE only if the map routes it elsewhere and the reason is recorded). M11: delete the
Person illustrative example both languages; every `artifacts.other` type gets an explicit
placement row.
*Blocks:* page map validation; release-mode convention check.

**D-11 · Manifest re-stamp vs accepted downgrade.**
*Question:* accept C5c/R4 as NICHT PRÜFBAR rows (documented tripwire) or re-measure
`template-pages.tsv`/`template-artifacts.tsv` at v0.13.2/v1.3.4 and pass them explicitly?
*Who:* user. *Recommendation:* re-measure into `migration-log/` and pass via
`--template-pages`/`--template-artifacts` (sanctioned hand edit — template-pages.tsv:36-38;
page set measured byte-identical v0.11.1→v0.13.2, recon/template.md §g). Optionally also file
the re-stamp upstream to agent-skills — but do NOT block this migration on a skill release.
*Blocks:* clean C5c/R4 verdicts (cosmetic; verification still runs without it).

**D-12 · Dependency transfer (Gate A).**
*Question:* source pins are only `hl7.fhir.r4.core 4.0.1` + `de.einwilligungsmanagement 2.0.2|2.0.3`
(per D-2); the template scaffold ships parity pins (`de.basisprofil.r4 1.5.4`,
`kerndatensatz.meta 2026.0.0`, `hl7.fhir.uv.xver-r5.r4 0.1.0`, `hl7.fhir.uv.crmi 2.0.0`,
`hl7.terminology.r4 7.3.0`, `hl7.fhir.uv.extensions.r4 5.3.0` — sushi-config.yaml:246-270,
recon/template.md §f).
*Recommendation:* source pins win (F2: exactly as the source pinned them); ADD only template
machinery `hl7.fhir.uv.crmi 2.0.0` (recorded at Gate A per SKILL.md step 3) and whatever the
template's rulesets strictly require, each recorded as a target-only addition for F2; do NOT
import basisprofil/xver/meta parity pins the source never had (recon/source.md §d: deliberately
absent).
*Blocks:* F2 expectations; SUSHI build.

**D-13 · Retire-after-Gate-D set (owner).**
*Question:* what retires once the template shape is merged and published?
*Recommendation (proposed set, owner signs at Gate D):* the raw-XML source dirs
(`ressourcen-profile/`, `searchparameters/`, `terminologie/*.xml`, `examples/*.xml`) once FSH is
the single source of truth (their byte-identical FSH-derived successors live in `input/fsh/`);
`CodeSystem-MiiConsentPolicy.md` (either retired or explicitly declared the Gültigkeit-column
side-car — its extra columns are not CS-representable, recon/source.md §i.3); the `.gitignore`
`fhirpkg.lock.json` line (Firely-era); the README rewritten (its guide link is dead anyway);
`figures/` exports consolidated into `input/images/` (keep `.graphml` sources). The Simplifier
guide store stops being the editing venue — the owners' own issue #63 — an intended sunset they
must consciously accept, mirroring the guides' demonstrated deletability (recon/guide.md §b).
*Blocks:* Gate D only; nothing before.

**D-14 · Registry-only 6th example (Gate A; owner).**
*Question:* the published 2026.0.0 package ships `Example_MII_Consent_Einwilligung_1.json` with
NO XML source in git (recon/source.md §e line 87 / §h line 126). D-2 = "migrate tag 2026.0.0"
plus Phase 3.1's goFSH input universe (the git tree: 19 XML + 1 JSON = 20) silently drops it
from a migration presented as faithful to 2026.0.0 — and NO verifier net catches the drop: C1
and prepost-delta are keyed on the pinned git tree passed as `--source` (recon/skills.md §e).
*Who:* owner.
*Recommendation:* INCLUDE it, extracted from the pinned 2026.0.0 tarball (the release the
migration claims fidelity to is the package, and the package has 6 examples), recorded as a
target-only addition with tarball provenance; if the owner prefers the git tree as the fidelity
anchor, record its explicit EXCLUSION instead. Either way it is a Gate-A
artefact-completeness-checklist item (Phase 6.2).
*Blocks:* Gate A artefact-completeness sign-off; the goFSH input reconciliation (Phase 3.1).

**Measure-at-execution-time list** (not decisions — instructions to the run): re-measure the
develop/rc fingerprint vs the pinned baseline (recon/context.md §e); re-run the guide-key census
(a 2026.0.1/2027 guide may appear); Gate-0 `ig-stats.py` counts replace all counts quoted here;
re-verify `i18n-default-lang` in the scaffolded target (it moved once — SKILL.md:430-432);
re-check template/ig-template latest tags at run start (P1 stale-render arm: the URL-form build
fetches the ig-template's LATEST release at build time — verify-migration.py:2129-2133);
hidden-page probe once authenticated access exists (serial-nr gaps, recon/guide.md §a);
placeholder census by exclusion (`grep -rIl '{{' .`) after scaffolding.

---

## 4. Execution plan (maps 1:1 onto skill v0.25.0; run-log rows in brackets)

Consent's expected-steps ledger is the FULL shape-B set — all 31 rows minus exactly one
conditional (`5.1c simplifier-discover` is not needed: both human URLs exist — pre.1 satisfied
by D-0/D-7). Absent-required rows are DIVERGIERT under L2 (expected-steps.tsv:2-5).

### Phase 0 — Preparation (human + operator)
0.0 **Evidence persistence + preservation harvest — BEFORE the D-0 wait (no GO needed;
    anonymous, read-only).** (a) Copy the recon reports, the harvested guide-page HTML
    snapshots, the package tarballs (`pkg-2026.0.0.tgz`, `pkg-rc4.tgz`), the clones' commit
    pins, and THIS PLAN out of the volatile scratchpad to a durable location (e.g. a dedicated
    branch of the FGDH sandbox repo, or any non-`/tmp` directory): everything currently lives
    under `/private/tmp`, which this Mac clears at reboot (MEASURED: `kern.boottime` =
    2026-06-11; all `/private/tmp` content postdates that boot) — and since the plan's
    wall-clock is dominated by owner-decision latency, the loss window is longest exactly while
    nothing else runs. Every `recon/<report>.md` citation in this plan dangles after one
    OS-update reboot unless this step happens. (b) Run the route-② `guide-harvest.sh` NOW as a
    PRESERVATION harvest and persist it with (a): the harvest is anonymous, read-only, needs no
    GO (verified 18/18 — recon/skills.md §b), the 14 narrative pages exist NOWHERE in git, and
    the 2023 predecessor guide was already deleted from Simplifier (recon/guide.md §b/§e) — the
    plan's own single point of failure must not sit behind an unbounded owner wait. Phase 4
    re-runs the harvest at execution time as the pinned run-of-record; the 0.0 copy is the
    backstop.
0.1 **D-0 owner contact**: GO + venue + toolkit + D-2 baseline/version + D-8 project-download
    ask + ballot-schedule question. THE critical path.
0.2 Venue setup per D-0 outcome. In-place: branch on the MII repo,
    `migration/<source-version>-template-v0.13.2` (the spec's mandated scheme —
    migration-spec.md:1844-1850), PR base discovered from the repo's own convention (release PR
    #104 was Develop→Main; if the base is the publication branch, say so at Gate D — "merging is
    what publishes"). **In-place venue-enablement checklist** (settled via D-0(e) before any
    push): access mechanism decided (collaborator grant / owner-pushed branch / fork-PR) + the
    user's explicit re-authorization recorded; Actions enabled and runner minutes clarified
    (the repo has never had CI — no `.github/` at all, recon/source.md §a/§f); Pages state for
    branch previews; SSH transport for workflow-file pushes (HTTPS tokens fail — MEMORY:
    agent-skills dry run); branch-protection rules on the discovered PR base. Sandbox: FRESH
    branch in `mii-kds-consent-ig-inoffiziell`; supersede stale
    PR #3 explicitly (close with a pointer, keep `migration-log/` as evidence). **Sandbox
    mechanics** (all measured): the repo's default branch is `develop` (a stale source mirror,
    tip `4d44dbe` — recon/context.md §c) — update the mirror to the SOURCE `develop` tip
    (`744f7ab`) FIRST, and cut the migration branch from the D-2 baseline commit: the baseline
    pin lives on the migration branch, NEVER on the mirror. (Pointing the mirror at tag
    2026.0.0 would be a non-fast-forward rewrite: `792f9f3e` is NOT an ancestor of `develop` —
    MEASURED, `git merge-base --is-ancestor 792f9f3e origin/develop` fails, develop 18 commits
    ahead on a diverged line — and would replace develop-line content with master-line content,
    breaking exactly the mirror semantics RISK-14 defends.) Never make the migration branch the
    default; `gh-pages` exists (branch previews land under
    `branches/<branch>/`); push over **SSH** — workflow-file pushes fail over HTTPS tokens
    (MEMORY: agent-skills dry run); repo variables can switch off Zulip/publication workflows
    without YAML edits (recon/template.md §8).
0.3 Toolchain [`pre.5 toolchain`]: node 22 (nvm), pinned `npx --yes fsh-sushi@3.20.0` +
    `npx --yes gofsh@2.6.1` (never bare `gofsh` — SKILL.md:79), python3, java + pinned
    `validator_cli.jar` (D-4), **Docker with `hl7fhir/ig-publisher-base`** — macOS system Ruby
    2.6 cannot run Jekyll 4.4.1, so every local publisher build runs in that container (operator
    practice proven in the PROs try-run; the skill mandates no Docker), `~/.fhir` cache mounted.
    `SKILL_DIR`-resolved script paths only (SKILL.md:88-93).
0.4 [`pre.2 classify-source-shape`]: `shape=B` — evidence: no sushi-config/ig.ini, 14
    resources detected BY CONTENT across five German-named dirs; third-bucket inventory: README.md
    (disposition: rewritten), CodeSystem-MiiConsentPolicy.md (disposition per D-13/Gate A) —
    recon/source.md §a. Record pre.3 target state (sandbox: re-migration — report the stale
    branch before changing anything; MII repo: plain Simplifier project) and pre.4 census plan.
0.5 `sibling-skill-check.sh` — `fhir-ig-analysis` must be installed alongside; the check WARNs
    with the pinned `npx skills add …/tree/v0.25.0` command and never installs
    (migration-spec.md:1767-1833). The `@ref` install form silently does not pin
    (template RETIRED.md:41-45).

### Phase 1 — Gate 0: measure the unmigrated source [`1 preflight-analysis`, `5.1 source-inventory`]
1.1 `ig-stats.py analyze` on the pinned source → `migration-log/preflight-analysis.json`:
    licence tiers (expect file-only CC-BY), special_url_prediction (expect the 2 urn:oid CS),
    dependency_health (parent snapshot-less flagged), M9 counts, qa_baseline `None` ⇒ obtain the
    source QA proof NOW (spec §9c).
1.2 **Build the source QA baseline** — none exists (recon/source.md §f). **Committed method
    (no OR left open): the publisher-in-Docker wrapper build** — assemble a throwaway
    ig.ini+IG-resource wrapper around the source XML (outside the migration tree, never
    committed) and build it with the SAME tool + pin as Phase 9 (IG Publisher 2.3.2 in
    `ig-publisher-base` Docker), because Phase 9.2's acceptance ("qa errors ⊆ the
    source-baseline classes") is only meaningful when both sides come from the same tool — the
    PROs precedent was publisher-vs-publisher (MEMORY: PROs try-run), and the skill's
    qa_baseline row offers only "build the unmigrated source or fetch its rendered qa"
    (recon/migration-spec-v0250.md:2093 — no validator-tarball path). `validator_cli` over the
    published 2026.0.0 tarball is a CROSS-CHECK only, never the acceptance basis. **Persist the
    error census AND the wrapper config into `migration-log/`** (the Gate-D acceptance basis
    must be reproducible). The census (incl. the D-9 dangling canonical) is the "no worse than
    source" acceptance basis. Compare by element path (PROs-try-run technique).
1.3 Source-inventory: every artefact + the narrative structure; single guide tree (no §5.1a
    multi-tree complexity — one authoritative tree of 18 pages, recon/guide.md §a).

### Phase 2 — Identity [`2.1 read-identity`, `2.1 package-identity`, `2.1 repo-identity`; Gate A]
2.1 No sushi-config in the source → tier P (`package-identity.sh`: manifest + canonical by
    unanimous common prefix — expect 13/13 `…/fhir/modul-consent`) and tier R
    (`repo-identity.sh`: LICENSE→CC-BY-4.0, README title, release-tag↔commit tie 2026.0.0↔792f9f3e)
    are REQUIRED ledger rows. Expected contradictions to close with `decision:` lines (L3):
    status active/draft (D-6), publisher (profiles have none; terminology says "MII Task Force
    Consent Umsetzung" vs JSON CS "Medizininformatik-Initiative"; tarball author string drifts —
    recon/source.md §b; Gate-A remainder measured to `publisher` alone, provenance.md:54 —
    **BUT the sushi-config `publisher` is NOT an owner carry decision**: under template ≥ v1.1
    it is template CHROME and stays `NUM-DIZ` (spec §2.2 deliberate exception,
    migration-spec.md:343-350; template sushi-config.yaml:108-114); a source publisher is NEVER
    carried over it — the recovered TFCU/MII strings go into the identity ledger as
    content-attribution evidence only, closing the L3 contradiction with a `decision:` line
    citing the spec exception), version (D-2), licence metadata (D-1). Tier G (goFSH-derived
    config) is never identity.

### Phase 3 — goFSH derivation [shape B; `5.1b.2 gofsh-input`, `5.1b.2 gofsh-convert`, `5.1b.3 sushi-before`, `5.1b.3 postprocess-gofsh`, `5.1b.3 sushi-after`, `5.1b.5 parent-snapshots`]
3.1 The verbatim SKILL.md:134-234 block: input count by content (expect 19 XML + 1 JSON = 20
    from the git tree — the registry-only 6th example is NOT in this universe and rides D-14;
    the trap is measured HERE — a flagless goFSH run converted **1 of 20 at exit 0**, so
    `-t json-and-xml` is mandatory — migration-spec.md:755-767), full `-d` set,
    `gofsh-results.sh` reconciliation, `sushi-before` (expect ~41 errors), `postprocess-gofsh.py`
    (expect ~5), parent snapshots via `parent-snapshots.sh detect/build` + official
    `validator_cli.jar snapshot` (D-4; the repin suffixes the SOURCE-pinned parent version —
    `2.0.2-snapshots` under a 2026.0.0 baseline, migration-spec.md:1098-1099; the resulting F2
    DIVERGIERT vs the source pin is expected and pre-triaged per D-4), `sushi-after
    --expected-nonzero` → 0. All error-count deltas logged; goFSH-minted ids → ② queue (D-5).

### Phase 4 — Harvest [`5.1d guide-harvest`]
4.1 This is the pinned RUN-OF-RECORD harvest — a fresh run, never a reuse of the Phase-0.0
    preservation copy (which stays as backstop + diff reference). Route per D-8. Default ②:
    `guide-harvest.sh --guide-url
    "https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0" --out
    migration-log/harvest --keep-html …` — slugs discovered never constructed, pages pinned to
    `?version=2026.0.0`, `preview-content` depth-scanned, narrative/artefact-view classified.
    Acceptance: 18/18/0 with 0 `missing_runs` on narrative pages (the measured reference —
    migration-spec.md:1405-1412); any `silent-partial-success:` WARN must be `resolved:` (L1).
    Keep the HTML (`--source-html` feeds comparative R1). Harvest the 3 assets + note the
    master-tracking image URLs (rewrite to local `input/images/` copies from `figures/`).

### Phase 5 — Skeleton [`5.2 skeleton-vendored`, `5.2 template-reference`, `5.2 license-align`, `5.2 sushi-skeleton`]
5.1 Scaffold from template **v0.13.2** at a named ref, in place on the working branch — never a
    new repository without a recorded decision. Substitute the 15 active placeholders
    (`MODULE_SLUG=consent` → `mii-ig-consent`, packageId, bare canonical — all M1–M7-PASS
    measured, recon/template.md §b); rename the 3 placeholder-NAMED files
    (`ImplementationGuide-mii-ig-consent.md` ×2 + `.po`); `{{TOPIC_NCI_CODE}}` per D-10;
    placeholder census by exclusion (pre.4).
5.2 **No-vendor doctrine**: keep `ig.ini:42` URL line; delete `ig-template/`,
    `.github/workflows/sync-ig-template.yml`, `scripts/sync-ig-template.sh`,
    `scripts/resolve-ig-template-source.sh`; record BOTH ledger rows —
    `5.2 skeleton-vendored ref=v0.13.2 commit=a2390dea` and
    `5.2 template-reference url=https://github.com/medizininformatik-initiative/ig-template-mii-kds
    release=v1.3.4` (P1 is blind without it — expected-steps.tsv:41).
5.3 Template-repo-only removals: **run `scripts/first-run-bootstrap.sh` in its default DRY-RUN
    mode** to obtain the authoritative removal list at the checked-out ref (the skill's step 3 /
    spec §5.2 mandate "run its first-run bootstrap" — SKILL.md:258-260,
    migration-spec.md:1435-1437), apply those removals, and **log a `decision:` line that
    `--apply` was NOT used** — its branch-setup/branch-protection side effects
    (first-run-bootstrap.sh:1-30) are out of scope on an in-place migration branch; the skip
    must be recorded, never silent. Expected list (verified against
    first-run-bootstrap.sh:174): `release-please.yml`,
    `notify-zulip.yml`, `release-demo.yml`, both release-please JSONs, template CHANGELOG. Delete
    the template example artefacts (`example-patient` FSH + instance, paths verified against the
    checkout) and the full **M8 demo set** (page ×2 languages + `pages:`/menu entries ×2 +
    `demo/` + `gen-rendering-demo.py` + `demo-en/de.md` + `rendering-demo-codes.json`).
5.4 **DE-first flip (D-3)**: invert `i18n-default-lang/i18n-lang/translation-sources`
    (footgun: the language must be in `translation-sources`, not only `i18n-lang`, or every `.po`
    is silently ignored — SKILL.md step 6); DE content becomes `input/pagecontent/`; EN mirror
    under `input/translations/en/`; menus swapped; **the 3-file CI patch in the SAME commit**
    (language-model-check.sh inverted incl. the `:(exclude)` line, convention-check.mjs de→en
    paths, convention-check.test.mjs fixtures — recon/template.md §c).
5.5 `license-align.py` [`5.2 license-align`]: source LICENSE exists → byte-faithful copy, expect
    exit 0 with a `license-replaced:` announcement + FIX row (the template's scaffold CC-BY text
    is replaced by the source's own CC-BY variant); D-1 records the sushi-config `license:` add.
5.6 **`.gitignore` un-ignore**: add `!migration-log/*.log` — the scaffold's blanket `*.log`
    (.gitignore:24) swallows the run log otherwise (recon/template.md §f).
5.7 FSH-collision rule: module definitions win; `aliases.fsh` per DEFINITION; both lists logged.
    Dependencies per D-12. Acceptance: `5.2 sushi-skeleton` clean (shape-B-qualified, §5.1b.4).

### Phase 6 — Artefact transfer [`5.3 transfer-artefacts`; → Gate A]
6.1 Transfer the derived FSH structure-preserving; IDs/URLs byte-unchanged; the 2 `urn:oid`
    canonicals into `special-url:` (regenerated per the template recipe, never copied from
    another module). Acceptance: `comm -3` over sorted repo-relative FSH path lists — empty apart
    from logged scaffold additions.
6.2 **Gate A** (module maintainer + TF-KDS): canonical/ID/licence/identity preservation, artefact
    completeness (incl. the D-14 registry-only 6th example disposition), goFSH-minted ids,
    parent-snapshot decision (D-4), publisher chrome check (sushi-config `publisher` stays
    `NUM-DIZ` per spec §2.2 — never an owner decision to carry TFCU/MII into it; the recovered
    source publisher strings are recorded as attribution evidence in the identity ledger only),
    D-1/D-2/D-5/D-6/D-9/D-10/D-12/D-14 recorded.

### Phase 7 — Narrative [`5.4 fql-scan`, `5.4a optional-page-decisions`, `5.4b security-privacy-decision`, `5.4c page-routing`, `5.4d derived-scan`; → Gate B]
7.1 `fql-scan.sh --strict` over the harvested pages (exit 2 = empty target set, never a pass);
    the 4 artefact-view pages' Simplifier renders re-express as IG-Publisher includes
    (structure-tabs etc. per `fql-rules.tsv`/crosswalk); `generated-view-lossy:` tokens keep
    generated tables from burying real narrative losses.
7.2 `page-structure-advice.py --map` → `migration-log/page-map.tsv` (v2 columns
    source_page/target/reason/branch/measure); universe = guide tree ∪ harvest manifest
    (auto-discovered `--harvest-tsv`); exit 1 until every page has a row and every RETIRED row a
    reason. Routing expectations: 3 folder stubs → hub/index handling (branch 4a, ≤250 words);
    the Consent page's Suchparameter sections → the kept search-parameters page; profile pages →
    intro-notes or artefact pages per branch 1; menu budget ≤33/≤10/≤8/depth 2.
    **A HUMAN reviews/edits the map file itself; step 5 consumes ONLY the map; re-running the
    generator OVERWRITES the reviewed map** — sequence the review after the final generator run
    or budget re-review (SKILL.md:460).
7.3 Write DE pages verbatim from the harvest (provenance headers + `TODO:REVIEW` from the
    harvester); link rewrite from the map + census (recon/guide.md §g.5): the 34 ig.fhir.de
    Einwilligungsmanagement links stay external (that IG is not being migrated) but get checked;
    13+2 plain-`http://` links → https; the 2 cross-guide `?version=current` Simplifier links →
    pinned or flagged; the ART-DECOR `effectiveDate=2021` service URL flagged as fragile
    (Gate-B item); images → local `input/images/` (from `figures/`, killing the master-tracking
    hot links); MII logo/CSS: the template brings its own branding — the guide's custom
    `MIICustomIGStyle` is NOT carried (template look-and-feel decision, note at Gate B).
7.4 §9b CapabilityStatement: absent in source → SUGGESTED from the module's profiles, marked,
    ① queue, rendered inline via `{% lang-fragment %}` (recon/skills.md §a step 5).
7.5 M9/M11 per D-10 [`5.4a`/`5.4b`]; every migration-WRITTEN text (hub one-liners, bridges,
    the CapabilityStatement suggestion) gets `DERIVED:` box markers; `derived-scan.py` clean
    [`5.4d`] — marker-without-box or missing language twin FAILS.
7.6 Known source-content defects surface as Gate-B findings, never silent fixes: the ART-DECOR
    terminology gap ("zeitnah" — recon/guide.md §g.6), the dangling category CodeSystem (D-9),
    the draft VersionModules CS bound in an active profile (recon/source.md §i.4), the dead
    README guide link. ② items for the owners.

### Phase 8 — Bilingual wiring [`5.5 gen-page-title-po`; → Gate C]
8.1 DE-first inversion of the skill's step 6: German `pages:` titles are the msgids;
    `gen-page-title-po.py` from the SUSHI-generated IG resource →
    `input/translations/en/ImplementationGuide-mii-ig-consent.po`, seeded from
    `migration-log/menu-titles-en.txt`; menu = `input/includes/menu.xml` (DE) + EN mirror.
    Hand-update the stale `publisher` unit in the IG-level `.po`: the template's NUM-DIZ chrome
    (spec §2.2) leaves a scaffold-era publisher string in the title catalogue that the generator
    does not touch — the spec mandates fixing it by hand (migration-spec.md:343-350).
8.2 EN pages: machine translations of all 14 DE pages, each marked
    `machine translation of source page <name> (de)` — NEVER "of the German source" (the exact
    wording language-model-check polices; 21 markers tripped it on the Studie try-run —
    migration-spec.md:2046-2049). R3 flags byte-identical "translations".
8.3 **Gate C** (bilingual reviewer): heaviest gate here — 14 machine-translated pages.

### Phase 9 — Build & QA [`5.6 sushi-build`, `5.6 ig-publisher`, `5.6a sibling-skill-check`, `7 prepost-delta`]
9.1 SUSHI 3.20.1 + IG Publisher 2.3.2 (SHA-pinned, read from the target's workflow env) in
    `ig-publisher-base` Docker locally; parent-snapshot prebuild per D-4; tx fallback
    tx.fhir.org (no SU-TermServ certs in a sandbox; `::notice`, never hard-fail —
    ig-publisher.yml:213-257).
9.2 Acceptance: qa errors ⊆ the source-baseline classes proven at 1.2 (incl. the D-9 whitelist);
    broken links 0 new.
9.3 `ig-stats` postflight + same-module verification (source FIRST, migrated second; equal
    packageId triggers it; identity/artifact set/canonical URLs must read IDENTISCH);
    `prepost-delta.py` [`7 prepost-delta`] — exit 1 = a property got worse, a stop not a delta;
    expect the **census-mode exception**: raw-resource `reduced` vs FSH `static` census reports
    count diffs as expected-change with both modes named (the Consent/harvest shape —
    prepost-delta.py:1-80).

### Phase 10 — Verification, report, PR [`11 verify-migration`; → Gates B/C/D]
10.1 Manifest re-measure per D-11 → `migration-log/template-pages-v0.13.2.tsv` +
     `template-artifacts-v1.3.4.tsv`, stamped, passed via `--template-pages`/`--template-artifacts`.
10.2 `bash "$ML" run 11 verify-migration --emits-runlog --expected-nonzero 'findings are this
     step OUTPUT (1 = DIVERGIERT, 3 = NICHT PRÜFBAR)' -- python3
     "$SKILL_DIR/scripts/verify-migration.py" --target . --source <pinned-source> --rendered output
     --log migration-log/run.log --harvest-tsv … --harvest-dir … --source-html … --page-map …
     --derived-tsv … --source-lang de --template-latest v0.13.2 --publisher-pin 2.3.2
     --expected-steps … --template-pages … --template-artifacts … --shape B` — note
     `--expected-nonzero` (with its mandatory WHY string) belongs to the `migration-log.sh run`
     WRAPPER, never to `verify-migration.py`, whose argparse defines no such flag and errors on
     it (verify-migration.py:3456-3483; migration-log.sh:433-434; sanctioned form
     SKILL.md:354-359); `--template-latest` = module-template tag (P2 axis), NOT v1.3.4; there
     is NO `--source-guide-url` on the verifier (that flag belongs to `comparison-table.py`) —
     recon/skills.md §e. Exit 1 while any DIVERGIERT is untriaged, 3 while NICHT PRÜFBAR rows
     remain; NEITHER is a pass; every DIVERGIERT triaged to a decision or fix. If no local/CI
     rendered build exists yet (D-4 unresolved), P1/P3, R1–R5, C2 return NICHT PRÜFBAR — plan
     the build environment or accept the rows owed (recon/skills.md blockers).
10.3 `qa-checklist.py` (per-gate sign-off boxes) + `comparison-table.py`
     (`--preview-url <branch preview> --source-guide-url <D-7 guide>`) pasted, never retyped;
     report from `migration-report-template.md` with per-item "Decision requested by / If nobody
     acts / owner / effort / reversibility"; protocol section generated from `run.log`.
10.4 Draft PR on the discovered base; branch preview under `gh-pages/branches/<branch>/`
     (enable Pages in the sandbox if root 404s). **Gate D** (TF KDS / AG IOP / NSG): merging is
     what publishes; the agent never merges; D-13 retire set rides Gate D.

---

## 5. Risks & gotchas (recon-confirmed only)

**Code legend (for the reader three weeks out).** This plan's own risks are `RISK-1…RISK-16`
(table below) — deliberately NOT `R1…R5`, which are verifier check codes. Everything else is
skill/template vocabulary (full lookup: `references/codes.md` in the `mii-ig-migration` skill,
agent-skills v0.25.0): verdicts IDENTISCH / DIVERGIERT / NICHT PRÜFBAR (the last is never a
pass); human gates 0 (measured scope) / A (identity) / B (narrative) / C (language) / D
(release — merging is what publishes); template CI checks **M1–M11** (e.g. M5 canonical space,
M6 CalVer, M8 demo page gone, M9 optional pages decided); verifier checks **C1–C7** (content
completeness), **F1–F4** (fidelity — F2 dependency pins vs the SOURCE pin, F3 licence from
evidence), **P1–P5** (provenance — P2 template ref is latest, P4 guide pinned to a published
version), **R1–R5** (rendered output — R4 = no links to deleted template examples, NOT this
plan's RISK-4), **L0–L4** (run-log — L2 expected steps logged, L3 no open identity
contradiction); identity evidence tiers **P/R/G** (Package / Repo / goFSH-derived — G is never
identity); report queues **①** DEC = someone must choose / **②** REV = someone must check /
**③** QA = triaged by provenance; source shapes **A** (FSH in repo) / **B** (raw XML → goFSH
derivation — the Consent shape).

| # | Risk / gotcha | Evidence | Mitigation |
|---|---|---|---|
| RISK-1 | No owner momentum on 2027; D-0 non-response stalls the in-place route entirely | recon/context.md §d (0 hits 2027/ballot) | Sandbox route as demonstrator; lead D-0 with the owners' own issues #36/#63/#64/#66 |
| RISK-2 | Parent `de.einwilligungsmanagement` snapshot-less in BOTH 2.0.2/2.0.3; local cache pin breaks CI on clean checkouts | migration-spec.md:1009-1020; sandbox D4 (recon/context.md §c) | D-4 CI-prebuild option; repin suffixes the SOURCE pin (`2.0.2-snapshots` under the 2026.0.0 baseline — migration-spec.md:1098-1099); pre-triage the by-construction F2 DIVERGIERT as the Gate-A carry decision (provenance.md:94); escalate the 3 refused differentials upstream |
| RISK-3 | Moving target: develop 18 ahead, rc-1..4 published, issue #124 churning the fingerprint area | recon/source.md §0/§h; recon/context.md §e | D-2 pins the tag; re-measure fingerprint at execution; expect a 2026.0.1 mid-migration |
| RISK-4 | Narrative single point of failure: 14 pages only in Simplifier; predecessor guide already deleted; the only current copies sit in volatile /tmp | recon/guide.md §e/§b; MEASURED kern.boottime (Phase 0.0) | Preservation harvest + durable persistence at Phase 0.0, BEFORE the D-0 wait; Phase 4 re-runs it as the pinned run-of-record; keep HTML |
| RISK-5 | goFSH `-t json-and-xml` trap: flagless run converts 1 of 20 at exit 0 | migration-spec.md:755-767 | Verbatim 5.1b.2 block; gofsh-results reconciliation by count |
| RISK-6 | DE-first trips template CI by configuration alone (language-model-check :46) | recon/template.md §c | 3-file one-commit patch in the skeleton commit (Phase 5.4); Dokument-proven |
| RISK-7 | C5c/R4 manifest staleness (v0.11.1 stamps vs v0.13.2 scaffold) | verify-migration.py:1034-1046; recon/template.md §g | D-11 re-measure (page set byte-identical — safe) |
| RISK-8 | URL-form template reference fetches ig-template LATEST at build time; offline builds impossible; template can move mid-run | ig.ini:42; verify-migration.py:2129-2133 | Record `release=v1.3.4`; rebuild+re-record on mid-run release; deliberate trade, stated |
| RISK-9 | `.gitignore:24 *.log` swallows `migration-log/*.log` | recon/template.md §f | Un-ignore line in the skeleton commit |
| RISK-10 | Dangling `mii-cs-consent-consent_category` reproduces a validation error on a faithful 2026.0.0 migration | recon/source.md §e | D-9 whitelist against the source baseline; never a silent fix |
| RISK-11 | Re-running the page-map generator overwrites the human-reviewed map | SKILL.md:460 | Review after the final generator run; re-apply+re-review on any regeneration |
| RISK-12 | macOS Ruby 2.6 cannot run Jekyll → no naive local publisher build | Studie plan §2.1/Phase 7 (operator practice); MEMORY: fhir-server not locally buildable analog | `hl7fhir/ig-publisher-base` Docker for every local build; CI branch preview as the second leg |
| RISK-13 | Force-push→merge race on the PR | MEMORY: force-push-then-merge | Verify `headRefOid` == local SHA before any human merges |
| RISK-14 | Sandbox default-branch trap: `develop` mirror is stale; making the migration branch default breaks the mirror semantics | recon/context.md §c | Update mirror to the SOURCE develop tip (`744f7ab`), never to the tag (non-ancestor — Phase 0.2); migration branch (cut from the D-2 baseline) never default |
| RISK-15 | `{{TOPIC_NCI_CODE}}` ships a bogus code if unreplaced; no source counterpart exists | sushi-config.yaml:233-237 (recon/template.md §h) | D-10 explicit code decision; placeholder census by exclusion catches leftovers |
| RISK-16 | Two live guide slugs; wrong anchor = wrong P4/provenance | recon/source.md §h | D-7 owner confirmation; default to the version-pinned key |

---

## 6. Effort & scale estimate

Mechanically heavier than both precedents per artefact of scale, but the scale is tiny: 14
conformance resources + 5 examples (Studie: 60), 18 harvested pages (Studie: 22 ×2 in-repo),
2-dependency surface. The heavy steps are all pre-measured by the skill on this exact module
(goFSH 41→5→0, harvest 18/18/0, snapshots 18/21 on 2.0.2 / 21/21 on 2.0.3), which converts
unknown-risk into known-work. Estimate ~1.5–2 agent-days of mechanics; wall-clock dominated by
owner-decision latency (D-0, D-1, D-2, D-4) and the Gate-C review of 14 machine-translated
pages. Critical path: D-0 → D-2/D-4 → CI-buildable preview → Gates.

## 7. What this plan deliberately does NOT do

- **No migration step is executed** — no branch, no fork, no issue/comment/PR on any
  medizininformatik-initiative repo (hard read-only policy for this engagement; also
  MEMORY: MII org access policy, tier 3), and no push to the FGDH sandbox either. The in-place
  route can therefore NOT be started by owner GO alone: it needs the D-0(e) access mechanics
  settled AND the user's explicit re-authorization lifting the standing MII read-only agent
  policy for `kerndatensatzmodul-consent` (see D-0 *Blocks*).
- No licence metadata, version bump, id/canonical change, or dependency edit before its decision
  (D-1/D-2/D-5/D-12) is recorded with its owner.
- No skill or template patching is assumed: the DE-first CI patch and the manifest re-stamp are
  carried as plan-level work INSIDE the migration branch, not as upstream releases this plan
  waits on.
- The Simplifier guide and project stay untouched; retirement of the raw-XML tree and the
  Simplifier editing venue is a Gate-D item (D-13), not a migration step.

## 8. Comparison to the Studie plan (one paragraph)

Consent is the Studie plan's inverse on almost every axis: Studie was shape A with in-repo
narrative and owner-authored EN translations — its hard parts were coordination (an owner
merging 8 PRs a day, a 3-way version contradiction, a missing LICENSE file) while its mechanics
were light (no goFSH, no harvest, no snapshots, Gate C a correspondence review). Consent has
CLEANER coordinates (master==tag, one guide version, LICENSE file present and unanimous, bare
canonical passing M1–M7 measured) but ALL the heavy machinery: shape-B goFSH derivation, the
mandatory 18-page Simplifier harvest (route 2c, which Studie skipped entirely), the
parent-snapshot blocker with its Gate-A CI decision, machine translation of the full page set
under DE-first, and a ~160-link rewrite surface. What is easier: the baseline decision, licence
evidence, M5/M6 fit, and the fact that the skill has already measured every hard step on this
exact module. What is harder: no owner 2027 momentum to attach to (D-0 is colder), the
narrative exists nowhere in git (single point of failure), and no QA baseline exists at all —
Gate 0 must build one before any equivalence claim. Net: same plan skeleton, shifted risk — from
"don't race the owner" (the Studie plan's own risk R1) to "get the owner in the loop at all, and
make CI able to build" (Consent RISK-1/RISK-2).

---

**NOT EXECUTED — the next action is D-0: contact Sebastian Stäubert (cc Martin Bialke / TF
Consent Umsetzung) with the GO question, the toolkit choice, the 2026.0.0-vs-develop baseline
question, and the project-download ask. Nothing in this plan runs before that.**
