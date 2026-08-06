<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE. Source: the Simplifier-rendered guide
  miiigmodulconsent, PUBLISHED version 2026.0.0 (Default, Read-only,
  Public, 2025-12-18), harvested 2026-08-06 by the mii-ig-migration
  skill (spec 5.1c discovery + 5.1d harvest). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile?version=2026.0.0
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/WeitererelevanteProfile?version=2026.0.0
  TODO:REVIEW at Gate B — mapped onto the template page set per spec 9.
-->

### FHIR-Profile dieses Moduls

Die Arbeiten der Kerndatensatzspezifikationen basieren, wo möglich, auf internationalen Standards und Terminologien. Insbesondere auf den Profilierungs-Vorarbeiten der [AG Einwilligungsmanagement zum FHIR Consent](https://ig.fhir.de/einwilligungsmanagement/stable/).

Alle Elemente des Kerndatensatzes, angepasst an die Details und Anforderungen für die Use Cases der Medizininformatik-Initative, werden nachfolgend in Form von FHIR StructureDefinitions beschrieben. Die Notwendigkeit der Anpassung der FHIR-Profile wird in textueller Form unterhalb der jeweiligen Profile erläutert.

Die profil-spezifische Beschreibung steht jeweils **auf der Artefaktseite des
Profils selbst** (siehe `input/intro-notes/`) und nicht hier:

| Profil | Canonical |
| --- | --- |
| MII\_PR\_Consent\_Einwilligung | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-einwilligung` |
| MII\_PR\_Consent\_Provenance | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-provenance` |
| MII\_PR\_Consent\_DocumentReference | `https://www.medizininformatik-initiative.de/fhir/modul-consent/StructureDefinition/mii-pr-consent-documentreference` |

Die Suchparameter des Moduls sind auf der Seite
[Suchparameter und Operationen](search-parameters-and-operations.html) beschrieben.

### Weitere relevante Profile

Neben [Consent](https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0), [Provenance](https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Provenance?version=2026.0.0) und [DocumentReference](https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/DocumentReference?version=2026.0.0) sind weitere Profile für den Umgang mit Einwilligungen und Einwilligungsvorlagen relevant, die unverändert aus dem [Implementierungsleitfaden Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Home.html) übernommen werden.

Die folgenden Profile sind dabei für die Nutzung dieses Leitfadens zwingend zu unterstützen:

| FHIR-Profil | Zur Abbildung von / Verwendung für |

| --- | --- |

| [Organization](https://ig.fhir.de/einwilligungsmanagement/stable/Organization.html) | Verantwortliche Einrichtung |

| [ResearchStudy](https://ig.fhir.de/einwilligungsmanagement/stable/ResearchStudy.html) | Forschungsprojekt |

| [Patient](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) | Betroffene Person (pseudonymisiert) |

Wird der Broad Consent mittels FHIR Questionnaires abgebildet bzw. abgefragt, sollten außerdem die folgenden Profile verwendet werden:

| FHIR-Profil | Zur Abbildung von / Verwendung für |

| --- | --- |

| [QuestionnaireResponse](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireResponse.html) | Ausgefüllte Einwilligung |

| [QuestionnaireComposed](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireComposed.html) | Einwilligungsvorlage (render-fähig) |

| [TemplateFrame](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateFrame.html) | Einwilligungsvorlage (Strukturdefinition) |

| [TemplateModule](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateModule.html) | Einwilligungsmodul |
