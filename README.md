# Knowledge Management

A hackathon prototype for exploring company policies in one place. Browse documents by company, country and topic, compare policy versions, and view summaries alongside their sources.

## Open the website

1. Extract the ZIP file.
2. Open the `knowledge-management` folder.
3. Double-click `index.html` to open it in your browser.

No installation, terminal, API key or internet connection is required. Chrome or Edge is recommended for folder import/export support.

## Try the demo

- Use **Folders** or **Graph** to explore the document tree.
- Open **Company A → America → Company Policies** to see the policy demo and its structured/summary views.
- Search for a topic such as payroll, salary or vacation.
- Open **Needs attention** to see the existing review indicators.
- Use **Import files** to add `.txt` documents, or **Import folder** to keep a folder structure.
- Use **Download all** to export your documents.

Changes are saved in this browser's local storage when available. They are not shared with teammates or saved back into `index.html`. Moving the file or using another browser may show a separate workspace. Export anything you want to keep before using **Reset demo data**, which replaces the browser workspace with the built-in examples.

If the Company Policies demo does not appear because the browser has saved an older workspace, export your changes and then select **Reset demo data**.

## Project files

| File | Purpose |
| --- | --- |
| `index.html` | Complete website: HTML, CSS, JavaScript and embedded demo documents. |
| `README.md` | Introduction and instructions. |
| `docs/GITHUB.md` | Upload the project to GitHub and optionally publish a website link. |
| `.gitignore` | Keeps common local files out of Git. |
| `.nojekyll` | Allows GitHub Pages to serve the static project directly. |

## Editing

Open this folder in VS Code and edit `index.html`. Refresh the browser after saving. All application code stays in this single file, so there is no build step or dependency installation.

## Prototype scope

This package preserves the supplied `index_company_policies.html` exactly, renamed to `index.html`. Its design, data and logic are unchanged.

The Company Policies resolved values and trust percentages are predefined demo values. Other review indicators use the file's existing browser-side rules. This is a demonstration, not a validated salary or policy decision system. There is no live AI, Google Cloud connection, backend or automatic messaging in this version.

## Submit or share

Submit this ZIP, or follow [the GitHub guide](docs/GITHUB.md) to upload the extracted project. For a live demo link, the same guide includes GitHub Pages instructions.
