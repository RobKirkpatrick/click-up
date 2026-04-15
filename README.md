# Go Nimbly × ClickUp Intelligence

A local browser tool for generating project documentation, weekly summaries, and living artifacts directly from your ClickUp data — no backend required.

---

## What it does

Open `index.html` in Chrome and walk through a guided 5-step flow:

1. **Auth** — paste your ClickUp personal API token and (optionally) a Claude API key
2. **Workspace** — pick your ClickUp workspace
3. **Project** — choose a Space, then search and select a List
4. **Output** — choose what to generate, optionally tune the AI prompt
5. **Generate** — fetches all tasks + comments, writes your document

All credentials stay in your browser tab. Nothing is sent to any server except ClickUp's API and Anthropic's API (if you provide a Claude key).

---

## Output types

| Type | Description |
|---|---|
| **Full Project Document** | Keystone artifact — every task, status, assignee, description, and full comment thread mapped as context and decision points |
| **Weekly Summary** | Tasks completed, in progress, and blocked in the last 7 days — built for standups and stakeholder updates |
| **Status Report** | Completion rate, status breakdown, open due dates, and blockers at a glance |
| **Decision Log** | Extracts substantive decisions and open questions from comment threads across the entire project |

If a Claude API key is provided, output is AI-written narrative markdown. Without one, the tool produces clean structured exports from the raw data.

---

## Prompt customization

Each output type exposes a **Customize Prompt** accordion on the output selection screen. You can edit:

- **System Prompt** — the role and instructions Claude follows
- **User Prompt Template** — the specific request sent per generation run

Templates support these variables:

| Variable | Value |
|---|---|
| `{{project}}` | Name of the selected ClickUp list |
| `{{workspace}}` | Workspace name |
| `{{space}}` | Space name |
| `{{date}}` | Generation timestamp |
| `{{count}}` | Total task count |
| `{{tasks}}` | Full task + comment data block |

Edits persist for the browser session. Use **Reset to default** to restore the original prompt.

---

## Google Docs integration

Paste a Google Doc URL in the output step. After generating, a **Copy Apps Script** button provides a snippet you paste into your doc via Extensions → Apps Script. Running it rewrites the document's content with your latest generation — no OAuth flow or backend needed.

For teams that want the doc to update automatically on a schedule, the Apps Script can be extended with a time-based trigger calling a Sheets/Apps Script webhook.

---

## Getting started

### 1. Get your ClickUp API token
Settings → My Settings → Apps → **Generate API Token**
`https://app.clickup.com/settings/apps`

### 2. Get a Claude API key (optional)
`https://console.anthropic.com/settings/keys`

### 3. Open the tool
Double-click `index.html` or open it in Chrome via `File → Open File`.

> **Note:** If your browser blocks the ClickUp API due to CORS on a `file://` URL, serve the file locally:
> ```bash
> npx serve .
> # then open http://localhost:3000
> ```

---

## Project structure

```
click-up/
├── index.html   # The entire application — one self-contained file
└── README.md
```

---

## Roadmap / ideas

- [ ] Multi-list selection for cross-project documents
- [ ] Scheduled auto-generation via the Cowork schedule skill
- [ ] Direct Google Docs push via OAuth (PKCE flow, no backend)
- [ ] ClickUp webhook listener to trigger re-generation on task updates
- [ ] Saved prompt presets per team member
- [ ] Export to `.docx` via the docx skill
