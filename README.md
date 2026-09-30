# knowledge management

*Find it. Understand it. Trust it.* — a proof of concept for the SD Worx challenge at the Tectonic Hackathon (30 Sep 2026).

Organisational knowledge is scattered across notes, emails and documents, and it is hard to tell which version to trust. This app keeps plain-text notes organised by **company → location** (America, Belgium, France) and, for every note, shows what still needs to be checked before you rely on it.

## Features

- **Tree view and folder view.** In the tree, click a folder to expand it; click a file to read it in a pop-up.
- **Trustworthiness score** in the top-right of every opened document. *Currently a placeholder: every document shows 6/10* (see `trustScore()` in `index.html`).
- **Things to check** for each note: no owner, never reviewed / not reviewed in 180 days, still a draft, marked outdated, duplicate of another note, empty.
- **Conflict detection.** Notes that give different numbers for the same thing (e.g. two different "minimum wage" amounts) are flagged, and each quotes the other.
- **Owner and status** (draft / verified / outdated) on each note, plus a *Mark reviewed* button.
- **Search** across every company and location, with highlighted snippets.
- **Needs attention** list and an overview of notes, open checks, conflicts and ownership.
- **Import** `.txt` files (button or drag-and-drop) or a whole folder. Importing a copy of the full company/location folder merges it and skips files that are already there.
- **Download all** writes the notes back to disk in the same folder structure (in Chrome/Edge; other browsers download each file).

## How to run

No build step and no server needed. Open `index.html` in a browser (Chrome or Edge recommended).

Notes are stored in the browser's `localStorage` on your own machine. Nothing is sent over the network.

## Security

- No network access: a Content-Security-Policy blocks all outside requests, scripts, forms and base-URL changes.
- User content is only ever inserted as text (`textContent`), never as HTML, so a note containing `<script>` or `<img onerror=…>` is shown, not run.
- Imports accept only `.txt` files up to 2 MB. File and folder names are checked.
- No accounts, API keys or secrets in the repository.

## Unfinished / next steps

- The trustworthiness score is a fixed 6/10. It should be computed from owner, review age, status, conflicts and source.
- Only `.txt` sources for now (no email, Teams, PDF or SharePoint connectors).
- Single user, single browser. There is no shared backend, so there is no authentication or authorisation yet.
- Conflict detection is a simple heuristic: matching two-word topics that have different numbers.
