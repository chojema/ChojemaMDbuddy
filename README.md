# MD·Buddy

A small, self-contained Markdown reader and editor — no build step, no external services, no dependencies. The whole app is one `index.html`; a few small companion files (`manifest.webmanifest`, `sw.js`, `icons/`) let browsers install it as an app and run it offline.

## Ways to use

The same app, three ways — pick whichever suits you:

1. **On the web** — open the hosted URL in a browser.
2. **Installed as an app (PWA)** — from the hosted URL, install it in Chrome or Edge (see below). It then opens in its own window with a Start menu / Dock icon, works offline, and can open `.md` files from your file manager.
3. **As a single file** — download `index.html` and double-click it. Everything works from that one file; only installation and the service-worker-based offline cache are unavailable (none are needed — the file is already on your disk).

| | Web | Installed app | Single file (`file://`) |
| --- | --- | --- | --- |
| Editing, rendering, shortcuts, themes | ✓ | ✓ | ✓ |
| Open / save back to the same file | Chrome, Edge | ✓ | Chrome, Edge |
| Works offline | ✓ after the first visit | ✓ | ✓ |
| Own window, Start menu / Dock icon | — | ✓ | — |
| Open `.md` files by double-click / "Open with" | — | ✓ | — |
| Updates | always latest | latest when online | re-download the file |

### Installing the app

Installation needs the app to be served over HTTPS (or `localhost`) and a Chromium-based browser — Chrome or Edge on Windows or macOS.

- Click **Install** in the top bar (shown only when your browser can install the app), or
- **Chrome:** the install icon at the right end of the address bar, or ⋮ menu → install option.
- **Edge:** the "App available" icon in the address bar, or … menu → Apps → *Install this site as an app*.

After installing, `.md` and `.markdown` files can be opened with MD·Buddy from Explorer or Finder; each file opens in its own window, and **Save** writes straight back to it. To uninstall, use the ⋮ menu inside the app window (or Windows *Settings → Apps*).

Safari's *File → Add to Dock* also works, but Safari cannot save back to the original file (see Browser support).

## Features

- **Split-pane layout** — the manuscript (source) pane is always on the left, the rendered pane is always on the right.
- **Both panes are editable** — type Markdown on the left, or edit the rendered text directly on the right (insert/delete text, formatting is preserved). The two panes stay in sync in both directions.
- **Editing toolbar** — format the selection in the last active pane: bold, italic, strikethrough, headings, lists, blockquotes, links, and inline code. **More** inserts a starter table, an image from a URL, or a code block. The toolbar shows which pane will receive the edit; hover over a button for its name and available shortcut.
- **Shared undo and redo** — typing and toolbar edits in either pane share a history of up to 100 document states. Opening or creating a document resets this history; it lives only in the current tab.
- **Live rendering** — the right pane updates as you type, powered by a small hand-written Markdown parser (headings, bold/italic/strikethrough, inline code, fenced code blocks, blockquotes, ordered/unordered lists with one level of nesting, tables, links, images, and backslash-escapes).
- **Open / New / Save / Save As** — uses the browser's native File System Access API when available, so Save writes straight back to the file you opened. Falls back to a plain file picker + download in browsers without that API.
- **Drag and drop** — drop a `.md` file anywhere on the window to open it.
- **Installable** — runs as its own app window with offline support and `.md` file association (see *Ways to use*).
- **Light and dark themes** — toggle in the top-right corner; the choice is remembered.
- **Resizable split** — drag the divider between the two panes to adjust the widths.
- Word count, character count, and an unsaved-changes indicator in the status bar.

## Using it

Shortcuts are shown with `Ctrl`; on macOS use `Cmd`.

| Action | How |
| --- | --- |
| Open a file | Click **Open**, press `Ctrl+O`, or drag a file onto the window |
| New document | Click **New** |
| Save | Click **Save**, or press `Ctrl+S` |
| Save As | Click **Save As**, or press `Ctrl+Shift+S` |
| Bold / italic selection | Toolbar buttons, or `Ctrl+B` / `Ctrl+I` in either pane |
| Undo / redo | Toolbar buttons, `Ctrl+Z` / `Ctrl+Shift+Z`, or `Ctrl+Y` for redo |
| Headings, lists, or blockquotes | Select text or place the caret in a line, then use the toolbar |
| Insert a link | Link button or `Ctrl+K`; enter the text and an HTTP, HTTPS, or mailto URL |
| Insert a table, image, or code block | **More** menu; images require an HTTP or HTTPS URL |
| Switch theme | Sun/moon button, top-right |

**Nothing is saved automatically** — in every way of using it. Edits only live in the browser tab (or app window) until you explicitly click **Save** (or **Save As**) — closing the tab, reloading, or navigating away without saving will lose your changes. The status bar's dot next to the filename turns solid/pulsing when there are unsaved changes, as a reminder to save.

Both panes support text editing and the toolbar. For complex Markdown, editing the source on the left is more reliable: the rendered pane uses the app's limited HTML-to-Markdown serializer and can normalize spacing or syntax when applying an edit.

## Browser support

Full functionality (opening a file and saving back to it directly) requires a Chromium-based browser (Chrome, Edge, etc.) with the File System Access API. In other browsers, Open uses a standard file picker and Save downloads a file instead of writing back to the original.

App installation and `.md` file association are likewise Chromium-only (Chrome or Edge on Windows and macOS).

## Tech notes

- Everything — markup, styles, and script — lives in `index.html`. There is no build step and nothing to install; the same file works served from a web server or opened locally.
- PWA support is additive: `manifest.webmanifest` (app name, icons, file handlers), `sw.js` (offline cache), and `icons/`. `index.html` links the manifest and registers the service worker only when served over http(s), so the single-file copy behaves exactly as before.
- The service worker loads the page network-first (online users always get the latest version; the cached copy is used offline) and serves the manifest and icons from cache. When you change any of those cached files, bump `CACHE_VERSION` in `sw.js`.
- The Markdown renderer and its reverse (HTML → Markdown, used to sync edits made in the rendered pane) are both hand-written; they cover common Markdown syntax but are not a full CommonMark implementation.
- No analytics, no requests to other servers, no external fonts or scripts — the only network traffic is the browser loading the app's own files. Everything you write stays in the browser tab until you explicitly save it.

## Credits

Chulwoo Park — [cantips.com](https://cantips.com)
