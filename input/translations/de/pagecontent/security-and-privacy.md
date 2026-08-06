<!-- markdownlint-disable MD041 -->
<!-- Sicherheit & Datenschutz. Diese Seite ist von den HL7-Best-Practices für
     Implementation Guides ausdrücklich gefordert ("Security and Privacy
     Considerations"). Sie richtet sich an Sicherheits- und
     Datenschutz-Fachleute. Ersetzen Sie die [TODO]-Hinweise durch die Aussagen
     Ihres Moduls; entfernen Sie die Seite NICHT. -->

### Sicherheit und Datenschutz

Dieser Abschnitt richtet sich an Sicherheits- und Datenschutz-Fachleute. Er
beschreibt, welche Angriffe und Risiken für das Modul **Consent**
betrachtet wurden und welche Gegenmaßnahmen vorgesehen sind.

Grundlagen und allgemeine Anforderungen stehen in der FHIR-Kernspezifikation:
[Security & Privacy Module](https://build.fhir.org/secpriv-module.html) und die
[Security-Checkliste](https://build.fhir.org/security.html). Dieser Abschnitt
wiederholt sie nicht, sondern nennt nur die **modul-spezifischen** Aspekte.

#### Datenschutzgrundsätze

Für die Verarbeitung personenbezogener Daten gelten Transparenz, Zweckbindung,
Datenminimierung, Richtigkeit, Speicherbegrenzung und Integrität/Vertraulichkeit
(DSGVO Art. 5). Im MII-Kontext erfolgt die Nutzung auf Basis der
MII-Broad-Consent-Regelungen.

##### Datenschutz-Aspekte der Consent-Ressource

*Aus dem Quell-Leitfaden migriert (Stand 2026.0.0, geerntet am 2026-08-06):
`.../TechnischeImplementierung/FHIRProfile/Consent`, Abschnitt
„Datenschutz-Aspekte“. Verweis von der Profilseite:
[MII\_PR\_Consent\_Einwilligung](StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.html).*

Da auch die FHIR-Consent-Ressource **keine personenidentifizierenden
Informationen** der einwilligenden Person enthält, sollte der
[**pseudonyme Personenbezug**](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html)
über entsprechende
[**pseudonyme Identifier**](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifier.html)
hergestellt werden. Etwaige personenidentifizierende Informationen (z. B.
Geburtsdatum, Geschlecht, Anschrift) sowie Referenzen, z. B. auf
(Klartext-)Patienten-Profile, sollten vor Ausleitung geeignet ersetzt werden.

*Technisch gesehen können Patienten-Ressourcen und abgeleitete Profile verwendet
werden, wie z. B. die Profile der
[AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html)
oder der
[MII](https://simplifier.net/medizininformatikinitiative-modulperson/sdmiipersonpatientpseudonymisiert).*
Um Pseudonyme, Fallnummern usw. unterscheiden zu können, ist es unabhängig davon
erforderlich, eine Kategorisierung des verwendeten Identifiers mittels
[`Patient.identifier.type`](https://ig.fhir.de/einwilligungsmanagement/stable/ContextIdentifierType.html)
vorzunehmen.

Die FHIR-Consent-Ressource enthält **keine Dokumenten-Scans und/oder
Unterschriften**. Ist eine Übermittlung je nach Anwendungsfall erforderlich, sind
separate Ressourcen gemäß den
[Vorgaben der AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/DocumentReference.html)
zu erstellen (Consent-Bundles) — in diesem Modul die Profile
[Provenance](StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.html) und
[DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.html).

#### Sicherheitsbetrachtung

Sicherheit ist Risikomanagement bezüglich Vertraulichkeit, Integrität und
Verfügbarkeit.

<div class="mii-highlight mii-highlight-grey" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; im Quell-Leitfaden nicht enthalten</h5>
<p>Der migrierte Quell-Leitfaden f&uuml;hrt keine Angriffs- oder Risikobetrachtung. Es wurde
nichts erfunden; die L&uuml;cke ist im Migrationsbericht vermerkt. Was die Quelle zum
Datenschutz sagt, steht vollst&auml;ndig im Abschnitt oben.</p>
</div>

#### Modul-spezifische Konformitätsanforderungen

<div class="mii-highlight mii-highlight-grey" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; im Quell-Leitfaden nicht enthalten</h5>
<p>Der Quell-Leitfaden formuliert keine als solche gekennzeichneten Sicherheits- oder
Datenschutz-Konformit&auml;tsaussagen. Die Pseudonymisierungs-Empfehlungen oben sind
als Empfehlungen formuliert, nicht als SHALL/SHOULD/MAY; sie wurden nicht in
Konformit&auml;tsaussagen umformuliert.</p>
</div>

#### Verbleibende Risiken

<div class="mii-highlight mii-highlight-grey" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; im Quell-Leitfaden nicht enthalten</h5>
<p>Der Quell-Leitfaden benennt keine verbleibenden Risiken. Nicht erg&auml;nzt.</p>
</div>
