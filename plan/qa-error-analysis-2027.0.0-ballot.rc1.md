# QA error analysis — 2027.0.0-ballot.rc1 (44 remaining errors)

**Status: ANALYSIS ONLY — no fixes applied** (user instruction 2026-09-01).
Build analysed: branch `migration/2027.0.0-ballot.rc1-template-v0.13.2` @ `fb6a02e`
(develop@744f7ba incorporated), IG Publisher 2.3.2, `output/qa.txt`:
**err = 44, warn = 136, info = 508**.

Every error was classified into one of two categories the release decision needs:

- **PACKAGE-AFFECTING** — the only real fix edits a conformance resource
  (StructureDefinition / CodeSystem / ValueSet) or its identity inside the
  release package ⇒ **enforces a new release package** and is observable by
  implementers (package bytes, file names, validation semantics, or REST ids).
- **NO-CONSEQUENCE** — the fix touches only illustrative material
  (`Usage: #example` instances); the conformance surface implementers validate
  against is bit-identical before and after.

## Executive summary

| Class | Count | Category | One-line fix | Origin | Effort |
|---|---|---|---|---|---|
| A — id/url mismatch (3 SDs + 3 VSs) | 18 | **PACKAGE-AFFECTING** (identity-level, not semantic) | Rename 6 resource `id`s to their canonical tails (upstream #97/#101) | Inherited from source baseline (identical 6 errors in `qa-baseline-source.txt`) | 1–2 h mechanical; real cost = upstream governance |
| B — unresolvable example references | 10 | **NO-CONSEQUENCE** | Add 4 synthetic instances (2 pseudonymous Patients, 2 Domain/ResearchStudy) with the exact referenced UUIDs | Inherited upstream gap (Simplifier never enforced intra-IG resolvability) | 30–60 min |
| C — `Consent.category` slicing not evaluable | 15 | **PACKAGE-AFFECTING** | Give the inherited `templateType` slice (and ideally `resultType`) a system-only `patternCodeableConcept` in the child profile | develop-inherent (parent + develop re-parent construct; any *correct* build surfaces it) | 1–2 FSH lines + upstream issue |
| D — Answer CS "all system" ValueSet | 1 | **PACKAGE-AFFECTING** (form) / effect-neutral (substance) | Make `mii-vs-consent-answer` a bare all-system include (or drop `CodeSystem.valueSet`) | Inherited from source baseline (`qa-baseline-source.txt:423`) | ~15 min |
| **Total** | **44** | | | **0 migration-introduced** | |

Key release facts:

- **None of the 44 errors was introduced by the migration.** A (18) and D (1) are
  byte-identical in the pre-migration source baseline; B (10) is a latent
  upstream gap the IG Publisher merely surfaces; C (15) is inherent to
  develop's re-parenting onto the HL7-D parent (the old baseline hid it only
  because its own snapshot build was defective).
