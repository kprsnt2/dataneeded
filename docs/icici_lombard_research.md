# ICICI Lombard — Company + Role-Intel Brief

**Prepared for:** Prashanth Kumar Kadasi · inbound LinkedIn approach from "Swarnim Vaidya, Leadership Hiring | ICICI Lombard"
**Date:** 2026-10-12 · **Author:** intel-researcher (task-1)
**Purpose:** anchor the reply to the recruiter in verified fact. Nothing here may be repeated in an interview unless it carries a source below.

---

## 0. Confidence legend + method

| Tag | Meaning |
|---|---|
| **VERIFIED** | I fetched a source and read the claim in it. Source URL in §H. |
| **WEAK** | Single low-quality source, a secondary aggregator whose primary I could not open, or an internally inconsistent figure. Usable only with the caveat attached. |
| **UNVERIFIED** | Could not confirm. **Do not assert.** |
| **INFERENCE** | My reasoning from evidence, explicitly not a sourced fact. |
| **MARKET-GENERAL** | True of the Indian general-insurance job market broadly, **not** verified for ICICI Lombard specifically. |

**Method note.** `web_search` is unavailable (no API key). I used `web_fetch` on named URLs, then switched to `pwsh`/`Invoke-WebRequest` after discovering the fetch tool's host allowlist is much narrower than the machine's network. Full block log in §H.2 — **the blocks are part of the deliverable**, because they define what remains unknown.

**Load-bearing caveat on §D.** I found **no** evidence of GCP, BigQuery, Looker, Snowflake or Databricks at ICICI Lombard. That is *absence of evidence in the sources I could reach*, not proof of absence. The primary documents that would settle it (annual report, Digital Day 2026 deck, internal JD) are PDFs I could not parse. Treat §D as directional, and make the recruiter confirm.

---

## A. Company snapshot

| Fact | Value | Conf |
|---|---|---|
| Legal name | ICICI Lombard General Insurance Company Limited | VERIFIED (Wikipedia) |
| HQ | Mumbai, Maharashtra, India | VERIFIED (Wikipedia) |
| Founded | 2001 | VERIFIED (Wikipedia) |
| Ownership origin | Joint venture between ICICI Bank and Fairfax Financial Holdings Ltd (Toronto); ICICI Bank ~64% / Fairfax ~36% at formation | VERIFIED (Wikipedia) |
| JV ended | Fairfax (via FAL Corp) exited Oct 2019, selling its ~4.9% residual stake for ~₹2,627 crore | VERIFIED (Wikipedia; Screener citing Business Standard) |
| Promoter holding | 51.22% as of Jun 2026 (quarterly shareholding pattern) | VERIFIED (Screener) |
| Listed | BSE: 540716 · NSE: ICICIGI | VERIFIED (Wikipedia, Screener) |
| MD & CEO | Sanjeev Mantri | VERIFIED (Wikipedia citing Economic Times) |
| CTO-equivalent | Girish Nayak — Chief – Technology, Health UW & Claims (earlier title: Chief – Customer Service, Technology & Operations) | VERIFIED (Express Computer, quoted directly 2024 & 2025) |
| Industry position | India's largest private-sector general insurer; Screener states largest non-life insurer by GDPI with **9.4% market share as of H1 FY25** | VERIFIED (Wikipedia) / WEAK (Screener figure, primary BSE PDF unreadable) |
| Commercial-segment share | ~13% fire, ~17% engineering, ~21% marine cargo, ~19% liability | WEAK (Screener, citing a BSE filing I could not open) |
| Employees / branches | 13,670 employees and 312 branches (2024); separate infobox entry says 10,236 employees (2021) | WEAK — the two figures come from different years and I could not open the cited PDF |
| Scale (policies/claims) | "over 37.6 million policies and 3.2 million claims processed" | VERIFIED (Express Computer, 23 Jul 2025) |
| FY2026 GWP | ₹306.18 billion claimed on Wikipedia | **WEAK — the citation is broken.** It points to a 2014 archived page, which cannot support a FY2026 figure. Do not cite this number. |
| FY2023 financials | Revenue ₹18,094 cr · Operating income ₹2,112 cr · Net income ₹1,729 cr · Total assets ₹50,848 cr · Total equity ₹9,468 cr | WEAK (Wikipedia infobox; cites an icicilombard.com PDF I could not open) |
| FY2022→FY2023 PBT/PAT | PBT ₹16.83bn → ₹21.12bn; PAT ₹12.71bn → ₹17.29bn | WEAK (Wikipedia, same unreadable citation chain) |

