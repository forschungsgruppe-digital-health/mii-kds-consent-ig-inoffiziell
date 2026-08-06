<!--
  MII_PR_Consent_Provenance — notes, ENGLISH (translation).
  Source of record: input/translations/de/intro-notes/<same file name>.
-->

{:.bg-warning}
**TODO:REVIEW (Gate C) — unreviewed machine translation.** The authoritative text
is the German notes file. Element paths and code values are identifiers and are
reproduced verbatim.

*Only the differences from the
[base profile](https://ig.fhir.de/einwilligungsmanagement/stable/Provenance.html)
are explained below.*

| FHIR element | Explanation |
| --- | --- |
| `Provenance.entity.what` | If a document scan is to be attached, the referenced resource has to be of profile type [DocumentReference](StructureDefinition-56375452-bfa1-4111-af7c-5b5ba9a1857c.html), must-support |
| `Provenance.entity.signature.type` | If a base64-encoded signature is to be attached, the kind of signature has to follow [MII\_VS\_Consent\_SignatureTypes](ValueSet-88464c5b-5338-4c2b-9c07-b42fef2ada64.html), must-support |

### Example

- [Example (complete)](Provenance-55219d12-6245-4de4-8b50-ddf6f16a789b.html)

> **TODO:REVIEW (Gate B).** On the rendered source page, embedding exactly this
> example failed ("File not found"). The example does exist in the module and is
> rendered by this guide as its own artifact page — the migration therefore fixes
> a rendering failure of the source. Please confirm it is the same example the
> source intended to embed.
{: .mii-highlight .mii-highlight-grey}
