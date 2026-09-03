# LocalMind-RAG
# UI Design Specification

**Version:** 1.0  
**Status:** Design proposal — pending approval  
**Target:** Phase F — Next.js Frontend  
**Frontend:** Next.js App Router + TypeScript + Tailwind CSS  
**Backend:** Existing FastAPI REST + SSE API  
**Product principle:** **LocalMind should feel like a research instrument, not an AI toy.**

---

# 1. Purpose

This document defines the visual language, information architecture, interaction model, responsive behavior, component system, states, accessibility requirements, and implementation constraints for the LocalMind-RAG frontend.

It is the source of truth for Phase F frontend implementation.

The frontend must expose the capabilities of the existing LocalMind RAG system clearly without exposing internal chain-of-thought, raw agent state, internal prompts, or implementation details that are not useful to the user.

The existing backend already produces structured telemetry such as query type, planning information, retrieval/tool activity, citations, critique scores, reviewer consensus, and Trust & Safety information. The UI should selectively expose this information through progressive disclosure rather than displaying raw internal state.

---

# 2. Product Identity

## 2.1 Product definition

LocalMind is a local/private research workspace that allows a user to:

1. Ask questions about their indexed knowledge.
2. Inspect the evidence supporting answers.
3. Add and manage documents.
4. Explore relationships between concepts in the knowledge graph.
5. Understand, when useful, how the system reached an answer.

The product is not primarily an AI chatbot.

It is a **knowledge exploration and research instrument**.

---

# 3. Product North Star

> **The interface should make the intelligence of the system visible through behavior, not decoration.**

A user should understand that LocalMind is sophisticated because:

- retrieval is transparent,
- evidence is inspectable,
- citations are meaningful,
- execution progress is honest,
- documents are clearly indexed,
- graph relationships can be traced back to evidence,
- technical details are available when requested.

The interface must never depend on glowing effects, animated AI imagery, or marketing language to communicate intelligence.

---

# 4. Core Information Architecture

The application consists of one persistent shell containing three primary workspaces.

```text
LOCALMIND
│
├── Chat
│   ├── Recent conversations
│   ├── Conversation
│   ├── Evidence
│   └── Technical details
│
├── Documents
│   ├── Document library
│   ├── Upload
│   └── Document inspector
│
├── Knowledge Graph
│   ├── Graph exploration
│   ├── Search
│   ├── Node inspector
│   └── Evidence
│
└── Settings
```

Primary product language:

```text
Chat       = Ask your knowledge.
Documents  = Curate your knowledge.
Graph      = Explore your knowledge.
```

These three surfaces must feel like parts of one system rather than independent applications.

---

# 5. Application Shell

## 5.1 Desktop structure

```text
┌──────────────────────────────────────────────────────────────────────┐
│ LOCALMIND                                      ● Local system ready   │
├──────────────────┬───────────────────────────────────────────────────┤
│                  │                                                   │
│ + New chat       │                                                   │
│                  │                                                   │
│ RECENT           │                                                   │
│                  │                  MAIN WORKSPACE                   │
│ Conversation 1   │                                                   │
│ Conversation 2   │                                                   │
│ Conversation 3   │                                                   │
│                  │                                                   │
│ WORKSPACE        │                                                   │
│ Documents        │                                                   │
│ Knowledge Graph  │                                                   │
│                  │                                                   │
│                  │                                                   │
│ Settings         │                                                   │
└──────────────────┴───────────────────────────────────────────────────┘
```

## 5.2 Sidebar

Target width:

**~240px**

The sidebar is navigation, not a dashboard.

It contains:

### Brand

```text
● LOCALMIND
```

Use a minimal geometric identity mark if desired.

Do not use:

- brain logos,
- robot heads,
- glowing neural networks,
- circuit-board illustrations,
- generic AI imagery.

### New Chat

```text
+ New chat
```

This is the primary sidebar action.

### Recent

Display recent sessions returned by:

`GET /api/chat/sessions`

Sessions should be grouped naturally by recency where useful.

Example:

```text
TODAY

Hybrid retrieval
RAG architecture
Python notes

YESTERDAY

Quantum computing
```

Avoid displaying an excessive number of conversations.

### Workspace

