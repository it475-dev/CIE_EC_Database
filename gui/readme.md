# CIE Engineered Controls Explorer

A standalone, browser-based dashboard for exploring the **Cyber-Informed Engineering (CIE) Engineered Controls Database** developed at Idaho National Laboratory. No server, no installation, no dependencies to manage — open the HTML file and go.

---

## What Is This?

The CIE Engineered Controls Database catalogs physical and procedural controls that can be applied across all 18 DHS Critical Infrastructure sectors to improve cyber-physical resilience. Each control is mapped to:

- A **resilience role** (e.g., Prevent impact, Accelerate recovery)
- A **category** (e.g., Fail-safe default, Redundant physical+digital)
- A **critical function** within a sector/subsector/asset scope
- A **type** — either *Known in Use* (deployed in practice) or *Idea/Opportunity* (possible but no evidence of use captured)

The dashboard makes this 60,000+ entry database navigable, searchable, and analytically useful without requiring any software installation.

---

## Features

### Hierarchy Browser

Walk the full DHS Infrastructure Taxonomy tree from Sector down to Asset level using interactive cards. Each card shows the **recursive total** of all controls beneath it in the tree — not just those tagged at that scope level.

- Click a card to drill down; the unselected cards dim to indicate scope narrowing
- Each new level of the taxonomy animates in below the previous
- A breadcrumb bar tracks your current position and lets you jump back to any ancestor level
- The **Hide/Show hierarchy** toggle collapses the card rows with an ease-in-out animation so you can maximize screen space for the table and analytics while retaining the breadcrumb context

### Controls Table

A paginated, sortable table showing all controls within the currently selected scope and active filters.

- Sort by any column (Name, Category, Scope, Critical Function)
- 25 rows per page with full pagination controls
- Click any row to open a **detail side panel** with the full control description, resilience roles, fail-safe status, implementation notes, and sector context

### Analytics Tab

Live charts that update to reflect the current hierarchy selection and sidebar filters:

- **Top 15 categories** — horizontal bar chart of most common control categories
- **Resilience role distribution** — color-coded by role across the six CIE resilience stages
- **Controls per scope** — breakdown among the direct children of the currently selected node (or all sectors at the top level), using fully recursive counts
- **Known vs Ideas donut** — proportion of known-in-use vs. potential for use (ideas) with no guarantee of use in a sector context.

### Filter Sidebar

Narrow controls by:

- Control type (Known in Use / Idea & Opportunity)
- Scope level (Sector → Subsector → Segment → Subsegment → Asset)
- Resilience role
- Priority (High / Medium / Low, applies to Ideas)
- Fail-safe status

Filters stack with the hierarchy selection and search — all three narrow the same result set simultaneously.

### Search

Full-text search across control name, category, description, critical function, and scope title.

### Footer

Displays database metadata (program name, author, organization, contact) and a version history tooltip showing all database revisions.

---

## Files

| File | Description |
| --- | --- |
| `engineered_controls_dashboard.html` | The complete dashboard — one self-contained HTML file |
| `idf_min.json` | DHS Infrastructure Taxonomy (minified) — enables the hierarchy browser |
| `engctrls.json` | The engineered controls database (included in the data directory of this repository) |

---

## How to Use

### 1. Open the dashboard

Download `engineered_controls_dashboard.html` and open it directly in any modern browser. No web server is needed.

Tested in Chrome 120+, Firefox 121+, Edge 120+, Safari 17+.

### 2. Load your files

The upload screen presents two slots:

**Controls Database (required)**
Load your `engctrls_full_...json` file. The dashboard auto-detects the file type by inspecting its structure. Accepts drag-and-drop or click-to-browse.

**IDF Taxonomy (optional but recommended)**
Load `idf_min.json` to unlock the full hierarchy browser with recursive counts. Without it, the dashboard still works — search, filter, table, and analytics all function, but there are no hierarchy cards.

Click **Open Dashboard** once the controls file is loaded.

### 3. Browse the hierarchy

The card browser at the top shows all 18 sectors. Each card displays:

