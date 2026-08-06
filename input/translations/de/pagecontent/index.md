<!-- markdownlint-disable MD041 -->

### Einleitung

Diese Spezifikation beschreibt die FHIR-Repräsentation des
Kerndatensatz-(KDS-)Moduls **Consent** der Medizininformatik-Initiative
(MII). Sie beschreibt die Anwendungsfälle des Moduls sowie die zugehörigen
FHIR-Profile, Extensions und Terminologie-Ressourcen in ihrer verbindlichen
Form. Der MII-Kerndatensatz dient der standardisierten Nutzung klinischer
Routinedaten für die medizinische Forschung.

> Das MII KDS Modul Consent ist ein Basismodul des Kerndatensatzes (KDS) der
> Medizininformatik-Initiative (MII). Es beschreibt, wie die
> Einwilligungsinformationen in Form von FHIR-Ressourcen für die Verarbeitung in
> einer lokalen Treuhandstelle und/oder einem DIZ einheitlich abgebildet werden.
> Es setzt auf den publizierten Vorarbeiten der MII Taskforce Consent Umsetzung
> und den FHIR-Profilen der HL7-D/IHE-D AG Einwilligungsmanagement auf und
> präzisiert diese für die Anforderungen der MII. — migriert von der Leitfadenseite
> *Beschreibung Modul Consent*. TODO:REVIEW an Gate B.
{: .mii-highlight .mii-highlight-grey}

| Veröffentlichung |               |
|------------------|---------------|
| Datum            | *nicht gesetzt — siehe Migrationsbericht, Entscheidungsliste* |
| Version          | 2026.0.1 (CalVer `JJJJ.n.n`) |
| Status           | active        |
| Realm            | DE            |

### Zielgruppe

Dieser Implementierungsleitfaden richtet sich an:

<div class="mii-highlight mii-highlight-blue">
<h5>Implementierende</h5>
<p>Datenintegrationszentren (DIZ), Software-Entwickelnde und System-Architekt:innen, die FHIR-basierte Lösungen umsetzen.<br/>
→ siehe <a href="profiles-and-extensions.html">Profile und Extensions</a> und <a href="logical-models.html">Logische Modelle</a>.</p>
</div>

<div class="mii-highlight mii-highlight-green">
<h5>Forschende</h5>
<p>Wissenschaftler:innen, die MII-Daten für die medizinische Forschung nutzen.<br/>
→ siehe <a href="researcher-guidance.html">Anleitung für Forschende</a>.</p>
</div>

### Inhalt dieses Leitfadens

- **[Anleitung](guidance.html)** — Einstieg und fachliche Hinweise.
- **[Konformität](conformance.html)** — verbindliche Anforderungen, Must-Support
  und der Umgang mit fehlenden Daten.
- **[Profile und Extensions](profiles-and-extensions.html)** und
  **[Terminologie](terminology.html)** — die technischen Artefakte.
- **[Beispiele](examples.html)** — Beispielinstanzen.

### Verwandte Leitfäden

Dieses Modul ist Teil des MII-Kerndatensatzes; die weiteren KDS-Module und ihre
Abhängigkeiten sind unter
[medizininformatik-initiative.de](https://www.medizininformatik-initiative.de/)
beschrieben.

> Dieses Modul hängt formal von `de.einwilligungsmanagement` ab (den FHIR-Profilen
> der HL7-D/IHE-D AG Einwilligungsmanagement,
> [ig.fhir.de/einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/)),
> von denen seine drei Profile abgeleitet sind, sowie von `hl7.fhir.uv.crmi`.
> Zum MII-Basismodul **Person** besteht ein Bezug über den pseudonymen
> Personenidentifikator — siehe [Hinweise für Implementierende](implementer-guidance.html).
{: .mii-highlight .mii-highlight-grey}

Weitere FHIR-Implementierungsleitfäden finden Sie im offiziellen
**[FHIR IG Registry](https://fhir.org/guides/registry/)** (Quelle:
[`FHIR/ig-registry`](https://github.com/FHIR/ig-registry)).

### Impressum

Dieser Leitfaden ist im Rahmen der Medizininformatik-Initiative erstellt worden
und unterliegt per Governance-Prozess dem Abstimmungsverfahren des
Interoperabilitätsforums und der Technischen Komitees von HL7 Deutschland e. V.

### Ansprechpartner

Fragen zu dieser Publikation können im HL7-FHIR-Zulip
[chat.fhir.org](https://chat.fhir.org) im Stream `german/mi-initiative` oder im
MII-Zulip [mii.zulipchat.com](https://mii.zulipchat.com/) im Stream
`MII-Kerndatensatz` gestellt werden.
Anmerkungen und Kritik werden als *Issues* auf
[GitHub](https://github.com/forschungsgruppe-digital-health/mii-kds-consent-ig-inoffiziell/issues) entgegengenommen.

> Inhaltlich verantwortlich für dieses Modul ist die **MII Taskforce Consent
> Umsetzung**. Leitung des Moduls: Sebastian Stäubert, Martin Bialke. Technische
> Umsetzung: Stefan Lang (FHIR-Profile und ImplementationGuides), Martin Bialke
> (ImplementationGuides). Ansprechpartnerin bei der TMF: Karoline Buckow. Fragen
> können auch formlos an `office@medizininformatik-initiative.de` gesendet werden.
{: .mii-highlight .mii-highlight-grey}

### Autor:innen (in alphabetischer Reihenfolge)

> Das Modul Consent ist unter Mitarbeit von Martin Bialke, Sebastian Stäubert,
> Angela Merzweiler, Lars Geidel, Jörg Römhild, Raffael Bild, Fabian Prasser und
> Stefan Lang (HL7 Deutschland, technisches Komitee FHIR, Gefyra GmbH, Lang Health
> IT Consulting) entstanden. — migriert aus dem Abschnitt *Autoren und
> Ansprechpartner* des Leitfadens; eine Zuordnung Institution je Person nennt die
> Quelle nicht. TODO:REVIEW an Gate B.
{: .mii-highlight .mii-highlight-grey}

### Urheberrecht und Lizenz

© 2019+ TMF e. V., Charlottenstraße 42, 10117 Berlin

Dieses Werk ist lizenziert unter der
[Creative Commons Namensnennung 4.0 International Lizenz (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.de).

Für die Nutzungsrechte der zugrunde liegenden FHIR-Technologie siehe die
FHIR-Basisspezifikation.

Einige der verwendeten Codesysteme werden von anderen Organisationen
veröffentlicht und gepflegt; es gilt das Urheberrecht der jeweiligen Herausgeber.

### Haftungsausschluss

Der Inhalt dieses Dokuments ist öffentlich. Bitte beachten Sie, dass Teile
dieses Dokuments auf FHIR Version R4 basieren, dessen Urheberrecht bei
HL7 International liegt.

Obwohl diese Publikation mit größter Sorgfalt erstellt wurde, können die
Autor:innen keine Haftung für direkte oder indirekte Schäden übernehmen, die
aus dem Inhalt dieser Spezifikation entstehen könnten.
