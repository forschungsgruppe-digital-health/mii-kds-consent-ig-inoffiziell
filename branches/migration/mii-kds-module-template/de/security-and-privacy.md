# Sicherheit und Datenschutz - MII Implementation Guide Consent v2026.0.1

* [**Inhaltsverzeichnis**](toc.md)
* [**Konformität**](conformance.md)
* **Sicherheit und Datenschutz**

## Sicherheit und Datenschutz

 Diese Seite enthält Übersetzungen aus der Originalsprache, in der der Leitfaden verfasst wurde. Informationen zu diesen Übersetzungen und Anweisungen zum Abgeben von Feedback zu den Übersetzungen finden Sie [hier](translationinfo.md). 

### Datenschutz

Da auch die FHIR Consent Ressource **keine personenidentifizierende Informationen** der einwilligenden Person enthält, sollte der [**pseudonyme Personenbezug**](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) über entsprechende [**pseudonyme Identifier**](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifier.html) hergestellt werden. Etwaige personenidentifizierende Informationen (z.B. Geburtsdatum, Geschlecht,Anschrift) sowie Referenzen, z.B. auf (Klartext-) Patienten-Profile, sollten vor Ausleitung geeignet ersetzt werden.

**Technisch gesehen können Patienten-Ressourcen und abgeleitete Profile, wie z.B. die Profile der [AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) oder der [MII](https://simplifier.net/medizininformatikinitiative-modulperson/sdmiipersonpatientpseudonymisiert) verwendet werden.** Um Pseudonyme, Fallnummern, etc. unterscheiden zu können, ist es unabhängig davon erforderlich eine Kategorisierung des verwendeten Identifiers mittels [patient.identifier.type](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifierType.html) vorzunehmen.

Die FHIR Consent Ressource enthält **keine Dokumenten-Scans und/oder Unterschriften**. Ist eine Übermittlung je nach Anwendungsfall erforderlich, sind separate Ressourcen gemäß den [Vorgaben der AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/DocumentReference.html) zu erstellen (Consent Bundles).

