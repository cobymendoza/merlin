# Merlin — Prospect Research Mission Control

**Merlin** is a small, static web app that turns "find me clients" into a rigorous,
repeatable research operation. You describe who you are and who you want to reach;
Merlin writes a **master research prompt** that any AI platform — ChatGPT, Claude,
Codex, Muse — can execute to scour the internet for prospect clients: published,
verified emails, official websites, and Instagram handles. The results come back
structured exactly like a gold-standard outreach workbook, and Merlin's Results
Viewer receives them in a friendly CRM-style desk with search, filters and export.

"Merlin" is simply the product's name. The app is platform-agnostic and
person-agnostic: it works for any user, with any AI platform, in any industry. The
architecture it enforces mirrors two reference implementations — a pair of ski-resort
outreach workbooks (US and Canada editions) built to this same gold standard.

## Who it's for

Freelancers, studios and small agencies who sell a service and need a defensible
prospect list: every email published and sourced, every Instagram handle checked,
nothing guessed, nothing duplicated. One day the user is a creative producer
pitching commercial films to ski resorts; the next, a designer pitching gyms,
coffee brands or law firms. The brief builder does not care — the standard is the
same for every industry.

## The flow

1. **Brief Builder** — Enter your name, business, role, what you sell, the target
   industry, sub-niche, geography, prospect type and target count. Choose which data
   to collect per prospect. The quality rules are fixed: published emails only, never
   guessed; multi-source verification; dedupe; suppression respected.
2. **Prompt Generator** — Merlin generates the complete master research prompt.
   Copy it, paste it into ChatGPT, Claude or Codex, and run it. The prompt encodes
   the **Super Intelligence research standard** (never settle for the first pass;
   official sites, press releases with media contacts, page source / JSON-LD, team
   pages, directories and review platforms, cross-checked until the realistic ceiling
   is reached) and the gold-standard workbook structure below.
3. **Run the research** — the AI platform does the legwork and returns tab-ready
   tables (CSV/TSV) in the workbook architecture.
4. **Results Viewer (CRM)** — Paste the Contacts table back into Merlin (or load the
   built-in sample) to search, filter by Instagram verification and outreach status,
   and read prospects as cards or a grid. Export again as a gold-standard Contacts
   CSV, plus a `TEMPLATE.md` describing the full workbook structure.

## The gold-standard architecture

Every Merlin run produces a workbook with seven tabs, modelled on the reference
ski-resort outreach workbooks (US and Canada editions):

| Tab | What it holds |
| --- | --- |
| **About** | Purpose, scope, research date, headline counts, how to use, the verification boundary, the SENDING RULES, and operator attribution. |
| **Contacts** | The master list: one row per unique published email, with source URL, evidence type, Record ID, Checked date, Notes with status history, Outreach status and Sent by among its 34 columns. |
| **Directory** | Every business found, contacted or not, with official website, phone, and the Instagram handle with its verification label and notes. |
| **Held contacts** | Closed, paused, ineligible or unverifiable prospects, parked with a reason — never deleted. |
| **Coverage rollup** | Per-region counts: directory entries, unique contacts, primary contacts, areas without email. |
| **Activity log** | Every action on the workbook, with "Recorded by" naming the operator who did it. |
| **Suppression register** | Addresses and domains that must never be contacted (dead domains, double failures, do-not-contact), honoured across workbooks. |

Instagram verification is always one of three honest labels: **Verified** (confirmed
as the business's own account from an official source), **Probable** (a strong
candidate that could not be confirmed — the doubt is written in the notes), or
**Not found** (searched; no official account established — a fan or template account
is not a handle).

See [`TEMPLATE.md`](TEMPLATE.md) for the exact column order of every tab.

## Cross-platform verification loop

Research is only as good as its checking. Merlin's workflow therefore builds in a
second, independent pass by a **different** AI platform than the one that did the
research:

1. The researcher platform (any AI — ChatGPT, Claude, Codex, or another) runs the
   master prompt and fills the sheet.
2. The sheet is shared — with **edit access** — to the account that a second,
   independent AI platform uses.
3. The verifying platform independently checks the record: it re-opens the source
   URL behind each published email to confirm the address is real and belongs to
   that business, checks that Instagram handles exist and match the business with
   honest labels, and hunts for duplicates and suppressed addresses that slipped in.
4. The verifying platform **writes its findings back into the same record**: it
   updates the Checked date and the verification/status fields, **appends** to Notes
   (verification never overwrites the original researcher's notes — history is
   preserved), and logs the verification pass in the Activity log with
   **Recorded by** naming the verifying platform/operator.

**Practical step:** when the researching AI delivers the workbook as a Google
Sheet, share that Sheet with **edit access** to the Google account the verifying AI
platform operates under. A read-only share, a PDF, or a locked export breaks the
loop — the checker must be able to write back into the living record.

## What Merlin does *not* do

Merlin performs **no scraping, no sending and no enrichment** of its own. There is
no backend and no database. Merlin is the guide and the results desk: it writes the
brief, enforces the standard, receives the results, and presents them cleanly. The
AI platform you choose does the research; the workbook is the system of record.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The app shell — Brief Builder, Prompt Generator, Results Viewer. |
| `styles.css` | All styling. No external assets; works offline. |
| `app.js` | The data model (gold-standard columns), prompt generator, CSV parser, viewer, filters and exporters. |
| `sample-data.csv` | Six clearly-labelled fictional sample rows in the Contacts format, so the Results Viewer demos immediately. |
| `TEMPLATE.md` | The seven-tab workbook specification with exact column orders. |
| `README.md` | This file. |

## Run it

- **Simplest:** open `index.html` in any modern browser. Everything runs locally.
- **GitHub Pages:** in the repo, go to *Settings → Pages*, choose *Deploy from a
  branch*, branch `main`, folder `/ (root)`. The app is published as a static site —
  no build step.
- **Any static host:** copy the five app files anywhere static files are served.

Tip: on `file://` some browsers block the "Load sample data" fetch of
`sample-data.csv`; Merlin automatically falls back to an embedded copy of the same
sample, so the demo works either way.

## A note on credit

"Merlin" is only the product's name — it claims no identity and represents no
person or assistant. Credit for actual work lives where it belongs: inside the
workbook itself. Whoever or whichever platform researches a row is the researcher
of record; whoever verifies it signs the Activity log under **Recorded by**. The
sheet, not the app, keeps the names.
