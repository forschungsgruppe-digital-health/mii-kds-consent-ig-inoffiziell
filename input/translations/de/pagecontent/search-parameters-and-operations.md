<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED NARRATIVE. Source: the Simplifier-rendered guide
  miiigmodulconsent, PUBLISHED version 2026.0.0, page
    https://simplifier.net/guide/miiigmodulconsent/MIIIGModulConsent/TechnischeImplementierung?version=2026.0.0
  (its search-parameter paragraphs, routed here per spec 9 — a section
  within the fixed page set, never a page of its own).
-->

### Suchparameter dieses Moduls

Es sind Suchparameter definiert, die bei Verwendung der FHIR RESTful API durch
die jeweiligen Systeme implementiert werden müssen. Grundsätzlich werden logische
AND- und OR-Verknüpfungen der Suchparameter unterstützt.

Grundlagen und weitere Details zur Suche und zur FHIR RESTful API wurden zum
Zeitpunkt der Erstellung dieses Implementierungsleitfadens im Rahmen der
Basismodule erarbeitet und können zu einem späteren Zeitpunkt ergänzt bzw.
präzisiert werden.

Dieses Modul definiert sechs Suchparameter auf der Consent-Ressource. Sie sind
mit ihren Canonicals und Expressions in der generierten Artefaktliste aufgeführt.

> [TODO:REVIEW — Gate A/B. Die sechs SearchParameter-Ressourcen tragen **in der
> Quelle keine `id`**; goFSH hat je eine erzeugt. Diese erzeugten Ids werden zu
> den Ids des Moduls und sind durch einen Menschen zu bestätigen.]
{: .mii-highlight .mii-highlight-grey}
