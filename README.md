# MD·Buddy

A small, self-contained Markdown reader and editor that runs entirely as a single HTML file — no build step, no external services, no dependencies. It's meant to be hosted on a web server and used at its URL; if you need it offline, you can also download `index.html` and open it directly in a browser (or just double-click it) — the file is fully self-contained either way.

## Features

- **Split-pane layout** — the manuscript (source) pane is always on the left, the rendered pane is always on the right.
- **Both panes are editable** — type Markdown on the left, or edit the rendered text directly on the right (insert/delete text, formatting is preserved). The two panes stay in sync in both directions.
- **Editing toolbar** — format the selection in the last active pane: bold, italic, strikethrough, headings, lists, blockquotes, links, and inline code. **More** inserts a starter table, an image from a URL, or a code block. The toolbar shows which pane will receive the edit; hover over a button for its name and available shortcut.
- **Shared undo and redo** — typing and toolbar edits in either pane share a history of up to 100 document states. Opening or creating a document resets this history; it lives only in the current tab.
- **Live rendering** — the right pane updates as you type, powered by a small hand-written Markdown parser (headings, bold/italic/strikethrough, inline code, fenced code blocks, blockquotes, ordered/unordered lists with one level of nesting, tables, links, images, and backslash-escapes).
- **Open / New / Save / Save As** — uses the browser's native File System Access API when available, so Save writes straight back to the file you opened. Falls back to a plain file picker + download in browsers without that API.
- **Drag and drop** — drop a `.md` file anywhere on the window to open it.
- **Light and dark themes** — toggle in the top-right corner; the choice is remembered.
- **Resizable split** — drag the divider between the two panes to adjust the widths.
- Word count, character count, and an unsaved-changes indicator in the status bar.

## Using it

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

**Nothing is saved automatically.** Edits only live in the browser tab until you explicitly click **Save** (or **Save As**) — closing the tab, reloading, or navigating away without saving will lose your changes. The status bar's dot next to the filename turns solid/pulsing when there are unsaved changes, as a reminder to save.

Both panes support text editing and the toolbar. For complex Markdown, editing the source on the left is more reliable: the rendered pane uses the app's limited HTML-to-Markdown serializer and can normalize spacing or syntax when applying an edit.

## Browser support

Full functionality (opening a file and saving back to it directly) requires a Chromium-based browser (Chrome, Edge, etc.) with the File System Access API. In other browsers, Open uses a standard file picker and Save downloads a file instead of writing back to the original.

## Tech notes

- Everything — markup, styles, and script — lives in `index.html`. There is no build step and nothing to install; the same file works served from a web server or opened locally.
- The Markdown renderer and its reverse (HTML → Markdown, used to sync edits made in the rendered pane) are both hand-written; they cover common Markdown syntax but are not a full CommonMark implementation.
- No analytics, no network requests, no external fonts or scripts — everything you write stays in the browser tab until you explicitly save it.

## Credits

Chulwoo Park — [cantips.com](https://cantips.com)
