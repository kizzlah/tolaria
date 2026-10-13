---
type: Note
_favorite: true
_favorite_index: 2
---
# Digital Assets - Organizational Methodologies w/ Examples

**TLDR:** The PARA method organizes digital information by actionability into four containers (Projects, Areas, Resources, Archives), while alternative systems focus on flat tagging, networked linking, numerical hierarchy, or functional workflows.

---

## PARA Method

Tiago Forte's system organizes digital assets by their relationship to active execution. Everything you store falls into one of four buckets:

- **Projects** — Short-term efforts with a specific goal and deadline.
- **Areas** — Ongoing responsibilities and standards to maintain indefinitely.
- **Resources** — Topic-based reference materials, interests, and research.
- **Archives** — Inactive items preserved from the other three buckets.

**Example Directory Structure:**

```
PARA/
├── 1 Projects/
│   ├── Website Redesign/
│   ├── Q4 Sales Deck/
│   └── Move to New Apartment/
├── 2 Areas/
│   ├── Health/
│   ├── Finances/
│   └── Product Management/
├── 3 Resources/
│   ├── Photography/
│   ├── Marketing Templates/
│   └── Cooking Recipes/
└── 4 Archives/
    ├── Website Redesign (completed)/
    └── 2024 Tax Filing/
```

**Strengths:** PARA standardizes folder structures across different apps (file storage, notes, tasks) and reduces cognitive load by separating active tasks from reference files.

**Limitations:** There's real boundary friction between active "Projects" and ongoing "Areas." The system also requires regular maintenance to move completed projects into archives.

---

## Johnny.Decimal

A structured numerical indexing system that organizes files into Categories (00–09) and IDs (00–99). Top-level areas are divided into 10 categories, each containing up to 10 subcategories. Files receive a static decimal address — for example, `11.02 Specification.pdf`.

**Example Directory Structure:**

```
00-09 System Administration/
├── 01 Accounts/
│   ├── 01.01 Vendor Logins.md
│   └── 01.02 License Keys.md
├── 02 Backups/
│   └── 02.01 Backup Schedule.md
10-19 Projects/
├── 11 Website Rebuild/
│   ├── 11.01 Brief.md
│   ├── 11.02 Specification.pdf
│   └── 11.03 Wireframes.fig
├── 12 Brand Refresh/
│   └── 12.01 Mood Board.pdf
20-29 Finance/
├── 21 Invoices/
│   └── 21.01 2024-Q3-Invoice.pdf
└── 22 Budgets/
    └── 22.01 Annual-Budget-2024.xlsx
```

**Ideal for:** Deep file system hierarchies, shared drives, and deterministic search without reliance on full-text indexing.

---

## Zettelkasten

A non-hierarchical, atomized knowledge management system built on bidirectional links. It distinguishes three note types:

- **Fleeting notes** capture quick thoughts.
- **Literature notes** summarize external content in the user's own words.
- **Permanent notes** contain standalone concepts connected to related notes via hyperlinks.

**Example Directory Structure:**

```
Zettelkasten/
├── Inbox/
│   ├── fleeting-2024-10-03.md
│   └── fleeting-2024-10-07.md
├── Literature/
│   ├── lit-ahrens-how-to-take-smart-notes.md
│   └── lit-sönke-thinking-in-systems.md
└── Permanent/
    ├── 202410031a-spaced-repetition-enhances-retention.md
    ├── 202410031b-active-recall-vs-passive-review.md
    ├── 202410052a-zettelkasten-forces-atomic-thinking.md
    └── 202410071a-bidirectional-links-enable-emergence.md
```

*Each permanent note links to related notes via* [[wikilinks]]*, forming a web rather than a tree.*

**Ideal for:** Long-term research, synthesizing insights, and knowledge graphs (e.g., Obsidian, Logseq).

---

## ACCESS Method

Nick Milo's Linking Your Thinking framework, designed for dynamic personal knowledge management. It defines six functional spaces:

- **Atlas** — Maps and top-level navigation.
- **Calendar** — Time-based tracking and logs.
- **Cards** — Atomic, standalone notes.
- **Extras** — Templates, assets, and tools.
- **Sources** — Raw inputs, highlights, and literature references.
- **Spaces** — High-level operational domains (e.g., Personal, Work).

**Example Directory Structure:**

```
ACCESS/
├── Atlas/
│   ├── Home.md
│   ├── MOC - Productivity.md
│   └── MOC - Writing.md
├── Calendar/
│   ├── Daily/
│   │   ├── 2024-10-01.md
│   │   └── 2024-10-02.md
│   └── Weekly/
│       └── 2024-W40.md
├── Cards/
│   ├── Atomic Habits Summary.md
│   ├── Flow State Triggers.md
│   └── Second Brain Principles.md
├── Extras/
│   ├── Templates/
│   │   └── Daily Note Template.md
│   └── Assets/
│       └── logo.png
├── Sources/
│   ├── Book - Building a Second Brain.md
│   └── Article - Digital Minimalism.md
└── Spaces/
    ├── Work/
    │   └── Project Alpha.md
    └── Personal/
        └── Fitness Plan.md
```

**Ideal for:** Networked thought environments that balance structured navigation with emergent links.

---

## Flat Search and Metadata-First Systems

The minimalist approach: organize files with zero or minimal folder depth, relying entirely on search and tags. The structure is simple — a small intake bucket or flat repository, with retrieval driven by full-text search, system tags, and structured naming conventions.

**Example Directory Structure:**

```javascript
Documents/
├── inbox/
│   ├── scan-receipt-2024-10-03.pdf
│   └── meeting-notes-kickoff.md
└── everything/
    ├── 2024-budget-final.xlsx          #finance
    ├── brand-guidelines-v2.pdf         #design #reference
    ├── recipe-sourdough-starter.md     #cooking
    ├── tax-return-2023.pdf             #finance #archive
    ├── project-alpha-proposal.docx     #work #projects
    └── reading-list-october.md         #reading
```

*No nested folders — retrieval depends on filename conventions, tags, and full-text search.*

**Ideal for:** Users who find folder maintenance inefficient and prefer rapid search tools like Spotlight, Raycast, or database queries.
