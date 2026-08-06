<!-- markdownlint-disable MD041 -->
<!--
  HINWEISE FUER IMPLEMENTIERENDE — DEUTSCHE FASSUNG (Quelltext, massgeblich).
  Herkunft des Inhalts (Migration 2026-08-06, spec 5.1c + spec 9):
    - .../KontextimGesamtprojektBezgezuanderenModulen?version=2026.0.0
    - .../Referenzen?version=2026.0.0
    - .../AnwendungsflleInformationsmodell/Fragebgen?version=2026.0.0
    - .../TechnischeImplementierung/FHIRProfile/Empfehlungen-zur-praktischen-Anwendung?version=2026.0.0
  Diese vier Quellseiten sind hier Abschnitte, keine eigenen Seiten: der
  Seitenbestand des Moduls ist fest (spec 9).
-->

### Hinweise für Implementierende

Diese Seite bündelt die fachlich-technischen Hinweise des Moduls Consent für
Datenintegrationszentren und Hersteller: die Einordnung des Moduls, die
Abbildung des MII Broad Consent über Fragebögen, die Empfehlungen zur
praktischen Anwendung und die Referenzen.

### Kontext im Gesamtprojekt / Bezüge zu anderen Modulen

Das Modul Consent dient der Unterstützung von standortübergreifenden
Datennutzungsanfragen basierend auf dem jeweils aktuellen Einwilligungsstatus des
Patienten am Standort.

Um den Bezug zwischen Person und Einwilligung herzustellen, wird die Einwilligung
mit mindestens einem eindeutigen Personenidentifikator versehen (Basismodul:
Person). Dies ist im Regelfall ein
[pseudonymer Identifikator](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html).

#### Verweise auf andere Vorhaben

