# Startseite - MII Implementation Guide Consent v2026.0.0

* [**Inhaltsverzeichnis**](toc.md)
* **Startseite**

## Startseite

| | |
| :--- | :--- |
| *Offizielle URL*:https://www.medizininformatik-initiative.de/fhir/modul-consent/ImplementationGuide/mii-ig-consent | *Version*:2026.0.0 |
| Draft Stand: 2026-08-06 | *Maschinenlesbarer Name*:MII_IG_Consent |

### Einleitung

Die vorliegende Spezifikation beschreibt die FHIR-Repräsentation des Kerndatensatz-Moduls **Consent** der Medizininformatik-Initiative (MII). Im Folgenden werden die Use Cases des Moduls sowie die dazugehörigen FHIR-Profile und Terminologie-Ressourcen in ihrer verbindlichen Form beschrieben.

| | |
| :--- | :--- |
| Datum | 18.12.2025 |
| Version | 2026.0.0 (CalVer`JJJJ.n.n`) |
| Status | active |
| Realm | DE |

> **TODO:REVIEW (Gate A):** Datum und Status stammen aus der Veröffentlichungs­tabelle des migrierten Simplifier-Leitfadens (18.12.2025, `active`). Die `sushi-config.yaml` dieses Repositoriums trägt demgegenüber `date: 2026-08-06` (Migrationsdatum) und `status: draft` (aus der publizierten ImplementationGuide-Ressource). Die Abweichung wurde **nicht** stillschweigend vereinheitlicht — sie ist eine menschliche Entscheidung.

### Beschreibung Modul Consent

![](MII-KDS_de_Consent.jpg)

Das MII KDS Modul Consent ist ein Basismodul des Kerndatensatzes (KDS) der Medizininformatik-Initiative (MII). Es setzt auf den [publizierten Vorarbeiten der MII Taskforce Consent Umsetzung](https://bmcmedinformdecismak.biomedcentral.com/articles/10.1186/s12911-020-01138-6) auf.

Dabei orientiert sich das Modul Consent für die Abbildung des [MII Broad Consent](https://www.medizininformatik-initiative.de/de/mustertext-zur-patienteneinwilligung) an den **[FHIR-R4-Profilen](https://ig.fhir.de/einwilligungsmanagement/stable) der [AG Einwilligungsmanagement](https://wiki.hl7.de/index.php?title=Einwilligungsmanagement_(Projekt)) des [Interop-Forums](https://wiki.hl7.de/index.php?title=Hauptseite)** zur Repräsentation von Formulardaten (Questionnaire, QuestionnaireResponse) und Einwilligungen (Consent).

Fokus des Moduls Consent liegt auf der Umsetzung (Enforcement) der vom Patienten ausgefüllten Einwilligung auf Basis der Einwilligungs-Policies (konsolidiert mit der MII AG Consent im Dezember 2021).

### Zielgruppen

##### Implementierende

Datenintegrationszentren (DIZ), Softwareentwicklung und Systemarchitektur, die FHIR-basierte Lösungen bauen.
 → siehe [Profile und Extensions](profiles-and-extensions.md) und [Hinweise für Implementierende](implementer-guidance.md).

##### Forschende

Wissenschaftler:innen, die MII-Daten für die medizinische Forschung nutzen.
 → siehe [Hinweise für Forschende](researcher-guidance.md).

### Inhalt

* **[Anleitung](guidance.md)** — Einstieg und fachliche Hinweise.
* **[Konformität](conformance.md)** — verbindliche Anforderungen, Must-Support und der Umgang mit fehlenden Daten.
* **[Profile und Extensions](profiles-and-extensions.md)** und **[Terminologie](terminology.md)** — die technischen Artefakte.
* **[Suchparameter und Operationen](search-parameters-and-operations.md)** — die modul-eigenen Suchparameter.
* **[Beispiele](examples.md)** — Beispielinstanzen.

### Verwandte Leitfäden

* [Implementierungsleitfaden der AG Einwilligungsmanagement des Interop-Forums](https://ig.fhir.de/einwilligungsmanagement/stable/) — formale Abhängigkeit dieses Moduls (`de.einwilligungsmanagement` in `sushi-config.yaml`).
* [Kerndatensatzbeschreibung im ART-DECOR](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.184) — die fachliche Datensatzbeschreibung des Moduls.
* [MII Broad Consent (Mustertext zur Patienteneinwilligung)](https://www.medizininformatik-initiative.de/de/mustertext-zur-patienteneinwilligung).

Die inhaltliche Einordnung des Moduls und die Bezüge zu anderen Modulen sind auf der Seite [Hinweise für Implementierende](implementer-guidance.md) beschrieben; die vollständige Referenzliste steht dort im Abschnitt **Referenzen**.

Weitere FHIR-Implementierungsleitfäden finden Sie im offiziellen **[FHIR IG Registry](https://fhir.org/guides/registry/)** (Quelle: [`FHIR/ig-registry`](https://github.com/FHIR/ig-registry)).

### Impressum

Dieser Leitfaden ist im Rahmen der Medizininformatik-Initiative erstellt worden und unterliegt per Governance-Prozess dem Abstimmungsverfahren des Interoperabilitätsforums und der Technischen Komitees von HL7 Deutschland e. V.

### Autoren und Ansprechpartner

Inhaltlich verantwortlich für das hier dargestellte Modul ist die **MII Taskforce Consent Umsetzung**.

Das Modul Consent ist unter Mitarbeit von Martin Bialke, Sebastian Stäubert, Angela Merzweiler, Lars Geidel, Jörg Römhild, Raffael Bild, Fabian Prasser und Stefan Lang (HL7 Deutschland, technisches Komitee FHIR, Gefyra GmbH, Lang Health IT Consulting) entstanden.

Leitung des Moduls:

* Sebastian Stäubert
* Martin Bialke

Technische Umsetzung:

* Stefan Lang (technische Umsetzung FHIR-Profile und ImplementationGuides)
* Martin Bialke (Unterstützung ImplementationGuides)

Ansprechpartnerin bei der TMF:

* Karoline Buckow

Kommentare können (nach kostenloser Anmeldung) in GitHub als Issue erstellt oder formlos per E-Mail an [office@medizininformatik-initiative.de](mailto:office@medizininformatik-initiative.de) gesendet werden.

* GitHub (Originalmodul): [medizininformatik-initiative/kerndatensatzmodul-consent/issues](https://github.com/medizininformatik-initiative/kerndatensatzmodul-consent/issues)

Bei Fragen stehen wir Ihnen unter [office@medizininformatik-initiative.de](mailto:office@medizininformatik-initiative.de) gerne zur Verfügung.

### Urheberrecht und Lizenz

© 2019+ TMF e. V., Charlottenstraße 42, 10117 Berlin

![](https://licensebuttons.net/l/by/4.0/88x31.png)

Diese Arbeit ist lizenziert unter der [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).

Zu den Nutzungsrechten der zugrunde liegenden FHIR-Technologie siehe die FHIR-Basisspezifikation.

Einige verwendete Codesysteme werden von anderen Organisationen herausgegeben und gepflegt. Es gilt das Copyright der dort jeweils aufgeführten Herausgeber (Publisher).

### Disclaimer

Der Inhalt dieses Dokuments ist öffentlich. Zu beachten ist, dass Teile dieses Dokuments auf FHIR Version R4 beruhen, für die das Copyright von HL7 International gilt.

Obwohl diese Publikation mit größter Sorgfalt erstellt wurde, können die Autoren keinerlei Haftung für direkten oder indirekten Schaden übernehmen, der durch den Inhalt dieser Spezifikation entstehen könnte.