```cmd
Sector Name
1,240          ← total controls recursively beneath this node
840 known / 400 ideas
████░░░░░░     ← known-in-use proportion bar
```

Click a sector card to drill into its subsectors. Click again on an already-selected card to deselect it. Use the breadcrumb bar to navigate back up.

Toggle **Hide hierarchy** to collapse the card rows and give the table/analytics more vertical space — your current selection remains active.

### 4. Filter and search

Use the left sidebar to apply filters. The result count in the toolbar reflects all active filters combined (hierarchy path + sidebar filters + search). Click **Clear all** in the sidebar to reset filters without affecting the hierarchy selection.

### 5. Explore a control in detail

Click any row in the Controls table to open the detail panel on the right side. Press the **x** button or click the overlay to close it.

### 6. Switch to Analytics

Click the **Analytics** tab in the toolbar to see the chart view for the current filtered result set. All charts respond live to hierarchy selection and filter changes.

---

## JSON File Formats

### Controls Database

```json
{
  "programName": "Cyber-Informed Engineering",
  "programTask": "Engineered Controls Database",
  "company": "Idaho National Laboratory",
  "author": "Benjamin Lampe",
  "authorEmail": "benjamin.lampe@inl.gov",
  "version": 2,
  "version_history": [...],
  "data": [
    {
      "id": "...",
      "input_id": 1,
      "scope_level": "Sector",
      "title": "Agriculture and Food",
      "brief_context": "...",
      "critical_functions": [...],
      "engineered_controls": {
        "known_in_use": [
          {
            "critical_function": "...",
            "category": "Fail-safe default",
            "name": "...",
            "how_it_works": "...",
            "resilience_roles": ["Prevent impact", "Control degradation slope"],
            "fail_safe": "Yes",
            "notes": "..."
          }
        ],
        "ideas_opportunities": [
          {
            "critical_function": "...",
            "category": "Redundant physical+digital",
            "concept": "...",
            "rationale": "...",
            "expected_resilience_roles": [...],
            "implementation_notes": "...",
            "priority_hint": "High"
          }
        ]
      }
    }
  ]
}
```

### IDF Taxonomy

```json
[
  {
    "ID": 1,
    "Name": "Agriculture and Food",
    "Scope": "Sector",
    "Level": 1,
    "ParentID": 0,
    "OutlineID": "1",
    "Description": "...",
    "IDTID": 6
  },
  {
    "ID": 2,
    "Name": "Supply",
    "Scope": "Subsector",
    "Level": 2,
    "ParentID": 1,
    ...
  }
]
```

The dashboard links `input_id` values in the controls file to `ID` values in the taxonomy to build the hierarchy and compute recursive counts.

---

## Resilience Roles

The six CIE resilience roles and their meaning:

| Role | Description |
| --- | --- |
| **Prevent impact** | Controls that stop a cyber event from causing physical consequences |
| **Enhance detection/monitoring** | Controls that improve visibility into anomalous conditions |
| **Control degradation slope** | Controls that slow the progression of a failure |
| **Redirect toward recovery** | Controls that shift system state toward a recoverable condition |
| **Accelerate recovery** | Controls that speed restoration of normal operation |
| **Enable adaptation** | Controls that allow the system to operate in a degraded mode |

---

## Technology

The dashboard is a single HTML file with no build step and no backend.

| Library | Version | Purpose |
| --- | --- | --- |
| React | 18.2 | UI rendering |
| Chart.js | 4.4.1 | Bar and donut charts |

Both are loaded from cdnjs CDN links embedded in the file. The dashboard requires an internet connection on first load to fetch these libraries; after that, browsers typically cache them.

---

## About CIE

**Cyber-Informed Engineering (CIE)** is a methodology developed by Idaho National Laboratory that integrates cybersecurity considerations into the engineering design and operation of critical infrastructure systems. Rather than treating cyber threats as purely an IT problem, CIE embeds security thinking into physical system design so that engineered safeguards provide resilience even when digital controls are compromised.

More information: [inl.gov/cie](https://inl.gov/cie)

---

## Contact

**Benjamin Lampe**
Idaho National Laboratory
<benjamin.lampe@inl.gov>
