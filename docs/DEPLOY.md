# Vercel deployment

Deploys `site/` — the static dashboard snapshot **and** the engineering blog — as
a live URL.

Two things ship from the same Vercel project:

| Path | What it is | Indexed? |
|---|---|---|
| `site/index.html` | The dashboard snapshot (aggregate pipeline metrics) | **No** — `noindex, nofollow` |
| `site/blog/` | The engineering blog series (6 static pages) | **Yes** — `index, follow` |

The dashboard is deliberately unlisted; the blog is deliberately indexable. See
[Header scope](#header-scope-dashboard-vs-blog) below for where that is set.

---

## What gets deployed

A **single self-contained HTML file** (about 22 KB). It has no server, no
database, and no external requests. All charts are inline SVG.

It shows aggregate pipeline metrics: jobs sourced, distinct roles, duplicate
merges, source coverage, score distribution, top hiring brands, seniority mix,
remote split, and posting freshness.

It does **not** contain:

- your name, email, phone, or profile links
- individual job listings or company names you applied to
- application status or outreach drafts

Verified: zero occurrences of personal data in the generated file.

---

## Deploy

### Option A — CLI (fastest, no dashboard setup)

```powershell
# Install once
npm install -g vercel

# From the repo root
cd D:\JobAgents
vercel deploy --prebuilt=false
```

The first run asks you to log in and confirm the project. Accept the defaults.
Vercel prints a preview URL.

To promote to production:

```powershell
vercel deploy --prod
```

### Option B — Git integration

1. Go to <https://vercel.com/new>.
2. Import `kprsnt2/JobAgents`.
3. Set **Root Directory** to `site`.
4. Framework Preset: **Other**. Build Command: leave empty.
   Output Directory: `.` (the `site` folder itself).
5. Deploy.

**Note on private repos:** Vercel's free (Hobby) plan cannot connect to a
**private** Git repository — that needs Pro. If you stay on Hobby, use Option A
(CLI), which uploads the files directly and does not require repo access.

---

## The blog (`site/blog/`)

The engineering blog is six self-contained static HTML pages:

```
site/blog/
  index.html                        the series index — posts in order, 01 → 05
  01-jobagents.html
  02-agentswarm.html
  03-bugagents.html
  04-engineering-findings.html
  05-what-agents-discovered.html
```

Same constraints as the dashboard: inline CSS only, no external CSS, no fonts,
no CDN, no JavaScript frameworks, no network requests. The pages reuse the
dashboard's exact CSS custom properties, so the two look like one site.

### Source of truth

**The Markdown in `docs/blog/` is the source. `site/blog/*.html` is the published
artifact.**

| Layer | Path | Role |
|---|---|---|
| Source | `docs/blog/*.md` | Edit here. Reviewable, diffable, plain text. |
| Published | `site/blog/*.html` | Generated from the Markdown. What Vercel serves. |

To update the blog: edit the Markdown in `docs/blog/`, then convert it to
`site/blog/` HTML, then deploy. Do not edit the HTML directly — the next
conversion overwrites it.

> **Note.** There is currently **no automated converter script** in this repo.
> The conversion was done by hand when the series was first published. If the
> blog becomes a recurring thing, that is the first thing worth automating —
> otherwise the Markdown and the HTML will drift.

### A pipeline run cannot clobber the blog

`python -m jobagents export` writes **only** `site/index.html`. It does not
touch `site/blog/` or any other file in `site/`. So the daily pipeline can
regenerate the dashboard freely without endangering the blog.

This matters because `export` is the last stage of `jobagents run`: a scheduled
09:00 run rewrites the dashboard snapshot every morning. The blog is outside that
blast radius by construction.

### Deploying

```powershell
cd D:\JobAgents
vercel deploy --prod
```

Both the dashboard and the blog deploy together, because Vercel's Root Directory
is `site` — it serves the whole folder.

---

## Header scope: dashboard vs blog

`vercel.json` sets headers for two path scopes. **Order matters:** Vercel
evaluates the `headers` array in order and the **last matching rule wins**.

| Order | Source | `X-Robots-Tag` | Why |
|---|---|---|---|
| 1 | `/(.*)` | `noindex, nofollow` | Catch-all. Keeps the dashboard unlisted. |
| 2 | `/blog/(.*)` | `index, follow` | Overrides the catch-all for blog pages. |
| 3 | `/blog` | `index, follow` | The index path itself (no trailing segment). |

All three scopes also carry `X-Content-Type-Options: nosniff`,
`Referrer-Policy: no-referrer`, and `X-Frame-Options: DENY`. Only the robots
header differs.

**If you reorder these, the blog silently becomes unindexable again.** Rule 2
must come after rule 1. `cleanUrls: true` means `/blog/01-jobagents.html` is
served at `/blog/01-jobagents`, and `/blog/index.html` at `/blog`.

### CRITICAL: never link with a `.html` extension

`cleanUrls: true` makes Vercel serve pages **only** at the extensionless path.
The `.html` form returns **404, not a redirect**:

| URL | Result |
|---|---|
| `/blog/` | 200 |
| `/blog/01-jobagents` | 200 |
| `/blog/01-jobagents.html` | **404** |

So every internal link must be written **without** the extension:

```html
<!-- correct -->
<a href="01-jobagents">...</a>
<a href="./">Series index</a>
<a href="../">JobAgents dashboard</a>

<!-- WRONG - these 404 in a real browser -->
<a href="01-jobagents.html">...</a>
<a href="index.html">Series index</a>
<a href="../index.html">JobAgents dashboard</a>
```

This is an easy mistake to make and a confusing one to debug, because the page
works perfectly when you open it from the filesystem (`file://`) — only the
deployed site 404s. **A local preview will not catch it.**

Verify after any edit:

```powershell
# must return no matches
Select-String -Path site\blog\*.html -Pattern 'href="[^"]*\.html"'
```

---

## vercel.json scope

Keep this file minimal. Vercel's schema rejects several properties that older
docs and tutorials still show:

| Property | Status |
|---|---|
| ame\ | **Rejected** — set the Project Name in the dashboard instead |
| \public\ | **Rejected** — removed from the schema |
| \uilds\, outes\, \env\ | Deprecated — use ewrites\, \headers\, \env\ in project settings |

A minimal, valid file only needs \headers\ (and optionally \cleanUrls\).
The error looks like:

    Invalid request: should NOT have additional property 'public'.

---

## Updating the snapshot

The daily pipeline regenerates the **dashboard** automatically. `export` is the
last stage:

```powershell
python -m jobagents run              # includes the export stage
python -m jobagents export           # or just refresh the dashboard
vercel deploy --prod                 # push the new snapshot
```

This does **not** rebuild the blog — `export` writes only `site/index.html`. To
update the blog, edit `docs/blog/*.md`, reconvert to `site/blog/*.html`, then
deploy. See [The blog](#the-blog-siteblog) above.

To automate the deploy too, add this to the end of `scripts/run_daily.ps1`:

```powershell
if (Get-Command vercel -ErrorAction SilentlyContinue) {
    vercel deploy --prod --yes 2>&1 | Add-Content $LogFile
}
```

Note this deploys the whole `site/` folder, so it also republishes whatever blog
HTML is currently on disk. If you are mid-edit on a blog post, finish the
conversion before the 09:00 run.

---

## Privacy

**The dashboard** (`site/index.html`) carries `X-Robots-Tag: noindex, nofollow`,
so search engines will not index it. The URL is still publicly reachable by
anyone who has it — treat it as "unlisted", not "private".

**The blog** (`site/blog/`) is deliberately **indexable** (`index, follow`). That
is the point of publishing it: a blog post nobody can find has no value to a
reader or a recruiter. Treat every blog page as fully public.

If you need true access control on the dashboard, enable **Vercel
Authentication** in Project Settings → Deployment Protection. That is available
on Hobby for preview deployments and on Pro for production. Note that this would
also gate the blog if applied project-wide.

**Do not** put anything in `site/` that you would not paste into a public
message. That applies to the blog in particular — it is indexed, cached, and
archived.

The BugAgents post is disclosure-safe by editorial rule, not by code: the
`tailor.py` disclosure guard covers **resume text only** and does not scan
`docs/blog/` or `site/blog/`. Nothing will stop you from publishing a vendor
name in a blog post. Check it yourself before deploying.