```text
Documents
Knowledge Graph
```

### Bottom navigation

```text
Settings
```

System status may appear subtly near the bottom or top-right.

---

# 6. Active Navigation State

Navigation must not use oversized colored pills.

Preferred:

- subtle surface change,
- slightly increased text contrast,
- small leading icon,
- optional restrained accent indicator.

The active state should be obvious without becoming visually dominant.

---

# 7. Top Bar

The top bar provides page context and lightweight global status.

## Chat

```text
Hybrid Retrieval                                      ···
```

## Documents

```text
Documents                                      + Add documents
```

## Graph

```text
Knowledge Graph
```

Avoid redundant navigation inside the top bar.

The sidebar already provides primary navigation.

---

# 8. System Status

A compact indicator may appear in the global shell:

```text
● Local system ready
```

It should remain visually secondary.

Selecting it opens a diagnostic/status panel.

Example:

```text
System status

API                  ✓
RAG pipeline         ✓
Vector store         ✓
Local model          ✓
Knowledge graph      ✓
```

Only display information that the backend actually exposes or that can be reliably determined.

Do not invent health metrics.

---

# 9. Visual Language

## 9.1 Overall direction

Dark-first.

The visual style should be:

- calm,
- technical,
- premium,
- restrained,
- editorial,
- highly readable.

It must **not** resemble:

- hacker terminals,
- gaming interfaces,
- cyberpunk dashboards,
- generic AI SaaS landing pages.

## 9.2 Surface hierarchy

Use a small number of surfaces:

```text
background
surface
surface-hover
surface-active
overlay
```

Borders should establish hierarchy more often than shadows.

## 9.3 Accent

Use one restrained accent.

Accent is scarce.

It should primarily communicate:

- selected states,
- interactive elements,
- meaningful system status,
- citation interaction,
- important focus states.

Do not color every component.

---

# 10. Typography

Use a modern, highly readable sans-serif.

Hierarchy:

```text
Page title             24–28px
Section title          16–18px
Body                   15–16px
Secondary              13–14px
Metadata               12–13px
```

Answers should use approximately:

```text
16px
~1.65 line-height
```

Typography should create hierarchy through:

- size,
- spacing,
- weight,
- contrast.

Do not bold every heading.

Do not use uppercase text excessively.

---

# 11. Spacing

Use a consistent spacing scale:

```text
4
8
12
16
24
32
48
64
```

Avoid arbitrary spacing values scattered throughout components.

---

# 12. Border Radius

Moderate radius.

Approximate system:

```text
buttons       8px
inputs        10px
cards         10–12px
dialogs       12–14px
```

Pills are reserved for genuinely semantic compact statuses.

Do not turn every element into a pill.

---

# 13. Icons

Use one consistent icon family.

Icons should communicate function.

Do not use emojis as navigation or interface icons.

---

# 14. Motion

Motion must be functional.

Allowed:

- hover transitions,
- focus transitions,
- navigation transitions,
- drawer opening,
- dialog opening,
- streaming state transitions,
- completion state changes.

Approximate timing:

```text
micro       100–150ms
standard    150–250ms
```

Do not implement:

- glowing animations,
- particles,
- animated gradients,
- text scrambling,
- fake AI thinking,
- bouncing AI avatars,
- perpetual movement.

Respect reduced-motion preferences.

---

# 15. Anti-AI-Slop Rules

These are hard constraints.

The frontend must NOT contain:

- giant AI orb,
- robot/brain illustration,
- purple-blue AI gradient,
- excessive gradients,
- neon glow,
- animated particles,
- excessive glassmorphism,
- giant rounded cards,
- dashboard containing many unrelated cards,
- meaningless badges,
- fake agent activity,
- fake progress percentages,
- fake token streaming,
- “AI-powered” marketing copy,
- “Unlock the power of AI” language,
- generic chatbot greeting,
- stock AI illustrations,
- excessive shadows,
- decorative telemetry,
- invented metrics.

Do not add UI merely because it "looks AI."

---

# 16. Chat Workspace

Chat is the primary product surface.

The experience should feel closer to a research editor than a traditional chatbot.

## 16.1 Desktop layout

Target:

