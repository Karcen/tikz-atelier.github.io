# TikZ Atelier

> A single-file, drag-and-drop visual editor that generates clean LaTeX/TikZ code in real time.

Sketch your diagram in the browser, edit text and colors visually, then copy the generated TikZ source into your paper. No build step, no dependencies, no account — just one HTML file.

![Status](https://img.shields.io/badge/status-stable-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Build](https://img.shields.io/badge/build-none%20required-lightgrey)

---

## ✨ Features

- **Drag-and-drop shapes** — rectangle, rounded rectangle, circle, ellipse, diamond, plain text node
- **Click-to-connect edges** with arrows (`→`, `←`, `↔`, none), labels, dashing, and adjustable bend
- **Live property editor** — text, fill, stroke, line width, font size, and dash style per node
- **Real-time TikZ output** in two modes:
  - `tikzpicture`-only (just the environment, with required libraries listed as a comment)
  - Full standalone document (ready to compile)
- **Auto-generated `\definecolor`** declarations for every custom hex color used
- **Light & dark mode** that follows your system preference, with a one-click toggle
- **Multiline node text** and **raw LaTeX** in labels (`$x^2$`, `\frac{a}{b}`, etc.)
- **One-click clipboard copy** with syntax-highlighted code preview
- **Zero dependencies** — single self-contained HTML file (~55 KB)

---

## 🚀 Quick Start

1. Download `tikz-atelier.html` from this repo (or clone it).
2. Open the file in any modern browser. That's the entire installation.

> No Node.js, no `npm install`, no server. Works offline.

You can also host it as a static page (GitHub Pages, Netlify, Cloudflare Pages — anywhere that serves an HTML file).

---

## 📖 Usage

### Adding nodes

1. Click a shape icon in the **left palette**.
2. Click anywhere on the canvas to place the node.
3. Press `Esc` if you want to cancel placement.

### Editing nodes

- Click a node to select it; its properties appear in the right inspector.
- Drag to reposition.
- Edit text, font size, fill, stroke, line width, and dash style live.
- Use `∅` to clear a fill or stroke; use the duplicate button to clone a node.

### Drawing edges

1. Click the **Connect** button in the left palette.
2. Click the source node (it highlights in accent color).
3. Click the target node — done.

Select an edge to change its arrow direction, dash style, label, color, or curvature.

### Keyboard

| Key | Action |
|-----|--------|
| `Esc` | Exit placement / connect mode, deselect |
| `Delete` / `Backspace` | Delete the selected node or edge |

---

## 🧠 Conventions

- The canvas's **bottom-left corner maps to TikZ origin `(0, 0)`** — the y-axis points up in the output, just like in TikZ.
- **1 cm in TikZ = 50 px on the canvas.**
- Node text is passed through verbatim — write LaTeX freely. Newlines become `\\` line breaks inside the node body.
- Default node strokes and edge colors that match the theme ink are written as TikZ defaults (no explicit color), so they render as plain black on the final PDF regardless of which mode you authored them in.

---

## 📦 Required LaTeX Packages

The full-document export uses:

```latex
\usepackage{tikz}
\usepackage{xcolor}
\usetikzlibrary{shapes.geometric, arrows.meta, positioning, calc}
```

If you copy the `tikzpicture`-only output into an existing document, those library and `\definecolor` lines are listed as comments at the top of the snippet for easy transfer to your preamble.

---

## 🖼️ Example Output

A flowchart drawn in the editor exports to roughly:

```latex
\begin{tikzpicture}[>=Stealth, font=\sffamily, line cap=round]
  \node[draw, rectangle, rounded corners=4pt, minimum width=2.6cm, minimum height=1.12cm,
        fill=c1] (n1) at (4,6) {Start};
  \node[draw, rectangle, minimum width=2.8cm, minimum height=1.12cm,
        fill=c2, inner sep=0pt] (n2) at (8,6) {Read data};
  \node[draw, diamond, aspect=1.4, minimum width=2.8cm, minimum height=1.8cm,
        fill=c3] (n3) at (8,4) {Valid?};

  \draw[->] (n1) -- (n2);
  \draw[->] (n2) -- (n3);
  \draw[->, dashed, color=c4] (n3) to[bend right=15] (n5)
        node[midway, above, sloped, font=\small\itshape] {No};
\end{tikzpicture}
```

---

## 🎨 Design

Built with an academic / drafting-paper aesthetic:

- **Type:** Fraunces (display), Newsreader (body), JetBrains Mono (code)
- **Light theme:** crisp white surfaces with warm ink and a clay-red accent
- **Dark theme:** deep ink surfaces with cream type and a warmer terracotta accent
- **Layout:** asymmetric three-column grid (palette / canvas / inspector) with a thin footer

No frameworks. Pure HTML + CSS + vanilla JavaScript + a single inline SVG canvas.

---

## 🛣️ Roadmap

Possible future additions:

- [ ] Undo / redo stack
- [ ] Save & load `.tikz` project files (JSON snapshot)
- [ ] PNG / SVG export of the canvas itself
- [ ] Snap-to-grid and alignment guides
- [ ] More shapes (cloud, cylinder, parallelogram, trapezium)
- [ ] Anchor-aware edge attachment (pick `north`, `south.west`, etc.)
- [ ] Bézier-controlled edges with handles

Pull requests welcome.

---

## 🤝 Contributing

Issues and PRs are welcome. Since the entire app is a single HTML file, contributing is as simple as:

1. Fork the repo
2. Edit `tikz-atelier.html`
3. Open it in a browser to verify
4. Submit a PR

Please keep the project dependency-free and the file self-contained.

---

## 📜 License

MIT — see `LICENSE` for details.

You can use, modify, and ship this in your own projects, commercial or otherwise. Attribution is appreciated but not required.

---

## 👤 Author

Made by **Karcen Zheng** — [Get in touch](https://karcen.github.io/zhengjiacheng.github.io/)

If TikZ Atelier saved you time on a paper, slide deck, or thesis, a ⭐ on the repo is the nicest way to say thanks.
