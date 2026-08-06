# Migration report — MII KDS Modul Consent → MII KDS module template

## L0 — Read this first (for everyone)

This module was moved from **Simplifier / Forge** onto the MII KDS module template
(`forschungsgruppe-digital-health/mii-kds-module-template` **v0.6.0**, commit `7efc8ff`),
in place, on a working branch of this repository.
**State:** complete through build, preview and pull request. Nothing published.
**Build:** SUSHI **0 errors / 9 warnings** · `qa.txt` **98 errors / 136 warnings / 482 info** —
**0 of the 98 are migration-induced**; every one is a pre-existing property of the source or of its
resource shape, each with proof in ③.
**Preview:** <https://forschungsgruppe-digital-health.github.io/mii-kds-consent-ig-inoffiziell/branches/migration/mii-kds-module-template/>
**Your job as reviewer:** work the three queues below in order — ① decide, ② review, ③ triage.
Nothing is published until Gate D; everything here is reversible.

> **This is an unofficial sandbox.** The canonical module is
> `medizininformatik-initiative/kerndatensatzmodul-consent`, which was read **read-only**
> throughout. Nothing was written to, forked from or filed against that organisation.

## Source of record

| What | Value |
|---|---|
| Source repository | `medizininformatik-initiative/kerndatensatzmodul-consent` |
| Source commit | **`4d44dbe9753807e24adc1c42b64e29ec9e95e24b`** (branch `develop`, 2026-08-06) |
| Source shape | **B** — raw FHIR resources, no `sushi-config.yaml`, no `ig.ini`, no `input/` (classified by content) |
| Published package read (tier P) | `de.medizininformatikinitiative.kerndatensatz.consent@`**`2026.0.1-rc-4`** |
| Rendered guide harvested | key `miiigmodulconsent`, version **`2026.0.0`** — *Default, Read-only, Public*, published 2025-12-18 01:17 |
| Guide root | `https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0` |
| Target template | `mii-kds-module-template` **v0.6.0** (`7efc8ff8440c945436f347e013359c59c7a3a7aa`) |
| Toolchain | goFSH 2.6.1 · SUSHI 3.20.0 · IG Publisher 2.2.11 (sha256 verified against the target workflow pin) · Jekyll 4.4.1 · validator_cli 6.10.0 |

**Which release the source commit corresponds to — measured, not assumed.** `dist-tags.latest` is
`2026.0.0`, and it is the **wrong** answer here. `MII_PR_Consent_Einwilligung` carries version
`1.0.9` in all three candidate releases, so the version string does not decide; the
`Consent.category` slice shape does:

| Artefact state | `Consent.category` slice |
|---|---|
| source `develop` @ 4d44dbe | `id=Consent.category:consentCategory`, `sliceName=loinc` |
| package `2026.0.0` | `id=Consent.category:loinc`, `sliceName=loinc` — **no match** |
| package `2026.0.1-rc-3` | `id=…:consentCategory`, `sliceName=consentCategory` — **no match** |
| package `2026.0.1-rc-4` | `id=…:consentCategory`, `sliceName=loinc` — **MATCH** |

Corroborated independently by the rc-4 manifest's own description: *"KDS Modul Consent Release
2026.0.1-rc-4 - resync from github branch develop"*. **Consequence:** the parent pin read from tier P
is `de.einwilligungsmanagement@`**`2.0.3`**, not the `2.0.2` that release 2026.0.0 pins.

## ① Decision queue (Gate A — someone must choose)

| # | Decision | Options (with consequence) | Default applied | Decide at |
|---|---|---|---|---|
| D1 | `canonical` | keep `https://www.medizininformatik-initiative.de/fhir/modul-consent` (consumers keep resolving) \| adopt the template pattern (identical here — the pattern produces the same string) | **kept source**, 12 of 12 packaged resource urls unanimous | A |
| D2 | `license` | keep source `CC-BY-4.0` \| adopt template literal `CC-BY-4.0` | **kept source**; both readings agree — recorded because agreement is a finding, not a reason it needed no check | A |
| D3 | **target `version`** | `2026.0.1-rc-4` (the source's own, but **fails** the template's CalVer gate `^\d{4}\.\d+\.\d+$`) \| `2026.0.1` (the CalVer the rc line leads to; not yet published) \| `2026.0.0` (published, but not this content) | **`2026.0.1`** — derived from the source version by dropping the prerelease label | A |
| D4 | **parent snapshots** | CI prebuild step \| vendor the rebuilt package \| internal registry \| do not re-pin and leave 3 profiles + 5 instances blocked | **re-pinned to `de.einwilligungsmanagement:2.0.3-snapshots`**, a LOCAL cache rebuild — it does **not** resolve in CI or on another machine | A |
| D5 | `{RELEASE_DATE}` | no source yields a publication date | **`2026-08-06`** — the source commit / harvest date, explicitly **not** a publication date; `go-publish.yml` validates `date == publication date`, so Gate D must reset it | A/D |
| D6 | `{APPROVAL_DATE}` | invent a governance date (forbidden) \| omit the extension | **`resource-approvalDate` REMOVED** — omitting asserts nothing; inventing would assert a governance act took place | A |
| D7 | `{TOPIC_NCI_CODE}` | guess an NCI code (a false semantic classification) \| omit the extension | **`artifact-topic` REMOVED** — the template's self-check value `C15607` is the *template's*, and basis's seven codes are *that module's* | A |
| D8 | `title` | tier R candidate `Medizininformatik Initiative - Modul Consent` \| tier I `MII IG Consent v2026` (a computer name) \| template pattern | **`MII Implementation Guide Consent`** (template pattern, tier T) | A |
| D9 | `description` | tier P `KDS Modul Consent Release 2026.0.1-rc-4 - resync from github branch develop` (a release note) \| tier R `Kerndatensatzmodul Consent` (a repo blurb) \| tier I `Medizininformatik Initiative - Modul Consent - Implementation Guide` | **tier I** — an `identity-contradiction:` is open between P and R and is **reported, not resolved** | A |
| D10 | `publisher` | no machine source carries one; the guide's *Impressum* names the MII / TMF e. V. as a **human reference** | **template literal `Medical Informatics Initiative (MII)`** | A |
| D11 | **same-module verification** | run it once the source is expressible as an IG project \| accept the hand-performed substitute | **substitute** — the mechanical check could not be triggered (see ③ and the protocol) | A |
| D12 | **example set** | ship the repository's 5 examples \| add the 6th that only the package carries (`Consent/89f494a3-…`) | **the repository's 5** | A |
| D13 | goFSH-minted ids | confirm `MII-SP-Consent-{PolicyUri,ProvisionCode,ProvisionCodePeriod,ProvisionCodeType,ProvisionPeriod,ProvisionType}` \| choose others | **confirmed as minted** — the six SearchParameters carry **no id** in the source *and none in the published package* | A |
| D14 | template `$sct` pin | keep the module's `$sct = http://snomed.info/sct` \| adopt the template's version-pinned `…\|…/version/20250701` | **kept the module's** — the module's FSH is never changed | A |
| D15 | dropped template dependencies | keep `de.basisprofil.r4`, `…kerndatensatz.meta`, `hl7.fhir.uv.xver-r5.r4` \| drop them | **dropped** — the source declares none and the module FSH references none | A |
| D16 | guide currency | accept a narrative one release line behind the resources \| publish a matching guide first | **accepted, flagged** — harvesting `?version=current` is forbidden (not reproducible) | B |

## ② Review queue (Gates B/C — someone must check)

