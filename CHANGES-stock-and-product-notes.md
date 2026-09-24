# Change Log: Product Stock, Product Notes and TikTok Try

**App:** glōw — skin ritual tracker
**File changed:** `index.html` (no other files touched)

## 1. Stock component

- New **My Stock** card for each category, listing every product the user owns.
  - **Facial Skin:** new **Stock** tab in the bottom navigation.
  - **Body Skin / Hair:** card at the bottom of each page, below the Weekly Schedule.
- Each stock entry supports: add (name, brand, notes), edit (🧪 details), delete (×, with confirmation).
- **Selecting from stock:** "+ Add product" in the Morning / Evening routines and in the Body / Hair schedules opens a picker of stock items not already in that routine. New products can still be typed in and are added to stock automatically.
- Removing a product from a routine does **not** remove it from stock. Removing it from stock does **not** remove it from a routine.
- Renaming a product from stock renames it everywhere (stock, routines, logs, tracker data, ingredients, details).
- Re-adding a product that was used before keeps its tracker data (previously it was reset).
- **Migration:** on first load after the update, stock is filled from the products already in the routines and schedules. Nothing is lost.

## 2. Brand and notes

- The **Product Details** modal (🧪), used across Facial, Body and Hair, has two new fields: **Brand** and **📌 Important Notes**. Both are also available when adding to stock.
- **Daily checklist:** brand shows under the product name. Notes show under it in a distinct **plum** colour (`NOTE_COLOR = #7b4fa0`) with a tinted background and left border, as a reminder. Notes dim slightly once the product is ticked.
  - Facial: Morning and Evening checklists.
  - Body / Hair: the "Today" card.
- Brand also appears beside the product name in the Weekly Schedule.
- To change the note colour, edit the single `NOTE_COLOR` constant near the top of the script.

## 3. TikTok Try (new category)

A fourth category in the top panel, next to Facial Skin, Body Skin and Hair.

- **Add** a product or a trend: name, brand (products only), what it claims, 📌 important notes, optional area (Face, Body, Hair…).
  - **Save for later** puts it in *To try*; **Start trial** begins it immediately.
  - Starting a trial means choosing a **trial period** (7 / 14 / 21 / 30 days or a custom number of days, max 90) and a start date.
- **Tracker:** one cell per day of the period. Tap a day to mark it as used (past or today only), or use **Check in today**. Shows progress through the period and days used.
- **Observations:** dated entries with an impression (😍 Better / 😐 No change / 😣 Worse) and free text. Latest is shown, with "Show all".
- **Reflection:** available from the last day of the period (**Reflect & decide**), or earlier via **Reflect early**. Includes a summary (period, days used, observations), a free-text reflection and a required **verdict**:
  - ✅ **It worked**
  - 🎭 **Just for show**
- Trials are grouped as *Reflection due*, *Trying now*, *To try* and *Finished*. A count of Worked / Just for show sits at the top.
- The TikTok Try category button shows a badge with the number of reflections due.
- Finished trials keep their tracker and observations read-only. The reflection and verdict can still be edited.

## 4. Data (localStorage)

| Key | Change |
|---|---|
| `glow_stock` | **New.** `{ facial: [names], body: [names], hair: [names] }` |
| `glow_tiktok` | **New.** Array of trials: `{ id, type, name, brand, claim, notes, area, status (idea/active/done), days, startDate, endDate, checkins {date: true}, observations [{id, date, impression, text}], reflection {text, reflectedOn}, verdict (worked/show) }` |
| `glow_product_meta` | Each entry gains `brand` and `notes` (existing `price` and `incompatible` unchanged) |

All other keys are unchanged.

## 5. Other

- Bottom navigation (Facial) now has 7 tabs; label size reduced slightly so they fit.
- If the app's `sw.js` caches files, bump its cache version so devices pick up the new `index.html`.
