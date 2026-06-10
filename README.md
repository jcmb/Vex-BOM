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

## Data expectations

Both pages expect CycloneDX JSON files with:

- `bomFormat: "CycloneDX"`
- `vulnerabilities` array

If a file is invalid, the page shows an error and resets results.

