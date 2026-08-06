<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE. Source: the Simplifier-rendered guide
  miiigmodulconsent, PUBLISHED version 2026.0.0 (Default, Read-only,
  Public, 2025-12-18), harvested 2026-08-06 by the mii-ig-migration
  skill (spec 5.1c discovery + 5.1d harvest). Source pages:
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung/FHIRProfile/Consent?version=2026.0.0
  TODO:REVIEW at Gate B — mapped onto the template page set per spec 9.
-->

### Datenschutz

Da auch die FHIR Consent Ressource **keine personenidentifizierende Informationen** der einwilligenden Person enthält, sollte der [**pseudonyme Personenbezug**](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) über entsprechende [**pseudonyme Identifier**](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifier.html) hergestellt werden. Etwaige personenidentifizierende Informationen (z.B. Geburtsdatum, Geschlecht,Anschrift) sowie Referenzen, z.B. auf (Klartext-) Patienten-Profile, sollten vor Ausleitung geeignet ersetzt werden.

*Technisch gesehen können Patienten-Ressourcen und abgeleitete Profile, wie z.B. die Profile der [AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) oder der [MII](https://simplifier.net/medizininformatikinitiative-modulperson/sdmiipersonpatientpseudonymisiert) verwendet werden.* Um Pseudonyme, Fallnummern, etc. unterscheiden zu können, ist es unabhängig davon erforderlich eine Kategorisierung des verwendeten Identifiers mittels [patient.identifier.type](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifierType.html) vorzunehmen.

Die FHIR Consent Ressource enthält **keine Dokumenten-Scans und/oder Unterschriften**. Ist eine Übermittlung je nach Anwendungsfall erforderlich, sind separate Ressourcen gemäß den [Vorgaben der AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/DocumentReference.html) zu erstellen (Consent Bundles).
