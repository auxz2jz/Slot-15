# Grocery List Android App — Project Memory

## Repository
- Canonical repository: `auxz2jz/Slot-15`
- Platform: Android
- Project type: Brand-new single-platform project
- Master rules: `auxz2jz/master-instruction-library`
- Required startup: read `INSTRUCTION_INDEX.md` and all mandatory files it references before development.

## Current status
- Status: PLANNED
- Source code: NOT STARTED
- Current version/build: none
- Last user-verified baseline: none
- Latest candidate: none
- Initial recovery point: empty Slot-15 repository before project initialization

## User-defined product intent
Create an Android shopping/grocery-list app with Android widgets. The app must support adding list items from both the main app and widgets.

The list is broader than food groceries and may include household goods, hardware, tools, and other shopping items.

Requested capabilities:
- Add shopping-list items from the app.
- Add shopping-list items from home-screen widgets.
- Categorize items.
- Filter/sort alphabetically.
- Filter/sort by price.
- Filter/group by store.
- Filter/group by product category such as groceries, household goods, hardware, and user-defined categories.
- Allow custom categories.
- Automatically suggest/sort items into appropriate categories.
- Maintain user-defined stores the user shops at.
- Allow an item to have one or more possible stores.
- Example: bread may normally map to Walmart.
- Example: a crescent wrench may map to Home Depot, Lowe's, Tractor Supply, or other configured stores.
- Record product prices.
- Record barcodes/UPCs.
- Build a reusable local product catalog from products the user has entered or scanned.
- Take/store product photos.
- Investigate optional online barcode/product lookup.
- Investigate optional product-name search, e.g. "wheat bread Walmart".
- Investigate optional AI-assisted classification/description where practical, but do not make core app functionality depend on AI availability.

## Data concepts — initial
These are planning concepts, not a frozen schema:
- ShoppingListItem
- Product
- Category
- Store
- ProductStorePreference
- PriceObservation / price history
- Barcode
- ProductPhoto
- AutoClassificationRule
- Widget configuration

A product may belong to one primary category plus optional tags.
A product may be available from multiple stores.
A shopping-list entry may optionally choose a preferred store and expected/current price.

## Current task
Initialize the project safely and define the first implementation slice.

## Implementation plan
1. Establish durable project memory, roadmap, diagnostics, and guided-testing documents.
2. Design the minimum local data model for products, stores, categories, shopping-list entries, prices, barcodes, and photos.
3. Create a minimal Android project without implementing online lookup or AI first.
4. Implement local list add/edit/check-off/delete and persistence.
5. Add store/category management and filtering/sorting.
6. Add widget-based quick-add.
7. Add barcode scanning and local barcode-to-product matching.
8. Add photos.
9. Add optional online lookup providers with graceful fallback.
10. Add optional smart/AI-assisted categorization only when device/service support is available and never as the sole classification mechanism.

## First development step
When coding begins, create the smallest Android/Kotlin baseline that can:
- launch,
- create a local shopping item,
- persist it,
- display it,
- and produce diagnostics proving each operation.

Do not start with online lookup, AI, barcode networking, or complex widgets before the local data foundation is verified.

## Files expected to act as source of truth
- `PROJECT_MEMORY.md` — current status/checkpoint/recovery state
- `GROCERY_LIST_ROADMAP.md` — permanent feature roadmap
- `DIAGNOSTICS.md` — app-specific diagnostic coverage map and implementation status
- `TESTING.md` — app-specific guided-test catalog/status

## Checkpoint — Initial
- Date: 2026-09-27
- Status: PLANNED
- Verified source: none
- Verified artifact: none
- Candidate source: none
- Candidate artifact: none
- Existing working source at risk: none; repository was empty
- Exact next action: create the minimal Android project/data baseline after the user is ready to begin coding.

## Known risks / constraints
- Public product/barcode databases have incomplete coverage, especially non-food products and store-specific products.
- Store pricing changes frequently and many retailers do not provide unrestricted free public product/price APIs.
- Web scraping/search-result parsing is fragile and may violate service terms; avoid making it a core dependency.
- AI feature availability varies by Android device and OS/service support.
- Automatic categorization must always allow manual correction.
- Widget operations must share the same durable data store as the main app.
- Diagnostics must never persist private photos or sensitive data by default.

## Failed approaches
None.

## User-supplied results/files received
None.

## Exact next action
Begin code only from this documented empty-project baseline and follow:
READ → PLAN → RECORD PLAN → CHECKPOINT → MODIFY → BUILD → TEST → ANALYZE → RECORD RESULT → CHECKPOINT → CONTINUE.
