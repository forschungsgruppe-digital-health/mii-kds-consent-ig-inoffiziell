# Adversarial verification — LANE FACT (factual accuracy)

Verified 2026-08-31 against the recon reports, the four local clones
(`recon/{agent-skills,source,source-tag,template}`), the sandbox clone (`recon/sandbox-consent`),
the wiki clone (`recon/wiki-meta`), and live read-only `gh`/`curl` re-measurement.
Target: `plan/consent-migration-plan.md`.

## Method

Every checkable factual claim in the plan was cross-checked against the recon reports; the ~10
most load-bearing were re-measured live or in the clones. MEASURED = command output below;
everything not listed as a finding **checked out clean**.

## Claims re-measured and CONFIRMED (no findings emitted)

| Claim | Re-measurement |
|---|---|
| master HEAD `792f9f3e` == tag `2026.0.0`, diff empty; develop +18; tags no `v` prefix | `git rev-parse HEAD` / `git rev-parse 2026.0.0^{commit}` both `792f9f3e4ce496185b428691d2ce252f2e18b9f2`; `git diff --stat` 0 lines; `git rev-list --count master..origin/develop` = 18 |
| 32 files, no `.github/`, README 43 lines | `find` = 32; `ls .github` → No such file; `wc -l README.md` = 43 |
| 2 `urn:oid` CS canonicals; Einwilligung UUID id vs slug url (xml:3-4); example dangling canonical at `Example_MII_Consent_Einwilligung.xml:40`; all 6 SPs id-less | sed/grep on the clone — all exact |
| agent-skills v0.25.0 = tag `5c0cc0c3…`, `version.txt` 0.25.0; expected-steps.tsv = **31 data rows** | `git log -1`; `grep -v '^#' … | tail -n +2 | wc -l` = 31 |
| Template v0.13.2 HEAD `a2390dea…`; M6 regex at `convention-check.mjs:192-195`; `.gitignore:24 *.log`; `ig.ini:42` URL template; `go-publish.yml:102/114`; `sushi-config.yaml:391-395` + `:233-237`; `language-model-check.sh:46`; `convention-check.yml:70-71`; bootstrap removal list at `first-run-bootstrap.sh:174` | all sed-verified byte-exact |
| verifier exit semantics "1 while any DIVERGIERT, 3 while NICHT PRÜFBAR remain" | `verify-migration.py` main: `status = 1 if nd else (3 if nu else 0)` |
| license-align expectation (exit 0, `license-replaced:` + FIX row): source LICENSE 18,658 B ≠ template LICENSE 18,657 B → replace path runs | `cmp` → DIFFER; replace path at license-align.py:~360 emits `license-replaced: … mode=source-file` |
| no `--source-guide-url` on the verifier; it exists on `comparison-table.py` | grep: 0 vs 6 hits |
| migration-spec cites: 32-34, 133-174, 396-402, 536-542, 755-767, 1009-1020, 1106-1116, 1405-1412, 1442-1453, 1844-1850, 2033-2041, 2046-2049; SKILL.md 79, 85-93, 399+, 430-432, 460; expected-steps.tsv:40-41; verify-migration.py:1034-1046, 2129-2133; provenance.md 54-56, 94/102 (F2 `2.0.3-snapshots` vs `2.0.3`) | all sed-verified, content matches the plan's paraphrases |
| registry dist-tags.latest `2026.0.0`, rc-1..rc-4 present; guide root HTTP 200 | live `curl` |
| sandbox: default branch `develop`, pushedAt 2026-08-06T19:07Z, PR #3 OPEN (2026-08-06T16:01Z), #1 CLOSED; template v0.6.0 vendored; "CI preview is disabled for this branch" (migration-report.md:525); base `4d44dbe` 3 commits behind develop | live `gh` + clone grep + `git rev-list --count` = 3 |
| Dokument PR #36 OPEN, draft, "…v0.13.1, DE-first"; ig-template latest v1.3.4 (2026-08-28); module-template latest v0.13.2 (2026-08-31T15:03:47Z) | live `gh` |
| zero 2027/ballot hits on the source repo | live `gh api search/issues` → 0 / 0 |
| wiki `Release-2027.md:9` = "IG Umbau - DE First" | sed on wiki clone — exact |
| Studie comparison numbers (60 artefacts, 22 pages ×2, Dokument 12 page-groups) | grep in `recon/studie-plan-precedent.md:158` |
| snapshots 18/21 on 2.0.2 / 21/21 on 2.0.3; 21 SDs / 0 snapshots both versions | provenance.md:54 + context.md §c (sandbox) |

## FINDINGS (defects with evidence)