```text
sidebar ~240px
        ↓
central content ~760–900px
        ↓
comfortable surrounding whitespace
```

Do not stretch conversation text across the entire screen.

---

# 17. Chat Empty State

The initial screen should communicate what LocalMind does without sounding like marketing.

Preferred:

```text
LocalMind

Search your local knowledge.

Ask questions about your indexed documents
and explore what your knowledge base contains.

┌────────────────────────────────────────────┐
│ Ask your knowledge base...                 │
└────────────────────────────────────────────┘

Compare documents    Explain a concept    Find...
```

Do not use:

```text
Hello! How can I help you today?
```

Do not use:

```text
Your AI research assistant is ready!
```

---

# 18. User Message

User questions should remain visually simple.

Do not use oversized colored chat bubbles.

The question itself is the focus.

Example:

```text
How does hybrid retrieval improve RAG performance?
```

---

# 19. Chat Execution Trace

The backend SSE stream provides actual progress events.

The UI should map those events into a compact execution trace.

Example:

```text
Researching your knowledge

✓ Supervisor
  Comparative query

✓ Planner
  3 research steps

● Researcher
  Gathering evidence

○ Generator

○ Critic

○ Reviewer
```

For a simple factual query:

```text
Researching your knowledge

✓ Query analysis
● Retrieval
○ Generation
○ Verification
```

The exact stages displayed must correspond to actual SSE events.

Do not fabricate stages.

Do not invent percentages.

Do not claim that the model is "thinking."

---

# 20. Execution Trace Behavior

During execution:

- current stage receives emphasis,
- completed stages become quiet/checkmarked,
- pending stages remain subdued.

After completion, collapse the trace.

Collapsed form:

```text
3 sources · Hybrid retrieval · Verified 9.1/10
```

The user can expand it to inspect execution metadata.

This implements progressive disclosure.

---

# 21. Answer Hierarchy

The visual hierarchy is:

```text
Answer
  ↓
Evidence
  ↓
System metadata
```

The answer must always be more prominent than internal telemetry.

Technical information must never overwhelm the answer.

---

# 22. Citations

Citations should be interactive.

Example:

```text
Hybrid retrieval combines multiple retrieval
signals to improve evidence coverage.[1][2]
```

Clicking `[1]` opens the relevant source inspector.

Citation markers must remain associated with the corresponding evidence.

Do not create decorative citation chips unrelated to actual evidence.

---

# 23. Source Inspector

Desktop:

**right-side inspector**

Mobile:

**bottom sheet/full-screen inspector**

Example:

```text
RAG Architecture.pdf

PDF
Section 3 — Retrieval

Page 12

Relevant passage
────────────────────────

"..."

────────────────────────

Retrieval
Hybrid retrieval
Reranked result

Open document →
```

Only display metadata actually supplied by the backend.

Do not invent page numbers, sections, scores, or provenance.

---

# 24. Technical Details

Technical information should be hidden behind progressive disclosure.

Example:

```text
Technical details
```

Expanded:

```text
Retrieval
Dense
BM25
RRF
Reranker

Generation
Local model

Evaluation
Faithfulness
Completeness
Consensus

Execution
Iterations
Graph RAG
```

The backend's telemetry includes retrieval/tool activity, graph usage, critique, reviewer consensus, and TSL information, so these are appropriate candidates for technical inspection where available.

Never expose:

- raw prompts,
- chain-of-thought,
- private inter-agent reasoning,
- raw LangGraph state,
- internal messages intended only for orchestration.

---

# 25. Memory Context

Memory should never be marketed as:

```text
LONG-TERM MEMORY ACTIVE
```

Instead:

```text
↳ Conversation context used
```

Clicking it may explain what kind of context was used.

Keep this subtle.

---

# 26. Retrieval Failure

When evidence is insufficient:

```text
I couldn't find enough relevant evidence
in your local knowledge base to answer this reliably.

Try narrowing the question or adding a relevant document.
```

Do not hallucinate an answer simply to avoid an empty state.

---

# 27. Guardrail Response

A blocked request should appear as a normal product response.

Avoid giant red warning panels.

Example:

```text
I can't help with that request.
```

Optional concise explanation.

Technical safety diagnostics remain behind details where appropriate.

