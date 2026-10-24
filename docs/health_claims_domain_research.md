# Indian Health Insurance Claims + GenAI — Domain Research

**Prepared for:** Prashanth Kumar Kadasi — interview at ICICI Lombard (Mumbai), "Product Owner: Health Claims Automation and Generative AI", interview invite says "Agentic AI".
**Prepared:** 13 Oct 2026.
**Purpose:** get to Indian health-claims fluency fast. Ground truth about the candidate is `config/profile.md`; nothing about him is invented here.

## How to read the tags

| Tag | Meaning |
|---|---|
| **VERIFIED** | The claim was read on the page at the cited URL in this session. |
| **WEAK** | Secondary coverage, partial text, or a source whose own citation is unreliable. Use with hedging. |
| **UNVERIFIED** | Could not source. Stated as "could not confirm". **Do not say it in the interview as fact.** |
| **INFERRED** | My reasoning or industry-general knowledge, explicitly not a sourced fact. |

**Source-access limitations in this session (important, and honest to disclose if asked):**
`irdai.gov.in` resolves to a non-public IP and could not be fetched. `business-standard.com` likewise. `icicilombard.com` was previously recorded as 403 in this workspace and was not retried. Long article pages on `expresscomputer.in` and `taxguru.in` returned mostly navigation boilerplate, so **article bodies for those two hosts could not be read**; only their headlines, dates, and search-result snippets were visible. Where that is the case it is marked.

