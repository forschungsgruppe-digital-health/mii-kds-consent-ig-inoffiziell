<!--
  MII_PR_Consent_Einwilligung — intro, ENGLISH (translation).
  Source of record: input/translations/de/intro-notes/<same file name>.
-->

{:.bg-warning}
**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text
of this module is German. This page is an unreviewed machine translation of the
German intro note, migrated from the Simplifier-rendered guide (version 2026.0.0,
harvested 2026-08-06). Consent policy wording and policy display names are left
in German on purpose: they are legally binding text and identifiers. Where the
two language variants differ, the German page applies.

This profile describes an operationalised, automatically generated and
processable consent within the Medical Informatics Initiative.

When a person is enrolled in a study (including an MII use case), a consent is
obtained for that person on the basis of the
[MII Broad Consent model texts](https://www.medizininformatik-initiative.de/de/mustertext-zur-patienteneinwilligung),
and the corresponding consent document is documented in a structured way at the
respective site, following the
[requirements of the MII Task Force Consent Umsetzung](https://art-decor.org/art-decor/decor-datasets--mide-?id=2.16.840.1.113883.3.1937.777.24.1.1&effectiveDate=2018-06-05T12%3A44%3A12&conceptId=2.16.840.1.113883.3.1937.777.24.2.184&conceptEffectiveDate=2018-06-29T16%3A26%3A50&language=de-DE).

The FHIR Consent resource is generated automatically on the basis of these
consent documents. The
[project context](https://ig.fhir.de/einwilligungsmanagement/stable/DomainReference.html)
is preserved.

The resource must be created before participating in cross-site feasibility
requests and data releases. Further obligations and adaptations have to be
checked for each use case.

**Privacy aspects** of this profile — pseudonymous person reference, handling of
person-identifying information, no document scans in the Consent resource — are
on [Security and Privacy](security-and-privacy.html).

### Interoperability

To ensure that the operationalised consent content can be exchanged beyond FHIR
as well, a uniform policy value set for the **semantic representation** of the
statements contained in the MII Broad Consent was agreed with the **MII AG
Consent** in December 2021 and documented in
[ART-DECOR](http://art-decor.org/decor/services/RetrieveValueSet?id=2.16.840.1.113883.3.1937.777.24.11.36&effectiveDate=2021-04-23T10:55:54&prefix=mide-&format=html&collapsable=true&language=de-DE&ui=en-US)
(policy OIDs).

*Using this code system is mandatory for the CDS module Consent.*
