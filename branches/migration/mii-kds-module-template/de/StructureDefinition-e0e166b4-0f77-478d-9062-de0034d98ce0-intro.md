<!--
  MII_PR_Consent_Einwilligung — Einleitung, DEUTSCHE FASSUNG (Quelltext, massgeblich).
  Herkunft (Migration 2026-08-06, spec 5.1c):
    .../TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0
  Der Elementbaum der Simplifier-Seite wurde nicht uebernommen: der IG Publisher
  erzeugt ihn unterhalb dieses Textes aus der StructureDefinition selbst.
-->

Dieses Profil beschreibt eine operationalisierte, automatisch erzeugte und
prozessierbare Einwilligung in der Medizininformatik-Initiative.

Beim Einschluss einer Person in eine Studie (auch in einen MII-Use-Case) wird eine
Einwilligung für diese Person auf Basis der
[MII Broad Consent Mustertexte](https://www.medizininformatik-initiative.de/de/mustertext-zur-patienteneinwilligung)
erhoben und das entsprechende Einwilligungsdokument am jeweiligen Standort
strukturiert dokumentiert, gemäß den
[Vorgaben der MII Task Force Consent Umsetzung](https://art-decor.org/art-decor/decor-datasets--mide-?id=2.16.840.1.113883.3.1937.777.24.1.1&effectiveDate=2018-06-05T12%3A44%3A12&conceptId=2.16.840.1.113883.3.1937.777.24.2.184&conceptEffectiveDate=2018-06-29T16%3A26%3A50&language=de-DE).

Auf Grundlage dieser Einwilligungsdokumente wird die FHIR-Consent-Ressource
automatisiert erzeugt. Der
[Projektkontext](https://ig.fhir.de/einwilligungsmanagement/stable/DomainReference.html)
bleibt erhalten.

Die Erstellung der Ressource muss vor der Teilnahme an standortübergreifenden
Feasibility-Anfragen und Datenherausgaben erfolgen. Weitere Pflichten und
Anpassungen sind für jeden Use Case zu prüfen.

**Datenschutz-Aspekte** dieses Profils — pseudonymer Personenbezug, Umgang mit
personenidentifizierenden Informationen, keine Dokumenten-Scans in der
Consent-Ressource — stehen unter
[Sicherheit und Datenschutz](security-and-privacy.html).

### Interoperabilität

Um die Austauschbarkeit der operationalisierten Einwilligungsinhalte auch über
FHIR hinaus sicherzustellen, wurde mit der **MII AG Consent** ein einheitliches
Policy-ValueSet zur **semantischen Abbildung** der im MII Broad Consent
enthaltenen Aussagen im Dezember 2021 abgestimmt und im
[ART-DECOR](http://art-decor.org/decor/services/RetrieveValueSet?id=2.16.840.1.113883.3.1937.777.24.11.36&effectiveDate=2021-04-23T10:55:54&prefix=mide-&format=html&collapsable=true&language=de-DE&ui=en-US)
(Policy-OIDs) dokumentiert.

*Die Verwendung dieses Codesystems ist bezogen auf das KDS-Modul Consent
verpflichtend.*
