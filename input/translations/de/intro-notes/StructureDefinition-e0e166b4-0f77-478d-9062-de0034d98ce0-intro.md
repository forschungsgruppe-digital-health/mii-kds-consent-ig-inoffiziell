<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE. Source: the Simplifier-rendered guide
  miiigmodulconsent, PUBLISHED version 2026.0.0 (Default, Read-only,
  Public, 2025-12-18), harvested 2026-08-06 by the mii-ig-migration
  skill (spec 5.1c discovery + 5.1d harvest). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0
  TODO:REVIEW at Gate B — mapped onto the template page set per spec 9.
-->

Dieses Profil beschreibt eine operationalisierte, automatisch erzeugte und prozessierbare Einwilligung in der Medizininformatik-Initiative.

Beim Einschluss einer Person in eine Studie (auch in einen MII-Use Case) wird eine Einwilligung für diese Person auf Basis der [MII Broad Consent Mustertexte](https://www.medizininformatik-initiative.de/de/mustertext-zur-patienteneinwilligung) erhoben und entsprechende Einwilligungsdokument am jeweiligen Standort strukturiert dokumentiert gemäß den [Vorgaben der MII Task Force Consent Umsetzung](https://art-decor.org/art-decor/decor-datasets--mide-?id=2.16.840.1.113883.3.1937.777.24.1.1&effectiveDate=2018-06-05T12%3A44%3A12&conceptId=2.16.840.1.113883.3.1937.777.24.2.184&conceptEffectiveDate=2018-06-29T16%3A26%3A50&language=de-DE).

Auf Grundlage dieser Einwilligungsdokumente wird die FHIR Consent Ressource automatisiert erzeugt. Der [Projektkontext](https://ig.fhir.de/einwilligungsmanagement/stable/DomainReference.html) bleibt erhalten.

Die Erstellung der Ressource muss vor der Teilnahme an Standort-übergreifenden Feasability-Anfragen und Datenherausgaben erfolgen. Weitere Pflichten und Anpassungen sind für jeden Use Case zu prüfen.

### Interoperabilität

Um die Austauschbarkeit der operationalisierten Einwilligungsinhalte auch über FHIR hinaus sicherzustellen, wurde mit der **MII AG Consent** ein einheitliches PolicyValueSet zur **semantischen Abbildung** der im MII Broad Consent enthaltenen Aussagen im Dezember 2021 abgestimmt und im [ART-DECOR](http://art-decor.org/decor/services/RetrieveValueSet?id=2.16.840.1.113883.3.1937.777.24.11.36&effectiveDate=2021-04-23T10:55:54&prefix=mide-&format=html&collapsable=true&language=de-DE&ui=en-US) (Policy-OIDs) dokumentiert.

*Die Verwendung dieses Codesystems ist bezogen auf das KDS-Modul Consent verpflichtend.*
