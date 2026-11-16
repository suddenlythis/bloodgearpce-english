# Installing the Blood Gear English translation (v1.0)

The download contains only the changes to the game's data tracks, not the game.
You need your own disc image of **Blood Gear (Japan)**.

## What you need

- A disc image of Blood Gear (Japan) as one `.cue` and 45 track `.bin` files, the
  form [Redump](http://redump.org/disc/36834/) catalogues (product code HCD4048).
- Two of those files get patched, and each must be exactly:

  | File | Size | SHA-1 |
  |---|---|---|
  | `Blood Gear (Japan) (Track 02).bin` | 20,079,024 bytes | `e318aedf1bbee57cf3c756b8347abbd4328664ec` |
  | `Blood Gear (Japan) (Track 45).bin` | 19,733,280 bytes | `bc5dc13bf0ca8365a447a61572d867cf39ba2dd6` |

  With any other file the patch refuses to apply.
- xdelta3, or a front end for it such as Delta Patcher or xdelta UI.
- A PC Engine CD emulator with a Super System Card (version 3.0).

## What is in the zip

| File | What it is |
|---|---|
| `BloodGear-EN-v1.0-Track02.xdelta` | The patch for Track 02, the game data |
| `BloodGear-EN-v1.0-Track45.xdelta` | The patch for Track 45, the disc's second copy of the data |
| `Blood Gear EN.cue` | Optional cue sheet, only for the side-by-side alternative below. Most people do not need it |
| `README.txt` | The release notes |

## Why two patches

The disc holds the game data twice: Track 02 is what the console normally reads,
and Track 45 is a copy it falls back on if it cannot read the first. The
translation changes both in the same way, so patch both: with only one patched,
the two copies on the disc no longer agree.

## How to apply

Patch each of the two files with its own `.xdelta`. Keep the file names, and open
your usual `.cue`. That is all.

### With Delta Patcher

Do this twice, once for each track:

1. **Original file** = your `Blood Gear (Japan) (Track 02).bin`
2. **XDelta patch** = `BloodGear-EN-v1.0-Track02.xdelta`
3. Tick **Backup original file** in the settings, then **Apply patch**.

Then the same with `(Track 45).bin` and `BloodGear-EN-v1.0-Track45.xdelta`.

### With the command line

xdelta3 writes a new file, so rename the originals first:

```
ren "Blood Gear (Japan) (Track 02).bin" "Track 02 original.bin"
ren "Blood Gear (Japan) (Track 45).bin" "Track 45 original.bin"
xdelta3 -d -s "Track 02 original.bin" BloodGear-EN-v1.0-Track02.xdelta "Blood Gear (Japan) (Track 02).bin"
xdelta3 -d -s "Track 45 original.bin" BloodGear-EN-v1.0-Track45.xdelta "Blood Gear (Japan) (Track 45).bin"
```

### Check the result

The patched files have these SHA-1 checksums:

| File | SHA-1 after patching |
|---|---|
| Track 02 | `e92eea46d8fe60e17937f38759cb5ba625e196a0` |
| Track 45 | `8c8306ae2aa610e0d4894b11a4b74cca8eb97be9` |

## Alternative: keep the Japanese and English discs side by side

Leave your two files alone, save the patched ones as `Blood Gear EN (Track 02).bin`
and `Blood Gear EN (Track 45).bin` in the same folder, and open `Blood Gear EN.cue`
from the zip. That cue lists your original audio tracks plus the two patched
tracks. If your files are named differently, edit the names in it.

## After patching

Start a new game or boot fresh. A save state made on the Japanese game keeps
showing the old text until the game loads that area again. In-game saves are not
affected.

## Tested on

Mednafen 1.32.1. Not tested on other emulators or on real hardware.