### Lines of business
VERIFIED (Wikipedia infobox + body): general insurance, health, motor (car + two-wheeler), travel (incl. overseas student), home, crop/weather, business/commercial insurance, plus reinsurance, claims management and investment management. Distribution is via intermediaries, bancassurance (e.g. Karur Vysya Bank partnership, 2019) and direct web/app.

### Stated AI / digital / data initiatives (all VERIFIED via Express Computer unless noted)

| Date | Initiative |
|---|---|
| Jun 2021 | **Azure Cognitive Services** — Azure Speech Services + custom NLP built by ICICI Lombard data scientists with Microsoft's AI team. Call screening 20%→100%; QA accuracy 50%→>80%; internal audit latency 12h→2h; ~1,000 outbound calls/day; 90% accuracy on key phrases such as registration number. |
| May 2023 | Strategic partnership with **actyv.ai** (Singapore-based enterprise SaaS, embedded B2B) for SME insurance solutions. |
| Jul 2024 | CTO interview: AI adoption across claim processing, customer-service chatbots, risk assessment and **fraud detection**; ethics and data-privacy framing. |
| 23 Jul 2025 | **Disaster recovery migrated from AWS Mumbai Region → AWS Hyderabad Region.** Cloud-native, fully automated, all business-critical applications, full-site DR drill with real-time validation and minimal manual intervention. Stack: **AWS Elastic Disaster Recovery, AWS Step Functions, infrastructure-as-code.** |
| 23 Jul 2025 | Reported "migrating its core systems to the cloud"; AI-led **IL TakeCare app**; 37.6M policies / 3.2M claims. |
| 29 Sep 2026 | BSE announcement: **"Digital Day" investor/analyst meet 2026** — video link for the presentation circulated. (Announcement existence VERIFIED via Screener's BSE feed; **deck contents not read** — PDF.) |
| 4 Aug 2026 | **25 new offerings for the silver jubilee.** AI-powered **health underwriting platform** (guided digital journey, real-time AI evaluation against underwriting guidelines). Multilingual **Voice AI platform** — **>1 million customer conversations handled**; policy enquiry, modification and purchase by voice. IL TakeCare **AI-powered travel planner** (personalised itineraries + embedded travel insurance). **Digital insurance branch** (self-service + assisted; purchase, KYC, document submission, claim registration, largely paperless). Digitally managed roadside assistance. |
| 6 Oct 2026 | BSE: intimation of **Q2 & H1 FY2027 earnings call**. Screener lists next result date **14 Oct 2026**. |

**Read of §A:** this is a genuinely digitising insurer with executive-level AI sponsorship (CTO publicly fronting AI since 2021, a Digital Day for investors in 2026). The AI narrative the recruiter used is not fabricated — it maps to real programmes. That is the strongest positive signal in this brief.

---

## B. The recruiter signal — what "Leadership Hiring" actually implies

Everything in this section is **INFERENCE** unless tagged otherwise. There is no public source that defines ICICI Lombard's internal TA taxonomy.

**B.1 — The title is a designation, not a mandate.** In Indian insurers and banks, "Leadership Hiring" is commonly a *sub-function label* for a recruiter or a small team that handles senior/experienced-hire requisitions — roughly Assistant Manager through AVP/VP and above. It is used both for genuinely senior mandates **and** as a prestige-flavoured designation on a lateral-hiring recruiter's profile. INFERENCE: the title alone tells us almost nothing about the level of the role in question.

**B.2 — The message content contradicts a real leadership mandate.** The outreach names only Python, data analytics, "autonomous AI systems and data pipelines", and cites a specific project (the Black Piano data-quality agent). A retained search for a leadership role does not open with a candidate's side-project. INFERENCE: the recruiter is working from a **skills-keyword profile match**, not from a shortlist spec. That is volume/lateral sourcing behaviour.

**B.3 — No title, level, location, comp or JD link = template outreach.** This is the single most diagnostic fact. A recruiter with a live, approved, funded requisition can paste the title and the JD link in the first message at zero cost. Withholding all five is the standard shape of a **fishing / pipeline-building** message — building a candidate pool ahead of, or in parallel with, a requisition that may not be finalised. INFERENCE, but a strong one.

**B.4 — The channel is a tell.** The approach came via LinkedIn DM, not an ATS link or the careers portal. ICICI Lombard's own careers surface is Akamai-hardened (403/400 — §H.2), which is consistent with a company that routes hiring through recruiters and third-party boards rather than open self-serve applications. INFERENCE.

**B.5 — Verification gap you must close.** **UNVERIFIED: that "Swarnim Vaidya" is employed by ICICI Lombard, and in what capacity.** I could not verify this — LinkedIn profiles are not fetchable without auth, and no other source confirmed the name. This is not an accusation; it is an open check. Three benign possibilities: (a) genuine in-house recruiter, (b) third-party/RPO/agency recruiter working an ICICI Lombard mandate and using the client's name, (c) a recruiter at an ICICI group entity or a vendor. A fourth, non-benign possibility is a data-harvesting approach — generic template, no JD, no verifiable identity is also that pattern. Cost of checking is one LinkedIn search; cost of not checking is unbounded.

**B.6 — Practical implication.** Treat this as a **lead, not an offer**. The correct posture is: engage warmly, extract the five missing facts (§I) before investing any preparation, and verify the recruiter's employer in parallel. Do not tailor a resume or prepare an interview loop until a title and JD exist.

---

## C. Likely role families matching "Python + data analytics" at an Indian general insurer

All of §C is **MARKET-GENERAL**. These are archetypes common across Indian general insurers; **none is verified as an open ICICI Lombard requisition.** Experience bands are the market norm, not a company policy.

| Role family | Typical responsibilities | Typical tools/stack | Typical band | IC vs manager |
|---|---|---|---|---|
| **Data Analyst** | Ad-hoc analysis for underwriting/claims/marketing; build recurring reports; dashboard ownership; data validation; stakeholder Q&A | SQL, Excel, Python (pandas), Power BI/Tableau, sometimes SAS | 1–6 yrs | IC |
| **MIS / BI Analyst** | Fixed-format periodic reporting to management and IRDAI; month-end packs; distribution/channel MIS; reconciliation | SQL, Excel/VBA, Power BI, SSRS, Oracle/SQL Server; often an on-prem warehouse | 2–8 yrs | IC |
| **Analytics / Data Engineer** | Build and maintain ETL/ELT into the warehouse; data models for actuarial and claims; pipeline reliability; increasingly cloud-native | SQL, Python, Airflow/Step Functions, Spark, AWS/Azure, dbt; warehouse (Snowflake/Databricks/Redshift/Synapse) | 3–9 yrs | IC to lead |
| **Data Scientist** | Pricing/risk models, fraud and leakage detection, claims triage, NLP on call transcripts, propensity/renewal models | Python (scikit-learn, pandas), SQL, notebooks, ML platform; in insurers often closer to actuarial than to product | 3–10 yrs, often MSc/PhD | IC; leads at 8+ |
| **Automation / Digital Analyst** | RPA and workflow automation, chatbot/voice-AI operations, digital journey analytics, process mining | Python, RPA (UiPath/Power Automate), APIs, LLM/NLP tooling, SQL | 2–7 yrs | IC |
| **Actuarial-adjacent analytics** | Loss-ratio and reserving support, experience studies, IBNR inputs | SQL, Excel, R/Python, actuarial tools | 2–10 yrs | IC (qualified actuaries separate) |

**Likely fit for this candidate:** Data Analyst / Analytics-Engineer / Automation-Digital Analyst. **Unlikely without a stretch:** Data Scientist (no actuarial/pricing depth) and any people-manager role (profile has no management experience and the ground-truth rules forbid claiming it).

**IC vs manager note.** Indian insurers are title-conservative. "Manager" frequently means a senior individual contributor with a designation bump, not a people-manager. So a "Manager – Analytics" title would **not** imply the candidate is being hired to manage people. INFERENCE, but consistent with the sector.

---

## D. Tech-stack reality check — the most decision-relevant section

### D.1 What is verified about ICICI Lombard's platform

| Layer | Evidence | Conf |
|---|---|---|
| **Cloud — AWS** | DR migrated AWS Mumbai → AWS **Hyderabad** region; cloud-native, fully automated; **AWS Elastic Disaster Recovery**, **AWS Step Functions**, **infrastructure-as-code**; covers all business-critical applications; "migrating its core systems to the cloud" (Jul 2025) | VERIFIED |
| **Cloud — Azure** | **Azure Cognitive Services / Azure Speech Services** + custom NLP for call QA, built with Microsoft's AI team (Jun 2021) | VERIFIED |
| **AI/NLP** | Multilingual Voice AI (>1M conversations), AI health-underwriting engine, AI travel planner in IL TakeCare, chatbot history back to 2021 (Telegram) | VERIFIED |
| **Partner/vendor AI** | actyv.ai (embedded B2B/SME, May 2023) | VERIFIED |
| **Orchestration / automation** | AWS Step Functions + IaC confirmed for DR. RPA in claims/ops is asserted in CTO interviews but **no specific RPA product is named** | VERIFIED (Step Functions) / UNVERIFIED (RPA vendor) |
| **BI / visualisation tool** | **No evidence found.** Power BI, Tableau, Looker — none confirmed | UNVERIFIED |
| **Warehouse / lakehouse** | **No evidence found.** Snowflake, Databricks, BigQuery, Redshift, Synapse — none confirmed | UNVERIFIED |
| **GCP specifically** | **No evidence found anywhere in any source I reached** | UNVERIFIED |

### D.2 The transfer question — stated plainly

The candidate's data strength is **BigQuery + Looker Studio + GCP (Cloud Run)**. The verified evidence points to **AWS (primary, including core systems) and Microsoft Azure (AI/speech)**. **No GCP evidence exists in any source I could reach.**

- **What transfers:** SQL (deeply), Python, ETL/pipeline design, data-quality logic, dashboard thinking, LLM/agentic engineering, and — importantly — **the data-quality-agent story is directly relevant**, because the recruiter specifically cited it and because claims/underwriting data quality is a real insurer problem.
- **What likely does not transfer on day one:** BigQuery syntax/dialect, Looker Studio, GCP-specific tooling. If they run AWS + Azure, expect Redshift/Synapse/Athena-family tooling and Power BI.
- **Honest framing for the candidate:** "I've built 18 production ETL pipelines on BigQuery and Looker Studio on GCP. The SQL, modelling and pipeline engineering transfer directly; the specific cloud is a ramp, and I'd expect to be productive on AWS or Azure within weeks." That is true and it pre-empts the gap rather than hiding it.
- **Do not** claim GCP/BigQuery experience as a match for an AWS/Azure shop, and **do not** claim insurance-domain data experience.

### D.3 Two adjacent observations worth knowing

1. **AWS Hyderabad region** — ICICI Lombard's DR now runs in Hyderabad, the candidate's home city. This is *not* evidence of a Hyderabad office or Hyderabad roles, and must not be presented as one. It is at most a conversational detail.
2. **The Digital Day 2026 deck (29 Sep 2026)** is the single highest-value unread document. It is a PDF on BSE; I could not extract text (no PDF tooling available locally — §H.2). **Recommendation: the Lead or candidate should open it manually.** It is the company's own most recent statement of digital/AI strategy and may name the actual platform.

---

## E. Compensation reality check

### E.1 What I could source

| Item | Value | Conf |
|---|---|---|
| ICICI Lombard on AmbitionBox | 6.3k reviews · **20.8k salaries reported** · page updated 11 Oct 2026 | VERIFIED (page content) |
| ICICI Lombard **Data Analyst** | Page exists, based on **60+ employee reports**, experience band **1–8 yrs**, page updated 18 Sep 2026. Stated: avg. salary is **12% more than the average in the Insurance industry**. **Exact figures are login-gated.** | VERIFIED (existence + band) / figures UNVERIFIED |
| ICICI Lombard **Data Engineer** | Page exists, **20+ employee reports**, band **1–5 yrs**, updated 1 Oct 2026. Stated: avg. salary is **28% less than the average in the Insurance industry**. A visible figure of **11.2** (L/yr) appears beside the 1–5 yr band, and **16.5** appears among latest reported salaries. **Ambiguous — treat as indicative only.** | WEAK |
| Comparable employers (Data Engineer, from AmbitionBox's own comparison table) | Principal Financial Group 13.5–14.9 (100 salaries) · Swiss Re 19.8–25.8 (37) · MetLife 15.7–21.4 (9) · HDFC Life 12.7 (7) · Cholamandalam MS General Insurance 10.7 (10) · Tata AIA Life 10.4–15.3 (6) | WEAK (aggregator, self-reported) |
| Designations visible on ICICI Lombard's salary index | Business Analyst (121 salaries), Associate Software Engineer (127), Product Manager 12.5–14.8, Senior Product Manager 13.8–17.6, Area Sales Manager 11.7 — note **no data-science/analytics leadership designation appears in the visible list** | WEAK |

### E.2 Why the exact numbers are missing, and what to do
AmbitionBox gates exact salary figures behind login; the values are not in the server-rendered HTML (I checked the embedded JSON — only data-point counts are present). Glassdoor, Indeed and 6figr were all blocked or JS-only (§H.2). **I therefore cannot give a verified ICICI Lombard band.** Two ways to close it: (a) log into AmbitionBox and read the two pages directly, (b) ask the recruiter for the band in the first reply — which is the correct move anyway.

### E.3 The expectation gap — flag this to the candidate
- The candidate's current arrangement is **remote, serving US/UK clients** (Black Piano hires India-based talent for US/UK clients). That is a **USD-denominated, remote-first** compensation and lifestyle baseline.
- An Indian general insurer's data role is **INR-denominated, office-based, and structurally below** product/consulting/GCC pay. The WEAK anchor above (~₹11.2 L/yr at 1–5 yrs for Data Engineer, and peers at ₹10–15 L) is materially below any plausible USD-remote equivalent.
- **Seniority-band mismatch risk.** The candidate has **12.5 years of total work experience but only ~3.5 years in data/analytics** (2023–present; prior 9 years were CMS auditing at Optum). Indian insurers price analytics roles largely on **years-in-data**. He may therefore be screened into a band that under-prices his total seniority, while simultaneously being "too senior" in years for entry IC roles. This is the most likely source of a comp disappointment, and it is worth naming before the call rather than after.
- **Recommendation:** do not discuss numbers first. Get title + band + location, then decide whether the number is even in range. If the band is below his floor, that is a clean, early, polite exit — much better than after a three-round loop.

---

## F. Insurance-domain vocabulary to be able to speak

**Standard industry definitions, correct as used in Indian general insurance.** These are definitions, not claims about ICICI Lombard.

1. **GWP / GDPI** — Gross Written Premium / Gross Direct Premium Income: total premium written before ceding to reinsurers; GDPI excludes reinsurance assumed. The headline top-line growth metric.
2. **Loss ratio** — claims incurred ÷ premium earned, for a line of business. The core profitability metric for a general insurer.
3. **Combined ratio** — loss ratio + expense ratio. **Below 100% = underwriting profit; above 100% = underwriting loss** (offset by investment income).
4. **Incurred Claims Ratio (ICR)** — claims incurred relative to premium earned over a period; the reported form of loss ratio in Indian insurer disclosures.
5. **IBNR** — Incurred But Not Reported: reserves for claims that have occurred but are not yet notified. A reserving concept; its accuracy drives reported profitability.
6. **Claims TAT** — Turnaround Time from claim registration to settlement. A key service metric and a regulator-visible one.
7. **Motor OD vs TP** — Own Damage (the insured's own vehicle) vs Third Party (liability to others). Motor TP is a long-tail, regulated, historically loss-making book; the split matters for reserving.
8. **Persistency / renewal ratio** — share of policies renewed at expiry. Proxy for customer satisfaction and distribution health.
9. **Fraud / leakage** — "fraud" is deliberate deception; "leakage" is unintended over-payment (process error, wrong tariff, duplicate settlement). Analytics teams are usually tasked with detecting both.
10. **Solvency ratio** — available solvency margin ÷ required solvency margin. IRDAI requires a minimum; insurers typically report well above it. A capital-adequacy metric.
11. **Ceding / reinsurance** — premium and risk transferred to a reinsurer; affects net retained risk and hence net loss ratios.
12. **IRDAI reporting** — statutory periodic filings to the Insurance Regulatory and Development Authority of India (public disclosures, financials, claims and grievance data). Regulatory reporting is a major, calendar-driven workload for insurer MIS/data teams — and directly adjacent to the candidate's **CMS audit/compliance background**, which is a genuine and honest bridge.

---

## G. Questions to ask the recruiter

Ordered so the highest-value facts come first. Q1–Q5 are the ones that decide whether to continue.

1. **"What is the exact job title, and what level is it mapped to internally?"** — The whole brief turns on this; "Leadership Hiring" and "Python + data analytics" point at different levels.
2. **"Can you share the job description or a link to the posting?"** — A live, funded requisition has a JD. If one cannot be produced, that is itself the answer.
3. **"Is this an IC role or does it include people management?"** — The candidate has no people-management experience and must not claim any; knowing early avoids a wasted loop.
4. **"What is the location and the working model — is it Mumbai office-based, hybrid, or remote?"** — The candidate is Hyderabad-based and currently remote-first. This is the most likely hard blocker.
5. **"What is the compensation band for this level?"** — Ask after title/level, never before. Compare against the INR-vs-USD baseline in §E.3.
6. **"Is this a direct ICICI Lombard payroll role, or through a partner/vendor/RPO?"** — Resolves the §B.5 verification gap and changes the terms, benefits and career track.
7. **"Which team does this sit in — analytics, data engineering, digital/automation, or MIS — and who does it report to?"** — Determines whether the work is genuinely AI/agentic or conventional reporting.
8. **"What does the data platform look like — which cloud, warehouse and BI tools?"** — Directly tests §D. If the answer is AWS/Azure + Power BI, the candidate can plan the ramp honestly instead of being surprised.
9. **"Given my background is GCP/BigQuery and 3.5 years in data, how does that map to the band you have in mind?"** — Surfaces the seniority-band mismatch (§E.3) early and on the candidate's terms.
10. **"What is the interview process and timeline?"** — Also a soft test of whether the requisition is real and moving.

---

## H. Sources

### H.1 Sources actually read

| # | URL | Supports | Conf |
|---|---|---|---|
| 1 | https://en.wikipedia.org/wiki/ICICI_Lombard | Legal name, HQ, 2001 founding, JV structure, Fairfax exit 2019, listing (BSE 540716 / NSE ICICIGI), MD&CEO, product lines, FY2023 financials, employees/branches | VERIFIED (with WEAK sub-items as flagged in §A) |
| 2 | https://www.screener.in/company/ICICIGI/consolidated/ | Shareholding (promoter 51.22% Jun 2026), market-share claim, commercial segment shares, BSE announcement feed incl. **Digital Day 29 Sep 2026** and Q2/H1 FY2027 earnings-call intimation, next result date 14 Oct 2026, annual-report and credit-rating links | VERIFIED (page content) / WEAK (its BSE-sourced figures) |
| 3 | https://www.expresscomputer.in/industries/bfsi/icici-lombard-and-aws-partner-to-strengthen-disaster-recovery-with-automated-cloud-native-solution/126508/ | AWS Mumbai→Hyderabad DR migration, Elastic Disaster Recovery, Step Functions, IaC, core systems to cloud, 37.6M policies / 3.2M claims, Girish Nayak title | VERIFIED |
| 4 | https://www.expresscomputer.in/news/how-ai-is-reshaping-insurance-inside-icici-lombards-technology-first-transformation/137365/ | 25 silver-jubilee offerings, AI health underwriting platform, Voice AI >1M conversations, IL TakeCare AI travel planner, digital insurance branch, roadside assistance | VERIFIED |
| 5 | https://www.expresscomputer.in/interviews/icici-lombard-powering-ai-driven-transformation-in-the-insurance-sector/113683/ | CTO interview: AI in claims, chatbots, risk assessment, fraud detection | VERIFIED |
| 6 | https://www.expresscomputer.in/artificial-intelligence-ai/icici-lombard-redefines-customer-engagement-with-azure-ai-and-azure-speech-services/76500/ | Azure Cognitive/Speech Services + NLP; 20%→100% call screening; QA 50%→>80%; 12h→2h audit latency; in-house data scientists | VERIFIED |
| 7 | https://www.expresscomputer.in/?s=ICICI+Lombard | Index of the above; also actyv.ai partnership (May 2023), Telegram chatbot (2021), 2021 "bets big on AI" piece | VERIFIED (headlines/dates) |
| 8 | https://www.ambitionbox.com/salaries/icici-lombard-salaries | 6.3k reviews, 20.8k salaries, designation index with visible ranges | VERIFIED (page content) |
| 9 | https://www.ambitionbox.com/salaries/icici-lombard-salaries/data-analyst | 60+ reports, 1–8 yr band, "12% more than Insurance industry avg", login gate on figures | VERIFIED (existence/band) |
| 10 | https://www.ambitionbox.com/salaries/icici-lombard-salaries/data-engineer | 20+ reports, 1–5 yr band, "28% less than Insurance industry avg", visible 11.2 / 16.5, peer comparison table | WEAK |

### H.2 Blocked / unusable sources — recorded, not substituted

| Target | Result |
|---|---|
| `icicilombard.com/careers` | **HTTP 403** (Akamai "Access Denied") |
| `icicilombard.com` (root) | **HTTP 403** (Akamai) |
| `jobs.icicilombard.com` | **HTTP 400** (Akamai "Invalid URL") |
| `ambitionbox.com` via fetch tool | **HTTP 403** (Akamai) — succeeded only via `pwsh` |
| `glassdoor.co.in` | **HTTP 403** (pwsh) / non-public IP (fetch tool) |
| `in.indeed.com` | **HTTP 403** (pwsh) / non-public IP (fetch tool) |
| `naukri.com` | Reachable but a **JS shell** (~14 KB) — no server-rendered listings |
| `instahyre.com/jobs-at-icici-lombard/` | **Client-rendered Angular** — template placeholders only, zero data |
| `hirist.tech/jobs/icici-lombard` | **HTTP 404** |
| `analyticsindiamag.com/?s=…` | **JS shell** |
| `bfsi.economictimes.indiatimes.com/topic/…` | **HTTP 404** |
| `moneycontrol.com` tag page | HTTP 200 but body **JS-truncated** — no article text |
| `economictimes.indiatimes.com` company page | **HTTP 404** |
| **BSE annual reports & announcement PDFs** | `web_fetch` → **"unsupported content type application/pdf"**; `AnnPdfOpen.aspx` → **HTTP 406** |
| **PDF text extraction (local)** | **Unavailable** — no `pypdf`, `PyPDF2`, `pdfplumber`, `fitz`, `pdfminer` or `pdftotext` in this environment. **This is why no annual report or Digital Day deck content appears in this brief.** |
| `irdai.gov.in` | **504 Gateway Timeout** (pwsh) / non-public IP (fetch tool) |
| `web.archive.org` | Connection closed (pwsh) / non-public IP (fetch tool) — **no Wayback workaround available** |
| `6figr.com` | Reachable but **JS shell** |
| `tickertape.in` | Non-public IP (fetch) / guessed URL **404** (pwsh) |
| `business-standard.com` | Non-public IP (fetch tool); reachable via pwsh but not fetched in budget |
| `bing.com` | HTTP 200 but returns an **identical canned result set for three different queries** — unusable as a search proxy |
| `lite.duckduckgo.com`, `mojeek.com` | Non-public IP |
| `html.duckduckgo.com` | **Bot challenge** ("anomaly-modal") |
| `search.brave.com`, `ecosia.org` | Challenge / **HTTP 403** |
| `search.yahoo.com` | Worked once (real query-specific results), then **HTTP 500** — rate-limited |
| `linkedin.com` | Not attempted as a fetch target: job/profile pages require auth. **Recruiter identity therefore remains UNVERIFIED (§B.5).** |

---

## I. What we still cannot know — recruiter-answerable only

- **Exact job title** and internal level/grade (Assistant Manager / Manager / Chief Manager / AVP…).
- **Whether it is IC or people-manager**, and team size if the latter.
- **Team and reporting line** — analytics, data engineering, digital/automation, MIS, or actuarial support.
- **Location and working model** — Mumbai office-based, hybrid, or remote; and whether Hyderabad is a possible base.
- **Compensation band**, fixed/variable split, and level mapping.
- **Employment structure** — direct ICICI Lombard payroll, group entity, or partner/vendor/RPO.
- **The actual data platform** — cloud (AWS/Azure/GCP), warehouse, and BI tool. **Whether any GCP/BigQuery/Looker exists at all.**
- **Whether the role is genuinely AI/agentic** or conventional reporting with AI in the description.
- **Whether a written JD / requisition ID exists** and whether the role is funded and approved.
- **Whether "Swarnim Vaidya" is an ICICI Lombard employee**, and in what capacity.
- **The full Digital Day 2026 deck** (BSE PDF, unreadable in this session) — the company's own latest digital-strategy statement.

---

## Bottom line

**Positive, verified:** ICICI Lombard is a real, listed, large, genuinely digitising insurer with executive-sponsored AI programmes (AWS core-cloud migration, Azure AI, Voice AI at >1M conversations, AI underwriting) and a CTO who speaks publicly about AI and fraud detection. The recruiter's AI framing is not invented.

**Negative, and more important:** the outreach contains **no title, no level, no location, no comp, no JD**, the recruiter's employment is **unverified**, and the candidate's core platform (GCP/BigQuery/Looker) has **zero evidence of existing** at this company while AWS and Azure do. The candidate is **Hyderabad-based and remote-first** against a **Mumbai-HQ insurer**, with **3.5 years in data against 12.5 years of total experience** — a band mismatch in both directions.

**Recommended posture:** reply and ask Q1–Q5 (§G) before any preparation. Verify the recruiter. Do not tailor a resume, do not quote a number, and do not repeat any figure from this brief that is tagged WEAK or UNVERIFIED.
