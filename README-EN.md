# Enterprise Responsive Layout System

A **zero-dependency · single-file · double-click-to-run** visual HTML layout designer. Built on absolute positioning + vh-based proportional scaling, purpose-built for data dashboards, control panels, and fixed-layout page design.

---

## Quick Start

1. Double-click `layout.html` to open
2. Right-click empty canvas area → **Add Element**, or insert from templates
3. **Drag** to move elements, use **8-direction resize handles** to adjust dimensions
4. Right-click an element → Edit HTML / JSON / styles
5. Export as static HTML or JSON archive

Zero config, zero install, runs entirely in the browser.

---

## Core Features

### Canvas Operations

| Action | Description |
|--------|-------------|
| Drag & Move | Drag selected elements with auto-snap alignment guides |
| 8-Direction Resize | Drag any of the eight resize handles |
| Smart Snap Lines | Edge alignment (red), center alignment (blue), canvas center (purple), equal spacing (green), same-size (orange) |
| Arrow Key Nudge | `↑↓←→` for precise movement, hold `Shift` to accelerate |
| Preview Mode | Right-click canvas → Toggle Preview, or `ESC` to exit |

### Element Context Menu

- **Edit Element HTML** — Inline Monaco Editor with CSS / JS support
- **Edit Element JSON** — Directly modify the element's JSON configuration
- **Auto-Height** — Content-driven height with cascading reposition of all elements below
- **Alignment** — Left, center-horizontal, right, top, center-vertical, bottom
- **Layer Order** — Bring to front / forward / backward / send to back
- **Layer Manager** — Visual layer panel with rename, lock, hide, and drag-to-reorder
- **Duplicate / Delete** element
- **Copy Element ID**

### Canvas Context Menu

- Add element / Insert from template
- Layer manager
- **Page Background** — Solid color / image background, with opacity and display mode controls
- **Global CSS / JS** — Inject custom styles or scripts across the entire canvas
- Export static HTML / Export layout JSON / Import layout JSON
- Clear canvas (confirmation required)

### Template System

Built-in preset templates (cards, panels, chart containers, etc.). Right-click canvas → **Insert from Template** to use.

### AI-Assisted Generation

Integrated DeepSeek API — enter natural language prompts in the editor and AI generates/modifies HTML code. Requires your own DeepSeek API Key (stored only in local browser storage).

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl + Z` | Undo |
| `Ctrl + Shift + Z` / `Ctrl + Y` | Redo |
| `Ctrl + S` | Export static HTML |
| `Delete` / `Backspace` | Delete selected element |
| `↑ ↓ ← →` | Nudge position (Shift to accelerate) |
| `ESC` | Exit preview mode / close dialogs |

---

## Architecture

### Coordinate System

- **Absolute positioning** (`position: absolute`): pixel-level precision placement
- **vh-based proportional scaling**: position and height stored as viewport height percentages, maintaining proportional relationships on window resize
- **Horizontal width**: stored as percentages, adapting to varying widths

### Auto-Height Mode

A specialized layout mode. When enabled:

1. Element height is determined by actual rendered content height (`height: auto`)
2. `ResizeObserver` monitors content size changes
3. All elements below are **cascaded downward** while preserving relative spacing
4. Snapshot-correction algorithm ensures positional consistency on window resize

Ideal for: dynamically-sized cards, comment sections, collapsible panels, etc.

### Data Persistence

- **Auto-save**: automatically writes to browser `localStorage` after each operation
- **JSON export/import**: full layout state serialization for cross-device migration
- **Static HTML export**: generates a standalone HTML file with no editor dependency
- **Undo/Redo**: up to 50 steps of history

---

## Use Cases

- Data visualization dashboards
- Console / admin panel interfaces
- Fixed-layout web pages
- HTML email templates
- Rapid prototyping

---

## Non-Use Cases

- Responsive layout pages (vh system does not handle breakpoints)
- Long-form document flow (absolute positioning ignores document flow)
- Complex component nesting (no parent-child semantic relationships between elements)

---

## Technical Details

- Pure frontend, zero backend dependencies
- Font Awesome 6.5 CDN icon library (internet required)
- Monaco Editor CDN (syntax highlighting for HTML/JSON editing)
- Built-in XSS protection (safe escaping for HTML attributes, styles, and scripts)
- `localStorage` fault tolerance (private browsing / QuotaExceeded graceful degradation)