- Fixing **B alone** (examples only) brings qa to **34** with zero package
  consequences. Fixing **B + C + D** reaches **18**; the last 18 (A) are the
  id-modernization question upstream already owns (#97/#101).
- ERROR-severity messages cannot be waived via `ignoreWarnings.txt` — a
  qa-err=0 ballot build requires actual fixes for all four classes.
- Even the PACKAGE-AFFECTING fixes are *validation-outcome-neutral for
  implementer instances* in two of three cases (A: canonicals unchanged;
  D: expansion unchanged). Only C changes slice-membership semantics — and it
  makes currently-unevaluatable slicing evaluable without invalidating any
  existing package example.

---

## Class A — 18 × id/url mismatch → PACKAGE-AFFECTING

### Nature and root cause

Six conformance resources carry legacy technical ids from the
ART-DECOR/Simplifier publication era while their canonical URLs use modern
slugs:

| Resource | id (legacy) | canonical tail | FSH source (Id line) |
|---|---|---|---|
| SD Einwilligung | `e0e166b4-0f77-478d-9062-de0034d98ce0` | `mii-pr-consent-einwilligung` | `input/fsh/profiles/MII_PR_Consent_Einwilligung.fsh:3` |
| SD Provenance | `f675b1e8-9f3f-44e8-bb59-9681f78eb464` | `mii-pr-consent-provenance` | `input/fsh/profiles/MII_PR_Consent_Provenance.fsh:3` |
| SD DocumentReference | `56375452-bfa1-4111-af7c-5b5ba9a1857c` | `mii-pr-consent-documentreference` | `input/fsh/profiles/MII_PR_Consent_DocumentReference.fsh:3` |
| VS Answer | `2.16.840.1.113883.3.1937.777.24.11.30--20210323234509` | `mii-vs-consent-answer` | `input/fsh/valuesets/MII_VS_Consent_Answer.fsh:2` |
| VS Policy | `2.16.840.1.113883.3.1937.777.24.11.36--20230331232804` | `mii-vs-consent-policy` | `input/fsh/valuesets/MiiConsentPolicyValueSet.fsh:2` |
| VS SignatureTypes | `88464c5b-5338-4c2b-9c07-b42fef2ada64` | `mii-vs-consent-signaturetypes` | `input/fsh/valuesets/MII_VS_Consent_SignatureTypes.fsh:2` |

Exactly **3 validator flavors fire per resource, 3 × 6 = 18** (all inside each
resource's per-file block in `output/qa.txt`):

1. Load-time canonical-consistency check — expected canonical := IG base +
   `/<Type>/` + id: "Conformance resource … the canonical URL (…/<Type>/<id>)
   does not match the URL (…). Use the special-url parameter…" (qa.txt:285,
   365, 621, 708, 728, 736).
2. "`<Type>.url`: Resource id/url mismatch: `<id>/<url>`" (qa.txt:286, 366,
   622, 711, 731, 739).
3. End-of-block publisher check keyed to the file path: "URL Mismatch
   `<base/Type/id>` vs `<declared url>`" (qa.txt:363, 619, 706, 726, 734, 746).

**The 2 urn:oid CodeSystems contribute ZERO errors to this class.** Their urls
are `urn:oid:…` (not base-derived) AND they are already exempted via the
`special-url` parameter (`sushi-config.yaml`, mirrored in the generated IG
resource). Their own qa hits (e.g. qa.txt:72) belong to other classes.

**Inherited, not migration-introduced:** the pre-migration source baseline
shows the identical 6 "Resource id/url mismatch" errors
(`migration-log/qa-baseline-source.txt:580,586,596,613,618,623`), and the
published upstream package
(`de.medizininformatikinitiative.kerndatensatz.consent#dev`) ships the same
UUID/ART-DECOR-keyed file names. The migration deliberately preserved upstream
identity; upstream issues **#97/#101** already request the id modernization.

### Fix proposals (ranked)

1. **id := canonical tail (the #97/#101 modernization), coordinated with
   upstream, shipped in the ballot package.** Clears all 18. Touch list in this
   tree: 6 FSH `Id:` lines (the `^url` caret lines become redundant-but-harmless
   since SUSHI then derives the same url); rename 6 filename-keyed intro notes
   (`input/intro-notes/StructureDefinition-<uuid>-intro.md` ×3 +
   `input/translations/en/intro-notes/` ×3 — the publisher matches them by id,
   so unrenamed notes **silently stop rendering**); rename 12 translation
   overlays (`translations/en/json/` ×6, `translations/en/xliff/` ×6, incl.
   internal id fields); rewrite id-based `.html` links in
   `input/pagecontent/profiles.md:20-22,26`, `uml-diagrams.md:10,16,18`,
   `value-sets.md:15,35` and the same three files under
   `input/translations/en/pagecontent/`; optionally annotate the dated
   migration logs. Everything under `fsh-generated/` and `output/` regenerates.
2. **Keep the errors for the RC (do nothing).** Defensible under the migration
   guardrail of identity fidelity: the class exists byte-for-byte in the
   upstream baseline; fixing it unilaterally makes the migrated package diverge
   from the official one before upstream decides #97/#101.
3. **Not recommended — extend `special-url` with the 6 slug canonicals.**
   Misuses the parameter (the template's own comment restricts it to canonicals
   NOT starting with the module base — these DO); at best silences flavor 1 and
   leaves the modernization undone.
4. **Forbidden — url := base/Type/uuid.** Canonicals are never changed by a
   migration; would break every downstream binding/derivation.

### Categorization: PACKAGE-AFFECTING (identity-level, not semantic)

The fix rewrites the `id` inside 6 of the release package's conformance
resources — the payload itself — so it can only ship as a new release package,
and implementers can observe it: package file names change
(`package/StructureDefinition-<uuid>.json` → `-<slug>.json`, plus
`package/xml/*.sch`), `.index.json` id+filename entries change,
`ImplementationGuide.definition.resource.reference` Type/id values change, and
REST `Type/id` addressing of package resources on loaded servers breaks.

Crucial nuance: **the conformance/validation surface is untouched.**
Canonical-based resolution — the normative path — is unaffected: every
canonical URL, snapshot, binding, `baseDefinition`
(→ `http://fhir.de/ConsentManagement/StructureDefinition/Consent` 2.0.3),
`meta.profile`, and `supportedProfile` already references the slug canonicals,
which do not change; validation results for instances are byte-identical.

### Secondary effects

- Package bytes: 6 payload file names + `.index.json` + IG Type/id references
  + the `id` element in each resource.
- Rendered site: artifact page URLs change (`StructureDefinition-<uuid>.html` →
  `-<slug>.html` incl. `-definitions`/`-examples` variants); existing deep
  links (branch previews recorded in `migration-log/comparison-table.md`) 404.
- Tree hygiene: filename-keyed intro notes and translation overlays must be
  renamed in lockstep or are silently dropped.
- Package-diff tooling (Simplifier-style) shows 6 removed + 6 added artifacts.

### Effort

Mechanical: ~26 file touches (6 FSH edits, 18 renames, 6 page-link edits) +
rebuild + qa re-run — 1–2 h. The real cost is governance: alignment with
upstream #97/#101 so the official 2027 package makes the same rename;
otherwise prefer option 2 for the RC.

---

## Class B — 10 × unresolvable example references → NO-CONSEQUENCE

### Nature and root cause

`output/qa.txt` contains exactly 10 `nicht auffindbar` ERRORs (lines 148–149,
155–156, 194–195, 202–203, 206, 259). Four distinct dangling target ids,
referenced from 6 example instances:

| Dangling target | Referenced from |
|---|---|
| `Patient/9b4a702d-162c-428a-8c5d-8b98af21b693` (5×) | `34150a23-….fsh:25` (`Consent.patient`); `89f494a3-….fsh:17`; `Example-MII-Consent-ResultType-document.fsh:24`; `8a3d1799-….fsh:8` (`DocumentReference.subject`, harvested source comment "literale Referenz auf den Patienten"); `55219d12-….fsh:18` (`Provenance.signature[0].who`) |
| `Patient/531cef77-2a30-4283-944d-affaf9ae234e` (1×) | `5143266b-….fsh:16` (`Consent.patient`) |
| `ResearchStudy/d7a65ce8-2810-401a-b0db-70782a7b19a6` (3×) | DomainReference `domain` valueReference in `34150a23-….fsh:7`, `89f494a3-….fsh:7`, `Example-MII-Consent-ResultType-document.fsh:7` |
| `ResearchStudy/c946ae17-e3e6-4178-b5ea-15f95aaeeeb4` (1×) | `5143266b-….fsh:7` |

**Root cause: inherited upstream gap, not a migration defect.** The upstream
package ships exactly the same 6 examples and NO Patient/ResearchStudy
instances. The Simplifier pipeline never enforced intra-IG reference
resolvability; the IG Publisher does, so the faithful migration surfaces the
latent dangling references.

**Profile context** (parent `de.einwilligungsmanagement#2.0.3-snapshots`):
`Consent.patient` 1..1 `Reference(ConsentManagement/Patient)` with
`.reference` 0..1 / `.identifier` 0..1 (logical references profile-legal);
DomainReference `domain` 1..1 `Reference(Domain/Organization |
Domain/ResearchStudy)`; the ConsentManagement **Patient profile is pseudonymous
by design** (`identifier` 1..*, typed via ContextIdentifierType
MR/GKV/PKV/ANON/PI/PT/VN; no name/birthDate mandated);
Domain/ResearchStudy requires `identifier` 1..* + `title` 1..1. The IG's own
Einwilligung profile marks both `patient.reference` and `patient.identifier`
mustSupport — literal and logical style are both in-contract. The module's own
privacy guidance (`security-and-privacy.md`) treats literal references as
legitimate inside a consent-management context; replacement is an export-time
(DIMP) concern.

### Fix options, ranked

1. **RECOMMENDED — add 4 synthetic example instances with the EXACT referenced
   ids** (2 Patients + 2 ResearchStudies) as new FSH files under
   `input/fsh/instances/`, `Usage: #example`, conforming to the parent
   profiles: Patient = one pseudonymous identifier (type `ANON`/`PI`,
   synthetic system+value — inherently PII-free, matching the privacy
   guidance); ResearchStudy = synthetic identifier + title + status.
   Precedent: the Symptome migration added 2 synthetic Patients and reached
   qa err=0. Resolves all 10 errors, keeps the 6 upstream-harvested examples
   byte-faithful (incl. the "literale Referenz" demonstration). Caveat: the
   added instances MUST conform to the reference targetProfiles, or the
   validator trades not-found for target-profile-conformance errors.
2. **Switch to identifier-only logical references** in the 6 examples.
   Profile-legal and arguably the module's own privacy best practice — but it
   edits the verbatim-migrated upstream examples, losing fidelity to the
   Simplifier source and creating reviewable semantic drift for the ballot.
3. **Leave as-is.** 10 ERRORs persist; not waivable → ballot goal qa err=0
   unreachable. Not viable.

### Categorization: NO-CONSEQUENCE

Example instances are `Usage: #example` — illustrative, not part of the
conformance surface. No SD/CS/VS/SP changes; the usage contract implementers
validate against is bit-identical.

Secondary effects: package byte content grows by 4 example resources; 4 new
rendered pages + artifact-index entries; SUSHI auto-registers the instances in
`ImplementationGuide.definition.resource` (metadata listing, not conformance
semantics).

### Effort

Small: ~4 short FSH files (~10–15 lines each) + rebuild + qa re-run to confirm
the 10 clear with no replacement errors. ~30–60 min.

---

## Class C — 15 × "Slicing kann nicht ausgewertet werden" (Consent.category) → PACKAGE-AFFECTING

### Nature and root cause

All 15 errors (qa.txt:144–147, 152–154, 190–193, 198–201) name the SAME slice:
`Slice $this in Profil Consent.category:templateType … hat keinen fixed Value,
kein Binding oder existence assertions`. They hit 4 example instances, one
error per `category` repetition: `34150a23…` (4 codings), `5143266b…` (3),
`89f494a3…` (4), `Example-MII-Consent-ResultType-document` (4) = 15.

**Parent slicing (critical):** the HL7-D parent
`http://fhir.de/ConsentManagement/StructureDefinition/Consent` 2.0.3 itself
slices `Consent.category` with discriminator `{type: pattern, path: $this}`,
`rules: open`, and defines THREE slices — `consentCategory` (no pattern/fixed),
`resultType` (only a **required** binding to `…/ValueSet/ResultType`),
`templateType` (only an **extensible** binding to `…/ValueSet/TemplateType`).
None carries a pattern. `resultType`/`templateType` are NOT new child slices —
the child differential contains only `consentCategory` (adds
patternCodeableConcept loinc#57016-8) and `mii` (new slice, version-modules
pattern); SUSHI optimized the FSH re-declarations of `resultType`/`templateType`
(`MII_PR_Consent_Einwilligung.fsh:45-54`) out of the differential because they
are exactly redundant with the parent snapshot.

**Why the validator fails:** for a `pattern`/`$this` discriminator the
validator must derive a matching rule per slice from fixed[x], pattern[x], a
**required** binding, or existence assertions. `consentCategory`+`mii` have
patterns; `resultType`'s required binding is accepted (never named in an
error); `templateType`'s **extensible** binding cannot discriminate (values
outside the VS are legal), so no rule can be built → the validator aborts
slicing evaluation for EVERY `Consent.category` repetition. One error per
category coding in the 4 Consent examples.

