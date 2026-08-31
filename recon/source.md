# SOURCE recon — medizininformatik-initiative/kerndatensatzmodul-consent

Measured 2026-08-31 (read-only). Clone: `/private/tmp/claude-503/-Users-marcel-Development-cross-hub-patientportal/9e6d07a4-6adb-4483-b4c7-d44df6dc83fb/scratchpad/recon/source` (full clone, all tags). Tag worktree: `…/recon/source-tag`.

## 0. Refs measured

| Ref | SHA | Date | Evidence |
|---|---|---|---|
| `master` HEAD | `792f9f3e4ce496185b428691d2ce252f2e18b9f2` | 2025-12-18 (Sebastian Stäubert, "Merge pull request #105…") | `git rev-parse HEAD`; `git log -1` |
| tag `2026.0.0` | `792f9f3e4ce496185b428691d2ce252f2e18b9f2` | same commit | `git rev-parse 2026.0.0^{commit}` |

**MEASURED: master HEAD and tag 2026.0.0 are the SAME commit — `git diff --stat 2026.0.0 master` is empty. Every statement below applies identically to both; there are zero differences to flag.**

The repo's `pushed_at` 2026-08-21 (gh api: `"pushed_at":"2026-08-21T07:21:49Z"`) is **branch `develop`**, not master: `git log -1 origin/develop` = `744f7ba 2026-08-21 Martin Bialke | slices templateType resultType wieder rein`. `develop` is **18 commits ahead of master** (`git rev-list --count master..origin/develop` = 18), touching 7 files (Einwilligung profile +61 lines, Policy CS/md, VersionModule CS JSON, 3 examples). Other branches: `fix/extension-cardinality-domainreference` (1 commit, 2026-02-06, Thomas Debertshäuser), `renovate/configure` (unmerged bot branch, PR #55).

Git tags (NO `v` prefix, confirmed `git tag -l`): `1.0.7`, `2025.0.0-alpha`, `2025.0.0`, `2025.0.3`, `2026.0.0`.

## a. SHAPE — what lives in-repo vs on Simplifier

Complete file census (`find . -type f -not -path './.git/*'` → 32 files):

```
.gitignore  LICENSE  README.md
examples/                    5 XML instances
figures/                     8 images (jpg/png/tiff/graphml)
ressourcen-profile/          3 XML StructureDefinitions
searchparameters/            6 XML SearchParameters
terminologie/codesystems/    2 XML CS + 1 JSON CS + 1 .md table (CodeSystem-MiiConsentPolicy.md)
terminologie/valuesets/      3 XML VS
```

