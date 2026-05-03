# Output Preferences — Amit Rajpurkar

## Guiding principle

Every artifact Cowork produces must be self-documenting, self-contained, and commit-ready. A person picking up any output — six months later, with no prior context — should understand its purpose, scope, and reasoning without needing to ask questions. If that test cannot be passed, the artifact is incomplete.

---

## Naming conventions

This is one of the most important standards in this file. Apply it to every artifact Cowork produces: file names, section headings, variable names, component names, diagram labels, and task names.

### Rule 1 — Nouns for objects, verbs for actions

- Things that exist (documents, components, services, data structures) get **noun names**
- Things that happen (tasks, processes, scripts, operations) get **verb-led names**

| Type | Bad name | Good name |
|---|---|---|
| Architecture document | `doc1.md`, `architecture.md` | `payment-gateway-integration-architecture.md` |
| Analysis file | `analysis.md`, `notes.md` | `api-latency-root-cause-analysis.md` |
| Script that runs a build | `run.sh`, `script.sh` | `build-and-package-service.sh` |
| ADR | `decision.md` | `adopt-event-sourcing-for-audit-trail.md` |
| Diagram | `diagram.png` | `order-fulfilment-context-diagram.png` |

### Rule 2 — Short, descriptive, and self-documenting

Names must describe intent and purpose — not implementation, not contents, not the date.

- Use kebab-case for all file names: `word-word-word.md`
- Maximum 5–6 words in a file name; if more are needed, the scope is probably too broad
- No generic words: `temp`, `util`, `helper`, `misc`, `draft`, `new`, `v2` are not acceptable as standalone names
- No timestamps in file names unless the file is explicitly a dated log or report

### Rule 3 — Names must survive without their folder context

A file named `architecture.md` inside a folder called `payment-gateway/` only makes sense with both pieces. A file named `payment-gateway-integration-architecture.md` makes sense anywhere. Always name as if the file could be moved.

---

## File format standards

### Primary working format: Markdown

All working documents, analyses, notes, architecture documents, ADRs, and drafts are produced as `.md` files.

