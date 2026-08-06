<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE, MACHINE TRANSLATION. English is this IG's default
  language; the module's authored text is German. The German page of the
  same name under input/translations/de/pagecontent/ carries the source
  text and is authoritative until a human confirms this translation.
  Source: the Simplifier-rendered guide miiigmodulconsent, PUBLISHED
  version 2026.0.0 (Default, Read-only, Public, 2025-12-18), harvested
  2026-08-06 (mii-ig-migration, spec 5.1c + 5.1d). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/KontextimGesamtprojektBezgezuanderenModulen?version=2026.0.0
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/Referenzen?version=2026.0.0
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Empfehlungen-zur-praktischen-Anwendung?version=2026.0.0
  TODO:REVIEW at Gate C (translation) and Gate B (narrative).
-->

### Context within the overall project / relationships to other modules

The Consent module supports cross-site data-use requests based on the patient's
current consent status at the site.

To establish the relationship between person and consent, the consent carries at
least one unique person identifier (base module: Person). As a rule this is a
[pseudonymous identifier](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html).

#### References to other undertakings

The [guidance document](https://www.bfarm.de/SharedDocs/Downloads/DE/Forschung/modellvorhaben-genomsequenzierung/Handreichung-zur-Implementierung-beim-LE.pdf?__blob=publicationFile)
on patient information for the model project on genome sequencing (§64e SGB V) is
referenced.

### References

The modelling of the Consent module's dataset contains references to the
following projects:

- [Implementation Guide of the Interop-Forum working group on consent management, version 1.0](https://ig.fhir.de/einwilligungsmanagement/stable/)
- [Core dataset description in ART-DECOR](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.184)

The [HL7 FHIR core specification](http://hl7.org/fhir/) — including the
[Consent](http://hl7.org/fhir/consent.html) resource — and the existing work on
the German base profiles were used in addition.

This specification was designed on the basis of the description of the MII core
dataset in the version of 10 March 2017
([PDF](https://www.medizininformatik-initiative.de/sites/default/files/inline-files/MII_04_Kerndatensatz_1-0.pdf)).

### Recommendations for practical use

#### What categorizing Consent resources with ResultType means

The IG of the **HL7-D AG Einwilligungsmanagement** and the corresponding
[publication](https://ebooks.iospress.nl/doi/10.3233/SHTI251389) describe the
meaning of the `ResultType` parameter comprehensively. The codes `consent-status`
and `document` deserve particular attention.

#### Recommendation on using Consent.category ResultType

Concrete, binding project requirements for using the ResultType search parameter
are only of limited use in practice, because the technical situation at the MII
sites is heterogeneous. The consent management system
[gICS](https://ths-greifswald.de/gics) provides the current
[reference implementation](https://ebooks.iospress.nl/doi/10.3233/SHTI251389) of
the HL7-D FHIR standard.

All implementations should support **at least the following variants**. The
cardinality of `Consent.category` is defined as `2..*` and provides the necessary
backward compatibility.

> The table below is carried over **verbatim** from the German source page:
> its cells are terminology (codes and the displays the code system publishes),
> and translating a published display would falsify the terminology.
{: .mii-highlight .mii-highlight-grey}

| ResultType | Bedeutung für die Consent-Ressource | Aggregation von Informationen |

Ideally, the FHIR server should hold only one Consent resource per patient,
carrying the current aggregated consent information (ResultType
`consent-status`).

*Where that is not possible for other reasons, at least one document-specific
Consent resource should be held per completed document (consent, updated consent,
partial revocation, full revocation).*

#### Recommendations for gICS users regarding key-figure determination and the FDPG

The data integration centres provide the information required to determine
core-dataset-specific key figures for the DIZ dashboard.

> [TODO:REVIEW — Gate B/C. The German source page carries further detail on the
> gICS recommendations; this translation is a summary and must be checked against
> input/translations/de/pagecontent/implementer-guidance.md.]
{: .mii-highlight .mii-highlight-grey}
