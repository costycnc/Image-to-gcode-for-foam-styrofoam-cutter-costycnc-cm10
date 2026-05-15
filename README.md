
# COSTYCNC - Image to G-code for Foam Cutter

**Original work by: Boboaca Costel (CostyCNC)**  
**Website: https://costycnc.it**  
**GitHub: @costycnc**

## Description

This software converts images (SVG, PNG, JPG, BMP) to G-code for CNC foam cutters with **rotary axis** capability.

## COSTYCNC Rotary-on-X Technology

This is the **original invention** by Boboaca Costel (09.05.2023).

### How it works:

1. **Rotary table is connected to the X axis driver** (not a separate Z axis)
2. **G-code uses only X and Y** (NO Z axis commands)
3. **X coordinates are automatically scaled** based on cylinder diameter
4. **GRBL setting `$102` is fixed** (user never changes it)

### Why this is unique:

| Traditional method | COSTYCNC method |
|-------------------|-----------------|
| Uses Z axis for rotation | Rotary on X axis |
| User must change `$102` for each diameter | User only enters diameter once |
| Complex CAM software required | Simple image → G-code |
| G-code with X, Y, Z | G-code with only X, Y |

## GRBL Settings (set once, never change)

```
$100=80.00    (Y axis steps/mm)
$101=80.00    (X axis steps/mm)
$102=8.888    (X axis for rotary - FIXED)
```

**Important:** `$102=8.888` is calibrated for a cylinder with **120mm diameter**.  
The software automatically scales X coordinates for any other diameter.

## How to Use

1. **Connect your rotary table to the X axis driver** (parallel to the X motor or replace it)

2. **Set GRBL once** with `$102=8.888`

3. **Open the software** (index.html)

4. **Enter cylinder diameter** in mm

5. **Load an image** (drag & drop, paste, or file upload)

6. **Click GENERATE** → G-code is created with scaled X coordinates

7. **Send to machine** or save to SD card

## Features

- ✅ Drag & drop images
- ✅ Paste SVG from clipboard
- ✅ Load BMP, JPG, PNG, SVG files
- ✅ Automatic X scaling based on cylinder diameter
- ✅ G-code with only X and Y (NO Z)
- ✅ Generate from text (with custom fonts)
- ✅ Save G-code to file
- ✅ Upload to SD card (ESP3D compatible)
- ✅ Visual path preview

## Technical Details

### Scaling Formula

```
scale_factor = standard_diameter / user_diameter
X_scaled = X_original * scale_factor
```

- Standard diameter: 120mm (circumference = 377mm)
- User enters any diameter → software scales X automatically
- GRBL `$102` never changes

### Example

| User diameter | Scale factor | Original X=100 → Scaled X |
|---------------|--------------|---------------------------|
| 120 mm | 1.00 | 100 |
| 150 mm | 0.80 | 80 |
| 100 mm | 1.20 | 120 |
| 60 mm | 2.00 | 200 |

## Files

| File | Description |
|------|-------------|
| `index.html` | Main software (run in browser) |
| `README.md` | This file |

## Requirements

- Modern web browser (Chrome, Firefox, Edge, Safari)
- GRBL-based CNC controller (ESP3D, Arduino + GRBL)
- Rotary table connected to X axis driver

## Installation

1. Download `index.html`
2. Open in any web browser
3. No server needed (runs locally)

## License

This software includes the **COSTYCNC Rotary-on-X Technology** invented by Boboaca Costel.