| Where | What to check | Suggested action | Gate |
|---|---|---|---|
| `input/pagecontent/*.md` (10 pages) | **machine translation** against the German original of the same name under `input/translations/de/pagecontent/` | correct the wording, remove the `TODO:REVIEW` header | C |
| `input/intro-notes/*-intro.md` (3) | machine translation of the per-profile prose | same | C |
| `input/pagecontent/terminology.md`, `changes.md` | the explanatory notes and release notes are **still German** inside the English page — deliberate, and marked | decide whether to translate | C |
| `input/pagecontent/general-requirements.md` | the source's *Anwendungsfälle* page is **empty in the published guide**; the gap is recorded, not filled | decide whether to write it | B |
| `researcher-guidance.md`, `missing-data.md`, `capability-statements.md`, `logical-models.md` (both languages) | **RECORDED GAPS** — still the template's starter text, each stamped with a banner saying why | write or remove the page | B |
| `general-requirements.md` vs `implementer-guidance.md` | which page is the right home for the **scenario narratives** (spec §9 says reviewers reasonably disagree) | confirm the routing | B |
| 4 harvested **artefact-view** pages | `generated-view-lossy:` on Terminologien (8 runs), Consent (8), Provenance (4), DocumentReference (2) — losses inside *rendered* trees the publisher regenerates | confirm nothing narrative was lost | B |
| all migrated pages | links and images are still **absolute to simplifier.net / raw.githubusercontent.com** (3 assets in `migration-log/guide-harvest-assets.tsv`) | decide whether to vendor the images | B |
| `input/fsh/instances/*.fsh` | 4 GUID-named files goFSH wrote for resources whose ids are GUIDs **in the source** | confirm | A |

## ③ QA triage (what the build says, and whose problem it is)

`qa.txt`: **err = 98, warn = 136, info = 482**. Every ERROR line is classified; **none is
migration-induced**.

| Finding (shortened) | Count | Provenance (proof) | Next action |
|---|---|---|---|
| `Slicing cannot be evaluated: Could not match discriminator ($this)` on `Consent.category` | 17 | **pre-existing, proven**: validating the *published package's own* 6 examples against the *published package* with `validator_cli 6.10.0` — no template, no migration — yields **30** of the same. Root cause read out of the source XML: `<element id="Consent.category:consentCategory">` carries `<sliceName value="loinc"/>` — id and slice name disagree | escalate to the module maintainers |
| `Wrong Display Name` for a policy code | 12 | **pre-existing, proven** — 18 in the same baseline | escalate |
| `None of the codings provided are in the value set` (MII Consent: Policy ValueSet) | 12 | **pre-existing, proven** — 18 in the same baseline | escalate |
| `Unable to resolve resource with reference 'Patient/…' \| 'ResearchStudy/…'` | 8 | **source property**: the examples reference pseudonymous resources the module deliberately does not ship (the Consent resource carries no person-identifying data). Not reproduced by the standalone baseline because reference resolution is IG-context-dependent — stated, not claimed as proven | accept, or ship contained/example Patient stubs (a maintainer decision) |
| `does not match the URL` / `Resource id/url mismatch` / `URL Mismatch` | 46 | **source shape**: the published resource **ids** are GUIDs and OIDs while their **urls** end in `mii-pr-consent-*` / `mii-vs-consent-*`. Verified id-by-id against the published package: identical. Guardrail 1 forbids changing either | Gate A: adopt the publisher's `special-url` parameter, or escalate upstream |
| `CodeSystem.count` vs actual concept count | 2 | **source shape** — SUSHI reports the same as warnings (`^count 20` vs 21 concepts; `101` vs 124) | escalate |
| implicit all-codes ValueSet on a CodeSystem | 1 | **source shape** | escalate |
| `Broken Links: 2` in the publisher summary | 2 | **unclassified** — the same run's HTML link check reports `121865 links, 0 broken links (0%)` and `qa.txt` lists no unresolved-link error | triage before Gate D |
| *(fixed during the run)* `The link 'Patient-ExamplePatientInstance.html' … cannot be resolved` | was 2 | **migration-induced** — the template's `examples.md` starter text linked the example artefact guardrail 5 deletes | **fixed**: `examples.md` rewritten to the module's own five examples; re-measured, gone |

## Content map (where every source page went)

**Narrative source (spec §5.1d):** the **guide harvest** (source ②). Source ① — the authenticated
project download — was **unavailable**: it requires a Simplifier login, this run was
non-interactive, and no human supplied an archive (`project-download-unavailable:`). It remains the
better source and a later run should prefer it.

`migration-log/guide-harvest.tsv`: **18 discovered, 18 harvested, 0 skipped** (14 narrative,
4 artefact-view), **0 narrative pages short**, 3 referenced assets, guide version `2026.0.0`.

| Harvested page | Title | Kind | Home in the template page set | Anything lost? |
|---|---|---|---|---|
| `index.md` | Kerndatensatz-Modul Consent | narrative | index.md (+ its German mirror) — module intro, imprint, authors, copyright | none |
| `release-notes.md` | Release Notes | narrative | changes.md — the Changelog page | none |
| `beschreibung-modul-consent.md` | Beschreibung Modul Consent | narrative | index.md § Introduction (the module summary) | none |
| `kontextimgesamtprojektbezgezuanderenmodulen.md` | Kontext im Gesamtprojekt / Bezüge zu anderen Modulen | narrative | implementer-guidance.md § Context within the overall project | none |
| `referenzen.md` | Referenzen | narrative | implementer-guidance.md § References | none |
| `anwendungsflleinformationsmodell.md` | Anwendungsfälle / Informationsmodell | narrative | general-requirements.md § Use cases (RECORDED GAP — the source page is empty) | none |
| `anwendungsflleinformationsmodell-beschreibungvonszenarienfrdieanwendungdesmoduls.md` | Beschreibung von Szenarien für die Anwendung des Moduls | narrative | general-requirements.md § Description of scenarios | none |
| `anwendungsflleinformationsmodell-datenstzeinkl.beschreibungen.md` | Datensätze inkl. Beschreibungen | narrative | datasets-and-descriptions.md § Datasets and descriptions | none |
| `anwendungsflleinformationsmodell-uml.md` | UML | narrative | uml-diagrams.md | none |
| `anwendungsflleinformationsmodell-fragebgen.md` | Fragebögen | narrative | datasets-and-descriptions.md § Questionnaires | none |
| `technischeimplementierung.md` | Technische Implementierung | narrative | conformance.md; its search-parameter paragraphs -> search-parameters-and-operations.md | none |
| `technischeimplementierung-fhirprofile.md` | FHIR Profile | narrative | profiles-and-extensions.md; its must-support section -> must-support.md | none |
| `technischeimplementierung-fhirprofile-consent.md` | Consent | artefact-view | input/intro-notes/StructureDefinition-e0e166b4-…-intro.md; its Datenschutz section -> security-and-privacy.md | **8 text run(s)** — rendered artefact view, regenerated by the publisher from the resource |
| `technischeimplementierung-fhirprofile-provenance.md` | Provenance | artefact-view | input/intro-notes/StructureDefinition-f675b1e8-…-intro.md | **4 text run(s)** — rendered artefact view, regenerated by the publisher from the resource |
| `technischeimplementierung-fhirprofile-documentreference.md` | DocumentReference | artefact-view | input/intro-notes/StructureDefinition-56375452-…-intro.md | **2 text run(s)** — rendered artefact view, regenerated by the publisher from the resource |
| `technischeimplementierung-fhirprofile-weitererelevanteprofile.md` | Weitere relevante Profile | narrative | profiles-and-extensions.md § Further relevant profiles | none |
| `technischeimplementierung-fhirprofile-empfehlungen-zur-praktischen-anwendung.md` | Empfehlungen zur praktischen Anwendung | narrative | implementer-guidance.md § Recommendations for practical use | none |
| `technischeimplementierung-terminologien.md` | Terminologien | artefact-view | terminology.md | **8 text run(s)** — rendered artefact view, regenerated by the publisher from the resource |