**Develop-inherent, not migration-made — with one nuance:** the identical
construct is verbatim in develop's XML
(`Profile_MII_Consent_Einwilligung.xml`). The recorded qa-baseline (same IG
Publisher 2.3.2) shows 0 hits for this class only because THAT build's
snapshot was itself defective — the parent's
consentCategory/resultType/templateType slices never reached the baseline
snapshot. The defect is a latent develop+parent inheritance that any CORRECT
build (proper resolution of the 2.0.3 parent, as the migration does) surfaces.

### Fix options, ranked

1. **RECOMMENDED — give the inherited `templateType` slice a discriminating
   system-only pattern in the child**:
   `* category[templateType] ^patternCodeableConcept.coding[0].system =
   "http://fhir.de/ConsentManagement/CodeSystem/TemplateType"`
   (analogous, optional but advisable for robustness, for `resultType` with
   `…/CodeSystem/ResultType` — today it discriminates only via
   terminology-dependent required-binding evaluation). FHIR-correct: a derived
   profile may constrain inherited slices; each of the 4 slices then
   discriminates on a DISTINCT system (loinc / mii version-modules / fhir.de
   ResultType / fhir.de TemplateType — both VS include exactly one system,
   verified in the parent package), fully compatible with the parent's `$this`
   pattern discriminator. Codings from other systems fall into the open
   portion (rules=open), matching the binding's intent.
