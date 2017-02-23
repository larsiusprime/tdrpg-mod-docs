##1.4 HD vs Pixel Art

Defender's Quest DX has two art modes -- "HD" art and "original" art, which is separately toggle-able for both cutscenes and "sprites" (ie, everything that's not cutscenes).

This will be discussed in-depth in [Graphics section 3.1: HD vs Original](03_01_hd_vs_original.md), but we'll summarize a few key points here:

* The `gfx/` folder has two subfolders, `_hd`, and `_orig`, one for each art mode
* HD art generally scales proportionally with the game window
* Orig art scales on a whole-number basis so that pixels stay clean
* All scaling refers to the base resolution

The game's base resolution is 600 vertical pixels, and unless otherwise specified, any x/y coordinates or width/height properties in the game's data files use that basis. This means that if the current game size is larger than 600, then a scale factor is applied to these properties. So at a resolution of 900 vertical pixels, an object at y coordinate 10 will actually appear at y coordinate 15, and a size 10 font will actually appear as a size 15 font, etc.