**Recorded gaps — pages that are still the template's starter text**, each carrying a banner in both
languages: `researcher-guidance.md`, `missing-data.md`, `capability-statements.md`,
`logical-models.md`. Plus `general-requirements.md` § *Use cases*, where the **source guide's own
page is empty**. `downloads.md`, `version-history.md`, `translationinfo.md`, `metadata.md`,
`guidance.md` and `conformance.md` carry the template's generic scaffolding by design.
The template's demonstration page `rendering-artifacts.md` was **deleted** (both languages, the
`pages:` entry and both menu entries).

## Identity (what makes this module *this* module — verified unchanged)

- **Canonical** `https://www.medizininformatik-initiative.de/fhir/modul-consent` — derived from the
  packaged resources' own urls, **12 of 12 unanimous**, carried over unchanged (guardrail 1).
- **Every resource id** was compared one by one against the published package and is identical.
  The three StructureDefinition ids are GUIDs (`e0e166b4-…`, `f675b1e8-…`, `56375452-…`) — those are
  the **source's own** `<id>` elements, not something goFSH minted.
- goFSH minted ids for the **six SearchParameters only**, which carry no id in the source *or* in
  the published package. → ① D13.
- **Nothing existing was rewritten from a recovered value.**

### Where each value came from (generated — do not retype)

| Field | Tier | Source | Value | Contradiction |
| --- | --- | --- | --- | --- |
| packageId | P | package/package.json | de.medizininformatikinitiative.kerndatensatz.consent |  |
| version | P | package/package.json | 2026.0.1-rc-4 |  |
| description | P | package/package.json | KDS Modul Consent Release 2026.0.1-rc-4 - resync from github branch develop | YES -- Gate A |
| fhirVersions | P | package/package.json | ["4.0.1"] |  |
| jurisdiction | P | package/package.json | urn:iso:std:iso:3166#DE |  |
| dependency:de.einwilligungsmanagement | P | package/package.json (source pin) | 2.0.3 |  |
| dependency:hl7.fhir.r4.core | P | package/package.json (source pin) | 4.0.1 |  |
| canonical | P | packaged resource urls (12 of 12 agree) | https://www.medizininformatik-initiative.de/fhir/modul-consent |  |
| title | R | README.md first heading | Medizininformatik Initiative - Modul Consent |  |
| license | R | LICENSE (text matched) | CC-BY-4.0 |  |
| description | R | GitHub repository description | Kerndatensatzmodul Consent | YES -- Gate A |
| license | R | GitHub license.spdx_id | CC-BY-4.0 |  |

> One `identity-contradiction:` is open (`description`, tier P vs tier R). It is **reported, not
> resolved** — `migration-log.sh claims` exits 1 while it stands. → ① D9.
> `title`, `license` and `publisher` are the fields a FHIR package manifest has no place for;
> `license` was recovered from the LICENSE text (tier R) and `publisher` was not recoverable from a
> repository at all.

## Protocol (what was executed — for auditors; keep last)

**Generated from `migration-log/run.log`** (231 events across 21 steps —
23 WARN, 4 ERROR), not from recollection. Where this report and the log disagree, the
log is right. Read the log back with
`grep -E '  (WARN |ERROR)  ' migration-log/run.log`.

### Step `pre.2`

- `classify-source-shape` — shape=B resources=20 xml=19 json=1 dirs=5 src_commit=4d44dbe9753807e24adc1c42b64e29ec9e95e24b

> **Acceptance:** met — shape B recorded by content (20 resources, 19 XML + 1 JSON, 5 hand-named dirs)

### Step `pre.3`

- `target-template` — state=plain-Forge-repo (no ig-template/, no ig.ini) -> the normal starting state for a shape-B module; this is a FIRST migration, not a re-migration

> **Acceptance:** met — target template read at the ref actually used (v0.6.0 / 7efc8ff)

### Step `pre.5`

- `toolchain` — node=v22.22.3 npx=10.9.8 python3=3.14.4 java=25.0.2 docker=29.6.2

> **Acceptance:** met — SUSHI and goFSH invoked only as version-pinned npx

### Step `2.1`

- `package-identity` — params  package=de.medizininformatikinitiative.kerndatensatz.consent version=2026.0.1-rc-4 registry=https://packages.simplifier.net work=/var/folders/d6/s255vt4x5pq9fy738bv7cs0h0000gq/T/tmp.irLwMdoHtB
- `package-identity` — version supplied by the operator  version=2026.0.1-rc-4 source=--version package=de.medizininformatikinitiative.kerndatensatz.consent
- `package-identity` — fetched  cmd=`curl -sfL https://packages.simplifier.net/de.medizininformatikinitiative.kerndatensatz.consent/2026.0.1-rc-4 -o pkg.tgz && tar xzf pkg.tgz`  bytes=68884 json_files=20 manifest=package/package.json
- `package-identity` — manifest field  name=de.medizininformatikinitiative.kerndatensatz.consent  -- = packageId (spec §2.1)
- `package-identity` — identity-claim  field=packageId value=de.medizininformatikinitiative.kerndatensatz.consent tier=P source=package/package.json
- `package-identity` — manifest field  version=2026.0.1-rc-4  -- the module version -- authoritative for this RELEASE
- `package-identity` — identity-claim  field=version value=2026.0.1-rc-4 tier=P source=package/package.json
- `package-identity` — manifest field  description=KDS Modul Consent Release 2026.0.1-rc-4 - resync from github branch develop
- `package-identity` — identity-claim  field=description value=KDS Modul Consent Release 2026.0.1-rc-4 - resync from github branch develop tier=P source=package/package.json
- `package-identity` — manifest field  fhirVersions=["4.0.1"]
- `package-identity` — identity-claim  field=fhirVersions value=["4.0.1"] tier=P source=package/package.json
- `package-identity` — manifest field  jurisdiction=urn:iso:std:iso:3166#DE
- `package-identity` — identity-claim  field=jurisdiction value=urn:iso:std:iso:3166#DE tier=P source=package/package.json
- `package-identity` — manifest field  author=sebastianstaeubert  -- a REGISTRY ACCOUNT, not `publisher`
- `package-identity` — manifest read  package/package.json  recovered=6 absent=5 fields=name,version,description,fhirVersions,jurisdiction,author
- **WARN** `package-identity` — not-in-a-package-manifest: title, license, publisher
- `package-identity` — manifest fields absent (optional in this format)  canonical, homepage
- `package-identity` — identity-claim  field=dependency:de.einwilligungsmanagement value=2.0.3 tier=P source=package/package.json (source pin)
- `package-identity` — identity-claim  field=dependency:hl7.fhir.r4.core value=4.0.1 tier=P source=package/package.json (source pin)
- `package-identity` — dependency pins from the SOURCE package  de.einwilligungsmanagement@2.0.3 hl7.fhir.r4.core@4.0.1
- `package-identity` — urls excluded from the canonical derivation  count=2
- `package-identity` — packaged resources carrying no url  count=6
- `package-identity` — identity-claim  field=canonical value=https://www.medizininformatik-initiative.de/fhir/modul-consent tier=P source=packaged resource urls (12 of 12 agree)
- `package-identity` — canonical derived by common prefix  canonical=https://www.medizininformatik-initiative.de/fhir/modul-consent agree=12 of 12
- `package-identity` — done  package=de.medizininformatikinitiative.kerndatensatz.consent version=2026.0.1-rc-4  canonical=derived exit=0
- `repo-identity` — params  dir=/tmp/consent-mig-57425/source-consent-readonly repo=medizininformatik-initiative/kerndatensatzmodul-consent rendered=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0
- `repo-identity` — identity-claim  field=title value=Medizininformatik Initiative - Modul Consent tier=R source=README.md first heading
- `repo-identity` — identity-claim  field=license value=CC-BY-4.0 tier=R source=LICENSE (text matched)
- `repo-identity` — identity-claim  field=description value=Kerndatensatzmodul Consent tier=R source=GitHub repository description
- **WARN** `repo-identity` — identity-contradiction: field=description  now=Kerndatensatzmodul Consent (tier R, GitHub repository description)  vs  description=KDS Modul Consent Release 2026.0.1-rc-4 - resync from github branch develop (tier P, package/package.json)
- `repo-identity` — identity-claim  field=license value=CC-BY-4.0 tier=R source=GitHub license.spdx_id
- **WARN** `repo-identity` — not-recoverable-from-a-repository: publisher  owner=medizininformatik-initiative
- `repo-identity` — release tags on GitHub (newest first)  tags=2026.0.0 2025.0.3 2025.0.0 2025.0.0-alpha 1.0.7
- `repo-identity` — rendered page probed  cmd=`curl -sL https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0`  http=200 bytes=24509 script_markers=5 identity_markers=0 guide_page_links=18
- `repo-identity` — server-rendered-guide: this URL space DOES deliver content  http=200 bytes=24509 guide_page_links=18 url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0
- `repo-identity` — done  fields_recovered=4 exit=0