---

# 28. Backend Error

Example:

```text
Something went wrong.

The conversation wasn't saved.
Please try again.

Run reference: XXXXX

Try again
```

Do not dump stack traces into the interface.

---

# 29. Conversation Scroll

Default behavior:

- keep the newest content visible,
- automatically scroll while the user is at the bottom,
- stop automatic scrolling if the user manually scrolls upward.

When new content arrives while the user is away from the bottom:

```text
↓ New response
```

Clicking returns to the latest content.

---

# 30. Stop Generation

A stop button may only be shown if actual backend cancellation is supported.

Do not implement fake cancellation that merely hides the UI while the backend continues processing.

---

# 31. Documents Workspace

Purpose:

> **Understand what LocalMind knows and manage the indexed knowledge base.**

The page should feel like a document library.

Not a dashboard.

---

# 32. Documents Header

```text
Documents

Your local knowledge base

12 documents · 1,284 indexed chunks

+ Add documents
```

Counts must come from actual backend data.

---

# 33. Document Search and Filtering

Provide:

```text
Search documents...
```

Optional file-type filters:

```text
All
PDF
DOCX
DOC
TXT
MD
```

Only expose filters that correspond to supported ingestion formats.

The current ingestion API supports PDF, DOCX, DOC, TXT and MD. The upload endpoint also supports chunking strategy, category, and optional graph construction.

---

# 34. Document List

Use rows.

Example:

```text
▣ RAG Architecture.pdf                       ✓ Indexed
  PDF · 86 chunks · Added today

▣ Python.docx                                ✓ Indexed
  DOCX · 233 chunks · Added yesterday
```

Use subtle separators.

Avoid giant document cards.

---

# 35. Document Statuses

Supported conceptual states:

```text
Uploading
Processing
Indexing
Indexed
Failed
```

Only display real progress if the backend supplies real progress.

Never show:

```text
73% AI processing...
```

unless that percentage is genuinely provided by the backend.

---

# 36. Upload Modal

```text
Add documents

Add knowledge to your local workspace.

┌─────────────────────────────────────────────┐
│                                             │
│       Drop files here / browse              │
│                                             │
│       PDF · DOCX · DOC · TXT · MD           │
│       Max 25 MB                              │
│                                             │
└─────────────────────────────────────────────┘

Advanced options ▾

Cancel                         Add documents
```

The backend currently enforces a 25 MB upload limit and validates supported extensions/MIME types.

---

# 37. Upload Advanced Options

```text
Chunking strategy

○ Sentence
○ Parent-Child
○ Semantic

Document category
[________________]

☐ Build knowledge graph
```

Only expose options supported by the backend.

Do not expose imagined configuration such as:

- embedding model selection,
- LLM selection,
- reranker selection,
- vector database selection,

unless the backend exposes those capabilities to users.

---

# 38. Multi-file Upload

Multiple files may be selected.

The UI should show individual states:

```text
RAG Architecture.pdf      ✓ Indexed
Python.docx               Processing
Notes.md                  Failed
```

Failure should expose a retry action where supported.

---

# 39. Document Inspector

Selecting a document opens a side inspector.

```text
RAG Architecture.pdf

✓ Indexed

PDF
86 chunks
Added today
12.4 MB

Category
Research

Strategy
Sentence

Knowledge graph
Not built

────────────────────

Delete document
```

Only display backend-supported metadata.

---

# 40. Document Deletion

Confirmation:

```text
Delete document?

This removes the document from your local
knowledge base and its indexed content.

Cancel                         Delete
```

No vague language.

---

# 41. Documents Empty State

```text
Nothing here yet.

Add documents to give LocalMind
something to search.

+ Add documents
```

---

# 42. Knowledge Graph Workspace

Purpose:

1. Discover concepts/entities.
2. Understand relationships.
3. Trace relationships to source evidence.
4. Explore a specific concept.

The graph is an analytical tool.

It is not a visual spectacle.

---

# 43. Graph Header

```text
Knowledge Graph

Explore relationships across your knowledge base

248 nodes · 431 relationships
```

Counts must come from actual graph data.

Do not invent graph metrics.

---

# 44. Graph Search

Search should be prominent:

```text
Search concepts, entities, documents...
```

The user should be able to locate something rather than manually hunting through a large graph.

---

# 45. Graph Canvas

The graph should use understated visual encoding.

Nodes may communicate type through:

- subtle shape,
- size,
- restrained accent,
- label treatment.

Highly connected nodes can be slightly larger.

Edges should remain visually quiet.

Do not use:

- neon nodes,
- glowing edges,
- rainbow node colors,
- animated particles,
- constant node movement.

---

# 46. Graph Interaction

When a node is selected:

- highlight selected node,
- highlight connected nodes,
- fade unrelated nodes.

Do not re-render the entire interface unnecessarily.

The selected node becomes the focus of the inspector.

---

# 47. Node Inspector

Example:

```text
BM25

Retrieval method

Relationships

Hybrid retrieval
Reranker
Sparse retrieval

Source documents

RAG Architecture.pdf
Retrieval Notes.md

Explore evidence →
```

The exact node metadata must come from the graph backend.

---

# 48. Graph Evidence Flow

The central conceptual interaction is:

```text
Graph node
    ↓
Relationship
    ↓
Document
    ↓
Evidence
```

This should allow the user to move from abstract graph structure to concrete source material.

Reuse the same source inspector concept used by Chat.

---

# 49. Graph Focus Controls

Compact controls:

```text
Focus: BM25
1 hop ▼
```

Options:

```text
1 hop
2 hops
3 hops
```

Only expose hop depths supported by the graph retrieval implementation.

---

# 50. Graph Controls

Provide:

```text
Zoom out
Zoom in
Reset
Fit
Fullscreen
```

Controls should remain compact.

---

# 51. Large Graph Behavior

Do not blindly render every node if the graph becomes large.

Preferred behavior:

```text
Overview
   ↓
Search
   ↓
Focus
   ↓
Expand relationships
```

The user should search/focus before the interface attempts to display an enormous graph.

---

# 52. Graph Empty State

```text
Your knowledge graph is empty.

Build a graph from your indexed documents
to explore relationships between concepts.

Go to Documents →
```

---

# 53. Graph Loading

Preferred:

```text
Loading knowledge graph...

Preparing your knowledge base
```

Do not animate fake nodes into existence.

If a real node count is available:

```text
Loading knowledge graph...

Preparing 248 nodes
```

---

# 54. Graph Error

```text
We couldn't load the knowledge graph.

Your documents are still available.

Retry
```

---

# 55. Cross-feature Navigation

The three surfaces should be connected.

Example:

```text
Chat
  ↓
Citation / concept
  ↓
Explore in graph →
  ↓
Graph focused on concept
  ↓
Node relationship
  ↓
Evidence
```

This is an important part of making LocalMind feel like one system.

---

# 56. Mobile Shell

Mobile must be intentionally designed.

Do not simply compress the desktop layout.

Top:

```text
┌─────────────────────────────┐
│ ☰   LOCALMIND         ···  │
└─────────────────────────────┘
```

Main workspace fills the viewport.

---

# 57. Mobile Navigation Drawer

```text
LOCALMIND                         ×

+ New chat

RECENT

Hybrid retrieval
Python notes
Quantum computing

WORKSPACE

Documents
Knowledge Graph

────────────────────

Settings
```

The drawer closes after navigation.

---

# 58. Mobile Chat

Structure:

```text
conversation

────────────────────────────

Ask your knowledge...       ↑
```

Input remains easily accessible.

The conversation should have sufficient horizontal padding for comfortable reading.

---

# 59. Mobile Source Inspector

Desktop:

```text
right-side panel
```

Mobile:

```text
bottom sheet
```

For larger evidence content, the sheet can become full-screen.

---

# 60. Mobile Technical Details

Technical details become a full-width expandable section.

Avoid nested side panels.

---

# 61. Mobile Documents

Use vertical document rows.

Example:

```text
Documents

+ Add

Search...

RAG Architecture.pdf
PDF · 86 chunks
✓ Indexed

Python.docx
DOCX · 233 chunks
✓ Indexed
```

Avoid horizontal-scroll tables.

---

# 62. Mobile Graph

The graph gets the available viewport.

Controls remain compact.

