# Resume Generator Guide

How the canonical resumes in `resume/` are rendered to printable HTML, and how
to turn that into a PDF.

> **Rewritten 2026-10-11.** The previous version of this guide documented three
> scripts that **do not exist** in this repository —
> `scripts/generate_resume_variants.js`, `scripts/generate_ats_resume.py` and
> `scripts/generate_resume_node.js`. Every command it gave failed with
> "file not found". Those sections have been removed and replaced with the
> renderer that actually works. See [Removed methods](#removed-methods-do-not-use)
> for the details, so nobody re-adds them by mistake.

---

## The source of truth

| File | Role |
|---|---|
| `resume/Prashanth_Kadasi_AI_Engineer_Resume.md` | Canonical AI Systems Engineer resume |
| `resume/Prashanth_Kadasi_Agentic_AI_Engineer_Resume.md` | Canonical AI / Agentic Engineer resume |
| `resume/Prashanth_Kadasi_AI_Safety_Engineer_Resume.md` | Canonical AI Safety & Evaluation resume |
| `resume/Prashanth_Kadasi_Senior_Data_Analyst_Resume.md` | Canonical Senior Data Analyst resume |

These four Markdown files are the **only** source of truth. Nothing is
hard-coded in the renderer, so you edit the `.md` and re-run — never the script.

---

## ✅ Method 1: `generate_resume_html.py` — the working path

**Prerequisites: none.** Python 3 standard library only. No npm, no Bun, no
Puppeteer, no `python-docx`, no `reportlab`, no `markdown` package, no network.
This is deliberate: those dependencies are not installed on this machine, which
is exactly why the old documented methods never worked.

```bash
# Render all four canonical resumes to resume/html/
python scripts/generate_resume_html.py

# Render just one (case-insensitive substring match on the filename)
python scripts/generate_resume_html.py --only analyst
python scripts/generate_resume_html.py --only safety

# Write somewhere else
python scripts/generate_resume_html.py --out build/html

# Dry run — show what would be rendered, write nothing
python scripts/generate_resume_html.py --list
```

Each run prints what it wrote:

```
Rendering 4 resume(s): D:\JobAgents\resume -> D:\JobAgents\resume\html
  OK    Prashanth_Kadasi_Agentic_AI_Engineer_Resume.html  (15,725 bytes)
  OK    Prashanth_Kadasi_AI_Engineer_Resume.html  (15,676 bytes)
  OK    Prashanth_Kadasi_AI_Safety_Engineer_Resume.html  (15,461 bytes)
  OK    Prashanth_Kadasi_Senior_Data_Analyst_Resume.html  (14,452 bytes)

Wrote 4/4 file(s) to D:\JobAgents\resume\html
Open one in a browser and press Ctrl+P (Print / Save as PDF).
```

**Output:** one self-contained `.html` per resume in `resume/html/`.

| Property | Value |
|---|---|
| Dependencies | none (Python stdlib only) |
| External requests | **zero** — CSS is inlined, no fonts, no images, no JS |
| Works from `file://` | yes, online or offline |
| Deterministic | yes — byte-identical output for identical input |

### Printing to PDF

Open the HTML file in any browser and press **Ctrl+P** → choose
**"Save as PDF"** as the destination. The print stylesheet sets an `@page` A4
rule, right-aligns dates, and avoids breaking headings and bullets across
pages. No PDF toolchain is needed.

To switch to US Letter, use the browser's own paper-size dropdown in the print
dialog — the 12 mm / 14 mm margins sit safely inside both A4 and Letter, so
nothing is clipped either way.

### What the parser handles

The renderer is generic — it reads the Markdown structure, not the text:

| Markdown | Rendered as |
|---|---|
| `# NAME` | Candidate name (centred, largest) |
| line right after the name | Professional title |
| contact line(s) before the first heading | Centred contact block |
| `### SECTION` / `## SECTION` | Ruled, uppercase section heading |
| `**bold**`, `*italic*`, `` `code` `` | `<b>`, `<i>`, `<code>` |
| `[text](url)` and bare domains | Real clickable `<a href>` |
| `-` / `*` / `•` bullets | Bullets, `break-inside: avoid` |
| `> quote` | Left-ruled italic note |
| `**Org** — *Role* \| Location` | Employer header, **date right-aligned** |
| Markdown tables | Real `<table>` |

Employer headers are recognised in **both** layouts the resumes use, so the
date is right-aligned either way:

```markdown
**Black Piano** — *Data Analyst* | Remote          <!-- one-line form -->
**Mar 2026 – Present**

**Optum (UnitedHealth Group)** — *Role* | Hyderabad, India | **Apr 2014 – Mar 2023**
```

### Unicode

The output is written as UTF-8 with `<meta charset="UTF-8">`, so `—` (em dash),
`→` (arrow), `–` (en dash) and `•` (bullet) all survive. Do **not** replace
them with ASCII to work around encoding problems — there are none.

### Page-count reality check

The renderer does **not** auto-shrink text to force one page — that would
silently change your resume. It prints what the Markdown says.

As measured on 2026-10-11, all four canonical resumes run to **2 pages at A4**,
with roughly 270 px of genuine overflow onto page 2 (content is ~1305 px tall
against a ~1032 px single-page content box). The second page holds real content,
not stray whitespace — so this is a content-length issue in the Markdown, not a
styling bug.

If you want one page, edit the Markdown (the source of truth) — trim the
summary, drop the weakest bullet per section, or shorten project descriptions.
Do not hand-edit `resume/html/*.html`: the next run overwrites it.

To fit more on a page without cutting content, use the browser's print dialog
(scale / margins) or switch to a larger paper size. Verify the result in the
print preview before saving.

---

## Method 2: JobAgents viewer (pipeline output only)

This is a **different** tool for a **different** set of files. It renders the
pipeline's tailored resumes from `generated/*.md`, not the hand-authored
canonical resumes in `resume/`. It is real, stdlib-only, and already wired into
the pipeline as the `render` stage.

```bash
python -m jobagents resumes --list          # index of every resume found
python -m jobagents resumes --build --open  # ONE self-contained printable HTML
python -m jobagents resumes --render 9653   # one resume, by job id or filename
python -m jobagents resumes --build --page Letter --no-scratch
```

| Route | What it is |
|---|---|
| `python -m jobagents resumes --build` | Writes `site/resumes.html` — every resume in one offline file |
| `/resumes` on the dashboard | Card index, click through to a printable page |
| `/resume/<key>` | One resume as a printable page (A4/Letter) |
| `/api/resumes` | JSON index |

Implementation: `jobagents/resume_view.py`.

> **Which method do I want?** Editing the four canonical resumes in `resume/` →
> **Method 1**. Want every pipeline-generated resume in one browsable offline
> bundle → **Method 2**.

---

## Removed methods (do not use)

These were documented here previously and **never worked** — the files do not
exist. They have been deleted from this guide rather than left as a trap:

| Removed command | Why it was removed |
|---|---|
| `python scripts/generate_ats_resume.py` | File does not exist. Also required `python-docx` + `reportlab`, neither installed. |
| `bun run scripts/generate_resume_variants.js` | File does not exist. Required Bun/Node + `puppeteer-core` + `docx`. |
| `bun run scripts/generate_resume_node.js` | File does not exist. Required a local `scripts/node_modules` install. |
| `cp scripts/generate_resume_node.package.json package.json` | That manifest does not exist either. |

The one Node renderer that *is* in the tree,
`scripts/render_generated_resumes.js`, still requires `puppeteer-core` and
`docx` from an **absolute path inside a different project**
(`C:/Users/hplap/Desktop/Projects_rash/kprsnt.in/scripts/node_modules`). It
cannot run here, and it targets `generated/`, not `resume/`. It is superseded by
Method 2 for that job.

**DOCX is not available.** There is no working DOCX path in this repository.
If an ATS portal demands `.docx`, paste the Markdown source into Word and save
it there — the Markdown is the source of truth and copies cleanly.

---

## Editing workflow

1. Edit the Markdown in `resume/*.md` — this is the only place content lives.
2. Run `python scripts/generate_resume_html.py`.
3. Open `resume/html/<name>.html` in a browser, check the print preview.
4. Ctrl+P → Save as PDF.

Never edit `resume/html/*.html` by hand: it is generated output and the next run
overwrites it.

---

## Pre-flight checklist before sending

- [ ] Dates are accurate and non-ambiguous
- [ ] Title does not inflate rank (no "Staff / Founding" unless literally true)
- [ ] Employer headers show a right-aligned date in the rendered HTML
- [ ] Contact line: email, phone, and all portfolio links are present and clickable
- [ ] No fabricated metrics — verified profile ground truth only
- [ ] Print preview fits the page count you want (currently 2 pages at A4 — see
      [Page-count reality check](#page-count-reality-check))
- [ ] The four HTML files were regenerated **after** the last Markdown edit
      (check timestamps: `.md` must not be newer than `.html`)

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `no resumes found in …` | You are pointing `--src` at a directory with no `*.md` resumes. |
| HTML looks out of date | Re-run the generator; `.md` was edited after the last render. |
| Bullets/arrows look wrong | Ensure you view the file as UTF-8; the output declares `<meta charset="UTF-8">`. |
| PDF spills to a second page | Content is genuinely long — trim the Markdown (source of truth). See [Page-count reality check](#page-count-reality-check). |
| Links not clickable in the PDF | Check the HTML has `<a href="…">` — Markdown links and bare domains are both auto-linked. |
| Need `.docx` | Not supported — paste the Markdown into Word. See above. |
| `python` not found | Install Python 3, or use the browser-print route from an already-generated HTML. |

---

*Last updated: 2026-10-11*
