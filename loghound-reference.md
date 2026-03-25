# LogHound — Complete App Reference for LLMs

---

## Instructions for the LLM

This document is the authoritative reference for LogHound, an iOS 18+ app for creating custom tracking logs. Use it to answer any question a user has about how the app works, what features it has, and how to accomplish specific goals.

### When to Surface Screenshots

Show a screenshot proactively whenever it would help a user find something, understand a concept, or orient themselves in the app. Specific triggers:

| User says / asks | Show this screenshot |
|-----------------|---------------------|
| "Where do I find..." or "How do I get to..." | Screenshot of that screen |
| "What does X look like?" | Most relevant screenshot |
| Questions about the home screen, log list | `assets/screenshots/01-log-list.jpg` |
| Questions about entries, card view | `assets/screenshots/02-running-cards.jpg` |
| Questions about table view, columns, sorting | `assets/screenshots/03-running-table.jpg` |
| Questions about summary view, aggregation, pickers | `assets/screenshots/12-summary-sum-week.jpg` and `assets/screenshots/13-summary-avg-week.jpg` |
| Questions about fields, schema, field types | `assets/screenshots/05-running-schema.jpg` |
| Questions about creating or filling in an entry | `assets/screenshots/06-entry-form.jpg` |
| Questions about settings, trial, backup | `assets/screenshots/07-settings.jpg` |
| Questions about alerts, how to set a reminder | `assets/screenshots/08-entry-form-alert-set.jpg` then `assets/screenshots/10-alert-config-repeat.jpg` |
| Questions about viewing all alerts | `assets/screenshots/11-alerts-list.jpg` |
| Confusion about Sum vs Average in summary | Show both `assets/screenshots/12-summary-sum-week.jpg` and `assets/screenshots/13-summary-avg-week.jpg` side by side |

### Screenshot Reference Table

| Path | Shows |
|------|-------|
| `assets/screenshots/01-log-list.jpg` | Log list home screen — 4 logs, entry counts, search bar, gear/bell icons, +/Archive/Trash toolbar |
| `assets/screenshots/02-running-cards.jpg` | Card view — running entry with distance, route, emoji rating, weather, notes fields |
| `assets/screenshots/03-running-table.jpg` | Table view — sortable timestamp/distance/duration columns, 10 rows |
| `assets/screenshots/04-calories-summary.jpg` | Summary view — simple single-field (Calories) daily totals example |
| `assets/screenshots/05-running-schema.jpg` | Schema editor — 6 fields: Distance (Number), Duration (Number), Route (Single Select), How I Felt (Rating), Weather (Single Select), Notes (Text) |
| `assets/screenshots/06-entry-form.jpg` | Entry form mid-fill — timestamp, numbers entered, Downtown route selected, star rating set, Weather field visible below |
| `assets/screenshots/07-settings.jpg` | Settings screen — Trial status, Return to last log, Week starts on, Numeric precision, Backup/Restore buttons |
| `assets/screenshots/08-entry-form-alert-set.jpg` | Entry form — Date/Time field ("Next Recital") with red bell icon and "Edit alerts" link indicating an active alert |
| `assets/screenshots/09-alert-config-1.jpg` | Alert config sheet — Enable Alert toggle ON, Number of Alerts picker showing 1 selected, Preview with one scheduled time |
| `assets/screenshots/10-alert-config-repeat.jpg` | Alert config sheet — 2 alerts selected, Repeating section with Minutes/Hours/Days picker, "Every 1 day" set, Preview showing 2 scheduled times labeled "(1 of 2)" and "(2 of 2)" |
| `assets/screenshots/11-alerts-list.jpg` | Active Alerts screen — time filter tabs (All/1dy/1wk/1mo/1yr), alert card showing log name with navigation arrow, field name with red bell, scheduled date/time, countdown, and full entry context |
| `assets/screenshots/12-summary-sum-week.jpg` | Summary — Running log, Week interval, Sum statistic: shows weekly totals (e.g. 15.2 miles, 134 min) across 4 weeks |
| `assets/screenshots/13-summary-avg-week.jpg` | Summary — Running log, Week interval, Average statistic: same data shows per-run averages (5.1 miles, 44.7 min) — identical entries, different insight |

**Version date:** March 2026

---

## What Is LogHound?

LogHound is an iOS 18+ app for creating fully custom tracking logs. Unlike apps with fixed templates (symptom trackers, habit apps, food diaries), LogHound lets the user define their own schema: they choose the fields, the field types, and the field names. Once a schema exists, they record entries against it and view their data three ways: as scrollable cards, as a sortable table, or as an aggregated summary.

Everything is stored on-device using Apple's SwiftData framework. There is no cloud sync, no account creation, no internet connection required at any point, and no data ever leaves the device.

LogHound includes a 30-day free trial. After the trial, a one-time purchase unlocks the app permanently — there is no subscription.

---

## Core Concepts (Read First)

Before answering specific questions, understand these concepts — they explain the "why" behind many user questions:

**Log**: A named container with a defined schema (set of fields) and a collection of entries. Analogous to a spreadsheet file.

**Schema / Fields**: The structure of a log — which fields it has and what type they are. Defined once in the schema editor, but editable at any time. Changing the schema affects future entries; existing data is retained (with caveats for field deletion).

**Entry**: A single record in a log. Has a timestamp and a value for each field in the schema. Analogous to a row in a spreadsheet.

**Field Type**: Determines what kind of data a field stores and how it's displayed and edited. Once set, the type cannot be changed — the field must be deleted and recreated.

**Views**: Three ways to look at a log's entries — Cards (individual records), Table (spreadsheet-style grid), Summary (aggregated statistics over time).

**Aggregatable fields**: Number, Star Rating, and Toggle — these are the only types that can be summarized in the Summary view. All other field types are excluded from aggregation.

---

## First Launch Experience

On first launch the app shows a welcome screen with a text field and two options:
- Enter a log name and tap **Create Log** — creates the log and immediately opens the schema editor
- Tap **Skip for now** — goes directly to the log list

Regardless of which option is chosen, four **sample logs** are automatically created with realistic sample data to demonstrate the app's capabilities:
- **Example: Miscellaneous Notes** — simple single-field text log
- **Example: Running** — rich log with 6 fields across 4 types (Number, Single Select, Star Rating, Text)
- **Example: Piano Practice** — demonstrates Multi Select and mood tracking
- **Example: Calories** — minimal two-field log

