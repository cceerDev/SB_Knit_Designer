# Release validation — 2026-10-30

SB Knit Designer 1.0.0, Indie-first release candidate for 2026-10-31.
Built with Houdini 21.0.729 on Linux using an Indie license. The asset is
`.hdalc`; the example is `.hiplc`. A commercial-format release is deferred.

## Automated checks

- 185 Python tests passed with Houdini 21's Python 3.11 and numpy.
- Free builder smoke: 6 presets and 2 stitches passed; sampler clearance 1.042.
- Plus builder smoke: 76 presets and 40 stitches passed; sampler clearance 1.000.
- Builder checks include garment mapping, per-piece overrides, missing input,
  empty input, and visibility of oversized-fabric errors on the asset.
- Both archives were extracted to temporary folders and tested with fresh
  preferences, only their own package directory, no repository PYTHONPATH,
  and CPU OpenCL. Their Indie examples loaded without load warnings.

| Houdini / Linux | Edition | Preview | Stitch Map | Final Yarn |
| --- | --- | --- | --- | --- |
| 21.0.729 | Free | 0.87 s | 1.09 s | 22.54 s |
| 22.0.466 | Free | 0.79 s | 1.10 s | 21.42 s |
| 21.0.729 | Plus | 0.99 s | 1.27 s | 23.21 s |
| 22.0.466 | Plus | 0.91 s | 1.09 s | 21.74 s |

Dress output: 3,131 preview points; 144,253 map points; 406,442 final points.
Times vary by machine and cache state. The dress's Auto/cm warning is expected.

Additional extracted-archive regressions verify:

- Free embeds only the six selected patterns and k/p stitch definitions;
  chart overrides reject paid stitch IDs; generated VEX contains no paid charts.
- Cache state is shared by instances. Fifteen tiny fabrics exercise count
  eviction, a stale lookup recovers through the store branch, and a reduced
  byte budget exercises memory eviction. This is a focused cache regression,
  not a stress test with twelve large garments.
- Empty input reports its own error without stale units or chart warnings.
- Edition metadata, stable menu tokens and relative example paths are present.

Reproduce with:

    /opt/hfs21.0.729/bin/hython tools/make_release.py --edition free
    /opt/hfs21.0.729/bin/hython tools/make_release.py --edition paid
    python3 tools/check_releases.py /opt/hfs21.0.729/bin/hython /opt/hfs22.0.466/bin/hython

The validator also checks actual metre/cm mismatch reporting and that the
Final Yarn garment path executes the Settle growth loop.

## Known limits

Windows is a supported target with a code audit, but no Windows runtime test
was available here. macOS is not promised. A sharp-corner 2 m box can settle
short of clearance (prior probe: 0.929 of the yarn diameter, 76 s, 2.4M points).
That limit and the suggested adjustments are documented in README.md.

The example includes a bypassed Vellum/Point Deform recipe, not a finished
animation. Configure constraints for the intended shot. Commercial Houdini
asset and scene formats are outside this Indie release.
