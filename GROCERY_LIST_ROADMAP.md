# Grocery List Android App — Roadmap

Status legend: PLANNED / IN PROGRESS / CANDIDATE / VERIFIED / FAILED / BLOCKED / DEFERRED / DONE

## Foundation

### F-001 — Local shopping list
Status: PLANNED
- Add item
- Edit item
- Mark purchased / unpurchased
- Delete/archive item
- Persist across app restarts

### F-002 — Product catalog
Status: PLANNED
- Reusable product records
- Name/brand/description
- Barcode(s)
- Photo(s)
- Category
- Store options
- Last/typical price
- Optional price history

### F-003 — Store management
Status: PLANNED
- Add/edit/remove stores
- Choose preferred stores
- Associate products with one or many stores
- Store-specific price observations

### F-004 — Category management
Status: PLANNED
- Built-in starter categories
- Custom categories
- Manual category correction
- Category rules/keywords
- Automatic category suggestion

Initial examples may include:
- Grocery
- Household
- Hardware
- Personal Care
- Automotive
- Pet
- Pharmacy
- Other

The actual category set remains user-editable.

## List organization

### F-010 — Sorting and filtering
Status: PLANNED
- Alphabetical
- Price
- Store
- Category
- Purchased/unpurchased
- Search

### F-011 — Multi-store planning
Status: PLANNED
- An item can list several possible stores.
- A shopping trip can optionally choose a preferred store.
- The UI should distinguish "available at" from "buy at this store".

### F-012 — Price handling
Status: PLANNED
- Expected/current price
- Store-specific price
- Optional quantity/unit
- Optional price history
- Shopping-list estimated total

## Widgets

### F-020 — Quick Add widget
Status: PLANNED
- Add an item directly from home screen.
- Use the same database as the app.
- Record diagnostics for widget trigger, request, persistence result, and failure.

### F-021 — Shopping List widget
Status: PLANNED
- Show active list items.
- Mark purchased where Android widget capabilities permit.
- Open an item/app for richer editing.

### F-022 — Configurable widget filters
Status: PLANNED
Potential configurations:
- All items
- One store
- One category
- Unpurchased only

## Barcode and product lookup

### F-030 — Barcode scanning
Status: PLANNED
- Decode UPC-A, UPC-E, EAN-8, EAN-13 and relevant formats on-device.
- First match against local product catalog.
- If unknown, optionally query configured online provider(s).
- Never require the internet merely to decode a barcode.

### F-031 — Local barcode memory
Status: PLANNED
When the user identifies an unknown scanned product, save the mapping locally so future scans resolve immediately.

### F-032 — Optional public product lookup
Status: RESEARCHED / PLANNED
Preferred strategy:
1. Local catalog first.
2. Open product database lookup where appropriate.
3. If no structured result, offer a user-visible web search fallback.
4. Let the user confirm/edit imported data before saving.

Do not silently trust online descriptions, categories, prices, or images.

### F-033 — Name-based online search
Status: PLANNED
Example input:
- "wheat bread"
- preferred store: Walmart

The app may form a query such as "wheat bread Walmart" and either:
- use an approved structured provider, or
- launch the user's browser/search app for a normal web search.

Automatic extraction from arbitrary search pages is not a core requirement.

## Photos and recognition

### F-040 — Product photos
Status: PLANNED
- Take photo
- Select existing photo
- Associate multiple photos if later useful
- Use thumbnail in product/list UI where helpful

### F-041 — OCR-assisted product identification
Status: FUTURE
Use on-device text recognition to extract brand/product text from packaging when practical. User confirms result before save.

### F-042 — AI-assisted categorization
Status: FUTURE / OPTIONAL
Possible uses:
- Suggest category from product name/description.
- Suggest likely store types.
- Describe a product photo on supported devices.

Requirements:
- Must be optional.
- Must have deterministic/manual fallback.
- Must check runtime device support.
- Must not block core list functionality.

## Usability

### F-050 — Fast add
Status: PLANNED
A minimal entry path should require only item name. Category/store can be suggested or filled later.

### F-051 — Smart defaults
Status: PLANNED
Learn from the user's own saved mappings, for example:
- product name/keywords → category
- product → preferred store
- barcode → product

User corrections should override automatic suggestions.

### F-052 — Duplicate awareness
Status: FUTURE
Warn when the same/similar item is already active on the list.

## Diagnostics/testing

### F-090 — Built-in diagnostics
Status: REQUIRED
Follow Master Diagnostics Standard for every implemented feature.

### F-091 — Test This Version
Status: REQUIRED
Each candidate must have guided tests based on the features actually present.

## Deferred decisions
- Final app name/branding
- Exact UI layout
- Exact database library/schema
- Whether price history is first-release or later
- Which optional online lookup providers are enabled by default
- Whether voice input is added
- Whether cloud sync is ever added
