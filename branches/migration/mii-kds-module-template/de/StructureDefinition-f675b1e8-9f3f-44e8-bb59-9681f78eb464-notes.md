<!--
  MII_PR_Consent_Provenance — Anmerkungen, DEUTSCHE FASSUNG (Quelltext, massgeblich).
  Herkunft: .../TechnischeImplementierung/FHIRProfile/Provenance?version=2026.0.0
  Der Abschnitt "Beispiele" der Quellseite konnte auf Simplifier selbst nicht
  gerendert werden ("Command 'xml' could not render: File not found for
  'subject=examples-example-mii-consent-provenance'"). Er ist hier gemaess
  Direktiven-Crosswalk als Verweis auf die Beispiel-Artefaktseite aufgeloest.
-->

*Nachfolgend werden nur die Unterschiede zum
[Basis-Profil](https://ig.fhir.de/einwilligungsmanagement/stable/Provenance.html)
erläutert.*

| FHIR-Element | Erklärung |
| --- | --- |
| `Provenance.entity.what` | Soll ein Dokumenten-Scan angehängt werden, muss die referenzierte Ressource vom Profiltyp [DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.html) sein, Must-support |
| `Provenance.entity.signature.type` | Soll eine base64-codierte Unterschrift angehängt werden, muss die Art der Unterschrift gemäß [MII\_VS\_Consent\_SignatureTypes](ValueSet-88464c5b-5338-4c2b-9c07-b42fef2ada64.html) erfolgen, Must-support |

### Beispiel

- [Beispiel (vollständig)](Provenance-55219d12-6245-4de4-8b50-ddf6f16a789b.html)

> **TODO:REVIEW (Gate B).** Auf der gerenderten Quellseite schlug die Einbettung
> genau dieses Beispiels fehl („File not found“). Das Beispiel existiert im
> Modul und wird von diesem Leitfaden als eigene Artefaktseite gerendert — die
> Migration behebt damit einen Renderfehler der Quelle. Bitte bestätigen, dass
> es dasselbe Beispiel ist, das die Quelle einbetten wollte.
{: .mii-highlight .mii-highlight-grey}
