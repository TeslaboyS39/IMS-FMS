# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

IMS-FMS (Inventory Management System - Fleet Management System) is a self-contained single-page web application for managing fleet telematics assets. It tracks devices (FMC 150, FMB 150, FMC 650), CAN adapters (E Can, All Can 300), SIM cards, MDVR units, and camera systems (ADAS, DMS, Others) with smart hardware-to-SIM binding capabilities.

## Running the Application

**No build step required.** This is a single-file HTML application (~68 KB).

- **Local development:** Open `index.html` directly in a web browser
- **Production:** Deployed on Netlify (entry file must be `index.html`)
- **Test data:** Import `fleet_inventory_2026-01-06.json` via the app's Import feature

## Tech Stack

- Tailwind CSS v3 (via CDN)
- Vanilla JavaScript (ES6+)
- Browser localStorage for data persistence
- No external dependencies or npm packages

## Architecture

The application follows an MVC-inspired pattern in a single HTML file with embedded JavaScript.

### Data Structure

```javascript
appData = {
  metadata: { last_updated, total_records, columns },
  inventory: [
    {
      no, asset_code, item_name, category, serial_number,
      sim_card_number, sim_card_iccid, camera_package,  // Base, Plus, Pro+ (for camera categories)
      status, condition, location, assigned_to, assigned_unit, installed_unit_vin,
      set_of: [],      // Linked asset codes (binding)
      history: [],     // Audit trail of changes
      created_at, last_modified
    }
  ]
}
```

### Asset Categories

| Category | Item Names |
|----------|------------|
| Device-Telematics | FMC 150, FMB 150, FMC 650 |
| CAN | E Can, All Can 300 |
| SIM | SIM Card |
| MDVR | MDVR |
| ADAS-Camera | ADAS Camera |
| DMS-Camera | DMS Camera |
| Others-Camera | Others Camera |
| Camera-SIM | Camera SIM Card |

### Three Main Views

1. **Dashboard** - Stats cards, category/status charts, location tracking, activity feed
2. **Inventory** - Searchable/paginated table, CRUD operations, asset binding modal
3. **Download** - Google Drive integration for centralized data backups

### Key Functions

| Function | Purpose |
|----------|---------|
| `switchTab(tab)` | Navigation between views |
| `renderDashboard()` | Render stats and charts |
| `renderTable()` | Paginated inventory table with search |
| `saveItem(e)` | Create/Update with automatic history tracking |
| `addBinding()` / `removeBinding()` | Smart asset linking (Device ↔ SIM/CAN) |
| `exportData()` / `importData(e)` | JSON data portability |
| `viewHistory(i)` | Display audit trail modal |
| `autofillCategory()` | Auto-select category based on item name |
| `toggleCameraPackage()` | Show/hide Camera Package dropdown for camera categories |

### Smart Features

- **Asset binding:** Device-Telematics can only bind with CAN or SIM categories
- **Asset code peek:** Shows previously used codes for quick reference
- **Auto-fill category:** Based on item name selection
- **Camera package selector:** Dropdown (Base/Plus/Pro+) appears only for camera categories (ADAS, DMS, Others)
- **Audit trail:** Automatic change tracking (status, condition, location, bindings)

## Storage

- **localStorage key:** `fleet_master_v4`
- **Export format:** JSON with timestamp naming (`fleet_inventory_{YYYY-MM-DD}.json`)

## Configuration

- `rowsPerPage` constant (line ~568) controls pagination - default is 15 items per page
