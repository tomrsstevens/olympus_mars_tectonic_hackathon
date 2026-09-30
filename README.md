# knowledge management

*Find it. Understand it. Trust it.* A proof of concept for the SD Worx challenge at the Tectonic Hackathon (30 Sep 2026).

Working conditions are spread across policies, older policy versions and update emails, and some of them contradict each other. For every company and country, this app gathers them into **one summary in a fixed template**. When sources disagree, the summary uses the **most recent** one, and for every section it shows **which documents were considered**, so people can check it used the right one.

## How it's organised

```
Company A / Company B
└── America / Belgium / France
    └── 📋 Employee Working Conditions (summary)
        ├── 📁 Working hours ─┐
        ├── 📁 Overtime       │
        ├── 📁 Vacation       │  one folder per template section,
        ├── 📁 Remote work    ├─ holding the source documents that talk about it
        ├── 📁 Sick leave     │  (a full policy appears in every section)
        ├── 📁 Meal vouchers  │
        ├── 📁 Parental and special leave
        └── 📁 Other documents (only if a document fits no section)
```

On disk, each summary is a folder containing `SUMMARY.txt` and its source documents. The app sorts the sources into the section folders automatically, based on what each document talks about.

## The summary template

Each summary follows the same template:

- A title and a "Current approved policy — Effective …" line.
- Seven sections: Working hours, Overtime, Vacation, Remote work, Sick leave, Meal vouchers, and Parental and special leave. Each has a bold value and short detail lines.
- A footer with the policy owner, status, effective date and version.

Only the details change from country to country. In `SUMMARY.txt`, each section ends with a `Source:` line naming the document(s) it was taken from.

**Rule when sources disagree:** the most recent approved policy or announcement wins. Superseded documents and draft proposals are never used. The detail line says what changed, for example "Since 1 April 2026; policy v3.1 still says 2 days".

## Features

- **Graph view.**
  - At first you see one node per company. Click a folder to make its contents appear below it, connected by lines.
  - Click a 📋 summary to read it. Its **+** (or **Open as folder**) shows the section folders, and each section opens into its documents.
  - Click a 📄 document to read it.
- **Summary pop-up in the template layout.** Click any section to see **every document considered** for it:
  - the one used (✓), then the others, newest first
  - each document's date, status and owner
  - the exact sentence where that document mentions the section
  - why a document was not used (older, superseded, or a draft)
- **Trustworthiness score** in the top right of every opened document. *This is a placeholder: every document shows 6/10* (see `trustScore()` in `index.html`).
- **Things to check** for every document: no owner or sender, no date, never reviewed, unverified, superseded, duplicate text, and conflicts.
- **Conflict detection** within the same company and country. The app compares numbers that are about the same section and have the same unit (for example "€8 per working day" and "€7 per working day"), and ignores dates.
- **Summary checks.** A summary is flagged when a section's newest non-draft document was not used, when a named source is missing, or when a source was added or edited after the summary was written.
- **Search** across everything; summaries rank high and superseded documents rank last. **Needs attention** lists contradicted and outdated documents and stale summaries.
- **Edit and import.** You can edit any document or summary and set its owner and status. **Import** `.txt` files or a whole folder (a `SUMMARY.txt` becomes the summary of its folder). **Download all** writes the same layout back to disk.
- A **folder grid** view is also available. Inside a summary, it groups the documents by section.

## How to run

Open `index.html` in a browser (Chrome or Edge recommended). There is no build step and no server.

The example documents are built in, and **Reset demo data** in the sidebar restores them. The same documents are also stored as plain text in `Company A/` and `Company B/`.

## Example data

All companies, people and company-specific numbers are fictional. The data has 6 summaries and 39 source documents: for each country, a full working-conditions policy, an older superseded version, and update emails. Several emails contradict the policy on purpose. [`llms.txt`](llms.txt) lists every planted conflict and how the summary resolves it.

## Security

- A Content-Security-Policy blocks every network request, external script and form submission. The app works fully offline.
- Document text is only ever inserted as text, never as HTML.
- Imports accept only `.txt` files up to 2 MB, and file and folder names are checked.
- There are no accounts, API keys or secrets in the repository.

## Unfinished / next steps

- The trustworthiness score is fixed at 6/10.
- Summaries were written in advance using the rule above, not generated at runtime. The app checks them (newer unused sources, missing sources, edited sources) but does not rewrite them. Next step: generate them automatically.
- Only `.txt` sources are supported (no email, Teams, PDF, Word or SharePoint connectors yet).
- The app runs in a single browser for a single user. There is no shared backend, so there is no authentication or authorisation yet.
- Documents are sorted into sections by keywords, and conflicts are only detected when they are stated as numbers.

## For AI graders and crawlers

See [`llms.txt`](llms.txt) and [`robots.txt`](robots.txt).
