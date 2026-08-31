# Recon: Simplifier IG "MII IG Modul Consent" v2026.0.0

Measured 2026-08-31 (Europe/Berlin) via plain `curl` GETs against simplifier.net plus read-only `gh api` GETs against the source repo. All fetched HTML snapshots are preserved next to this report under `recon/` (see Evidence appendix). MEASURED = observed in a fetched page/command output; INFERENCE and NICHT PRÜFBAR are marked as such.

Primary entry: <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0>

---

## Executive summary

- The guide has **exactly 18 addressable pages** (1 root index + 3 folder pages + 14 markdown leaf pages); all 18 returned HTTP 200. This is the complete harvest universe.
- Simplifier hosts **only one version of this guide: 2026.0.0**, which is also the default ("current"). No 2025, no 2027, no ballot version, no English twin exists on Simplifier (probes 404'd; web search found none).
- **None of the 14 narrative markdown pages exist in the git repo** — the repo (`medizininformatik-initiative/kerndatensatzmodul-consent`) contains no `pagecontent/` at all (only `README.md` and one terminology `.md`). The narrative lives exclusively in the Simplifier guide store. Harvesting from Simplifier is therefore mandatory, not optional.
- 4 pages embed rendered conformance resources (Consent, Provenance, DocumentReference profiles + Terminologien); the renders resolve from the Simplifier project files `ressourcen-profile/*.xml` etc., which DO match the git repo layout.
- Licence: **CC BY 4.0, © 2019+ TMF e. V.**; governance via HL7 Deutschland ballot process (quoted below).
- Oddities: guide index says Status **active** while the underlying ImplementationGuide resource says **draft**; the package registry already carries **2026.0.1-rc-1…rc-4** (no matching guide version, no matching GitHub release); the pre-2025 guide survives only as a static mirror (v1.0.4-MII-KDS-MM2, 2023) on medizininformatik-initiative.de.

---

## a. Complete page tree of version 2026.0.0

Source of the tree: the server-rendered `<table id="treetable">` in the guide root page plus the guide's own "Inhaltsverzeichnis" — both agree, and both agree with the raw ImplementationGuide resource served at the bare guide URL (`/guide/miiigmodulconsent`, `<definition><page>…` — saved as `recon/guide-bare.html`). All URLs verified HTTP 200 on 2026-08-31.

Legend: [F] = folder node ("generation=generated", has its own URL + short content), [G] = `.guide.md` (guide-embedded markdown), [P] = `.page.md` (project-file markdown). "content" = size of the extracted `preview-content` div.

| # | Tree position | Title | Type | URL | content |
|---|---|---|---|---|---|
| 1 | root | MIIIGModulConsent (index/"Kerndatensatz-Modul Consent") | [F] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0> | full index + Impressum/Copyright |
| 2 | 1. | Release Notes | [P] `Release-Notes.page.md` | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/Release-Notes?version=2026.0.0> | 5,167 B |
| 3 | 2. | Beschreibung Modul Consent | [G] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/Beschreibung-Modul-Consent?version=2026.0.0> | 1,398 B |
| 4 | 3. | Kontext im Gesamtprojekt / Bezüge zu anderen Modulen | [G] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/KontextimGesamtprojektBezgezuanderenModulen?version=2026.0.0> | 1,280 B |
| 5 | 4. | Referenzen | [G] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/Referenzen?version=2026.0.0> | 1,304 B |
| 6 | 5. | Anwendungsfälle / Informationsmodell | [F] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell?version=2026.0.0> | 178 B (heading only) |
| 7 | 5.1 | Beschreibung von Szenarien für die Anwendung des Moduls | [G] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/BeschreibungvonSzenarienfrdieAnwendungdesModuls?version=2026.0.0> | 1,781 B |
| 8 | 5.2 | Datensätze inkl. Beschreibungen | [G] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/Datenstzeinkl.Beschreibungen?version=2026.0.0> | 777 B |
| 9 | 5.3 | UML | [G] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/UML?version=2026.0.0> | 3,695 B |
| 10 | 5.4 | Fragebögen | [G] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/Fragebgen?version=2026.0.0> | 4,484 B |
| 11 | 6. | Technische Implementierung | [F] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung?version=2026.0.0> | 892 B |
| 12 | 6.1 | FHIR Profile | [F] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile?version=2026.0.0> | 1,098 B |
| 13 | 6.1.1 | Consent | [G] + embedded renders | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0> | 891,047 B |
| 14 | 6.1.2 | Provenance | [G] + embedded renders | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Provenance?version=2026.0.0> | 188,311 B |
| 15 | 6.1.3 | DocumentReference | [G] + embedded renders | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/DocumentReference?version=2026.0.0> | 187,745 B |
| 16 | 6.1.4 | Weitere relevante Profile | [G] | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/WeitererelevanteProfile?version=2026.0.0> | 2,691 B |
| 17 | 6.1.5 | Empfehlungen zur praktischen Anwendung | [P] `Empfehlungen-zur-praktischen-Anwendung.page.md` | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Empfehlungen-zur-praktischen-Anwendung?version=2026.0.0> | 4,300 B |
| 18 | 6.2 | Terminologien | [G] + embedded renders | <https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/Terminologien?version=2026.0.0> | 73,197 B |

**Counts (MEASURED):** 18 pages total = 1 root + 3 folder nodes + 14 markdown leaves (12 × `.guide.md` + 2 × `.page.md`). All 18 fetched HTTP 200 (fetch log in Evidence appendix).

Note on internal node numbering: the treetable rows carry `data-serial-nr` values 8, 11–15, 17–19, 21, 22, 24, 26–28, 30–32 — the gaps (9, 10, 16, 20, 23, 25, 29) suggest guide-internal nodes not exposed in the published tree (e.g. deleted/hidden pages or metadata nodes). Whether hidden pages exist is **NICHT PRÜFBAR** without project write access; the ImplementationGuide resource at the bare URL lists exactly the 18 nodes above and no more.

---

## b. Guide metadata, status, and version history

From the root page's "Veröffentlichung / Status" table (MEASURED, `recon/guide-entry.html` lines 311–336):

| Field | Value |
|---|---|
| Datum | 18.12.2025 |
| Version | 2026.0.0 |
| Status | **active** |
| Realm | DE |

Guide title: "Medizininformatik Initiative – ImplementationGuide – Consent v2026" (HTML `<title>` and `<h1>`).

From the raw ImplementationGuide resource rendered at <https://simplifier.net/guide/miiigmodulconsent> (MEASURED, `recon/guide-bare.html`): `version=2026.0.0`, **`status=draft`**, `fhirVersion=4.0.1`, description "Medizininformatik Initiative - Modul Consent - Implementation Guide". ⚠ **Status mismatch** with the index table ("active") — see §g.

**Not a ballot**: no ballot marker anywhere in the guide; the package description for 2026.0.0 is "KDS Modul Consent Release 2026.0.0" and it is the registry's `latest` dist-tag (MEASURED, packages.simplifier.net JSON below). The only ballot-tagged artifact in the module's history is package `1.0.0-ballot1` ("Initiale Ballotierungsversion").

### Versions of THIS guide on Simplifier (MEASURED by probe)

`GET https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=<v>`:

| version probed | HTTP |
|---|---|
| 2026.0.0 | 200 |
| current | 200 |
| (no version param) | 200 — **byte-identical** to 2026.0.0 (`diff` = empty) ⇒ default/current = 2026.0.0 |
| 2025.0.0 / 2025.0.3 / 2025.0.4 / 2025.0.0-alpha / 2024.0.0 / 1.0 | 404 |
| 2026.0.1 / 2026.0.1-rc-1…rc-4 | 404 |
| 2027.0.0 / 2027.0.0-ballot | 404 |

⇒ **Only one guide version exists on Simplifier: 2026.0.0.** There is **no 2027/ballot guide** and **no separate EN guide** (see §c). Caveat: this is probing, not an authoritative version list — Simplifier's version dropdown is rendered client-side (SPA) and could not be enumerated without JS; treat "no other versions" as very strongly supported (default==2026.0.0, all plausible probes 404) but formally NICHT VOLLSTÄNDIG PRÜFBAR.

### Version history as documented inside the guide (Release Notes page, MEASURED)

The Release Notes page lists: **2026.0.0 (18.12.2025), 2025.0.4 (16.06.2025), 2025.0.3 (12.06.2025), 2025.0.2 (11.06.2025), 2025.0.1 (21.01.2025), 2025.0.0 (17.12.2024)**, with GitHub compare links `1.0.7...2025.0.0`, `2025.0.0...2025.0.3`, `2025.0.3...2026.0.0`. 2026.0.0 headline changes (quoted from the page): SignatureTypes VS + "Verification Signature"; Policy CS `period-of-validity` property; 4 policies deprecated; new CS `mii-cs-consent-version-modules`; OIDs for Ablehnungen (BC v1.6d/v1.7.2); `Consent.provision(.provision).period.end` now 0..1; new page "Empfehlungen zur praktischen Anwendung".

### Package registry (context; MEASURED via `https://packages.simplifier.net/de.medizininformatikinitiative.kerndatensatz.consent`)

Versions: `1.0.0-ballot1, 1.0.1–1.0.7, 2025.0.0-alpha, 2025.0.0–2025.0.4, 2026.0.0, 2026.0.1-rc-1, 2026.0.1-rc-2, 2026.0.1-rc-3, 2026.0.1-rc-4`; dist-tag `latest = 2026.0.0`. ⚠ Four **2026.0.1 release candidates already exist as packages** but have **no guide version and no GitHub release** (GitHub releases per pinned context: 2026.0.0, 2025.0.3, 2025.0.0; repo last push 2026-08-21 — INFERENCE: the rc's correspond to that recent push activity). Also note: package 2025.0.4 exists but was never a GitHub release.

### Predecessor guide (older years)

The pre-2025 IG was a **different Simplifier guide** (key `IGMIIKDSModulConsent`) that no longer exists on Simplifier (probes on several key variants: 404). It survives as a static HTML export on the MII website: <https://www.medizininformatik-initiative.de/Kerndatensatz/Modul_Consent/IGMIIKDSModulConsent.html> — showing **Version 1.0.4-MII-KDS-MM2, Datum 2023-08-31, Status final** (MEASURED, `recon/mii-mirror-index.html`). The MII website does NOT mirror the 2026 guide (`MIIIGModulConsent.html` there → 404).

---

## c. Language situation

- **German-only.** All 14 markdown pages are German (titles and prose, MEASURED across all fetched pages). The only English text is Simplifier renderer boilerplate inside embedded resource renders ("Invocations", "Details", "Additional Language Displays") and the standard Simplifier footer.
- **No English twin guide found**: no EN version on this guide key (only 2026.0.0 exists), and web searches for an EN MII consent guide surfaced nothing (searches dated 2026-08-31; see Evidence). NICHT PRÜFBAR beyond search coverage, but there is no link to any EN edition anywhere inside the guide itself (MEASURED: full external-link census in §g contains none).
- Curiosity: the git repo contains an English overview figure `figures/MII-KDS_en_Consent.jpg`, but the guide embeds only the German `MII-KDS_de_Consent.jpg` (MEASURED: repo tree + `Beschreibung-Modul-Consent` page img src).

---

## d. Licence / copyright statements (verbatim quotes)

All on the guide root page (<https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0>, `recon/guide-entry.html` lines 339–373):

**Impressum:**
> „Dieser Leitfaden ist im Rahmen der Medizininformatik-Initiative erstellt worden und unterliegt per Governance-Prozess dem Abstimmungsverfahren des Interoperabilitätsforums und der Technischen Komitees von HL7 Deutschland e. V."

**Autoren und Ansprechpartner:**
> „Inhaltlich verantwortlich für das hier dargestellte Modul ist die **MII Taskforce Consent Umsetzung**." — Mitarbeit: Martin Bialke, Sebastian Stäubert, Angela Merzweiler, Lars Geidel, Jörg Römhild, Raffael Bild, Fabian Prasser, Stefan Lang (HL7 Deutschland, TK FHIR, Gefyra GmbH, Lang Health IT Consulting). Leitung: Sebastian Stäubert, Martin Bialke. Technische Umsetzung: Stefan Lang, Martin Bialke. TMF-Kontakt: Karoline Buckow. Kommentare via GitHub issues (<https://github.com/medizininformatik-initiative/kerndatensatzmodul-consent/issues>) oder office@medizininformatik-initiative.de.

**Copyright-Hinweis, Nutzungshinweise:**
> „© 2019+ TMF e. V., Charlottenstraße 42, 10117 Berlin"
> „Diese Arbeit ist lizensiert unter der Creative Commons Attribution 4.0 International License." (link + CC-BY-4.0 button img from licensebuttons.net)
> „Zu den Nutzungsrechten der zugrunde liegenden FHIR-Technologie siehe die FHIR-Basis-Spezifikation."
> „Einige verwendete Codesysteme werden von anderen Organisationen herausgegeben und gepflegt. Es gilt das Copyright der dort jeweils aufgeführten Herausgeber (Publisher)."

**Disclaimer:**
> „Der Inhalt dieses Dokuments ist öffentlich. Zu beachten ist, dass Teile dieses Dokuments auf FHIR Version R4 beruhen, für die das Copyright von HL7 International gilt."
> „Obwohl diese Publikation mit größter Sorgfalt erstellt wurde, können die Autoren keinerlei Haftung für direkten oder indirekten Schaden übernehmen, der durch den Inhalt dieser Spezifikation entstehen könnte."

Repo licence for comparison: the git repo's `LICENSE` file exists (repo tree, MEASURED); its content was not read in this pass — **for-cross-check-with-source-recon** (memory from the Dokument-module dry run warns about silent licence divergence).

---

## e. Rendered-resource pages vs hand-written narrative; git-repo counterparts

### Classification (MEASURED via content size + StructureDefinition/snapshot marker counts + heading census)

**Pages with embedded conformance-resource renders (4):**

| Page | What it embeds |
|---|---|
| 6.1.1 Consent (891 KB content, 906 render markers) | Profile `mii-pr-consent-einwilligung` (tree/differential/snapshot/hybrid renders), plus extensive hand-written German sections around it: „Grundsätzliche Verwendung des Profils FHIR Consent", Interoperabilität, Suchparameter (incl. „Mitgeltende Suchparameter gemäß HL7-D Standard Einwilligungsmanagement", „Komplexere Beispiele (Suchanfragen)"), Widerruf/Ablehnung semantics, 16× „Beispiel" occurrences. Render anchors point at `/resolve?scope=project:MedizininformatikInitiative-ModulConsent&filepath=ressourcen-profile/Profile_MII_Consent_Einwilligung.xml#…` |
| 6.1.2 Provenance (188 KB, 373 markers) | Profile `mii-pr-consent-provenance` render + short „Darstellung"/„Beispiele" narrative |
| 6.1.3 DocumentReference (188 KB, 312 markers) | Profile `mii-pr-consent-documentreference` render + short „Darstellung"/„Beispiele" narrative |
| 6.2 Terminologien (73 KB) | Rendered terminology: ValueSets `mii-vs-consent-signaturetypes`, `mii-vs-consent-answer`; CodeSystems „MII CS Consent Version and Modules", „MII_CS_Consent_Answer", „MII CS Consent Policy" (with Properties/Concepts/Additional-Language-Displays tables) |

**Pure narrative pages (10 leaves + 3 folder stubs + root):** Release Notes, Beschreibung Modul Consent, Kontext im Gesamtprojekt, Referenzen, Beschreibung von Szenarien, Datensätze inkl. Beschreibungen, UML (narrative + one embedded PNG hot-linked from GitHub), Fragebögen, Weitere relevante Profile, Empfehlungen zur praktischen Anwendung — plus the three folder pages and the root index (Impressum/licence). None contain resource renders (0 markers each).

### Git-repo counterparts (MEASURED: full recursive tree of `medizininformatik-initiative/kerndatensatzmodul-consent@master`, 32 blobs)

The repo contains **NO pagecontent/markdown for any guide page**. Complete `.md` inventory of the repo: `README.md` and `terminologie/codesystems/CodeSystem-MiiConsentPolicy.md` — nothing else. There is no `pagecontent/`, no `input/`, no IG-publisher scaffolding of any kind (top level: `.gitignore, LICENSE, README.md, examples/, figures/, ressourcen-profile/, searchparameters/, terminologie/`).

⇒ **All 14 markdown pages (12 `.guide.md` + 2 `.page.md`) have no counterpart in git.** The `.guide.md` pages live only in the Simplifier guide store; the two `.page.md` pages (Release Notes, Empfehlungen zur praktischen Anwendung) are Simplifier **project files** by naming convention (INFERENCE from the `.page.md` suffix and `generation=markdown` in the IG resource) — they are also absent from git, so presumably exist only in the Simplifier project file store (project file listing itself is behind the SPA/auth — NICHT PRÜFBAR without a Simplifier account).

What DOES round-trip to git: the conformance artifacts the renders resolve from — `ressourcen-profile/Profile_MII_Consent_{Einwilligung,Provenance,DocumentReference}.xml`, 6 × `searchparameters/SearchParameter_MII_Consent_Einwilligung_*.xml`, `terminologie/{codesystems,valuesets}/*` (3 CS xml + 1 CS json + 3 VS xml), 5 × `examples/Example_MII_Consent_*.xml`, and `figures/*` (the two images the guide hot-links are in git: `figures/MII-KDS_de_Consent.jpg`, `figures/information-model_UML-Diagramm_MII-spez.png`).

---

## f. Pointers to other consent-related guides/projects on Simplifier

- **HL7 Deutschland „Einwilligungsmanagement" IG is the guide's biggest dependency**: 34 links to `https://ig.fhir.de/einwilligungsmanagement/stable/…` (Consent, Patient, Organization, ResearchStudy, DocumentReference, Provenance, QuestionnaireComposed, QuestionnaireResponse, TemplateFrame, TemplateModule, ContextIdentifier(-Type), DomainReference, ResultType, TemplateType, Mitgeltende Erläuterungen…) across Beschreibung, Kontext, Fragebögen, UML, FHIR-Profile pages. Two links additionally target its **Simplifier guide form**: <https://simplifier.net/guide/Einwilligungsmanagement/Consent?version=current> and <https://simplifier.net/guide/Einwilligungsmanagement/Mitgeltende-Erl-uterungen?version=current> (both on the Consent / Empfehlungen pages).
- **MII Modul Person**: the Consent page links to <https://simplifier.net/medizininformatikinitiative-modulperson/sdmiipersonpatientpseudonymisiert> (pseudonymized-patient profile).
- **German base profiles**: Referenzen page links to <https://simplifier.net/basisprofil-de-r4> and <https://simplifier.net/basisprofilde>.
- **Hosting project**: <https://simplifier.net/medizininformatikinitiative-modulconsent> ("MII - Modul Consent", HTTP 200; the URL from the task briefing, `simplifier.net/miiigmodulconsent`, is **404** — that slug is only the guide key, not a project). The project page is a JS SPA; server HTML exposes no resource list. Via WebFetch: description "working version of the Consent module … stable versions published as packages", public, FHIR R4, scope Germany; team: Koordinationsstelle MII (owner), Alexander Zautke, Sebastian Stäubert, Stefan Lang, Martin Bialke (admins), Angela Merzweiler, Jörg Römhild, Julian Sass (writers). Download endpoints exist (`/medizininformatikinitiative-modulconsent/$actions/downloading?format=json|xml`). A full resource inventory of the project was **NICHT PRÜFBAR** anonymously (SPA/API); the package tarball (registry above) is the reliable equivalent — for-cross-check-with-source-recon.
- **ART-DECOR (mide- project)** as the dataset/questionnaire source of truth: 11 links (`decor-datasets--mide-`, `decor-valuesets--mide-`, `decor-project--mide-`, `RetrieveDataSet`/`RetrieveValueSet` service URLs) on Datensätze, Fragebögen, Referenzen, Consent, Terminologien pages. The Terminologien page states the answer-option ValueSets from ART-DECOR „werden zeitnah durch die TFCU in diesem IG eingepflegt" (i.e. migration into the IG is announced but pending).
- **THS Greifswald (gICS)** operational guidance: <https://ths-greifswald.de/gics>, <https://www.ths-greifswald.de/diz-dashboard-empfehlung-gics-kds-consent-status/>, and the Dezember-2025 release news post (Consent + Empfehlungen pages).

---

## g. Unusual findings / migration-relevant hazards

1. **Status contradiction (MEASURED):** root-page table says `Status: active`; the ImplementationGuide resource rendered at the bare guide URL says `status: draft`. Pick one for the migrated IG; ask the module owners which is intended.
2. **Package registry is ahead of both guide and GitHub:** `2026.0.1-rc-1 … rc-4` packages exist (registry JSON), with no guide version and no GitHub release. A migration snapshotting 2026.0.0 may be chasing a moving 2026.0.1 target. (Repo last push 2026-08-21 per pinned context.)
3. **Narrative single point of failure:** the 14 markdown pages exist only inside Simplifier (see §e) — no git backup. The 2023-era predecessor guide has already vanished from Simplifier (only the MII-website static mirror remains), demonstrating that these guides do get deleted.
4. **Hot-linked images that must be re-hosted on migration (MEASURED img srcs):**
   - `https://raw.githubusercontent.com/medizininformatik-initiative/kerndatensatzmodul-consent/master/figures/MII-KDS_de_Consent.jpg` (Beschreibung page)
   - `https://github.com/medizininformatik-initiative/kerndatensatzmodul-consent/blob/master/figures/information-model_UML-Diagramm_MII-spez.png?raw=true` (UML page; blob-URL form, currently 200) — both track `master`, not the release tag ⇒ content can drift under the released guide.
   - MII logo hot-linked from `https://www.medizininformatik-initiative.de/themes/custom/mii/assets/img/Logo_MII_270px_Hoehe_de.png` (every page header) and the CC-BY button from `licensebuttons.net`.
5. **External-link rewrite inventory (census across all 18 pages, MEASURED):** hl7.org 63 + www.hl7.org 3 (13 of them plain `http://`), ig.fhir.de 34, medizininformatik-initiative.de 26 (incl. Mustertext, Kerndatensatz-PDF, Komplettwiderruf-PDF), art-decor.org 11 (2 plain `http://`, incl. one `RetrieveValueSet` service URL with pinned `effectiveDate=2021-04-23` — fragile), simplifier.net 5 (2 cross-guide `?version=current` links), github.com 4 (3 compare-links on Release Notes + issues link), ths-greifswald.de 4, wiki.hl7.de 2, ebooks.iospress.nl 2 (DOI 10.3233/SHTI251389), creativecommons.org 2, ihe.net 1 (PDF `#nameddest` deep link), bfarm.de 1 (PDF, §64e Modellvorhaben Genomsequenzierung), build.fhir.org 1 (IPS must-support), bmcmedinformdecismak.biomedcentral.com 1.
6. **Terminologien page announces incomplete content:** answer-option ValueSets still live in ART-DECOR and are only "zeitnah" to be added — the IG is not self-contained on terminology.
7. **Canonical-URL check on Terminologien:** links `https://www.medizininformatik-initiative.de/fhir/modul-consent/ValueSet/mii-vs-consent-signaturetypes` (the module's canonical base `…/fhir/modul-consent/` — note: NOT resolvable hosting, standard MII practice).
8. **No broken guide pages** (all 18 → HTTP 200); no "old version" banner present in the served HTML (the version dropdown/banner is SPA-side; the static HTML carries none).
9. **Simplifier serial-nr gaps** in the page tree (9, 10, 16, 20, 23, 25, 29 missing) — possible deleted/hidden nodes; NICHT PRÜFBAR (see §a).
10. **packages.fhir.org mirror:** a Google-indexed mirror URL (`packages.fhir.org/guide/miiigmodulconsent/…`) appeared in search results but returned **404** when fetched directly — do not rely on it as a fallback mirror.
11. **Custom styling:** the guide loads a project-specific stylesheet `…/files/static/styles/MIICustomIGStyle/style.css` on every page — the MII look-and-feel is a Simplifier guide asset, also not in git.

---

## Evidence appendix

Saved snapshots (all under `/private/tmp/claude-503/-Users-marcel-Development-cross-hub-patientportal/9e6d07a4-6adb-4483-b4c7-d44df6dc83fb/scratchpad/recon/`):
- `guide-entry.html` — root page 2026.0.0 (24,509 B); `guide-noversion.html` — identical (diff empty); `guide-bare.html` — raw IG resource render; `mii-mirror-index.html` — MII-website mirror of the 2023 guide; `project-guides-tab.html`, `project-modulconsent.html` — SPA project pages; `pages/*.html` — all 17 sub-pages (fetch log with HTTP 200 + byte sizes in session transcript).

Key commands (exact, reproducible):
- Page fetches: `curl -sL "https://simplifier.net/guide/miiigmodulconsent/<path>?version=2026.0.0"` → 18 × HTTP 200.
- Version probes: `curl -sL -o /dev/null -w "%{http_code}" "https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=<v>"` → table in §b.
- Package registry: `curl -s https://packages.simplifier.net/de.medizininformatikinitiative.kerndatensatz.consent` → 19 versions, `latest: 2026.0.0`.
- Repo tree (read-only): `gh api "repos/medizininformatik-initiative/kerndatensatzmodul-consent/git/trees/master?recursive=1" --jq '.tree[] | select(.type=="blob") | .path'` → 32 blobs, no pagecontent.
- Old-guide probes: `curl` on `simplifier.net/guide/{igmiikdsmodulconsent/IGMIIKDSModulConsent, IGMIIKDSModulConsent, medizininformatikinitiative-modulconsent/IGMIIKDSModulConsent}` → all 404; MII mirror `…/Modul_Consent/IGMIIKDSModulConsent.html` → 200 (v1.0.4-MII-KDS-MM2, 2023-08-31, final).

Web searches used (2026-08-31): "simplifier.net guide 'Modul Consent' Medizininformatik Initiative Implementation Guide 2025" and "simplifier.net 'guide' MII Consent 2025.0 ImplementationGuide Kerndatensatz Einwilligung" — no EN twin, no 2025/2027 Simplifier guide surfaced. Sources: [Simplifier package 2025.0.0](https://simplifier.net/packages/de.medizininformatikinitiative.kerndatensatz.consent/2025.0.0), [MII website mirror](https://www.medizininformatik-initiative.de/Kerndatensatz/Modul_Consent/IGMIIKDSModulConsent.html), [project page](https://simplifier.net/medizininformatikinitiative-modulconsent), [Einwilligungsmanagement IG](https://ig.fhir.de/einwilligungsmanagement/stable/UseCases.html).