- **FSH: NONE.** No `input/fsh`, no `sushi-config.yaml` (measured: absent from file census; open issue **#36 "IG auf FSH umstellen"**, open since 2024-01-19, confirms FSH was never adopted).
- **Raw XML conformance resources are the source form** (`ressourcen-profile/`, `searchparameters/`, `terminologie/`) — plus exactly ONE JSON resource, `terminologie/codesystems/CodeSystem-MiiConsentVersionModuleCodeSystem.json` (mixed-format inconsistency; open issue #101 "CodeSysteme und ValueSet einheitlich nach JSON transformieren").
- **Simplifier project files: NONE in tree.** No `.simplifier`, `project.yaml`, `package.bake.yaml`, `fhirpkg.lock.json`. But `.gitignore:1` = `fhirpkg.lock.json` — someone runs Firely/Simplifier tooling locally and deliberately keeps the lock out. History: `fhirpkg.lock.json` and a stale `package.json` (`"name":"consent","version":"1.0.3"`, dep `de.einwilligungsmanagement 1.0.1`) existed and were DELETED (`git show 07e826d` — "Delete package.json", 2025-06-13, Stäubert; `c0bb212 remove lock file`).
- **IG-Publisher files: NONE.** No `ig.ini`, no `input/pagecontent`, no `menu.xml`, no ImplementationGuide resource in-repo, ever (`git log --all -- ig.ini input/ …` shows only the package.json/lockfile deletions).
- **Narrative/guide pages: NONE in-repo.** The published package 2026.0.0 contains a Simplifier-generated `ImplementationGuide.json` whose page tree (`MII-IG-Modul-Consent/Release-Notes.page.md`, `Beschreibung-Modul-Consent.guide.md`, …) references Simplifier-only markdown pages; the IG skeleton has `url = "/guide/mii-ig-modul-consent-2026?version=current"` (a relative Simplifier link, not a canonical), `id/packageId/license/publisher = null`.
- **No CI whatsoever**: no `.github/` directory at all (`ls .github` → No such file). Open issues #64 (auto-ig-builder) and #66 (CI FHIR-validator pipeline) confirm CI is wanted but absent.

**Conclusion (INFERENCE, well-supported):** In-repo = conformance resources + examples + figures only. Package manifest, package build (XML→JSON conversion), ImplementationGuide resource, and ALL guide narrative live exclusively on Simplifier. Issue #63 ("github statt simplifier für IG-Edit nutzen", open since 2024-12) shows the maintainers themselves want to invert this. Any migration must recover/rewrite the narrative from the Simplifier guide — it cannot be harvested from git.

## b. Package identity

There is NO manifest in the tree — identity comes from the Simplifier-published package (registry evidence, section h):

- **Package id/name:** `de.medizininformatikinitiative.kerndatensatz.consent` (package.json inside the 2026.0.0 tarball)
- **Version in tree:** does not exist as a single value. Per-resource `version` elements diverge: Einwilligung 1.0.9 (`ressourcen-profile/Profile_MII_Consent_Einwilligung.xml:5`), DocumentReference/Provenance 1.0.8, all 6 SearchParameters 1.0.7, Answer CS/VS 1.6.0, Policy CS 1.1.0, Policy VS 1.0.3, SignatureTypes VS 1.0.1, VersionModules CS 0.2.0 (status `draft` while everything else is `active`). Package-level version (2026.0.0) exists only registry-side.
- **Canonical space: the BARE space** — `https://www.medizininformatik-initiative.de/fhir/modul-consent/…` (e.g. `Profile_MII_Consent_Einwilligung.xml:4`). NOT `/fhir/ext/modul-consent` and NOT `/fhir/core/modul-consent`, despite the README calling it "Erweiterungsmodul" (extension module). This is the third MII canonical space (bare), the one the template's M5 does NOT model natively → special-url handling predicted.
- **Publisher:** absent from the 3 profiles and 6 SearchParameters (no `<publisher>`/`<contact>` at all — measured by grep). Terminology resources carry `publisher = "MII Task Force Consent Umsetzung"` (CS/VS XML files); the JSON CS says `"publisher": "Medizininformatik-Initiative"`. Package tarball `author` = `"sebastianstubert"` (2026.0.0) vs `"sebastianstaeubert"` (2026.0.1-rc-4) — even the author string drifts.
- **jurisdiction** (tarball package.json): `urn:iso:std:iso:3166#DE`. **No `canonical` field and no `license` field in the tarball package.json.**
- Contacts per README ("Autoren und Ansprechpartner"): Leitung Martin Bialke + Sebastian Stäubert (@SebStaeubert); technische Umsetzung Stefan Lang, Martin Bialke.

## c. Licence — tiered evidence

1. **Machine-readable in package manifest: ABSENT.** The published tarball `package.json` (both 2026.0.0 and 2026.0.1-rc-4) has NO `license` field; the packaged `ImplementationGuide.json` has `license = null`. No sushi-config exists.
2. **LICENSE file: PRESENT** — 18,658 bytes, sha256 `f5b745ef98087f531e719ee8ca6a96809444573ecc7173c6fa68eaad39b3cc3f`, first line "Attribution 4.0 International". Byte-diff vs creativecommons.org `legalcode.txt` (18,657 B): whitespace/line-wrapping differences only, identical legal text → **CC-BY-4.0 full legal code (GitHub's standard wrap variant)**. GitHub license API detects `"license":"CC-BY-4.0"` (gh api repos/... → spdx_id).
3. **Licence prose in resources:** exactly ONE resource carries a copyright: `terminologie/codesystems/CodeSystem-MiiConsentVersionModuleCodeSystem.json:48` — `"copyright": "© 2019+ TMF e. V., Charlottenstraße 42, 10117 Berlin … CC BY 4.0 …"`. The other 13 conformance resources have no copyright element (grep across *.xml/*.json).

**Verdict: prior survey classification "file-only CC-BY" CONFIRMED precisely** — LICENSE file yes (CC-BY-4.0), machine-readable licence metadata no (neither in-repo — no manifest exists — nor in the published package), per-resource copyright only on 1 of 14 resources.

## d. Dependencies

Declared (published package.json, 2026.0.0 tarball — the ONLY dependency declaration that exists; nothing in-repo to blame/log):

| Dependency | Pin | Note |
|---|---|---|
| `hl7.fhir.r4.core` | `4.0.1` | matches `<fhirVersion value="4.0.1">` in all 3 profiles |
| `de.einwilligungsmanagement` | `2.0.2` (2026.0.0) → **`2.0.3` in 2026.0.1-rc-4** | HL7-DE/IHE-DE Einwilligungsmanagement IG; base of 2 of 3 profiles |

- **NOT present:** `de.basisprofil.r4` (no basisprofil dependency at all), no `hl7.fhir.extensions.r5`/xver packages, no R5-backport, no CRMI, no terminology package. The dependency surface is unusually small.
- Actual cross-package canonical usage (grep in profiles): `baseDefinition` = `http://fhir.de/ConsentManagement/StructureDefinition/DocumentReference` (`Profile_MII_Consent_DocumentReference.xml:50`), `…/Provenance` (`Profile_MII_Consent_Provenance.xml:40`); Einwilligung is based directly on core `http://hl7.org/fhir/StructureDefinition/Consent` (`Profile_MII_Consent_Einwilligung.xml:35`) but type-references `http://fhir.de/ConsentManagement/StructureDefinition/DomainReference`, `…/Xacml`, `…/Patient`, `…/QuestionnaireResponse` (grep output in transcript).
- **Bot-added dependency lines: NONE possible/found** — there is no manifest in master. Renovate was proposed (PR #55 "Configure Renovate", app/renovate, 2024-12-01) and **never merged**; `renovate.json` exists only on branch `renovate/configure`.

## e. Resource census (master == tag 2026.0.0)

By type and format (14 conformance + 5 example resources in-repo):

| Type | Count | Format | Files |
|---|---|---|---|
| StructureDefinition (profiles) | 3 | XML | `ressourcen-profile/Profile_MII_Consent_{Einwilligung,DocumentReference,Provenance}.xml` |
| Extensions / logical models / CapabilityStatement / OperationDefinitions | 0 | — | none exist |
| SearchParameter | 6 | XML | `searchparameters/SearchParameter_MII_Consent_Einwilligung_*.xml` (incl. 3 composite provision* params) |
| CodeSystem | 3 | 2 XML + 1 JSON | Answer, Policy (XML); VersionModules (JSON, status draft, 20 concepts) |
| ValueSet | 3 | XML | Answer, Policy, SignatureTypes |
| Examples | 5 | XML | 3 Consent, 1 DocumentReference, 1 Provenance |
| non-resource | 1 | md | `terminologie/codesystems/CodeSystem-MiiConsentPolicy.md` — a human-readable German policy table duplicating the Policy CS (generated-vs-source ambiguity, see i) |

FSH count: 0. The **published package** additionally contains `ImplementationGuide.json` and a 6th example (`Example_MII_Consent_Einwilligung_1.json`, Consent `89f494a3-…`) that has NO XML source in the repo (Simplifier-side extra; measured by tarball listing).

**Out-of-space canonicals (special-url work predictor) — 2 of 14:**
- `CodeSystem-MiiConsentAnswerCodeSystem.xml`: `url = urn:oid:2.16.840.1.113883.3.1937.777.24.5.2`
- `CodeSystem-MiiConsentPolicyCodeSystem.xml:6`: `url = urn:oid:2.16.840.1.113883.3.1937.777.24.5.3`
Both are referenced by their in-space ValueSets via `<system value="urn:oid:…">` (compose includes, measured). Everything else (3 profiles, 6 SPs, 3 VS, 1 JSON CS) is in the bare space `…/fhir/modul-consent/…`.

**id ↔ url mismatches — EVERY resource that has an id (9 of 14):**
- 3 profiles: random UUID ids vs slug urls — e.g. Einwilligung `id = e0e166b4-0f77-478d-9062-de0034d98ce0` vs `url …/mii-pr-consent-einwilligung` (`Profile_MII_Consent_Einwilligung.xml:3-4`); DocumentReference `56375452-…`; Provenance `f675b1e8-…`.
- 2 XML CS + 2 XML VS: ART-DECOR-style `OID--timestamp` ids — e.g. Policy CS `id = 2.16.840.1.113883.3.1937.777.24.5.3--20251211153003` (`…PolicyCodeSystem.xml:2`); Policy VS `id = 2.16.840.1.113883.3.1937.777.24.11.36--20230331232804` vs url `…/mii-vs-consent-policy` (`…PolicyValueSet.xml:2,11`); SignatureTypes VS has a UUID id (`88464c5b-…`).
- 1 JSON CS is the ONLY id-matching resource: `id = mii-cs-consent-version-modules` matches url slug.
- **All 6 SearchParameters have NO id element at all** (grep `-c '<id '` = 0 for each).
- Name-style inconsistency inside one release: `name = "MII CS Consent Policy"` (spaces — invalid vs usual convention; open issue #97 wants it renamed) vs `MII_CS_Consent_Answer`, `MiiConsentPolicyValueSet` vs `MII_VS_Consent_Answer`.

**Dangling in-space canonical:** 3 example Consents reference `…/fhir/modul-consent/CodeSystem/mii-cs-consent-consent_category` (e.g. `examples/Example_MII_Consent_Einwilligung.xml:40`) — **this CodeSystem is defined NOWHERE** (not in repo, not in package). The develop branch commits of 2026-03-19 ("Update consent category system URL in XML") change exactly these lines → known-broken on the 2026.0.0 release, fixed only unreleased.

## f. QA baseline

- **No in-tree qa.txt/qa.html, no build logs, no CI config, no `.github/` at all** (measured, section a). There is no repo-owned toolchain; the only toolchain evidence is the ignored `fhirpkg.lock.json` (Firely Terminal / Simplifier sync, INFERENCE from filename) and Simplifier's package build.
- Consequence: **no validation baseline exists to compare against** — a migration QA comparison must build its own source baseline (as in the PROs try-run: run IG-Publisher/validator over source and target and diff by element path). Open issues #64/#66/#107 (auto-ig-builder, validator CI, SearchParameter tests) confirm zero automated QA today.

## g. Activity + people

Last 25 master commits: 2025-12-01 → 2025-12-18 (all in the v2026 release window; full one-liner list in measurement transcript, `git log -25`). Authors all-time (98 commits): Sebastian Stäubert 52, Stefan Lang 26, Martin Bialke 11 (+6 as `mbialke`, +2 as `bialkem`), Jörg Römhild 1. **Mergers:** SebStaeubert merged 7 of the last 8 PRs; mbialke merged the release PR #104 ("Release v2026: Develop -> Main") — two active maintainers, matching the README's Leitung.

- **Open PRs: exactly 1** — #55 "Configure Renovate" (app/renovate, 2024-12-01, unmerged).
- **Open issues: 44** (gh search total_count; 40 newest listed in transcript). Migration-relevant: **#36 IG auf FSH umstellen** (2024-01), **#63 github statt simplifier für IG-Edit** (2024-12), **#64 auto-ig-builder**, **#66 CI FHIR-Validator**, **#101 CS/VS einheitlich nach JSON**, **#97 Policy-CS name rename**, #107 SearchParameter tests, #115 resultType verpflichtend, #111 eigene Profile pro Consent-Art (potential future resource growth), #123 FHIR-Search-Korrektheit, #128 TF CU Enforcement (2026-08-06, newest).
- **2027/ballot activity: NONE** — `gh api search` for "2027" and "ballot" in issues → 0 hits each; no 2027/ballot branches. Release cadence (tags 2025.0.0 → 2025.0.3 → 2026.0.0, Dec/Jun/Dec) makes a 2026.0.1 patch (develop + rc-1..4) the imminent event, **not** a 2027 ballot.
- Latest release: "KDS Modul Consent 2026.0.0" 2025-12-18 (gh release list). Post-release master is untouched; all 2026 work sits on develop.

## h. Registry cross-check (packages.simplifier.net)

`curl https://packages.simplifier.net/de.medizininformatikinitiative.kerndatensatz.consent`:

- **dist-tags.latest = `2026.0.0`** (matches git tag/master).
- Published versions (19): `1.0.0-ballot1, 1.0.1 … 1.0.7, 2025.0.0-alpha, 2025.0.0, 2025.0.1, 2025.0.2, 2025.0.3, 2025.0.4, 2026.0.0, 2026.0.1-rc-1 … rc-4`.
- **Version drift vs git (both directions):**
  - Registry-only versions with **no git tag**: `1.0.0-ballot1`–`1.0.6`, `2025.0.1`, `2025.0.2`, **`2025.0.4`**, and **`2026.0.1-rc-1..rc-4`** (rc-4 description: "resync from github branch develop" — the rc line IS the develop branch, published ahead of any tag).
  - Git-tagged versions all exist on the registry (1.0.7, 2025.0.0(-alpha), 2025.0.3, 2026.0.0) — no tag-without-package.
- Tarball diffs 2026.0.0 → 2026.0.1-rc-4 (extracted, listings in transcript): rc-4 **drops `ImplementationGuide.json` and `CodeSystem-MiiConsentVersionModuleCodeSystem.json`** from the package, adds `.index.json`, bumps `de.einwilligungsmanagement` 2.0.2→2.0.3. Resource versions/ids inside 2026.0.0 package match the repo XML exactly (spot-checked 5 resources — no within-release drift, unlike Studie).
- Simplifier guide URLs: pinned-context guide `https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0` → HTTP 200; `https://simplifier.net/guide/mii-ig-modul-consent-2026` (from the packaged IG resource) → HTTP 200; **the README's own guide link** (`…/guide/MedizininformatikInitiative-ModulConsent-ImplementationGuide/IGMIIKDSModulConsent`) → **HTTP 404 (dead)**. Which of the two live guides is authoritative for 2026.0.0: NICHT PRÜFBAR from repo alone (INFERENCE: the pinned one, since it carries the version query; both may be the same guide under old/new slug).

## i. Other migration-shaping observations

1. **No build scripts, no Makefile, no scripts/ — nothing executable in-repo.** The entire XML→JSON→package pipeline is Simplifier-side and invisible to git.
2. **No submodules** (no `.gitmodules`), **no LFS** (`git lfs ls-files` empty, no `.gitattributes`), **no files >50MB** (largest: `figures/MII-KDS_de_Consent_highres.tiff` 1.6MB), **all files UTF-8**, all 19 XML files well-formed (`xmllint --noout` clean).
3. **Generated-vs-source ambiguity:** `CodeSystem-MiiConsentPolicy.md` is a hand-maintained(?) markdown mirror of the Policy CodeSystem (252-line churn on develop in lockstep with the XML — evidence: develop diffstat) with extra columns ("Gültigkeit" 5/30/EINMALIG, strike-through deprecations) that are NOT fully representable in the CS → it is a parallel source, not a rendering; keeping the two in sync is manual. Similarly `figures/` mixes source (`.graphml`) and exports (`.png/.jpg/.tiff`).
4. **Draft resource inside an active release:** `CodeSystem-MiiConsentVersionModuleCodeSystem.json` is `status: draft`, version 0.2.0, and is bound in the Einwilligung profile (`Profile_MII_Consent_Einwilligung.xml:166`); rc-4 then removes it from the package while develop keeps editing it — its packaging status is actively unstable.
5. **The old XML variant** `terminologie/codesystems/CodeSystem-MiiConsentVersionModuleCodeSystem.xml` was deleted in history (git log --diff-filter=D) — format migration XML→JSON happened per-file, mid-flight (issue #101 = finish it).
6. Examples carry `<div>`-heavy narratives and mixed id styles (4 UUIDs, 1 speaking id `Example-MII-Consent-ResultType-document`).
7. Wiki enabled (`has_wiki: true`); content NICHT PRÜFBAR (not cloned — out of scope, but a possible extra narrative location).

## Summary for the migration plan

The consent module is the **inverse of an IG-Publisher repo**: tiny (14 conformance resources, 2-package dependency surface), raw-XML source, zero tooling, zero CI, zero narrative in git, bare canonical space, ART-DECOR/UUID id legacy on every resource, 2 urn:oid out-of-space canonicals, one dangling example canonical, and a live develop→rc pipeline (2026.0.1) that has already diverged from the 2026.0.0 release in package content AND dependency pin. Master==tag makes the migration baseline unambiguous; everything else (manifest, IG resource, pages, packaging behavior) must be reconstructed from Simplifier, not git.