> **Acceptance:** met — every field recorded with its tier and source; one contradiction reported, not resolved

### Step `2.1.1`

- `release-identification` — the migrated source commit corresponds to prerelease 2026.0.1-rc-4, NOT to dist-tags.latest 2026.0.0
- **WARN** `release-identification` — the pinned release is a PRERELEASE (2026.0.1-rc-4) — Gate A confirms that migrating the development branch against a prerelease manifest is intended
- `release-identification` — CORROBORATION, independent of the slicing test: the rc-4 manifest's own description reads 'KDS Modul Consent Release 2026.0.1-rc-4 - resync from github branch develop'

> **Acceptance:** met — the release the source commit corresponds to identified by measurement, not by dist-tags.latest

### Step `2.2`

- **WARN** `unsourced-identity` — resolution of the three placeholders NO source tier yields — chosen to avoid BOTH fabrication and a dead build; every one is a decision-queue item

> **Acceptance:** MET AS QUALIFIED — three values no tier yields; two extensions removed rather than fabricated, one provisional date recorded. All three are ① items.

### Step `5.1b.2`

- `gofsh-input` — inputs=20 src=/tmp/consent-mig-57425/source-consent-readonly
- `gofsh-convert` — start  cmd=`npx --yes gofsh@2.6.1 /tmp/consent-mig-57425/source-consent-readonly -o /tmp/consent-mig-57425/gofsh-out -s file-per-definition -t json-and-xml -d de.einwilligungsmanagement@2.0.3 -d hl7.fhir.r4.core@4.0.1`  raw_log=migration-log/gofsh.log
- `gofsh-convert` — done  cmd=`npx --yes gofsh@2.6.1 /tmp/consent-mig-57425/source-consent-readonly -o /tmp/consent-mig-57425/gofsh-out -s file-per-definition -t json-and-xml -d de.einwilligungsmanagement@2.0.3 -d hl7.fhir.r4.core@4.0.1`  exit=0 raw_log=migration-log/gofsh.log raw_log_lines=98
- `gofsh-convert` — goFSH RESULTS table (of 1 in the log, the last) profiles=3 extensions=0 logicals=0 resources=0 valuesets=3 codesystems=3 instances=11 invariants=0 mappings=0 aliases=7  converted=20 counted=profiles+extensions+logicals+resources+valuesets+codesystems+instances not_counted=invariants,mappings,aliases  gofsh_log=migration-log/gofsh.log
- `gofsh-convert` — converted 20 of 20 inputs  expected=20 actual=20 exit=0

> **Acceptance:** met — converted 20 of 20 inputs, no unresolved-parent warning, -t json-and-xml and the source -d pins used

### Step `5.1b.3`

- `sushi-before` — start  cmd=`bash -c 'cd '\''/tmp/consent-mig-57425/gofsh-out'\'' && npx --yes fsh-sushi@3.20.0 .'`  raw_log=migration-log/sushi-before.log
- **ERROR** `sushi-before` — failed  cmd=`bash -c 'cd '\''/tmp/consent-mig-57425/gofsh-out'\'' && npx --yes fsh-sushi@3.20.0 .'`  exit=11 raw_log=migration-log/sushi-before.log raw_log_lines=86
- `sushi-before` — errors=11
- `postprocess-gofsh` — start  cmd=`python3 /tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/scripts/postprocess-gofsh.py /tmp/consent-mig-57425/gofsh-out/input/fsh --gofsh-log migration-log/gofsh.log`  raw_log=migration-log/postprocess-gofsh.log
- `postprocess-gofsh` — params  fsh_dir=/tmp/consent-mig-57425/gofsh-out/input/fsh dry_run=False drop_comments=False
- `postprocess-gofsh` — scan  files=21 entities_declared=27 gofsh_log=migration-log/gofsh.log renames_reported=1
- `postprocess-gofsh` — /tmp/consent-mig-57425/gofsh-out/input/fsh/instances/34150a23-b1c8-404f-874f-e042a30435d2.fsh  changes=34
- `postprocess-gofsh` — /tmp/consent-mig-57425/gofsh-out/input/fsh/instances/5143266b-8d60-4b28-8ee9-635140ffa5bb.fsh  changes=27
- `postprocess-gofsh` — /tmp/consent-mig-57425/gofsh-out/input/fsh/instances/55219d12-6245-4de4-8b50-ddf6f16a789b.fsh  changes=8
- `postprocess-gofsh` — /tmp/consent-mig-57425/gofsh-out/input/fsh/instances/8a3d1799-2463-405e-b49c-6a16c8692b01.fsh  changes=3
- `postprocess-gofsh` — /tmp/consent-mig-57425/gofsh-out/input/fsh/instances/Example-MII-Consent-ResultType-document.fsh  changes=20
- `postprocess-gofsh` — result  fhir_comments=53 (preserved as FSH comments) code_references=39 changed=5 of 21 file(s)  exit=0
- `postprocess-gofsh` — next: run `npx --yes fsh-sushi@3.20.0 .`; remaining errors are NOT mechanical
- `postprocess-gofsh` — done  cmd=`python3 /tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/scripts/postprocess-gofsh.py /tmp/consent-mig-57425/gofsh-out/input/fsh --gofsh-log migration-log/gofsh.log`  exit=0 raw_log=migration-log/postprocess-gofsh.log raw_log_lines=105
- `postprocess-gofsh` — acceptance: exit status  exit=  (0 required)
- `sushi-after` — start  cmd=`bash -c 'cd '\''/tmp/consent-mig-57425/gofsh-out'\'' && npx --yes fsh-sushi@3.20.0 .'`  raw_log=migration-log/sushi-after.log
- **WARN** `sushi-after` — anticipated-nonzero-exit: shape B: unresolvable parents are a Gate-A escalation (§5.1b.4)  cmd=`bash -c 'cd '\''/tmp/consent-mig-57425/gofsh-out'\'' && npx --yes fsh-sushi@3.20.0 .'`  exit=8 raw_log=migration-log/sushi-after.log raw_log_lines=77
- `sushi-after` — errors=8 resolved=3  before=11
- `postprocess-gofsh` — correction to the preceding line, whose exit token was emitted empty by the caller's shell: postprocess-gofsh.py exited 0, as its own 'done' line records (raw_log=migration-log/postprocess-gofsh.log)
- `sushi-before` — DIVERGENCE from the spec's reference measurement (41 -> 5): this run measures 11 -> 8
- `sushi-control-unrepaired` — start  cmd=`bash -c 'cd '\''/tmp/consent-mig-unrepaired'\'' && npx --yes fsh-sushi@3.20.0 .'`  raw_log=migration-log/sushi-control-unrepaired.log
- **WARN** `sushi-control-unrepaired` — anticipated-nonzero-exit: control measurement: the unrepaired FSH is expected to fail — this run exists to count HOW MUCH  cmd=`bash -c 'cd '\''/tmp/consent-mig-unrepaired'\'' && npx --yes fsh-sushi@3.20.0 .'`  exit=50 raw_log=migration-log/sushi-control-unrepaired.log raw_log_lines=233
- `sushi-control-unrepaired` — CONTROL RESULT errors=50

