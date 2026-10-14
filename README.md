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

- **Split-pane layout** — the manuscript (source) pane is on the left, the rendered pane on the right. **Reading mode** (book button) temporarily shows the rendered pane alone.
- **Both panes are editable** — type Markdown on the left, or edit the rendered text directly on the right (insert/delete text, formatting is preserved). The two panes stay in sync in both directions.
- **Editing toolbar** — format the selection in the last active pane: bold, italic, strikethrough, headings, lists, blockquotes, links, and inline code. **More** inserts a starter table, an image from a URL, or a code block. The toolbar shows which pane will receive the edit; hover over a button for its name and available shortcut.
- **Shared undo and redo** — typing and toolbar edits in either pane share a history of up to 100 document states. Opening or creating a document resets this history; it lives only in the current tab.
- **Live rendering** — the right pane updates as you type, powered by a small hand-written Markdown parser: headings, bold/italic/strikethrough, inline code, fenced code blocks with light syntax colouring (JavaScript/TypeScript/JSON, Python, shell/YAML, SQL, HTML/XML, and C-family languages), blockquotes, nested ordered/unordered lists, **task lists** (`- [ ]` / `- [x]`, clickable in the rendered pane), tables, links, images, bare-URL autolinks, reference-style links (`[text][id]`), **footnotes** (`[^1]`), YAML **front matter** (shown as a quiet metadata box), and backslash-escapes. Links with `javascript:` and similar URLs are never made clickable.
- **Smart source editing** — `Enter` continues a list, numbered list, task list, or quote (and ends it on an empty item); `Tab` / `Shift+Tab` indent or outdent the selected lines or the current list item. Press `Esc` then `Tab` to move keyboard focus out of the editor.
- **Find and replace** — `Ctrl+F` / `Ctrl+H` (or the magnifier button) searches the manuscript, with match count, match case, *Replace*, and *Replace all*.
- **Outline** — the outline button lists every heading; pick one to jump there in both panes.
- **Scroll sync** — the two panes follow each other as you scroll (toggle with the ⇅ button; the choice is remembered).
- **Export** — save the rendered document as a standalone HTML page, copy it as formatted text for mail, blogs, or word processors, or print it / save it as PDF (printing shows the rendered document only, on white paper).
- **Open / New / Save / Save As** — uses the browser's native File System Access API when available, so Save writes straight back to the file you opened. Falls back to a plain file picker + download in browsers without that API.
- **Files stay intact** — line endings (CRLF or LF), a UTF-8 BOM, and a final newline are kept exactly as they were. Legacy Korean (EUC-KR/CP949) and UTF-16 files open correctly; MD·Buddy saves as UTF-8 and asks before converting. The status bar shows the current encoding and line endings.
- **Drag and drop** — drop a `.md` file anywhere on the window to open it.
- **Installable** — runs as its own app window with offline support and `.md` file association (see *Ways to use*).
- **English or Korean interface** — English by default; the **한 / EN** button in the top-right corner switches every menu, tooltip, message, and the welcome document to Korean (한국어) and back. The choice is remembered.
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
| Task list | Task list button, or type `- [ ] `; click a box in the rendered pane to tick it |
| Continue / end a list | `Enter` / `Enter` on an empty item |
| Indent / outdent lines | `Tab` / `Shift+Tab` (`Esc`, then `Tab` leaves the editor) |
| Find / replace | `Ctrl+F` / `Ctrl+H`; `Enter` next, `Shift+Enter` previous, `F3` next, `Esc` close |
| Jump to a heading | Outline button |
| Reading mode / scroll sync | Book button / ⇅ button |
| Export HTML, copy formatted, print or PDF | **Export** menu (or `Ctrl+P` to print) |
| Switch language (English / 한국어) | **한** / **EN** button, top-right |
| Switch theme | Sun/moon button, top-right |

**Nothing is saved automatically** — in every way of using it. Edits only live in the browser tab (or app window) until you explicitly click **Save** (or **Save As**) — closing the tab, reloading, or navigating away without saving will lose your changes. The status bar's dot next to the filename turns solid/pulsing when there are unsaved changes, as a reminder to save.

Both panes support text editing and the toolbar. For complex Markdown, editing the source on the left is more reliable: the rendered pane uses the app's limited HTML-to-Markdown serializer and can normalize spacing or syntax when applying an edit. Front matter, link definitions, and footnote definitions are always written back exactly as typed.

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
