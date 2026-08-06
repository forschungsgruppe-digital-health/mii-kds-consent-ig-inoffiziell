<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate C) &mdash; mixed page: MII-wide English text plus an unreviewed machine translation</h5>
<p>The MII-wide requirements on this page were authored in English (the German mirror
<code>input/translations/de/pagecontent/conformance.md</code> is their translation). The section(s)
marked <em>&#8220;migrated from the source guide&#8221;</em> below are the opposite direction: their
authoritative text is <strong>German</strong>, migrated from the Simplifier-rendered guide
(version 2026.0.0, harvested 2026-08-06), and the English wording of those sections is an
<strong>unreviewed machine translation</strong>. Where the two differ, the German page applies
for those sections.</p>
</div>

<!-- Default-language (English) page. Overview of the Conformance section. The
     FIRST THREE sub-pages carry the conformance topics of the MII meta wiki page
     "Conformance",
     https://github.com/medizininformatik-initiative/kerndatensatz-meta/wiki/Conformance;
     structure as in kerndatensatz-basis input/pagecontent/conformance.md.
     "Security and Privacy" is an addition of this template per HL7 IG best
     practice — see docs/ig-best-practices-checklist.md.
     German mirror: input/translations/de/pagecontent/conformance.md — both files
     must say the same thing, and both must list the same sub-pages as the two
     menu files. -->

### Conformance

This section defines the conformance requirements for systems implementing the
profiles of the **Consent** module.

* **[General Requirements](general-requirements.html)** — the conformance verbs
  (SHALL/SHOULD/MAY per RFC-2119), claiming conformance, using codes in the
  profiles, and the expectations on the FHIR RESTful API.
* **[Must Support](must-support.html)** — what *Must Support* means for
  data-providing and data-consuming systems.
* **[Handling Missing Data](missing-data.html)** — how missing or unknown values
  are represented.
* **[Security and Privacy](security-and-privacy.html)** — the security and
  data-protection considerations of this module.

The MII meta wiki page
[Conformance](https://github.com/medizininformatik-initiative/kerndatensatz-meta/wiki/Conformance)
is authoritative for the MII-wide conformance rules. General Requirements, Must
Support and Handling Missing Data restate them for this module; where the two
differ, the wiki wins. Security and Privacy is an additional page of this guide,
following HL7's IG best-practice guidance.

#### Technical implementation

*Migrated from the source guide — source of record: the German page, harvested
from `.../TechnischeImplementierung` (version 2026.0.0, 2026-08-06).*

This section describes the syntactic and semantic requirements for implementing
the Consent module.

Search parameters are also defined, which the respective systems have to
implement when using the FHIR RESTful API. Logical AND and OR combinations of
FHIR search are supported in principle, cf.
[hl7.org/fhir/search.html](http://www.hl7.org/fhir/search.html). The module's own
search parameters are listed on
[Search Parameters and Operations](search-parameters-and-operations.html).

At the time this implementation guide was written, the fundamentals and further
details on search and on the FHIR RESTful API were being worked out within the
base modules and may supplement the requirements made here at a later point. A
new version of this guide may then be published.

For implementation guidance see the [Guidance](guidance.html) section; for the
technical artifacts see the [Artifacts](artifacts.html) section.

<div class="mii-highlight mii-highlight-grey" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; no conformance statements were marked</h5>
<p>The migrated source guide phrases its requirements as prose and as
must-support/not-supported entries in the element tables; it marks no sentence as a
conformance statement. <b>No sentence of the migration was turned into one</b> &mdash; wrapping
migrated prose in conformance markers would change how binding it reads, which is a decision
for the module owners, not for a migration. The table below is therefore empty by design. How
the markers work is documented in <code>input/pagecontent/general-requirements.md</code>, which
carries the MII-wide statements the template ships.</p>
</div>

---

### List of Conformance Statements

The table below lists every marked conformance statement of this guide together
with its expectation and a link back to where it is stated.

§§§
