<!-- markdownlint-disable MD041 -->
<!-- Deutsche Übersetzung der Standardsprachseite
     input/pagecontent/conformance.md — beide Dateien müssen dasselbe aussagen
     und dieselben Unterseiten aufführen wie die beiden Menü-Dateien.
     Die ERSTEN DREI Unterseiten tragen die Konformitätsthemen der Seite
     "Conformance" des MII-Meta-Wikis,
     https://github.com/medizininformatik-initiative/kerndatensatz-meta/wiki/Conformance;
     Aufbau wie kerndatensatz-basis input/pagecontent/conformance.md.
     "Sicherheit und Datenschutz" ist eine Ergänzung dieser Vorlage gemäß den
     HL7-IG-Best-Practices — siehe docs/ig-best-practices-checklist.md. -->

### Konformität

Dieser Abschnitt definiert die Konformitätsanforderungen für Systeme, die die
Profile des Moduls **Consent** umsetzen.

* **[Allgemeine Anforderungen](general-requirements.html)** — die
  Konformitäts-Verben (MUSS/SOLLTE/KANN nach RFC-2119), das Beanspruchen von
  Konformität, die Verwendung von Codes in den Profilen und die Erwartungen an
  die FHIR-RESTful-API.
* **[Must-Support](must-support.html)** — was *Must Support* für
  daten-erzeugende und daten-verarbeitende Systeme bedeutet.
* **[Umgang mit fehlenden Daten](missing-data.html)** — wie fehlende oder
  unbekannte Werte kodiert werden.
* **[Sicherheit und Datenschutz](security-and-privacy.html)** — die
  Sicherheits- und Datenschutzbetrachtungen dieses Moduls.

Maßgeblich für die MII-weiten Konformitätsregeln ist die Seite
[Conformance](https://github.com/medizininformatik-initiative/kerndatensatz-meta/wiki/Conformance)
des MII-Meta-Wikis. Allgemeine Anforderungen, Must-Support und Umgang mit
fehlenden Daten geben sie für dieses Modul wieder; bei Abweichungen gilt das
Wiki. Sicherheit und Datenschutz ist eine zusätzliche Seite dieses Leitfadens
gemäß den HL7-IG-Best-Practices.

#### Technische Implementierung

*Aus dem Quell-Leitfaden migriert (Stand 2026.0.0, geerntet am 2026-08-06):
`.../TechnischeImplementierung`. Dieser Abschnitt ist der maßgebliche Text; die
englische Seite ist seine Übersetzung.*

Dieser Abschnitt beschreibt die syntaktischen und semantischen Vorgaben zur
Implementierung des Consent-Moduls.

Weiterhin sind auch Suchparameter definiert, die bei Verwendung der FHIR RESTful
API durch die jeweiligen Systeme implementiert werden müssen. Grundsätzlich
werden logische AND- und OR-Verknüpfungen der FHIR-Search unterstützt, vgl.
[hl7.org/fhir/search.html](http://www.hl7.org/fhir/search.html). Die
modul-eigenen Suchparameter sind unter
[Suchparameter und Operationen](search-parameters-and-operations.html)
beschrieben.

Grundlagen und weitere Details zur Suche und zur FHIR RESTful API werden zum
Zeitpunkt der Erstellung dieses Implementierungsleitfadens im Rahmen der
Basismodule erarbeitet und können zu einem späteren Zeitpunkt die hier gemachten
Vorgaben ergänzen. Ggf. wird dann auch eine neue Version dieses Leitfadens
veröffentlicht.

Hinweise zur Umsetzung stehen im Abschnitt [Anleitung](guidance.html), die
technischen Artefakte im Abschnitt [Artefakte](artifacts.html).

<div class="mii-highlight mii-highlight-grey" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; es wurden keine Konformit&auml;tsaussagen markiert</h5>
<p>Der migrierte Quell-Leitfaden formuliert seine Vorgaben als Flie&szlig;text und als
Must-support-/not-supported-Angaben in den Elementtabellen; er markiert keinen Satz als
Konformit&auml;tsaussage. <b>Kein Satz der Migration wurde zu einer gemacht</b> &mdash;
migrierten Flie&szlig;text in Konformit&auml;tsmarker zu fassen w&uuml;rde seine
Verbindlichkeit &auml;ndern; das ist eine Entscheidung der Modulverantwortlichen, nicht der
Migration.</p>
</div>

---

{:.bg-info}
**Hinweis:** Eine Liste der Konformitätsaussagen ist in der englischen Fassung
dieses Implementierungsleitfadens verfügbar. Die Aussagen sind ausschließlich
auf den englischen Originalseiten markiert und werden nur dort erzeugt.
