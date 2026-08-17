# Ground truth — pinned facts for the tariff paper

Every number a draft uses comes from here. Source classes: **[read]** =
artifact read or produced in the 2026-08-07 session (file/commit named);
**[posted]** = published today by this campaign (URL named); **[recall]**
= campaign memory — carries `[NEEDS VERIFICATION]` until the research
lane confirms against the primary artifact.

## The conformance result (Axiom leg)

- us-tariff-yale **conformant TRUE on main**, closed 2026-08-03: 10/10
  policies covered (100%), unexplained 0, axiom_attributed_open 0,
  invalid_exclusions [], 4 tripwired exclusions, oracle_attributed 8,283
  classified, temporal debt 48,000 pre-domain + 1,200 straddle-clipped
  intervals surfaced non-blocking. Snapshot pin: axiom-oracles #452 @
  `dc1da3af`. [read: _tariff-parity/CAMPAIGN.md close block]
- Policy-record conformance predicate: the count of in-scope policy records
  with `covered: true` equals the count of in-scope policy records, and
  `unexplained == 0 && axiom_attributed_open == 0`; this `covered` field is not
  the 20,400 covered-interval-cell term used by the tariff report. The universe
  is generated from the oracle's own spine. [read:
  project_axiom_certification_stack.md]
- Scope (CORRECTED per the dc1da3af detail file): 10 covered policy
  constructs — MFN column rate, §232 (aluminum in the composition),
  §301 China + Brazil + forced-labor, IEEPA (fentanyl+reciprocal as
  one combined slot), §122, §201, §338, total — at the reference's
  default legal-date mode; 4 excluded:technical with tripwires (other,
  rate_301_cs, stacking_outputs, swiss_framework). Estimation layer
  (metal_share, USMCA utilization, exemption shares, effective
  constructs) out of scope entirely. [read: detail file @ dc1da3af]
- Reference vintage: Yale tariff-rate-tracker commit `c4307e51`; their
  full R build measured locally: 6368.27 s real (1 h 46 m), peak memory
  footprint 132,526,069,168 bytes (123.4 GiB), maximum RSS
  89,850,789,888 bytes (83.7 GiB). [read:
  ~/TheAxiomFoundation/_tariff-yale/build-timing.log; two failed
  attempts preserved as .locale-fail and .stale-gate variants]. Panel
  rate_timeseries.rds = 1,929,830,536 bytes (1.93 GB). [read: local file]
- Corpus grounding: 138 signed corpus versions ingested for the
  campaign (47 FR instruments + 44 HTS revision snapshots + 47 chapter-99
  /US-note extractions). [read: CAMPAIGN.md cycle-3 block]
- Adversarial arc on the harness: sol rounds r2→r7 to APPROVE; battery
  2,396 passing at close; final sweep 0 predicate disagreements across
  220 committed dashboard reports. [read: CAMPAIGN.md]

## Encoding mechanics (verified against code 2026-08-07)