### FACT-1 · MINOR — "~180-link external rewrite surface" contradicts its own cited census (sums to 160)
Plan §1 ("a ~180-link external rewrite surface") and §8 ("a ~180-link rewrite surface") cite the
census in recon/guide.md §g.5 — which the plan itself reproduces correctly in §2.2. That census
sums to **160**: 63+3 (hl7.org+www) + 34 (ig.fhir.de) + 26 (mii.de) + 11 (art-decor) + 5
(simplifier) + 4 (github) + 4 (ths-greifswald) + 2 (wiki.hl7.de) + 2 (iospress) + 2
(creativecommons) + 1+1+1+1 (ihe/bfarm/build.fhir/bmc) = 160 (`python3` sum, MEASURED).
No source anywhere in the recon gives ~180. Fix: say "~160-link" (or state explicitly what the
extra ~20 counts, e.g. per-page logo/CSS asset references — currently unbacked).

### FACT-2 · MINOR — "30 of 31 open issues" is stale/wrong; live measurement: Stäubert authored 40 of 44
Plan §2.1 People: "Sebastian Stäubert (… 30 of 31 open issues)" (citing recon/context.md §d).
Live re-measurement 2026-08-31:
`gh api "search/issues?q=repo:medizininformatik-initiative/kerndatensatzmodul-consent+type:issue+state:open" --jq .total_count` → **44**;
author breakdown via `gh issue list … --json author` → **SebStaeubert 40**, four others 1 each.
recon/source.md §g already said "Open issues: 44" — the plan copied context.md's contradicting
count without resolving the recon-internal conflict. The conclusion (Stäubert dominant, primary
contact) survives; the numbers do not. Fix: "40 of 44 open issues".

### FACT-3 · MINOR — Phase 10.2 command passes `--expected-nonzero` to `verify-migration.py`, which has no such flag
Plan Phase 10.2: "`verify-migration.py --expected-nonzero --target . --source …`". MEASURED:
`grep -c "expected.nonzero" scripts/verify-migration.py` → **0**; the argparse block
(verify-migration.py:3456-3483) defines no such option → the command exits with an argparse error
as written. `--expected-nonzero WHY` belongs to the run-log wrapper `migration-log.sh run`
(migration-log.sh:72,99,433-434 — and it **requires a WHY argument**, so even in the wrapper the
bare form would swallow `--target` as the reason). The skill's own invocation is
`bash "$ML" run 11 verify-migration --emits-runlog --expected-nonzero '…' -- python3 …/verify-migration.py --target . …`
(SKILL.md:354-359). Fix: move the flag (with a WHY string) onto the `run` wrapper in the plan's
command line.

### FACT-4 · MINOR — D-10 "counts decide M9" misstates the spec's rule for researcher-guidance/metadata
Plan D-10 *Who:* "counts decide M9 (agent measures, human ratifies)"; recommendation "REMOVE
researcher-guidance/…/metadata (re-measure at Gate 0 — counts, not preference)". The cited spec
(migration-spec.md:1988-1995, MEASURED) decides only extensions/search-parameters/operations/
value-sets/code-systems by built-package artifact count; **researcher-guidance and metadata are
decided from "source narrative for them"**, not counts. Material because the guide DOES carry a
candidate researcher-guidance narrative: page 6.1.5 "Empfehlungen zur praktischen Anwendung"
(4,300 B, recon/guide.md §a #17) — under the spec's actual criterion "REMOVE researcher-guidance"
is not automatic; it depends on where the page map routes that page. Fix: split the D-10 rule
(counts for the five artifact pages; source-narrative presence for researcher-guidance/metadata,
cross-referenced with the Empfehlungen page's map row).

### FACT-5 · MINOR — D-0(b) blurs which FGDH repo the Release-2027 wiki names
Plan D-0: "the Release-2027 wiki names BOTH MII's own `mii-ig-publisher-migration` skill and the
FGDH toolkit's **sandbox demonstrator** (wiki Release-2027.md:4-7)". MEASURED (wiki clone, lines
6-7): the second link is `https://github.com/forschungsgruppe-digital-health/mii-kds-sample-ig-inoffiziell`
— the **sample-IG** reference migration, NOT the Consent sandbox `mii-kds-consent-ig-inoffiziell`
that the plan calls "the sandbox (demonstrator)" everywhere else (§1, D-0(a), Phase 0.2, R1).
As written, D-0(b) invites the reading that the wiki endorses the Consent sandbox; it does not
mention it. Fix: name `mii-kds-sample-ig-inoffiziell` explicitly in D-0(b).

## NICHT PRÜFBAR (checked, could not be decided — no finding)

- The true total of external links if chrome/asset references are meant to be included in
  FACT-1's "~180" — the census methodology (content links only) is the only measured basis.
- Whether the two `.page.md` files "live only in the project file store" (plan D-8) — recon/guide.md
  §e marks this as INFERENCE behind Simplifier auth; the plan states it slightly more firmly than
  the evidence carries, but it is consistent with their measured absence from git.

Everything else in the plan that was checked — including all pinned-context coordinates, all
template/skill file:line citations sampled (~35), the goFSH/harvest/snapshot measurements, and
the license-align expectation — is backed by the recon evidence or by live re-measurement.
