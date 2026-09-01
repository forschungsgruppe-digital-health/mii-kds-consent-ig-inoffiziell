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
| A — id/url mismatch (3 SDs + 3 VSs) | 18 | **PACKAGE-AFFECTING** (identity-level, not semantic) | Rename 6 resource `id`s to their canonical tails (id modernization — needs a NEW upstream issue; #97/#101 are adjacent only) | Inherited from source baseline (identical 6 errors in `qa-baseline-source.txt`) | 1–2 h mechanical; real cost = upstream governance |
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
  id-modernization question, which upstream has NOT yet formally opened —
  adjacent hygiene issues #97 (CS naming) and #101 (CS/VS XML→JSON) show the
  terminology identities are under rework, but neither requests the id rename;
  a new upstream issue is needed. *(Corrected 2026-09-01 — an earlier revision
  of this document overstated #97/#101.)*
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
identity. **Correction (2026-09-01):** upstream issues #97 ("'MII CS Consent
Policy' in 'MII_CS_Consent_Policy' umbennen" — CS naming) and #101 ("CodeSysteme
und ValueSet einheitlich nach JSON transformieren") do NOT request this id
modernization — it must be filed as a new upstream issue; #97/#101 are natural
anchors to reference from it.

### Fix proposals (ranked)

1. **id := canonical tail (the id modernization — file as a new upstream issue,
   referencing adjacent #97/#101), coordinated with
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
   from the official one before upstream decides the id question.
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

Mechanical: ~30 file touches (6 FSH `Id:` edits + 6 intro-note renames +
12 overlay renames + 6 page-link edits) +
rebuild + qa re-run — 1–2 h. The real cost is governance: alignment with
upstream (new issue) so the official 2027 package makes the same rename;
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
   guidance); ResearchStudy = synthetic identifier + title + status **plus the
   parent-mandated `description` (1..1) and ConsentManagement ContextIdentifier
   extension (1..*)** — verified in profile-ConsentManagement-Domain-ResearchStudy.
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

Side effects: qa errors expected to drop 44→29 (confirm by rebuild — once
slicing becomes evaluable, previously-suppressed slice-membership/binding
checks re-activate; the examples' category codings were spot-verified to match
their slices); profile snapshot/HTML/CSV renderings
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
   Bonus: the twelve SNOMED designation-`use` warnings on the VS side
   (qa.txt 714–725: 3 concepts × 2 designations × 2 flavors — the VS block's
   entire warn count) don't recur; the identical CS-side designations keep
   their own twelve.
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
4. **Class A** last (−18 → qa 0): hold for the upstream id decision (file a
   new issue; #97/#101 adjacent); the
   rename is mechanical but its governance (official package identity) is
   upstream's call. Defensible to ship the RC with these 18 documented.

Package verdict: any qa-err=0 build REQUIRES a new release package (C and D
touch conformance bytes; A touches identity). A "no-new-package" fix pass can
only reach qa = 34 (B alone).

---

## Comprehensive classification table — audience: profile/IG authors (2026-09-01)

**Subject:** the MII KDS module **Consent** (repo
`medizininformatik-initiative/kerndatensatzmodul-consent`), migrated from the
ART-DECOR/Simplifier publication pipeline to the HL7 IG Publisher for the 2027
ballot. Branch `migration/2027.0.0-ballot.rc1-template-v0.13.2` (v0.13.2 = the
MII KDS module template used for the IG-Publisher build) @ `fb6a02e`,
IG Publisher 2.3.2, `output/qa.txt` err = 44. Validator quotes are verbatim
German-locale output (`[sic]` marks a verbatim typo); English glosses in
brackets. This table was adversarially verified (3-lens review, 2026-09-01);
it supersedes wordings above where they differ.

Category definitions (tightened): **PACKAGE-AFFECTING** = the fix edits a
validation-relevant conformance artifact (StructureDefinition / CodeSystem /
ValueSet / SearchParameter / CapabilityStatement) or its identity in the
release package ⇒ a new release package is required and implementers can
observe the change. **NO-CONSEQUENCE** = only example instances plus
IG-resource/index bookkeeping change — nothing an implementer validates
against.

| | **A — resource id ≠ canonical URL (18)** | **B — dangling example references (10)** | **C — Consent.category slicing not evaluable (15)** | **D — "all-system" ValueSet contradiction (1)** |
|---|---|---|---|---|
| **Where** | 18 = 3 validator flavors × 6 resources; per-resource blocks in `output/qa.txt` (flavor lines between 285 and 746). | 10 across 6 example instances; 4 distinct dangling targets, referenced 5× / 1× / 3× / 1×; qa.txt 148–259. | 15 = one per `Consent.category` repetition in 4 Consent examples (4+3+4+4; each repetition carries a single coding); qa.txt 144–201 — the range overlaps class B's because qa.txt groups findings per resource and the Consent examples carry both classes. | 1; qa.txt 72. |
| **What the validator reports** | Three messages per resource: (1) *"Conformance resource … the canonical URL (…/`<Type>`/`<id>`) does not match the URL (…). Use the special-url parameter…"*; (2) *"`<Type>.url`: Resource id/url mismatch: `<id>`/`<url>`"*; (3) *"URL Mismatch `<base/Type/id>` vs `<declared url>`"*. | *"Ressource Patient/9b4a702d-… nicht auffindbar"* [resource … not found] — likewise for the other three targets. | *"Slice $this in Profil Consent.category:templateType … hat keinen fixed Value, kein Binding oder existence assertions — Slicing kann nicht ausgewertet werden"* [the slice offers no usable matching rule — slicing cannot be evaluated] — repeated for every category repetition, even those that plainly match another slice. | *"CodeSystem urn:oid:2.16.840.1.113883.3.1937.777.24.5.2 hat einen 'all system' ValueSet von …/ValueSet/mii-vs-consent-answer, aber das Include beeinhaltet [sic] zusätzliche Details"* [declares an all-system ValueSet, but the include contains additional details]; message id `CODESYSTEM_CS_VS_INCLUDE_DETAILS`. |
| **The defect — author's view** | The technical `id` and the canonical `url` disagree on 6 conformance resources: 3 StructureDefinitions (Einwilligung, Provenance, DocumentReference) + 3 ValueSets (Answer, Policy, SignatureTypes) still carry ids minted in the ART-DECOR/Simplifier era (UUIDs like `e0e166b4-…`, OID-timestamp composites like `2.16.…24.11.30--2021…`), while the canonicals use the modern slugs (`mii-pr-consent-einwilligung`, …). The IG Publisher derives the expected canonical as IG base + `/<Type>/` + `<id>` and requires equality. The two urn:oid-canonical CodeSystems (Answer `…777.24.5.2`, Policy `…777.24.5.3`) are NOT in this class: their canonicals are not base-derived and are correctly declared under `special-url`. | The 6 shipped examples reference 2 Patients and 2 ResearchStudies via literal references (`Consent.patient`, `DocumentReference.subject`, `Provenance.signature.who`, and the ConsentManagement DomainReference extension's consent-domain target) that are not in the package — and never were. The Simplifier pipeline never enforced intra-IG reference resolvability; the IG Publisher does, so the faithful migration surfaces a latent gap. | The profile inherits `Consent.category` slicing from its parent, the HL7-Deutschland profile `http://fhir.de/ConsentManagement/StructureDefinition/Consent` 2.0.3 (package `de.einwilligungsmanagement`): discriminator `pattern` on `$this`, `rules: open`, parent slices `consentCategory` / `resultType` / `templateType`; the child adds a fourth slice `mii` (pattern on the MII version-modules CodeSystem) and adds the LOINC `57016-8` pattern to `consentCategory` — 4 slices in the child snapshot. As the HL7 validator implements pattern discrimination (R5-aligned value/pattern merge — stricter than the literal R4 text), every slice must be decidable from `fixed[x]`, `pattern[x]`, a REQUIRED binding, or existence assertions. `templateType` has ONLY an EXTENSIBLE binding — undecidable by definition (values outside the VS are legal) — so the validator abandons slicing evaluation for the entire element. The other three slices are decidable (patterns / required binding). | FHIR R4 `CodeSystem.valueSet` must reference the implicit "all codes of this system" ValueSet, whose compose has to be a single bare `include` of the system — ANY extra detail (a concept enumeration, filters, additional includes) triggers the check. The Answer CS (`content: complete`, 3 codes) declares such a VS, but `mii-vs-consent-answer` enumerates its 3 concepts explicitly; the designations (de-DE/en-US) and `valueset-concept-comments` extensions merely ride along on that enumeration. The expansion is identical today, but the VS is a frozen enumeration: a 4th CS code would silently fall outside it — precisely what the rule guards against. Contrast: the Policy pair passes this check (bare include over the 124-code CS; the Policy VS's own 3 qa errors belong to class A). |
| **Origin** | Inherited from released 2026.0.0 — identical 6 mismatches in the pre-migration baseline QA; the published package ships the same UUID-keyed files. NOT yet requested upstream: adjacent hygiene issues #97 (CS naming) / #101 (CS/VS XML→JSON) do not cover the id rename — a new issue is needed. Not migration-introduced. | Inherited upstream gap — the published package ships the same 6 examples and no targets. Not migration-introduced. | Inherited from the upstream `develop` branch: develop (18 commits to `744f7ba`, 2026-08-21 — predating and independent of this migration) re-parented the profile from the FHIR core Consent resource onto the HL7-D ConsentManagement profile, whose own `templateType` slice is non-discriminable — a design defect in the parent itself. The 2026.0.0 baseline showed zero errors of this class only because its Simplifier-era snapshot was defective (the parent slices never reached it); any build that correctly resolves the 2.0.3 parent surfaces the defect. Not migration-introduced. | Inherited — the identical error is in the pre-migration source baseline. Nothing binds this VS (no StructureDefinition in the IG or the parent package references it; it appears only narratively). Not migration-introduced. |
| **Suggested improvement** | Set each `id` to its canonical tail (`Id: mii-pr-consent-einwilligung`, …). Lockstep renames, or content silently disappears: 6 intro-note files (3 DE `input/intro-notes/StructureDefinition-<id>-intro.md` + 3 EN `input/translations/en/intro-notes/` — SD intros only; the publisher matches them by the id in the filename); 12 overlays in the repo-root `translations/en/json/` + `translations/en/xliff/` (NOT the separate `input/translations/` tree — rename the files AND update the id fields inside them); id-based `.html` links in `profiles.md`, `uml-diagrams.md`, `value-sets.md` (DE + EN). RC alternative: consciously keep the 18 errors until upstream decides the id question. | Add 4 synthetic example instances whose ids are EXACTLY the referenced UUIDs: 2 Patients conforming to `http://fhir.de/ConsentManagement/StructureDefinition/Patient` (pseudonymous by design: one typed identifier, e.g. type `ANON`/`PI`, synthetic system+value — no name, no birthDate ⇒ PII-free by construction) and 2 ResearchStudies conforming to `http://fhir.de/ConsentManagement/StructureDefinition/Domain/ResearchStudy` — which also mandates `description` 1..1 and the ConsentManagement ContextIdentifier extension 1..*, so the minimum content is identifier + title + description + status + that extension (both profiles from `de.einwilligungsmanagement` 2.0.3, the profile's parent package). | Constrain the inherited slice in the child profile with a system-only pattern: `* category[templateType] ^patternCodeableConcept.coding[0].system = "http://fhir.de/ConsentManagement/CodeSystem/TemplateType"`. Advisably the analogous line for `resultType` (`…/CodeSystem/ResultType`): its required-binding discrimination forces ValueSet expansion at slicing-evaluation time, so slice membership silently depends on terminology-server availability and VS version — a pattern makes it decidable offline and deterministically (zero errors today, but fragile). ALSO file the defect upstream with HL7-D `de.einwilligungsmanagement` — the parent is its true home. | Replace the VS compose with a bare all-system include: `* include codes from system MII_CS_Consent_Answer` (project alias for `urn:oid:2.16.840.1.113883.3.1937.777.24.5.2`). Minimal alternative: delete the CS's `^valueSet` line — keeps the VS byte-exact to upstream but drops the CS→all-codes-VS discoverability link and keeps the change-fragile enumeration. Report upstream as well. |
| **Why — and the rejected alternatives** | The canonical URL is the public contract — every binding, derivation, `meta.profile`, `supportedProfile` references it, and the MII Namenskonventionen mandate that established URLs of published artifacts are never changed retroactively — so the `id` is the only movable half. The current ids also violate that same wiki's kebab-case id convention, making the rename a correction toward MII's own rules. Rejected: extending `special-url` with the 6 slugs — it would at best silence the publisher's canonical-pattern flavor while the validator's id/url-mismatch flavors remain, and it papers over the identity defect (the parameter's proper use is externally-governed canonicals like the urn:oid CodeSystems, not base-derived slugs whose id is simply stale). Forbidden: `url := base/Type/<uuid>` — breaks every downstream reference. | Keeps the 6 upstream examples byte-faithful — including the deliberate literal-reference demonstration, which the module's own security-and-privacy page legitimizes inside the consent-management context (literal Patient references are replaced by pseudonymous identifiers only when data LEAVES that context). Caveat: the new instances must genuinely conform to the reference targetProfiles, or the not-found errors just become target-profile-conformance errors — hence the mandatory description/ContextIdentifier content. Precedent: the parallel Simplifier→IG-Publisher migration of the MII KDS Symptome module (same error class) reached qa err = 0 exactly this way. Rejected: rewriting the examples to identifier-only logical references — profile-legal (`.reference` and `.identifier` are both 0..1 and mustSupport) but it edits verbatim upstream content = review-relevant drift for the ballot. Rejected: leaving as-is — ERROR-severity messages cannot be waived via `ignoreWarnings.txt`, so err = 0 is unreachable. | A derived profile may constrain inherited slices — legal, and exactly what patterns are for; each of the 4 slices then discriminates on a DISTINCT code system (LOINC / MII version-modules / fhir.de ResultType / fhir.de TemplateType — each parent VS draws on exactly one system). Category repetitions whose codings match none of the patterns fall into the open portion (`rules: open`) — the extensible binding's intent. Note: a single repetition mixing codings from two discriminating systems would match two slices and error ("matches more than one slice") — keep the four axes in separate repetitions, as the shipped examples do. Rejected: changing the discriminator — a derived profile must not alter the discriminator/ordering or loosen the rules of inherited slicing (rejected at snapshot generation; distinct from re-slicing, the legal slice-within-a-slice mechanism, which also cannot help here). Rejected: dropping the FSH slice re-declarations — no effect; the slices arrive via the parent snapshot (SUSHI already emits no differential for them). | Root-cause fix; the VS becomes intensionally the all-codes VS (future-proof). Information loss negligible — the CS concepts already carry the SAME de/en designations; only the 3 documentation-only comment extensions ("valid"/"not valid"/"unknown") leave the compose; expansion membership unchanged. Bonus: the 12 SNOMED `designation.use` warnings in the VS block (3 concepts × 2 designations × 2 message flavors, qa.txt 714–725 — the block's entire warn count; the validator cannot resolve SNOMED CT without a terminology-server edition — infrastructure noise, not a content defect) disappear; the CS-side designations keep their own 12. Rejected: doing nothing — ERRORs are not waivable. |
| **Release-package impact** | **PACKAGE-AFFECTING** (identity, not semantics): package file names (`StructureDefinition-<uuid>.json` → `-<slug>.json`, plus `.sch`), `.index.json`, IG `Type/id` references, REST `Type/id` addressing on loaded servers, and artifact page URLs all change ⇒ new release package. Validation outcomes for implementer data are byte-identical (canonicals, snapshots, bindings untouched). | **NO-CONSEQUENCE**: `Usage: #example` instances plus IG-resource/index bookkeeping only — nothing an implementer validates against changes. Package grows by 4 example files, the site by 4 pages. | **PACKAGE-AFFECTING**: edits the profile implementers validate against; slice membership becomes system-decidable (that IS the fix). No shipped example changes outcome, nor does any instance that keeps one code system per category repetition; an instance mixing two discriminating systems in one repetition would newly fail multi-slice matching (a theoretical edge under the parent's one-axis-per-repetition design). Expected qa 44 → 29 — to be confirmed by rebuild (re-enabled slice-membership/binding checks are the residual risk). | **PACKAGE-AFFECTING in form, effect-neutral in substance**: a canonical ValueSet's bytes change ⇒ new release package — but nothing binds the VS, the expansion stays the identical 3 codes, and `CodeSystem.valueSet` plays no role in instance validation: no implementer's validation outcome moves. |
| **MII release classification** | **Patch** (technical correction). Footnote-10 test: no ETL adaptation — canonicals untouched (the Namenskonventionen mandate their stability), validation byte-identical; the ids currently violate MII's own id convention, so this corrects a *"Mangel … intensional anders angedacht"* (§4.5.3). No MII rule governs technical ids of published artifacts at all ⇒ formally a TF-Kerndatensatz adjudication on the module team's assessment — file the new upstream issue; release notes must flag the changed package file names / `Type/id` addressing. Even the most conservative "breaking" reading collapses to patch via §4.5.3's small-effort rule. | **Simple patch** — §4.5.3 *"Klarstellungen"*; zero conformance/ETL impact; precedent: consent 2025.0.4 shipped example/display corrections as a patch. The clearest patch of the four. | **Patch** (profile defect correction) — declare prominently in the release notes. Footnote-10 test: no instance becomes invalid, nothing becomes mandatory, no ETL change is forced; the slicing was INTENDED to be evaluable — the literal §4.5.3 case (*"Mängel in der Spezifikation, die intensional anders angedacht waren"*). Precedent: kerndatensatz-basis v2026.0.1 added an optional slice to a published profile in a PATCH. Conservative fallback: feature/change per §4.5.2 (*"substanzielle Änderungen an … Profilen"*) — defensible, but MII practice never uses the MINOR digit, and even a breaking reading collapses to patch (small effort). TF Kerndatensatz adjudicates if contested. | **Simple patch** — textbook §4.5.3 metadata correction; direct precedent: medikation v2026.0.1 shipped a ValueSet-compose correction as a patch. |
| **Effort** | ~30 file touches (6 FSH `Id:` edits + 24 lockstep renames/link edits), 1–2 h + rebuild; the real cost is upstream coordination. | 4 short FSH files, 30–60 min + rebuild. | 1–2 FSH lines + rebuild; plus the upstream issue. | 1 FSH edit, ~15 min + rebuild. |

## MII versioning classification — governance basis

The normative source is the **KDS-Governance v4.0** ("Geschäftsordnung für die
Weiterentwicklung des MII-Kerndatensatzes", NSG-approved, Stand 2026-05-07),
§4.5 "Versionierung": CalVer `YYYY.MINOR.PATCH`, version per module (never per
resource). The three change classes:

- **Breaking change** — defined ONLY operationally (§4.5.1 footnote 10):
  *"Änderung, die zu Anpassung in den ETL-Strecken der Standorte führen muss
  (weil z.B. neue Datenelemente verpflichtend sind)"*. No enumerated technical
  list exists anywhere in MII governance; breaking changes must be recorded in
  the release notes. The year position carries no breaking signal (unlike a
  SemVer major).
- **Feature/change (MINOR)** — §4.5.2: *"neue Funktionen, Erweiterungen oder
  substanzieller Änderungen an bestehenden Objekten wie Informationsmodell
  oder Profilen"*; no NSG approval needed. In practice virtually unused: every
  published module version is `YYYY.0.x`.
- **Patch** — §4.5.3: *"Klarstellungen, Korrekturen von Fehlschreibungen oder
  Mängel in der Spezifikation, die intensional anders angedacht waren"*.
  Explicitly: *"Im Einzelfall kann ein Patch auch einen Breaking Change
  bedeuten … Breaking Changes mit überschaubarem Änderungsaufwand sollen als
  Patches klassifiziert werden."* The Taskforce Kerndatensatz decides contested
  cases on the module team's assessment.
- Observed release practice (implicit governance): patches in the wild carry
  additive terminology (consent 2025.0.2/2025.0.3 added SNID/DZPG policies),
  an added optional slice + MS harmonization (basis v2026.0.1), a
  ValueSet-compose correction (medikation v2026.0.1), packaging cleanups
  (molgen 2026.0.1–.4).

**Bottom line:** none of the four fixes is a breaking change under the
official MII definition (footnote-10 ETL test). The genuinely breaking content
in the 2027 line comes from the develop delta itself (re-parent onto the HL7-D
consent profile, `category` min 2→0, `loinc`→`consentCategory` slice rename),
which the changelog already declares as BREAKING. All four fixes are
patch-class: shipped inside 2027.0.0-ballot.rc1 they simply ride the annual
release (release notes declare A and C explicitly; B and D as corrections);
hypothetically back-ported, all four would be legitimate `2026.0.x` patches
under §4.5.3 and observed practice — A additionally wants TF coordination
because no MII rule covers id changes of published artifacts.

*Caveat: the "MII_KDS_Best_Practices" document (Governance 4.0 Anhang B, where
a finer change taxonomy would live if one exists) is SharePoint-internal and
could not be retrieved; this classification rests on the public governance
PDF, the kerndatensatz-meta wiki, and observed release practice.*
