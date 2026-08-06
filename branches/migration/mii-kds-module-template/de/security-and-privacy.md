# Sicherheit und Datenschutz - MII Implementation Guide Consent v2026.0.0

* [**Inhaltsverzeichnis**](toc.md)
* [**Konformität**](conformance.md)
* **Sicherheit und Datenschutz**

## Sicherheit und Datenschutz

 Diese Seite enthält Übersetzungen aus der Originalsprache, in der der Leitfaden verfasst wurde. Informationen zu diesen Übersetzungen und Anweisungen zum Abgeben von Feedback zu den Übersetzungen finden Sie [hier](translationinfo.md). 

##### TODO:REVIEW (Gate B) — Startseiten-Vorlage, Narrativ noch nicht migriert

Dies ist die **Vorlagenseite des MII-KDS-Modul-Templates**, unveraendert uebernommen. Es ist **nicht** das Narrativ des MII-KDS-Moduls Consent.

Der Leitfadentext des Moduls existiert nur als gerenderter Simplifier-Guide (`simplifier.net/guide/miiigmodulconsent`) und liegt **nicht im Quell-Repository**. Es gab daher nichts, was in diese Seite haette migriert werden koennen, und es wurde nichts erfunden. Seitenstruktur, Menue und Artefakt-Rendering sind echt; der Fliesstext ist ein Platzhalter, bis das Narrativ von Simplifier migriert ist.

### Sicherheit und Datenschutz

Dieser Abschnitt richtet sich an Sicherheits- und Datenschutz-Fachleute. Er beschreibt, welche Angriffe und Risiken für das Modul **Consent** betrachtet wurden und welche Gegenmaßnahmen vorgesehen sind.

Grundlagen und allgemeine Anforderungen stehen in der FHIR-Kernspezifikation: [Security & Privacy Module](https://build.fhir.org/secpriv-module.html) und die [Security-Checkliste](https://build.fhir.org/security.html). Dieser Abschnitt wiederholt sie nicht, sondern nennt nur die **modul-spezifischen** Aspekte.

#### Datenschutzgrundsätze

Für die Verarbeitung personenbezogener Daten gelten Transparenz, Zweckbindung, Datenminimierung, Richtigkeit, Speicherbegrenzung und Integrität/Vertraulichkeit (DSGVO Art. 5). Im MII-Kontext erfolgt die Nutzung auf Basis der MII-Broad-Consent-Regelungen.

> [TODO: Beschreiben Sie, welche Datenkategorien Ihr Modul führt und welche Zweckbindung bzw. Rechtsgrundlage im MII-Kontext gilt.]

#### Sicherheitsbetrachtung

Sicherheit ist Risikomanagement bezüglich Vertraulichkeit, Integrität und Verfügbarkeit.

> [TODO: Nennen Sie die betrachteten Angriffe/Risiken und die Gegenmaßnahmen — z. B. Zugriffsschutz der FHIR-API, Pseudonymisierung, Transportverschlüsselung, Protokollierung.]

#### Modul-spezifische Konformitätsanforderungen

> [TODO: Falls Ihr Modul sicherheits- oder datenschutzbezogene SHALL/SHOULD/MAY-Anforderungen definiert, führen Sie sie hier auf und benennen Sie, welchem Risiko sie begegnen.]

#### Verbleibende Risiken

> [TODO: Nennen Sie Risiken, die NICHT durch diese Spezifikation adressiert werden und daher im Systemdesign, im Betrieb oder per Policy behandelt werden müssen.]

