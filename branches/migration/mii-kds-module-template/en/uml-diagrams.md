# UML Diagrams - MII Implementation Guide Consent v2026.0.1

* [**Table of Contents**](toc.md)
* [**Guidance**](guidance.md)
* **UML Diagrams**

## UML Diagrams

### UML class diagram

#### Consent

The Consent resource is a purely machine-readable representation of a person's actual consent, and is used to enforce the consent content.

Consent is obtained in a concrete context (for example the MII), which is expressed in FHIR as a reference to the responsible organization ([Organization](https://ig.fhir.de/einwilligungsmanagement/stable/Organization.html)) and, where applicable, the research project ([ResearchStudy](https://ig.fhir.de/einwilligungsmanagement/stable/ResearchStudy.html)).

#### Provenance

The Provenance resource describes the origin of the consent content (signatures among other things) and links it to the persons involved ([Patient](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html)).

#### Representing questionnaires

Using **all** of the profiles developed by the AG Einwilligungsmanagement is **not mandatory**. For representing the Questionnaire-based content, see [Datasets and Descriptions](datasets-and-descriptions.md).

#### Relevant profiles

Notes on the UML class diagram of the Consent extension module:

* Classes coloured **blue** are considered in the FHIR representation and profiling, are profiled in this IG, and are required for the MII implementation.
* Classes coloured **orange** are profiled in the IG of the AG Einwilligungsmanagement and are required for the MII implementation.
* Classes coloured **grey** are profiled in the IG of the AG Einwilligungsmanagement and are optional for the MII implementation.
* Classes coloured **light grey** are referenced, but are not considered in the FHIR representation and profiling.

The attributes shown in the diagram's classes are mandatory. Further optional attributes may be supplied in addition.

![](https://github.com/medizininformatik-initiative/kerndatensatzmodul-consent/blob/master/figures/information-model_UML-Diagramm_MII-spez.png?raw=true)

