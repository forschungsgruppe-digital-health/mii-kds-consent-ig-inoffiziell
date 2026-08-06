# Migration report — MII KDS Modul Consent → MII KDS module template

## L0 — Read this first (for everyone)

This module was moved from **Simplifier/Forge** onto the **MII KDS module template v0.6.0**.
**State:** complete through skeleton, artefacts, **narrative**, build and rendered preview.
**The narrative WAS migrated on 2026-08-06** — see the correction note below; the earlier claim that
it could not be was wrong.
**Build:** sushi **0 errors** · qa **84 errors / 157 warnings / 0 broken links** (local, `-tx n/a`;
unchanged by the narrative migration; CI with `tx.fhir.org` before it: 83/137/0) · preview:
<https://forschungsgruppe-digital-health.github.io/mii-kds-consent-ig-inoffiziell/branches/migration/mii-kds-module-template/>
**Your job as reviewer:** work the three queues below in order — ① decide, ② review, ③ triage.
Nothing is published until Gate D (a human merge decision); everything here is reversible.

> ### Correction, 2026-08-06 — the narrative is migrated after all
>
> An earlier version of this report said the module's guide "exists only as a rendered Simplifier
> guide, which is client-rendered and was **not** scraped", and shipped **the module template's
> starter pages** under this module's name. **That claim was false.** It was measured on the
> Simplifier **project** page (`simplifier.net/MedizininformatikInitiative-ModulConsent/` — genuinely
> a client-rendered app shell) and wrongly generalised to the **guide** pages, which are a different
> URL space and **are server-rendered**.
>
> Re-measured on 2026-08-06 with the corrected `mii-ig-migration` skill: the guide root
> `simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0` returns HTTP 200 with
> the whole page tree, and each leaf page returns its real German narrative. `guide-harvest.sh`
> harvested **18 of 18 discovered pages, 0 skipped, 0 narrative pages short**. Those 18 pages are now
> mapped onto the template's fixed page set, and **no page of this guide is a template starter page
> any more**.
>
> The lesson is now guardrail 9/10 of the skill: *a negative capability finding is only valid for the
> artefact it was measured on, and is never generalised to a sibling URL.*

## ① Decision queue (Gate A — someone must choose)

