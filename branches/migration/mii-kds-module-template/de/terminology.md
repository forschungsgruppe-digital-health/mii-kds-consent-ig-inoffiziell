# Terminologie - MII Implementation Guide Consent v2026.0.0

* [**Inhaltsverzeichnis**](toc.md)
* **Terminologie**

## Terminologie

### Terminologie

Diese Seite beschreibt die ValueSets und CodeSysteme des Moduls **Consent**. Allgemeine Hinweise zur Verwendung von Codes finden sich unter [FHIR Terminology](http://hl7.org/fhir/R4/terminologies.html).

**Wichtig:** CodeSystem-Ressourcen externer Terminologien (z. B. ICD-10-GM, OPS, SNOMED CT) werden in diesem Modul **nicht** veröffentlicht; sie werden über den MII-Terminologieserver (SU-TermServ) bezogen: [https://mii-termserv.de/](https://mii-termserv.de/).

**Expansionen:** ValueSet-Expansionen in diesem Leitfaden werden von einem FHIR-Terminologieserver erzeugt — SU-TermServ, sofern das Client-Zertifikat konfiguriert ist, sonst der öffentliche HL7-Server `tx.fhir.org` (in diesem Fall expandieren einige MII-spezifische ValueSets möglicherweise unvollständig).

Dieses Modul verwendet **kein SNOMED CT**.

### ValueSets

| | |
| :--- | :--- |
| [MII Consent: Policy ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.36--20230331232804.md) | alle Codes des CodeSystems**MII CS Consent Policy** |
| [MII Consent: Signature Types](ValueSet-88464c5b-5338-4c2b-9c07-b42fef2ada64.md) | die zulässigen Unterschriftsarten |
| [MII Consent: Answer ValueSet](ValueSet-2.16.840.1.113883.3.1937.777.24.11.30--20210323234509.md) | die zulässigen Antworten im Fragebogen |

Erweiterungen des Policy-ValueSets im ART-DECOR werden zeitnah durch die TFCU in diesem IG eingepflegt. Eine erneute Ballotierung ist nicht erforderlich.

#### MII Consent: Signature Types

Gemäß Empfehlung der HL7-D AG Einwilligungsmanagement. Canonical: `https://www.medizininformatik-initiative.de/fhir/modul-consent/ValueSet/mii-vs-consent-signaturetypes`

| | | | |
| :--- | :--- | :--- | :--- |
| Unterschrift der einwilligenden Person | urn:iso-astm:E1762-95:2013 | 1.2.840.10065.1.12.1.7 | Consent Signature |
| Unterschrift der (gesetzlich) vertretenden Person | urn:iso-astm:E1762-95:2013 | 1.2.840.10065.1.12.1.11 | Consent Witness Signature |
| Unterschrift der aufklärenden Person | urn:iso-astm:E1762-95:2013 | 1.2.840.10065.1.12.1.5 | Verification Signature |

**Die Spalte „Art der Unterschrift“ ist eine Erläuterung des Leitfadens; sie steht nicht im ValueSet und wird deshalb hier geführt.**

#### MII Consent: Answer ValueSet

Dieses ValueSet findet ausschließlich im Kontext von Questionnaires Verwendung. Die Zuordnung der Antworten zu den Checkboxen des Formulars steht unter [Hinweise für Implementierende](implementer-guidance.md).

### CodeSysteme

| | |
| :--- | :--- |
| [MII CS Consent Policy](CodeSystem-2.16.840.1.113883.3.1937.777.24.5.3--20251211153003.md) | die Consent-Policy-Codes zur Operationalisierung des MII Broad Consent |
| [MII Consent Version and Modules](CodeSystem-mii-cs-consent-version-modules.md) | die OIDs der Broad-Consent-Versionen und Zusatzmodule |
| [MII Consent: Answer CodeSystem](CodeSystem-2.16.840.1.113883.3.1937.777.24.5.2--20210423105554.md) | gültig / nicht gültig / unbekannt |

#### MII CS Consent Policy

**Hinweis**: Das Konzept der **verschachtelten Provision-Elemente** im MII-Kontext arbeitet mit zwei Leveln. Das übergeordnete Provision-Element, die Level1-Provision, repräsentiert eine Frage in der Einwilligung und legt über `Provision.Type=DENY` (Opt-In-Modell) fest, dass alles verboten ist, außer es ist in Form von untergeordneten Provision-Elementen, den Level2-Provisions, explizit erlaubt. D. h. für die Interpretation, ob eine Erlaubnis für eine bestimmte Nutzung (erheben, speichern, nutzen) von spezifischen Daten (IDAT, MDAT, BIOMAT, …) vorliegt, müssen die Elemente der Level2-Provisions ausgewertet werden.

Teilwiderrufe können ebenfalls auf den Level2-Provisions Änderungen hervorrufen. Z. B. kann die Erhebung untersagt werden, aber die Speicherung und Nutzung kann davon unbetroffen bleiben („MDAT erheben“ = `deny`, aber „MDAT wissenschaftlich nutzen EU DSGVO NIVEAU“ = `permit`).

**Achtung: Für die Nutzung in Level2-Provisions sind ausschließlich Policy-Codes vorgesehen** (in der Konzepttabelle die Konzepte der zweiten Ebene, also die Kind-Konzepte eines Moduls).

Policies, die den Status „deprecated/inactive“ haben, sollen zukünftig nicht mehr neu erzeugten Consent-Ressourcen hinzugefügt werden. Diese Policies sollten zukünftig auch nicht mehr ausgewertet werden (Enforcement).

Das CodeSystem `urn:oid:2.16.840.1.113883.3.1937.777.24.5.3` enthält 101 Konzepte. Die vollständige Tabelle — Ebene (Modul/Policy über die Hierarchie), Display, Code, Gültigkeitsdauer (Property `period-of-validity`) und Status (Properties `status`/`inactive`) — steht auf der Artefaktseite [MII CS Consent Policy](CodeSystem-2.16.840.1.113883.3.1937.777.24.5.3--20251211153003.md) und wird vom IG Publisher aus der Ressource selbst erzeugt.

> **TODO:REVIEW (Gate B) — Policy-Tabelle nicht abgeschrieben.** Der Quell-Leitfaden trägt diese Tabelle mit rund 124 Zeilen als handgepflegtes Markdown auf der Terminologie-Seite. Sie ist hier **nicht** übernommen, weil dieselben Angaben in der CodeSystem-Ressource dieses Moduls stehen und vom IG Publisher gerendert werden; eine zweite, handgepflegte Kopie würde beim nächsten Policy-Zuwachs auseinanderlaufen. Bitte auf der erzeugten Artefaktseite prüfen, dass Gültigkeitsdauer und Status tatsächlich sichtbar sind — andernfalls muss die Tabelle zurück in diese Seite. (Beim Build vom 2026-08-06 waren sie es: Ebene, Display, Code, `P30Y`/`P5Y` und „Deprecated“ stehen auf der erzeugten Seite.) **Eine Formulierung musste dabei umgehängt werden:** Der Klammerzusatz der Quelle „(Siehe nachstehende Tabelle, Spalte Lvl mit Wert 2)“ verweist auf eine Tabelle, die es hier nicht mehr gibt; er zeigt jetzt auf die Konzept-Ebene der erzeugten Tabelle. Inhaltlich derselbe Verweis, aber bitte gegenlesen.