Sample logs can be explored, edited, or deleted just like any user-created log. They are labeled "Example: ..." to distinguish them.

---

## Log List (Home Screen)

> 📸 `assets/screenshots/01-log-list.jpg`

The log list is the main screen users return to when navigating between logs or starting the app.

### What's on Screen

**Navigation title**: "Active Logs"

**Search bar** (top): Labeled "Search entries." Searches across all active logs simultaneously — both log names and entry field content. Uses fuzzy matching, so slight misspellings still find results.

**Log rows**: Each row shows:
- A document icon (left)
- Log name (bold)
- Entry count and time since last entry (e.g., "10 entries · 4 days")
- A "..." button (right side) for actions

**Gear icon** (top-left): Opens Settings

**Bell icon** (top-right): Opens Active Alerts. Shows a red badge with the count of upcoming alerts when any exist.

**+ button** (top-right): Creates a new log

**Bottom toolbar**:
- Left: Archive button (box with arrow) — opens the Archive view
- Right: Trash button — opens the Trash view

### Accessing Log Actions

Tap the **"..."** button on a log row, OR long-press the row itself. Both open the same action menu:
- Rename
- Duplicate
- Backup (exports .loghound file for this log)
- CSV Export
- Archive
- Delete

Tapping the log row itself (not the "..." button) navigates into the log detail view.

### Reordering Logs

Drag any log row up or down to reorder. The drag handle is the entire row area. Order is persisted immediately.

### Search Behavior

The search bar searches all active logs at once. Results appear as a list showing:
- Which log the entry belongs to
- The entry's timestamp
- The matching field value(s), with matched text highlighted

Tapping a search result navigates to that log and scrolls to that entry in card view.

Search does not search archived or trashed logs.

---

## Creating and Managing Logs

### Creating a New Log

Tap **+** (top-right of log list) → enter a name → tap **Save**.

The schema editor opens immediately so the user can add fields. The log exists even before any fields are added — it just won't have useful data until fields are defined.

**Name rules**: Must be unique among active logs. Maximum length is not explicitly limited but very long names will be truncated in the UI.

### Renaming a Log

"..." menu → **Rename** → edit the name → confirm.

Will reject the new name if it duplicates another active log's name. The name does not need to be unique across archived or trashed logs.

### Duplicating a Log

"..." menu → **Duplicate** → choose a new name → set options → tap **Duplicate**.

Options:
- **New name**: Pre-filled with "Copy of [original]". Must be unique.
- **Include all entries** toggle (default: ON): If on, all entries from the original are copied into the new log. If off, only the schema is copied — the new log starts empty.

After duplicating, the new log opens in the schema editor so the user can make adjustments.

