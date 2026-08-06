<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate C) &mdash; unreviewed machine translation</h5>
<p>The authoritative text of this module is <strong>German</strong>. This English page is an
<strong>unreviewed machine translation</strong> of
<code>input/translations/de/pagecontent/search-parameters-and-operations.md</code>, migrated
from the Simplifier-rendered guide (version 2026.0.0, harvested 2026-08-06). Search-parameter
codes, FHIRPath expressions, OIDs and the query examples are reproduced
<strong>verbatim</strong>. Where the two language variants differ, the German page applies.</p>
</div>

### Search Parameters and Operations

When the FHIR RESTful API is used, the search parameters listed here have to be
implemented by the respective systems. Logical AND and OR combinations of FHIR
search are supported in principle, cf.
[hl7.org/fhir/search.html](http://www.hl7.org/fhir/search.html).

This module defines **no operations of its own**.

#### Category

In the context of this guide the standard search parameter
**`Consent.category`** has to be supported (cf.
[hl7.org/fhir/consent.html#search](http://www.hl7.org/fhir/consent.html#search)).

Example:

```text
GET [base]/Consent?category=2.16.840.1.113883.3.1937.777.24.2.184
```

finds all Consent resources (valid and no longer valid at query time) that
correspond to any version of the MII Broad Consent (e.g. 1.6d, 1.7.2, …).

#### The module's own search parameters

| Search parameter | Type | FHIRPath | Explanation |
| --- | --- | --- | --- |
| [`mii-provision-provision-code`](SearchParameter-MII-SP-Consent-ProvisionCode.html) | token | `Consent.provision.provision.code` | provision code |
| [`mii-provision-provision-type`](SearchParameter-MII-SP-Consent-ProvisionType.html) | token | `Consent.provision.provision.type` | type of the provision (`permit`, `deny`) |
| [`mii-provision-provision-code-type`](SearchParameter-MII-SP-Consent-ProvisionCodeType.html) | composite | `Consent.provision.provision` | type of a particular provision identified by a code |
| [`mii-provision-provision-period`](SearchParameter-MII-SP-Consent-ProvisionPeriod.html) | date | `Consent.provision.provision.period` | provision period |
| [`mii-provision-provision-code-period`](SearchParameter-MII-SP-Consent-ProvisionCodePeriod.html) | composite | `Consent.provision.provision` | period of a particular provision identified by a code |
| [`mii-policy-uri`](SearchParameter-MII-SP-Consent-PolicyUri.html) | uri | `Consent.policy.uri` | policy URI (version-specific MII Broad Consent) |

Examples per search parameter:

```text
GET [base]/Consent?mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8

GET [base]/Consent?mii-provision-provision-type=permit

GET [base]/Consent?mii-provision-provision-code-type=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8$permit

GET [base]/Consent?mii-provision-provision-period=2020-12-15

GET [base]/Consent?mii-provision-provision-code-period=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8$2020-12-15

GET [base]/Consent?mii-policy-uri=urn:oid:2.16.840.1.113883.3.1937.777.24.2.1791
```

#### Search parameters that also apply, per the HL7-D consent-management standard

For searching Consent resources, the
[HL7-D standard for consent management](https://ig.fhir.de/einwilligungsmanagement/stable/Consent.html)
(version 2.0) defines the following search parameters for filtering Consent
resources. They are supported by the MII KDS Consent module as well. Concrete
examples are documented in the IG of the HL7-D working group.

| Search parameter | Explanation |
| --- | --- |
| `domain` | consent domain. Supporting logical references (reference by identifier, i.e. the `:identifier` modifier on the search parameter) is particularly recommended. |
| `category` | kind of document (consent, withdrawal, …); ResultType (document, consent status, …) |
| `patient.identifier` | the data subject, identified by an identifier |

*Note: because a dependency on the package of the HL7-D AG
Einwilligungsmanagement exists, the `domain` search parameter is available
automatically and does not have to be defined explicitly for the CDS module. It
is technically "just inherited".*

#### More complex examples (queries)

```text
GET [base]/Consent?mii-provision-provision-type=permit&mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8&mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.9
```

finds all Consent resources with a permit provision in which both the provision
code `2.16.840.1.113883.3.1937.777.24.5.3.8` and the provision code
`2.16.840.1.113883.3.1937.777.24.5.3.9` are set.

```text
GET [base]/Consent?mii-provision-provision-type=permit&mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.8,mii-provision-provision-code=urn:oid:2.16.840.1.113883.3.1937.777.24.5.3|2.16.840.1.113883.3.1937.777.24.5.3.9
```

finds all Consent resources with a permit provision in which either the provision
code `2.16.840.1.113883.3.1937.777.24.5.3.8` or the provision code
`2.16.840.1.113883.3.1937.777.24.5.3.9` is set.

```text
GET [base]/Consent?domain:identifier=MII&category=http://fhir.de/ConsentManagement/CodeSystem/TemplateType|CONSENT-OPT-IN&category=http://fhir.de/ConsentManagement/CodeSystem/ResultType|document
```

finds all Consent resources of type "Einwilligung" (consent) in a domain `mii` —
one Consent resource per consent document. `Bundle.total` gives the number of
consents.

```text
GET [base]/Consent?category=http://fhir.de/ConsentManagement/CodeSystem/TemplateType|WITHDRAWAL&category=http://fhir.de/ConsentManagement/CodeSystem/ResultType|document
```

finds all Consent resources of type "Widerruf" (withdrawal) — one Consent
resource per withdrawal document. `Bundle.total` gives the number of withdrawals.

```text
GET [base]/Consent?category=http://fhir.de/ConsentManagement/CodeSystem/TemplateType|REFUSAL&category=http://fhir.de/ConsentManagement/CodeSystem/ResultType|document
```

finds all Consent resources of type "Ablehnung" (refusal) — one Consent resource
per refusal document. `Bundle.total` gives the number of refusals.

```text
GET [base]/Consent?domain:identifier=MII&category=http://fhir.de/ConsentManagement/CodeSystem/ResultType|consent-status
```

finds all Consent resources in the domain `mii`. Each Consent resource **takes
into account all relevant consent, withdrawal and refusal documents for one (!)
patient**. A Consent resource with ResultType `consent-status` aggregates consent
information, refers to exactly one patient and represents that patient's current
consent status. At the same time `Bundle.total` corresponds to the number of
patients for whom at least one document with consent information (consent,
withdrawal, refusal) exists.
