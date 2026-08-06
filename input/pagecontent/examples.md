<!-- markdownlint-disable MD041 -->
<!--
  MIGRATED. The template's starter text linked the example patient that
  guardrail 5 deletes (Patient-ExamplePatientInstance.html), which the IG
  Publisher reported as a broken link. Replaced with the module's OWN five
  examples, taken from the source repository's examples/ directory.
-->

### Examples

This guide ships the module's own example instances, migrated unchanged from the
source repository's `examples/` directory. They are **synthetic**; the Consent
resource deliberately carries no person-identifying information, so the examples
reference pseudonymous `Patient` and `ResearchStudy` resources that this module
does not itself publish.

| Example | Profile | Source file |
| --- | --- | --- |
| [Consent 34150a23-b1c8-404f-874f-e042a30435d2](Consent-34150a23-b1c8-404f-874f-e042a30435d2.html) | MII\_PR\_Consent\_Einwilligung | `examples/Example_MII_Consent_Einwilligung.xml` |
| [Consent 5143266b-8d60-4b28-8ee9-635140ffa5bb](Consent-5143266b-8d60-4b28-8ee9-635140ffa5bb.html) | MII\_PR\_Consent\_Einwilligung | `examples/Example_MII_Consent_ResultType_ConsentStatus.xml` |
| [Consent Example-MII-Consent-ResultType-document](Consent-Example-MII-Consent-ResultType-document.html) | MII\_PR\_Consent\_Einwilligung | `examples/Example_MII_Consent_Einwilligung_2.xml` |
| [DocumentReference 8a3d1799-2463-405e-b49c-6a16c8692b01](DocumentReference-8a3d1799-2463-405e-b49c-6a16c8692b01.html) | MII\_PR\_Consent\_DocumentReference | `examples/Example_MII_Consent_DocumentReference.xml` |
| [Provenance 55219d12-6245-4de4-8b50-ddf6f16a789b](Provenance-55219d12-6245-4de4-8b50-ddf6f16a789b.html) | MII\_PR\_Consent\_Provenance | `examples/Example_MII_Consent_Provenance.xml` |

> **TODO:REVIEW — Gate A.** The published package `…kerndatensatz.consent@2026.0.1-rc-4`
> carries a **sixth** example, `Consent/89f494a3-cd75-44f5-a78a-581dfdd47a94`
> (`package/examples/Example_MII_Consent_Einwilligung_1.json`), which is **not in
> the source repository**. This guide ships what the repository holds. A human
> decides whether the sixth example belongs here.
{: .mii-highlight .mii-highlight-grey}
