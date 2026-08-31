# RISK-lane adversarial verification — consent-migration-plan.md (2026-08-31)

Lane: completeness, sequencing, decision quality. Only evidence-backed defects are reported;
checks that passed are not listed. Plan under test:
`scratchpad/plan/consent-migration-plan.md` (line numbers below refer to it).

## RISK-1 · MAJOR — In-place route: the write-access decision and mechanics are missing

The plan's headline route is "on GO, migrate IN PLACE on the MII repo" (plan lines 22-24) and
Phase 0.2 says "In-place: branch on the MII repo" (plan lines 420-425). D-0 asks the owner for
"GO for a migration and its venue" (lines 215-220) — but nowhere does the plan state HOW a branch
on `medizininformatik-initiative/kerndatensatzmodul-consent` comes into existence:

- The standing access policy makes every MII repo read-only for agents except the two template
  repos (user MEMORY "MII org access policy": "tier 1: the two MII template repos = full workflow;
  ... all other MII repos read-only"), and this engagement's own §7 (lines 646-649) confirms the
  read-only scope. Executing in-place therefore requires BOTH an owner-side access grant
  (collaborator/branch rights, or an owner-sanctioned fork+PR) AND an explicit user
  re-authorization widening the agent policy for that one repo. Neither appears as a decision or
  a Phase-0 step.
- The Dokument precedent the plan leans on (PR #36, recon/context.md §f) proves the interaction
  MODEL works, but access rights are per-repo; whether msusky can push to the consent repo is
  NICHT PRÜFBAR from the recon and the plan never asks.
- Asymmetry: Phase 0.2 gives the sandbox a measured mechanics list (SSH for workflow-file pushes,
  repo variables, Pages) but the in-place branch — which carries the same `.github/workflows/`
  files and needs Pages/preview enablement on a repo that has NO `.github/` at all
  (recon/source.md §a: "no CI whatsoever") — gets no equivalent checklist.

**Fix:** add to D-0 an explicit access-mechanics sub-question (owner grants write / owner pushes
the branch / sanctioned fork-PR), a plan-level line that in-place execution needs the user to
re-authorize beyond the current read-only policy, and an in-place venue-enablement checklist
mirroring the sandbox one (Actions/Pages state, SSH push for workflow files).

## RISK-2 · MAJOR — The entire evidence base lives in volatile /private/tmp with no persistence step

The plan's evidence citations are "recon/<report>.md plus the underlying file:line" (plan
lines 5-7), and every one of those artifacts — the recon reports, the 18 harvested guide-page
HTML snapshots (recon/guide.md Evidence appendix), the source/template/agent-skills clones, the
extracted package tarballs, and the plan itself — lives under
`/private/tmp/claude-503/.../scratchpad/`. MEASURED on this machine: `kern.boottime` = Jun 11
2026 and the oldest `/private/tmp` entries date to Jun 11-12 — i.e. /tmp is cleared at reboot;
one OS update between now and execution deletes the plan's whole evidence base. The plan's own
effort section says wall-clock is "dominated by owner-decision latency" (lines 642-643), i.e.
the wait is exactly where the loss risk accrues, and the /tmp-scratchpad volatility is a known
precedent failure mode. No phase copies anything to a durable location; the
"measure-at-execution-time" list (lines 401-408) re-measures live sources but cannot re-create
the 2026-08-31 snapshots (e.g. the guide HTML as-of-today, the rc-4 tarball state) that D-2/D-9
argue from.

**Fix:** add a Phase-0.0 step (before the D-0 wait): persist the recon reports, harvested HTML,
tarballs, and the plan to a durable location (sandbox repo branch, or a directory outside /tmp).

## RISK-3 · MAJOR — Sequencing: the single-point-of-failure harvest waits behind the unbounded D-0 latency

The plan itself declares the narrative a "single point of failure: 14 pages only in Simplifier;
predecessor guide already deleted" (risk R4, line 619) and its mitigation says "Harvest early" —
yet the execution plan schedules the harvest as Phase 4, AFTER Phase 0 (blocked on D-0, "THE
critical path", line 420, with no response deadline) and after Phase 3 goFSH work. The harvest
route ② is anonymous and read-only (recon/skills.md §b: `guide-harvest.sh`, verified anonymous;
recon already fetched all 18 pages today without credentials) — nothing about it requires GO,
a venue, or a toolchain beyond the script. Meanwhile the only existing copies of the pages sit
in the volatile scratchpad (RISK-2). If the guide is deleted or replaced during a weeks-long
D-0 silence — the plan's own evidence shows the 2023 guide vanished from Simplifier
(recon/guide.md §b) — Phases 4-8 lose their input.

**Fix:** run the route-② harvest immediately as a Phase-0 preservation act, persist it durably,
and re-run it at execution time for pinned provenance (the run-of-record harvest). The plan even
calls the harvest "also a preservation act" (line 160) without scheduling it as one.

## RISK-4 · MAJOR — Registry-vs-tree drift: the packaged 6th example has no recorded disposition

The published 2026.0.0 package contains `Example_MII_Consent_Einwilligung_1.json` "that has NO
XML source in the repo" (recon/source.md §e line 87, §h line 126). The plan NOTES this in the
drift bullet (lines 99-102) but D-2's recommendation "migrate tag 2026.0.0" operates on the git
tree: Phase 3.1 expects exactly "19 XML + 1 JSON = 20" goFSH inputs (line 473) — the packaged
example is not among them, so a migration presented as faithful-to-2026.0.0 silently drops one
published example. No decision row assigns its disposition (D-9 and D-13 cover other content
dispositions; this one is skipped), and no verifier net catches it: C1 conservation is keyed on
`--source` = the pinned git tree (recon/skills.md §e), and prepost-delta compares the same
preflight. The skill's shape-B doctrine requires every narrative/content item to carry "a
recorded disposition" — this artifact-of-record has none.

**Fix:** add a decision (owner): include the registry-only example (extract from the tarball
into the migration) or record its exclusion explicitly, and add it to the Gate-A completeness
checklist either way.

## RISK-5 · MAJOR — QA-baseline method left as an undecided "OR", with a non-comparable option and no provenance home

Phase 1.2 (lines 454-458): "Assemble a throwaway ig.ini+IG-resource wrapper ... OR validate the
published 2026.0.0 tarball with the pinned validator". Defects:

1. **Undecided:** no D-row, no owner, no criterion picks between the two — yet Phase 9.2's
   acceptance ("qa errors ⊆ the source-baseline classes proven at 1.2", lines 580-581) depends
   entirely on which was chosen.
2. **The second option is non-comparable:** Phase 9's QA comes from IG Publisher 2.3.2 qa output;
   `validator_cli` over a tarball produces a different error universe (no link checking, no
   publisher pipeline, different message classes), so "⊆ the baseline classes" becomes
   ill-defined. The cited PROs-try-run technique (line 458) was publisher-vs-publisher
   ("QA baseline via hl7fhir/ig-publisher-base docker ... compared by element path" — user
   MEMORY), and the skill's own qa_baseline row says "build the unmigrated source or fetch its
   rendered qa" (recon/migration-spec-v0250.md:2093) — a validator-over-tarball baseline is a
   plan-invented third path.
3. **No provenance home:** the wrapper is "outside the migration tree, never committed" — correct
   for the wrapper, but the plan never says where the resulting error census and the wrapper
   config land (migration-log/? scratchpad?), leaving the Gate-D acceptance basis unreproducible
   (and, per RISK-2, likely deleted).

**Fix:** commit to the publisher-in-Docker wrapper build as the baseline method (same tool +
pin as Phase 9), record the census + wrapper config into `migration-log/`, and keep the
validator-tarball route only as a cross-check.

## RISK-6 · MINOR — Sandbox mirror-update instruction is incoherent under the recommended baseline

Phase 0.2 (lines 427-431): sandbox default branch `develop` is "a stale source mirror ... update
the mirror to the pinned baseline FIRST". Under the D-2 recommendation the pinned baseline is tag
2026.0.0 = `792f9f3e` — MEASURED in the source clone: `git merge-base --is-ancestor 792f9f3e
origin/develop` → NOT an ancestor (develop diverged; 18 commits, separate line). Pointing the
develop-mirror branch at the tag is therefore a non-fast-forward rewrite that replaces
develop-line content with master-line content — breaking exactly the "mirror semantics" the
plan's own R14 (line 629) defends. A mirror update should move `develop` to the source develop
tip (`744f7ab`); the BASELINE pin belongs on the migration branch, not the mirror.

**Fix:** reword 0.2 to "update the develop mirror to the source develop tip; cut the migration
branch from the D-2 baseline commit".

## RISK-7 · MINOR — Identifier collision and unglossed skill jargon degrade 3-week readability

The plan's risk table uses ids R1-R16 (§5) while the verifier's check codes R1-R5 appear in the
same document with entirely different meanings: line 181 "C5c and R4 downgrade to NICHT PRÜFBAR"
(verifier R4 = template-example links) vs table R4 = "Narrative single point of failure";
line 599 "P1/P3, R1–R5, C2 return NICHT PRÜFBAR" (verifier codes) vs §8 "Consent R1/R2" (risk
ids). A reader three weeks out cannot tell which R4 is meant without re-deriving the skill's
code table. Additionally the plan uses ①/② queues, L1-L4, F2/F3, tier P/R/G, M1-M11, C5c, P1-P4
throughout without any legend — all defined only in `recon/skills.md`/the skill spec (which,
per RISK-2, may no longer exist when the plan is read).

**Fix:** rename the plan's risks (e.g. RISK-1..16) and add a 10-line legend block for the skill's
check/queue codes.

---

Checks attacked and PASSED (not findings): stale-sandbox reuse (fresh branch + supersede PR #3 +
evidence-only carry — handled, lines 24-31/425-427); licence-contradiction path (D-1 with owner
sign-off + tier evidence — handled); D-2 moving-target handling (re-measure fingerprint,
lines 103-106); page-map overwrite sequencing (R11); DE-first 3-file CI patch as plan-level work
(matches recon/template.md §c exactly); verifier flag set incl. --template-latest axis and the
absent --source-guide-url (matches recon/skills.md §e); expected-steps ledger count (31 minus
5.1c — matches recon/skills.md §a); M1-M7 pass simulation and bare-canonical zero-edit claim
(recon/template.md §b); parent-snapshot D-4 option set and cache-name==pin rule (recon spec
§5.1b.5); link census figures (hl7.org 66 = 63+3, ig.fhir.de 34 — recon/guide.md §g.5).
