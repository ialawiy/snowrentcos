# ❄️ Snowrentcos (real store btw 😉) - Cozy Scrapbook Rental Catalog 

Welcome to **Snowrentcos**! This is a lightweight, zero-framework, anime- and cosplay-focused rental catalog. Inspired by the cozy, playful, "made-with-love" aesthetic of `straw.page`, the frontend blends a digital scrapbook feel with a dynamic, live-updating booking engine powered entirely by Google Sheets.

---

## 🛠️ The Tech Stack

No heavy frameworks, no bloated node modules, and absolutely zero compilation required. 

* **HTML5 & Vanilla JavaScript (ES6+):** Handles the core app state, dynamic client-side filtering, and swipe gesture mapping.
* **CSS3 (Scrapbook Engine):** Uses custom CSS layers, dashed borders, rotation offsets, and CSS gradients to achieve a tactile, paper-like UI without relying on heavy image assets.
* **Google Fonts API:** Pulls **Fredoka** (for bubbly, sticker-style headers) and **Quicksand** (for clean, readable metadata).
* **OpenSheet API (`opensheet.elk.sh`):** A free, blazingly fast open-source microservice that turns any public Google Spreadsheet into a clean JSON endpoint instantly.

---

## 📂 Code Section Breakdown

The single-file architecture (`index.html`) is structured into three clean layers:

### 1. The State & Configuration Layer
Located at the top of the `<script>` block, this contains the hardcoded configurations for your brand:
* `SPREADSHEET_ID`: Points directly to your live Google Sheet ecosystem.
* `AVAILABLE_SHEETS`: An array tracking exactly which sheet tabs the app should fetch.
* `TABLE_VISIBLE_COLUMNS`: Safely whitelists which spreadsheet columns display in the logistics views (`Resi`, `COD`).

### 2. The Data Fetch & Render Pipeline
* `fetchSheetData(sheetName)`: Asynchronously calls the OpenSheet endpoint. It displays a cute loading state, flips the layout view depending on the tab type, and passes raw JSON downstream.
* `executeRenderPipeline()`: The central traffic controller. It takes your search queries, filters the rows dynamically across all columns, and builds the visual elements.
* `renderGridView()` vs `renderTableView()`: `List` defaults to the high-energy asset grid, while logistics sheets seamlessly morph into clean, scannable ledger tables.

### 3. Interactive Ecosystem
* **Booking Engine (`openBookingModal`):** Tracks dates relative to the timeline, triggers safety warnings if an user selects a past date, maps costume variables, and builds a beautifully formatted WhatsApp template.
* **Touch Vector Matrix:** Uses `touchstart` and `touchend` event listeners to calculate swipe distances (`SWIPE_MIN_DISTANCE = 60`), allowing mobile users to turn pages just like a physical notebook.

---

## 🎨 Visual Architecture & Aesthetics

The interface is custom-tailored to look completely personalized and youthful:

* **The Sticker Title (`h2`):** Styled with layered text-shadows and a subtle `-1.5deg` rotation to look like a physical sticker slapped onto the page.
* **Polaroid Card System (`.grid-card`):** Uses alternating `nth-child` rotations (`0.8deg` / `-0.8deg`) so items look organically spread across a desk. A CSS pseudo-element (`::before`) automatically pins a `📎` paperclip to the top-left of every single image.
* **Washi-Tape Tabs (`.tab-button`):** Standard browser buttons are replaced with soft border capsules that tilt playfully when clicked active.
* **Dotted Journal Canvas:** The background utilizes a lightweight dual-layered radial CSS gradient to simulate grid-dot bullet journal paper without downloading a single image.

---

## ⚙️ Customization & Fine-Tuning

Want to change things up? Here is how to customize your notebook on the fly:

### 🔄 Swapping the Data Source
Simply change these two strings in your `<script>` tag to map your own inventory:
```javascript
const SPREADSHEET_ID = 'YOUR_NEW_GOOGLE_SHEET_ID_HERE';
const AVAILABLE_SHEETS = ['List', 'Resi JNT', 'Resi Paxel', 'COD'];

```

### 🎨 Tweak the Color Palette

The page colors are controlled via CSS variables and standard hex codes. To change the overall vibe, adjust these key classes in your `<style>` block:

* **Main Accent Blue (Tabs/Headers):** Change `#7cb5ec` and `#5b9bd5`.
* **Price Sticker Tag (Pink):** Change `.price-circle` background-color (`#ff8fa3`) to match your favorite theme color.
* **Dot Grid Canvas:** Adjust `#cbdbe6` in the `body` background-image property to make the journal dots darker or lighter.

### 📝 Modifying the WhatsApp Booking Template

Locate the `templateText` variable inside `openBookingModal()`. You can freely rewrite the text template using standard backticks. Use `${costumeName}` and `${dateString}` to insert dynamic data automatically.

```javascript
const templateText = `☃️ Your Shop Name ☃️\n\n1. Costume: ${costumeName}\n2. Date: ${dateString}`;

```
