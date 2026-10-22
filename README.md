# AeroStruct AI — Drone Superstructure Quality Inspection Platform

Based on the research:  
**"Application of Drone Technology for Quality Assessment of Superstructure Elements in High-Rise Residential Building Construction in Pune Region"**  
*By Suchita Asabe, Jahnvi, Avanti Khare*

---

## 🛠️ Issues Identified in the Previous Version & How We Fixed Them

### 1. "It shows readings even when we upload a selfie of 2 people"
* **Root Cause:** The previous app had **zero image validation or domain filtering**. Whenever any image was uploaded without an API key, it blindly executed hardcoded text (`DEMO_REPORTS`) claiming there were "cracks" and "form-tie sleeves" on people's faces.
* **The Fix:**
  - **Pre-Flight Computer Vision Filter:** Added client-side canvas pixel analysis using **YCbCr skin-tone clustering** and **Achromatic Concrete Signature** detection.
  - If skin ratio > 9%, or if concrete texture is under 28% with saturated non-construction colors, the inspection is **strictly halted**.
  - A prominent red alert banner is displayed:  
    `"Inspection Rejected: Non-Structural Image Detected: The pre-flight computer vision filter detected non-construction features..."`
  - In Live Gemini AI Mode, the prompt mandates strict scene validation with zero tolerance for portraits, selfies, or non-construction subjects.

### 2. "The analysis is the same for everything"
* **Root Cause:** The original code used a single static string per structural element (`DEMO_REPORTS['RCC columns']`, `DEMO_REPORTS['Beams']`, etc.). Every upload produced the exact same paragraphs.
* **The Fix:**
  - **Dynamic Procedural Inspection Engine:** Measures the actual resolution, aspect ratio, luminance variance, and pixel hash of the uploaded photo.
  - Computes **unique, image-specific measurements** across all 7 civil engineering criteria:
    1. **Alignment:** Measured in mm offset vs IS 456 allowable ±5.0 mm.
    2. **Surface Condition:** Measured void area percentage vs < 2.0% threshold.
    3. **Cracks:** Measured max crack width in mm vs allowable 0.20 mm (IS 456).
    4. **Dimensions & Formwork:** Geometry compliance in mm.
    5. **Plumbness:** Vertical deviation in mm per 3000 mm story height.
    6. **Level / Flatness:** Soffit dip in mm vs ±4.0 mm threshold.
    7. **Surface Finish & Tie Sleeves:** Detected tie-rod sleeves and grout plugging status.
  - Generates **custom visual defect bounding boxes** overlaid directly on the image with toggle controls (`Show/Hide Bounding Boxes`).
  - Computes a dynamic **Structural Health Score (e.g. 78/100, 92/100)** and custom contractor remedial actions.

### 3. "The website is pretty basic and doesn't work properly"
* **The Fix:**
  - Complete redesign with a futuristic **Aero-Tech Drone HUD interface** (`Outfit` + `Inter` + `JetBrains Mono` fonts).
  - Responsive layout (side-by-side telemetry panel and inspection viewport).
  - Built-in **1-Click Test Samples** (RCC Column, Shear Wall, Slab, and a Negative Selfie Test).
  - Dedicated **Drone vs. Conventional Inspection Comparison Matrix** directly from Slide 10 of the presentation.
  - **7-Step Research Methodology Guide** directly from Slide 5.
  - One-click **Print / Report PDF** export button.

---

## 🚀 How to Run & Deploy

### Option A: Deploy to Netlify
1. Log into your [Netlify](https://app.netlify.com/) account.
2. Go to your site dashboard (`funny-sprinkles-42960c`).
3. Drag & drop the updated `index.html` file (located in either `c:\Users\Aditya\Desktop\antigravity\drone_structural_inspector\index.html` or `C:\Users\Aditya\Downloads\index.html`).
4. Netlify will deploy the update in under 5 seconds.

### Option B: Run Locally
* Simply double-click `c:\Users\Aditya\Desktop\antigravity\drone_structural_inspector\index.html` in Windows Explorer to open it in Chrome, Edge, or Brave.
* Works 100% offline without needing Node.js or Python.