In der
[Handreichung](https://www.bfarm.de/SharedDocs/Downloads/DE/Forschung/modellvorhaben-genomsequenzierung/Handreichung-zur-Implementierung-beim-LE.pdf?__blob=publicationFile)
zur Patienteninformation & Teilnahmeerklärung zum **„Modellvorhaben
Genomsequenzierung bei seltenen und bei onkologischen Erkrankungen“** nach § 64e
SGB V in der Version V1 wird unter Kapitel 2.1.4 Forschungseinwilligung die
Nutzung des MII-Broad Consent ab der Version 1.6d empfohlen, die im gesetzlichen
Sinn mindestens der Basisversion ohne Zusatzmodule entspricht.

### Fragebögen

Die [AG Einwilligungsmanagement](https://ig.fhir.de/einwilligungsmanagement/stable/)
hat sich umfassend mit der Modellierung von Einwilligungen und
Einwilligungsvorlagen befasst. Der vorliegende Implementation Guide setzt
wesentlich auf diesen Vorarbeiten auf.

#### Die strukturierte Einwilligungsvorlage

Die Profile
[Questionnaire Composed](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireComposed.html),
[Template Frame](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateFrame.html) und
[Template Module](https://ig.fhir.de/einwilligungsmanagement/stable/TemplateModule.html)
basieren auf der FHIR-Ressource Questionnaire und dienen der Abbildung des
Einwilligungsformulars (hier: MII Broad Consent).

Dabei stellt das Template Module einen wiederverwendbaren basalen Bestandteil
dar, welcher in einem oder mehreren Formularabschnitten (TemplateFrames)
verwendet bzw. eingebunden wird. Ein oder mehrere TemplateFrames können zu einem
vollständigen, render-fähigen Formular (QuestionnaireComposed) zusammengesetzt
werden.

#### Die ausgefüllte Einwilligung

Das Profil
[QuestionnaireResponse](https://ig.fhir.de/einwilligungsmanagement/stable/QuestionnaireResponse.html)
bildet den vom Patienten ausgefüllten Fragebogen elektronisch ab. Hier werden die
Antworten des Patienten auf den referenzierten Fragebogen (QuestionnaireComposed)
des MII Broad Consent dokumentiert.

Zur Abbildung der Antworten sollte das Value Set
„[MII Consent: Answer ValueSet](https://art-decor.org/art-decor/decor-valuesets--mide-?id=2.16.840.1.113883.3.1937.777.24.11.30)“
verwendet werden — im vorliegenden Leitfaden das ValueSet
[MII Consent: Answer ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.30--20210323234509.html):

| Checkbox | Code-Bezeichner | Code (OID) |
| --- | --- | --- |
| ‚Ja‘ angekreuzt | gültig | 2.16.840.1.113883.3.1937.777.24.5.2.1 |
| ‚Nein‘ angekreuzt | nicht gültig | 2.16.840.1.113883.3.1937.777.24.5.2.2 |
| nicht angekreuzt | unbekannt | 2.16.840.1.113883.3.1937.777.24.5.2.3 |

*Antworten (Checkbox), Code-Bezeichner und OIDs*

#### Abbildung des MII Broad Consent

Die Datenelemente des MII Broad Consent Formulars in Version
[1.6d](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.1790)
und
[1.6f](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.1791)
sind als Dataset in ART-DECOR modelliert, siehe Abschnitt
[Datensätze inkl. Beschreibungen](datasets-and-descriptions.html).

#### Verwendung einheitlicher Policies

Die benötigten Value Sets sind ebenfalls in ART-DECOR modelliert und mit den
entsprechenden Datenelementen assoziiert. Die Kompatibilität zu IHE BPPC
(Integrating the Healthcare Enterprise,
[Profil „Basic Patient Privacy Consent“](https://www.ihe.net/uploadedFiles/Documents/ITI/IHE_ITI_TF_Vol1.pdf#nameddest=19_Basic_Patient_Privacy_Consen))
wird über Policies adressiert.

Die **Operationalisierung bzw. Durchsetzung (Enforcement) der Consent-Informationen**
wird durch ein
[einheitliches Policy-ValueSet](http://art-decor.org/decor/services/RetrieveValueSet?id=2.16.840.1.113883.3.1937.777.24.11.36&effectiveDate=2021-04-23T10:55:54&prefix=mide-&format=html&collapsable=true&language=de-DE&ui=en-US)
unterstützt. Dies kann interoperabel in IHE BPPC verwendet werden. Im
vorliegenden Leitfaden ist es das ValueSet
[MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.html).

### Empfehlungen zur praktischen Anwendung

#### Bedeutung der Kategorisierung von Consent-Ressourcen mittels ResultType

Im IG der **HL7-D AG Einwilligungsmanagement** und der korrespondierenden
[Publikation](https://ebooks.iospress.nl/doi/10.3233/SHTI251389) wird die
Bedeutung des Parameters `ResultType` umfassend erläutert.

Besonderes Augenmerk sei an dieser Stelle auf die Codes `consent-status` und
`document` gelegt. Weitere Details und Zusammenhänge sind
[hier](https://simplifier.net/guide/Einwilligungsmanagement/Mitgeltende-Erl-uterungen?version=current)
beschrieben.

#### Nutzungsempfehlung zur Verwendung der Consent.category ResultType

Konkrete verpflichtende Projektvorgaben zur Verwendung des Suchparameters
ResultType sind in der Praxis aufgrund heterogener technischer Gegebenheiten an
den MII-Standorten nur bedingt zielführend. Die **technische Umsetzung der
Vorgaben ist abhängig von der konkreten Implementierung**.

Das Einwilligungsmanagement [gICS](https://ths-greifswald.de/gics) stellt die
aktuelle [Referenzimplementierung](https://ebooks.iospress.nl/doi/10.3233/SHTI251389)
des HL7-D FHIR Standards für Einwilligungsmanagement (Version 2.0) dar.

Alle Implementierungen sollten **mindestens folgende Varianten unterstützen**.
Die Kardinalität von `Consent.category` ist mit `2..*` definiert und ermöglicht
die notwendige Abwärtskompatibilität.

| ResultType | Bedeutung für die Consent-Ressource | Aggregation von Informationen |
| --- | --- | --- |
| `document` | Die Consent-Ressource bezieht sich auf **ein (!) ausgefülltes Dokument** (QuestionnaireResponse). *Dies sollte der Default in einem (MII) FHIR-Server sein.* | nein |
| `consent-status` | Die Consent-Ressource **berücksichtigt alle relevanten Einwilligungs- und Widerrufsdokumente** im Kontext der MII **für einen (!) Patienten**. Die Consent-Ressource mit ResultType `consent-status` bezieht sich immer auf einen Patienten und enthält den aktuellen Einwilligungsstand. *Dies sollte idealerweise durch den (MII) FHIR-Server unterstützt werden.* | ja, berechnet durch entsprechende Business-Logik zum Zeitpunkt der Abfrage oder für einen bestimmten Zeitraum |

Idealerweise sollte der FHIR-Server je Patient stets nur eine Consent-Ressource
mit den aktuellen aggregierten Einwilligungsinformationen (ResultType
`consent-status`) vorhalten.

*Ist dies aus dritten Gründen nicht möglich, sollte mindestens je ausgefülltem
Dokument (Einwilligung, aktualisierte Einwilligung, Teil-Widerruf, vollständiger
Widerruf) eine dokumentspezifische Ausleitung ermöglicht werden (ResultType
`document`). Es bleibt in diesem Fall in der Verantwortung des Standortes, diese
Informationen* **in der vom FDPG geforderten Form** *bereitzustellen.*

##### Empfehlungen für gICS-Anwender bezogen auf Kennzahlen-Ermittlung und FDPG

Die Datenintegrationszentren stellen die erforderlichen Informationen zur
Ermittlung von kerndatensatzspezifischen Kennzahlen für das DIZ-Dashboard bereit.
Die Ermittlung der Kennzahlen wird auf Seiten des DIZ-Dashboard durch
entsprechende Aufrufe an die Standorte auch für das MII KDS Consent Modul
getriggert.

Standorte, die das [Einwilligungsmanagement gICS](https://ths-greifswald.de/gics)
verwenden, sollten bei der **Kennzahlen-Ermittlung** sowie bei der Bereitstellung
der Consent-Ressourcen für das **FDPG** den präzisen
[**Hersteller-Empfehlungen**](https://www.ths-greifswald.de/diz-dashboard-empfehlung-gics-kds-consent-status/)
folgen.

### Referenzen

Die Modellierung des Datensatzes zum Modul Consent enthält Referenzen zu
folgenden Projekten:

- [Implementation Guide der Arbeitsgruppe Einwilligungsmanagement des Interop-Forum, Version 1.0](https://ig.fhir.de/einwilligungsmanagement/stable/)
- [Kerndatensatzbeschreibung im ART-DECOR](https://art-decor.org/art-decor/decor-datasets--mide-?conceptId=2.16.840.1.113883.3.1937.777.24.2.184)

Es wurden außerdem die
[Kernspezifikation von HL7 FHIR](http://hl7.org/fhir/), hierunter die
entsprechende Ressource [Consent](http://hl7.org/fhir/consent.html), und die
bisherigen Arbeiten zu den Deutschen Basisprofilen in
[STU3](https://simplifier.net/basisprofilde) und
[R4](https://simplifier.net/basisprofil-de-r4) berücksichtigt.

Die vorliegende Spezifikation wurde gestaltet auf Basis der Beschreibung des
MII-Kerndatensatzes in der Version vom 10.3.2017
([PDF](https://www.medizininformatik-initiative.de/sites/default/files/inline-files/MII_04_Kerndatensatz_1-0.pdf)),
sowie der Datensatzbeschreibung in
[ART-DECOR](https://art-decor.org/art-decor/decor-project--mide-).
