---
type: Note
---
# Hermes re: Zed Config

I configured Zed as a source-first writing and markup IDE while preserving your existing coding settings.

Configured:

- Writing profile in: /Users/kbc/.config/zed/settings.json
- Writing-friendly defaults:
  - 16px buffer text
  - Comfortable line height
  - 88-character writing width
  - Bounded soft wrapping
  - Rewrapping enabled for Markdown and Plain Text
  - Centered writing layout
  - Breadcrumbs hidden
  - Trailing whitespace visible
- Language support tuned for:
  - Markdown
  - Plain Text
  - HTML/CSS
  - JSON
  - YAML
  - TOML
  - JavaScript/TypeScript
  - Python
  - Rust
  - Shell scripts
- Markdown and Plain Text formatting-on-save disabled so prose is not unexpectedly reformatted.
- Keymap in: /Users/kbc/.config/zed/keymap.json

Shortcuts added:

- Cmd-Alt-P — Open Markdown preview to the side
- Cmd-Alt-R — Rewrap the current paragraph/document
- Cmd-Alt-Enter — Toggle centered writing layout
- Cmd-Shift-P and Ctrl-P — Command Palette remain available

Writing/export tasks added in:

/Users/kbc/.config/zed/tasks.json

Available through “task: spawn”:

- Markdown: export HTML
- Markdown: export PDF using Typst
- Markdown: export Word DOCX
- Markdown: open exported HTML

Pandoc and Typst were available on your system, and I successfully smoke-tested HTML and PDF generation.

Backups were created:

- /Users/kbc/.config/zed/settings.json.pre-writing
- /Users/kbc/.config/zed/keymap.json.pre-writing

To activate the profile in Zed:

1. Press Cmd-Shift-P.
2. Run “settings profile selector: toggle”.
3. Select “Writing”.

Important limitation: Zed is excellent for Markdown, plain text, HTML, markup, and code, but it is not a native Word-style WYSIWYG rich-text editor. The practical workflow is:

Markdown/HTML source → Zed editing and preview → HTML, PDF, or DOCX export.

Zed’s Settings window also displayed an existing “settings are out of date” migration notice. I left that automatic migration untouched so it would not rewrite unrelated settings.
╰────────────────────────────────────────────────────────────────────────────────────────────────────╯
💾 Self-improvement review: Skill 'editor-configuration' created.