If you use or modify this code, you must:
- Keep the original copyright header
- Give credit to COSTYCNC (https://costycnc.it)
- Link to this repository

## Contact

- Website: https://costycnc.it
- GitHub: @costycnc

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 09.05.2023 | Original invention (Rotary-on-X) |
| 1.1 | 15.05.2026 | Added automatic diameter scaling, removed Z axis |

---

**Created by Boboaca Costel (CostyCNC)**  
*"Keep the credits, keep the innovation."*

# COSTYCNC - Perforated Hollow Cylinder Foam Cutter

**Original work by: Boboaca Costel (CostyCNC)**  
**Website: https://costycnc.it**  
**GitHub: @costycnc**

**Patent pending - Rotary-on-X Technology for Hollow Cylinder Cutting**

---

## What is this?

This software enables **CNC hot wire cutting of perforated hollow cylinders** (foam lampshades, decorative columns, cylindrical patterns) using a **single continuous path** that never breaks the workpiece.

**Watch the original video:**  
https://www.youtube.com/shorts/MuAxfM_hZJw

---

## The Problem This Solves

| Traditional problem | COSTYCNC solution |
|--------------------|-------------------|
| Cutting a hollow cylinder with internal pockets usually destroys the workpiece | Continuous path logic (loops and bridges) - wire enters, cuts internal pockets, exits on same path |
| Requires expensive 4/5 axis CAM software | Simple image → G-code |
| Complex programming for rotary axis | Rotary table connected to X axis |
| User must reconfigure GRBL for each diameter | Automatic X scaling based on diameter |

---

## COSTYCNC Rotary-on-X Technology (Invented 09.05.2023)

### The Core Innovation

1. **Rotary table connected to X axis driver** (not a separate Z axis)
2. **G-code uses only X and Y** (NO Z axis commands)
3. **X coordinates automatically scale** based on cylinder diameter
4. **GRBL `$102` is fixed** (user never changes it)

### Why This Creates Perforated Hollow Cylinders

The continuous path logic allows the hot wire to:
- **Enter** the foam cylinder
- **Cut internal light pockets** (perforations)
- **Exit on the same path** without breaking the structure

This is impossible with traditional CNC methods (laser, router, or standard hot wire).

---

## GRBL Settings (Set Once - Never Change)

```
$100=80.00    (Y axis steps/mm)
$101=80.00    (X axis steps/mm)
$102=8.888    (X axis for rotary - calibrated for 120mm diameter)
```

**Important:** `$102=8.888` is fixed. The software automatically scales X coordinates for any cylinder diameter.

---

## How It Works - Step by Step

### 1. Physical Setup
- Rotary table connected to **X axis driver** (parallel to X motor)
- Hot wire on Y/Z axes

### 2. Software
- User enters **cylinder diameter** (mm)
- Loads an **image** (SVG, PNG, JPG, BMP)
- Software **automatically scales X coordinates** based on diameter

### 3. G-code Generated
```
(COSTYCNC Rotary-on-X - NO Z axis)
(Cylinder diameter: 150mm)
(Scale factor: 0.80)
G21 G90
G92 X0 Y0
G01 X0 Y0
G01 X80 Y10    (X scaled from 100 to 80)
G01 X160 Y20   (X scaled from 200 to 160)
...
G01 X0 Y0
```

### 4. Result
- Hot wire cuts a **perfect hollow cylinder**
- **Perforated patterns** (internal pockets) are cut without breaking the structure
- Continuous path ensures the cylinder remains intact

---

## Scale Factor Examples

| Cylinder Diameter | Circumference | Scale Factor | Original X=100 → Scaled X |
|-------------------|---------------|--------------|---------------------------|
| 120 mm (default) | 377 mm | 1.00 | 100 |
| 150 mm | 471 mm | 0.80 | 80 |
| 100 mm | 314 mm | 1.20 | 120 |
| 200 mm | 628 mm | 0.60 | 60 |
| 60 mm | 188 mm | 2.00 | 200 |

---

## Comparison with Other Methods

| Method | Can cut hollow cylinder? | Can perforate internal pockets? | Cost |
|--------|-------------------------|--------------------------------|------|
| COSTYCNC Hot Wire | ✅ YES | ✅ YES | Low |
| Laser cutter | ✅ YES | ❌ NO (cannot enter/exit) | High |
| CNC router | ❌ NO (cannot reach inside) | ❌ NO | Medium |
| 3D printing | ✅ YES | ✅ YES | Slow, expensive |
| Traditional hot wire (airfoils) | ❌ NO | ❌ NO | Low |

---

## Applications

- 🔦 **Foam lampshades** (hollow with perforated light pockets)
- 🏛️ **Decorative columns** (hollow with carved patterns)
- 🎄 **Christmas decorations** (hollow spheres with cutouts)
- 📦 **Protective packaging** (custom hollow shapes)
- 🎨 **Art installations** (perforated cylindrical sculptures)

---

## How to Use

1. **Connect rotary table to X axis driver**

2. **Set GRBL once** (`$102=8.888`)

3. **Open index.html** in browser

4. **Enter cylinder diameter** (mm)

5. **Load an image** (drag & drop, paste, or file upload)

6. **Click GENERATE** → G-code is created

7. **Send to machine** or save to SD card

---

## Technical Details

### The Continuous Path Logic

Traditional CNC cutting requires:
- Tool enters material
- Cuts shape
- **Lifts tool** (impossible with hot wire)

COSTYCNC method:
- Wire enters cylinder
- Cuts internal pockets using X rotation
- **Exits on the same path** using loop/bridge logic
- Cylinder remains intact

### Why NO Z axis?

The rotary table is on X axis, so:
- Z axis is free for hot wire vertical movement
- G-code is simpler (only X and Y)
- Compatible with standard GRBL (no 4th axis firmware needed)

---

## Requirements

- GRBL-based CNC controller (ESP3D, Arduino + GRBL)
- Rotary table connected to **X axis driver**
- Hot wire foam cutter (Nichrome wire)
- EPS or polyurethane foam
- Modern web browser

---

## Installation

1. Download `index.html`
2. Open in any web browser
3. No server needed (runs locally)

---

## Credits & Copyright

This software contains the **COSTYCNC Rotary-on-X Technology** for **perforated hollow cylinder cutting**.

**Invented by:** Boboaca Costel (CostyCNC) on 09.05.2023

**Original demonstration:**  
https://www.youtube.com/shorts/MuAxfM_hZJw

**If you use or modify this code:**
- ✅ Keep the original copyright header
- ✅ Give credit to COSTYCNC (https://costycnc.it)
- ✅ Link to this repository and the original video
- ❌ Do not remove the COSTYCNC branding from variables and functions

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 09.05.2023 | Original invention - Rotary-on-X for hollow cylinders |
| 1.1 | 15.05.2026 | Added automatic diameter scaling, removed Z axis, COSTYCNC branding |

---

## Contact

- Website: https://costycnc.it
- GitHub: @costycnc
- YouTube: COSTYCNC channel

---

**Created by Boboaca Costel (CostyCNC)**  
*"Perforated hollow cylinders - made simple."*

**Watch the original video:** https://www.youtube.com/shorts/MuAxfM_hZJw


