# awesome-noteser

A curated list of plugins, themes, and resources for
[Noteser](https://noteser.app) — the browser-first markdown notes app.

> v1: plugins install by URL paste in **Settings → Plugins**. Copy any
> `manifest.json` URL below and paste it in.

---

## Plugins

### Sidebar panels

| Plugin | Version | Description | Install URL |
| --- | --- | --- | --- |
| **Word count** | 0.1.0 | Live word + character count for the active note, with reading-time estimate. | https://noteser-dev.vercel.app/plugins/noteser-word-count/manifest.json |

### Commands

_None yet — first one earns a section header._

### Code-block renderers

| Plugin | Version | Claimed languages | Install URL |
| --- | --- | --- | --- |
| **Callouts** | 0.1.0 | `note` / `info` / `tip` / `warn` / `danger` | https://noteser-dev.vercel.app/plugins/noteser-callout/manifest.json |

Use a callout in any note:

````markdown
```warn
title: Pay attention
This line becomes a colored callout box.
```
````

The `title:` line is optional.

---

## Submitting a plugin

1. Build your plugin as a single ES module + a `manifest.json` (see
   [the plugin docs](https://noteser.app/help/plugins) and the
   [`@noteser/plugin-sdk`](https://github.com/ipapakonstantinou/noteser/tree/main/packages/noteser-plugin-sdk)
   package).
2. Host both files at any HTTPS URL (GitHub Pages works, Vercel
   works, S3 works).
3. Confirm a fresh install works on
   [`noteser-dev.vercel.app`](https://noteser-dev.vercel.app).
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

Three v1 surfaces:

- **Commands** appear in the command palette (Ctrl+P)
- **Sidebar panels** stack inside the "Plugins" sidebar tab
- **Code-block renderers** claim a fenced-code language and turn its
  body into rendered output

Plugin code runs in an isolated Web Worker — no DOM, no
`localStorage`, no GitHub token, no `fetch` (v2 may add it with
explicit per-domain permissions).

## License

The list itself is MIT-licensed. Individual plugins set their own
license; check the linked plugin's repo or `package.json`.