**Use case**: Great for creating a log with the same structure but starting fresh (e.g., a new month's log with the same fields as last month).

### Copy Fields to New Log

Available from the log detail "..." menu (not the log list). Creates a brand new log with identical fields but no entries. Opens the schema editor for the new log. Useful when the user wants a similar structure but wants to customize it first.

**Difference from Duplicate**: Duplicate always uses the existing schema as-is and optionally copies entries. Copy Fields always starts with no entries and opens the schema editor for customization.

### Archiving a Log

"..." menu → **Archive**.

The log disappears from the active log list and moves to the Archive. All data is fully preserved. Archived logs do not appear in search results.

To access archived logs: tap the **Archive button** (bottom-left toolbar) on the log list.

To restore: open the Archive → tap the log → tap **Restore**. If the name conflicts with an existing active log, a **Name Conflict sheet** appears asking the user to choose a new name.

**Archive vs Delete**: Archive is for logs you're done with but want to keep. Delete (trash) is for logs you no longer need, with a 30-day safety window before permanent deletion.

### Deleting a Log (Sending to Trash)

"..." menu → **Delete**.

The log moves to Trash. It remains there for **30 days** before being automatically and permanently deleted.

To access trashed logs: tap the **Trash button** (bottom-right toolbar).

The Trash view shows each log with a countdown ("28 days remaining"). From here the user can:
- **Restore**: moves back to active logs (with name conflict handling)
- **Delete Permanently**: immediate permanent deletion with confirmation
- **Empty Trash** (button at top): permanently deletes all trashed logs at once

### Delete All Entries

From the log detail "..." menu → **Delete All Entries**. Permanently deletes every entry in the log but leaves the log itself and its schema intact. Requires confirmation showing the exact entry count. This cannot be undone.

**Use case**: Starting fresh with a new period of tracking while keeping the same schema.

### What Happens to Alerts When a Log is Deleted/Archived?

Alerts associated with entries in a deleted or archived log are cancelled. They will no longer appear in the Active Alerts view and iOS notifications will not fire.

---

## Schema Editor

> 📸 `assets/screenshots/05-running-schema.jpg`

The schema editor defines what fields a log has. Access it via:
- "..." menu in the log detail view → **Edit Fields**
- Automatically opened after creating or duplicating a log

### What's on Screen

- **Title**: "Logging Setup" with a subtitle "What You're Tracking"
- List of existing fields, each showing:
  - A type icon (left)
  - Field name
  - Field type label (e.g., "Single Select", "Number")
  - A red circle minus button (left, to delete)
  - A drag handle (right, to reorder)
- **"+ Add Field"** button at the bottom
- **Eye icon** (top-right): opens a live preview of how the entry form will look

### Reordering Fields

Drag fields using the handle on the right side. The order determines:
- The order fields appear in the entry form
- The order of columns in Table view (timestamp is always first)

### Deleting a Field

Tap the red minus button on the left of a field row, or swipe left on the field.

A confirmation dialog shows:
- How many existing entries have data in this field
- A warning that this data will be permanently lost

**This cannot be undone.** Field deletion destroys all data stored in that field across all entries in the log.

### Editing a Field

Tap anywhere on a field row (not the minus or drag handle) to open the field configuration editor.

### Cannot Change Field Type

Once a field is created with a specific type, the type cannot be changed. The user must delete the field and add a new one with the desired type. They will lose any data stored in the old field.

### Schema Preview

The eye icon (top-right) opens a **FormPreviewView** that shows exactly how the entry form will look with the current fields. This is useful for checking layout and order before committing.

### "Done" Button

Tap Done (top-right) to close the schema editor and return to the log detail view.

---

## Field Types — Complete Reference

### 1. Text

**What it stores**: Any string of characters. Supports emoji, line breaks, and special characters.

**Entry form**: Standard iOS text input. Keyboard appears when focused. A "dismiss keyboard" (×) button appears in the keyboard toolbar.

**Empty vs filled**: An empty string (nothing typed) and whitespace-only entries are treated as empty/unfilled.

**Configuration options**:
- Max length (optional) — if set, the input rejects characters beyond this limit

**Display in views**:
- Cards: shown as text, wraps to multiple lines if long
- Table: shown truncated to fit column width; tap row to see full value
- Summary: Text fields do not appear in Summary view

**When to use**: Notes, descriptions, labels, freeform observations, anything that doesn't fit a structured type.

---

### 2. Number

**What it stores**: A numeric value. Can be integer or decimal depending on configuration.

**Entry form**: Numeric keyboard. The user types a number. Min/max validation is shown inline — if the value is out of range, a warning appears and the Save button may be disabled.

**Zero is valid**: A value of 0 is considered filled, not empty. A required Number field is satisfied by entering 0.

**Negative values**: Allowed unless a minimum value prevents it.

**Configuration options**:
- **Allow decimals** (toggle) — if OFF, only whole numbers are accepted; if ON, decimal values like 5.2 or 3.14 are accepted. Affects keyboard type.
- **Minimum value** (optional) — input is rejected if below this
- **Maximum value** (optional) — input is rejected if above this

**Display in views**:
- Cards: shown as-is
- Table: shown with the number of decimal places set in Settings (Numeric Precision, 0–10). This is purely display — stored precision is unaffected.
- Summary: appears as a column; participates in Sum, Average, Count

**When to use**: Distances, durations, weights, measurements, counts, calories, anything quantitative.

---

### 3. Toggle

**What it stores**: A boolean yes/no value.

**Entry form**: A switch labeled "Yes" / "No". Defaults to **No (false)** in new entries.

**Always filled**: Unlike other field types, a Toggle always has a value (either yes or no). It cannot be empty. Because of this, **Toggle fields cannot be set as Required** — the setting has no effect since the field is inherently always filled.

**Clonable behavior**: If marked Clonable, the value (Yes or No) is copied when duplicating an entry.

**Display in views**:
- Cards: shown as "Yes" or "No"
- Table: shown as "Yes" or "No"
- Summary: Toggle contributes 1 (Yes) or 0 (No) to Sum and Average calculations. With Sum + Day, you get a daily count of how many Yes entries there were. With Average + Week, you get a weekly compliance rate (e.g., 0.71 = completed the habit 5 out of 7 days).

**When to use**: Habit tracking (did I do X today?), yes/no attributes (took medication, completed warmup, paid bill).

---

### 4. Single Select

**What it stores**: One selected option from a predefined list.

**Entry form**: A scrollable list of options. Selecting one deselects any previous selection. Can be left empty (no option selected).

**Option management**: Options are defined in the field configuration. Each option can be:
- **Active**: appears in the picker for new entries
- **Deprecated**: hidden from the picker when creating or editing entries, but preserved in existing entries that used it. Deprecated options still display correctly in card/table views for old data.

To deprecate an option: edit the field in the schema editor → long-press the option → choose Deprecate (or there may be a toggle depending on version).

**Configuration options**:
- Options list: add, rename, reorder, delete, or deprecate options

**Display in views**:
- Cards: shown as the option text
- Table: shown as the option text
- Summary: Single Select does not appear in Summary view

**When to use**: Category, route, location, status, type — anything with a fixed set of mutually exclusive choices.

**Single Select vs Multi Select**: Use Single Select when exactly one option applies. Use Multi Select when multiple options can apply simultaneously (e.g., symptoms present, focus areas in a practice session).

---

### 5. Multi Select

**What it stores**: Zero or more selected options from a predefined list.

**Entry form**: A list of checkboxes. Multiple can be checked. A count of selected options is shown. Can be left empty (no options checked).

**Option management**: Same as Single Select — options can be added, renamed, reordered, deleted, or deprecated. Deprecated options are hidden from new entries but preserved in existing ones.

**Display in views**:
- Cards: shown as a comma-separated list of selected options
- Table: shown as a comma-separated list (may truncate in narrow columns)
- Summary: Multi Select does not appear in Summary view

**When to use**: Tags, multiple applicable categories, symptoms (multiple can be present at once), focus areas, ingredients, skills practiced.

---

### 6. Date/Time

**What it stores**: A date, a time, or both, depending on the picker mode configuration.

**Entry form**: Shows pickers for date and/or time based on the configured mode. Always displays:
- The selected date/time value
- A **relative time indicator** alongside the value (e.g., "2 hours ago", "in 3 days", "yesterday", "in 4 wk 5 days")
- A **Clear** button — removes the value entirely (field becomes empty; any active alert is also removed)
- A **Now** button — instantly sets the field to the current date and time
- An **"Edit alerts"** link (or bell icon) — visible when a date is set; opens the alert configuration sheet

**Configuration options**:
- **Picker mode**: Date only, Time only, or Date & Time
- **Default time offset**: if set, when creating a new entry this field auto-populates to (entry timestamp) + (offset). E.g., an offset of +1 hour means the field defaults to 1 hour after the entry was created. Useful for "next scheduled time" patterns.

**When a date is set and an alert is active**: The field shows a **red bell icon** next to the field label and an "Edit alerts" link.

**Display in views**:
- Cards: shown as formatted date/time or relative time
- Table: shown as formatted date/time
- Summary: Date/Time fields do not appear in Summary view (cannot be meaningfully aggregated)

**When to use**: Appointments, due dates, scheduled times, "next recital", event logging with precise times, dose times, medication scheduling.

---

### 7. Star Rating

**What it stores**: A numeric rating from 1 to the configured maximum (1–5).

**Entry form**: Tappable emoji icons arranged horizontally. Tapping a position sets the rating. The selected emoji is repeated to visually represent the value (e.g., 💪💪💪 for a rating of 3).

**Can be empty**: No star tapped = empty/unfilled.

**Configuration options**:
- **Maximum stars**: 1 to 5 (default 5)
- **Emoji**: any single emoji, shown as the rating symbol. Examples: ⭐, 💪, 🎵, 😊, 🔥. Default: ⭐

**Display in views**:
- Cards: repeated emoji (e.g., 🎵🎵🎵🎵 for 4)
- Table: numeric value (e.g., 4)
- Summary: participates in Sum, Average, Count — appears as a numeric column

**When to use**: Quality, effort, mood, satisfaction, perceived difficulty — anything where a nuanced rating is more expressive than a raw number.

---

### 8. Location

**What it stores**: GPS coordinates — latitude and longitude, and optionally altitude and accuracy values.

**Entry form**: A **"Capture Current Location"** button. When tapped:
- The app requests iOS location permission if not already granted
- On success: displays the coordinates to 6 decimal places
- On failure or denied permission: shows an error

**Configuration options**:
- **Include altitude**: stores the device's altitude in meters
- **Include horizontal accuracy**: stores the accuracy radius of the lat/lon in meters
- **Include vertical accuracy**: stores the accuracy of the altitude reading

**Display in views**:
- Cards: shown as "lat, lon" to 6 decimals, with altitude if configured
- Table: shown as coordinates
- Summary: Location fields do not appear in Summary view

**Cannot manually type coordinates**: There is no text input — location can only be captured by tapping the button (which reads live GPS).

**When to use**: Recording where something happened (a sighting, a run starting point, a maintenance site), location-tagged observations.

---

## Field Configuration Reference

Every field type shares these configuration options:

### Name
Any text, including emoji. An **emoji picker** is available inline when editing the name. The emoji appears as a leading icon in the entry form, cards, and table columns.

### Required
When enabled, the **Save button** in the entry form is disabled until this field has a value. The field label shows a red asterisk (*).

Notes:
- Toggle fields cannot be Required (they always have a value)
- For Number fields: 0 counts as a valid value and satisfies Required
- For Date/Time fields: a date must be set (Clear removes the value and makes the field empty again)
- For Star Rating: at least one star must be tapped

### Clonable
When enabled, this field's value is **automatically copied** from the source entry when duplicating.

When disabled, the field starts **empty** in the duplicate, requiring the user to fill it in.

**Choosing clonable vs not**:
- Make fields Clonable when the value often stays the same across duplicate entries (e.g., route for a regular commute run, medication name for daily logging)
- Make fields non-Clonable when the value is always different (e.g., how I felt today, specific notes, weight measurement)

### Default Value
A value pre-filled when creating a **new** entry (not when duplicating — duplicates use Clonable logic instead). Default behavior varies by field type. For Date/Time, the "default time offset" serves as the default value mechanism.

---

## Recording Entries

> 📸 `assets/screenshots/06-entry-form.jpg`

### Creating a New Entry

Tap the blue **+** floating action button (bottom-right corner of the log detail view). Opens the entry form in "New Entry" mode.

**Timestamp**: At the top, automatically set to the current date and time. Tap **Edit** to open a date/time picker. Changing the timestamp is useful for logging something that happened earlier (e.g., "I should have logged this run yesterday").

**Fields**: One section per field, in schema order. Fill in as many as needed.

**Save**: Tap **Save** (top-right). If required fields are empty, Save is greyed out with an indicator on the unfilled required field.

**Cancel**: Tap **Cancel** (top-left) to dismiss without saving. Values entered so far are saved as a **draft** (see below).

### Drafts

If the user starts filling an entry form and dismisses it without saving, the in-progress values are automatically saved as a draft. The next time a new entry form is opened for the same log, the draft is restored.

- Drafts survive app backgrounding and device restarts
- A draft is cleared when the entry is saved or when the user explicitly discards it
- Only one draft per log exists at a time
- Drafts are per-log — the draft for Running is separate from the draft for Piano Practice

If a user reports seeing a form pre-filled with old data, it's because a draft was saved from a previous session.

### Editing an Entry

**From card view**: Tap anywhere on the entry card to open the entry detail view, then tap **Edit**. Or tap the edit (pencil) icon directly on the card if visible.

**From table view**: Tap a row to open the entry detail view, then tap Edit. Or right-click/long-press a row and choose Edit.

The edit form is identical to the creation form, plus a red **Delete Entry** button at the very bottom.

### Duplicating an Entry

Tap the duplicate/copy icon on a card (the overlapping pages icon), or from the entry detail view tap **Duplicate**. From table view: right-click → Duplicate.

Opens a new entry form with values pre-filled according to each field's **Clonable** setting:
- Clonable = YES → value is copied from the source entry
- Clonable = NO → field starts empty

The **timestamp** is set to the current time (not copied from the source entry). The user can edit the timestamp before saving.

### Deleting an Entry

- Card view: tap the trash icon on the card (if visible in the card's action buttons)
- Edit mode: scroll to the bottom of the form → tap the red **Delete Entry** button
- Table view: right-click/long-press a row → Delete
- Entry detail view: open the Edit form → Delete Entry button

Deletion is **immediate and permanent** — there is no undo and no trash for individual entries (only for entire logs).

### Keyboard Handling

A **dismiss keyboard** button (×) appears in the toolbar above the keyboard when any text input is focused. Tapping it hides the keyboard without moving focus or losing the current input.

---

## Viewing Data

> 📸 `assets/screenshots/02-running-cards.jpg` — Card view.
> 📸 `assets/screenshots/03-running-table.jpg` — Table view.

The three view modes (Summary / Table / Cards) are switched using the segmented control at the top of the log detail view. The **last used view mode** is remembered per log.

All three views share:
- The same **Fields selection** for that log (which fields are shown)
- The same **Filter state** for that log

### Card View

> 📸 `assets/screenshots/02-running-cards.jpg`

Entries displayed as vertical scrolling cards, **newest entry first**.

Each card shows:
- Date in bold (e.g., "Sat, Mar 21, 2026")
- Time (e.g., "6:45 AM")
- Relative time (e.g., "4 days 2 hr ago") — top-right
- A **copy/duplicate icon** (overlapping pages) — top-right
- All field values, each with its field name as a label above the value

**Fields button** ("≡ Fields (all)" or "≡ Fields (N selected)"): Opens a sheet listing all fields with checkboxes. Toggle to show or hide individual fields on all cards. Useful when the log has many fields but only some are interesting to see at a glance.

**Filter button** ("≡ No Filters" or "≡ Filters Active"): Opens the filter configuration sheet.

**Scrolling**: Standard vertical scroll. All entries are loaded and rendered.

### Table View

> 📸 `assets/screenshots/03-running-table.jpg`

Entries as rows. Columns for timestamp (always first) and each field in schema order.

**Column header**: Shows field name. Tap to sort ascending; tap again to sort descending. An arrow indicates sort direction. Default sort is by timestamp descending (newest first).

**Column resizing**: Drag the divider between column headers left or right to resize.

**Horizontal scroll**: If there are more columns than fit on screen, the table scrolls horizontally. The timestamp column may be pinned.

**Tap a row**: Opens the entry in a detail modal showing all values. The detail modal has Edit and Duplicate buttons.

**Right-click / long-press a row**: Shows a context menu with Edit, Duplicate, Delete.

**Numeric precision**: The decimal places shown for Number fields is set in Settings → Numeric Precision (0–10). This is display-only.

**Fields button**: Same as card view — toggles which columns are shown.

**Filter button**: Same filter state as card view.

### Summary View

> 📸 `assets/screenshots/12-summary-sum-week.jpg`
> 📸 `assets/screenshots/13-summary-avg-week.jpg`

Aggregates the log's numeric data over time intervals.

**Which fields appear**: Only **Number**, **Star Rating**, and **Toggle** fields. Text, Single Select, Multi Select, Date/Time, and Location are excluded. If the log has no aggregatable fields, a message says so and the view is empty.

**Two pickers at top**:

**Interval picker** (Day / Week / Month / Year):
- Groups entries into time buckets
- The Date column shows the start of each bucket: "2026-03-15" means the week of March 15
- "Week" respects the **Week starts on** setting (Sunday or Monday) from Settings
- Buckets with no entries are not shown — the table only shows intervals that have at least one entry

**Statistic picker** (Sum / Average / Count):
- **Sum**: adds all values in each bucket. Example: total miles run in a week = 15.2
- **Average**: divides the sum by the number of entries. Example: average miles per run in a week = 5.1 (if 3 runs)
- **Count**: counts entries regardless of field values. Shows how many times the user logged something in each interval. For Toggle fields, Count tells you how many entries existed; Sum tells you how many were "Yes."

**Toggle fields in summary**:
- **Sum**: number of "Yes" entries in the interval (e.g., 5 out of 7 days I did the habit)
- **Average**: proportion of "Yes" entries (e.g., 0.71 = 71% compliance)
- **Count**: total number of entries in the interval (regardless of Yes/No)

**"Summarizing X of Y entries"**: Shown above the table. If a filter is active, X < Y tells the user how many entries are excluded.

**Column sorting**: Tap any column header to sort by that value.

**Fields button**: Toggle which aggregatable fields appear as columns.

**Week start day**: Configured in Settings → Week starts on (Sunday or Monday).

---

## Search and Filters

### Global Search

The search bar at the top of the log list (placeholder: "Search entries") searches:
- All active log names
- All entry field values across all active logs
- Entry timestamps (formatted text)

Uses **fuzzy matching** — partial matches and slight misspellings are found.

Results appear as a list. Each result shows:
- The log the entry belongs to
- The entry timestamp
- The matching field content with highlighting

Tapping a result navigates to that log in card view and highlights the matching entry.

Search does **not** search archived or trashed logs.

Clearing the search field (tap × in search bar) returns to the full log list.

### Per-Log Filters

Each log has its own filter configuration that is **independent from other logs** and **persists between sessions**. A filter set on Tuesday is still active on Thursday.

#### Accessing Filters

Tap the **"≡ No Filters"** or **"≡ Filters Active"** button in card, table, or summary view. Both show the same filter sheet for that log.

#### Filter Sheet Layout

- A master **enable/disable toggle** at the top: turns all filters on or off without clearing the configured conditions. Useful for quickly comparing filtered vs. full data.
- Expandable **cards** — one for Timestamp, one for each field in schema order
- Each card header shows the field name and, when collapsed, a summary of any active filter condition (e.g., "= Trail" or "between Mar 1 – Mar 31")
- A **×** button on each card deletes that field's filter
- **"Clear All"** button removes all filter conditions
- When filters are active: the view shows "**X of Y entries**" to indicate how many entries pass the filter

#### Filter Operators by Field Type

**Number and Star Rating:**
- equals (=)
- not equals (≠)
- greater than (>)
- less than (<)
- greater than or equal (≥)
- less than or equal (≤)
- between (min and max, inclusive)
- is set (has any value)
- is not set (empty/unfilled)

**Text:**
- equals
- not equals
- contains
- starts with
- ends with
- is empty
- is not empty

**Toggle:**
- is on (Yes/true)
- is off (No/false)
- is set (always true — Toggle is always set)
- is not set (never true — Toggle is always set)

**Single Select:**
- is [option]
- is not [option]
- is set (has a selection)
- is not set (no selection made)

**Multi Select:**
- includes any of [options]
- includes all of [options]
- excludes [option]
- is set (at least one option checked)
- is not set (no options checked)

**Date/Time:**
- before [date]
- after [date]
- between [date] and [date]
- is set (a date has been entered)
- is not set (no date entered)

**Location:**
- is set (coordinates were captured)
- is not set (no location captured)

**Timestamp** (built-in, always available):
- before [date]
- after [date]
- between [date] and [date]

---

## Alerts and Notifications

> 📸 `assets/screenshots/08-entry-form-alert-set.jpg` — Where alerts are configured in the entry form.
> 📸 `assets/screenshots/09-alert-config-1.jpg` — Alert config with 1 alert.
> 📸 `assets/screenshots/10-alert-config-repeat.jpg` — Alert config with 2 alerts and repeat interval.
> 📸 `assets/screenshots/11-alerts-list.jpg` — Active Alerts list.

### Fundamental Concept

An alert fires an iOS notification at the exact date and time stored in a **Date/Time field** in a specific entry. Alerts are configured per-entry — each entry independently decides whether its Date/Time field should trigger an alert and how many.

The same "Next Appointment" field in Entry A and Entry B can have completely different alert settings (or none at all).

### Requirements

1. The log must have at least one **Date/Time** field in its schema
2. That field must be set to a **future** date and time (past dates cannot trigger alerts)
3. iOS **notification permission** must be granted. The app prompts on first alert save. If denied, the user must go to iOS Settings → LogHound → Notifications to enable.

### Setting Up an Alert

**Step 1**: Ensure the log has a Date/Time field. If not, open the schema editor ("..." → Edit Fields) and add one. Recommended picker mode: "Date & Time" for precise scheduling.

**Step 2**: Create or edit an entry. Set the Date/Time field to a future date and time.

**Step 3**: Tap **"Edit alerts"** (appears next to the Date/Time field when a date is entered) or the bell icon.

**Step 4**: In the alert configuration sheet:
- Toggle **Enable Alert** ON
- Choose **Number of Alerts**: 1, 2, 3, or 4 using the segmented picker
- If 2 or more alerts: a **Repeating** section appears with:
  - A picker: Minutes / Hours / Days
  - A number: Every [N] [unit]
  - Alert 1 fires at the stored date/time; Alert 2 fires at that time + 1 interval; Alert 3 at +2 intervals; Alert 4 at +3 intervals
- Check the **Preview** section: it lists every scheduled notification time, labeled "(1 of 2)", "(2 of 2)", etc. Verify these are correct before saving.
- Tap **Save**

**Step 5**: The entry form now shows the Date/Time field with a **red bell icon** next to the label and a countdown ("Next Recital in 4 wk 5 days"), confirming the alert is active.

### Alert Configuration Details

**Number of alerts**: 1–4. If 1, no repeat interval is needed. If >1, the repeat interval determines the gap between successive alerts.

**Repeat interval ranges**:
- Minutes: 1 to 59
- Hours: 1 to 23
- Days: 1 (exactly one day between alerts)

**Interval example**: Date = April 28 at 9:57 AM, 2 alerts, every 1 day → Alert 1 fires April 28 at 9:57 AM, Alert 2 fires April 29 at 9:57 AM.

**Preview**: Always check this before saving. It shows the exact times all alerts will fire.

### Disabling an Alert

Open the alert config (tap "Edit alerts" on the entry form) → toggle **Enable Alert** OFF → Save. The red bell icon disappears.

Alternatively, tapping **Clear** on the Date/Time field removes the date entirely, which also removes the alert.

### Alert Behavior

- Alerts fire as iOS notifications even when the app is closed
- Tapping the notification opens LogHound and navigates directly to the relevant entry
- Alerts are scheduled locally — no internet connection required
- If the app is reinstalled, alerts may need to be re-saved to reschedule them

### Editing an Entry After Setting an Alert

If the user edits an entry and changes the Date/Time value, the alert is **not automatically updated**. The alert still fires at the originally scheduled time. To update the alert, the user must re-open the alert config ("Edit alerts") and tap Save again — this reschedules the alert based on the new date.

### Active Alerts View

> 📸 `assets/screenshots/11-alerts-list.jpg`

From the log list, tap the **bell icon** (shows a red badge with the count of pending alerts).

Shows all upcoming alerts across all logs.

**Time filter tabs**: All, 1dy (next 24 hours), 1wk (next 7 days), 1mo (next month), 1yr (next year).

**Each alert card shows**:
- Log name with a **→ arrow** (tap to navigate to that log and entry)
- Field name with red bell icon and relative countdown ("in 4 wk 5 days")
- The exact scheduled date and time
- All field values of that entry below (for context — the full entry is visible in the card)

Alerts are sorted **earliest first** within each time filter.

---

## Exporting and Backup

### CSV Export

Available from:
- Log list → "..." button on a log → **CSV Export**
- Log detail view → "..." menu → **CSV Export**
- Both open the same flow

**Output format**:
- First row: headers — "timestamp" followed by each field name in schema order
- Subsequent rows: one per entry, sorted by timestamp (newest first)
- Timestamp format: ISO 8601 or a readable date/time string
- **Text**: value as-is
- **Number**: numeric value, decimal places as stored
- **Toggle**: "true" or "false"
- **Single Select**: the option text, or empty if not set
- **Multi Select**: comma-separated list of selected option texts, or empty
- **Date/Time**: formatted date/time or empty
- **Star Rating**: numeric value (e.g., 3), or empty
- **Location**: "latitude, longitude" or extended format if altitude/accuracy included, or empty

**Share Sheet**: After generating, the iOS Share Sheet opens. Available destinations: AirDrop, email, Files app, iCloud Drive, third-party apps that accept files.

**Disabled when**: The log has no entries (no data to export).

### .loghound Backup

**What it is**: A proprietary file format that packages one or more complete logs — schema, all entries, all configurations — into a single portable file.

**How to create**:
1. Settings → tap **Backup Logs**
2. A list of all active logs appears with checkboxes
3. Select desired logs (individual checkboxes or **Select All**)
4. Tap **Backup**
5. Share Sheet opens

**What's included in the file**:
- Complete field schema for each selected log
- Every entry with all field values
- All field configurations (options lists, deprecated options, etc.)
- Log metadata (name, sort order)

**Archived and trashed logs**: Are not available in the backup selection — only active logs are shown.

### Restoring from a .loghound File

**How to restore**:
1. Settings → tap **Restore Logs**, OR
2. Tap a .loghound file from Files app / email attachment → LogHound opens and handles the import

**Confirmation**: A sheet shows "Restore X log(s) from this file?" with the list of log names. The user taps Restore to proceed.

**Name conflict resolution**: If a log in the backup has the same name as an existing active log, the imported log is automatically renamed: "My Log" → "My Log (1)". If "My Log (1)" also exists, it becomes "My Log (2)", and so on. A success message lists all renames.

**Result**: Restored logs are **added** to the active log list alongside existing logs. No existing logs are overwritten or deleted.

**Archived/trashed logs**: If a user's active log list includes archived logs they want to restore from backup — they should restore from backup and the imported log will be active. The archived version remains in Archive separately.

---

## Settings

> 📸 `assets/screenshots/07-settings.jpg`

Accessed via the **gear icon** on the log list. Opens as a modal sheet with a "Done" button to close.

### License Section

**Status**: Shows "Trial: X days remaining" or "Purchased". This is purely informational.

### Navigation Section

**Return to last log**: When the app is re-opened (from background or after being closed), if the user was last using a specific log within the selected time window, the app automatically navigates back to that log rather than showing the log list.

Options: 5 minutes, 15 minutes, 1 hour, 48 hours (labeled "1 day"), Never.

Example: Set to "1 hour" → user opens LogHound, uses Running log, puts phone down, reopens LogHound 45 minutes later → goes straight to Running log. Reopens 90 minutes later → shows log list instead.

### Calendar Section

**Week starts on**: Sunday or Monday.

This affects how the **Week** interval groups entries in Summary view. If set to Monday, "the week of March 15" means Monday March 16 through Sunday March 22 (or similar, depending on the exact date). If set to Sunday, "the week of March 15" means Sunday March 15 through Saturday March 21.

### Table View Section

**Numeric precision**: A stepper control (0–10). Sets the number of decimal places shown for Number fields in **Table view** and **Summary view**. This is purely a display setting — the stored values have their full precision preserved.

Example: A stored value of 5.2847... displayed at precision 1 shows "5.3", at precision 0 shows "5", at precision 2 shows "5.28".

### Privacy Section

**Share Crash Reports** (toggle): If enabled, the next time the app crashes and is reopened, anonymous technical diagnostics are sent. Includes: device model, iOS version, stack trace. Does **not** include: log names, entry content, field values, any personal information.

### Data Section

**Backup Logs** (button): Opens the log selection screen for creating a .loghound backup.

**Restore Logs** (button): Opens the iOS Files picker to select a .loghound file for import.

### Danger Zone Section

**Reset All Data** (red destructive button): A two-step confirmation leads to permanently and irreversibly deleting:
- Every active log and all its entries
- Every archived log
- Every trashed log
- All settings (reset to defaults)
- All drafts

The app returns to the first launch welcome screen. **This cannot be undone.**

The confirmation dialog text: "Reset All Data? This will permanently delete all logs, entries, fields, and reset all settings to defaults. This action cannot be undone." with a "Yes, Permanently Delete All Logs and Data" button.

---

## Trial and Purchase

### Free Trial

The 30-day free trial begins on the **first launch**. All features are fully unlocked during the trial.

Remaining days are visible in: Settings → License → Status (e.g., "Trial: 23 days remaining").

### After Trial Expires

The app enters **read-only mode**.

**Still accessible**:
- View all logs, entries, cards, table, summary
- Search across all logs
- Access Settings
- View Active Alerts (already scheduled alerts may still fire)

**Blocked** (shows paywall sheet when attempted):
- Create a new log
- Edit any entry (fields, timestamp)
- Delete any entry
- Add, edit, or delete schema fields
- Duplicate a log or entry
- Archive, delete, restore any log
- CSV Export
- .loghound Backup
- Reset All Data

### Paywall Sheet

Shown when a blocked action is attempted. Contains:
- Lock icon
- "Unlock LogHound" title
- Description explaining the trial has ended
- **"Purchase — [price]"** button (e.g., "Purchase — $4.99")
- **"Restore Purchases"** button
- Dismiss button (×)

### Purchase

Tap **"Purchase — [price]"** → Apple ID confirmation dialog → on success, all features unlock immediately. One-time payment, no subscription, no recurring charges.

### Restoring a Purchase

Used when: reinstalling the app, switching to a new device, or if the app incorrectly shows the trial as expired after purchasing.

Tap **"Restore Purchases"** on the paywall or in Settings. This contacts Apple's App Store servers to re-validate the purchase. Requires an internet connection. On success, all features unlock.

---

## Common Questions and Answers

**Q: Can I change a field's type after creating it?**
A: No. Field types are permanent. The user must delete the field (losing any existing data in that field) and add a new one with the desired type.

**Q: I deleted a field by accident — can I get the data back?**
A: No. Field deletion is permanent and immediate. The data cannot be recovered. Encourage the user to use Backup regularly to protect against this.

**Q: Can I use LogHound on iPad?**
A: LogHound is an iOS app and runs on iPad via iOS compatibility. The interface is designed for iPhone but functions on iPad.

**Q: Does LogHound sync between devices?**
A: No. There is no cloud sync. Data lives only on the device where it was entered. To move data between devices, use the .loghound backup and restore workflow.

**Q: Why doesn't my field appear in Summary view?**
A: Summary view only shows Number, Star Rating, and Toggle fields. Text, Single Select, Multi Select, Date/Time, and Location fields are excluded. If the log has none of those three types, Summary view shows an empty state.

**Q: Why is the "..." log action menu showing fewer options than expected?**
A: CSV Export is disabled when the log has no entries. All other actions are always available.

**Q: My notification didn't fire — what should I check?**
A: (1) iOS Settings → LogHound → Notifications — ensure "Allow Notifications" is ON. (2) The alert was set for a future time — past-dated alerts are skipped silently. (3) The date in the entry matches what the user expected — tap "Edit alerts" to verify the preview.

**Q: I see old values pre-filled in a new entry form — is this a bug?**
A: No. This is the **draft** feature. The user previously started filling an entry, dismissed the form without saving, and the values were saved as a draft. To clear the draft, they can tap Cancel → Discard (if prompted) or just save the form.

**Q: Can I import data from other apps?**
A: Not directly. LogHound does not import CSV files — it only exports them. Data must be entered manually or restored from a .loghound backup created by LogHound itself.

**Q: Why are some options not showing in my Single Select field?**
A: Options may have been **deprecated**. Deprecated options are hidden from the picker but preserved in existing entries. To see all options including deprecated ones, go to the schema editor → tap the field → view the options list.

**Q: I bought LogHound on my old phone but it shows "Trial Expired" on my new phone.**
A: Tap **Restore Purchases** on the paywall or in Settings. This re-validates the purchase with Apple's servers and unlocks the app.

**Q: How do I see all my alerts in one place?**
A: Tap the **bell icon** on the log list (top area). If there are no alerts, the icon may not have a badge. The Active Alerts view shows all upcoming alerts across all logs with time filter tabs.

**Q: Can I track something that happens multiple times a day?**
A: Yes. Just create multiple entries in the same log on the same day. Each entry has its own timestamp. Filters and Summary view can aggregate or filter by date range.

**Q: What happens to my filters when I close the app?**
A: Filters **persist** between sessions. If you set a filter and close the app, the filter is still active when you return. To clear filters, open the Filter sheet and tap "Clear All" or toggle the master switch off.

**Q: Can I have different fields in different logs?**
A: Yes. Each log has its own completely independent schema. A Running log can have Distance, Duration, and Route while a Medication log has Dose, Time, and Notes. There is no shared schema system.

**Q: What is the entry limit per log?**
A: There is no documented per-log entry limit. Performance depends on device storage and available memory.

---

## Use Case Schema Recipes

These are recommended field configurations for common tracking needs. Share these with users who ask "how would I track X in LogHound?"

### Medication / Supplement Log
- **Medication** — Single Select (options: each medication name)
- **Dose** — Number (allow decimals: off, for whole pill counts) or Text (for "500mg")
- **Time Taken** — Date/Time (picker: Date & Time; set alert for next dose)
- **Side Effects** — Multi Select (options: nausea, headache, drowsiness, none, etc.) or Text
- **Notes** — Text

### Fitness / Workout Log
- **Exercise Type** — Single Select (options: Running, Cycling, Weights, Yoga, etc.)
- **Duration** — Number (minutes, allow decimals: off)
- **Distance** — Number (miles/km, allow decimals: on)
- **Intensity** — Star Rating (emoji: 🔥, max: 5)
- **Heart Rate** — Number (bpm, allow decimals: off)
- **Notes** — Text

### Habit Tracker
- **Habit** — Single Select (if tracking multiple habits in one log) OR use a separate log per habit
- **Completed** — Toggle (this is the key field; Summary → Sum + Week shows total completions)
- **Duration** — Number (minutes, if tracking time-based habits)
- **Quality** — Star Rating (if tracking quality of completion)
- **Notes** — Text

### Sleep Log
- **Bedtime** — Date/Time (time only)
- **Wake time** — Date/Time (time only)
- **Hours slept** — Number (allow decimals: on, e.g., 7.5)
- **Quality** — Star Rating (emoji: 😴 or ⭐)
- **Dreams** — Toggle
- **Notes** — Text

### Mood / Mental Health Diary
- **Mood** — Star Rating (emoji: 😊 or ❤️, max: 5)
- **Energy** — Star Rating (emoji: ⚡, max: 5)
- **Anxiety** — Star Rating (emoji: 😰, max: 5)
- **Activities** — Multi Select (options: exercise, socializing, work, nature, etc.)
- **Sleep hours** — Number (allow decimals: on)
- **Notes** — Text

### Food / Nutrition Log
- **Meal** — Single Select (Breakfast, Lunch, Dinner, Snack)
- **Food** — Text
- **Calories** — Number (allow decimals: off)
- **Protein** — Number (grams, allow decimals: off)
- **Satisfaction** — Star Rating (emoji: 😋)

### Reading Log
- **Title** — Text (required)
- **Author** — Text
- **Genre** — Single Select (Fiction, Non-fiction, Biography, etc.)
- **Rating** — Star Rating (emoji: ⭐, max: 5)
- **Pages read** — Number (allow decimals: off)
- **Started** — Date/Time (date only)
- **Finished** — Date/Time (date only)
- **Notes** — Text

### Car Maintenance Log
- **Service Type** — Single Select (Oil Change, Tire Rotation, Brakes, Inspection, etc.)
- **Mileage** — Number (allow decimals: off)
- **Cost** — Number (allow decimals: on, for dollars/cents)
- **Shop** — Text or Single Select
- **Next Service Due** — Date/Time (date only; set an alert for reminder)
- **Notes** — Text

### Symptom Diary
- **Symptom** — Multi Select (options: headache, fatigue, nausea, pain, brain fog, etc.)
- **Severity** — Star Rating (emoji: 🩺 or 😣, max: 5)
- **Duration** — Number (hours, allow decimals: on)
- **Possible Trigger** — Multi Select (stress, food, sleep, weather, etc.)
- **Medication taken** — Toggle
- **Notes** — Text

### Plant / Garden Log
- **Plant** — Single Select or Text
- **Action** — Single Select (Watered, Fertilized, Pruned, Repotted, etc.)
- **Health** — Star Rating (emoji: 🌿, max: 5)
- **Notes** — Text
- **Next action** — Date/Time (date only; set alert as a reminder)

---

## Data Loss Prevention Guide

Help users avoid losing data. These are the scenarios that can cause permanent data loss:

1. **Deleting a field**: All data in that field across all entries is permanently deleted. No undo. Recommendation: only delete fields you are sure you don't need.

2. **Deleting an entry**: Permanent, no trash. Recommendation: use Duplicate if you want to modify an entry while preserving the original.

3. **Emptying trash**: Logs in trash are permanently deleted. Recommendation: restore important logs from trash before using Empty Trash.

4. **Reset All Data**: Nuclear option, no recovery. Should only be used to completely start over.

5. **No backup**: If the device is lost, damaged, or reset without a .loghound backup, all data is gone. Recommendation: regular backups via Settings → Backup Logs, stored to iCloud or emailed to yourself.

6. **Deprecating a select option and then deleting it**: Deprecated options are preserved in existing entries. If a deprecated option is later fully deleted (removed from the options list), entries that used it may show an empty value. Check before deleting options.

---

## Troubleshooting Reference

| Problem | Likely Cause | Solution |
|---------|-------------|----------|
| Data seems missing | Log was archived or deleted | Check Archive (bottom-left toolbar) and Trash (bottom-right toolbar) |
| Notifications not arriving | iOS permission denied | iOS Settings → LogHound → Notifications → Allow |
| Alert fired at wrong time | Alert not updated after editing the date | Open entry → Edit alerts → Save again to reschedule |
| Form pre-filled with old data | Draft was saved from previous session | Fill correctly and Save, or tap Cancel → Discard Draft |
| Save button greyed out | Required field not filled | Look for field with red asterisk (*) |
| Field not in Summary view | Wrong field type | Only Number, Star Rating, Toggle appear in Summary |
| Option not in Select picker | Option was deprecated | Check schema editor → field → options list for deprecated options |
| Purchased but trial expired message | Purchase not validated on this device | Tap Restore Purchases (paywall or Settings) |
| Log not in active list | Log was archived | Check Archive view |
| Alert not available to set | Date is in the past | Change the Date/Time field to a future value |
| Restore overwrote my log | It didn't — restore adds logs, never overwrites | The original and restored logs coexist (restored may be renamed) |
| Summary showing no data | No Number/Rating/Toggle fields | Add one of those field types to the schema |
| CSV export greyed out | Log has no entries | Add at least one entry first |