Node inspector becomes a bottom sheet.

Search remains accessible.

---

# 63. Global Loading System

Use layout-matching skeletons.

Example:

```text
Documents

████████████████

────────────────────
████████████████████
████████████████
────────────────────
████████████████████
████████████████
```

Avoid a single centered spinner for the entire application.

---

# 64. Global Error System

Every error should answer:

1. What happened?
2. What can the user do?

Example:

```text
We couldn't load your documents.

Try again. If the problem continues,
check local system status.

Retry
```

Technical diagnostics should be progressively disclosed.

---

# 65. Toast System

Use only for short-lived confirmations.

Good:

```text
✓ Document added
```

```text
✓ Conversation deleted
```

Bad:

```text
🎉 AMAZING!
Your AI knowledge has been SUPERCHARGED!
```

---

# 66. Dialog System

Dialogs are reserved for:

- destructive actions,
- important confirmations,
- focused configuration.

Do not turn ordinary navigation into modal workflows.

---

# 67. Accessibility

Minimum requirements:

- semantic HTML,
- keyboard navigation,
- visible focus states,
- sufficient contrast,
- accessible labels,
- accessible buttons,
- accessible dialogs,
- focus trapping for modal dialogs,
- screen-reader-friendly status updates,
- reduced-motion support,
- keyboard-accessible citation interactions.

The graph cannot be the only way users can access graph information.

Search and the node inspector must provide an accessible alternative to visual graph interpretation.

---

# 68. Keyboard Behavior

Chat:

```text
Ctrl/Cmd + Enter
Send
```

Other expected behavior:

```text
Esc
Close active inspector/dialog
```

All interactive controls must be keyboard reachable.

---

# 69. Component Architecture

Suggested component organization:

```text
frontend/
│
├── app/
│   ├── page.tsx
│   ├── chat/
│   │   └── page.tsx
│   ├── documents/
│   │   └── page.tsx
│   ├── graph/
│   │   └── page.tsx
│   └── settings/
│       └── page.tsx
│
├── components/
│   ├── shell/
│   │   ├── AppShell
│   │   ├── Sidebar
│   │   ├── MobileNav
│   │   ├── TopBar
│   │   └── SystemStatus
│   │
│   ├── chat/
│   │   ├── ChatWorkspace
│   │   ├── MessageList
│   │   ├── MessageItem
│   │   ├── ChatInput
│   │   ├── ExecutionTrace
│   │   ├── Citation
│   │   ├── SourceInspector
│   │   └── TechnicalDetails
│   │
│   ├── documents/
│   │   ├── DocumentLibrary
│   │   ├── DocumentRow
│   │   ├── UploadDialog
│   │   ├── UploadDropzone
│   │   └── DocumentInspector
│   │
│   ├── graph/
│   │   ├── GraphWorkspace
│   │   ├── GraphCanvas
│   │   ├── GraphSearch
│   │   ├── GraphControls
│   │   └── NodeInspector
│   │
│   └── ui/
│       ├── Button
│       ├── Input
│       ├── Dialog
│       ├── Drawer
│       ├── Sheet
│       ├── Skeleton
│       ├── Toast
│       └── Status
│
├── lib/
│   ├── api.ts
│   ├── sse.ts
│   └── types.ts
│
└── hooks/
    ├── useChat.ts
    ├── useSessions.ts
    ├── useDocuments.ts
    └── useGraph.ts
```

This structure is guidance rather than permission to invent additional product features.

---

# 70. API Integration Constraints

The frontend must consume the existing FastAPI API.

Known endpoints include:

```text
GET    /api/health

POST   /api/chat
POST   /api/chat/stream

POST   /api/documents/upload
GET    /api/documents

GET    /api/chat/sessions
GET    /api/chat/sessions/{session_id}
DELETE /api/chat/sessions/{session_id}
```

The existing architecture specifically defines Next.js as the frontend communicating with FastAPI over HTTP/SSE.

Do not bypass FastAPI.

Do not import Python backend logic into Next.js.

Do not duplicate RAG logic in TypeScript.

---

# 71. Chat API Contract

The chat request supports:

```json
{
  "query": "...",
  "session_id": "...",
  "user_role": "analyst",
  "use_memory": true
}
```