**Primary source obtained (the anchor for Section D):** IRDAI Master Circular on Health Insurance Business, ref **IRDAI/HLT/CIR/PRO/84/5/2024**, dated **29.05.2024**, reproduced in full at [taxguru.in](https://taxguru.in/corporate-law/master-circular-irdai-insurance-productsregulations-2024health-insurance.html) — **VERIFIED**. Issued under s.14(2)(e) IRDAI Act 1999 and s.34 Insurance Act 1938 read with Regulation 7 of Schedule-III of the IRDAI (Insurance Products) Regulations 2024; signed Ramana Rao A, Chief General Manager; repeals 55 earlier circulars.

---

# A. Health-claims glossary — 30 terms

Indian usage first. Where Indian usage diverges from the US payer terminology the candidate already knows, that is flagged **⚑ US-DIFF** — this is the highest-value contrast for him.

| # | Term | Precise meaning |
|---|---|---|
| 1 | **Cashless settlement** | The insurer/TPA pays the network hospital directly; the policyholder pays only non-covered items. **⚑ US-DIFF:** roughly "direct billing to a network provider" — but in India it is gated by a *pre-authorization* decision made *during* the admission, not a retrospective claim. |
| 2 | **Reimbursement claim** | The policyholder pays the hospital and later claims from the insurer. The Master Circular states insurers must "strive to achieve 100% cashless claim settlement" and keep reimbursement "at bare minimum and only in exceptional circumstances" — **VERIFIED** ([source](https://taxguru.in/corporate-law/master-circular-irdai-insurance-productsregulations-2024health-insurance.html)). |
| 3 | **Pre-authorization (pre-auth)** | The hospital, on the patient's behalf, requests the insurer's approval of an expected treatment and cost *before or at the start of* admission. The insurer must decide "immediately but not more than **one hour**" from receipt — **VERIFIED** (same circular). **⚑ US-DIFF:** in the US, prior authorization is usually initiated by the provider for a scheduled service; in India the pre-auth form is a standard hospital–TPA artefact and is the single most automation-relevant decision point. |
| 4 | **Final authorization / discharge authorization** | Approval of the final bill at discharge. The insurer must grant it within **three hours** of the hospital's discharge request; delays beyond three hours mean any extra hospital charge is borne by the insurer **from shareholders' fund** — **VERIFIED** (same circular). This is a hard, machine-checkable SLA and the strongest argument for STP in cashless. |
| 5 | **TPA (Third-Party Administrator)** | A licensed intermediary that administers claims, the hospital network, and pre-auth on the insurer's behalf. **⚑ US-DIFF:** the US TPA concept is self-funded-employer claims administration; the Indian TPA is an IRDAI-licensed health-services entity inside the insurer–hospital triangle. The Master Circular requires insurers to monitor TPA performance and to pay TPAs only on full satisfactory service, with clawback passed to policyholders — **VERIFIED** (same circular). |
| 6 | **Insurer–TPA–hospital triangle** | The insurer owns the risk and the money; the TPA runs pre-auth, network and claim processing; the hospital delivers care and raises the bill. The policyholder sits outside the data flow — the circular says insurers/TPAs must collect documents **from hospitals**, and "policyholder shall not be required to submit the documents" — **VERIFIED** (same circular). **Automation consequence:** the primary document sources are hospital systems and TPA portals, not customer uploads. |
| 7 | **Network hospital** | A hospital empanelled by the insurer/TPA for cashless. Non-network means reimbursement only. Insurers must display the empanelled list on their website — **VERIFIED** (same circular). |
| 8 | **Medical scrutiny / medical audit** | A clinician (insurer or TPA medical officer) reviews the clinical documents against the diagnosis, the proposed line of treatment, and medical necessity. **⚑ US-DIFF:** the nearest US analogue is a utilization-review / medical-necessity review by a clinician reviewer. |
| 9 | **Adjudication** | The determination of payable amount and liability: apply policy terms (sub-limits, deductibles, co-pay, waiting periods, exclusions) to the admitted claim. **⚑ US-DIFF:** US "adjudication" is largely a rules-engine/EDI process (837/835); Indian health adjudication is document- and clinician-heavy because the input is a hospital bill, not a coded claim. |
| 10 | **Repudiation** | Formal rejection of the claim. **Indian-specific control:** "No claim shall be repudiated without the approval of PMC or a three-member sub-group of PMC called the **Claims Review Committee (CRC)**" — **VERIFIED** (same circular). **This is the single most important governance fact for an automation programme:** a repudiation is not an individual's decision, it is a committee decision. |
| 11 | **Partial disallowance** | Part of the claim paid, part rejected (e.g. non-payable consumables, room-rent excess). Where a claim "is repudiated or disallowed partially", full details must be conveyed "giving reference to the specific terms and conditions of the policy document" — **VERIFIED** (same circular). |
| 12 | **Settlement** | Payment of the admitted amount, and closure of the claim. Settlement is a *financial* event; adjudication is the *decision* event. Confusing the two is a common PO mistake. |
| 13 | **Co-payment** | A fixed percentage of the admissible claim the policyholder bears. Listed in the Customer Information Sheet as a core policy feature — the CIS covers "coverage details, exclusions, sub-limits, deductibles, and waiting periods" — **VERIFIED** (same circular). |
| 14 | **Deductible** | A specified amount up to which the insurer pays nothing; deducted from the claim if the claim exceeds it (the circular's own definition) — **VERIFIED** (same circular). |
| 15 | **Sub-limit** | "A pre-defined limit above which insurance company will not pay" (the circular's own words) — **VERIFIED** (same circular). E.g. a cap on room rent or on a specific procedure. **⚑ US-DIFF:** the US analogue is a benefit maximum or a visit/day limit, but Indian sub-limits are commonly expressed as *room-rent-category-linked* limits, which cascade into proportional deduction of other charges — a notorious source of customer disputes. |
| 16 | **Room-rent limit** | A sub-limit on daily room charges, usually expressed as a % of sum insured or a rupee cap. **⚑ US-DIFF:** no direct US payer analogue in the same form; in India breaching it commonly triggers *proportionate deduction* across associated charges, which is the classic "why was my claim cut?" complaint. |
| 17 | **Waiting period** | "Time period during which specified diseases/treatments are not covered" (the circular's own definition) — **VERIFIED** (same circular). Distinct from the PED waiting period. |
| 18 | **Pre-Existing Disease (PED)** | A condition existing before cover, subject to a declared waiting period. The circular requires products catering to "pre-existing diseases and chronic conditions" and requires that PED waiting-period credits survive migration and portability — **VERIFIED** (same circular). |
| 19 | **Moratorium period** | The period after which the policy and claim **cannot be contested** on grounds of non-disclosure or misrepresentation, except for established fraud. The circular fixes it at **60 months of continuous coverage**, and says credits accrued under ported/migrated policies count towards it — **VERIFIED** (same circular). **This is a legal-immunity clock and must be a first-class field in any automation.** |
| 20 | **Claim intimation** | The first notice of a claim (call, app, portal, hospital, or TPA). It starts the clock and creates the claim ID. |
| 21 | **Discharge summary** | The hospital's clinical narrative at discharge: admission/discharge dates, diagnosis, procedures, course of treatment, follow-up. The single richest unstructured document in the claim, and the main IDP target. |
| 22 | **ICD-10 / medical coding** | ICD-10 is the WHO's 10th revision of the International Classification of Diseases, endorsed by the 43rd World Health Assembly in 1990, effective 1 Jan 1993, with over 14,000 codes, and replaced by ICD-11 on 1 Jan 2022 — **VERIFIED** ([Wikipedia: ICD-10](https://en.wikipedia.org/wiki/ICD-10)). **⚑ US-DIFF:** India does **not** run a CPT/HCPCS-driven claim like US professional billing; Indian hospital bills are line-item invoices mapped to package/procedure descriptions. Mapping bill line items to policy coverage, not to CPT, is the core rule-engine problem. |
| 23 | **Cashless denial reason** | The coded reason a pre-auth or final auth is refused (e.g. not a covered treatment, waiting period active, non-payable item, insufficient documents, non-network). It must be explainable — see #10 and #11 for the repudiation/partial-disallowance communication duty. |
| 24 | **Claim TAT** | Turnaround time from a defined start (intimation, or receipt of last necessary document) to a defined end (pre-auth decision, final auth, or settlement). **The definition must be pinned in the BRD** — a TAT metric with an ambiguous start point is unfalsifiable. Regulatory anchors exist for pre-auth (1 hour) and final auth (3 hours) — **VERIFIED**; the settlement TAT is governed by the Protection of Policyholders' Interests Regulations 2024, whose text **could not be confirmed** in this session. |
| 25 | **NCB (No Claim Bonus)** | Reward for a claim-free year, at the policyholder's express choice of either **cumulative bonus** (sum insured increase without premium increase) and/or a **renewal premium discount** — **VERIFIED** (same circular). |
| 26 | **Portability** | Moving a policy between insurers while carrying credits. Timelines: the existing insurer must give information via the **Insurance Information Bureau of India (IIB, iib.gov.in)** portal "immediately but not more than **72 hours**" of request; the acquiring insurer must decide and communicate within **5 days** of receiving that information — **VERIFIED** (same circular). **⚑ US-DIFF:** not analogous to US HIPAA portability; this is credit-carrying between insurers, like a no-claims/NCB transfer. |
| 27 | **Migration** | Moving between products **within the same insurer**, carrying sum insured, NCB, specific waiting periods, PED waiting period and moratorium credits — **VERIFIED** (same circular). |
| 28 | **Grievance redressal** | The insurer's internal complaint mechanism. The insurer's response letter **must include the contact details of the concerned Insurance Ombudsman** for escalation — **VERIFIED** (same circular). |
| 29 | **Ombudsman** | The external escalation forum for a dissatisfied policyholder. If the insurer does not honour an Ombudsman award within **30 days** of receipt, a penalty of **₹5,000 per day** is payable to the complainant, in addition to penal interest under The Insurance Ombudsman Rules, 2017 — **VERIFIED** (same circular). The Ombudsman's monetary award ceiling **could not be confirmed** in this session (**UNVERIFIED**). |
| 30 | **Customer Information Sheet (CIS)** | A one-place, plain-language summary given with every policy (individual and group member), covering type, sum insured, coverage, summary of exclusions, **sub-limits, deductibles, waiting periods**, plus free-look, renewal, migration, portability and **moratorium period**, and containing claims procedure and grievance-redressal contacts — **VERIFIED** (same circular). **Automation consequence:** the CIS is the authoritative, customer-facing statement of the very fields your rule engine reads. |

### The four contrasts most worth saying out loud in the interview

1. **India is document-first, the US is code-first.** A US claim arrives as a coded EDI transaction; an Indian health claim arrives as a hospital bill plus discharge summary. That is precisely why IDP/OCR and LLM extraction matter more here than in US adjudication.
2. **Repudiation is a committee act, not a system outcome.** The CRC requirement (**VERIFIED**) means "auto-decline" cannot mean "the model said no". Any honest architecture routes decline *recommendations* to a human body.
3. **The regulator has already legislated sub-hour SLAs** on cashless pre-auth and final auth (**VERIFIED**). Automation is not a cost play here first — it is a compliance play first.
4. **The moratorium clock (60 months, VERIFIED)** is a hard legal state variable. Systems that treat it as a date field rather than a governed entitlement will produce contestable denials.

---

# B. Claims lifecycle end to end

Two distinct pipelines run through one organisation: **cashless** (real-time, SLA-bound, TPA-mediated) and **reimbursement** (retrospective, document-heavy, customer-mediated). Everything below applies to both; the differences are called out.

### B.1 Stage table

| # | Stage | What happens | Who does it | Common manual-intervention / failure points | Data generated |
|---|---|---|---|---|---|
| 1 | **Intimation & registration** | Claim is reported (hospital desk, call centre, app, portal, agent, TPA). Identity, policy, and event are matched; a claim ID is issued. | TPA front office / insurer call centre / hospital insurance desk | Policy not found or wrong policy variant; group vs retail mismatch; duplicate claim created for the same admission; **intimation clock start point recorded inconsistently** | Claim ID, intimation timestamp & channel, policy/member key, hospital ID, admission type (planned/emergency), provisional diagnosis |
| 2 | **Document collection & verification** | Documents gathered — for cashless, by the insurer/TPA **from the hospital**, not the customer (**VERIFIED**, Master Circular); for reimbursement, from the customer. Completeness and legibility checked; identity and policy eligibility verified. | TPA back office; insurer ops | Illegible scans and photographs; missing discharge summary or investigation reports; **multiple reminder cycles**; hospital-specific form variants; name/age mismatch between bill and policy | Document manifest, per-document receipt timestamps, deficiency codes, reminder/query log, first/last-document dates |
| 3 | **Medical scrutiny** | A clinician reviews diagnosis, line of treatment, medical necessity, and consistency between the bill and the clinical record. | TPA medical officer, then insurer medical officer for escalated/high-value cases | Queue build-up at peak hours; specialist opinion needed but not available in-shift; **opinion variance between reviewers**; query raised to hospital and then stalled waiting for a reply | Reviewer ID, review timestamp, clinical query text, hospital response, necessity opinion, specialty referral |
| 4 | **Adjudication** | Policy terms applied to the admitted amount: sum insured and remaining balance, sub-limits, room-rent limit and proportionate deduction, co-pay, deductible, waiting periods, PED, exclusions, NCB, moratorium status, other policies in force. | Adjudication desk / rules engine + human for exceptions | **Rules ambiguity on non-payable consumables**; proportionate-deduction arithmetic; multiple-policy coordination; wrong waiting-period start date; manual lookups of policy wording | Admissible amount, deduction line items with reason codes, rule version applied, benefit balances consumed, calculation audit trail |
| 5 | **Approval / repudiation / partial disallowance** | Decision on liability. Repudiation requires **Claims Review Committee (PMC or a three-member sub-group of PMC) approval** — **VERIFIED**. Partial disallowance must be communicated with reference to specific policy terms — **VERIFIED**. | CRC for repudiation; delegated authority for approvals within limits | **Committee throughput becomes the bottleneck for declines**; reason codes too coarse to explain; decision not traceable to the policy clause; escalation limits unclear | Decision, decision-maker/committee ID, reason code(s), clause reference, authority limit used, decision timestamp |
| 6 | **Settlement** | Cashless: final authorization to hospital within **3 hours** of discharge request, with delay cost borne by insurer from shareholders' fund — **VERIFIED**. Reimbursement: payment to the policyholder's bank account. | Finance/payment ops, TPA for cashless | Bank-detail errors and re-issues; NEFT/UPI batch cut-offs; hospital billing revisions after final auth; **interest exposure if settlement SLA breached** | Payment reference, amount, mode, payee, settlement timestamp, TAT actuals, interest paid (if any) |
| 7 | **Closure, records & grievance** | Claim file closed; documents archived; any grievance routed internally, with the Ombudsman's contact in the response letter — **VERIFIED**; Ombudsman award non-implementation attracts **₹5,000/day** — **VERIFIED**. | Ops + grievance cell + compliance | Reopened claims; grievance not linked back to the original decision; **no feedback loop from grievance outcome into rules** | Closure code, archival reference, grievance ID, grievance category, resolution time, award compliance status |

### B.2 Decision points a Product Owner must define

Each of these is a place where the process either branches or stops, and each needs an explicit owner, input set, output, and SLA.

1. **Is the policy in force and is the member eligible on the admission date?** (deterministic)
2. **Is the hospital in network for cashless, or is this reimbursement?** (deterministic)
3. **Is the admission within a waiting period — initial, specific-disease, or PED?** (deterministic against declared dates; the *fact pattern* may need extraction)
4. **Is the moratorium (60 months continuous coverage) complete, and therefore is contestability barred except for established fraud?** (deterministic — **VERIFIED** rule)
5. **Is the proposed treatment medically necessary and consistent with the documented diagnosis?** (clinical judgement — human, or LLM-assisted with human sign-off)
6. **Is the treatment/procedure covered by this product, and is it in the exclusion list or CIS summary of exclusions?** (deterministic on a curated coverage table; retrieval-assisted on wording)
7. **Does the amount breach a sub-limit, room-rent limit, co-pay, or deductible?** (deterministic arithmetic)
8. **Are there other policies in force, and who is primary?** (deterministic; the chosen policy's insurer must coordinate settlement of the balance — **VERIFIED**)
9. **Are fraud indicators present at a level that changes the path?** (scoring — human confirmation required)
10. **Does the decision amount exceed the delegated authority of the automated path?** (deterministic threshold)
11. **Is this a repudiation?** → **must go to CRC** (**VERIFIED**). No automation may bypass this.
12. **Has the required communication (reason + specific policy terms) been generated and evidenced as sent?** (deterministic control)

### B.3 Escalation triggers

| Trigger | Why it escalates | Escalates to |
|---|---|---|
| Sum insured / claim amount above threshold | Financial materiality | Senior adjudicator → CRC for decline |
| Diagnosis in a high-variance or high-abuse category | Clinical ambiguity, fraud exposure | Medical officer → specialist reviewer |
| Fraud score above band | Potential misrepresentation | Special investigations unit (SIU) |
| Document set internally inconsistent (dates, diagnosis vs procedure) | Cannot be adjudicated safely | Medical scrutiny, with query to hospital |
| Claim near the pre-auth 1-hour or final-auth 3-hour limit | **Regulatory SLA breach imminent (VERIFIED)** | Ops supervisor / auto-escalation to on-call reviewer |
| Reopened claim, or a grievance on a settled claim | Precedent and regulatory risk | Grievance cell + compliance |
| Ombudsman award received | Legal obligation, **₹5,000/day** on non-implementation (**VERIFIED**) | Compliance / legal |
| Moratorium-complete claim where fraud is alleged | Contestability barred except established fraud (**VERIFIED**) | Legal + CRC |

### B.4 System controls a PO would specify

- **Clock controls:** independent, server-side timers for pre-auth (1 h), final auth (3 h), portability responses (72 h existing insurer / 5 days acquiring insurer), Ombudsman award (30 days). Timers must start from an *evidenced* receipt event, not a user action. *(Timelines VERIFIED; the control design is INFERRED.)*
- **Maker–checker** on any monetary override, deduction, or waiver.
- **CRC gate as a hard system gate:** a repudiation cannot be dispatched without a CRC decision record (**VERIFIED** requirement).
- **Rule-version pinning:** every decision stores the policy wording version and rule-set version used.
- **Immutable decision log** with the inputs, the rule trace, the model/prompt version (if any), the human actor, and the timestamp.
- **Communication control:** block dispatch of a rejection unless it contains the specific policy clause reference and the Ombudsman contact details (**VERIFIED** requirements).
- **Dual control on vendor/model changes**, with a documented regression pack before any prompt, model, or rule change goes live.
- **TPA performance instrumentation** feeding the contractual clawback mechanism (**VERIFIED** that the circular requires monitoring, service-linked payment and clawback).

---

# C. The JD's KPIs, defined precisely

**Sourcing note:** the *definitions* below are standard insurance-operations usage and are marked **INFERRED** unless a source is cited. The one KPI where I found an explicit regulatory remark is **settlement ratio** — see C.2.

### C.1 Claim TAT (turnaround time)
- **Means:** elapsed time from a defined start event to a defined end event. There is no single TAT; there are at least four, and a PO must name them separately: **pre-auth TAT**, **final-authorization TAT**, **settlement TAT** (reimbursement), and **total claim-cycle TAT**.
- **Regulatory anchors (VERIFIED):** pre-auth decision "immediately but not more than one hour"; final authorization within three hours of the discharge request; excess hospital charge for delay beyond three hours borne by the insurer from shareholders' fund. **The reimbursement settlement TAT sits in the IRDAI (Protection of Policyholders' Interests, Operations and Allied Matters of Insurers) Regulations, 2024 — the text could not be confirmed in this session (UNVERIFIED).**
- **What drives it:** document completeness, medical-review queue depth, hospital responsiveness to queries, bank/payment batch cycles, and reviewer availability in shift.
- **What automation typically does:** cuts the *document completeness* and *data-capture* segments hard (IDP), and the *routine adjudication* segment moderately. It does **not** by itself fix hospital query latency or payment batch timing. **INFERRED** — but note the honest corollary: if TAT is already dominated by waiting on the hospital, automation of internal steps yields less than the business case assumes. That is a question worth asking them.

### C.2 Settlement ratio
- **Means:** the proportion of claims settled relative to claims received (or lodged). Commonly quoted by insurers as a marketing metric.
- **Sourced, decision-relevant nuance (VERIFIED):** IRDAI's own health-insurance sub-committee, at its 3rd meeting on 28 Aug 2026, "noted that assessment of claims and grievance outcomes **should not focus solely on settlement ratios but should also consider absolute values**" — [taxguru.in](https://taxguru.in/corporate-law/irdai-health-insurance-committee-advances-customer-trust-nhcx-adoption.html). **Say this in the interview.** It signals you read primary material, and it reframes the metric from a ratio to a volume-and-value view.
- **What drives it:** repudiation policy, waiting-period and disclosure-driven denials, fraud controls, and product design.
- **What automation typically does:** *increases* the settled count through faster processing, but a badly designed auto-decline can *reduce* it while *increasing* grievances. Optimising settlement ratio alone is a known trap — the regulator has effectively said so.

### C.3 Processing accuracy
- **Means:** proportion of claims where the payable amount, deduction codes, and decision are correct on first pass — measured by re-audit against policy terms, not by self-report.
- **What drives it:** rule completeness, policy-wording ambiguity, non-payable-list drift, reviewer variance, and whether the bill was captured correctly.
- **What automation typically does:** improves arithmetic and rule application (deterministic), and can *reduce* accuracy if extraction errors propagate silently. **Therefore accuracy must be measured at the extraction layer separately from the adjudication layer.**

### C.4 Automation rate / STP rate
- **Means:** share of claims (or claim *steps*) that complete with no human touch. Ambiguity is fatal here: "90% automation" is meaningless without saying whether it is by claim count, by value, or by step.
- **What drives it:** proportion of claims that are low-value, clean-document, network, non-PED, within-limits — i.e. the *addressable* share — and the confidence thresholds set for the automated path.
- **What automation typically does:** a well-run programme reports STP by **claim value band**, because a 60% STP rate on small claims and 5% on large ones is a very different business outcome from 60% flat. **A PO should refuse a single blended automation-rate number.**

### C.5 Leakage
- **Means:** value paid that should not have been paid — wrong sub-limit applied, non-payable items paid, duplicate payment, rate/package mismatch, or failure to apply other-policy coordination.
- **What drives it:** rule gaps, non-payable-list staleness, hospital billing practices, and manual override culture.
- **What automation typically does:** leakage detection is one of the *best* justifications for automation, because it is deterministic pattern-matching over structured bill lines. Expect leakage reduction to be the CFO's preferred benefit and TAT improvement to be the COO's.

### C.6 Rework
- **Means:** a claim re-entering a stage it had already completed — re-opened, re-adjudicated, or returned for correction. Measured as rework rate and rework loops per claim.
- **What drives it:** bad first-pass data capture, unresolved hospital queries, and downstream discovery of missing documents.
- **What automation typically does:** reduces rework only if extraction confidence is routed honestly (low confidence → human) rather than forced through. **The failure mode is automating the happy path and dumping all ambiguity into a queue — which raises rework, not lowers it.**

### C.7 Cost per claim
- **Means:** total claims-operations cost ÷ claims processed. Must be split into *touch cost* (per human-touched claim) and *infrastructure cost* (per claim, including model inference and IDP licensing).
- **What drives it:** human minutes per claim, queue depth, and rework.
- **What automation typically does:** reduces touch cost on the automated band, but **adds a per-claim inference/IDP cost on every claim**. The honest business case is on *net* cost per claim and on leakage avoided, not on headcount alone.

### C.8 Customer satisfaction (CSAT / NPS)
- **Means:** post-claim satisfaction, usually surveyed after settlement. For health claims the strongest driver is *predictability of what will be paid* and *speed of discharge*, not raw speed of the back office.
- **What drives it:** clarity of the deduction explanation, cashless experience at the hospital desk, and whether the customer had to chase anything.
- **What automation typically does:** helps most through **explanation generation** (a clear, clause-referenced deduction note) and through hitting the 3-hour discharge SLA — both of which are directly regulation-adjacent (**VERIFIED** timelines). It hurts CSAT sharply if an automated decline is unexplained or perceived as arbitrary.

### C.9 The KPI a PO should add (INFERRED, my recommendation)
**Grievance-to-decision linkage rate** — the share of grievances traced back to a specific decision, rule, or model version, with a corrective action recorded. The regulator's remark that grievance outcomes matter alongside settlement ratios (**VERIFIED**) is the hook for this. It is also the single best defence when a regulator or auditor asks "how do you know your automation is not producing bad denials?"

---

# D. India regulatory constraints on automated claim decisions

### D.1 IRDAI's role
- **VERIFIED** ([Wikipedia: IRDAI](https://en.wikipedia.org/wiki/Insurance_Regulatory_and_Development_Authority_of_India)): statutory body under the Ministry of Finance, constituted by the IRDAI Act 1999; HQ Hyderabad (moved from Delhi in 2001); 10-member body (chairperson, five full-time, four part-time members). **Section 14 functions** include protecting policyholder interests, promoting efficiency in the conduct of insurance business, regulating rates/terms/conditions, regulating margin of solvency, inspecting and investigating insurers, and specifying how books are kept. Chairman as of the article's July 2025 state: Mr. Ajay Seth.
- **Why this matters for automation (INFERRED):** "protecting policyholder interests" plus "promoting efficiency" is the exact tension the role sits in. IRDAI can and does prescribe *process SLAs and decision governance* — so an agentic claims design that cannot evidence its own compliance is not deployable.

### D.2 Claim-settlement and decision-timeline rules — all **VERIFIED** from the Master Circular dated 29.05.2024 ([source](https://taxguru.in/corporate-law/master-circular-irdai-insurance-productsregulations-2024health-insurance.html))

| Rule | Exact provision |
|---|---|
| Cashless pre-auth decision | "Insurer shall decide on the request for cashless authorization **immediately but not more than one hour** of receipt of request." Systems and procedures to be in place "not later than **31st July, 2024**." |
| Pre-auth via digital mode | Insurers "shall also provide **pre-authorization to the policyholder through Digital mode**." |
| Final authorization at discharge | "Insurer shall grant final authorization **within three hours** of the receipt of discharge authorization request from the hospital." |
| Cost of delay | "If there is any delay beyond three hours, the additional amount if any charged by the hospital **shall be borne by the insurer from shareholder's fund**." |
| Death during treatment | Insurer must "immediately process the request for claim settlement" and "get the mortal remains (dead body) released from the hospital immediately." |
| Cashless aspiration | "Every insurer shall **strive to achieve 100% cashless** claim settlement in a time bound manner"; reimbursement "at bare minimum and only in exceptional circumstances." |
| Document collection | "Insurers and Third Party Administrators (TPAs) **shall collect the required documents from the Hospitals**. Policyholder shall not be required to submit the documents." |
| Hospital help desks | Insurers "may arrange for dedicated Help Desks in physical mode at the hospital to deal and assist with the cashless requests." |

### D.3 Policyholder-protection rules on rejection and communication — **VERIFIED** (same circular)

- **No claim shall be repudiated** without the approval of the **PMC or a three-member sub-group of PMC called the Claims Review Committee (CRC)**.
- If a claim "is repudiated or **disallowed partially**, details shall be conveyed to the claimant along with full details giving reference to the **specific terms and conditions of the policy document**."
- The insurer must have a robust grievance-redressal system, and **the response letter in any grievance must include the contact details of the concerned Insurance Ombudsman**.
- **Ombudsman award implementation:** compliance within **30 days** of receipt; failure attracts **₹5,000 per day** payable to the complainant, in addition to penal interest under The Insurance Ombudsman Rules, 2017.
- The circular states that detailed provisions on paras covering CIS, free look, nomination, portability, claim settlement, multiple policies, grievance redressal and Ombudsman awards "will be given in the Master Circular issued under IRDAI (**Protection of Policyholders' Interests, Operations and Allied Matters of Insurers) Regulations, 2024**." **That companion text could not be fetched (UNVERIFIED).**

**Direct design consequence (INFERRED, and worth stating as your opinion):** an "auto-decline agent" is not a permissible primary actor in India. The permissible pattern is **auto-approve within deterministic limits + auto-recommend-decline with a full evidence pack to the CRC + auto-explain every partial disallowance with clause references.** The regulation has, in effect, already written your routing policy.

### D.4 Portability and moratorium constraints (data-automation relevant) — **VERIFIED** (same circular)
- Existing insurer must provide the acquiring insurer's requested information through the **IIB portal within 72 hours** of request; the acquiring insurer must decide and communicate **within 5 days** of receiving it.
- Ported/migrated credits (sum insured, NCB, specific waiting periods, PED waiting period, moratorium period) must be carried forward and **count towards the 60-month moratorium**.
- **INFERRED:** this makes **credit-state portability a hard systems requirement**. Any claims agent that computes waiting periods or moratorium from a single policy record — without ingesting IIB portability history — will compute the wrong answer for exactly the customers most likely to complain.

### D.5 DPDP Act 2023 — **VERIFIED** ([Wikipedia: DPDP Act 2023](https://en.wikipedia.org/wiki/Digital_Personal_Data_Protection_Act,_2023))
- **Act No. 22 of 2023**; passed Lok Sabha 7 Aug 2023, Rajya Sabha 9 Aug 2023, President's assent 11 Aug 2023.
- **Commencement is staggered — this is live and material:** **13 November 2025** for sub-section (2) of section 1, section 2, sections 18–26, sections 35, 38–43 and sub-sections (1) and (3) of section 44; **13 November 2026** for sub-section (9) of section 6 and clause (d) of sub-section (1) of section 27; **13 May 2027** for the remaining provisions.
- Establishes obligations of **Data Fiduciaries**, rights and duties of **Data Principals**, financial penalties for breach, and the **Data Protection Board of India**.
- The Board is "an adjudicating body established under **section 18**" of the Act, adjudicating disputes between data principals and platforms that breached the Act's obligations — **VERIFIED** ([Wikipedia: Data Protection Board of India](https://en.wikipedia.org/wiki/Data_Protection_Board_of_India)).
- **Key structural point vs GDPR (VERIFIED via Wikipedia's comparison, sourced to Latham and HSF):** the DPDP Act applies **only to digital personal data** (GDPR covers all forms), and it **does not distinguish between personal and sensitive personal data** (GDPR does).
- **Could not confirm (UNVERIFIED):** the exact maximum penalty amounts, the specific Rules' provisions on medical/health data, and any health-sector-specific carve-out. **Do not quote a penalty figure.**

**Design consequences for handling medical records (INFERRED):** because the Act does not create a separate "sensitive" tier, *all* claim documents — discharge summaries, bills, prescriptions, IDs — carry the same statutory weight, so a single consent, purpose-limitation and retention discipline must cover the whole claim file. Practical guardrails: consent captured for the specific claims purpose; no PHI in prompts sent to third-party models without a data-processing basis and contractual no-training terms; no PHI in logs or evaluation datasets; retention and deletion schedules that survive audit; breach-notification readiness; and a named Data Protection Officer-equivalent owner. **The compliance question to ask them is whether the GenAI stack is on-prem/VPC-hosted or third-party API — because that single answer changes the entire data-protection design.**

### D.6 Ombudsman route
- **VERIFIED:** exists as the external escalation forum; the insurer's grievance response must carry the Ombudsman's contact details; awards must be honoured within 30 days or ₹5,000/day is payable; penal interest additionally runs under The Insurance Ombudsman Rules, 2017.
- **UNVERIFIED (could not confirm):** the monetary ceiling on an Ombudsman award, the limitation period for filing a complaint, and whether the award is binding on the insurer in the way commonly described. **Ask, don't assert.** A reasonable interview question: *"What's our current Ombudsman volume by claim-decision type, and which of those decisions would an automated path have made differently?"*

### D.7 The age-limit item from the brief — resolution
The brief asked to verify: *IRDAI removed the age limit for buying new health policies effective 01-Apr-2024, previously 65 years.*
- **WEAK.** The statement appears in [Wikipedia: IRDAI](https://en.wikipedia.org/wiki/Insurance_Regulatory_and_Development_Authority_of_India), which cites The Hindu (21 Apr 2024) — but the citation link is to `thehindu.com` and **the underlying article was not fetched in this session**, so this is Wikipedia-level evidence only. The same passage adds, also unsourced at primary level, that IRDAI directed health insurers to develop specialised policies for senior citizens and dedicated grievance and claim channels for them.
- **Recommended handling:** say "IRDAI removed the age bar on buying new health policies from April 2024 — reported by The Hindu" and do not build an argument on it. If pressed for the circular number: **could not confirm**.

### D.8 The NHCX item — genuinely new and worth leading with
- **VERIFIED** ([taxguru.in, IRDAI press release dated 28 Aug 2026](https://taxguru.in/corporate-law/irdai-health-insurance-committee-advances-customer-trust-nhcx-adoption.html)): IRDAI's **IAC Sub-Committee on Health Insurance** held its **3rd meeting on 28 August 2026** (2nd was 17 July 2026). It considered measures to encourage insurers and hospitals to onboard the **National Health Claims Exchange (NHCX)**, "including possible incentives linked to on boarding, payments and faster settlement". It also discussed publishing **Standard Treatment Guidelines (STGs)** and treatment package rates; simplification of policy wording; stronger underwriting at the point of sale to reduce claim disputes from inadequate disclosure; the roles of insurers, intermediaries, agents and TPAs in supporting policyholders at hospitals; hospital certification and Digital Health Standards (presented by NABH chairperson Rizwan Koita); health savings accounts; analysis of ported policies as a separate cohort; and reviewing exclusions in the **Customer Information Sheet**.
- **Committee composition (VERIFIED, same source):** four members — chaired by **Ajay Seth, Chairman IRDAI**; with Deepak Sood (Member, IRDAI), Dr. Indu Bhushan (former CEO, NHA), and Monika Halan. Supported by insurance-sector invitees **Sanjeev Mantri, CEO, ICICI Lombard**; Mayank Bathwal (Aditya Birla Health); K. Ramachandran (Niva Bupa Health). Plus Dr. Soumil Nagpal (World Bank) and Dr. Nishant Jain (ADB) as experts.
- **Honest caveat, stated in the source itself (VERIFIED):** the press release "does not state that the discussed measures have themselves become binding regulatory requirements or prescribe specific implementation dates." **Do not present NHCX incentives as settled rules.**
- **Why this is the single best interview lever:** **the CEO of the company you are interviewing at sits on the IRDAI sub-committee that is steering NHCX onboarding and standardisation.** NHCX is a claims-interoperability rail. An agentic claims system at ICICI Lombard will either consume NHCX or be architected around its absence. **Ask about NHCX readiness explicitly.**

---

# E. Where GenAI genuinely helps, and where it must not be trusted

### E.1 Use cases ranked by honest value

| Use case | Value | Why | Trust posture |
|---|---|---|---|
| **Document classification & routing** | High, immediate | Deciding "this is a discharge summary / a pharmacy bill / an investigation report / a pre-auth form" is a bounded classification task with a large, cheap training signal. | Automate. Log confidence. Low blast radius if wrong — it routes to the wrong queue, it does not deny a claim. |
| **OCR / IDP of hospital bills and discharge summaries** | Highest, foundational | Every downstream step depends on it. Indian hospital bills are heterogeneous, multi-vendor, often photographed. | Automate **with per-field confidence**, and route low-confidence fields to human verification rather than guessing. This is the single most important engineering decision in the programme. |
| **Policy-coverage mapping (which clause covers this line item?)** | High | Retrieval over policy wording + CIS + non-payable list. Genuinely hard for humans at speed and consistency. | **Retrieve and cite; do not decide.** The model returns clause references and candidate coverage; the deterministic engine applies them. |
| **Summarisation for reviewers** | High, low-risk | Compresses a 60-page file into a 10-line brief with citations. Directly attacks reviewer minutes per claim. | Automate, but **always with document-anchored citations** so the reviewer can verify. A summary without citations is a liability. |
| **Communication drafting (deduction explanations, query letters)** | High, and regulation-adjacent | The Master Circular requires clause-referenced explanation of repudiation and partial disallowance (**VERIFIED**). Drafting that well, in plain language, is exactly what LLMs are good at. | Automate drafting; **template the structure and inject clause references deterministically**; require human release for declines. |
| **Fraud-indicator surfacing** | Medium-high | Pattern detection across bill lines, provider, timing, and history. | **Surface, never conclude.** Output is a ranked indicator list for the SIU. "The model accused a customer of fraud" is a reputational and legal event. |
| **Medical-necessity assessment** | Medium, with sharp limits | Genuinely useful as a *consistency check* (does the documented diagnosis support the procedure and length of stay?). | **Assist only.** The final necessity opinion must be a clinician's. This is the boundary that must not be crossed. |

### E.2 Hard limits — stated as constraints, not caveats

1. **Hallucination in clinical decisions.** A model that invents a diagnosis code, a procedure, or a clinical fact produces a denial that cannot be defended. **Mitigation:** extraction must be grounded to document coordinates; clinical reasoning must cite the document and page; no fact may enter adjudication that is not traceable to a source field.
2. **Non-determinism.** The same claim can produce different model output on two runs. **Mitigation:** deterministic rules own every monetary and eligibility outcome; models are confined to extraction, retrieval, summarisation and drafting; and every model call is versioned and logged so a decision can be reproduced.
3. **Explainability.** Indian regulation already requires clause-referenced explanation of partial disallowance and repudiation (**VERIFIED**). A black-box score is non-compliant in effect even if compliant in form. **Mitigation:** the explanation is generated from the rule trace, not from the model's self-report.
4. **Audit trail.** You must be able to reconstruct, months later, what the system saw, what it decided, under which rules and model version, and who approved. **Mitigation:** append-only decision ledger with input hashes, rule-set version, model/prompt version, human actor, and timestamps.
5. **Bias.** Room-rent sub-limits, non-payable consumable lists, and fraud scores can systematically disadvantage particular hospitals, geographies, or customer segments. **Mitigation:** monitor approval and deduction rates by segment, provider and product; treat a statistically significant divergence as a defect with an owner, not a curiosity.
6. **PII/PHI handling.** DPDP obligations attach to all digital personal data with no separate sensitive tier (**VERIFIED** structural point). **Mitigation:** data-minimised prompts, no PHI in logs or eval sets, contractual no-training terms, regional hosting, retention/deletion discipline, and a documented lawful basis.
7. **Liability for a wrong denial.** The insurer owns the decision regardless of which component produced it. The CRC requirement (**VERIFIED**) means the *organisation* is accountable, and a vendor contract does not transfer regulatory liability. **Mitigation:** named human accountability for every decline, and an indemnity/liability position reviewed by legal before go-live.

### E.3 Human-in-the-loop (HITL) and straight-through processing (STP)

- **STP** = a claim completes end-to-end with **no human touch at all**. It is only safe where every input is machine-readable with high confidence and every decision rule is deterministic and within a pre-authorised limit.
- **HITL** = a human is in the decision path. Three distinct flavours, and a PO must name which one they mean:
  - **Human-in-the-loop (approve-before-act):** the system recommends, a human approves, then the action fires. Required for declines and for anything above the value threshold.
  - **Human-on-the-loop (act-then-audit):** the system acts, a human samples and can reverse. Appropriate for auto-approvals within limits.
  - **Human-out-of-the-loop:** only for non-consequential steps (classification, routing, OCR of a low-value claim).
- **What determines which path a claim takes** (this is the routing policy a PO owns — **INFERRED**, but grounded in the VERIFIED constraints):

| Condition | Path |
|---|---|
| All required documents present and extracted above confidence threshold; network hospital; within sum insured and all sub-limits; no waiting period or PED issue; moratorium complete or no contestability question; fraud score in the low band; amount within auto-approval limit | **Auto-approve (STP)** |
| Any of: low extraction confidence; missing document; amount above auto-approval limit; clinical ambiguity; conflicting dates | **Human review (HITL)** |
| Fraud score in the high band | **SIU referral**, claim clock managed and communicated |
| Decision would be a repudiation or a material partial disallowance | **CRC** — **mandatory by regulation (VERIFIED)**; the system's role is to assemble the evidence pack and draft the clause-referenced explanation |
| Contestability question after the 60-month moratorium | **Legal/CRC** — the circular bars contestation except for established fraud (**VERIFIED**) |

---

# F. What an agentic claims system would look like

### F.1 Reference architecture

```
  INTAKE  ──▶  IDP / EXTRACTION  ──▶  NORMALISATION & VALIDATION
  (NHCX / TPA portal / hospital / app / email)
                        │
                        ▼
        ┌───────────────────────────────────────────────┐
        │  DETERMINISTIC CORE  (must NOT be an LLM)      │
        │  • policy & coverage rule engine               │
        │  • benefit balances, sub-limits, co-pay,       │
        │    deductible, room-rent + proportionate       │
        │    deduction arithmetic                        │
        │  • waiting period / PED / moratorium clock     │
        │  • non-payable & exclusion tables              │
        │  • authority-limit and routing decision        │
        └───────────────────────────────────────────────┘
                        │
      ┌─────────────────┼──────────────────┐
      ▼                 ▼                  ▼
  LLM-ASSISTED      FRAUD SCORING      CLINICAL REVIEW
  (retrieval over   (features +        (clinician, LLM
   policy wording,   anomaly model;     provides the
   summarisation,    surfaces only)     consistency brief)
   drafting)
      └─────────────────┼──────────────────┘
                        ▼
             ROUTING: auto-approve │ auto-recommend-decline │ human review
                        ▼
        EXPLANATION GENERATION (rule-trace driven, clause-cited)
                        ▼
        COMMUNICATION + SETTLEMENT + IMMUTABLE AUDIT LEDGER
```

### F.2 Where deterministic rules MUST sit (non-negotiable)

1. **Every monetary computation.** Sum insured consumption, sub-limit application, room-rent limit and proportionate deduction, co-pay, deductible, non-payable exclusions, other-policy coordination. Money must be reproducible to the paisa.
2. **Eligibility and time-state logic.** Policy in force, member eligibility, waiting periods, PED dates, the **60-month moratorium clock** (**VERIFIED** rule), NCB credits, portability/migration credit carry-forward (**VERIFIED** rules with 72-hour/5-day timelines).
3. **Authority limits and routing.** Which claims go to STP, which to a human, which to the CRC, and at what value.
4. **The CRC gate on repudiation** (**VERIFIED** regulatory requirement).
5. **Explanation assembly.** The clause references in a partial-disallowance letter must come from the rule trace (**VERIFIED** communication duty), not from a model's paraphrase of the policy.
6. **SLA timers.** Pre-auth 1 hour, final auth 3 hours, portability 72 h/5 days, Ombudsman 30 days (**all VERIFIED**).
7. **Consent, purpose, retention and access control.**

### F.3 Where an LLM can legitimately be used

- **Document classification and page-level segmentation** of a mixed PDF bundle.
- **Field and entity extraction** from bills, discharge summaries, investigation reports, prescriptions — always with confidence scores and document coordinates.
- **Retrieval over policy wording, CIS, and non-payable circulars**, returning candidate clauses with citations.
- **Clinical consistency briefing:** "the documented diagnosis is X, the procedure billed is Y, length of stay is Z days; here are the passages that support or contradict necessity." The *opinion* remains human.
- **Fraud-indicator narrative** assembled from deterministic features.
- **Drafting** customer and hospital communication from a fixed template plus injected facts.
- **Reviewer summarisation** with mandatory citations.

### F.4 Guardrails an insurer will demand (and should)

| Guardrail | Concrete form |
|---|---|
| **No model owns a monetary outcome** | The rule engine is the only writer of payable amounts. |
| **No automated repudiation** | Declines are recommendations to the CRC (**VERIFIED** regulatory constraint). |
| **Grounded extraction only** | Every extracted field links to a document and coordinate; ungrounded fields are discarded, not guessed. |
| **Confidence-gated routing** | Per-field thresholds; below threshold → human verification, never silent acceptance. |
| **Versioned everything** | Model, prompt, rule-set, non-payable list, and policy wording versions stamped on each decision. |
| **Reproducibility** | Re-running the same claim with the same versions yields the same decision (or the difference is explainable and logged). |
| **Immutable ledger** | Append-only, stored outside the agents' writable scope, so the audited cannot edit the audit. |
| **Data protection** | PHI minimisation in prompts, no PHI in logs/eval sets, no vendor training on customer data, documented lawful basis and retention. |
| **Bias and drift monitoring** | Approval/deduction rates by provider, product, geography, and value band, reviewed on a cadence. |
| **Kill switch and circuit breaker** | One control that reverts to fully manual processing, tested, with a named owner. |
| **Shadow mode before live** | Run the agent alongside humans on live claims, compare, and only then narrow the human path. |
| **Escalation with evidence** | When the agent is unsure, it escalates with a complete, cited evidence pack — not a bare "needs review". |

### F.5 My opinionated position on what can and cannot be automated

**Can be automated now, with confidence:**
- Document classification and segmentation.
- Extraction of structured fields from bills and discharge summaries, with confidence gating.
- Coverage/benefit arithmetic and non-payable application.
- Eligibility, waiting-period, moratorium and portability credit computation.
- Auto-approval of clean, network, low-value, in-limit cashless claims — which is also the fastest route to the 1-hour and 3-hour regulatory SLAs (**VERIFIED**).
- Summarisation and communication drafting.
- Fraud-indicator surfacing.

**Cannot be automated, and should not be attempted:**
- **Final repudiation.** Not a technical limit — a regulatory one (CRC, **VERIFIED**) and a liability one.
- **Final medical-necessity opinion.** A clinician's judgement, defensible in a forum, is the deliverable; a model's is not.
- **Post-moratorium contestability calls** (the circular bars contestation except for established fraud — **VERIFIED**).
- **Fraud accusation.** Detection and prioritisation, yes; the finding belongs to the SIU and, ultimately, to a forum.
- **Any decision above the delegated authority limit**, however clean the documents look.

**Why:** the constraint that actually binds is not model capability, it is **defensibility**. An Indian health claim decision can end up in front of the insurer's CRC, its grievance cell, the Insurance Ombudsman, and potentially a consumer forum. A decision survives that journey only if it is traceable to a clause, reproducible, and owned by a named accountable human. Design the system so that **every automated decision is already in the shape an auditor would want it** — and the automation rate will follow, because the clean cases are the ones that pass that test.

---

# G. Product Owner craft for this role

### G.1 What a PO in an insurer's claims/health function actually does daily

| Activity | What it concretely looks like here |
|---|---|
| **BRD / functional specs** | Write the business requirements for a claims-automation release: scope (which claim types, which value bands, which hospitals), the rule inventory, the data contracts with TPA and hospital systems, the SLA targets, and the regulatory constraints as *requirements*, not as footnotes. |
| **Process maps** | Current-state and future-state maps for cashless and reimbursement, with the decision diamonds of §B.2 made explicit, plus swimlanes for hospital, TPA, insurer ops, medical, CRC, finance. |
| **User journeys** | Three distinct ones: the **customer** (did I get paid, and do I understand why?), the **hospital insurance desk** (will I get authorisation inside the SLA?), and the **claims reviewer** (can I decide in two minutes with evidence I trust?). |
| **User stories + acceptance criteria** | Written so QA can fail them. Given/When/Then with regulatory SLAs and clause references as testable assertions (see §G.2). |
| **Backlog prioritisation** | Sequence by regulatory exposure first, then leakage, then TAT, then cost. A defensible order: (1) SLA timers and the CRC gate, (2) IDP/extraction, (3) deterministic rule engine, (4) auto-approval band, (5) fraud surfacing, (6) explanation generation. |
| **Sprint ceremonies** | Refinement with medical, ops, legal/compliance, data science, and TPA representatives in the room — a claims sprint without a clinician and a compliance officer will ship something undeployable. |
| **UAT** | Scenario-based, not demo-based. The UAT pack must include edge cases: PED just inside/outside the waiting period, moratorium at 59 vs 61 months, ported policy with carried credits, room-rent breach and proportionate deduction, multiple policies, low-confidence scan, non-network hospital, and a claim designed to trip the 1-hour and 3-hour clocks. |
| **Defect management** | Severity defined by **customer and regulatory impact**, not by engineering convenience. A wrong payable amount on an auto-approved claim is a Sev-1 even though nothing "crashed". |
| **Rollout** | Shadow mode → limited value band → widen band by measured accuracy, with a rollback plan and a kill switch. Never a big-bang switch-on. |
| **Stakeholder management** | Claims ops (whose queue you are changing), medical (whose judgement you are assisting), compliance (who signs the regulatory position), finance (leakage and cost per claim), and the TPA (whose contract and incentives must change). |

### G.2 Three concrete user stories with acceptance criteria

**Story 1 — Cashless pre-authorisation within the regulatory hour**

> **As a** TPA pre-authorisation officer,
> **I want** routine network cashless pre-auth requests to be auto-adjudicated against the policy rule set and returned to the hospital within the regulatory window,
> **so that** we meet the IRDAI one-hour decision requirement and hospitals stop escalating routine cases to a human.

**Acceptance criteria**
1. **Given** a cashless pre-auth request received from a network hospital for a policy in force, **when** all mandatory fields are extracted with confidence ≥ the configured threshold, the diagnosis is not in an excluded category, the amount is within the sum insured and all sub-limits, no waiting period or PED restriction applies, and the requested amount is within the auto-approval authority limit, **then** the system issues an approval without human intervention.
2. **Given** any of the above conditions is not met, **when** the request is processed, **then** the claim is routed to a human reviewer with a cited evidence pack, and the pre-auth SLA clock continues to run.
3. **Given** an approval is issued, **when** it is dispatched to the hospital, **then** the decision record stores: request receipt timestamp, decision timestamp, elapsed time, rule-set version, policy wording version, extracted field values with document coordinates and confidence, and the approving actor (system or human).
4. **Given** elapsed time reaches 45 minutes without a decision, **when** the timer fires, **then** the case is escalated to the on-call reviewer and flagged as SLA-at-risk. *(Threshold is my proposal, INFERRED.)*
5. **Given** the request is received outside the auto-approval band, **then** no approval is issued by the automated path under any circumstances, even if all data is clean.

**Story 2 — Discharge final-authorisation and the three-hour guarantee**

> **As a** hospital insurance desk executive,
> **I want** the final discharge authorisation to be computed and issued automatically for claims that match the approved pre-auth,
> **so that** the patient is not made to wait for discharge and the insurer avoids bearing additional hospital charges from the shareholders' fund.

**Acceptance criteria**
1. **Given** an approved pre-auth exists and a discharge authorisation request is received, **when** the final bill's extracted line items match the approved treatment and stay duration within configured tolerance, **then** final authorisation is issued automatically within the three-hour regulatory limit.
2. **Given** the final bill contains line items not present in the pre-auth or in the coverage tables, **when** the variance exceeds the configured tolerance, **then** only the matched portion is auto-authorised and the variance is routed to a human reviewer as a partial authorisation, with a clause-referenced explanation generated.
3. **Given** the elapsed time since the discharge request reaches two hours without authorisation, **then** the case escalates to a supervisor with an SLA-breach risk flag, and the potential shareholder-fund exposure is recorded on the claim record.
4. **Given** final authorisation is issued, **then** the record evidences the elapsed time against the three-hour limit and stores the clause references used for every deduction.
5. **Given** the patient died during treatment, **when** the claim is processed, **then** the case is flagged for immediate processing and for immediate release of mortal remains, and is never routed through the standard queue.

**Story 3 — Clause-referenced explanation for every partial disallowance**

> **As a** policyholder whose claim has been partially disallowed,
> **I want** a clear written explanation that names the specific policy terms that caused each deduction,
> **so that** I understand the decision and do not need to escalate to a grievance or the Ombudsman.

**Acceptance criteria**
1. **Given** a claim is partially disallowed, **when** the decision is finalised, **then** the system generates an explanation listing every deduction with its amount, its reason code, and the **specific policy term or clause** that caused it.
2. **Given** the explanation is generated, **then** the clause references are taken from the rule trace, not paraphrased by a language model, and the letter is reproducible from the stored decision record.
3. **Given** the claim is a full repudiation, **then** the system blocks dispatch until a **Claims Review Committee** decision reference is recorded against the claim.
4. **Given** the explanation is dispatched, **then** it includes the grievance-redressal process and the **contact details of the concerned Insurance Ombudsman**.
5. **Given** the policyholder raises a grievance on the decision, **then** the grievance is linked to the originating decision record, the rule-set version and the clause references, so the root cause is traceable.

*(Stories 1 and 2 encode the VERIFIED one-hour and three-hour rules. Story 3 encodes the VERIFIED CRC gate and the VERIFIED clause-reference and Ombudsman-contact communication duties.)*

---

# H. ICICI Lombard health insurance — publicly known, sourced

### H.1 Company facts — **VERIFIED** ([Wikipedia: ICICI Lombard](https://en.wikipedia.org/wiki/ICICI_Lombard))

| Fact | Value |
|---|---|
| Legal name | ICICI Lombard General Insurance Company Ltd |
| Founded | 2001, as a JV between ICICI Bank and Fairfax Financial Holdings |
| HQ | Mumbai, Maharashtra |
| Listed | BSE: 540716 · NSE: ICICIGI |
| Parent | ICICI Bank |
| MD & CEO | Sanjeev Mantri |
| Products | General insurance including **Health**, Motor, Travel, Home, Crop, Business |
| Size (2024) | 13,670 employees, 312 branches, 840 virtual offices |
| Position | "The largest private-sector general insurance company in India" (Wikipedia's words) |
| Financials quoted | Revenue ₹18,094 crore (2023); GWP ₹306.18 billion (FY2026); PBT ₹16.83bn (FY22) → ₹21.12bn (FY23); PAT ₹12.71bn → ₹17.29bn |
| Industry share | "second highest industry market share of 8.30 percent in the general insurance market as of February 2022" |

**Citation-integrity warning (important, and a good thing to be able to say):** the Wikipedia page carries a promotional-content maintenance banner (January 2021). Its FY2026 GWP figure of ₹306.18 billion is cited to an **archived 2014 "About ICICI Lombard" page**, which cannot support a FY2026 number — treat that figure as **WEAK**. The ₹18,094 crore / ₹2,112 crore / ₹1,729 crore 2023 figures are cited to an ICICI Lombard financial-outcome PDF that was **not fetched** — **WEAK**. *(This exact citation defect was already recorded in this workspace's earlier research; it stands.)*

**Honest, interview-safe framing:** ICICI Lombard is one of India's largest private general insurers, headquartered in Mumbai, listed on BSE and NSE, with ICICI Bank as parent and Sanjeev Mantri as MD & CEO. **Do not quote the FY2026 GWP or the 8.30% share figure as fact.**

### H.2 Named AI / automation activity — **VERIFIED as headlines, WEAK as content**

These were confirmed to exist, with these titles and dates, from the publisher's own search-results listing at [expresscomputer.in/?s=ICICI+Lombard+AI](https://www.expresscomputer.in/?s=ICICI+Lombard+AI). **The article bodies could not be read** — the pages returned navigation only. Treat the substance as **WEAK** and do not attribute specifics.

| Date | Headline | Interview relevance |
|---|---|---|
| **12 Nov 2019** | "ICICI Lombard is using AI for **claims processing, fraud detection** and policy renewal" — snippet states the company has an internal team of data scientists developing AI models for multiple use cases. | Shows a **seven-year** internal AI-in-claims track record. Your role is not greenfield. |
| **3 Jun 2021** | "ICICI Lombard redefines customer engagement with **Azure AI and Azure Speech** services" — snippet cites increased call screening from **20% to 100%**, improved QA accuracy of calls by **30%**, reduced response time. | Cloud AI stack precedent; call-audio processing already in production. **Snippet-level only — WEAK.** |
| **14 Jun 2021** | "ICICI Lombard bets big on AI to improve customer experience" — snippet: "a major focus on AI… exploring how it can use the technology for **automating most of its core**…" | Strategic intent predates GenAI. |
| **18 May 2023** | "ICICI Lombard collaborates with **actyv.ai** to offer insurance solutions for SMEs" | Partnership precedent, though SME/embedded, not health claims. |
| **3 Jul 2024** | Interview: **Girish Nayak, Chief – Technology, Health UW & Claims**, ICICI Lombard. | **The single most useful name to know.** A single executive owns Technology **and** Health Underwriting **and** Claims — i.e. the exact intersection this role sits in. |
| **23 Jul 2025** | "ICICI Lombard and **AWS** Partner to strengthen disaster recovery with automated cloud-native solution" (Mumbai) | Cloud-native modernisation continues. |
| **4 Aug 2026** | "How AI is reshaping insurance: Inside ICICI Lombard's technology-first transformation" — snippet: "AI is rapidly moving from pilot projects to the core of insurance operations. From underwriting and customer…" | The most recent statement of direction. **Read this before the interview if you can — I could not.** |

### H.3 Regulatory standing — **VERIFIED** ([taxguru.in, 28 Aug 2026 press release](https://taxguru.in/corporate-law/irdai-health-insurance-committee-advances-customer-trust-nhcx-adoption.html))
**Sanjeev Mantri, CEO, ICICI Lombard**, is an insurance-sector invitee supporting IRDAI's **IAC Sub-Committee on Health Insurance** — the body driving NHCX onboarding, standard treatment guidelines, policy-wording simplification, and CIS exclusion review. **The company's CEO is personally in the room where Indian health-claims standardisation is being decided.** This is the strongest single fact you can bring to the interview.

Also **VERIFIED as existing** (headline + date only, content not read): "IRDAI Imposes Rs. 1 Crore Penalty on ICICI Lombard for Regulatory Violations" — [taxguru.in](https://taxguru.in/corporate-law/irdai-imposes-rs-1-crore-penalty-icici-lombard-regulatory-violations.html), ~4 weeks before 13 Oct 2026. **Do not raise this in the interview; do not cite its cause — I could not read it.**

### H.4 Health products, network size, claim-settlement record — **UNVERIFIED**
`icicilombard.com` is blocked (403, recorded previously in this workspace) and no aggregator page was successfully fetched. Therefore:
- **Specific retail health product names: could not confirm. Do not name a product in the interview.**
- **Advertised claim-settlement ratio: could not confirm. Do not quote a percentage.**
- **Cashless network hospital count: could not confirm. Do not quote a number.**

**How to handle this gracefully and turn it into strength:** say plainly — *"I deliberately didn't quote your claim-settlement ratio or network numbers, because I could only find them on marketing pages I couldn't verify. I'd rather ask you for the current figures and the definitions behind them."* That is a better answer than a wrong number, and it demonstrates the anti-fabrication discipline this workspace enforces. Then ask the definition question from §I.

---

# I. Fifteen questions to ask them

Each with why it matters.

1. **"Is the first release aimed at cashless pre-authorisation and discharge authorisation, or at reimbursement claims?"**
 *Why:* they are different products with different data sources and different SLAs. Cashless has hard regulatory clocks (1 h / 3 h) and hospital-system integration; reimbursement has document chaos and a customer-facing explanation problem. The answer determines the entire roadmap.

2. **"Where does the 1-hour pre-auth and 3-hour discharge clock actually start in our systems, and who owns the timestamp?"**
 *Why:* the regulation sets the limit (**VERIFIED**) but the *receipt event* is an internal design choice. If the timestamp is unreliable, every TAT number and every SLA claim is unfalsifiable — and this is the first thing an auditor will test.

3. **"What is our current straight-through-processing rate, and is it measured by claim count, by value, or by step?"**
 *Why:* a blended STP number hides everything. Asking for the split signals you have run this before.

4. **"What share of claims are declined today, and how does the Claims Review Committee actually operate — batch, on-demand, or threshold-based?"**
 *Why:* the CRC gate is a **regulatory** constraint (**VERIFIED**). If the committee meets weekly, an automated decline-recommendation engine just moves the bottleneck. This question will impress.

5. **"Is the GenAI stack going to run on a third-party model API, or inside our own VPC?"**
 *Why:* under DPDP (all digital personal data, no separate sensitive tier — **VERIFIED** structural point), this single architectural answer determines the consent design, the vendor contracts, the logging rules, and whether clinical text can leave the perimeter.

6. **"How far along is our NHCX onboarding, and does the agent consume NHCX from day one or sit behind an adapter?"**
 *Why:* NHCX is the interoperability rail IRDAI is actively pushing (**VERIFIED**, and our own CEO is on the sub-committee). Building a bespoke hospital integration in 2026 that NHCX will obsolete is a real risk.

7. **"Who signs off the regulatory position when an automated decision produces a denial — compliance, legal, or the claims head?"**
 *Why:* it tells you whether the organisation has actually resolved the accountability question, or is hoping the PO will absorb it.

8. **"What is the medical-review capacity we can rely on, and what is the peak queue depth today?"**
 *Why:* automation shifts work from data entry to exception review. If the exception queue is already saturated, automating the happy path makes the *visible* backlog worse, not better.

9. **"How is the non-payable consumables list maintained, and who owns its versioning?"**
 *Why:* it is a top leakage source and a top customer-complaint source. If it lives in a spreadsheet owned by one person, that is your first quick win and a genuine credibility moment.

10. **"Do we have a fraud-scoring model in production for health, and is it a rules scorecard or an ML model?"**
 *Why:* determines whether your role includes model governance, drift monitoring and bias review — or just integration. The 2019 headline suggests something exists; ask what it is now.

11. **"How are TPAs measured, and does the contract carry the service-linked payment and clawback the Master Circular requires?"**
 *Why:* the circular explicitly requires TPA performance monitoring, payment only on full satisfactory service, and clawback passed to policyholders (**VERIFIED**). If the contracts have not been updated, the automation programme inherits a misaligned incentive.

12. **"What does the Product Owner own here — the backlog and requirements, or also the model-quality metrics and the audit evidence?"**
 *Why:* "PO" means different things in different insurers. Getting this wrong means either over-reaching or being blindsided by accountability you did not know you had.

13. **"What is the acceptance bar for go-live — a UAT sign-off, or shadow-mode accuracy on live claims against human decisions?"**
 *Why:* it reveals whether the organisation is serious about safety or is running a demo culture. A shadow-mode bar is the answer you want to hear.

14. **"How does the Claims Review Committee's workload change if we automate approvals and route only declines to them?"**
 *Why:* it shows you have thought about the *second-order* effect of automation on the control function, which is exactly what separates a PO from a project manager.

15. **"Six months from now, what number on which dashboard tells you this programme worked?"**
 *Why:* the honest answer might be leakage, or TAT, or grievance volume. Note the IRDAI sub-committee's own remark that settlement ratios alone are insufficient and absolute values matter too (**VERIFIED**) — if they answer "settlement ratio", you have a genuinely useful thing to raise.

---

# J. Honest gap analysis

Four real gaps. Each with the best honest framing — no overclaiming, and in every case the gap is paired with an adjacent, verifiable strength from `config/profile.md`.

### J.1 Claims adjudication *operations*
- **The gap:** the candidate's 9 years at Optum were in **US Medicare/Medicaid enrollment** transaction auditing for CMS compliance (Apr 2014 – Mar 2023), with an earlier stint as a Claims Associate (Apr 2014 – Feb 2016). He has **not** run Indian health-claims adjudication, has not owned a claim queue, and has not applied policy sub-limits to a hospital bill.
- **Honest framing:** *"My claims exposure is a year as a Claims Associate early on, and my real depth is nine years auditing high-volume regulated transactions for CMS — which is the same discipline this role needs, applied to a different transaction. I have not run Indian health adjudication. What I bring is the audit mindset: I know what an examiner asks for, and I build systems that can answer on the first request."*
- **Do not say:** that he has claims adjudication experience, or that enrollment work was claims work. The profile is explicit that the two are different.

### J.2 Indian health-insurance specifics
- **The gap:** he knows US payer terminology and CMS compliance. Indian product structures (room-rent limits and proportionate deduction, PED waiting periods, the 60-month moratorium, IIB portability, CIS, TPA-mediated cashless) are new.
- **Honest framing:** *"I've spent the last weeks learning the Indian health-claims stack properly — the 2024 Master Circular, the one-hour and three-hour cashless clocks, the CRC gate on repudiation, the 60-month moratorium, NHCX. I know the US side well, which is actually useful because the contrast is sharp: US claims arrive as coded transactions, Indian health claims arrive as a hospital bill and a discharge summary. That difference is exactly why document AI matters more here."*
- **Use the contrast, don't hide the gap.** The US-vs-India contrast is a genuine asset, not a substitute for knowledge.

### J.3 TPA experience
- **The gap:** no TPA-side or TPA-integration experience.
- **Honest framing:** *"I haven't worked with or inside a TPA. What I have done is integrate with external data sources and third-party systems and make their output verifiable — at Pi Software I built production pipelines across 10+ client dashboards, and at Black Piano 18 automated ETL pipelines into BigQuery. The TPA relationship question I'd want to understand early is contractual: the Master Circular requires service-linked payment and clawback, so the TPA's incentives and my automation targets have to be aligned before I write a single story."*
- **The framing works because it converts an experience gap into a requirements question he can ask in the interview.**

### J.4 Product Owner *title* experience
- **The gap:** the titles held are **Data Analyst** (Black Piano, Mar 2026 – present; Pi Software, Mar 2023 – Feb 2026) and **Enrollment Quality & Audit Representative (CMS Auditor)** (Optum). He has **not** held a Product Owner title, has no people-management experience, and should not claim either.
- **Honest framing:** *"I haven't held the PO title. What I've done is the substance of it without the label: I built a custom MCP tool so non-technical marketing and sales teams could generate data-grounded content from a one-line prompt — that's requirements gathering, user research, and shipping something non-technical users actually adopt. I built a self-healing data-quality agent with a defined escalation path that emails a human only when it cannot resolve — that's acceptance criteria and human-in-the-loop design. And my JobAgents pipeline scores candidates deterministically before any model is called, which is the same cost-gate and determinism discipline a claims rule engine needs."*
- **Strengthen with the anti-fabrication angle, which is directly relevant to claims:** *"I also enforce anti-fabrication in code, not in prompts — my tailor service validates every generated claim against a ground-truth file. That instinct is exactly what an automated claims decision needs: the model may not assert a fact that isn't traceable to a source document."*
- **Do not say:** "acting PO", "de facto product owner", or anything implying a held title. The profile forbids inflating titles and forbids claiming people-management.

### J.5 What to lead with instead of apologising
Three verifiable strengths that map cleanly onto this role:
1. **Audit discipline at scale** — nine years applying zero-tolerance quality gates to high-volume regulated transactions, producing audit-ready documentation for CMS. **This is the compliance backbone an automated decisioning system needs.**
2. **Human-in-the-loop and bounded autonomy, actually built** — a self-healing agent that retries three times and escalates to a human only when unresolved; a JobAgents pipeline that scores 22,839 candidates with zero model calls and sends only the top matches to an LLM. **That is a cost gate and a determinism boundary — the same architecture a claims rule engine requires.**
3. **Verification infrastructure** — hash-chained audit ledgers stored outside the agents' writable directory, an independent oracle checking every agent turn, a report-promotion gate that refused 34 of 36 candidates. **Translating that to claims: an immutable decision ledger and an independent verifier are things he has already built, not things he has read about.**

---

# Appendix — source ledger

| Source | URL | Status |
|---|---|---|
| IRDAI Master Circular on Health Insurance Business, 29.05.2024 (full text) | https://taxguru.in/corporate-law/master-circular-irdai-insurance-productsregulations-2024health-insurance.html | **VERIFIED** — primary text read |
| IRDAI IAC Sub-Committee on Health Insurance, 3rd meeting, 28 Aug 2026 | https://taxguru.in/corporate-law/irdai-health-insurance-committee-advances-customer-trust-nhcx-adoption.html | **VERIFIED** — press release read in full |
| Wikipedia: Insurance Regulatory and Development Authority | https://en.wikipedia.org/wiki/Insurance_Regulatory_and_Development_Authority_of_India | **VERIFIED** (age-limit passage: **WEAK**, underlying Hindu article not fetched) |
| Wikipedia: DPDP Act 2023 | https://en.wikipedia.org/wiki/Digital_Personal_Data_Protection_Act,_2023 | **VERIFIED** |
| Wikipedia: Data Protection Board of India | https://en.wikipedia.org/wiki/Data_Protection_Board_of_India | **VERIFIED** |
| Wikipedia: ICD-10 | https://en.wikipedia.org/wiki/ICD-10 | **VERIFIED** |
| Wikipedia: ICICI Lombard | https://en.wikipedia.org/wiki/ICICI_Lombard | **VERIFIED** for structure/leadership; **WEAK** for financials (broken citation chain, promotional banner) |
| Express Computer — ICICI Lombard AI article index | https://www.expresscomputer.in/?s=ICICI+Lombard+AI | **VERIFIED** as a list of headlines and dates; **article bodies not readable** |
| Express Computer — Digit's seven-minute claims | https://www.expresscomputer.in/exclusives/the-rise-of-real-time-insurance-inside-digits-seven-minute-claims-revolution/130460/ | Headline/date only; **body not readable** |
| Express Computer — NHCX/cashless search index | https://www.expresscomputer.in/?s=IRDAI+health+insurance+cashless | Headline/date only |
| TaxGuru IRDAI tag index | https://taxguru.in/tag/irda/ | **VERIFIED** as an index |

### Could not source — do not assert any of these
1. **Reimbursement settlement TAT** (the commonly cited 15-day / 30-day-with-investigation figures and the penal-interest provision) — the operative text is in the IRDAI (Protection of Policyholders' Interests, Operations and Allied Matters of Insurers) Regulations 2024 Master Circular, which I could not fetch. **The Master Circular I did read explicitly cross-refers to it**, so the instrument exists; the numbers are **UNVERIFIED**.
2. **Insurance Ombudsman award monetary ceiling, complaint limitation period, and binding effect.**
3. **DPDP penalty amounts** and any health-specific Rules provisions.
4. **ICICI Lombard's retail health product names, advertised claim-settlement ratio, and cashless network size.**
5. **The specific circular number for the 01-Apr-2024 removal of the health-insurance age bar.**
6. **Bodies of the Express Computer and TaxGuru article pages** cited in §H.2 — headlines, dates and snippets only.

### Blocked or failed in this session (do not retry)
`irdai.gov.in` (non-public IP) · `business-standard.com` (non-public IP) · `icicilombard.com` (403, previously recorded) · `policyholder.gov.in` · `medibuddy.in/blog/health-insurance/cashless-hospitalisation/` (404) · several `taxguru.in/insurance/...` and other guessed URL paths (404) · `en.wikipedia.org/wiki/Insurance_Ombudsman_(India)`, `/wiki/Cashless_hospitalisation`, `/wiki/ICICI_Lombard_General_Insurance_Company` (all 404 — the correct titles are `Insurance_ombudsman` (also missing) and `ICICI_Lombard`).