| # | Decision | Options (with consequence) | Default applied | Decide at |
|---|---|---|---|---|
| D1 | **`publisher`** — the one identity field no tier yields | name the real publishing organisation \| keep the template's `Medical Informatics Initiative (MII)` (publishes the module under an organisation nobody verified) | **template default, marked `TODO:REVIEW` in `sushi-config.yaml`** — no value was recovered or invented; the registry `author` (`sebastianstubert`) and the GitHub owner are accounts, not publishers | Gate A |
| D2 | `title` | template pattern `MII Implementation Guide Consent` \| tier-R candidate `Medizininformatik Initiative - Modul Consent` (README heading) \| the packaged IG's computable name `MII IG Consent v2026` (invalid as a FHIR `name` — it has spaces) | template pattern, marked in-tree | Gate A |
| D3 | `description` | tier P `KDS Modul Consent Release 2026.0.0` \| tier R `Kerndatensatzmodul Consent` \| packaged IG `Medizininformatik Initiative - Modul Consent - Implementation Guide` | tier P (highest tier), the other two recorded in the comment | Gate A |
| D4 | **how the snapshot-bearing parent reaches CI** | CI prebuild step regenerating it (187 MB generator per run) \| **vendoring** (a derived artefact of someone else's package in version control) \| internal registry (governance) \| do not re-pin and leave 3 profiles blocked (SUSHI stays at 5 errors) | **vendored** at `parent-snapshots/` + one added step in `.github/workflows/ig-publisher.yml`; labelled as a local rebuild, upstream untouched. The durable fix is upstream publishing snapshots. | Gate A |
| D5 | `version` | tier P **2026.0.0** (published manifest) \| tier G `1.0.8` (goFSH's config — one profile's version, never identity) | 2026.0.0 | Gate A |
| D6 | parent pin | tier P **2.0.2** (source pin) \| `2.0.3` (registry `dist-tags.latest`, used in run 1) | 2.0.2 (rebuilt as `2.0.2-snapshots`) | Gate A |
| D7 | `status` | source `draft` (packaged ImplementationGuide) \| template default `active` | **source wins: `draft`** | Gate A |
| D8 | the three generator-refused parent profiles (`TemplateFrame`, `TemplateModule`, `QuestionnaireComposed`) | escalate to the `de.einwilligungsmanagement` maintainers (malformed upstream differential) \| ignore (none is a `Parent`/`InstanceOf` in this module) | not hand-finished, not used by this module — recorded | Gate A |
| D9 | ids the migration had to mint: the six `SearchParameter`s carry **no `id`** in the source *or* in the published package | keep goFSH's filename-derived ids (`MII-SP-Consent-PolicyUri`, …; 12 QA errors, see ③) \| adopt the url's last segment (`mii-sp-consent-policyuri`, clears them) | goFSH's, unchanged — minting a module's ids is a human decision | Gate A |
| D10 | values no tier yields, kept at the template's documented default and marked `TODO:REVIEW`: `date` / `approvalDate` (2026-08-06 = the migration date), `copyrightYear` (2019), `releaseLabel` (Release), `artifact-author` email (`office@…`), **`artifact-topic` NCI code (block commented out rather than filled with a guess)** | supply the real values \| keep | template defaults, all marked | Gate A/D |

`license` is **not** a decision: `CC-BY-4.0` was read twice from the source (LICENSE text and GitHub's
`license.spdx_id`). It happens to equal the template literal — verified, not defaulted.

## ② Review queue (Gates B/C — someone must check)

| Where | What to check | Suggested action | Gate |
|---|---|---|---|
| **the German pages** `input/translations/de/pagecontent/*.md` + `input/translations/de/intro-notes/*.md` | this is the **authoritative text** — it is the harvested German narrative, re-flowed and with the Simplifier render directives resolved. Read it against the rendered source guide, page by page. | confirm each section landed in the right template page (the content map below says where), then drop the `TODO:REVIEW` markers you have checked | B |
| **the English pages** `input/pagecontent/*.md` + `input/intro-notes/*.md` | every page carrying migrated content says at the top that it is an **unreviewed machine translation** of the German page. **Nothing on the English side has been read by a human.** | translate/proof-read properly, or have the module owners do it; keep the banner until then | C |
| **consent wording specifically** | policy display names, MII Broad Consent module/version labels (`1.6d Komplettwiderruf`, `Zusatzmodul ACRIBiS (Z2)`, …), the answer designators `gültig`/`nicht gültig`/`unbekannt`, and the signature-kind descriptions were **deliberately left in German on every English page**, because they are legally binding text and identifiers rather than prose | confirm that this is what the module owners want, and that no English sentence around them reads as if it were the binding version | C |
| `input/intro-notes/StructureDefinition-e0e166b4-…-notes.md` (+ German mirror) | the source's element table lists **two rows under the same slice name** `Consent.category:templateType.coding`, and this profile in fact slices `category` into `loinc`/`mii` | both rows are reproduced unchanged with a `TODO:REVIEW`; get the source corrected rather than the copy | B |
| `input/pagecontent/general-requirements.md` (+ German mirror) | the source guide's page "Beschreibung von Szenarien für die Anwendung des Moduls" was routed **here** rather than onto Guidance for Implementers | confirm the routing (the migration spec calls this one out as a case reviewers disagree on) | B |
| `input/pagecontent/terminology.md` (+ German mirror) | the source's ~124-row policy table was **replaced by a link** to the generated CodeSystem page, and one parenthetical was re-pointed at it | the generated page was checked and does render level/display/code/`P30Y`/`Deprecated`; re-check after any CodeSystem change | B |
| `input/pagecontent/examples.md` (+ German mirror) | the source guide renders a Consent example, `89f494a3-cd75-44f5-a78a-581dfdd47a94`, that **the module does not ship** | ask the module owners for the instance, or drop the example from the source guide — not recreated here | B |
| pages with **no** source content: `researcher-guidance`, `capability-statements`, `logical-models`, `missing-data`, the risk/residual-risk sections of `security-and-privacy` | each now states explicitly that the source guide has nothing on this, instead of carrying a template prompt | decide whether to write the missing content (out of scope for a migration) or delete the page | B |
| `sushi-config.yaml` | the `TODO:REVIEW` markers on `publisher`, `title`, `date`, `copyrightYear`, `releaseLabel`, `artifact-topic` | replace with real values, delete the marker | A |
| `parent-snapshots/README.md` | the vendored parent: provenance, 18 of 21 generated, 3 refused | confirm the vendoring decision (D4) | A |
| `input/translations/de/ImplementationGuide-mii-ig-consent.po` | 23 page-title units, **0 untranslated**; verified on the built site (`/de/` renders *Startseite*, *Profile und Extensions*) | spot-check wording | C |
| the module's own German artefact descriptions | they render in the English default pages too (KDS convention) | decide whether English translations are in scope | C |
| `README.md` (the module's own, German, kept) | it still describes the Simplifier/Forge workflow | rewrite for the template workflow before Gate D | B |
| retained source trees `ressourcen-profile/`, `terminologie/`, `searchparameters/`, `examples/`, `figures/`, `sushi-config.gofsh-derived.yaml` | the raw Forge sources the FSH was derived from — **listed, not removed** | retire after Gate D | D |

## ③ QA triage (what the build says, and whose problem it is)

84 errors, local build, IG Publisher 2.2.11, `-tx n/a`. **Broken links: 0.** Classified:

| Finding (shortened) | Count | Provenance (proof) | Next action |
|---|---|---|---|
| `the canonical URL … does not match the URL` / `URL Mismatch` / `Resource id/url mismatch` on StructureDefinitions, ValueSets, CodeSystems | 34 | **pre-existing, proven against the published package**: `de.medizininformatikinitiative.kerndatensatz.consent@2026.0.0` ships `StructureDefinition` ids that are Forge **GUIDs** (`56375452-…`) and CodeSystem/ValueSet ids that are **OID+timestamp** strings, while the urls follow `mii-pr-consent-*`. Guardrail 1 forbids changing either. | escalate to the module maintainers; or declare `special-url` (template recipe) — a Gate-A decision, not a migration fix |
| same class, on the six `SearchParameter`s | 12 | **migration-derived id**: neither the source XML nor the published package carries an `id`; goFSH minted one from the file name (see D9) | decide D9 — adopting the url's last segment clears all 12 |
| terminology: `None of the codings … are in the value set`, `Wrong Display Name`, `code system is complete but the number of concepts …` | 27 | **environment + source**: the local build ran with `-tx n/a` (no terminology server), so nothing expanded. The CI build against `tx.fhir.org` reports 83/137 — the same class. The `Wrong Display Name` findings are the source's own display strings vs the OID code system it ships. | re-run against the MII SU-TermServ before reading these; then escalate the display mismatches |
| `Unable to resolve resource with reference 'Patient/…'` / `'ResearchStudy/…'` | 8 | **pre-existing**: the module's examples reference patients and studies that the module does not ship (same in the published package) | accept for a preview; escalate as an example-completeness item |
| `Consent.category:loinc: max allowed = 1, but found 2` | 3 | **pre-existing source defect, verifiable in the source bytes**: `MII_PR_Consent_Einwilligung` slices `category` `loinc 1..1`, and the source examples carry two `category` entries whose first coding is LOINC | escalate to the module maintainers |
| broken links to the template's example artefacts | was 4, **now 0** | **migration-induced** — the template's starter pages linked the example artefacts that guardrail 5 removed | **fixed** in this branch (the four links are gone from `examples.md` / `profiles-and-extensions.md`, en + de) |
| `module-release.yml`'s placeholder guard would skip the CalVer release path | n/a (not run) | **template property, not a migration finding**: the guard is `grep -q '{{' sushi-config.yaml`, and the file's own 60-line header *documents* the placeholder names, so it matches in every instantiated module. Verified in the vendored workflow (line 118). | report upstream to the module template; harmless here (no release runs in a sandbox) |
| `FHIR validation` workflow red | 1 job | **environment**: it calls MII's reusable Simplifier QC workflow, which needs the secrets `SIMPLIFIER_USERNAME` / `SIMPLIFIER_PASSWORD`; this sandbox has neither. No secret was added. | ignore in the sandbox |

**No error in the build is unclassified.** The `IG build and preview` workflow is green.

## Content map (where every source page went)

**Narrative source (spec §5.1c):** ② **the guide harvest** — anonymous, verified, and a *rendering*.
① the authenticated project download was **not** used: `…/$actions/downloading` requires a Simplifier
login (re-measured 2026-08-06: anonymous access redirects to `/login?ReturnUrl=…`) and no credentials
were offered in this run — logged as `project-download-unavailable:`. A later run with credentials
would get the authored Markdown instead of a rendering and should redo the mapping against it.

**Harvest:** `guide-harvest.sh --guide-url https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0`
→ **discovered 18, harvested 18, skipped 0, narrative pages short 0**, 14 `narrative` + 4
`artefact-view`, 3 referenced assets. Per-page account:
`migration-log/guide-harvest.tsv`; the harvested Markdown: `migration-log/guide-harvest/pagecontent/`.

| Source page (guide 2026.0.0) | kind | Target | Anything lost? |
|---|---|---|---|
| `MIIIGModulConsent` (root) | narrative | `index.md` — intro, publication table, Impressum, Autoren/Ansprechpartner, Copyright, Disclaimer | the page's own *Inhaltsverzeichnis* — the IG Publisher generates menu + ToC (directive crosswalk) |
| `Release-Notes` | narrative | `changes.md` (all six versions, verbatim) | no |
| `Beschreibung-Modul-Consent` | narrative | `index.md` § *Beschreibung Modul Consent*, incl. the module figure | no — figure transferred to `input/images/` |
| `KontextimGesamtprojektBezgezuanderenModulen` | narrative | `implementer-guidance.md` § *Kontext im Gesamtprojekt* (spec §9: this is its primary home) | no |
| `Referenzen` | narrative | `implementer-guidance.md` § *Referenzen*; short link list on `index.md` § *Verwandte Leitfäden* (spec §9) | no |
| `AnwendungsflleInformationsmodell` | narrative | — (the source page says only "Diese Seite wurde absichtlich leer gelassen"; its children were routed individually) | nothing to lose |
| `…/BeschreibungvonSzenarienfrdieAnwendungdesModuls` | narrative | `general-requirements.md` § *Beschreibung von Szenarien* (spec §9 default; flagged for Gate B) | no |
| `…/Datenstzeinkl.Beschreibungen` | narrative | `datasets-and-descriptions.md` | no |
| `…/UML` | narrative | `uml-diagrams.md`, incl. the class diagram | no — diagram + its GraphML source transferred |
| `…/Fragebgen` | narrative | `implementer-guidance.md` § *Fragebögen* (incl. the checkbox→code table, which is **not** in the ValueSet) | no |
| `TechnischeImplementierung` | narrative | `conformance.md` § *Technische Implementierung*; the FHIR-search paragraph also on `search-parameters-and-operations.md` | no |
| `…/FHIRProfile` | narrative | `profiles-and-extensions.md` intro; the must-support paragraph also on `must-support.md` | no |
| `…/FHIRProfile/Consent` | **artefact-view** | prose → `input/intro-notes/StructureDefinition-e0e166b4-…-intro.md` + `-notes.md`; *Datenschutz-Aspekte* → `security-and-privacy.md`; *Suchparameter* → `search-parameters-and-operations.md`; *Beispielhafte Consent-Ressourcen* → `examples.md` | the rendered element tree and the inline XML dumps — regenerated by the IG Publisher on the artefact page (crosswalk) |
| `…/FHIRProfile/Provenance` | **artefact-view** | prose + element table → `…-f675b1e8-…-intro.md` / `-notes.md`; example → `examples.md` | element tree, as above. The source's own example embed had **failed on Simplifier** ("File not found") — here it is a working link |
| `…/FHIRProfile/DocumentReference` | **artefact-view** | prose + element table → `…-56375452-…-intro.md` / `-notes.md`; example → `examples.md` | element tree, as above |
| `…/FHIRProfile/WeitererelevanteProfile` | narrative | `profiles-and-extensions.md` § *Weitere relevante Profile* (both tables) | no |
| `…/FHIRProfile/Empfehlungen-zur-praktischen-Anwendung` | narrative | `implementer-guidance.md` § *Empfehlungen zur praktischen Anwendung* | no |
| `…/Terminologien` | **artefact-view** | `terminology.md` — all prose, the signature-types table kept (its first column is not in the ValueSet) | the ~124-row policy table and the generated ValueSet/CodeSystem expansions → replaced by links; **verified on the built page** that level, display, code, `period-of-validity` and `Deprecated` all render there |

**Conversion losses measured by the harvester:** 22 text runs across the 4 `artefact-view` pages
(`generated-view-lossy:` WARNs). All 22 were inspected: every one is inside a generated element tree
or property table — none is authored narrative. One Terminologien run straddles the boundary (an
authored parenthetical joined to generated table text); its content is migrated and re-pointed, and
that is flagged on `terminology.md`.

**Package reconciliation (spec §5.1c.3):** 15 of 15 module conformance artefacts (3 profiles,
3 ValueSets, 3 CodeSystems, 6 SearchParameters) are documented by a harvested page or section. The
CRMI expansion manifest `Parameters-mii-param-consent-manifest` has no guide page and none is
expected — template machinery. *(A `silent-partial-success: documented 15 of 16` WARN is in the log
because I first counted the manifest as an expected artefact; the correcting INFO follows it.)*

**Assets transferred** (from `migration-log/guide-harvest-assets.tsv`, the module's own `figures/`):
`MII-KDS_de_Consent.jpg`, `information-model_UML-Diagramm_MII-spez.png` (+ its `.graphml` source to
`input/images-source/`), and `MII-KDS_en_Consent.jpg` for the English index page. The CC-BY badge
stays an absolute link to `licensebuttons.net`, as in the source.

**Directive residues:** the harvest is a *rendering*, so `fql-scan.sh` finds 0 directives by design.
What it cannot see are Simplifier's **own** render-failure messages, of which the source carries 5:
4× `Command 'pagelink' could not render: Page not found` on the Consent page (resolved per the
crosswalk to links to the Policy ValueSet artefact page — the link text named it) and 1× `Command
'xml' could not render: File not found` on the Provenance page (resolved to a link to the Provenance
example). No literal was left in the tree.

**Template pages that received no source content — recorded gaps, each stated on the page itself:**
`researcher-guidance` (the source has no researcher-facing section; so does the MII reference module
`kerndatensatz-basis`), `capability-statements` (the module ships none), `logical-models` (the module
ships none; the model lives in ART-DECOR), `missing-data` (the source says nothing about it), and the
risk/conformance-statement/residual-risk sections of `security-and-privacy`. `downloads` and
`metadata` describe this repository's own publication machinery; their remaining prompts are template
setup items for the module owners and now say so.

**Not created:** no page outside the template's fixed page set (spec §9). 18 source pages → sections
within the existing 22 pages plus 6 `intro-notes` files per language.

**Language direction (spec §4.2):** German is the source and stays the **authoritative** text under
`input/translations/de/`; the English `input/pagecontent/*.md` are **machine translations marked
`TODO:REVIEW` for Gate C**. Legally binding consent wording — policy displays, Broad-Consent version
and module labels, the answer designators — is **not** translated anywhere; it stays German with a
note saying why. `translationinfo.md` states the whole arrangement in both languages.

**Source files retained for Gate-D retirement (listed, not removed):** `ressourcen-profile/`,
`terminologie/`, `searchparameters/`, `examples/`, `figures/`, `sushi-config.gofsh-derived.yaml`.
**Template artefacts deleted (guardrail 5):** `input/fsh/profiles/example-patient.fsh`,
`input/fsh/instances/example-patient-instance.fsh`, the demo page `rendering-artifacts.md` + its
German mirror + its generator and `pages:`/menu entries, and the `tests/profiles/` fixtures that
validate the deleted example.

## Identity (what makes this module *this* module — verified unchanged)

| Field | Value | Same as source? |
|---|---|---|
| `id` | `mii-ig-consent` | new (the source has none; template pattern) |
| `packageId` | `de.medizininformatikinitiative.kerndatensatz.consent` | yes (tier P) |
| `canonical` | `https://www.medizininformatik-initiative.de/fhir/modul-consent` | yes — 13 of 13 packaged resource urls agree; template pattern agrees |
| `version` | `2026.0.0` | yes (tier P) — DIVERGES from goFSH's `1.0.8` → D5 |
| `status` | `draft` | yes (packaged IG) — DIVERGES from template default `active` → D7 |
| `license` | `CC-BY-4.0` | yes (tier R, twice) |
| `publisher` | template default | **UNRECOVERED → D1** |
| `dependencies` | `de.einwilligungsmanagement 2.0.2-snapshots` (source pin 2.0.2 + local rebuild), `hl7.fhir.uv.crmi 2.0.0` | source pin kept → D4/D6; CRMI added as template machinery (the `meta.profile` claims require it) |
| resource ids / urls | unchanged, including the Forge GUIDs | yes — guardrail 1 |

### Where each value came from (generated — do not retype)

Tiers: **P** published package · **R** source repository · **G** goFSH (never identity).
Generated by `bash migration-log.sh claims --markdown` from `migration-log/identity-claims.tsv`:

| Field | Tier | Source | Value | Contradiction |
|---|---|---|---|---|
| packageId | P | `package/package.json` | de.medizininformatikinitiative.kerndatensatz.consent | — |
| version | P | `package/package.json` | 2026.0.0 | YES — Gate A (D5) |
| description | P | `package/package.json` | KDS Modul Consent Release 2026.0.0 | YES — Gate A (D3) |
| fhirVersions | P | `package/package.json` | ["4.0.1"] | — |
| jurisdiction | P | `package/package.json` | urn:iso:std:iso:3166#DE | — |
| dependency:de.einwilligungsmanagement | P | `package/package.json` (source pin) | 2.0.2 | YES — Gate A (D6) |
| dependency:hl7.fhir.r4.core | P | `package/package.json` (source pin) | 4.0.1 | — |
| canonical | P | packaged resource urls (13 of 13 agree) | https://www.medizininformatik-initiative.de/fhir/modul-consent | — |
| title | R | `README.md` first heading | Medizininformatik Initiative - Modul Consent | candidate — Gate A (D2) |
| license | R | `LICENSE` (text matched) | CC-BY-4.0 | — |
| license | R | GitHub `license.spdx_id` | CC-BY-4.0 | — (independent agreement) |
| description | R | GitHub repository description | Kerndatensatzmodul Consent | YES — Gate A (D3) |
| version | G | `sushi-config.gofsh-derived.yaml` | 1.0.8 | YES — Gate A (D5) |
| dependency:de.einwilligungsmanagement | G | `sushi-config.gofsh-derived.yaml` (dist-tags.latest, run 1) | 2.0.3 | YES — Gate A (D6) |

**Still unrecovered after every tier (a human supplies these):** `publisher` (D1), plus the
template-defaulted values in D10. The rendered Simplifier guide was measured as **client-rendered**
(HTTP 200, 22 616 bytes, 5 script markers, **0 identity markers**) and used as a *human* reference
only — nothing was extracted from it.

**Parent packages missing snapshots (spec §5.1b.5):** `de.einwilligungsmanagement@2.0.2` —
**21 of 21** StructureDefinitions carry none (2.0.3 likewise), rebuilt with the official HL7
generator as `de.einwilligungsmanagement#2.0.2-snapshots` (**18 of 21** generated and verified,
**3 refused** by the generator on a malformed upstream differential, none of them used by this
module), SUSHI **5 → 0** errors. **How the rebuild reaches CI:** vendored + an installer step →
**D4**. Upstream `#2.0.2` re-verified after installing: still 0 of 21 snapshots — untouched.

## Protocol (what was executed — for auditors; keep last)

Generated from `migration-log/run.log` (the narrative re-migration = **run 6**; runs 1–5 are earlier
invocations and remain in the log).

| Step | What ran (`cmd=` from the log) | Measured outcome | Raw log | WARN/ERROR → queue | Acceptance |
|---|---|---|---|---|---|
| 2.1 | `package-identity.sh --package de.medizininformatikinitiative.kerndatensatz.consent --version 2026.0.0` | 8 fields; canonical unanimous 13/13; `title`/`license`/`publisher` absent from the manifest | run.log | `ig-url-not-canonical:`, `not-in-a-package-manifest:` → ① | met |
| 2.1 | `repo-identity.sh --dir <mirror> --repo medizininformatik-initiative/kerndatensatzmodul-consent --rendered …/miiigmodulconsent` | 4 fields; licence CC-BY-4.0 twice; tags 2026.0.0 … 1.0.7; guide 200/22 616 B/0 identity markers | run.log | `identity-contradiction:` (description) → ①, `not-recoverable-from-a-repository: publisher` → ① (D1), `client-rendered-page:` → ② | met |
| 5.2 | vendor template v0.6.0 → module root | 206 files copied, **6 skipped** (skip list in the log) | run.log | none | met |
| 5.2 | `bash scripts/first-run-bootstrap.sh --apply` | 6 template release-automation paths removed; **branch setup declined** (this repo's default branch is `master`, not `main`) | `first-run-bootstrap.log` | `branch-setup-declined:` → ③ (informational) | met |
| 5.1b.5 | `parent-snapshots.sh build --package de.einwilligungsmanagement --version 2.0.2 --validator validator_cli.jar 6.10.0 --install --replace --require …DocumentReference …Provenance …Consent` | 18 of 21 generated (`DocumentReference` 61/45/8, `Provenance` 65/32/20, `Consent` 132/57/32 = snapshot/base/differential), all 3 required present, installed as `#2.0.2-snapshots` | `parent-snapshots.log` | `silent-partial-success: 18 of 21`, `generator-refused:` ×3 → ① (D8) | met (`--require` all satisfied) |
| 5.2 | `npx --yes fsh-sushi@3.20.0 .` with the **upstream** pin 2.0.2 | **5 errors**, 2 warnings (3 × `missing a snapshot` + 2 consequential `InstanceOf … not found`) | `sushi-skeleton-upstream-pin.log` | `anticipated-nonzero-exit:` → ① | met-as-qualified (§5.1b.4) |
| 5.2 | `npx --yes fsh-sushi@3.20.0 .` with the **rebuilt** pin 2.0.2-snapshots | **0 errors**, 5 warnings, 21 resources exported | `sushi-skeleton.log` | none | **met** |
| 5.5 | `gen-page-title-po.py fsh-generated/resources/ImplementationGuide-mii-ig-consent.json migration-log/menu-titles-de.txt de input/translations/de/ImplementationGuide-mii-ig-consent.po` | 23 pages / 23 units / **0 untranslated**; 1 unit dropped (the deleted demo page) | `gen-page-title-po.log` | 4 seed/unit WARNs → ② (informational) | met |
| 5.4 | `fql-scan.sh --strict` | 22 files scanned, **0 directives**, exit 0 | `fql-scan.log` | none | met (no Simplifier/FQL directives — there is no migrated narrative) |
| 5.6 | `docker run … kds-ig-toolchain:v0.4.0 java -Xmx6g -jar /opt/publisher.jar -ig ig.ini -tx n/a` | `err = 84, warn = 157, info = 543, Broken Links: 0` | `qa-build.log` | none | met-as-qualified — every error classified in ③ |
| **5.1c** | `guide-harvest.sh --guide-url https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent?version=2026.0.0 --out migration-log/guide-harvest/pagecontent --keep-html …` | `discovered=18 harvested=18 skipped=0 short=0 artefact_views=4 assets=3`, exit 0 | `guide-harvest.tsv` | 4 × `generated-view-lossy:` → ② (all 22 runs inspected; none is narrative) | **met** |
| **5.4** | `fql-scan.sh --strict input/pagecontent input/intro-notes input/translations/de/pagecontent input/translations/de/intro-notes` | **56 files scanned**, 0 directives, 0 unknown, exit 0 | `fql-scan.log` | none | met |
| **7** | `npx --yes fsh-sushi@3.20.0 .` after the narrative migration | **0 errors**, 5 warnings, 21 resources | `sushi-verify.log` | none | met |
| **5.6** | `docker run … kds-ig-toolchain:v0.4.0 java -Xmx6g -jar /opt/publisher.jar -ig ig.ini -tx n/a` after the narrative migration | `err = 84, warn = 157, info = 542, Broken Links: 0` — **errors and warnings unchanged**, info −1 | `qa-build.log` | none | met-as-qualified — same classification as ③ |
| **5.6** | rendered-output checks (German breadcrumbs, per-language intro-notes, the CodeSystem pointer, images) | `de/…` breadcrumb *Inhaltsverzeichnis \| Terminologie*; `en/…` *Table of Contents \| Terminology*; no cross-language leakage on any of the 3 profile pages; the policy CodeSystem page renders level/display/code/`P30Y`/`Deprecated`; 3 images at the output root | `run.log` | none | **met** |
| 5.6 | the repository's own `.github/workflows/ig-publisher.yml` (run 31094166701) | green in 3 m 8 s; `err = 83, warn = 137, info = 466`; preview pushed to `gh-pages/branches/migration/mii-kds-module-template/` | GitHub Actions | `validation-workflow` environment WARN → ③ | met |

**Log:** `migration-log/run.log` — 6 runs; the one ERROR is run 2’s `sushi-before` (41 errors, the
pre-post-processing baseline), long since resolved.
**Silent-partial-success WARNs:** two. `generated 18 of 21 snapshots` (run 5, the 3 generator
refusals → ① D8), and `documented 15 of 16 package artefacts` (run 6) — the second has **no finding
behind it**: I passed the CRMI expansion manifest as an expected artefact when it is template
machinery with no guide page. The log is append-only, so the WARN stands and its correcting INFO
follows it. The run-2 goFSH conversion reported `converted 20 of 20`; the run-6 harvest reported
`harvested 18 of 18`.
**Deviations from the skill or the template, with justification:**
1. **One step added to the vendored `.github/workflows/ig-publisher.yml`** — it unpacks
   `parent-snapshots/*.tgz` into the FHIR package cache before SUSHI. Without it the
   `2.0.2-snapshots` pin does not resolve on a clean checkout and CI cannot build at all
   (spec §5.1b.5, "carrying it upstream"). Disclosed here and in `parent-snapshots/README.md`.
2. **`first-run-bootstrap.sh` step 1 did not run** — see the protocol row; this is an existing
   repository with `master` as its default branch, and the skill says the module repository's own
   convention wins (spec §5.8). No branch was created and no protection was changed.
3. ~~The narrative was not migrated…~~ **Superseded on 2026-08-06** — see the correction note at
   the top. The narrative *was* migrated, from the server-rendered Simplifier guide; the starter
   pages are gone.
4. **Four harvested pages are committed truncated.** `migration-log/guide-harvest/pagecontent/` holds
   the 14 narrative pages in full, but the 4 `kind=artefact-view` pages (425 / 103 / 102 / 23 KB of
   element trees the IG Publisher regenerates) keep only their provenance header, and the
   `--keep-html` output was not committed at all. Both are reproducible by re-running
   `guide-harvest.sh` against the same pinned URL, and the manifest keeps their character counts.
5. **The English pages are unreviewed machine translations** — the one exception guardrail 3 grants
   (spec §4.2), because every translated page traces to the source page it renders. Every such page
   says so at the top; Gate C is where that stops being true.

## Mini-glossary (novices start here)

- **canonical** — the module's permanent identifying URL; changing it breaks everyone who uses it.
- **snapshot** — the fully resolved element list of a profile. A parent published without one cannot
  be imported; it must be generated with the official tool, never merged by hand.
- **qa.txt / qa.html** — the IG Publisher's validation report; errors block a release, warnings need
  judgement, "broken links" are unresolved references in the rendered site.
- **Gate A–D** — the four human sign-offs: identity (A) → narrative (B) → language (C) → release
  governance (D). The agent never passes a gate itself.
- **TODO:REVIEW** — an in-tree marker meaning "a human must look here"; queue ② lists them all.
- **Run log** — `migration-log/run.log`, the timestamped record of every step, the command it ran and
  what that command measurably produced. The protocol above is generated from it.
- **Guide harvest** — reading a published guide's own rendered pages and converting them to Markdown,
  when the narrative is not in the repository. Anonymous and verified: every discovered page is
  accounted for in `migration-log/guide-harvest.tsv` as harvested-with-counts or skipped-with-a-reason.
- **artefact-view** — a harvested page that is Simplifier's *rendering of a resource this module
  ships* (a profile's element tree, a code system's concept table) rather than prose. The prose above
  the tree is migrated; the rendering is not, because the IG Publisher generates it.
- **intro-notes** — `input/intro-notes/<Type>-<id>-intro.md` / `-notes.md`: prose that renders on an
  artefact's own page, above and below the generated tables. Used here for the three profiles, so the
  per-profile narrative sits where a reader of that profile is looking.
