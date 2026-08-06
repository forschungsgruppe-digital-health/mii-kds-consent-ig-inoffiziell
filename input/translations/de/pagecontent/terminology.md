<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; Startseiten-Vorlage, Narrativ noch nicht migriert</h5>
<p>Dies ist die <strong>Vorlagenseite des MII-KDS-Modul-Templates</strong>, unveraendert
uebernommen. Es ist <strong>nicht</strong> das Narrativ des MII-KDS-Moduls Consent.</p>
<p>Der Leitfadentext des Moduls existiert nur als gerenderter Simplifier-Guide
(<code>simplifier.net/guide/miiigmodulconsent</code>) und liegt <strong>nicht im
Quell-Repository</strong>. Es gab daher nichts, was in diese Seite haette migriert werden
koennen, und es wurde nichts erfunden. Seitenstruktur, Menue und Artefakt-Rendering sind
echt; der Fliesstext ist ein Platzhalter, bis das Narrativ von Simplifier migriert ist.</p>
</div>

<!-- Terminologie-Seite. Der IG-Publisher listet ValueSets/CodeSystems auf den
     Artefakt-Seiten automatisch; hier stehen die MII-Hinweise dazu. -->

Diese Seite beschreibt die im Modul **Consent** verwendeten ValueSets
und CodeSystems. Allgemeine Hinweise zur Verwendung von Codes: siehe
[FHIR Terminology](http://hl7.org/fhir/R4/terminologies.html).

{:.bg-info}
**Wichtig:** CodeSystem-Ressourcen externer Terminologien (z. B. ICD-10-GM, OPS,
SNOMED CT) werden in diesem Modul **nicht** publiziert, sondern über den
MII-Terminologieserver (SU-TermServ) bezogen:
[https://mii-termserv.de/](https://mii-termserv.de/).

{:.bg-info}
**Expansionen:** ValueSet-Expansionen dieses Leitfadens werden über einen
FHIR-Terminologieserver erzeugt — über SU-TermServ, sofern das
Client-Zertifikat konfiguriert ist, sonst über den öffentlichen HL7-Server
`tx.fhir.org` (dann expandieren einige MII-spezifische ValueSets ggf. nicht
vollständig).

> [TODO: Falls Ihr Modul SNOMED CT nutzt, geben Sie die verwendete Edition/Version
> an. Listen Sie die modul-eigenen ValueSets/CodeSystems auf oder verweisen Sie
> auf die automatisch erzeugte Artefakt-Liste. Soll Ihr Modul Implementierenden
> eine verbindliche Anforderung an Expansionen auferlegen, gehört sie auf die
> Konformitätsseiten — diese Seite gehört nicht zum Konformitäts-Abschnitt.]
{: .mii-highlight .mii-highlight-grey}
