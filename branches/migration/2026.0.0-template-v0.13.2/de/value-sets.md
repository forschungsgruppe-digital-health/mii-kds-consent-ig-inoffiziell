# ValueSets - MII Implementation Guide Consent v2026.0.0

* [**Table of Contents**](toc.md)
* **ValueSets**

## ValueSets

> **Optionale Seite (0..1).** Das KDS-Modulmenü führt diese Seite als **optional**. Entscheiden Sie für Ihr Modul: Seite **behalten** — Inhalte ausfüllen und dieses Banner samt `OPTIONAL-PAGE`-Marker-Kommentar löschen (in dieser Datei UND in der englischen Quellseite) — oder Seite **entfernen**, nach der Schritt-für-Schritt-Anleitung in [`docs/optional-pages.md`](https://github.com/forschungsgruppe-digital-health/mii-kds-consent-ig-inoffiziell/blob/main/docs/optional-pages.md) dieses Repositories. Ein Release darf dieses Banner nicht enthalten (Konventions-Check M9).

### ValueSets

Diese Seite beschreibt die ValueSets des Moduls **Consent** (Namenskonvention `MII_VS_<Modul>_<Name>`). Allgemeine Hinweise zur Verwendung von Codes: siehe [FHIR Terminology](http://hl7.org/fhir/R4/terminologies.html); die zugrunde liegenden CodeSystems beschreibt die Seite [CodeSystems](code-systems.md).

**Expansionen:** ValueSet-Expansionen dieses Leitfadens werden über einen FHIR-Terminologieserver erzeugt — über SU-TermServ, sofern das Client-Zertifikat konfiguriert ist, sonst über den öffentlichen HL7-Server `tx.fhir.org` (dann expandieren einige KDS-spezifische ValueSets ggf. nicht vollständig).

> [TODO: Falls Ihr Modul SNOMED CT nutzt, geben Sie die verwendete Edition/Version an. Listen Sie die modul-eigenen ValueSets auf oder verweisen Sie auf die automatisch erzeugte Artefakt-Liste — oder entfernen Sie diese Seite, wenn Ihr Modul keine definiert.]

