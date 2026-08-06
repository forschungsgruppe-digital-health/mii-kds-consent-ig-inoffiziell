<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate C) &mdash; unreviewed machine translation</h5>
<p>The authoritative text of this module is <strong>German</strong>. This English page is an
<strong>unreviewed machine translation</strong> of
<code>input/translations/de/pagecontent/implementer-guidance.md</code>, migrated from the
Simplifier-rendered guide (version 2026.0.0, harvested 2026-08-06). Consent policy wording,
policy display names and the names of the MII Broad Consent form modules are
<strong>deliberately left in German</strong>: they are legally binding text and identifiers,
not prose. Where the two language variants differ, the German page applies.</p>
</div>

<!--
  GUIDANCE FOR IMPLEMENTERS — ENGLISH (translation).
  Source of record and section provenance:
  input/translations/de/pagecontent/implementer-guidance.md
-->

### Guidance for Implementers

This page collects the domain and technical guidance of the Consent module for
Data Integration Centers and vendors: how the module fits into the overall
project, how the MII Broad Consent is represented via questionnaires, the
recommendations for practical use, and the references.

### Context within the overall project / relations to other modules

The Consent module supports cross-site data-use requests based on the patient's
current consent status at the site.

To relate a person to a consent, the consent carries at least one unique person
identifier (base module: Person). As a rule this is a
[pseudonymous identifier](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html).

#### References to other undertakings

The
[guidance document](https://www.bfarm.de/SharedDocs/Downloads/DE/Forschung/modellvorhaben-genomsequenzierung/Handreichung-zur-Implementierung-beim-LE.pdf?__blob=publicationFile)
on patient information & declaration of participation for the **"Modellvorhaben
Genomsequenzierung bei seltenen und bei onkologischen Erkrankungen"** (model
project on genome sequencing for rare and oncological diseases) under § 64e SGB V,
version V1, recommends in section 2.1.4 (research consent) the use of the MII
Broad Consent from version 1.6d onwards, which in the legal sense corresponds at
least to the base version without additional modules.

### Questionnaires

The [AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/)
has dealt comprehensively with the modelling of consents and consent templates.
This implementation guide builds substantially on that preliminary work.

#### The structured consent template

The profiles
[Questionnaire Composed](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireComposed.html),
[Template Frame](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateFrame.html) and
[Template Module](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateModule.html)
are based on the FHIR resource Questionnaire and serve to represent the consent
form (here: MII Broad Consent).

A Template Module is a reusable basic building block that is used in, or embedded
into, one or several form sections (TemplateFrames). One or several TemplateFrames
can be assembled into a complete, renderable form (QuestionnaireComposed).

#### The completed consent

The profile
[QuestionnaireResponse](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireResponse.html)
represents the questionnaire filled in by the patient. It documents the patient's
answers to the referenced questionnaire (QuestionnaireComposed) of the MII Broad
Consent.

The value set
"[MII Consent: Answer ValueSet](https://art-decor.org/art-decor/decor-valuesets--mide-?id=2.16.840.1.113883.3.1937.777.24.11.30)"
should be used to represent the answers — in this guide the ValueSet
[MII Consent: Answer ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.30--20210323234509.html).
The code designators below are the **German** designators of the code system and
are not translated:

| Checkbox | Code designator | Code (OID) |
| --- | --- | --- |
| "Ja" ticked | gültig | 2.16.840.1.113883.3.1937.777.24.5.2.1 |
| "Nein" ticked | nicht gültig | 2.16.840.1.113883.3.1937.777.24.5.2.2 |
| not ticked | unbekannt | 2.16.840.1.113883.3.1937.777.24.5.2.3 |

*Answers (checkbox), code designators and OIDs*

#### Representing the MII Broad Consent

The data elements of the MII Broad Consent form in versions
[1.6d](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.1790)
and
[1.6f](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.1791)
are modelled as a dataset in ART-DECOR, see
[Datasets and Descriptions](datasets-and-descriptions.html).

#### Using uniform policies