2. **Upstream issue to HL7-D `de.einwilligungsmanagement`** — the defect's true
   home is the parent (its own templateType slice is non-discriminable, and
   even its consentCategory slice has no pattern). Right long-term, but outside
   this IG's control and not achievable for the 2027 ballot; do it IN ADDITION
   to (1).
3. **REJECTED — change the discriminator** (e.g. to value/`coding.system`): a
   derived profile must not redefine the discriminator of inherited slicing;
   incompatible re-slice, validator-rejected.
4. **REJECTED — drop/ignore the slices**: SUSHI already emits no differential
   for them; they arrive via the parent snapshot regardless.

### Categorization: PACKAGE-AFFECTING

The only real fix edits `StructureDefinition/mii-pr-consent-einwilligung` — a
conformance artifact implementers validate against. Adding the pattern changes
slice-membership semantics (a category CodeableConcept without the fhir.de
TemplateType system no longer matches the slice) and the profile's byte
content ⇒ enforces a new release package. No currently-valid instance becomes
invalid (slice min=0, all package examples keep validating), but the
conformance surface changes. Not MIXED: the examples are correct; nothing
example-only fixes this.

Side effects: qa errors drop 44→29; profile snapshot/HTML/CSV renderings
change; no file renames, no page links affected; instances untouched.

