# SB Knit Designer

Procedural knitwear for **Houdini Indie**. Turn garment meshes into stitch
patterns and detailed yarn geometry.

This repository distributes SB Knit Designer Free. It contains downloads,
examples and documentation. The development source and Plus pattern library
are maintained separately.

## Download

[Download SB Knit Designer Free 1.0.0](downloads/SB_Knit_Designer_v1.0.0.zip?raw=true)

The download includes a `.hdalc` asset, an Indie `.hiplc` dress example,
installation instructions and license terms. It includes six patterns:
Stockinette, Reverse Stockinette, Garter, 1x1 Rib, 2x2 Rib and Seed.

**Free is for personal practice and learning, with no commercial use.**
SB Knit Designer Plus adds all 76 patterns and permits commercial use,
subject to Houdini Indie eligibility and license limits.

## Requirements

Houdini Indie 21 or 22. Tested on Linux; Windows is a supported target with
a code audit, with runtime verification still pending. macOS is not promised.
This is an Indie-first tool; a commercial-format release may follow later.

## Start here

1. Unzip the download to a permanent folder.
2. Install the `.hdalc` through Assets > Install Asset Library, or follow
   the package installation instructions in the [user guide](docs/USER_GUIDE.md).
3. Open the supplied dress example at Stitch Map. Step to Final Yarn when ready.

See the [user guide](docs/USER_GUIDE.md), [license](LICENSE.txt),
[changelog](CHANGELOG.md) and [validation results](RELEASE_VALIDATION.md).

For animation, simulate the garment with Vellum and Point Deform the yarn.
The example includes this bypassed recipe. Avoid rebuilding the knit every
frame from a moving simulation.

Free and Plus use the same node type. Remove Free before installing Plus,
and restart Houdini.
