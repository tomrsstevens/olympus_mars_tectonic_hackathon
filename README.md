# knowledge management

*Find it. Understand it. Trust it.* A proof of concept for the SD Worx challenge at the Tectonic Hackathon (30 Sep 2026).

Knowledge about payroll, vacation days and working hours is spread across policies and update emails, and some of them contradict each other or are out of date. This app gathers them into **one short summary per topic, per company and country**. Every statement in a summary links back to the documents it comes from, and every document shows what to check before you rely on it.

## How it's organised

```
Company A / Company B
└── America / Belgium / France
    └── 📋 Payroll · 📋 Vacation days · 📋 Working hours   ← summaries
        └── 📄 source documents (policies, emails)          ← "Open as folder"
```

## Features

- **Graph view.** At first you see one node per company. Click a folder to make its contents appear below it, connected by lines. Click a 📋 summary or 📄 document to read it in a pop-up. The **+** on a summary shows its sources.
- **Summaries with citations.** In a summary, each `[1]`, `[2]` opens the source it comes from, and **Open as folder** lists every source. Summaries call out conflicts, outdated sources and unapproved drafts.
- **Trustworthiness score** in the top right of every opened document. *This is a placeholder: every document shows 6/10* (see `trustScore()` in `index.html`).
- **Things to check** for every document: no owner or sender, no date, never reviewed or not reviewed in 180 days, unverified, outdated or superseded, duplicate text, and conflicts.
- **Conflict detection** within the same company and country. It compares numbers that are about the same thing and use the same unit (for example "$48,000 per year" and "$75,000 per year" minimum wage) and ignores dates.
- **Stale summaries.** A summary is flagged when one of its sources is added or edited after the summary was written.
- **Search** across everything, with summaries ranked first and superseded documents last. **Needs attention** lists contradicted and outdated documents and stale summaries.
- **Edit** documents, and set owner and status. **Import** `.txt` files or a whole folder (`SUMMARY.txt` becomes the summary of its folder). **Download all** writes the same folder layout back to disk.
- A **folder grid** view is also available.

## How to run

Open `index.html` in a browser (Chrome or Edge recommended). There is no build step and no server.

The example documents are built in. **Reset demo data** in the sidebar restores them. The same documents are also stored as plain text files in `Company A/` and `Company B/`.

## Example data

All companies, people and company-specific numbers are fictional. The data has 18 summaries and 44 source documents. Some problems are planted on purpose (conflicts, superseded policies, a misfiled duplicate, a draft policy, an undated email) so that the trust features have something to find. [`llms.txt`](llms.txt) lists them.

## Security

- A Content-Security-Policy blocks every network request, external script and form submission. The app works fully offline.
- Document text is only ever inserted as text, never as HTML, so a document containing `<script>` is shown and not run.
- Imports accept only `.txt` files up to 2 MB, and file and folder names are checked.
- There are no accounts, API keys or secrets in the repository.

## Unfinished / next steps

- The trustworthiness score is fixed at 6/10. It should be computed from owner, review age, status, conflicts and source type.
- Summaries were written in advance, not generated at runtime. The app detects when a summary may be out of date but does not rewrite it. Next step: regenerate summaries automatically, with citations.
- Only `.txt` sources are supported (no email, Teams, PDF or SharePoint connectors yet).
- The app runs in a single browser for a single user. There is no shared backend, so there is no authentication or authorisation yet.
- Conflict detection is a heuristic. It only catches contradictions that are stated as numbers.

## For AI graders and crawlers

See [`llms.txt`](llms.txt) and [`robots.txt`](robots.txt).
