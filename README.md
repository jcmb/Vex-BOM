# Vex-BOM

Simple static HTML tools for viewing and comparing CycloneDX VEX vulnerability data.

## Pages

- `index.html` - single-file VEX viewer
- `compare.html` - two-file VEX comparison viewer

Open either file directly in a browser.

## Single-file viewer (`index.html`)

Use this page to inspect one CycloneDX VEX JSON file.

- Load one VEX file with the file picker.
- Filter by `Severity`, `Analysis`, `Justification`, and `Response`.
- Sort by clicking sortable column headers.

## Compare viewer (`compare.html`)

Use this page to compare two CycloneDX VEX JSON files.

- Load:
  - `Orginal VEX JSON` (baseline side)
  - `Updated VEX JSON` (candidate side)
- Filter change types with checkboxes:
  - `Added`, `Removed`, `Changed`, `Unchanged`
- Additional filters:
  - `Severity`, `Analysis`, `Justification`, `Response`
- Sort by clicking sortable headers.

### Compare row layout

Each vulnerability is displayed across 3 rows:

- Row 1: `Updated` values that differ from original (otherwise blank)
- Row 2: values that are the same in both files (otherwise blank)
- Row 3: `Original` values that differ from updated (otherwise blank)

`Change`, `CVE ID`, and `Description` span all three rows for each vulnerability.

### UI features

- Light/Dark/System theme selector
- Draggable table column resizers
- Horizontal scroll when total column width exceeds viewport

### Follow-up annotations

The compare page supports per-CVE follow-up tracking.

- Add/update annotation data in the `Annotations` column:
  - `Follow-up` toggle
  - `Status` (`open`, `in_progress`, `resolved`, `blocked`)
  - free-text `Comment`
- Annotation state is keyed by CVE ID and remains visible while sorting/filtering.

### Notes JSON import/export

Annotations are persisted with explicit JSON files.

- `Download Notes JSON` exports all annotations currently in memory.
- `Upload Notes JSON` imports and merges notes by CVE ID.
- Invalid entries are ignored with feedback in the UI.

Schema shape:

```json
{
  "format": "vex-compare-notes",
  "version": 1,
  "exportedAt": "2026-06-10T19:40:00.000Z",
  "annotations": {
    "CVE-2024-12345": {
      "status": "in_progress",
      "needsFollowUp": true,
      "comment": "Need vendor confirmation on mitigation timeline.",
      "updatedAt": "2026-06-10T19:38:20.000Z"
    }
  }
}
```

## Data expectations

Both pages expect CycloneDX JSON files with:

- `bomFormat: "CycloneDX"`
- `vulnerabilities` array

If a file is invalid, the page shows an error and resets results.