> **Acceptance:** MET AS QUALIFIED (spec 5.1b.4) — mechanical defects repaired; residual errors were unresolvable parents only

### Step `5.1b.5`

- `parent-snapshots` — params  mode=detect package=de.einwilligungsmanagement version=2.0.3 registry=https://packages.simplifier.net fhir_version=4.0.1
- `parent-snapshots` — surveyed  structure_definitions=21 with_snapshot=0 without_snapshot=21
- **WARN** `parent-snapshots` — parent-without-snapshots: 21 of 21 StructureDefinitions carry NO snapshot
- `parent-snapshots` — derivation chain is flat: every SD derives directly from outside this package  count=21
- `parent-snapshots` — done  mode=detect missing_snapshots=21 of 21 exit=1
- `parent-snapshots` — params  mode=build package=de.einwilligungsmanagement version=2.0.3 registry=https://packages.simplifier.net fhir_version=4.0.1
- `parent-snapshots` — surveyed  structure_definitions=21 with_snapshot=0 without_snapshot=21
- **WARN** `parent-snapshots` — parent-without-snapshots: 21 of 21 StructureDefinitions carry NO snapshot
- `parent-snapshots` — derivation chain is flat: every SD derives directly from outside this package  count=21
- `parent-snapshots` — base package for the element-count floor  base_dir=/Users/marcel/.fhir/packages/hl7.fhir.r4.core#4.0.1/package
- `parent-snapshots` — generating with the OFFICIAL HL7 generator  validator=/tmp/validator_cli_6.10.0.jar java="openjdk version "25.0.2" 2026-01-20" fhir_version=4.0.1
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-ConsentMode.json snapshot=12 differential=5 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-ContextIdentifier.json snapshot=20 differential=12 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-DomainReference.json snapshot=22 differential=11 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-Logo.json snapshot=5 differential=2 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-OrganizationDescription.json snapshot=5 differential=2 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-SignatureLocation.json snapshot=5 differential=2 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-SourceDocument.json snapshot=15 differential=4 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-SubQuestionnaire.json snapshot=11 differential=6 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-VersionFormat.json snapshot=15 differential=10 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-Xacml.json snapshot=5 differential=2 base=5
- `parent-snapshots` — snapshot verified and merged  file=extension-ConsentManagement-XacmlTemplate.json snapshot=15 differential=9 base=5
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagement-Consent.json snapshot=132 differential=32 base=57
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagement-DocumentReference.json snapshot=61 differential=8 base=45
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagement-Domain-Organization.json snapshot=91 differential=23 base=26
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagement-Domain-ResearchStudy.json snapshot=104 differential=23 base=44
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagement-Patient.json snapshot=64 differential=7 base=45
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagement-Provenance.json snapshot=65 differential=20 base=32
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagement-TemplateFrame.json snapshot=163 differential=58 base=65
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagement-TemplateModule.json snapshot=111 differential=28 base=65
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagementQuestionnaireComposed.json snapshot=152 differential=52 base=65
- `parent-snapshots` — snapshot verified and merged  file=profile-ConsentManagementQuestionnaireResponse.json snapshot=39 differential=14 base=33
- `parent-snapshots` — rebuild written  dir=/var/folders/d6/s255vt4x5pq9fy738bv7cs0h0000gq/T/tmp.s4b5NF1iWR/rebuilt/package merged=21 refused=0
- `parent-snapshots` — generated 21 of 21 snapshots  expected=21 actual=21
- `parent-snapshots` — required parent snapshotted  require=http://fhir.de/ConsentManagement/StructureDefinition/DocumentReference file=profile-ConsentManagement-DocumentReference.json
- `parent-snapshots` — required parent snapshotted  require=http://fhir.de/ConsentManagement/StructureDefinition/Consent file=profile-ConsentManagement-Consent.json
- `parent-snapshots` — required parent snapshotted  require=http://fhir.de/ConsentManagement/StructureDefinition/Provenance file=profile-ConsentManagement-Provenance.json
- `parent-snapshots` — installed as a NEW cache entry  dest=/Users/marcel/.fhir/packages/de.einwilligungsmanagement#2.0.3-snapshots version=2.0.3-snapshots
- `parent-snapshots` — done  mode=build generated=21 of 21 required=all-snapshotted exit=0
- `parent-snapshots` — params  mode=detect package=de.einwilligungsmanagement version=2.0.3 registry=https://packages.simplifier.net fhir_version=4.0.1
- `parent-snapshots` — surveyed  structure_definitions=21 with_snapshot=0 without_snapshot=21
- **WARN** `parent-snapshots` — parent-without-snapshots: 21 of 21 StructureDefinitions carry NO snapshot
- `parent-snapshots` — derivation chain is flat: every SD derives directly from outside this package  count=21
- `parent-snapshots` — done  mode=detect missing_snapshots=21 of 21 exit=1
- `sushi-after-snapshots` — start  cmd=`bash -c 'cd '\''/tmp/consent-mig-57425/gofsh-out'\'' && npx --yes fsh-sushi@3.20.0 .'`  raw_log=migration-log/sushi-after-snapshots.log
- `sushi-after-snapshots` — done  cmd=`bash -c 'cd '\''/tmp/consent-mig-57425/gofsh-out'\'' && npx --yes fsh-sushi@3.20.0 .'`  exit=0 raw_log=migration-log/sushi-after-snapshots.log raw_log_lines=71
- `sushi-after-snapshots` — errors=0 before_repin=8 resolved=8 raw_log=migration-log/sushi-after-snapshots.log

> **Acceptance:** met — 21 of 21 snapshots generated with the official HL7 generator, 0 refused, upstream re-verified untouched; SUSHI 8 -> 0

### Step `5.1c`

- `simplifier-discover` — params  base=https://simplifier.net org=koordinationsstellemii module=consent package=<none> project=<none> guide=<none> pin=<propose> out=migration-log
- `simplifier-discover` — hop 1 org project list  cmd=`curl -sL https://simplifier.net/organization/koordinationsstellemii/~projects`  http=200 bytes=142233 packages=23
- `simplifier-discover` — hop 1b module resolved  module=consent package=de.medizininformatikinitiative.kerndatensatz.consent
- `simplifier-discover` — hop 2 package -> project  cmd=`curl -sL https://simplifier.net/packages/de.medizininformatikinitiative.kerndatensatz.consent/latest`  http=200 package=de.medizininformatikinitiative.kerndatensatz.consent project=medizininformatikinitiative-modulconsent
- `simplifier-discover` — hop 3 project -> guide keys  cmd=`curl -sL https://simplifier.net/medizininformatikinitiative-modulconsent/filterprojectguides`  http=200 bytes=4657 keys=3
- `simplifier-discover` — hop 4 guide versions  cmd=`curl -sL https://simplifier.net/published-guide/mii-ig-modul-consent-2025/versions`  http=200 key=mii-ig-modul-consent-2025 published=5 preview=0
- `simplifier-discover` — hop 4 proposed pin  key=mii-ig-modul-consent-2025 version=2025.0.4 reason=flagged Default
- `simplifier-discover` — hop 5 guide pages  cmd=`curl -sL 'https://simplifier.net/guide/mii-ig-modul-consent-2025?version=2025.0.4'`  http=200 bytes=20803 key=mii-ig-modul-consent-2025 version=2025.0.4 root=MII-IG-Modul-Consent pages=16 out=migration-log/simplifier-pages-mii-ig-modul-consent-2025-2025.0.4.tsv
- `simplifier-discover` — hop 4 guide versions  cmd=`curl -sL https://simplifier.net/published-guide/mii-ig-modul-consent-2026/versions`  http=200 key=mii-ig-modul-consent-2026 published=1 preview=0
- `simplifier-discover` — hop 4 proposed pin  key=mii-ig-modul-consent-2026 version=2026.0.0 reason=flagged Default
- `simplifier-discover` — hop 5 guide pages  cmd=`curl -sL 'https://simplifier.net/guide/mii-ig-modul-consent-2026?version=2026.0.0'`  http=200 bytes=22966 key=mii-ig-modul-consent-2026 version=2026.0.0 root=MII-IG-Modul-Consent pages=18 out=migration-log/simplifier-pages-mii-ig-modul-consent-2026-2026.0.0.tsv
- `simplifier-discover` — hop 4 guide versions  cmd=`curl -sL https://simplifier.net/published-guide/miiigmodulconsent/versions`  http=200 key=miiigmodulconsent published=1 preview=1
- `simplifier-discover` — hop 4 proposed pin  key=miiigmodulconsent version=2026.0.0 reason=flagged Default
- `simplifier-discover` — hop 5 guide pages  cmd=`curl -sL 'https://simplifier.net/guide/miiigmodulconsent?version=2026.0.0'`  http=200 bytes=22616 key=miiigmodulconsent version=2026.0.0 root=MIIIGModulConsent pages=18 out=migration-log/simplifier-pages-miiigmodulconsent-2026.0.0.tsv
- `simplifier-discover` — done  pages=52 guides=migration-log/simplifier-guides.tsv exit=0