The required value sets are likewise modelled in ART-DECOR and associated with the
corresponding data elements. Compatibility with IHE BPPC (Integrating the
Healthcare Enterprise,
[profile "Basic Patient Privacy Consent"](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_TF_Vol1.pdf#nameddest=19_Basic_Patient_Privacy_Consen))
is addressed via policies.

The **operationalisation and enforcement of the consent information** is supported
by a
[uniform policy value set](http://art-decor.org/decor/services/RetrieveValueSet?id=2.16.840.1.113883.3.1937.777.24.11.36&effectiveDate=2021-04-23T10:55:54&prefix=mide-&format=html&collapsable=true&language=de-DE&ui=en-US).
It can be used interoperably in IHE BPPC. In this guide it is the ValueSet
[MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.html).

### Recommendations for practical use

#### Meaning of categorising Consent resources via ResultType

The IG of the **HL7-D AG Einwilligungsmanagement** and the corresponding
[publication](https://ebooks.iospress.nl/doi/10.3233/SHTI251389) explain the
meaning of the `ResultType` parameter comprehensively.

Particular attention should be paid to the codes `consent-status` and `document`.
Further details and relationships are described
[here](https://simplifier.net/guide/Einwilligungsmanagement/Mitgeltende-Erl-uterungen?version=current).

#### Recommendation on using Consent.category ResultType

Concrete mandatory project requirements on using the ResultType search parameter
are only of limited use in practice, because of the heterogeneous technical
situation at the MII sites. The **technical realisation of the requirements
depends on the concrete implementation**.

The consent management system [gICS](https://ths-greifswald.de/gics) is the
current [reference implementation](https://ebooks.iospress.nl/doi/10.3233/SHTI251389)
of the HL7-D FHIR standard for consent management (version 2.0).

All implementations should support **at least the following variants**. The
cardinality of `Consent.category` is defined as `2..*` and enables the necessary
backwards compatibility.

| ResultType | Meaning for the Consent resource | Aggregation of information |
| --- | --- | --- |
| `document` | The Consent resource refers to **one (!) completed document** (QuestionnaireResponse). *This should be the default in an (MII) FHIR server.* | no |
| `consent-status` | The Consent resource **takes into account all relevant consent and withdrawal documents** in the MII context **for one (!) patient**. A Consent resource with ResultType `consent-status` always refers to one patient and carries the current consent status. *This should ideally be supported by the (MII) FHIR server.* | yes, computed by the corresponding business logic at query time or for a given period |

Ideally the FHIR server should hold only one Consent resource per patient, with
the current aggregated consent information (ResultType `consent-status`).

*If this is not possible for other reasons, at least one document-specific export
per completed document (consent, updated consent, partial withdrawal, full
withdrawal) should be made possible (ResultType `document`). In that case it
remains the site's responsibility to provide this information* **in the form
required by the FDPG**.

##### Recommendations for gICS users regarding key-figure determination and the FDPG

The Data Integration Centers provide the information required to determine
core-dataset-specific key figures for the DIZ dashboard. The determination of the
key figures is triggered on the DIZ dashboard side by corresponding calls to the
sites, for the MII KDS Consent module as well.

Sites using the consent management system
[gICS](https://ths-greifswald.de/gics) should follow the precise
[**vendor recommendations**](https://www.ths-greifswald.de/diz-dashboard-empfehlung-gics-kds-consent-status/)
for **key-figure determination** and for providing the Consent resources to the
**FDPG**.

### References

The modelling of the dataset of the Consent module contains references to the
following projects:

- [Implementation Guide of the working group Einwilligungsmanagement of the Interop-Forum, version 1.0](https://ig.fhir.de/einwilligungsmanagement/stable/)
- [Core Dataset description in ART-DECOR](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.184)

The [HL7 FHIR core specification](http://hl7.org/fhir/) — in particular the
[Consent](http://hl7.org/fhir/consent.html) resource — and the existing work on
the German base profiles in [STU3](https://simplifier.net/basisprofilde) and
[R4](https://simplifier.net/basisprofil-de-r4) were also taken into account.

This specification was designed on the basis of the description of the MII Core
Dataset in the version of 10 March 2017
([PDF](https://www.medizininformatik-initiative.de/sites/default/files/inline-files/MII_04_Kerndatensatz_1-0.pdf)),
and of the dataset description in
[ART-DECOR](https://art-decor.org/art-decor/decor-project--mide-).