### Effort

Small: 1–2 FSH lines in `MII_PR_Consent_Einwilligung.fsh` (after line 54) +
rebuild + re-QA; plus filing the upstream issue.

---

## Class D — 1 × Answer CodeSystem "all system" ValueSet → PACKAGE-AFFECTING (form), effect-neutral (substance)

### The error (exact)

`output/qa.txt:72`:
> `ERROR: CodeSystem/2.16.840.1.113883.3.1937.777.24.5.2--20210423105554:
> CodeSystem: CodeSystem urn:oid:2.16.840.1.113883.3.1937.777.24.5.2 hat einen
> 'all system' ValueSet von
> https://…/ValueSet/mii-vs-consent-answer, aber das Include beeinhaltet
> zusätzliche Details`

(Validator message `CODESYSTEM_CS_VS_INCLUDE_DETAILS`.)

### Nature and root cause

- The Answer CS (`content: complete`, 3 codes) declares
  `valueSet: …/ValueSet/mii-vs-consent-answer`
  (`MII_CS_Consent_Answer.fsh:16`).
- FHIR R4 requires `CodeSystem.valueSet` to point at the implicit
  all-codes VS — its compose must be a single bare `include {system}` with no
  extras.
- `mii-vs-consent-answer` instead composes the system PLUS an explicit
  `concept` list of all 3 codes, each with designations (de-DE/en-US) and a
  `valueset-concept-comments` extension (`MII_VS_Consent_Answer.fsh:20-54`) —
  the "zusätzliche Details".