> **Acceptance:** met — guide discovered from an org key and a module name; a PUBLISHED, read-only version pinned

### Step `5.1d`

- `guide-harvest` — guide root fetched  cmd=`curl -sL https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0`  http=200 bytes=24509
- `guide-harvest` — page tree discovered from the root's own hrefs  discovered=18 region_id=preview-content
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/index.md  region=found kind=narrative src_text_chars=2806 md_text_chars=4667 missing_runs=0 internal_links=13 images=1 artefact_markers=0 title=Kerndatensatz-Modul Consent
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/Release-Notes?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/release-notes.md  region=found kind=narrative src_text_chars=3662 md_text_chars=4124 missing_runs=0 internal_links=0 images=0 artefact_markers=0 title=Release Notes
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/Beschreibung-Modul-Consent?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/beschreibung-modul-consent.md  region=found kind=narrative src_text_chars=680 md_text_chars=1168 missing_runs=0 internal_links=0 images=1 artefact_markers=0 title=Beschreibung Modul Consent
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/KontextimGesamtprojektBezgezuanderenModulen?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/kontextimgesamtprojektbezgezuanderenmodulen.md  region=found kind=narrative src_text_chars=858 md_text_chars=1094 missing_runs=0 internal_links=0 images=0 artefact_markers=0 title=Kontext im Gesamtprojekt / B
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/Referenzen?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/referenzen.md  region=found kind=narrative src_text_chars=613 md_text_chars=1083 missing_runs=0 internal_links=0 images=0 artefact_markers=0 title=Referenzen
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/anwendungsflleinformationsmodell.md  region=found kind=narrative src_text_chars=81 md_text_chars=84 missing_runs=0 internal_links=0 images=0 artefact_markers=0 title=Anwendungsfälle / Informationsmodell
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/BeschreibungvonSzenarienfrdieAnwendungdesModuls?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/anwendungsflleinformationsmodell-beschreibungvonszenarienfrdieanwendungdesmoduls.md  region=found kind=narrative src_text_chars=1407 md_text_chars=1640 missing_runs=0 inte
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/Datenstzeinkl.Beschreibungen?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/anwendungsflleinformationsmodell-datenstzeinkl.beschreibungen.md  region=found kind=narrative src_text_chars=384 md_text_chars=604 missing_runs=0 internal_links=0 images=0 artefact_markers=0
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/UML?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/anwendungsflleinformationsmodell-uml.md  region=found kind=narrative src_text_chars=1861 md_text_chars=2913 missing_runs=0 internal_links=5 images=1 artefact_markers=0 title=UML
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/Fragebgen?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/anwendungsflleinformationsmodell-fragebgen.md  region=found kind=narrative src_text_chars=2094 md_text_chars=3293 missing_runs=0 internal_links=1 images=0 artefact_markers=0 title=Fragebögen
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/technischeimplementierung.md  region=found kind=narrative src_text_chars=731 md_text_chars=773 missing_runs=0 internal_links=0 images=0 artefact_markers=0 title=Technische Implementierung
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile.md  region=found kind=narrative src_text_chars=760 md_text_chars=895 missing_runs=0 internal_links=0 images=0 artefact_markers=0 title=FHIR Profile
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-consent.md  region=found kind=artefact-view src_text_chars=239875 md_text_chars=423755 missing_runs=8 internal_links=0 images=0 artefact_markers=2171 title=Consent
- `guide-harvest` — rendered-artefact-view: this page is a RENDERING of a conformance resource, not narrative  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0 file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-consent.md src_text_chars=239875
- **WARN** `guide-harvest` — generated-view-lossy: 8 text run(s) of a RENDERED ARTEFACT VIEW did not survive the conversion  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0 file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-consent.md src_text_chars=239875 md_text_chars=423755
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Provenance?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-provenance.md  region=found kind=artefact-view src_text_chars=73477 md_text_chars=102418 missing_runs=4 internal_links=1 images=0 artefact_markers=397 title=Provenan
- `guide-harvest` — rendered-artefact-view: this page is a RENDERING of a conformance resource, not narrative  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Provenance?version=2026.0.0 file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-provenance.md src_text_chars=73477
- **WARN** `guide-harvest` — generated-view-lossy: 4 text run(s) of a RENDERED ARTEFACT VIEW did not survive the conversion  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Provenance?version=2026.0.0 file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-provenance.md src_text_chars=73477 md_text_chars=102418
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/DocumentReference?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-documentreference.md  region=found kind=artefact-view src_text_chars=74149 md_text_chars=101637 missing_runs=2 internal_links=0 images=0 artefact_markers=359 
- `guide-harvest` — rendered-artefact-view: this page is a RENDERING of a conformance resource, not narrative  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/DocumentReference?version=2026.0.0 file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-documentreference.md src_text_chars=74149
- **WARN** `guide-harvest` — generated-view-lossy: 2 text run(s) of a RENDERED ARTEFACT VIEW did not survive the conversion  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/DocumentReference?version=2026.0.0 file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-documentreference.md src_text_chars=74149 md_text_chars=101637
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/WeitererelevanteProfile?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-weitererelevanteprofile.md  region=found kind=narrative src_text_chars=892 md_text_chars=1959 missing_runs=0 internal_links=3 images=0 artefact_markers=
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Empfehlungen-zur-praktischen-Anwendung?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/technischeimplementierung-fhirprofile-empfehlungen-zur-praktischen-anwendung.md  region=found kind=narrative src_text_chars=2960 md_text_chars=3440 missing_runs=0 internal_lin
- `guide-harvest` — page harvested  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/Terminologien?version=2026.0.0  file=migration-log/guide-harvest/pagecontent/technischeimplementierung-terminologien.md  region=found kind=artefact-view src_text_chars=30045 md_text_chars=22255 missing_runs=8 internal_links=0 images=0 artefact_markers=5 title=Terminologien
- `guide-harvest` — rendered-artefact-view: this page is a RENDERING of a conformance resource, not narrative  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/Terminologien?version=2026.0.0 file=migration-log/guide-harvest/pagecontent/technischeimplementierung-terminologien.md src_text_chars=30045
- **WARN** `guide-harvest` — generated-view-lossy: 8 text run(s) of a RENDERED ARTEFACT VIEW did not survive the conversion  url=https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/Terminologien?version=2026.0.0 file=migration-log/guide-harvest/pagecontent/technischeimplementierung-terminologien.md src_text_chars=30045 md_text_chars=22255
- `guide-harvest` — harvested 18 of 18 pages  expected=18 actual=18
- `guide-harvest` — harvest complete  discovered=18 harvested=18 skipped=0 short=0 artefact_views=4 assets=3 out=migration-log/guide-harvest/pagecontent

