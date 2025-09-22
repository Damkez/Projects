# Sabah Deforestation Monitoring (Earth Engine App)

Interactive Google Earth Engine (GEE) app to visualize **integrated deforestation alerts** in *Sabah, Malaysia*, inspect **Sentinel-2 before/after** imagery with a swipe, and plot **yearly trend charts** (2020–2025) for Sabah or any ADM2 district.

> Click a pixel → see alert date → open synced Sentinel-2 swipe → export alerts for offline analysis.

---

## ✨ Features

- **Integrated Alerts layer** (RADD radar + GLAD Landsat + GLAD Sentinel-2) with continuous date palette.
- **TMF Deforestation Year (2020–2024)** overlay.
- **JRC Global Forest Cover** context layer.
- **Sentinel-2 swipe:** before (~1 year) vs after (alert date) with linked maps for smooth wiping.
- **Trend chart (2020–2025):**
  - **Sabah-wide** chart shown automatically on app start.
  - Updates and shows the **selected district name** in the title.
- **One-click GeoTIFF export** of integrated alerts for the selected district.
- Layer toggles, opacity sliders, ADM2 boundary overlay, dynamic legend dates.

---

## 🗺️ Data Sources

- **Admin boundaries:**  
  `USDOS/LSIB_SIMPLE/2017`, `FAO/GAUL/2015/level1`, `FAO/GAUL/2015/level2`
- **JRC Global Forest Cover:** `JRC/GFC2020/V2`
- **TMF Deforestation Year:** `projects/JRC/TMF/v1_2024/DeforestationYear` (2020–2024)
- **Alerts integration (module & feeds):**  
  - Module: `users/nrtwur/alert_integration:alert_integration`  
  - RADD: `projects/radar-wur/raddalert/v1`  
  - GLAD Landsat: `projects/glad/alert/*` (2021–2023 + `UpdResult` for 2025)  
  - GLAD Sentinel-2: `projects/glad/S2alert/*`
- **Map styles:** `users/ProductDevelopment/Soy:MapStyles`

> Some `projects/*` assets require access; ensure your Earth Engine account is whitelisted.

---

## ▶️ Open Earth Engine Application

1. Open [https://code.earthengine.google.com/](https://productdevelopment.users.earthengine.app/view/sabah-deforestation-monitoring)

**Startup behavior:**  
- Centers on Sabah, loads default layers.  
- Shows the **Sabah-wide trend chart** automatically.  
- Selecting a district zooms, clips layers, and retitles the chart with the district name.

---

## 🧭 How to use

- **Click the map** (with Integrated Alerts ON) → shows pixel **alert date** + details panel.
- **“Show Sentinel-2 Swipe”** → opens linked “Before / After” maps for quick visual confirmation.
- Use **opacity sliders** to compare layers.
- **Export alerts**: “Get Integrated Alerts Download Link” generates a GeoTIFF for the selected district.

---

## 🧱 Implementation Notes

- **Homogeneous S2 composites:** collections are reduced after selecting a common RGB band set and casting to float to avoid “incompatible bands” errors.
- **S2 masking:** SCL-based mask excludes cloud/shadow/cirrus classes (3, 7, 8, 9, 10).
- **Trend chart:** sums pixel area (ha) by earliest alert year (2020–2025) within current AOI.

---

## 🛠️ Troubleshooting

**Error:** “Expected a homogeneous image collection…”  
**Fix:** Select a consistent subset (e.g., `['B4','B3','B2']`) and `toFloat()` **before** median/mosaic.

**No cloud-free S2 in window**  
Increase date window (e.g., ±60 days) or relax `CLOUDY_PIXEL_PERCENTAGE` (e.g., 30–40%).

**No download link**  
You must select a district first and have asset read permissions.

---
<img width="1676" height="1053" alt="image" src="https://github.com/user-attachments/assets/8768df67-faa3-4963-a8c6-6abbbf9961b7" />





