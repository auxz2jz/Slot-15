# Grocery List Android App — Guided Testing

This file follows the Master Guided Testing Standard.

Source code does not yet exist, so these are planned test areas. Exact test steps and button labels MUST be updated from the real application UI for each candidate build.

## Test This Version
Every testable candidate should expose a guided "Test This Version" workflow containing:
- exact app version/build
- unique test session ID
- one step at a time
- persistent progress
- automatic evidence
- human confirmation where needed
- Problem / Expected Behavior Failed control
- TXT report
- structured JSON results when practical
- Export Test + Diagnostics

## Planned baseline test catalog

### T-001 — Add and persist an item
User intent:
Add a simple item such as "Bread".

Automatic verification:
- add request recorded
- database write succeeds
- generated record can be queried back
- item appears in list data

Failure examples:
- item missing after restart
- duplicate unintended record
- write/read mismatch

### T-002 — Edit item
Verify the edited value persists and the old value is replaced as intended.

### T-003 — Purchased state
Mark an item purchased and then unpurchased.
Verify persistent state after refresh/restart.

### T-004 — Store assignment
Assign a product/list item to a store and verify filter/group behavior.

### T-005 — Category assignment
Assign built-in and custom categories.
Verify manual category correction persists.

### T-006 — Alphabetical sort
Use controlled test data and verify expected order.

### T-007 — Price sort
Use controlled numeric prices and verify ordering, including missing-price behavior.

### T-008 — Store filter
Use items assigned to multiple stores and verify inclusion/exclusion semantics.

### T-009 — Category filter
Verify only intended category results are returned.

### T-010 — Widget quick add
From the actual widget, add an item.
PASS requires:
- widget request logged
- shared database write succeeds
- item appears in main app/list query

A widget interaction alone is not PASS.

### T-011 — Barcode local match
Scan a barcode already saved in the local catalog.
PASS requires:
- barcode decoded
- correct local product resolved
- no unnecessary online lookup

### T-012 — Unknown barcode fallback
Unknown barcode should reach the intended lookup/manual-identification workflow without crashing or silently inventing product data.

### T-013 — Product photo
Capture/select and save a product photo.
Verify metadata/file reference persists and image can be reopened/rendered.

### T-014 — Automatic category suggestion
Use known controlled examples.
Automatic suggestion may be machine/rule verified, but final UX also requires human confirmation that the suggestion is sensible.
Manual correction must persist.

### T-015 — Diagnostic export
Export diagnostics.
PASS requires a non-empty package with expected manifest/summary/events and no unintended private product-photo content.

## Result sources
Use:
- AUTO_VERIFIED
- AUTO_FAIL
- MANUAL_PASS
- MANUAL_FAIL
- MANUAL_OVERRIDE
- BLOCKED
- SKIPPED
- UNTESTED

## False-positive protection
Examples:
- Tapping Add is not success; persistence/read-back is success.
- A barcode value decoded is not product-lookup success.
- An HTTP 200 is not lookup success unless usable validated product data is parsed.
- A widget refresh request is not success unless the widget update completes.
- A photo capture callback is not success unless the image reference is saved and can be read.

## Candidate requirement
No candidate should be called VERIFIED until the user physically tests it and confirms it works.
