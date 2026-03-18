# CardioFlow — Auxetic Coronary Stent Design Studio

> **Athens 2026 Course — Medical Device Hackathon**
> Universidad Politecnica de Madrid

An interactive, browser-based parametric design tool for auxetic coronary artery stents. Built as the engineering companion for the [CardioFlow](https://platform.ubora-biomedical.org/projects/3d6c68ed-c419-4d23-b59a-aa43c83ee3b6) open-source biomedical device on the UBORA platform.

**Live demo:** [stent.vincentsmid.xyz](https://stent.vincentsmid.xyz)

---

## About the Device

The proposed device is a **self-expanding, drug-eluting metallic stent** manufactured via 3D additive printing (Selective Laser Melting) using a superelastic **Nitinol (Nickel-Titanium)** shape-memory alloy.

- **Technology:** 3D-printed auxetic (negative Poisson's ratio) geometry optimized for the coronary arteries. Delivered in a compressed state, it self-expands upon release from a retractable sheath when exposed to body temperature.
- **Intended use:** Transcatheter treatment of *de novo* stenotic lesions caused by atherosclerosis. The device permanently restores coronary blood flow by exerting continuous outward radial force against the arterial wall.
- **Key clinical benefits:**
  - Zero longitudinal foreshortening during deployment (auxetic geometry), enabling highly accurate placement across the cardiac lesion.
  - Biomimetic, laser-induced superhydrophobic surface texture that repels blood proteins to prevent acute thrombosis.
  - Bioresorbable polymer coating eluting Sirolimus to inhibit smooth muscle cell hyperproliferation, preventing long-term in-stent restenosis.
- **Intended users:** Board-certified interventional cardiologists operating in a clinical catheterization laboratory equipped with fluoroscopy.
- **Limitations:** Highly dependent on ultra-precise 3D-printing resolutions (70-100 um struts) and strict thermal control during shipping/storage to maintain Nitinol in its compressed (Martensitic) phase.
- **Contraindications:** Hypersensitivity to Nickel or Sirolimus; inability to tolerate long-term dual antiplatelet therapy (DAPT); target lesions that cannot be crossed by standard 0.014-inch guidewires or microcatheters.

---

## What the Simulator Does

The design studio is a single-page web application (pure HTML/JS, no build step) that lets engineers and researchers interactively explore stent geometry and mechanical behavior in real time via a 3D viewport powered by Three.js.

### Parametric Geometry

All stent parameters are adjustable through the control panel:

| Parameter | Range | Description |
|---|---|---|
| Diameter (start/end) | 1.5 - 6.0 mm | Outer diameter at proximal and distal ends (supports tapered designs) |
| Length | 5 - 30 mm | Total stent length |
| Strut width / depth | 0.10 - 0.40 mm | Cross-section dimensions of individual struts |
| H (vertical rib) | 0.20 - 1.20 mm | Height of the vertical rib element |
| L (diagonal rib) | 0.20 - 1.00 mm | Length of the diagonal rib element |
| Re-entrant angle | 15 - 40 deg | Controls the degree of auxetic behavior |
| Cells (circumferential) | 6 - 18 | Number of unit cells around the circumference |
| Cells (axial) | 4 - 24 | Number of unit cells along the length |

### Auxetic Cell Topologies

Four unit-cell geometries are available:

- **Re-entrant honeycomb** — classic negative Poisson's ratio structure
- **Double arrowhead** — alternative auxetic with different compliance profile
- **Anti-tetrachiral** — chiral lattice with rotating nodes
- **Star honeycomb** — star-shaped auxetic pattern

### Deformation Animations

The 3D viewport visualizes four mechanical loading modes:

- **Crimp** — simulates catheter loading; the stent contracts radially and axially, demonstrating the negative Poisson's ratio behavior
- **Expand** — simulates self-expansion at body temperature with axial elongation and no foreshortening
- **Bend** — shows conformability to vessel curvature
- **Flex** — simulates pulsatile cardiac loading

Each mode has adjustable deformation intensity (0-100%) and animation speed, with play/pause controls.

### Real-Time Metrics

The viewport overlay displays live computed values:

- Current effective diameter
- Poisson's ratio (nu)
- Re-entrant angle (theta)
- Total strut count

### Compare Mode

A split-view mode allows side-by-side comparison of two configurations. Snapshot the current design into viewport B, then modify parameters in viewport A to visually compare geometries.

### Presets

- Save and load named parameter presets (persisted in localStorage)
- Export/import full configurations as JSON files for sharing between team members

### Export

- **STL download** — generates a watertight STL mesh via SDF voxelization and Marching Cubes, suitable for 3D printing or FEA import. Voxel resolution is adjustable (0.020 - 0.080 mm).
- **PDF spec sheet** — generates a printable A4 document with a 3D render, all geometry parameters, computed mechanical properties, and additive manufacturing printability notes (LPBF feature sizes, overhang angles, post-processing allowances).

---

## Getting Started

No build tools or dependencies required. Open `index.html` in any modern browser.

```bash
# Clone and open
git clone https://github.com/vincentsmid/coronary-artery-stent-simulator.git
open index.html
```

External libraries loaded via CDN:
- [Three.js](https://threejs.org/) r128 — 3D rendering
- [jsPDF](https://github.com/parallax/jsPDF) 2.5.1 — PDF generation

---

## License

This project is part of the [UBORA](https://platform.ubora-biomedical.org/) open-source biomedical device ecosystem.