The frontend must preserve `session_id` across turns.

If no session exists, the backend may generate one.

Session state is therefore a frontend responsibility.

The backend documentation explicitly requires the client to continuously pass `session_id` for conversational continuity.

---

# 72. SSE Integration

The streaming endpoint is:

```text
POST /api/chat/stream
```

The frontend should consume actual SSE events.

The UI must not simulate backend progress.

Event-to-UI mapping must be deterministic.

For example:

```text
firewall     → safety/input state
memory       → memory context state
supervisor   → query analysis
planner      → planning
retrieval    → research
generation   → answer generation
critique     → verification
review       → review
refinement   → refinement
tsl          → safety verification
final        → completed answer
error        → error state
```

Only events actually emitted by the backend should be rendered.

---

# 73. Data Ownership

Frontend owns:

- active session ID,
- current conversation view,
- UI state,
- selected citation,
- open inspector,
- graph viewport,
- filters,
- temporary upload UI state.

Backend owns:

- RAG execution,
- memory,
- session persistence,
- document indexing,
- retrieval,
- graph data,
- evaluation,
- Trust & Safety,
- canonical answer generation.

Do not duplicate backend state unnecessarily.

---

# 74. Session Lifecycle

New chat:

```text
User clicks New chat
        ↓
Frontend clears active session
        ↓
Next query sends session_id = null
        ↓
Backend creates session
        ↓
Frontend stores returned session_id
```

Continuation:

```text
existing session_id
        ↓
POST /api/chat/stream
        ↓
conversation continues
```

Session history is loaded from:

```text
GET /api/chat/sessions/{session_id}
```

---

# 75. Delete Session UX

Before deletion:

```text
Delete conversation?

This removes the conversation history.

Your saved knowledge and memories remain.

Cancel                         Delete
```

This distinction matters because conversation persistence and longer-lived memory are separate concepts in the backend. The session implementation preserves semantic/user-profile/memory data when a session is deleted.

---

# 76. Documents API Integration

Upload through:

```text
POST /api/documents/upload
```

List through:

```text
GET /api/documents
```

The frontend must represent actual backend results.

The ingestion architecture performs document loading, structure parsing, chunking, node persistence, BM25 construction, dense indexing and optional graph construction.

---

# 77. Graph Data

The UI must only visualize graph semantics supplied by the backend.

Do not invent:

- relationship categories,
- node categories,
- graph metrics,
- provenance,
- centrality scores.

The graph should remain an evidence-exploration interface.

---

# 78. State Model

Each major screen must explicitly support:

```text
idle
loading
success
empty
error
```

Chat additionally supports:

```text
streaming
blocked
insufficient evidence
```

Documents additionally support:

```text
uploading
processing
indexing
indexed
failed
```

Graph additionally supports:

```text
loading graph
graph loaded
node selected
empty graph
graph error
```

---

# 79. Progressive Disclosure

Default interface:

```text
Answer
Sources
Minimal execution summary
```

Expanded:

```text
Execution trace
Retrieval details
Evaluation
Memory information
TSL information
```

The system should remain understandable to a normal user without requiring knowledge of RAG terminology.

Experts can inspect technical details when desired.

---

# 80. Language Guidelines

Prefer:

```text
Searching your knowledge
```

over:

```text
Activating autonomous neural retrieval agents
```

Prefer:

```text
Evidence
```

over:

```text
AI Knowledge Proof Matrix
```

Prefer:

```text
Verified
```

over:

```text
TRUST SCORE: ULTRA HIGH
```

Prefer:

```text
3 sources · Hybrid retrieval
```

over:

```text
POWERED BY ADVANCED MULTI-AGENT AI
```

The interface should describe what the system actually did.

---

# 81. What the UI Must Never Claim

The frontend must never claim:

- that the model is thinking,
- that a tool ran when it did not,
- that a document was indexed when it was not,
- that an answer is verified when no verification occurred,
- that a citation supports an answer when the backend did not provide it,
- that a progress percentage exists when it does not,
- that cancellation occurred when the backend did not cancel,
- that memory was used when it was not,
- that graph retrieval occurred when it did not.