- Rules carry `versions:` lists with `effective_from`; changes append
  dated versions, never edits. No `effective_until` in the overlays;
  supersession by later versions or explicit termination rules.
  [read: rulespec-us us/policies/usitc/us-tariff-duty/overlays/*]
- Terminations are encoded law: `overlays/ieepa/termination.yaml`
  encodes EO 14389 — `terminated_ieepa_additional_ad_valorem_duty_rate
  = 0` effective 2026-02-20, proof atom excerpt "shall no longer be in
  effect", corpus citation `us/rulemaking/federal-register/2026-02-25/
  2026-03832`. Companion test evaluates the one-day period ON
  2026-02-20. [read: termination.yaml + termination.test.yaml]
- Every version carries proof atoms citing corpus paths
  (`us/statute/hts/9903.01.25`-style) with verbatim excerpts.
  [read: reciprocal-baseline-9903-01-25.yaml]
- HTS revision consolidations are their own dated modules
  (e.g. section-232-aluminum/rev12-consolidation.yaml). [read: ls of
  overlays/section-232-aluminum/]
- Composed spine: `us:policies/cbp/us-tariff-duty/composition`, imports
  line modules + per-authority overlays (IEEPA fentanyl ×4, reciprocal
  per-country modules, §122, §232-aluminum incl. RU 200%, §301 families).
  [read: composition.yaml imports block]
- **No five-line domain guard at `dbf09f44`.** The composition defines five
  exact-line predicates but never requires their disjunction. For an unsupported
  line, `mfn_ad_valorem_rate` falls through to `else: 0`; during
  2026-02-24 through 2026-07-23, `section_122_component_rate` falls through to
  the blanket 10 percent rate; the total adds these components. Off-slice calls
  can therefore return plausible rates rather than errors. All paper inference
  is caller-restricted to the five lines; a fail-closed guard and negative tests
  are an Axiom-side archival prerequisite. [read: composition.yaml lines
  691–799, 2214–2282, 2945–2996, 3804–3821 @ `dbf09f44`]
- Engine operational semantics at `ffd82132`: version bounds are inclusive and
  selected at the query period's start; the applicable version with greatest
  `effective_from` wins, gaps error, and same-start overlap precedence is not a
  legal semantic to rely on. Formula branch order carries precedence; stacking
  is explicit component addition; declared scalar/judgment types and missing
  inputs/versions produce runtime errors. The composed output is a `Rate`, not a
  duty amount. [read: engine docs/rulespec.md, src/model.rs, src/engine.rs]

## Legal timeline (the "why 2026" hook) — ALL [verified 2026-08-07, research/verification-report.md]

- IEEPA: Learning Resources, Inc. v. Trump, 607 U.S. 229 (2026),
  No. 24-1287 (with No. 25-250), decided 2026-02-20; holding (syllabus,
  verbatim): "IEEPA does not authorize the President to impose
  tariffs." EO 14389 ("Ending Certain Tariff Actions", 91 FR 9437,
  doc 2026-03832) signed the SAME DAY: duties "shall no longer be in
  effect and, as soon as practicable, shall no longer be collected" —
  NO date in the order's text for collection. The 2026-02-24 00:00 ET
  collection cutoff was set operationally by CBP CSMS # 67834313
  (issued 2026-02-22). EO 14388 = the de minimis CONTINUATION order
  (91 FR 9433), NOT the collection end — never cite it for that.
- §122: Proclamation 11012 (91 FR 9339), 10% surcharge on all imports
  (annex exceptions; not stacked on §232), effective 2026-02-24
  00:01 EST through 2026-07-24 00:01 EDT — exactly the 150-day
  statutory maximum of 19 U.S.C. § 2132(a) (which caps at 15%). Ran to
  scheduled expiry (no modifying FR instrument through 2026-08-07).
- Forced-labor §301: 91 FR 47318 (doc 2026-15181, USTR, pub.
  2026-07-28): 60 investigations determined actionable; rates 10%
  (prohibition/agreement economies) / 12.5% (others); TRQs for four;
  Annex I inserts chapter-99 U.S. note 52 (headings 9903.05.85–
  9903.06.21); effective 2026-07-24 — THE SAME DAY the §122 surcharge
  expired (verified seam).
- HTS 2026: Revision 15 dated 2026-08-03 (Rev 14 was 2026-07-31).
  Rev 15's sole change: heading 9903.04.63 (UK PATENTED pharmaceutical
  articles) +10% → +0% per 91 FR 49406 implementing Proclamation 11020;
  context rates: 9903.04.60 general pharma 100%, 9903.04.62
  EU/JP/KR/CH/LI 15%.
- §201 solar: Proclamation 10339 (87 FR 7357) Annex I staged table
  verbatim: 14.75% / 14.5% / 14.25% / 14% for the four years ending
  2026-02-06; current HTS marks note 18 EXPIRED. Yale's flat 14.5% past
  the end is therefore wrong on two axes (stale stage since 2024-02-07;
  nonzero past expiry). Later Procs 10779/10790 changed TRQ/coverage,
  not the terminal date.
- GN 3(b) verbatim (HTS 2026 Rev 15): column-2 rates apply to products
  "of the following countries and areas": Republic of Belarus, Cuba,
  North Korea, Russian Federation (footnote cross-references note 30 /
  9903.90.08 additional duties).
- Yale tracker: MIT license, org Budget-Lab-Yale, commit c4307e51
  reachable upstream (2026-07-24, ancestor of master); companion Budget
  Lab post "Introducing the Tariff Rate Tracker" (2026-04-01).

## Yale tracker defects (reported upstream, unacknowledged)

All six filings verified open with 0 maintainer comments as of
2026-08-07 [read: gh api this session]:
- #23 + PR #24 — non-UTF-8 locale corruption + fix.
- #25 — measured build envelope vs documented 32 GB guidance.
- #26 — proposal: publish the line-level panel as a release artifact.
- #27 — §201 solar flat 14.5% carried past Proclamation 10339's staged
  table end (2026-02-06). Independent derivation recorded in
  axiom-oracles `conformance/detail/us-tariff-yale.json` (Proclamation
  10339 referenced; snapshot report
  `reports/axiom-yale-us-tariff-panel-all-2026-08-03.json`). [read:
  oracles main @ 7085600b greps]
- #28 — no GN3(b)/column-2 branch: CU/KP/BY/RU carry column-1 base
  rates. Column-2 disposition recorded in the same detail file (×2
  mentions). Statutory derivation verified: GN 3(b) verbatim above.

## Prohibitions (never appear in any draft)

- "Nonprofit" as Axiom's descriptor; the org is "The Axiom Foundation."
- Thesis (the org concept) — never in public artifacts.
- "Certified"/"certification" for the internal sol review — it is
  independent adversarial cross-model review; external certification
  (notary pattern) is future work.
- "Confirmed by Yale" or any maintainer-acceptance implication for
  #27/#28 — they are reported, derivation-backed, unacknowledged.
- Lowercase product names in prose (Microcosm, PolicyEngine, Chronicle,
  RuleSpec); "populace"/"ledger" only as code identifiers.
- Policy advocacy in any direction.
- Unpinned scoreboard numbers (every scoreboard claim carries its
  snapshot SHA).

## Conformance waterfall + pins (extracted from the dc1da3af artifacts, 2026-08-07)

- Universe (per policy, from the -all report): 240 countries; 68,400
  in-scope intervals = 20,400 covered + 48,000 temporal debt;
  comparisons 39,600; raw matches 24,400 (61.6%); raw mismatches
  15,200; error_count 0. Reference panel rows total: 277,303,920.
- Per-policy conformance record (detail file): explained_rate 100,
  unexplained 0, axiom_attributed_open 0, oracle_attributed 8,283
  (cells); dispositions operate per concept-slot (per-concept mismatch
  counts overlap across slots: mfn 594, ieepa 476, s122 4,560, s232
  1,920, s201 7,887; row-level total 15,200).
- Authoritative dispositions at
  `axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:dispositions/us-tariff-panel.yaml`
  are dated 2026-08-03 and partition 15,200 units into 30 entries:
  8,283 `upstream_engine_gap` units (10 entries) plus 6,917
  `explained_residual` units (20 entries). Their MFN footprint is 594 = 528
  column-2 + 66 preference units. The public mirror at the same pin,
  `dashboard/public/data/dispositions/us-tariff-panel.json`, is stale: dated
  2026-08-02, 46 entries, with a 462 MFN footprint (396 + 66). It must be
  regenerated under a synchronization tripwire before archival release.
- 14 policy records: 10 conformant, 4 excluded:technical, IDs:
  us-tariff-yale:{other, rate_301_cs, stacking_outputs,
  swiss_framework}.
- IEEPA note (verbatim from the detail record): fentanyl compared
  jointly with reciprocal via the suite's combined ieepa slot (the
  composition encodes one IEEPA component).
- Full pins: rulespec-us dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df;
  axiom-rules-engine ffd8213271947b0189a9dd61a055c1e0e78908a0 (v0.1.0,
  binary sha256 674ca6e70afdccb59c3d6847933bc24b4590105e49db54790f2dcd0bdbbe32d7);
  axiom-oracles dc1da3af067c50fa7138458faf3703b4b9efd7cb; Yale
  c4307e514196618afcbf88cf7fd33746417eeabf

## Witness-slice disclosure + section 201 mechanism (round-3 verifications, 2026-08-07)

- **The reconciliation universe is a five-line witness slice** (verified
  in the pinned report's scope.covered_lines): 2203.00.0030 (beer),
  7202.11.1000 (ferromanganese), 7601.10.3000 (unwrought aluminum),
  8541.42.0010 (crystalline-silicon solar cells), 9506.62.4040
  (inflatable balls) × 240 partners × 57 intervals = 68,400. Lines were
  chosen as authority witnesses; full-schedule expansion is the
  recorded backlog (campaign T1). ~0.025% of the reference's
  277,303,920-row spine. EVERY reconciliation claim must carry this.
- **Section 201 encoding mechanism at dbf09f44** (composition.yaml
  section_201_component_rate): ONE version, effective_from 2026-02-15,
  formula an explicit zero — with proof atoms quoting the ENTIRE staged
  table (14.75/14.5/14.25/14%, each period's dates) and the schedule's
  expiry compiler's note. Zero by explicit version with the derivation
  in the proof, NOT by absence of a version. The encoded domain begins
  2026-02-15 (post-expiry) temporally; this does not create a spatial guard.
- Temporal debt semantics per artifact: 48,000 pre-domain intervals =
  debt; boundary-straddling intervals are clipped to the covered
  portion (straddle/clip fields present in the report; 1,200 clip
  events recorded).
- **Rate-versus-amount boundary:** the composition supports posted ad valorem
  component-rate stacks under the input date supplied. It does not compute the
  beer column-2 specific duty of 13.2 cents per liter, the beer Section 232
  amount on declared aluminum-content value, quota position, or sub-monthly
  timing.

## Full-schedule generated rate spine (landed 2026-08-10..13; VERIFIED)

- Corpus feedstock: version
  `2026-08-09-usitc-hts-2026-rev15-full-schedule` (axiom-corpus PR
  #595, merge-commit): all 29,845 HTS-numbered rows of the pinned
  Revision 15 snapshot (sha `59a76c12…`) as per-line provisions +
  document root; provision bodies byte-identical to the witness-chapter
  version for all 1,706 overlapping citation paths (reproducer-gated).
  Sol adversarial review, 3 rounds to APPROVE.
- The live USITC API cannot serve vintages: `reststop/exportList`
  accepts and silently ignores `release=` (proven: heading 9903.02.01,
  born April 2025, returned for "2025HTSRev1"). Frozen vintages exist
  ONLY as corpus snapshots.
- Spine: 13,790 rated lines across 98 chapters, emitted as 100
  generated rulespec modules (chapter 99 as three sub-shards: 9901 +
  9902 first half / 9902 second half / 9903–9999). Per-line general and
  column-2 rate tables (ad valorem + Free; Free = 0) and total-partition
  disposition tables: ad_valorem 6,247 / free 5,795 / specific 777 /
  conditional 548 / compound 326 / component 93 / empty 4 (column-2-only
  records). Non-ad-valorem lines carry explicit markers, never silent
  zeros.
- Grounding: per-cell proof atoms citing `us/statute/hts/<htsno>` with
  verbatim body-line excerpts (48,479 atoms; full-batch proof validation
  196/196 under the pinned toolchain; full validate battery (compile +
  companion tests + grounding) 98/98 locally before landing.
- Gates: witness identity (generated cells reproduce the 3 hand-built
  witness modules' encoded rates exactly; expectations parsed from
  those YAMLs, never memory); double-emit determinism; window
  stability (0 general-column diffs on 11,504 common base lines,
  2025-basic ↔ 2026-rev15; the single column-2 diff is USITC's own
  source-text repair on 2909.19.18.00, caught as `conditional` by the
  partition, not force-parsed).
- Membership: 19,948/19,949 ten-digit statistical lines map to their
  rate-bearing ancestor (1 unowned: 9802.00.91.00, ch-98 special
  regime). The hts10→rate-line map ships as a generated DATA artifact
  (spine.json), deliberately NOT as a statutory parameter table — its
  synthetic integer keys are not groundable in provision text.
- Applied per-entry duty is a declared deferred output on every module
  (composition-layer work); the five-line witness composition is
  UNCHANGED in this revision — the spine publishes statutory rate
  TABLES at full schedule, not full-schedule duty computation.
- Landed as rulespec-us PRs #1267 (ch 01–25), #1275 (26–50), #1276
  (51–75), #1280 (76–89), #1284 (90–98), #1286/#1287/#1288 (chapter 99
  sub-shards a/b/c; #1288 MERGED 2026-08-13, spine-completing merge
  `f062088fb` — all 13,790 lines on main, reproducer --check green
  over the complete 200-file set). Each PR: subset manifests via
  `sign-applied-files --manual-exception rulespec-us#1190`
  (deterministic-generator provenance class), append-only
  oracle-coverage ledger entries, regenerated reverse index.
- CI-scale facts for §7-class claims: the us-shard validate leg under
  the production (unindexed) resolver costs roughly 6–10 s per cited
  path; single PRs exceeding ~3,000 cited lines hit GitHub's 6-hour
  job cap (observed thrice). A resolver memoization (60+ min →
  27.5 s per module locally; sol-reviewed to APPROVE over 3 rounds) is
  structurally unpinnable until the repo's strict toolchain cutover
  (encode pins must live on encode main; encode main requires bound
  releases the repo cannot yet bind).
