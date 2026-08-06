# `parent-snapshots/` — a LOCALLY REBUILT parent package, vendored on purpose

**What is in here:** `de.einwilligungsmanagement-2.0.2-snapshots.tgz`, a copy of the
upstream FHIR package `de.einwilligungsmanagement@2.0.2` **with `snapshot` elements added**.
It is **not** an upstream release, and it must never be published or treated as one.

## Why it exists

`de.einwilligungsmanagement@2.0.2` — the parent IG this module's profiles derive from, and the
version the module's own published package pins — ships **21 StructureDefinitions and 0
snapshots**. SUSHI cannot import a parent without a snapshot:

```text
error Structure Definition http://fhir.de/ConsentManagement/StructureDefinition/DocumentReference
      is missing a snapshot. Snapshot is required for import.
```

Measured on this repository: **5 SUSHI errors** with the upstream pin (3 × `missing a snapshot`
for `Consent`, `DocumentReference`, `Provenance`, plus 2 consequential `InstanceOf … not found`),
and **0 errors** with the rebuild. Version-shopping does not help: `2.0.3` ships 0 snapshots too.

## How it was produced (never hand-rolled)

With the **official HL7 generator** — `validator_cli.jar` **6.10.0**, subcommand `snapshot`,
backed by the same `ProfileUtilities` the IG Publisher uses — driven by
`parent-snapshots.sh build --install` from the `mii-ig-migration` skill (agent-skills v0.12.0):

```bash
bash scripts/parent-snapshots.sh build \
  --package de.einwilligungsmanagement --version 2.0.2 \
  --validator ./validator_cli.jar --install --replace \
  --require http://fhir.de/ConsentManagement/StructureDefinition/DocumentReference \
  --require http://fhir.de/ConsentManagement/StructureDefinition/Provenance \
  --require http://fhir.de/ConsentManagement/StructureDefinition/Consent
```

Result: **18 of 21** StructureDefinitions snapshotted and verified (every snapshot must carry
more elements than its own differential and at least as many as its R4 base's snapshot — a
differential wearing the name `snapshot` is refused). **3 of 21 were refused by the generator**
— `TemplateFrame`, `TemplateModule`, `QuestionnaireComposed` — all with the same cause, a
malformed **upstream** differential:

> `Questionnaire.item.text.extension:renderingMarkdown.value[x]:valueMarkdown` launches straight
> into slicing without the slicing being set up properly first

None of the three is a `Parent` or `InstanceOf` target in this module's FSH, so none blocks the
build. **They were not hand-finished** — that would fabricate a parent.

Only the `snapshot` property was added; every other field is the upstream bytes re-serialized, so
do not expect byte equality with upstream. Upstream `de.einwilligungsmanagement#2.0.2` in the FHIR
package cache is **untouched** (re-verified after the build: still 0 of 21 snapshots).

## How it is consumed

`sushi-config.yaml` pins `de.einwilligungsmanagement: 2.0.2-snapshots`. That id resolves from **no
registry** — it only exists in a FHIR package cache — so the build installs it first:

* **CI:** the step *“Install the vendored snapshot-bearing parent package”* in
  `.github/workflows/ig-publisher.yml` unpacks this tarball into
  `~/.fhir/packages/de.einwilligungsmanagement#2.0.2-snapshots` before SUSHI runs.
* **Locally:** `mkdir -p ~/.fhir/packages/'de.einwilligungsmanagement#2.0.2-snapshots' && tar xzf
  parent-snapshots/de.einwilligungsmanagement-2.0.2-snapshots.tgz -C
  ~/.fhir/packages/'de.einwilligungsmanagement#2.0.2-snapshots'`.

## TODO:REVIEW (Gate A) — this is a decision, not a solution

Vendoring a derived artefact of someone else's package is one of four documented options (the
others: a CI prebuild step that regenerates it, an internal registry, or not re-pinning and
leaving three profiles blocked). It was chosen here so that a **clean checkout builds** and the
preview is reproducible. **The durable fix is upstream**: `de.einwilligungsmanagement` publishing
snapshot-bearing releases. Re-generate this tarball on every parent release; never edit it by hand.
