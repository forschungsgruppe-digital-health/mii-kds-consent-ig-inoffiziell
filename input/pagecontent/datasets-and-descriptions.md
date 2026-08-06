<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE, MACHINE TRANSLATION. English is this IG's default
  language; the module's authored text is German. The German page of the
  same name under input/translations/de/pagecontent/ carries the source
  text and is authoritative until a human confirms this translation.
  Source: the Simplifier-rendered guide miiigmodulconsent, PUBLISHED
  version 2026.0.0 (Default, Read-only, Public, 2025-12-18), harvested
  2026-08-06 (mii-ig-migration, spec 5.1c + 5.1d). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/Datenstzeinkl.Beschreibungen?version=2026.0.0
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/Fragebgen?version=2026.0.0
  TODO:REVIEW at Gate C (translation) and Gate B (narrative).
-->

### Datasets and descriptions

The dataset description of the KDS Consent module is held in full in ART-DECOR:

- [form-based description, MII Dataset, concept 'Consent'](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.184)
- [tabular description, MII Dataset, concept 'Consent'](https://art-decor.org/decor/services/RetrieveDataSet?conceptId=2.16.840.1.113883.3.1937.777.24.2.184)

This covers the descriptions of the MII Broad Consent in the following versions:

- MII Broad Consent version 1.6.d
- MII Broad Consent version 1.6.f

### Questionnaires

The [AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/)
has dealt comprehensively with modelling consents and consent templates. This
implementation guide builds substantially on that work.

#### The structured consent template

The profiles
[Questionnaire Composed](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireComposed.html),
[Template Frame](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateFrame.html)
and [Template Module](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateModule.html)
together represent a consent template. A Template Module is a reusable basic
building block, used or embedded in one or more form sections (Template Frames).

#### The completed consent

The profile
[QuestionnaireResponse](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireResponse.html)
represents the questionnaire the patient filled in. The value set
"[MII Consent: Answer ValueSet](https://art-decor.org/art-decor/decor-valuesets--mide-?id=2.16.840.1.113883.3.1937.777.24.11.30)"
should be used to represent the answers.

> The table below is carried over **verbatim** from the German source page:
> its cells are terminology (codes and the displays the code system publishes),
> and translating a published display would falsify the terminology.
{: .mii-highlight .mii-highlight-grey}

| Checkbox | Code-Bezeichner | Code (OID) |

*Answers (checkbox), code designators and OIDs.*

#### Representing the MII Broad Consent

The data elements of the MII Broad Consent form in versions
[1.6d](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.1790)
and 1.6f are modelled in ART-DECOR.

#### Using uniform policies

The required value sets are likewise modelled in ART-DECOR and associated with
the corresponding data elements. Compatibility with IHE BPPC is taken into
account. The **operationalization and enforcement of the consent information** is
achieved through a
[uniform policy value set](http://art-decor.org/decor/services/RetrieveValueSet?id=2.16.840.1.113883.3.1937.777.24.11.36).

> [TODO:REVIEW — Gate B/C. The German source page carries further detail; this
> translation is a summary of it and must be checked against
> input/translations/de/pagecontent/datasets-and-descriptions.md.]
{: .mii-highlight .mii-highlight-grey}
