# SB Knit Designer 1.0.0

Knit an MD/CLO garment from its flat-pattern UVs. Free includes Stockinette,
Reverse Stockinette, Garter, 1x1 Rib, 2x2 Rib and Seed. Plus includes all 76
patterns. Free is for personal practice and learning; Plus permits commercial
use subject to your Houdini license. See LICENSE.txt in your download.

These downloads are Houdini Indie assets (`.hdalc`) with an Indie example
(`.hiplc`). Opening them makes the scene Limited Commercial. They are intended
for eligible Houdini Indie users, including users on either edition of this
asset. They are not a commercial-license studio asset distribution.

## Install

Unzip the entire download to a permanent folder. Before launching Houdini, add
that folder (the one containing `SB_Knit_Designer.json`) to
`HOUDINI_PACKAGE_DIR`. Keep existing package directories in that variable.
Alternatively, install `otls/sop_sishir.SB_Knit_Designer.1.0.hdalc` using
Houdini's Assets > Install Asset Library. The HDA embeds its modules and icon;
no Python installation is required.

If copying the JSON into your Houdini preferences `packages` folder, first set
`SB_KNIT_DESIGNER_ROOT` to the extracted download's absolute path, using forward
slashes on Windows. The JSON alone cannot find a separately installed asset.

Remove Free before installing Plus, then restart Houdini. Both define
`sishir::SB_Knit_Designer::1.0`, so existing scenes retain their pattern names
when upgraded. Install only one edition at a time. Plus-only patterns need
Plus; downgrading a Plus scene is not supported.

## Quick start

1. Open `examples/SB_Knit_Designer_dress_demo.hiplc`, or wire an MD/CLO garment
   into SB Knit Designer. Preserve UVs: one flat-pattern island per piece.
2. Choose a Pattern in Pattern Preview, then select Stitch Map to inspect the
   garment. Check Garment Units; Auto infers units from overall size.
3. Select Final Yarn to generate curves. Use Sweep for a tube preview.
4. For animation, freeze the garment at its rest frame with Time Shift. Build
   the yarn once from this rest garment. Simulate the garment with Vellum
   Cloth, then use Point Deform with yarn, rest garment and simulated garment
   as its three inputs. The example contains this bypassed recipe.

Do not feed a moving simulation directly into the knit node: it rebuilds the
knit every frame. Keep garment topology and point order consistent for Point
Deform. The yarn is a visual surface, not a strand-by-strand Vellum simulation.

## Performance and limits

On the demo dress, Houdini 22 on Linux: Stitch Map about 1 second, Final Yarn
about 21–23 seconds and 406k points. Subsequent identical cooks can reuse the
session's fabric cache. First Final Yarn after reopening a scene is a full
cook. Cache entries are shared across nodes, limited to 12 and approximately
256 MiB (one larger fabric can exceed that budget).

Settle runs for each distinct fabric, with cost depending on pattern and size.
It reduces yarn collisions; it does not guarantee clearance on every garment.
A sharp 2 m box test produced 2.4M points in about 76 seconds and warned that
closest approach was 0.929 of the yarn diameter. If clearance warns, reduce
Yarn Radius or increase Settle Steps, check the garment and gauge, and inspect
the result. Large or incorrectly scaled garments can need millions of stitches;
check Garment Units and UV Scale when the node refuses a piece.

Supported target: Houdini Indie 21 and 22 on Linux and Windows. Release assets
are built with 21.0.729; validation results are in RELEASE_VALIDATION.md.
Windows has a code audit but no runtime verification on this machine. macOS
is not promised. Settle uses OpenCL; when GPU OpenCL is unavailable, launch
Houdini with `HOUDINI_OCL_DEVICETYPE=CPU`.
