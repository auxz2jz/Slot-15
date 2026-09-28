# Grocery List Android App — Diagnostics

This file implements the project-specific side of the mandatory Master Diagnostics Standard.

Because source code does not yet exist, this is an initial coverage plan. It MUST be reconciled against the actual controls, screens, workflows, background jobs, states, and outputs after each feature is implemented. Do not invent controls merely to match this document.

## Required architecture

Planned central structured logger:
- JSONL chronological event stream
- app/session UUID
- event sequence number
- UTC timestamp
- monotonic time
- correlation ID for important operations
- app version/build
- screen/module/control where applicable
- request, state/progress, result, and error separated
- persistent bounded rolling action trace
- recent-event buffer
- crash preservation
- diagnostic export
- privacy redaction

Important events must be flushed promptly.

## Privacy
Do not log:
- product photo bytes
- secrets/tokens/API keys
- unrestricted typed text unrelated to the shopping operation
- precise location
- private account information

Safe product metadata may be logged only as needed for diagnosis.

## Initial Diagnostic Coverage Map

### Shopping item add
Trigger:
- app add action or widget quick-add action

Record:
- USER_ACTION / WIDGET_TRIGGER
- OPERATION_START: item-add request
- validation state
- database write attempt
- OPERATION_RESULT with generated item ID
- ERROR on failure

PASS:
- item persisted and can be read back.

FAIL:
- validation rejects unexpectedly, database write fails, or read-back does not match safe expected fields.

### Shopping item edit
Record request separately from database result.
PASS only after persisted read-back confirms intended change.

### Mark purchased/unpurchased
Record:
- requested state
- previous state
- resulting persisted state

PASS only if stored state changes correctly.

### Delete/archive
PASS only after the stored record is absent/archived as intended.

### Store/category changes
Record before/after IDs or safe labels.
PASS only after persistence and refresh confirm the assignment.

### Sorting/filtering
Record:
- requested sort/filter mode
- active filters
- input count
- output count
- completion/error

PASS:
- rendered/query result satisfies selected rule according to automated test data where feasible.

### Widget quick add
Record:
- widget instance
- trigger
- request
- storage result
- refresh/update result
- error

A widget tap alone never counts as success.

### Widget list refresh
Record trigger (manual/system/data-change), data query, count, render/update completion or failure.

### Barcode scan
Record:
- scan requested
- scanner ready
- barcode format
- redacted/hashed barcode if diagnostics privacy policy requires it; otherwise safe value only when appropriate
- decode success/failure
- local lookup result
- optional online lookup start/result/error

Scanning a barcode is not proof product lookup succeeded.

### Online lookup
Give each lookup a correlation/operation ID.
Record:
- provider
- request type
- safe query metadata
- HTTP/result class
- parsed result count
- selected/imported result
- timeout/error
- user confirmation

Do not persist API credentials.

### Product photo
Record:
- capture/select request
- permission/readiness
- file save/import result
- safe size/dimensions
- thumbnail generation result
- error

Do not include the actual image in normal diagnostic export unless explicitly designed as an opt-in diagnostic artifact.

### Automatic categorization
Record:
- trigger
- classifier/rule source
- candidate category
- confidence/rule match when applicable
- user override
- persisted final category

### Diagnostic export
Record:
- USER_ACTION
- EXPORT STARTED
- files included
- bytes produced
- completion or diagnostic-export failure

## Stall/watchdog targets
Add where appropriate for:
- online product lookup
- photo processing
- bulk database migration/import
- any future long-running sync

## First-real-failure rule
When a feature fails, diagnostic review must identify the earliest divergence from expected behavior rather than only the visible final symptom.

## Update rule
Every important new feature must update this coverage map and TESTING.md before it can be considered diagnostically complete.