> **Acceptance:** met — 18 of 18 discovered pages harvested, 0 skipped, 0 narrative pages short

### Step `5.1d.1`

- **WARN** `project-download` — project-download-unavailable: no credentials offered

> **Acceptance:** NOT met — the preferred source (authenticated project download) was unavailable; recorded, escalated, named

### Step `5.1d.2`

- `guide-selection` — pinned guide key=miiigmodulconsent version=2026.0.0 root=MIIIGModulConsent flags=Default,Read-only,Public date=2025-12-18 01:17
- **WARN** `guide-currency` — the newest PUBLISHED guide (2026.0.0) is one release line BEHIND the migrated resources (2026.0.1-rc-4 / develop)

> **Acceptance:** met — pinned to a published version; the guide is one release line behind the resources (① item)

### Step `5.1d.3`

- **WARN** `package-vs-repo` — the published package carries ONE example the source repository does not: Consent/89f494a3-cd75-44f5-a78a-581dfdd47a94 (package/examples/Example_MII_Consent_Einwilligung_1.json)

> **Acceptance:** met — harvested set reconciled against the published package; one package-only example reported

### Step `5.2`

- `first-run-bootstrap` — applied the bootstrap's STEP 2 only (remove the template's own SemVer release automation): 6 paths removed
- `delete-template-examples` — removed input/fsh/profiles/example-patient.fsh and input/fsh/instances/example-patient-instance.fsh (guardrail 5) — paths verified against the checked-out template v0.6.0
- **WARN** `fsh-collision` — skip list: input/fsh/aliases.fsh (template) NOT copied — it collides with the module's own aliases.fsh
- `sushi-skeleton` — start  cmd=`npx --yes fsh-sushi@3.20.0 .`  raw_log=migration-log/sushi-skeleton.log
- **ERROR** `sushi-skeleton` — failed  cmd=`npx --yes fsh-sushi@3.20.0 .`  exit=8 raw_log=migration-log/sushi-skeleton.log raw_log_lines=86
- `dependencies` — carried the SOURCE dependency pins; template-only pins dropped
- `sushi-skeleton` — start  cmd=`npx --yes fsh-sushi@3.20.0 .`  raw_log=migration-log/sushi-skeleton.log prev_raw_log=migration-log/sushi-skeleton.prev.log
- `sushi-skeleton` — done  cmd=`npx --yes fsh-sushi@3.20.0 .`  exit=0 raw_log=migration-log/sushi-skeleton.log raw_log_lines=93

> **Acceptance:** met — SUSHI 0 errors after the source dependency pins were carried over; skip list logged; template examples deleted

### Step `5.3`

- `transfer-artefacts` — moved the post-processed goFSH output into input/fsh/  files=32 (ids and URLs unchanged)
- `id-preservation` — guardrail 1 verified against the published package: every migrated id equals the published one

> **Acceptance:** met — every id and canonical verified against the published package

### Step `5.4`

- `fql-scan` — start  cmd=`bash /tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/scripts/fql-scan.sh --strict`  raw_log=migration-log/fql-scan.log
- `fql-scan` — params  rules=/tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/references/fql-rules.tsv  targets=input/pagecontent  defaulted=1
- `fql-scan` — target  path=input/pagecontent  kind=dir  files=22
- `fql-scan` — result  mapped=0 unknown=0 files=22  exit=0  no directives found
- `fql-scan` — done  cmd=`bash /tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/scripts/fql-scan.sh --strict`  exit=0 raw_log=migration-log/fql-scan.log raw_log_lines=3
- `fql-scan-translations` — start  cmd=`bash /tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/scripts/fql-scan.sh --strict input/translations/de/pagecontent input/intro-notes input/translations/de/intro-notes`  raw_log=migration-log/fql-scan-translations.log
- `fql-scan` — params  rules=/tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/references/fql-rules.tsv  targets= input/translations/de/pagecontent input/intro-notes input/translations/de/intro-notes  defaulted=0
- `fql-scan` — target  path=input/translations/de/pagecontent  kind=dir  files=22
- `fql-scan` — target  path=input/intro-notes  kind=dir  files=3
- `fql-scan` — target  path=input/translations/de/intro-notes  kind=dir  files=3
- `fql-scan` — result  mapped=0 unknown=0 files=28  exit=0  no directives found
- `fql-scan-translations` — done  cmd=`bash /tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/scripts/fql-scan.sh --strict input/translations/de/pagecontent input/intro-notes input/translations/de/intro-notes`  exit=0 raw_log=migration-log/fql-scan-translations.log raw_log_lines=5
- `examples-page` — REWROTE input/pagecontent/examples.md and its German mirror: the template's starter text linked Patient-ExamplePatientInstance.html, the example artefact guardrail 5 deletes — a MIGRATION-INDUCED broken link (2 QA errors, en+de), now fixed and listing the module's own five examples

> **Acceptance:** met — fql-scan --strict exit 0 over 22 + 28 files, 0 findings, 0 [UNKNOWN]

### Step `5.5`

- `sushi-for-po` — start  cmd=`npx --yes fsh-sushi@3.20.0 .`  raw_log=migration-log/sushi-for-po.log
- `sushi-for-po` — done  cmd=`npx --yes fsh-sushi@3.20.0 .`  exit=0 raw_log=migration-log/sushi-for-po.log raw_log_lines=93
- `menu-seed` — paired 26 of 26 anchors  expected=26 actual=26
- `menu-seed` — wrote the page-title seed  entries=22 out=migration-log/menu-titles-de.txt
- `gen-page-title-po` — start  cmd=`python3 /tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/scripts/gen-page-title-po.py fsh-generated/resources/ImplementationGuide-mii-ig-consent.json migration-log/menu-titles-de.txt de input/translations/de/ImplementationGuide-mii-ig-consent.po`  raw_log=migration-log/gen-page-title-po.log
- `gen-page-title-po` — params  ig=fsh-generated/resources/ImplementationGuide-mii-ig-consent.json seed=migration-log/menu-titles-de.txt lang=de out=input/translations/de/ImplementationGuide-mii-ig-consent.po
- `gen-page-title-po` — seed  path=migration-log/menu-titles-de.txt  lines=22 entries=22 matched=19 applied=0 unused=3
- **WARN** `gen-page-title-po` — seed entry unused (no such page title)  title='Artifacts'
- **WARN** `gen-page-title-po` — seed entry unused (no such page title)  title='Artifacts Summary'
- **WARN** `gen-page-title-po` — seed entry unused (no such page title)  title='Metadata'
- `gen-page-title-po` — written  out=input/translations/de/ImplementationGuide-mii-ig-consent.po pages=23 units=23 translated=23 untranslated=0 carried_over=23 preserved_foreign=2 header_preserved=False
- **WARN** `gen-page-title-po` — unit dropped (no longer in the pages: tree)  title='Rendering Artifacts (demo)'
- `gen-page-title-po` — result  exit=0  every page title translated
- `gen-page-title-po` — done  cmd=`python3 /tmp/agentskills-consent-mig/agent-skills/skills/mii-ig-migration/scripts/gen-page-title-po.py fsh-generated/resources/ImplementationGuide-mii-ig-consent.json migration-log/menu-titles-de.txt de input/translations/de/ImplementationGuide-mii-ig-consent.po`  exit=0 raw_log=migration-log/gen-page-title-po.log raw_log_lines=8

> **Acceptance:** met — 23 page-title units for 23 pages, 0 empty msgstr; German breadcrumb confirmed on the BUILT output

### Step `5.6`