- **All-system-equivalent?** Extensionally YES today (identical expansion);
  intensionally NO — a frozen enumeration that would silently stop covering
  the CS if a concept were added. A **real (mild) metadata defect**, not
  validator pedantry — practical impact nil today.
- Proof by contrast: the sibling Policy CS (124 codes) declares
  `valueSet → mii-vs-consent-policy`, whose compose IS a bare include — no
  error.
- **In the source baseline: YES** (`qa-baseline-source.txt:423`, identical
  error, English wording) — inherited, not migration-introduced.
- **Usage:** no SD in the target build or the parent package binds
  `mii-vs-consent-answer` (zero grep hits); it appears only narratively
  (IHE-BPPC guidance in the Policy VS description) and in the artifact list.

### Fix proposals (ranked)

1. **Simplify the VS compose to a bare all-system include** — replace
   `MII_VS_Consent_Answer.fsh:20-54` with
   `* include codes from system MII_CS_Consent_Answer`. Root-cause fix; the VS
   becomes intensionally the all-codes VS (future-proof); the CS stays
   byte-identical to upstream. Information loss negligible: the CS concepts
   already carry the SAME designations; only the 3 documentation-only
   `valueset-concept-comments` extensions disappear; expansion unchanged.
   Bonus: the two SNOMED designation-`use` WARNINGs on the VS side don't recur.
2. **Remove the `^valueSet` declaration from the CS** — delete
   `MII_CS_Consent_Answer.fsh:16`. Minimal one-line diff, keeps the VS exactly
   as upstream authored it, but drops the useful CS→all-codes-VS
   discoverability link and leaves the VS a change-fragile enumeration.
3. **Do nothing / report upstream** — not viable for a clean ballot QA; the
   defect should ADDITIONALLY be reported upstream since the source baseline
   ships it.

### Categorization: PACKAGE-AFFECTING (form), effect-neutral (substance)

Either fix edits a canonical conformance resource (ValueSet.compose or
CodeSystem.valueSet) in the release package ⇒ enforces a new release package.
Nuance for the release decision: the *effective* usage contract does not
move — the expansion stays the identical 3 codes, no profile binds the VS, and
`CodeSystem.valueSet` plays no role in instance validation. Bytes change;
no implementer's validation outcome changes.

Side effects: one package file's bytes change; the VS page loses its
per-concept comments table (option 1). No renames, no link changes.

### Effort

Trivial: 1 FSH edit + rebuild + QA re-check. ~15 minutes.

---

## Suggested sequencing (when a fix GO is given)

1. **Class B** first (NO-CONSEQUENCE, qa 44→34): pure example additions;
   shippable without any release-package debate.
2. **Class D** (44→33 territory): trivial, effect-neutral; pair with an
   upstream report.
3. **Class C** (−15): 1–2 FSH lines + upstream issue to HL7-D
   einwilligungsmanagement; changes profile bytes ⇒ new package.
4. **Class A** last (−18 → qa 0): hold for upstream #97/#101 alignment; the
   rename is mechanical but its governance (official package identity) is
   upstream's call. Defensible to ship the RC with these 18 documented.

Package verdict: any qa-err=0 build REQUIRES a new release package (C and D
touch conformance bytes; A touches identity). A "no-new-package" fix pass can
only reach qa = 34 (B alone).