- Markdown is the source of truth for all content
- Files must be clean, well-structured markdown — valid for rendering on GitHub without modification
- Use ATX-style headings (`#`, `##`, `###`) — not underline-style
- Use fenced code blocks with language identifiers (` ```java `, ` ```bash `, ` ```json `) — never raw unformatted code blocks
- Use tables for structured comparative information — not bullet lists of pairs
- Use numbered lists for sequential steps; use bullet lists for unordered items

### Deliverable conversion pipeline

```
Working draft (.md)
        ↓
Reviewed and finalised in markdown
        ↓
Committed to GitHub repository
        ↓
Converted to PowerPoint (.pptx) or PDF for stakeholder distribution
```

Cowork should produce markdown as the primary output. Do not produce Word documents, plain text files, or HTML unless explicitly requested. When a task is destined for stakeholder presentation, note it in the output so the conversion step is not forgotten — but still produce markdown first.

---

## Document structure standards

### Every document must open with a header block

```markdown
# [Self-documenting document title]

**Purpose:** [One sentence — what this document is for]
**Audience:** [Who this is written for — e.g., "Engineering leads and solution architects"]
**Status:** [Draft | In Review | Accepted | Superseded]
**Last updated:** [Date]
**Related documents:** [Links or references to connected ADRs, architecture docs, usage guides]
```

This block makes the document's intent immediately clear to any reader, including Cowork in a future session where context must be re-established.

### Project root structure

All projects Cowork works on follow this structure unless Amit explicitly specifies otherwise:

```
project-root/
├── README.md
├── docs/
│   ├── architecture.md
│   └── usage-guide.md
└── [additional folders as appropriate]
```

**README.md responsibilities:**
- State what the project is and why it exists (2–3 sentences)
- Explain how to use or navigate it
- Explicitly reference `docs/architecture.md` and `docs/usage-guide.md` in appropriate sections
- Do not duplicate content from those files — reference, do not repeat

**docs/architecture.md responsibilities:**
- Document system design decisions, component relationships, and integration patterns
- Reference relevant ADRs
- Include or link to diagrams at the appropriate C4 level

**docs/usage-guide.md responsibilities:**
- Explain how to set up, run, operate, or extend the system
- Written for a technical reader who was not involved in building it
- Must include prerequisites, step-by-step instructions, and known failure modes

### ADR storage

Architecture Decision Records are stored at:

```
project-root/
└── docs/
    └── decisions/
        ├── ADR-001-[descriptive-title].md
        ├── ADR-002-[descriptive-title].md
        └── ...
```

ADRs are numbered sequentially and never deleted — superseded ADRs are marked with status `Superseded by ADR-N` and kept for historical traceability.

---

## Writing style standards

### Tone

- **Professional and precise** — not casual, not academic, not overly formal
- **Direct** — state the point first, then support it. Do not build to a conclusion
- **Plain language** — use the simplest word that is accurate. Do not use jargon when a plain word works equally well
- **Active voice** by default — passive voice only when the subject is genuinely unknown or irrelevant

### Length

- Match depth to complexity — do not pad, do not truncate important detail
- Sections that are not relevant to a specific document may be omitted — do not add placeholder sections
- Executive summaries and purpose statements must be concise: 2–4 sentences maximum
- Technical detail sections should be as long as necessary and no longer

### What to avoid

| Avoid | Use instead |
|---|---|
| "It is worth noting that..." | State the point directly |
| "As mentioned above..." | Repeat the relevant fact briefly or use a reference link |
| "In conclusion..." | End when the content is complete |
| "This document aims to..." | State what the document does, not what it aims to do |
| Vague intensifiers: "very", "quite", "rather" | Remove or replace with specific language |
| Hedging without reason: "might", "could potentially" | Commit to the statement or explicitly flag uncertainty |
| Unexplained acronyms | Define on first use: "Application Programming Interface (API)" |

### Uncertainty handling

When Cowork is not certain about a fact, recommendation, or design decision:

- State the uncertainty explicitly: "This assumes X — confirm before proceeding"
- Do not paper over uncertainty with confident-sounding language
- Flag open questions in a dedicated section at the end of the document:

```markdown
## Open questions

- [ ] [Question] — [what would resolve it and who owns the answer]
```

---

## Diagram and visual output standards

When a task calls for an architecture diagram, Cowork should:

1. Identify the appropriate C4 level: Context, Container, Component, or Code
2. Name the diagram file following the naming convention: `[system]-[level]-diagram.md` or `.png`
3. Include the diagram inline in the relevant architecture document as well as saving it separately
4. Add a caption below every diagram explaining what it shows and at what level of abstraction

Prefer text-based diagram formats (Mermaid, PlantUML, or C4 DSL in markdown) over binary image files where possible — these can be version-controlled and diffed in GitHub.

---

## GitHub commit-readiness checklist

Before any file is considered complete, it must pass these checks:

- [ ] File name follows naming convention — self-describing, kebab-case, no generic words
- [ ] Header block is present and complete (purpose, audience, status, date)
- [ ] All code blocks have language identifiers
- [ ] No placeholder text (`TODO`, `TBD`, `[fill this in]`) left in the document
- [ ] All acronyms defined on first use
- [ ] Open questions documented in the open questions section, not scattered inline
- [ ] Related documents referenced explicitly
- [ ] Document renders cleanly in GitHub markdown preview (tables, headings, code blocks all valid)

---

## What Cowork must not produce

- Files named with generic, non-descriptive names (`output.md`, `draft.md`, `analysis.md`)
- Documents without a header block stating purpose, audience, and status
- Markdown with formatting errors that would break GitHub rendering
- Unexplained acronyms or undefined domain terms
- Content that mixes concerns — if a document is doing two things, it should be two documents
- Placeholder sections with no content — omit sections that do not apply rather than leaving them empty
