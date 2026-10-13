# Styles

Images the Hangouts app pulls from this repo (through the jsDelivr mirrors). Each file is a sealed `.hngts`
(zip of images, same `H26-SEAL-1` / ES256 seal as every other package). A 0-byte file is valid and means "no images".

| file | used by | contents |
| --- | --- | --- |
| `Carousel.hngts` | Today carousel | up to 5 slide images, shown in file-name order (`01-name.webp`, `02-name.webp`, ...) |

## Carousel slide images

- **Size: 2400 x 510 px** (about 4.7:1; the original banners were 2353 x 500). The carousel is 238 px tall and up to 2200 px wide, so this stays sharp on wide and 2x screens.
- Keep text and faces inside the **centered 85%**, since the sides crop on narrower windows (the slide is `object-fit: cover`).
- Keep the **bottom 12% and the middle 18% of the width** quiet: the progress dots sit there.
- Format: WebP (best), PNG, JPEG or AVIF. Under 600 KB each, under 24 MB per package.
- File names: letters, digits, `.` `_` `-` only, max 64 characters. The part before the extension is the slide's alt text.

## Sealing

```
node tools/build.mjs styles --dir <folder of images>
```

writes `Styles/Carousel.hngts` into the repo checkout (`HANGOUTS_REPO`), sealed with the official key. Commit it and purge
jsDelivr for `Styles/Carousel.hngts`.
