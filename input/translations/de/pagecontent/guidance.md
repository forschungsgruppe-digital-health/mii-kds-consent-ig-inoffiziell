<!-- markdownlint-disable MD041 -->
<!-- Übersichtsseite "Anleitung". Ersetzen Sie die [TODO]-Hinweise; die
     Unterseiten-Struktur folgt kerndatensatz-basis. -->

Dieser Abschnitt bündelt die fachlichen Hinweise zur Umsetzung und Nutzung des
Moduls **Consent**.

### Allgemeine Umsetzungshinweise

* **[Datensätze und Beschreibungen](datasets-and-descriptions.html)** —
  ausführliche Beschreibung der Datenelemente / logischen Modelle des Moduls.
* **[UML-Diagramme](uml-diagrams.html)** — visuelle Darstellung der Datenmodelle
  und ihrer Beziehungen.

### Zielgruppenspezifische Hinweise

* **[Anleitung für Forschende](researcher-guidance.html)** — für Forschende, die
  Moduldaten nutzen.
* **[Anleitung für Implementierende](implementer-guidance.html)** — technische
  Hinweise für DIZ-Implementierende.

Fokus des Moduls liegt auf der Umsetzung (Enforcement) der vom Patienten
ausgefüllten Einwilligung auf Basis der Einwilligungs-Policies. Die Abgrenzung,
die der Quell-Leitfaden zieht: Der Einsatz *aller* in der AG
Einwilligungsmanagement entwickelten Profile ist nicht verpflichtend, und die
FHIR-Consent-Ressource enthält weder personenidentifizierende Informationen noch
Dokumenten-Scans oder Unterschriften. Siehe
[Hinweise für Implementierende](implementer-guidance.html) und
[Sicherheit und Datenschutz](security-and-privacy.html).

---
Für Konformitätsanforderungen siehe [Konformität](conformance.html); für die
technischen Artefakte siehe [Profile und Extensions](profiles-and-extensions.html).
