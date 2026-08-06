<!-- markdownlint-disable MD041 -->
<!--
  PROFILE UND EXTENSIONS — DEUTSCHE FASSUNG (Quelltext, massgeblich).
  Herkunft (Migration 2026-08-06, spec 5.1c):
    - .../TechnischeImplementierung/FHIRProfile?version=2026.0.0 (Einleitung)
    - .../TechnischeImplementierung/FHIRProfile/WeitererelevanteProfile?version=2026.0.0
  Das Narrativ JE PROFIL steht nicht hier, sondern in input/intro-notes/ bzw.
  input/translations/de/intro-notes/ und wird oben auf der jeweiligen
  Artefaktseite gerendert (spec 9: bei mehr als zwei Profilen). Die
  Elementbaeume der Simplifier-Seiten wurden NICHT uebernommen: der IG Publisher
  erzeugt sie aus den StructureDefinitions selbst (Direktiven-Crosswalk).
-->

### Profile und Extensions

Die Arbeiten der Kerndatensatzspezifikationen basieren, wo möglich, auf
internationalen Standards und Terminologien, insbesondere auf den
Profilierungs-Vorarbeiten der
[AG Einwilligungsmanagement zum FHIR Consent](https://ig.fhir.de/einwilligungsmanagement/stable/).

Alle Elemente des Kerndatensatzes, angepasst an die Details und Anforderungen für
die Use Cases der Medizininformatik-Initiative, werden in Form von FHIR
StructureDefinitions beschrieben. Die Notwendigkeit der Anpassung der
FHIR-Profile wird in textueller Form auf der jeweiligen Profilseite erläutert.

#### Verpflichtende / must-support Elemente

Für **verpflichtende** oder als **must-support** markierte Elemente sei an dieser
Stelle auf die entsprechenden
[Regeln der IPS](https://build.fhir.org/ig/HL7/fhir-ips/design.html#must-support)
verwiesen, die auch für diesen ImplementationGuide gelten. Siehe auch
[Must-Support](must-support.html).

#### Profile dieses Moduls

| Profil | Zur Abbildung von |
| --- | --- |
| [MII\_PR\_Consent\_Einwilligung](StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.html) | Die operationalisierte, maschinenlesbare Einwilligung |
| [MII\_PR\_Consent\_Provenance](StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.html) | Herkunft der Einwilligungsinhalte, u. a. Unterschriften |
| [MII\_PR\_Consent\_DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.html) | Scan des Einwilligungsdokuments (PDF) |

Die ausführliche Erläuterung je Profil — Datenschutz-Aspekte,
Interoperabilität, die Unterschiede zum Basis-Profil, die verschachtelten
Provision-Elemente und die Policy-OIDs — steht **auf der jeweiligen
Profilseite**; die Seite selbst zeigt darunter den vom IG Publisher erzeugten
Elementbaum, die Differenz zum Basis-Profil sowie XML- und JSON-Serialisierung.

Dieses Modul definiert **keine eigenen Extensions**. Die verwendete Extension
`DomainReference` stammt aus dem
[Implementierungsleitfaden Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/).

#### Weitere relevante Profile

Neben
[Consent](StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.html),
[Provenance](StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.html) und
[DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.html)
sind weitere Profile für den Umgang mit Einwilligungen und
Einwilligungsvorlagen relevant, die unverändert aus dem
[Implementierungsleitfaden Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Home.html)
übernommen werden.

Die folgenden Profile sind dabei für die Nutzung dieses Leitfadens zwingend zu
unterstützen:

| FHIR-Profil | Zur Abbildung von / Verwendung für |
| --- | --- |
| [Organization](https://ig.fhir.de/einwilligungsmanagement/stable/Organization.html) | Verantwortliche Einrichtung |
| [ResearchStudy](https://ig.fhir.de/einwilligungsmanagement/stable/ResearchStudy.html) | Forschungsprojekt |
| [Patient](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html) | Betroffene Person (pseudonymisiert) |

Wird der Broad Consent mittels FHIR Questionnaires abgebildet bzw. abgefragt,
sollten außerdem die folgenden Profile verwendet werden:

| FHIR-Profil | Zur Abbildung von / Verwendung für |
| --- | --- |
| [QuestionnaireResponse](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireResponse.html) | Ausgefüllte Einwilligung |
| [QuestionnaireComposed](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireComposed.html) | Einwilligungsvorlage (render-fähig) |
| [TemplateFrame](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateFrame.html) | Einwilligungsvorlage (Strukturdefinition) |
| [TemplateModule](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateModule.html) | Einwilligungsmodul |

#### Siehe auch

- [Suchparameter und Operationen](search-parameters-and-operations.html) — die
  modul-eigenen Suchparameter der Consent-Ressource.
- [Terminologie](terminology.html) — die ValueSets und CodeSysteme des Moduls.
- [Beispiele](examples.html) — die Beispielinstanzen zu den drei Profilen.
