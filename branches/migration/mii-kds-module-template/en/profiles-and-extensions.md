# Profiles and Extensions - MII Implementation Guide Consent v2026.0.1

* [**Table of Contents**](toc.md)
* **Profiles and Extensions**

## Profiles and Extensions

### FHIR profiles of this module

The core-dataset specifications build, where possible, on international standards and terminologies — in particular on the profiling work of the [AG Einwilligungsmanagement on consent management](https://ig.fhir.de/einwilligungsmanagement/stable/).

All core-dataset elements, adapted to the details and requirements of the Medical Informatics Initiative's use cases, are described below as FHIR StructureDefinitions.

The profile-specific description is on **the artifact page of the profile itself** (`input/intro-notes/`, spec 9), not here:

| | |
| :--- | :--- |
| MII_PR_Consent_Einwilligung | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung` |
| MII_PR_Consent_Provenance | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-provenance` |
| MII_PR_Consent_DocumentReference | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-documentreference` |

The module's search parameters are described on [Search Parameters and Operations](search-parameters-and-operations.md).

### Further relevant profiles

Besides Consent, Provenance and DocumentReference, further profiles of the AG Einwilligungsmanagement are relevant. The following profiles **must** be supported in order to use this guide:

> The table below is carried over **verbatim** from the German source page: its cells are terminology (codes and the displays the code system publishes), and translating a published display would falsify the terminology.

| | |
| :--- | :--- |
| FHIR-Profil | Zur Abbildung von / Verwendung für |

Where the Broad Consent is represented or queried by means of FHIR Questionnaires, the following profiles should be used in addition:

| — | — |

