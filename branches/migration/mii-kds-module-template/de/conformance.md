# Konformität - MII Implementation Guide Consent v2026.0.0

* [**Inhaltsverzeichnis**](toc.md)
* **Konformität**

## Konformität

 Diese Seite enthält Übersetzungen aus der Originalsprache, in der der Leitfaden verfasst wurde. Informationen zu diesen Übersetzungen und Anweisungen zum Abgeben von Feedback zu den Übersetzungen finden Sie [hier](translationinfo.md). 

### Konformität

Dieser Abschnitt definiert die Konformitätsanforderungen für Systeme, die die Profile des Moduls **Consent** umsetzen.

* **[Allgemeine Anforderungen](general-requirements.md)** — die Konformitäts-Verben (MUSS/SOLLTE/KANN nach RFC-2119), das Beanspruchen von Konformität, die Verwendung von Codes in den Profilen und die Erwartungen an die FHIR-RESTful-API.
* **[Must-Support](must-support.md)** — was **Must Support** für daten-erzeugende und daten-verarbeitende Systeme bedeutet.
* **[Umgang mit fehlenden Daten](missing-data.md)** — wie fehlende oder unbekannte Werte kodiert werden.
* **[Sicherheit und Datenschutz](security-and-privacy.md)** — die Sicherheits- und Datenschutzbetrachtungen dieses Moduls.

Maßgeblich für die MII-weiten Konformitätsregeln ist die Seite [Conformance](https://github.com/medizininformatik-initiative/kerndatensatz-meta/wiki/Conformance) des MII-Meta-Wikis. Allgemeine Anforderungen, Must-Support und Umgang mit fehlenden Daten geben sie für dieses Modul wieder; bei Abweichungen gilt das Wiki. Sicherheit und Datenschutz ist eine zusätzliche Seite dieses Leitfadens gemäß den HL7-IG-Best-Practices.

#### Technische Implementierung

**Aus dem Quell-Leitfaden migriert (Stand 2026.0.0, geerntet am 2026-08-06): `.../TechnischeImplementierung`. Dieser Abschnitt ist der maßgebliche Text; die englische Seite ist seine Übersetzung.**

Dieser Abschnitt beschreibt die syntaktischen und semantischen Vorgaben zur Implementierung des Consent-Moduls.

Weiterhin sind auch Suchparameter definiert, die bei Verwendung der FHIR RESTful API durch die jeweiligen Systeme implementiert werden müssen. Grundsätzlich werden logische AND- und OR-Verknüpfungen der FHIR-Search unterstützt, vgl. [hl7.org/fhir/search.html](http://www.hl7.org/fhir/search.html). Die modul-eigenen Suchparameter sind unter [Suchparameter und Operationen](search-parameters-and-operations.md) beschrieben.

Grundlagen und weitere Details zur Suche und zur FHIR RESTful API werden zum Zeitpunkt der Erstellung dieses Implementierungsleitfadens im Rahmen der Basismodule erarbeitet und können zu einem späteren Zeitpunkt die hier gemachten Vorgaben ergänzen. Ggf. wird dann auch eine neue Version dieses Leitfadens veröffentlicht.

Hinweise zur Umsetzung stehen im Abschnitt [Anleitung](guidance.md), die technischen Artefakte im Abschnitt [Artefakte](artifacts.md).

##### TODO:REVIEW (Gate B) — es wurden keine Konformitätsaussagen markiert

Der migrierte Quell-Leitfaden formuliert seine Vorgaben als Fließtext und als Must-support-/not-supported-Angaben in den Elementtabellen; er markiert keinen Satz als Konformitätsaussage. **Kein Satz der Migration wurde zu einer gemacht** — migrierten Fließtext in Konformitätsmarker zu fassen würde seine Verbindlichkeit ändern; das ist eine Entscheidung der Modulverantwortlichen, nicht der Migration.

-------

**Hinweis:** Eine Liste der Konformitätsaussagen ist in der englischen Fassung dieses Implementierungsleitfadens verfügbar. Die Aussagen sind ausschließlich auf den englischen Originalseiten markiert und werden nur dort erzeugt.