- `sushi-build` — start  cmd=`npx --yes fsh-sushi@3.20.0 .`  raw_log=migration-log/sushi-build.log
- `sushi-build` — done  cmd=`npx --yes fsh-sushi@3.20.0 .`  exit=0 raw_log=migration-log/sushi-build.log raw_log_lines=93
- `sushi-build` — errors=0 warnings=9 exit=0 raw_log=migration-log/sushi-build.log
- `ig-publisher` — start  cmd=`docker run --rm -v /tmp/consent-mig-57425/consent-migration:/ig -v /Users/marcel/.fhir:/root/.fhir -w /ig kds-ig-toolchain:v0.4.0 java -Xmx4g -jar /opt/publisher.jar -ig . -no-sushi`  raw_log=migration-log/qa-build.log
- **ERROR** `ig-publisher` — failed  cmd=`docker run --rm -v /tmp/consent-mig-57425/consent-migration:/ig -v /Users/marcel/.fhir:/root/.fhir -w /ig kds-ig-toolchain:v0.4.0 java -Xmx4g -jar /opt/publisher.jar -ig . -no-sushi`  exit=1 raw_log=migration-log/qa-build.log raw_log_lines=45
- **ERROR** `ig-publisher` — MEASURED: an unreplaced ACTIVE placeholder in a date field is a HARD BUILD STOP, not a 'bogus artefact' that ships silently
- `sushi-build` — start  cmd=`npx --yes fsh-sushi@3.20.0 .`  raw_log=migration-log/sushi-build.log prev_raw_log=migration-log/sushi-build.prev.log
- `sushi-build` — done  cmd=`npx --yes fsh-sushi@3.20.0 .`  exit=0 raw_log=migration-log/sushi-build.log raw_log_lines=93
- `ig-publisher` — start  cmd=`docker run --rm -v /tmp/consent-mig-57425/consent-migration:/ig -v /Users/marcel/.fhir:/root/.fhir -w /ig kds-ig-toolchain:v0.4.0 java -Xmx4g -jar /opt/publisher.jar -ig . -no-sushi`  raw_log=migration-log/qa-build.log prev_raw_log=migration-log/qa-build.prev.log
- `ig-publisher` — done  cmd=`docker run --rm -v /tmp/consent-mig-57425/consent-migration:/ig -v /Users/marcel/.fhir:/root/.fhir -w /ig kds-ig-toolchain:v0.4.0 java -Xmx4g -jar /opt/publisher.jar -ig . -no-sushi`  exit=0 raw_log=migration-log/qa-build.log raw_log_lines=5472
- `ig-publisher` — qa=MII_IG_Consent : Validation Results =========================================   qa_txt=output/qa.txt raw_log=migration-log/qa-build.log
- `sushi-build` — start  cmd=`npx --yes fsh-sushi@3.20.0 .`  raw_log=migration-log/sushi-build.log prev_raw_log=migration-log/sushi-build.prev.log
- `sushi-build` — done  cmd=`npx --yes fsh-sushi@3.20.0 .`  exit=0 raw_log=migration-log/sushi-build.log raw_log_lines=93
- `ig-publisher` — start  cmd=`docker run --rm -v /tmp/consent-mig-57425/consent-migration:/ig -v /Users/marcel/.fhir:/root/.fhir -w /ig kds-ig-toolchain:v0.4.0 java -Xmx4g -jar /opt/publisher.jar -ig . -no-sushi`  raw_log=migration-log/qa-build.log prev_raw_log=migration-log/qa-build.prev.log
- `ig-publisher` — done  cmd=`docker run --rm -v /tmp/consent-mig-57425/consent-migration:/ig -v /Users/marcel/.fhir:/root/.fhir -w /ig kds-ig-toolchain:v0.4.0 java -Xmx4g -jar /opt/publisher.jar -ig . -no-sushi`  exit=0 raw_log=migration-log/qa-build.log raw_log_lines=5280
- `qa-triage` — qa.txt err=98 warn=136 info=482; publisher summary also reports 'Broken Links: 2' while the HTML link check in the same run reports '121865 links, 0 broken links (0%)' and qa.txt lists NO unresolved-link error — recorded as an open triage item, not claimed as clean
- `qa-triage` — classification of all 98 ERROR lines, and HOW each class was established:
- `qa-baseline` — PROOF that A1-A3 are PRE-EXISTING, not migration-induced — a build that contains no migration at all

> **Acceptance:** MET AS QUALIFIED — qa err=98, every one classified pre-existing or source-shape with proof; 0 migration-induced

### Step `5.6a`

- `sibling-skill-check` — sibling-skill-present  skill=fhir-ig-analysis path=/tmp/agentskills-consent-mig/agent-skills/skills/fhir-ig-analysis roots_examined=1 ref=<ref> ref_source=not recorded
- **WARN** `same-module-verification` — the sibling skill fhir-ig-analysis IS installed and ran, but its SAME-MODULE comparison could NOT be triggered — a Definition-of-Done item that is NOT met, recorded rather than dropped

> **Acceptance:** NOT met — the sibling skill is present, but its same-module comparison could not be triggered (① item)


### Deliberate deviations from the skill's reference measurements

- **SUSHI 11 → 8, not the spec's 41 → 5.** The repair set is *identical* to the reference
  (`fhir_comments=53`, `code_references=39`, 5 of 21 files changed), so the source content is the
  same. The difference is what SUSHI could *see*: the mechanical errors were **masked** by the
  unresolvable parent. Proven by a **controlled measurement** — the *unrepaired* goFSH output built
  against the *snapshot-bearing* parent reports **50** errors (41 `fhir_comments` path errors,
  3 parse errors, 3 `Cannot find definition for Instance`, 3 consequential cardinality errors),
  against **0** for repaired + snapshots.
- **21 of 21 parent snapshots generated, 0 refused.** The spec measured three refusals
  (`TemplateFrame`, `TemplateModule`, `QuestionnaireComposed`) on `2.0.2`; on `2.0.3` — the pin this
  module's own release line carries — the generator accepts all 21. Element counts for the three
  required parents match the spec's table exactly (DocumentReference 61/45/8, Provenance 65/32/20,
  Consent 132/57/32).
- **`aliases=7`, not the spec's 8** — a consequence of the different `-d` pin (2.0.3 vs 2.0.2).
- **The bootstrap's branch setup was deliberately NOT run.** `scripts/first-run-bootstrap.sh
  --apply` creates `dev`, protects both branches and `PATCH`es `default_branch=main`. Guardrail 6
  forbids modifying the default branch, and this repository's default branch is `develop`. Only the
  bootstrap's step 2 (removing the template's own SemVer release automation, 6 paths) was applied.
- **CI preview is disabled for this branch** (`vars.ENABLE_PREVIEW=false`, the template's own
  documented toggle): the `2.0.3-snapshots` pin resolves only from a local FHIR cache, so the CI
  build would fail at dependency resolution. The preview was therefore built **locally** with the
  pinned toolchain and pushed to `gh-pages`. → ① D4 is what removes this.

## Mini-glossary (novices start here)

- **IG / Implementation Guide** — a publishable specification bundling FHIR profiles, terminology,
  examples and narrative.
- **FSH / SUSHI / goFSH** — FSH is a text language for authoring FHIR artefacts; SUSHI compiles FSH
  to FHIR resources; goFSH goes the other way, deriving FSH from existing resources.
- **Snapshot** — a profile's fully resolved element list. A package that ships only *differentials*
  cannot be imported by SUSHI, which is what §5.1b.5 exists for.
- **Shape B** — a source repository holding raw FHIR XML/JSON with no IG scaffolding: the normal
  state of a module authored in Forge and published on Simplifier.
- **Gate A/B/C/D** — the four mandatory human reviews: identity, narrative, language, release.
- **CalVer** — MII module versions are `YYYY.n.n`, not SemVer.
