# Terminologie - MII Implementation Guide Consent v2026.0.0

* [**Inhaltsverzeichnis**](toc.md)
* **Terminologie**

## Terminologie

 Diese Seite enthält Übersetzungen aus der Originalsprache, in der der Leitfaden verfasst wurde. Informationen zu diesen Übersetzungen und Anweisungen zum Abgeben von Feedback zu den Übersetzungen finden Sie [hier](translationinfo.md). 

##### TODO:REVIEW (Gate B) — Startseiten-Vorlage, Narrativ noch nicht migriert

Dies ist die **Vorlagenseite des MII-KDS-Modul-Templates**, unveraendert uebernommen. Es ist **nicht** das Narrativ des MII-KDS-Moduls Consent.

Der Leitfadentext des Moduls existiert nur als gerenderter Simplifier-Guide (`simplifier.net/guide/miiigmodulconsent`) und liegt **nicht im Quell-Repository**. Es gab daher nichts, was in diese Seite haette migriert werden koennen, und es wurde nichts erfunden. Seitenstruktur, Menue und Artefakt-Rendering sind echt; der Fliesstext ist ein Platzhalter, bis das Narrativ von Simplifier migriert ist.

Diese Seite beschreibt die im Modul **Consent** verwendeten ValueSets und CodeSystems. Allgemeine Hinweise zur Verwendung von Codes: siehe [FHIR Terminology](http://hl7.org/fhir/R4/terminologies.html).

**Wichtig:** CodeSystem-Ressourcen externer Terminologien (z. B. ICD-10-GM, OPS, SNOMED CT) werden in diesem Modul **nicht** publiziert, sondern über den MII-Terminologieserver (SU-TermServ) bezogen: [https://mii-termserv.de/](https://mii-termserv.de/).

**Expansionen:** ValueSet-Expansionen dieses Leitfadens werden über einen FHIR-Terminologieserver erzeugt — über SU-TermServ, sofern das Client-Zertifikat konfiguriert ist, sonst über den öffentlichen HL7-Server `tx.fhir.org` (dann expandieren einige MII-spezifische ValueSets ggf. nicht vollständig).

> [TODO: Falls Ihr Modul SNOMED CT nutzt, geben Sie die verwendete Edition/Version an. Listen Sie die modul-eigenen ValueSets/CodeSystems auf oder verweisen Sie auf die automatisch erzeugte Artefakt-Liste. Soll Ihr Modul Implementierenden eine verbindliche Anforderung an Expansionen auferlegen, gehört sie auf die Konformitätsseiten — diese Seite gehört nicht zum Konformitäts-Abschnitt.]

