<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE. Source: the Simplifier-rendered guide
  miiigmodulconsent, PUBLISHED version 2026.0.0 (Default, Read-only,
  Public, 2025-12-18), harvested 2026-08-06 by the mii-ig-migration
  skill (spec 5.1c discovery + 5.1d harvest). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/UML?version=2026.0.0
  TODO:REVIEW at Gate B — mapped onto the template page set per spec 9.
-->

### UML-Klassendiagramm

### [Consent](https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0)

Die Consent-Resource stellt eine rein maschinen-lesbare Repräsentation der real existierenden Einwilligung einer Person dar und wird für das Enforcement (Durchsetzung, Umsetzung) der Consent-Policies verwendet.

Die Einwilligung wird in einem konkreten Kontext (z.B. MII) erhoben, was in FHIR in Form einer Referenz auf die verantwortliche Organisation ([Organization](https://ig.fhir.de/einwilligungsmanagement/stable/Organization.html)) und/oder zu einem Forschungsprojekt ([ResearchStudy](https://ig.fhir.de/einwilligungsmanagement/stable/ResearchStudy.html)) modelliert wird.

### [Provenance](https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Provenance?version=2026.0.0)

Die Provenance-Resource beschreibt die Herkunft der Einwilligungsinhalte (u.a. Unterschriften) und verknüpft diese mit den beteiligten Personen ([Patient](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html), Consent Witness) und eventuell vorhandenen Dokumenten-Scans ([DocumentReference](https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/DocumentReference?version=2026.0.0)). Ebenso können die für die Erhebung genutzten Anwendungssysteme genannt (display) bzw. referenziert werden, sowie im Anwendungssystem geltende Patienten-Identifier.

### Abbildung von [Fragebögen](https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/Fragebgen?version=2026.0.0)

Der Einsatz *aller* in AG Einwilligungsmanagement entwickelten Profile ist *nicht verpflichtend*. Für die Abbildung der Questionnaire-basierten Inhalte ([Fragebögen](https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/AnwendungsflleInformationsmodell/Fragebgen?version=2026.0.0)) sind die Empfehlungen der TFCU zu berücksichtigen.

### Relevante Profile

Hinweise zum UML-Klassendiagramm des Erweiterungsmoduls Consent:

- *Blau* eingefärbte Klassen werden bei der Abbildung und Profilierung in FHIR berücksichtigt, sind in diesem IG profiliert und bei der MII Umsetzung erforderlich.

- *Orange* eingefärbte Klassen sind im IG der AG Einwilligungsmanagement profiliert und erforderlich für die MII Umsetzung.

- *Grau* eingefärbte Klassen sind im IG der AG Einwilligungsmanagement profiliert und optional für die MII Umsetzung.

- *Hellgrau* eingefärbte Klassen werden referenziert. Diese werden jedoch nicht bei der Abbildung und Profilierung in FHIR berücksichtigt.

Die in den Klassen des Diagramms hinterlegten Attribute sind verpflichtend. Darüber hinaus können weitere optionale Attribute angegeben werden.

![](https://github.com/medizininformatik-initiative/kerndatensatzmodul-consent/blob/master/figures/information-model_UML-Diagramm_MII-spez.png?raw=true)
