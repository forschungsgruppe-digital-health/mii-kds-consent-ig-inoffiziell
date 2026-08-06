# Conformance - MII Implementation Guide Consent v2026.0.0

* [**Table of Contents**](toc.md)
* **Conformance**

## Conformance

##### TODO:REVIEW (Gate C) — mixed page: MII-wide English text plus an unreviewed machine translation

The MII-wide requirements on this page were authored in English (the German mirror `input/translations/de/pagecontent/conformance.md` is their translation). The section(s) marked **“migrated from the source guide”** below are the opposite direction: their authoritative text is **German**, migrated from the Simplifier-rendered guide (version 2026.0.0, harvested 2026-08-06), and the English wording of those sections is an **unreviewed machine translation**. Where the two differ, the German page applies for those sections.

### Conformance

This section defines the conformance requirements for systems implementing the profiles of the **Consent** module.

* **[General Requirements](general-requirements.md)** — the conformance verbs (SHALL/SHOULD/MAY per RFC-2119), claiming conformance, using codes in the profiles, and the expectations on the FHIR RESTful API.
* **[Must Support](must-support.md)** — what **Must Support** means for data-providing and data-consuming systems.
* **[Handling Missing Data](missing-data.md)** — how missing or unknown values are represented.
* **[Security and Privacy](security-and-privacy.md)** — the security and data-protection considerations of this module.

The MII meta wiki page [Conformance](https://github.com/medizininformatik-initiative/kerndatensatz-meta/wiki/Conformance) is authoritative for the MII-wide conformance rules. General Requirements, Must Support and Handling Missing Data restate them for this module; where the two differ, the wiki wins. Security and Privacy is an additional page of this guide, following HL7's IG best-practice guidance.

#### Technical implementation

**Migrated from the source guide — source of record: the German page, harvested from `.../TechnischeImplementierung` (version 2026.0.0, 2026-08-06).**

This section describes the syntactic and semantic requirements for implementing the Consent module.

Search parameters are also defined, which the respective systems have to implement when using the FHIR RESTful API. Logical AND and OR combinations of FHIR search are supported in principle, cf. [hl7.org/fhir/search.html](http://www.hl7.org/fhir/search.html). The module's own search parameters are listed on [Search Parameters and Operations](search-parameters-and-operations.md).

At the time this implementation guide was written, the fundamentals and further details on search and on the FHIR RESTful API were being worked out within the base modules and may supplement the requirements made here at a later point. A new version of this guide may then be published.

For implementation guidance see the [Guidance](guidance.md) section; for the technical artifacts see the [Artifacts](artifacts.md) section.

##### TODO:REVIEW (Gate B) — no conformance statements were marked

The migrated source guide phrases its requirements as prose and as must-support/not-supported entries in the element tables; it marks no sentence as a conformance statement. **No sentence of the migration was turned into one** — wrapping migrated prose in conformance markers would change how binding it reads, which is a decision for the module owners, not for a migration. The table below is therefore empty by design. How the markers work is documented in `input/pagecontent/general-requirements.md`, which carries the MII-wide statements the template ships.

-------

### List of Conformance Statements

The table below lists every marked conformance statement of this guide together with its expectation and a link back to where it is stated.

§§§

