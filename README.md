# FabricBOM

**Cross-product Bill of Materials generator for Fortinet Security Fabric deployments**

![Version](https://img.shields.io/badge/version-1.0.1b-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![PWA](https://img.shields.io/badge/PWA-installable-purple) ![Offline](https://img.shields.io/badge/offline-ready-brightgreen)

![FabricBOM demo BOM screenshot](docs/screenshots/fabricbom-screenshot-demobom.jpg)

---

## Overview

FabricBOM is a client-side web application for building and exporting structured Bill of Materials quotes for Fortinet network security deployments. Select from 30+ supported products across eight solution categories, configure hardware models, support tiers, and add-on licenses, then assemble everything into a single exportable Project BOM — no backend, no installation, no internet connection required.

Designed to be run entirely offline. Install it as a web app on most modern browsers, iOS, or Android for convenient repeat access.

> **Disclaimer:** FabricBOM is not an officially sanctioned Fortinet product. Always validate output against official Fortinet product ordering guides. All source and reference materials are public.

---

## Features

### Building a BOM
- **30+ product configurators** — dedicated per-product pages organized in a sidebar by solution category
- **Per-product configuration** — select hardware model, quantity, FortiCare support tier, and product-specific add-on licenses
- **Sections** — **Add ▸ Add section** inserts a divider for a site, phase, or option (e.g., "Core Firewall", "Option A – SD-WAN") with an optional note and price total; everything below a section belongs to it until the next one
- **Item classification** — tag line items as REQUIRED, OPTIONAL, or EXCLUDED; items without pricing auto-flag as ATTENTION
- **Inline editing** — edit quantities, notes, product and section names, and item types directly in the BOM table
- **Drag-to-reorder** — drag products, sections (with everything under them), and individual line items into any order; line items can also be moved with ↑/↓ from the keyboard
- **Copy & paste** — duplicate a product, or a section with everything under it, anywhere in the BOM; the clipboard persists across reloads and other open tabs, so blocks can be moved between projects
- **Add part numbers** — with a price list loaded, **Add ▸ Add part numbers** opens on a search of it: part numbers and descriptions, `OR` / `NOT` / `"phrases"`, family and type filters, and one result per part number with its price (term versions -12 / -36 / -60 collapse to -DD). Tap **+ Add**, and again for more. Anything else can be typed in manually, with sub-headings to organize the lines
- **Configure a product** — **Add ▸ Configure a product…** opens the product list (behind ☰ on a phone) to build a FortiGate, FortiSwitch, FortiAP and more step by step

### Project Management
- **New BOM** — one click in the sidebar clears the BOM and Project Information to start a fresh quote (with a confirmation when there's anything to lose)
- **Named project saves** — the toolbar **Save** button stores the project under its Customer / Opportunity name (asking for one if it's blank) and shows **Saved** or an unsaved-changes dot, so it's always clear whether the current BOM has been saved
- **Version history** — each project retains previous saves; restore any prior version with one click
- **Session persistence** — IndexedDB keeps your active BOM intact across page refreshes
- **Project metadata** — capture customer/opportunity name, opportunity ID, SE name, date, and project scope notes

### Pricing
- **Price list upload** — drag-and-drop a Fortinet CSV or XLSX price list to apply pricing across all BOM items; columns are matched by name, so old and new Fortinet layouts both import even as columns are added, dropped, or reordered
- **Auto-applied pricing** — matched prices appear inline; SKUs with no price match are flagged automatically
- **Section totals** — optionally show a price total on each section
- **Quote scope** — in Pricing & Quotes, quote the entire Project BOM or just one section, so a multi-phase BOM can be priced and exported per phase / site
- **Discount matrix columns** — add, rename, re-type, and remove extra partner-type and named-account columns directly in the Discount Matrix; no CSV round trip needed, and rates carry over on rename

### Export & Sharing
- **Export ▸ Excel (.xlsx)** — project details plus a filterable line-item table (section, heading, sub-heading, part number, description, qty, type, notes), with list price, extended price, and totals when a price list is loaded; built with the bundled SheetJS library, so it works offline. The workbook also carries a hidden **FabricBOM data** sheet (the same project data a share link holds) so it can be reopened in FabricBOM
- **Export ▸ CSV (.csv)** — the same line-item table as a plain CSV for importing into other tools
- **Export ▸ Print / Save as PDF** — browser-native print layout optimized for customer-ready output
- **Export ▸ Copy share link** — a compressed URL containing the full BOM; pastes as a named hyperlink in email / Teams / Slack and as a plain URL elsewhere, and recipients open it directly in their browser
- **Export ▸ Copy to clipboard** — the line items as a table for Excel, CSV, or Markdown
- **File ▸ Download .fbom file** — the native FabricBOM format for saving a full project to disk
- **File ▸ Open file** — reopens a `.fbom`, Excel, or CSV file:
  - an **Excel** export that hasn't been changed reopens exactly, including section notes, type overrides, and password protection
  - an **edited Excel** export keeps your edits — changed quantities, added or removed rows, retyped items, and updated project details — while the hidden sheet fills in what a table can't hold
  - a **CSV** export (or any spreadsheet with a *Part Number* / *SKU* column) is read row by row and replaces the BOM's line items, keeping the current Project Information since CSV files don't include it
  - SKUs exported with a -12 / -36 / -60 term are turned back into -DD so the term selector keeps working
- Term suffixes (-12 / -36 / -60) are resolved on every SKU in every export
- **Global license term** — apply 1-year, 3-year, 5-year, or co-term suffixes to all SKUs at export time

### Security & Privacy
- **Read-Only mode** — lock a BOM against accidental edits; toggle with a single checkbox
- **Password protection** — optionally require a password to unlock; encrypts the Customer, Opportunity ID, and Project Scope fields in all exports so recipients without the password cannot view sensitive deal details
- **Fully local** — all data (projects, pricing, BOM state) is stored in your browser's IndexedDB and never transmitted to any server

### App & Accessibility
- **Progressive Web App** — installable on desktop, iOS, and Android; works fully offline via service worker
- **Sidebar product search** — filter the 30+ product list by name in real time
- **Responsive layout** — mobile-optimized with a slide-in sidebar and expandable row details
- **Help & FAQ** — built-in documentation page with animated GIF walkthroughs
- **Dependency-free runtime** — plain HTML, CSS, and JavaScript; no build step, no npm, no frameworks

---

## Supported Products

| Category | Products |
|---|---|
| Network Security | FortiGate (FGT), FortiADC (FAD), FortiDDoS, FortiDeceptor (FDC), FortiPAM, FortiProxy, FortiSandbox (FSA), FortiWeb (FWB) |
| Cloud Security | FortiAppSec Cloud, FortiCNAPP, FortiSASE |
| Email Security | FortiMail (FML), FortiMail Workspace |
| Network Access | FortiAP (FAP), FortiExtender (FEX), FortiPresence, FortiSwitch (FSW) |
| Endpoint Security | FortiClient (FCT), FortiDLP, FortiEDR |
| Access Control | FortiAuthenticator (FAC), FortiNAC |
| Management | FortiAnalyzer (FAZ), FortiAIOps, FortiManager (FMG), FortiMonitor, FortiRecon, FortiSIEM, FortiSOAR |
| Licensing | FortiFlex |
| Part Numbers | Add part numbers (search the price list or type them in) |

---

## Getting Started

**Requirements:** Any modern web browser. No installation, build step, or internet connection needed.

**Open locally:**

```bash
# Option 1 — open directly in your browser
open index.html

# Option 2 — serve with any static file server
npx serve .
python3 -m http.server 8080
```

**Basic workflow:**

1. Select a product from the sidebar (use the search box to filter quickly)
2. Configure the hardware model, quantity, support tier, and any add-on licenses
3. Click **Add to Project BOM**
4. Repeat for each product; use **Add ▸ Add section** to divide the BOM by site, phase, or option, and **Add ▸ Add part numbers** for SKUs you already know
5. Fill in project metadata (customer name, opportunity ID, SE, date, scope)
6. Optionally upload a Fortinet price list to show pricing
7. Click **Save**, then select the license term and use **Export** for Excel, CSV, print/PDF, or a share link

---

## Architecture

FabricBOM is intentionally dependency-free — everything runs in the browser with plain HTML, CSS, and JavaScript.

```
FabricBOM/
├── index.html              # Main hub: sidebar, project metadata, BOM cart
├── sw.js                   # Service worker for offline PWA support
├── manifest.json           # PWA manifest
├── products/               # Self-contained per-product configurators (30+)
│   ├── fortigate-bomgen.html
│   ├── fortiswitch-bomgen.html
│   ├── custom-sku-bomgen.html
│   └── ...
├── docs/
│   ├── help-faq.html       # Built-in help documentation
│   └── screenshots/
├── forti-icons/            # SVG product icons
└── js/
    └── xlsx.mini.min.js    # Bundled SheetJS for Excel export
```

- **`index.html`** hosts the sidebar navigation, project metadata form, BOM cart, saved projects manager, and all export/share/import logic
- **`products/*.html`** are embedded as iframes; each is a standalone product configurator
- **PostMessage API** carries BOM line-item data from product iframes to the parent hub
- **IndexedDB** stores saved projects, version history, and uploaded price lists — all local, all private
- **LZString compression** encodes BOM state into shareable URLs without any server involvement
- **SKU convention** — internal SKUs use a `-DD` placeholder; the hub substitutes the correct term suffix (`-12`, `-36`, `-60`) at export time

---

## License

[MIT](LICENSE) — 2026 msalty
