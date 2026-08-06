# Sicherheit und Datenschutz - MII Implementation Guide Consent v2026.0.0

* [**Inhaltsverzeichnis**](toc.md)
* [**Konformität**](conformance.md)
* **Sicherheit und Datenschutz**

## Sicherheit und Datenschutz

 Diese Seite enthält Übersetzungen aus der Originalsprache, in der der Leitfaden verfasst wurde. Informationen zu diesen Übersetzungen und Anweisungen zum Abgeben von Feedback zu den Übersetzungen finden Sie [hier](translationinfo.md). 

### Sicherheit und Datenschutz

Dieser Abschnitt richtet sich an Sicherheits- und Datenschutz-Fachleute. Er beschreibt, welche Angriffe und Risiken für das Modul **Consent** betrachtet wurden und welche Gegenmaßnahmen vorgesehen sind.

Grundlagen und allgemeine Anforderungen stehen in der FHIR-Kernspezifikation: [Security & Privacy Module](https://build.fhir.org/secpriv-module.html) und die [Security-Checkliste](https://build.fhir.org/security.html). Dieser Abschnitt wiederholt sie nicht, sondern nennt nur die **modul-spezifischen** Aspekte.

#### Datenschutzgrundsätze

Für die Verarbeitung personenbezogener Daten gelten Transparenz, Zweckbindung, Datenminimierung, Richtigkeit, Speicherbegrenzung und Integrität/Vertraulichkeit (DSGVO Art. 5). Im MII-Kontext erfolgt die Nutzung auf Basis der MII-Broad-Consent-Regelungen.

##### Datenschutz-Aspekte der Consent-Ressource

**Aus dem Quell-Leitfaden migriert (Stand 2026.0.0, geerntet am 2026-08-06): `.../TechnischeImplementierung/FHIRProfile/Consent`, Abschnitt „Datenschutz-Aspekte“. Verweis von der Profilseite: [MII_PR_Consent_Einwilligung](StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.md).**

Da auch die FHIR-Consent-Ressource **keine personenidentifizierenden Informationen** der einwilligenden Person enthält, sollte der [**pseudonyme Personenbezug**](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) über entsprechende [**pseudonyme Identifier**](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifier.html) hergestellt werden. Etwaige personenidentifizierende Informationen (z. B. Geburtsdatum, Geschlecht, Anschrift) sowie Referenzen, z. B. auf (Klartext-)Patienten-Profile, sollten vor Ausleitung geeignet ersetzt werden.

**Technisch gesehen können Patienten-Ressourcen und abgeleitete Profile verwendet werden, wie z. B. die Profile der [AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) oder der [MII](https://simplifier.net/medizininformatikinitiative-modulperson/sdmiipersonpatientpseudonymisiert).** Um Pseudonyme, Fallnummern usw. unterscheiden zu können, ist es unabhängig davon erforderlich, eine Kategorisierung des verwendeten Identifiers mittels [`Patient.identifier.type`](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifierType.html) vorzunehmen.

Die FHIR-Consent-Ressource enthält **keine Dokumenten-Scans und/oder Unterschriften**. Ist eine Übermittlung je nach Anwendungsfall erforderlich, sind separate Ressourcen gemäß den [Vorgaben der AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/DocumentReference.html) zu erstellen (Consent-Bundles) — in diesem Modul die Profile [Provenance](StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.md) und [DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.md).

#### Sicherheitsbetrachtung

Sicherheit ist Risikomanagement bezüglich Vertraulichkeit, Integrität und Verfügbarkeit.

##### TODO:REVIEW (Gate B) — im Quell-Leitfaden nicht enthalten

Der migrierte Quell-Leitfaden führt keine Angriffs- oder Risikobetrachtung. Es wurde nichts erfunden; die Lücke ist im Migrationsbericht vermerkt. Was die Quelle zum Datenschutz sagt, steht vollständig im Abschnitt oben.

#### Modul-spezifische Konformitätsanforderungen

##### TODO:REVIEW (Gate B) — im Quell-Leitfaden nicht enthalten

Der Quell-Leitfaden formuliert keine als solche gekennzeichneten Sicherheits- oder Datenschutz-Konformitätsaussagen. Die Pseudonymisierungs-Empfehlungen oben sind als Empfehlungen formuliert, nicht als SHALL/SHOULD/MAY; sie wurden nicht in Konformitätsaussagen umformuliert.

#### Verbleibende Risiken

##### TODO:REVIEW (Gate B) — im Quell-Leitfaden nicht enthalten

Der Quell-Leitfaden benennt keine verbleibenden Risiken. Nicht ergänzt.

