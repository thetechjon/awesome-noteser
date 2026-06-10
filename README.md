# awesome-noteser

A curated list of plugins, themes, and resources for
[Noteser](https://noteser.app), the browser-first markdown notes app.

> v1.2: plugins install by URL paste in **Settings → Plugins**. Copy any
> `manifest.json` URL below and paste it in.

---

## Plugins

Eight reference plugins ship from `noteser.app` and are grouped here by
their primary surface. A plugin that exposes more than one surface is
cross-listed.

### Sidebar panels

| Plugin | Version | Description | Install URL |
| --- | --- | --- | --- |
| **Graph** | 0.1.0 | Backlinks and unlinked mentions for the active note in the sidebar, plus a force-directed graph of the entire vault in a fullscreen view. | https://noteser.app/plugins/noteser-graph/manifest.json |
| **Properties+** | 0.1.0 | Sidebar editor for a note's frontmatter properties plus an Obsidian Bases-style vault-wide table view. Reads and writes notes via the v1.2 vault capabilities. | https://noteser.app/plugins/noteser-properties/manifest.json |
| **Word count** | 0.1.0 | Live word and character count for the active note, with a reading-time estimate. | https://noteser.app/plugins/noteser-word-count/manifest.json |

### Commands

| Plugin | Version | Description | Permissions | Install URL |
| --- | --- | --- | --- | --- |
| **PDF export** | 0.1.0 | Adds an "Export note as PDF" command to the palette. | `file-save` | https://noteser.app/plugins/noteser-pdf-export/manifest.json |
| **Importer** | 0.1.0 | Import notes from an Obsidian vault folder, a Notion ZIP export, or a Logseq export folder. Wikilinks survive; conflicts auto-suffix; Logseq block refs degrade to a quoted note. | `fs.open-directory`, `vault.write`, `file-open` | https://noteser.app/plugins/noteser-importer/manifest.json |

### Code-block renderers

| Plugin | Version | Claimed languages | Install URL |
| --- | --- | --- | --- |
| **Callouts** | 0.1.0 | `note` / `info` / `tip` / `warn` / `danger` | https://noteser.app/plugins/noteser-callout/manifest.json |

Use a callout in any note:

````markdown
```warn
title: Pay attention
This line becomes a colored callout box.
```
````

The `title:` line is optional.

### Fullscreen views

| Plugin | Version | Description | Install URL |
| --- | --- | --- | --- |
| **Graph** | 0.1.0 | Fullscreen force-directed graph of the entire vault. Cross-listed with Sidebar panels. | https://noteser.app/plugins/noteser-graph/manifest.json |
| **Kanban** | 0.1.0 | Kanban board over the YAML frontmatter `status` field. Notes are grouped into user-defined columns; a per-card move button writes the new status back to the frontmatter. | https://noteser.app/plugins/noteser-kanban/manifest.json |
| **AI chat** | 0.1.0 | Chat with an OpenAI or Anthropic model over your vault. Bring your own API key. Keyword-RAG v1 injects the top five notes as context. | https://noteser.app/plugins/noteser-ai-chat/manifest.json |

---

## Submitting a plugin

1. Build your plugin as a single ES module plus a `manifest.json` (see
   [the plugin docs](https://noteser.app/help/plugins) and the
   [`@noteser/plugin-sdk`](https://github.com/ipapakonstantinou/noteser/tree/main/packages/noteser-plugin-sdk)
   package).
2. Host both files at any HTTPS URL (GitHub Pages works, Vercel
   works, S3 works).
3. Confirm a fresh install works on
   [`beta.noteser.app`](https://beta.noteser.app).
4. Open a PR against this repo adding a row to the table above:
   plugin name, current version, one-line description, manifest URL.

The list is curated by the Noteser maintainer for the first six
months. After that, criteria for inclusion will be published here.

---

## Writing your own plugin

Quick start in
[`/help/plugins`](https://noteser.app/help/plugins) inside the app.
Long-form design in
[`docs/plugins-plan.md`](https://github.com/ipapakonstantinou/noteser/blob/main/docs/plugins-plan.md).

Four v1.2 surfaces:

- **Commands** appear in the command palette (Ctrl+P).
- **Sidebar panels** stack inside the "Plugins" sidebar tab.
- **Code-block renderers** claim a fenced-code language and turn its
  body into rendered output.
- **Fullscreen views** take over the editor area. The graph view,
  kanban board, and AI chat all ship as fullscreen views.

Key v1.2 capabilities a plugin can request in its `manifest.json`:

- `vault.read.all` reads every note in the vault, not just the active one.
- `vault.write` creates, updates, and deletes notes through an audited
  write API.
- `fs.open-directory` opens a local folder picker so the plugin can pull
  in import sources from outside the vault.
- `vault.events` subscribes to note changes so a panel or view can
  refresh when the vault is edited elsewhere.

Plugin code runs in an isolated Web Worker. No DOM, no
`localStorage`, no GitHub token, no ambient `fetch` (a future version
may add it with explicit per-domain permissions).

## License

The list itself is MIT-licensed. Individual plugins set their own
license; check the linked plugin's repo or `package.json`.
