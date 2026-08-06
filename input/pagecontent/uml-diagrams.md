<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate C) &mdash; unreviewed machine translation</h5>
<p>The authoritative text of this module is <strong>German</strong>. This English page is an
<strong>unreviewed machine translation</strong> of
<code>input/translations/de/pagecontent/uml-diagrams.md</code>, migrated from the
Simplifier-rendered guide (version 2026.0.0, harvested 2026-08-06). The diagram itself is the
module's own figure and is <strong>labelled in German</strong>; it was not redrawn. Where the
two language variants differ, the German page applies.</p>
</div>

### UML Diagrams

#### [Consent](StructureDefinition-e0e166b4-0f77-478d-9062-de0034d98ce0.html)

The Consent resource is a purely machine-readable representation of a person's
real-world consent and is used to enforce the consent policies.

The consent is collected in a concrete context (e.g. MII), which in FHIR is
modelled as a reference to the responsible organisation
([Organization](https://ig.fhir.de/einwilligungsmanagement/stable/Organization.html))
and/or to a research project
([ResearchStudy](https://ig.fhir.de/einwilligungsmanagement/stable/ResearchStudy.html)).

#### [Provenance](StructureDefinition-f675b1e8-9f3f-44e8-bb59-9681f78eb464.html)

The Provenance resource describes the provenance of the consent content
(signatures among other things) and links it to the persons involved
([Patient](https://ig.fhir.de/einwilligungsmanagement/stable/Patient.html),
consent witness) and to any document scans
([DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.html)).
The application systems used for the collection can likewise be named (display)
or referenced, as can the patient identifiers valid in the application system.

#### Representing questionnaires

Using *all* of the profiles developed in the AG Einwilligungsmanagement is *not
mandatory*. For representing the questionnaire-based content (see
[Questionnaires](implementer-guidance.html)), the recommendations of the TFCU are
to be observed.

#### Relevant profiles

Notes on the UML class diagram of the Consent extension module:

- Classes coloured *blue* are considered in the FHIR representation and
  profiling, are profiled in this IG, and are required for the MII
  implementation.
- Classes coloured *orange* are profiled in the IG of the AG
  Einwilligungsmanagement and are required for the MII implementation.
- Classes coloured *grey* are profiled in the IG of the AG
  Einwilligungsmanagement and are optional for the MII implementation.
- Classes coloured *light grey* are referenced. They are, however, not considered
  in the FHIR representation and profiling.

The attributes shown in the classes of the diagram are mandatory. Further
optional attributes may be provided in addition.

![UML class diagram of the information model, MII-specific](information-model_UML-Diagramm_MII-spez.png)
