<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE. Source: the Simplifier-rendered guide
  miiigmodulconsent, PUBLISHED version 2026.0.0 (Default, Read-only,
  Public, 2025-12-18), harvested 2026-08-06 by the mii-ig-migration
  skill (spec 5.1c discovery + 5.1d harvest). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung?version=2026.0.0
  TODO:REVIEW at Gate B — mapped onto the template page set per spec 9.
-->

### Technische Implementierung

Dieser Abschnitt beschreibt die syntaktischen und semantischen Vorgaben zur Implementierung des Consent-Moduls.

Weiterhin sind auch Suchparameter definiert, die bei Verwendung der FHIR RESTful API durch die jeweiligen Systeme implementiert werden müssen. Grundsätzlich werden logische AND- und OR-Verknüpfungen der FHIR-Search unterstützt, vgl. [http://www.hl7.org/fhir/search.html](http://www.hl7.org/fhir/search.html) .

Grundlagen und weitere Details zur Suche und zur FHIR RESTful API werden zum Zeitpunkt der Erstellung dieses Implementierungsleitfadens im Rahmen der Basismodule erarbeitet und können zu einem späteren Zeitpunkt die hier gemachten Vorgaben ergänzen. Ggf. wird dann auch eine neue Version dieses Leitfadens veröffentlicht.

### Konformitätsseiten dieses Leitfadens

- **[Grundlegende Anforderungen](general-requirements.html)** — Anwendungsfälle und Szenarien.
- **[Must Support](must-support.html)** — Umgang mit verpflichtenden und Must-Support-Elementen.
- **[Umgang mit fehlenden Daten](missing-data.html)**.
- **[Sicherheit und Datenschutz](security-and-privacy.html)** — Datenschutz-Aspekte der Consent-Ressource.
