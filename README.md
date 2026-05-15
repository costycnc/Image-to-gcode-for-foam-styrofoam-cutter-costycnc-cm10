*"Keep the credits, keep the innovation."*

# COSTYCNC - Perforated Hollow Cylinder Foam Cutter

**Original work by: Boboaca Costel (CostyCNC)**  
**Website: https://costycnc.it**  
**GitHub: @costycnc**

**Patent pending - Rotary-on-X Technology for Hollow Cylinder Cutting**

---

## What is this?

This software enables **CNC hot wire cutting of perforated hollow cylinders** (foam lampshades, decorative columns, cylindrical patterns) using a **single continuous path** .

**Watch the original video:**  
https://www.youtube.com/shorts/MuAxfM_hZJw

---

## The Problem This Solves

| Traditional problem | COSTYCNC solution |
|--------------------|-------------------|
| Requires expensive 4/5 axis CAM software | Simple image → G-code |
| Complex programming for rotary axis | Rotary table connected to X axis |


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

3. **Open <a href="https://costycnc.github.io/Image-to-gcode-for-foam-styrofoam-cutter-costycnc-cm10/">Image-to-gcode</a>

4. **Enter cylinder diameter** (mm)

5. **Load an image** (drag & drop, paste, or file upload)

6. **Send to machine** or save to SD card

---

## Requirements

- GRBL-based CNC controller (ESP3D, Arduino + GRBL)
- Rotary table connected to **X axis driver**
- Hot wire foam cutter (Nichrome wire)
- EPS or polyurethane foam
- Modern web browser

---

## Installation

No installation.Directly in browser!

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


