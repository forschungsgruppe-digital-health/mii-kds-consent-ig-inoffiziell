# Suchparameter und Operationen - MII Implementation Guide Consent v2026.0.1

* [**Inhaltsverzeichnis**](toc.md)
* **Suchparameter und Operationen**

## Suchparameter und Operationen

 Diese Seite enthält Übersetzungen aus der Originalsprache, in der der Leitfaden verfasst wurde. Informationen zu diesen Übersetzungen und Anweisungen zum Abgeben von Feedback zu den Übersetzungen finden Sie [hier](translationinfo.md). 

### Suchparameter dieses Moduls

Es sind Suchparameter definiert, die bei Verwendung der FHIR RESTful API durch die jeweiligen Systeme implementiert werden müssen. Grundsätzlich werden logische AND- und OR-Verknüpfungen der Suchparameter unterstützt.

Grundlagen und weitere Details zur Suche und zur FHIR RESTful API wurden zum Zeitpunkt der Erstellung dieses Implementierungsleitfadens im Rahmen der Basismodule erarbeitet und können zu einem späteren Zeitpunkt ergänzt bzw. präzisiert werden.

Dieses Modul definiert sechs Suchparameter auf der Consent-Ressource. Sie sind mit ihren Canonicals und Expressions in der generierten Artefaktliste aufgeführt.

> [TODO:REVIEW — Gate A/B. Die sechs SearchParameter-Ressourcen tragen **in der Quelle keine `id`**; goFSH hat je eine erzeugt. Diese erzeugten Ids werden zu den Ids des Moduls und sind durch einen Menschen zu bestätigen.]

