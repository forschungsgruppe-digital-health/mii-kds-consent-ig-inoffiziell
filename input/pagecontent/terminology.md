<!-- markdownlint-disable MD041 -->
<div class="mii-highlight mii-highlight-orange" markdown="0">
<h5>TODO:REVIEW (Gate B) &mdash; starter page, narrative not yet migrated</h5>
<p>This is the <strong>MII KDS module template's starter page</strong>, carried over as-is.
It is <strong>not</strong> the narrative of the MII KDS Modul Consent.</p>
<p>The module's guide text exists only as a rendered Simplifier guide
(<code>simplifier.net/guide/miiigmodulconsent</code>); it is <strong>not in the source
repository</strong>, so there was nothing to migrate into this page and nothing was
invented for it. The page <em>structure</em>, the menu and the artifact rendering below are
real; the prose is a placeholder until the narrative is migrated from Simplifier.</p>
</div>

<!-- Source: kerndatensatz-basis input/pagecontent/terminology.md; SNOMED CT
     version policy from the meta wiki page "Terminology Version Policy".
     Terminology page. The IG Publisher lists ValueSets/CodeSystems on the
     artifact pages automatically; this page carries the MII notes on them.
     German mirror: input/translations/de/pagecontent/terminology.md. -->

This page describes the ValueSets and CodeSystems used in the
**Consent** module. For general guidance on using codes, see
[FHIR Terminology](http://hl7.org/fhir/R4/terminologies.html).

{:.bg-info}
**Important:** CodeSystem resources of external terminologies (e.g. ICD-10-GM,
OPS, SNOMED CT) are **not** published in this module; they are obtained from the
MII terminology service (SU-TermServ):
[https://mii-termserv.de/](https://mii-termserv.de/).

{:.bg-info}
**Expansions:** ValueSet expansions in this guide are produced by a FHIR
terminology server — SU-TermServ if the client certificate is configured,
otherwise the public HL7 server `tx.fhir.org` (in which case some MII-specific
ValueSets may not expand completely).

> [TODO: If your module uses SNOMED CT, state the edition/version used. List the
> module's own ValueSets/CodeSystems, or refer to the automatically generated
> artifact list. If your module wants to place a binding requirement about
> expansions on implementers, state it on the Conformance pages with an explicit
> `§…§` marker — this page is not part of the Conformance section.]
{: .mii-highlight .mii-highlight-grey}