This is especially important because the backend has real structured execution telemetry. The UI should expose truth rather than simulate sophistication.

---

# 82. Performance Expectations

The backend can take approximately 15–45+ seconds for a full local query because of planning, retrieval, reranking, multi-agent execution, evaluation, and local inference.

Therefore:

- never freeze the interface,
- show actual execution progress,
- preserve the user's question,
- keep navigation available,
- make the waiting state informative but quiet,
- handle connection interruption gracefully.

---

# 83. Visual Quality Acceptance Criteria

The frontend is not complete merely because the routes work.

It must pass a visual review.

### The UI should feel:

- coherent,
- calm,
- intentional,
- technically sophisticated,
- readable,
- premium,
- restrained.

### It should NOT feel:

- generic,
- template-generated,
- overdecorated,
- overly rounded,
- neon,
- futuristic for its own sake,
- like a ChatGPT clone,
- like a SaaS marketing dashboard.

---

# 84. Implementation Acceptance Checklist

Before Phase F is considered complete:

## Shell

- [ ] Persistent desktop sidebar.
- [ ] Responsive mobile navigation.
- [ ] Consistent top bar.
- [ ] System status.
- [ ] New chat works.
- [ ] Session list works.
- [ ] Navigation works.

## Chat

- [ ] Empty state.
- [ ] Message rendering.
- [ ] SSE streaming.
- [ ] Real execution trace.
- [ ] Citation interaction.
- [ ] Source inspector.
- [ ] Technical details.
- [ ] Memory indicator.
- [ ] Error states.
- [ ] Guardrail state.
- [ ] Insufficient evidence state.
- [ ] Scroll behavior.
- [ ] Session persistence.

## Documents

- [ ] Document listing.
- [ ] Search/filter UI.
- [ ] Upload dialog.
- [ ] Drag/drop.
- [ ] Supported file types.
- [ ] 25 MB limit.
- [ ] Real upload state.
- [ ] Processing/indexing state.
- [ ] Failure state.
- [ ] Document inspector.
- [ ] Delete confirmation.

## Graph

- [ ] Graph loading.
- [ ] Graph rendering.
- [ ] Search.
- [ ] Node selection.
- [ ] Connected-node highlighting.
- [ ] Node inspector.
- [ ] Focus/hop control.
- [ ] Zoom/reset/fit.
- [ ] Evidence navigation.
- [ ] Empty state.
- [ ] Error state.

## Responsive

- [ ] Desktop.
- [ ] Tablet.
- [ ] Mobile.
- [ ] Mobile source sheet.
- [ ] Mobile node sheet.
- [ ] Mobile navigation.

## Accessibility

- [ ] Keyboard navigation.
- [ ] Focus states.
- [ ] Semantic controls.
- [ ] Accessible dialogs.
- [ ] Screen-reader status updates.
- [ ] Reduced motion.
- [ ] Contrast.

---

# 85. Explicit Non-Goals for Phase F

Do NOT add:

- authentication unless already required by the current API contract,
- billing,
- multi-user organizations,
- sharing,
- collaborative editing,
- web search UI,
- MCP controls,
- model selection UI,
- prompt editing UI,
- admin dashboard,
- analytics dashboard,
- arbitrary settings,
- document editing,
- chat export,
- artificial AI onboarding,
- marketing landing page inside the application.

These can be future phases if required.

---

# 86. Final Design Philosophy

LocalMind's frontend should communicate one idea:

```text
Your knowledge
       ↓
Documents
       ↓
Retrieval
       ↓
Evidence
       ↓
Reasoned answer
       ↓
Inspectable result
```

The user should be able to move naturally between these layers.

```text
ASK
 ↓
UNDERSTAND
 ↓
INSPECT
 ↓
EXPLORE
 ↓
TRACE TO EVIDENCE
```

The interface does not need to tell the user that LocalMind is intelligent.

It needs to **demonstrate it through the quality and transparency of the interaction.**

---

# 87. Final North Star

> **LocalMind is a research instrument for exploring your own knowledge.**

Every UI decision should reinforce that sentence.

If a visual element does not improve:

- understanding,
- navigation,
- evidence inspection,
- knowledge exploration,
- or system transparency,

it should probably not exist.