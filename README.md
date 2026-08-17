<div align="center">

# 📚 ReadMD

**The Markdown reader that knows how your documents connect.**

Read, navigate, search, and export a folder of Markdown files as a connected knowledge package — with a guided reading order you define once and can share anywhere.

[Features](#-features) • [Why ReadMD?](#-why-readmd) • [Download](#-download) • [Quick Start](#-quick-start) • [FAQ](#-faq)

</div>

---

## 🎯 Why ReadMD?

Markdown is great for *writing* — but not for *reading*. A folder of notes, documentation, or course materials has structure that lives only in file names, a table of contents, or the author's memory:

- **What's the intended reading order?** Which file comes after this one?
- **How do documents relate?** Which ones reference each other?
- **How do I find anything?** When the folder grows, scrolling stops working.

ReadMD answers all three. It turns a plain folder of `.md` files into an interactive knowledge environment with **four complementary views** of the same content:

| View | What it gives you |
|------|-------------------|
| 📖 **Reader** | Beautiful, native rendering of any Markdown file |
| 🕸️ **Knowledge graph** | See and edit how your documents connect |
| 🔗 **Reading sequences** | Follow an explicit, guided reading order |
| 🔍 **Search** | Full-text search across every document |

**The core idea — a reading flow.** ReadMD's standout concept is the *reading flow*: an explicit, machine-readable chain of `source → target` edges that states precisely which document comes next. Define it once (via connections, `[[wikilinks]]`, or frontmatter), and ReadMD renders the entire chain as a guided, chapter-like sequence — while the same folder simultaneously remains an explorable graph and a searchable corpus.

The flow is portable: it can be saved to a `reading-flow.json` file that re-imports into any reader honoring the contract. Your content stays **plain Markdown** — no proprietary format, no build step, no lock-in.

---

## ✨ Features

### 📖 Markdown Reader with Beautiful Typography

Clean, readable typography in light and dark mode, supporting the full CommonMark spec plus:

- **Syntax-highlighted code blocks** for dozens of languages (with a copy button)
- **KaTeX math** — `$...$` and `$$...$$` rendered inline and in blocks
- **Mermaid diagrams** — fenced ```mermaid blocks and `.mmd` files rendered as live, theme-aware diagrams
- **Images** — local files, remote URLs, and base64 data URLs, all **lazy-loaded** as you scroll
- **Tables, blockquotes, task lists, footnotes**, and YAML frontmatter (title, tags, metadata)
- **Auto-generated Table of Contents** — hierarchical, with scroll tracking
- **Click-to-lightbox** on any image or diagram — zoom, pan, and download
- **External links open in-app** in an isolated window — never navigates away

### 🕸️ Knowledge Graph — connections made visible

The graph is ReadMD's signature feature. It automatically builds an interactive graph of your documents and the relationships between them:

- **Automatic edges** discovered from `[[wikilinks]]` and `next:` frontmatter fields
- **Manual connections** — Shift+drag between nodes, or pick source/target in the Connect panel
- **Collapsible folders** — explore the graph from coarse structure down to individual files
- **Drag, pan, and zoom** — rearrange nodes freely; layout is fast even for hundreds of nodes

Your manual connections are **session-only by design**: ReadMD never writes into your workspace without you asking. When you close the app or switch folders, it offers to **save them as a `connections.json` file** — or export mid-session anytime with **Save flow…**. Saved flows are re-importable later.

### 🔗 Reading Sequences — guided reading on demand

Define an order for your documents and ReadMD loads it as a seamless, lazy sequence:

- Click any node in the chain to open the full path — file names appear instantly, content loads on click
- **Numbered headers and dividers** show your position in the chain
- **Prev/Next navigation** with a sticky progress bar
- **Folder-aware sequence TOC** — collapsible folders, per-file level badges, live updates when connections change
- Open any single file in a chain and its chain's tree is shown, even outside sequence mode

This makes course material, tutorials, and chaptered documentation genuinely navigable — the reader always knows what comes next.

### 🔍 Full-Text Search

Every word in your folder is indexed with SQLite **FTS5 + BM25** — the same ranking algorithm used by modern search engines:

- Ranked results with **highlighted `<mark>` snippets**
- **Click a result to jump** to the exact match, with a temporary flash highlight
- Debounced, instant results as you type
- Index rebuilt automatically when you open or scan a folder

### 📤 DOCX & PDF Export

Export to Word (`.docx`) or PDF with one click — **Pandoc and Typst are bundled inside the installers**, no setup required:

| Mode | What it produces |
|------|------------------|
| **Single file** | One `.docx` / `.pdf` from one Markdown file |
| **Multiple files (merged)** | Several files combined into one document |
| **Multiple files (batch)** | One document per file |

Export is print-quality: Mermaid diagrams are pre-rendered to high-resolution PNGs, raster images are page-fitted and DPI-tagged, and DOCX uses a custom Word reference template.

### ✏️ Built-in Editor with Live Preview

Edit Markdown without leaving the app:

- **CodeMirror 6** editor with a **draggable live-preview split pane** (`Ctrl+E`)
- Preview updates as you type — including **live Mermaid diagrams**
- **`Ctrl+S`** saves atomically and invalidates caches instantly
- Unsaved-change guard prompts before you lose work

### 🔖 Bookmarks — never lose your place

- One bookmark per file, storing the exact scroll position
- **Per-folder**, stored in the OS app-data directory (never in your workspace)
- Resume jumps straight back to the saved offset; dead bookmarks auto-pruned

### 🌙 Everything, in Dark Mode

Dark mode themes the entire app — including **Mermaid diagrams**, which re-render with Mermaid's dark theme on toggle. Font zoom (`Ctrl+Scroll`), split-pane resizing, and a persistent session restore round out a reading experience designed for long sessions.

---

## 💡 What Makes It Different

The feature matrix below — taken from the ReadMD paper — positions the app against six representative tools: Ghostwriter, MarkText, VSCodium, Obsidian, LiaScript, and Hyperbook.

| Dimension | ReadMD | Ghostwriter | MarkText | VSCodium | Obsidian | LiaScript | Hyperbook |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Local-first desktop reader | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ <sup>a</sup> | ⚠️ <sup>b</sup> |
| Plain Markdown (no custom dialect) | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |
| Explicit sequential reading flow | ✅ | ❌ | ❌ | ⚠️ <sup>c</sup> | ❌ | ⚠️ <sup>e</sup> | ⚠️ <sup>e</sup> |
| Built-in knowledge graph | ✅ | ❌ | ❌ | ⚠️ <sup>f</sup> | ✅ | ❌ | ❌ |
| Reading-flow import (`reading-flow.json`) | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| DOCX/PDF export | ✅ | ✅ | ⚠️ <sup>g</sup> | ❌ | ❌ | ⚠️ <sup>h</sup> | ❌ |
| No build / no hosting / no LMS | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Free & open source | ✅ (MIT) | ✅ | ✅ | ✅ | ⚠️ <sup>i</sup> | ✅ | ✅ |

<sup>a</sup> Browser interpreter · <sup>b</sup> Build step and hosting · <sup>c</sup> Via file-naming conventions or extensions · <sup>e</sup> Linear, but dialect- or pipeline-bound · <sup>f</sup> Via extensions (e.g., Foam) · <sup>g</sup> HTML/PDF only · <sup>h</sup> PDF/SCORM, no DOCX · <sup>i</sup> Proprietary

Among these tools, **only ReadMD satisfies every dimension of the package model**: local-first desktop delivery, plain Markdown, an explicit machine-readable reading flow, a built-in knowledge graph, reading-flow import, lossless DOCX/PDF export, zero-configuration operation, and an open-source license. The closest competitors satisfy at most four of the eight dimensions — the decisive difference is the combination: each other tool supplies one or two pieces of the package contract, while ReadMD supplies all of them, so a package authored for the model imports, reads, navigates, searches, edits, and exports within a single system.

---

## 📦 Download

| Platform | Format | How to get it |
|----------|--------|---------------|
| **Windows** | `.exe` (NSIS) or `.msi` (WiX) | Download from [Releases](https://github.com/user/ReadMD/releases) |
| **Linux** | `.deb` or `.AppImage` | Download from [Releases](https://github.com/user/ReadMD/releases) |

> **Why is the installer this size?** ReadMD's installers bundle everything needed to work out of the box: the Pandoc and Typst engines for DOCX/PDF export (~150–220 MB of binaries each, compressed inside the package), the Noto Color Emoji font, and — for the AppImage — the WebKitGTK runtime itself. That's what makes export and emoji work with zero setup; the app's own code is a fraction of the total.

**Requirements:**

- **Windows:** Windows 10 or later (WebView2 is built-in)
- **Linux:** System with WebKitGTK 4.1, GTK3, and a working X11 display. The `.deb` automatically installs `fonts-noto-color-emoji`; the AppImage needs no font setup
- **Emoji:** Noto Color Emoji is **bundled inside every installer** — emoji render on any system, no font installation needed
- **DOCX/PDF export:** Pandoc and Typst are **bundled with the Windows and Linux installers** — no action needed

---

## 🚀 Quick Start

1. **Download and install** the latest release for your platform
2. **Launch ReadMD** — you'll see the sidebar, toolbar, and viewer
3. **Open a folder** — click "Open Folder" in the sidebar or toolbar
4. **Click a file** to read it in the viewer
5. **Search** — click the search icon to find content across all files
6. **Explore the graph** — click the Graph tab to see connections between your documents
7. **Connect documents** — Shift+drag on the graph, or use the Connect panel, to link related content
8. **Follow a sequence** — click any connected node to walk the full chain with Prev/Next

> **Tip:** Open a folder of linked Markdown notes (with `[[wikilinks]]`) to see the graph come to life. Import an existing `reading-flow.json` to materialize a guided reading sequence instantly.

### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+E` | Toggle edit mode (editor + live preview) |
| `Ctrl+S` | Save the current file (in edit mode) |
| `Ctrl+Scroll` | Zoom text in/out in the viewer |
| `Shift+Drag` (on graph) | Create a connection between two nodes |

---

## 📸 Screenshots

> *Screenshots coming soon. The app is in active development — here's what you'll see:*

- **Reader view:** Clean, full-width Markdown rendering with syntax-highlighted code, KaTeX math, and live Mermaid diagrams
- **File tree sidebar:** Nested folder structure with active-file highlighting
- **Knowledge graph:** Interactive graph with draggable nodes and Shift+drag connections
- **Sequence view:** Multiple files concatenated with numbered headers, dividers, and Prev/Next navigation
- **Search panel:** Ranked results with highlighted snippets and jump-to-match
- **Editor:** CodeMirror with a draggable live-preview split pane
- **Export dialog:** Single, merged, or batch DOCX/PDF modes

---

## ❓ FAQ

**Q: Can I use ReadMD with my existing Markdown notes?**

Yes. ReadMD works with plain `.md` files (plus `.markdown`, `.mdown`, `.mdtext`, `.mdx`, `.mmd`). Open any folder and it scans all Markdown files recursively. No special metadata or configuration required — `[[wikilinks]]` and `next:` frontmatter are optional enhancements.

**Q: Does ReadMD modify my files?**

No. ReadMD is read-only with respect to your source files — it indexes and caches content in its own SQLite database, and stores bookmarks and logs in OS app-data directories. The only exceptions: DOCX/PDF export creates new output files alongside your originals, and saving a connection flow writes the `reading-flow.json` / `connections.json` file you explicitly asked for.

**Q: What is a reading flow?**

A reading flow is an ordered chain of document-to-document edges — a machine-readable answer to "what comes next?" ReadMD can import one from a `reading-flow.json` file, build one from your `[[wikilinks]]` and `next:` frontmatter, or let you create one by connecting documents on the graph. The flow renders as a guided sequence, and it's portable: you can save it and re-import it into any tool that honors the contract.

**Q: How does the graph handle very large folders?**

The graph is built lazily and layout is fast even for hundreds of nodes. Loading the case-study course (17 chapters, ~114 files) and folders with several times more documents kept every node responsive and interactive. You can zoom, pan, and collapse folders to navigate even complex graphs.

**Q: Can I export to PDF?**

Yes. Use the export dropdown and switch the format to **PDF**. PDFs are generated with Pandoc's Typst engine, which handles images (including Mermaid diagrams) and LaTeX math natively. Pandoc and Typst are **bundled with the Windows and Linux installers** — no setup needed.

**Q: Are my images stored in the app?**

Only base64 data-URL images are cached in ReadMD's internal database (so they display instantly on re-open). Local file images and remote URL images load from their original sources each time.

**Q: Emojis show as empty boxes on Linux?**

This shouldn't happen on current installers — Noto Color Emoji is **bundled inside every installer**, so emoji render without any system font. On older installs, install the system font once (`sudo apt install fonts-noto-color-emoji`) and restart ReadMD.

**Q: Does ReadMD support Obsidian or Roam-style Markdown?**

ReadMD supports standard CommonMark plus `[[wikilinks]]` and YAML frontmatter with `title`, `tags`, and `next:` fields. Other extended syntaxes (Obsidian callouts, Dataview queries, etc.) are not yet supported.

---

## 🛠️ Development

ReadMD is built with **Tauri 2.0** (Rust) + **Vue 3** (TypeScript) + **Tailwind CSS v4**.

**Run in development mode:**

```bash
npm install
npm run tauri dev
```

**Build installers with Docker (Linux/Windows):**

```bash
docker compose --profile build run --rm build-linux     # .deb + AppImage
docker compose --profile build run --rm build-windows   # Windows NSIS installer
```

**Documentation:** the [docs/](docs/README-FIRST.md) directory contains a full developer guide — project architecture, Rust backend, Vue frontend, Tauri IPC, data flow, database caching, and a complete feature catalog.

**Building installers locally** requires these bundled resource files in `src-tauri/resources/` (they're git-ignored; CI downloads them automatically):

```bash
# Noto Color Emoji (emoji rendering — ~10 MB)
curl -L -o src-tauri/resources/NotoColorEmoji.ttf \
  https://github.com/googlefonts/noto-emoji/raw/main/fonts/NotoColorEmoji.ttf

# Pandoc + Typst (DOCX/PDF export) — see the error messages in commands.rs for exact URLs
```

**Docker dev-container troubleshooting** — if the mouse pointer is invisible over the app window when running `docker compose up`:

```bash
docker compose build readmd-dev   # needed once after Dockerfile changes
```

The dev image installs `dmz-cursor-theme`, writes `gtk-cursor-theme-name=DMZ-White` into devuser's GTK settings, and sets `XCURSOR_THEME=DMZ-White` plus WebKitGTK software-rendering fallbacks. Packaged builds are unaffected — those env vars only apply inside the container.

**If you're on Windows with Docker Desktop / WSLg and the pointer is still invisible:** the cursor over an X11 window is drawn by WSLg's Xwayland compositor, which resolves cursor themes from the **WSL distro's** filesystem — *not* from inside the container:

```powershell
# 1. Open your WSL distro and install a cursor theme there:
wsl -d Ubuntu -- sudo apt update && wsl -d Ubuntu -- sudo apt install -y dmz-cursor-theme

# 2. Make sure XCURSOR_THEME reaches WSLg (PowerShell):
wsl -d Ubuntu -- sudo sh -c 'echo "export XCURSOR_THEME=DMZ-White" >> /etc/profile.d/cursor.sh'

# 3. Fully restart WSL so the compositor picks up the theme:
wsl --shutdown
```

Then restart Docker Desktop and `docker compose up` again.

---

<div align="center">

**ReadMD** is released under the MIT License.

Built with [Tauri](https://v2.tauri.app/), [Vue 3](https://vuejs.org/), and [Tailwind CSS](https://tailwindcss.com/).

</div>
