# Outreach Templates

Copy-paste-ready templates for cold outreach. Generic and reusable — fill in the
five placeholders per role (see §5).

**Ground rules:** every number below traces to the reconciled metrics in
`config/profile.md` (2026-10-11). Lead with what a client or team actually used,
not with a keyword list. Nothing here is auto-sent; a human copies, personalises,
and sends.

---

## 1. Cold email to a hiring team

**Subject:** `{{role}} — Data Analyst, BigQuery + Looker Studio pipelines`

```
Hi {{name}},

I'm applying for {{role}} at {{company}}.

At Black Piano I build the pipelines behind client dashboards — 18 automated ETL
pipelines feeding BigQuery and Looker Studio across 18 industry sectors. Before
that, at Pi Software Solutions, I built production Python pipelines (internal
Pi-API package) for automated BigQuery access across 10+ client dashboards and
delivered 30+ analytical reports for US and UK clients.

I noticed {{keyword}} in the posting — that's the work I do most often:
{{keyword_sentence}}.

I also build independent, self-directed data systems — including a sourcing
pipeline that resolved 7,613 jobs / 5,854 distinct roles from 10 sources with
1,759 duplicates merged, scoring 22,839 matches with zero model calls. Those are
my own projects, not client work.

Earlier I spent 9 years at Optum auditing CMS enrollment transactions — where I
learned to treat data quality as a gate, not a report.

Happy to walk through any of this. Resume attached.

Best regards,
Prashanth Kumar Kadasi
kprsnt@live.com · +91-9948311964 · https://kprsnt.in
```

---

## 2. LinkedIn connection note

**Hard limit: 300 characters including spaces and the sign-off** (this version is
247). If you need room, drop the `30+ reports at Pi Software` clause first.

```
Hi {{name}} — Data Analyst, 3.5+ yrs building BigQuery/Looker pipelines: 18 automated ETL pipelines across 18 sectors at Black Piano, 30+ reports at Pi Software. Interested in {{role}} at {{company}} — {{keyword}} is the work I do daily. Prashanth
```

---

## 3. LinkedIn DM to a recruiter

**Roughly 400–600 characters.** More room than a connection note, so name one
concrete production outcome and one honest project detail.

```
Hi {{name}}, thanks for connecting. I'm interested in {{role}} at {{company}}.

Quick context: I'm a Data Analyst with 3.5+ years in production data work. At Black Piano I own 18 automated ETL pipelines into BigQuery feeding Looker Studio dashboards across 18 sectors; at Pi Software I built Python pipelines across 10+ client dashboards and wrote 30+ analytical reports for US/UK clients.

Your posting mentions {{keyword}} — that's squarely what I do. Open to a short call?

Prashanth · kprsnt@live.com · https://kprsnt.in
```

---

## 4. X / Twitter DM

**Roughly 200–280 characters.** Shortest form; one proof point only.

```
Hi {{name}} — Data Analyst here (3.5+ yrs). I build BigQuery + Looker pipelines: 18 automated ETL pipelines across 18 sectors at Black Piano. Keen on {{role}} at {{company}} — {{keyword}}. Portfolio: https://kprsnt.in
```

---

## 5. How to personalise

Swap **two or three tokens per role** and leave the rest alone. The templates are
deliberately generic in the middle so that only these change:

| Token | What to put there | Where to find it |
|---|---|---|
| `{{company}}` | The company you're writing to | The posting |
| `{{role}}` | The **exact** job title from the posting | The posting |
| `{{name}}` | The recruiter or hiring manager's first name | LinkedIn / the posting |
| `{{keyword}}` | **One** skill or tool the posting emphasises that you genuinely have | The requirements section |
| `{{keyword_sentence}}` | One sentence connecting that keyword to real work you did | Your own history |

Guidance:

- **One keyword, not five.** Pick the single requirement you can back with a
  production example. `{{keyword_sentence}}` exists so you say *what you did*
  with it, not that you know it.
- **Only claim what you actually used.** If the posting wants Tableau and you
  have used it, say so. If it wants dbt and you have not, leave it out — the
  resume carries the real stack and an interview will find the gap anyway.
- **Do not touch the numbers.** They are the verified set. If a number is not in
  `config/profile.md`, it does not go in the message.
- **Keep the projects labelled as projects.** The independent work
  (JobAgents, AgentSwarm, BugAgents, AI Eco, mSeat, BrandXY) is self-directed,
  not client or employer work. Say so, as the templates do.

---

## 6. Never say this

| Never write | Why |
|---|---|
| "Staff / Principal / Founding Engineer", "Head of Data" | The real titles are **Data Analyst** at both Black Piano and Pi Software. There is no seniority to inflate. |
| "Agentic AI Systems Engineer" as a held job title | Not an employment title. It may describe a *direction*, never a job held. |
| "My pipeline serves 10,000 users" / "drove $X revenue" / "grew adoption" | There are no production users, revenue, customers, or adoption figures. None. |
| "My findings were disclosed / accepted / paid / resolved" | BugAgents findings are **submission-ready drafts**. Nothing has been submitted and no bounty exists. |
| Naming the BugAgents vendor, program, asset, or vulnerability class | Withheld pending responsible disclosure. Cite the project and severity only, or omit entirely. |
| "My paper was peer-reviewed" / "published in a journal" | Paper 1 is a **Zenodo preprint** (DOI 10.5281/zenodo.23232189) — not peer-reviewed, not a journal. Paper 2 is a **manuscript, not submitted**. |
| "I authored the cosmology papers" | The agent authors are `A001_DarkMatter` / `A002_QuantumCosmos`. You built the system that wrote them; you are not the paper author. |
| Any number not in `config/profile.md` | Superseded figures are actively misleading. `config/profile.md` carries a binding "Stale values — do not use" list; treat every number there as deleted. If it is not in the current metrics table, it does not go in the message. |
| Any "enterprise dashboards" count | Superseded wording. The verified figure is **10+ client dashboards** at Pi Software. |
| Any BugAgents report count above the promoted total | Superseded. BugAgents promoted **2 reports** from **8 findings**; the remainder were filter refusals. |
| A wall of tools with no outcome | Keyword soup reads as a template. One tool, one outcome, per sentence. |
| "Dear Sir/Madam", "To Whom It May Concern" | Use a real name, or "Hi {{company}} hiring team". |
| Claims about clients you cannot name | Client confidentiality. Describe the work, not the client list. |
