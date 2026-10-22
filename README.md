# Wajir rangelands blog assets

Interactive pieces for the emLab blog post *What pastoralists in Wajir told us about rangeland resilience* by Kathy Baylis and Heather Lahr:

- **Scrolling map.** As readers scroll, the map moves from Kenya's national parks and Nairobi to Wajir County, then out to the long-distance migration of herds toward Mozambique.
- **Photo gallery.** A slideshow of photos from the trip that readers can swipe or click through, and that advances on its own.

Each piece is plain HTML with no build step.

```
index.html              the scrolling map
gallery/
  photo-gallery.html    the photo gallery
  images/               the gallery's photos
README.md
```

## Publish with GitHub Pages

1. Put the files on the `main` branch, keeping the layout above. `index.html` sits in the root, and the gallery sits in its own `gallery` folder.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch," choose `main` and `/ (root)`, then click **Save**.
4. After a minute or two, both pieces are live:
   - Map: `https://emlab-ucsb.github.io/wajir-rangelands-map/`
   - Gallery: `https://emlab-ucsb.github.io/wajir-rangelands-map/gallery/photo-gallery.html`

Pages is free for public repositories. A private repository needs a paid GitHub plan to use Pages.

## Embed in Drupal

Paste each snippet into the blog body where the piece should appear.

**Map**

```html
<iframe src="https://emlab-ucsb.github.io/wajir-rangelands-map/"
        title="Interactive map: from Kenya's national parks to Wajir County and the migration of herds"
        width="100%" height="700"
        style="border:0;" loading="lazy"></iframe>
```

Readers scroll inside the map box itself. A height of 600–800 px works well.

**Photo gallery**

```html
<iframe src="https://emlab-ucsb.github.io/wajir-rangelands-map/gallery/photo-gallery.html"
        title="Photos from Wajir"
        width="100%" height="540"
        style="border:0; display:block; height:min(540px, calc(66vw + 70px));"
        loading="lazy" allowfullscreen></iframe>
```

The `height:min(...)` part shrinks the box on phones so there's no empty space under the gallery; on larger screens it stays 540 px. `allowfullscreen` lets readers click a photo to see it full screen. (iPhones don't allow full screen from an embed, so there the photo opens in a new tab instead.) The gallery advances every 5 seconds. To change the speed, add `?autoplay=8` to the end of the `src` link (for 8 seconds), or use `?autoplay=0` to turn autoplay off.

If an iframe disappears after saving, switch the text format to **Full HTML**, or ask a site admin to allow `<iframe>` in the usual format.

## Edit the map

Everything you're likely to change sits near the top of the `<script>` in `index.html`, in the section marked **EDIT THIS SECTION**.

- **Story text and camera:** each entry in `STEPS` is one scroll card. Change `title` and `text` for the words, `center` (longitude, latitude) and `zoom` for where the map flies to, and `show` for which map elements appear:
  - `"region"`: the Wajir County outline
  - `"places"`: the Wajir town dot
  - `"landmarks"`: the Nairobi skyline and park badges
  - `"mask"`: the gray veil over countries outside Kenya
  - `"migration"`: the animated route, the Mozambique tint, and the hotspot
- **Park badges:** edit `LANDMARKS` to add, remove, or move icons. Each entry has a name, a designation (shown on the label's second line), an icon type (`city` or `park`), coordinates, and a label position (`left`, `right`, `below`, or `none`).
- **Migration hotspot:** `MIGRATION_END` sets where the route ends, and `MIGRATION_BEND` sets how it curves. The destination is illustrative, since the post describes reports rather than a specific route.
- **Colors:** the emLab palette is defined as variables at the top of the `<style>` block.
- **Gray veil strength:** change `0.35` in the `mask` line (lower values are lighter).

To check changes before publishing, open `index.html` directly in a browser. The preview in Claude's chat interface can't load map tiles, so the map appears blank there even when the code is fine.

## Edit the gallery

The photos are listed in `PHOTOS`, near the top of the `<script>` in `gallery/photo-gallery.html`. Each line is one photo, shown in the order listed:

```js
{ src: "images/team.jpg", alt: "Team photo", caption: "The team", credit: "" },
```

- **`src`:** the file name inside `gallery/images/`.
- **`alt`:** a short description for screen readers.
- **`caption`:** the text under the photo.
- **`credit`:** an optional photographer credit, shown in lighter text after the caption. Leave it as `""` for none.

To add a photo, upload it to `gallery/images/` and add a line to `PHOTOS`. Resize photos to about 1,600 px wide before uploading so the gallery loads quickly.

Keep captions short (under about 40 characters, including the credit) so they fit on one or two lines on phones.

To change the default autoplay speed, edit the `5` in the line that sets `AUTOPLAY`. Colors are variables at the top of the `<style>` block, taken from the emLab site.

To check changes before publishing, open `gallery/photo-gallery.html` directly in a browser.

## Credits and data

- Basemap: [OpenFreeMap](https://openfreemap.org), © [OpenMapTiles](https://openmaptiles.org), data © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors
- Map library: [MapLibre GL JS](https://maplibre.org) 4.7.1 (BSD-3-Clause), loaded from jsDelivr
- Wajir County and Kenya boundaries: [geoBoundaries](https://www.geoboundaries.org) (source: RCMRD GeoPortal), public domain
- Mozambique boundary: [geoBoundaries](https://www.geoboundaries.org) (source: OpenStreetMap contributors), Open Database License 1.0
- Typefaces: Literata (map) and Nunito Sans (gallery) via Google Fonts (SIL Open Font License)
- Gallery photos: from the blog post, stored in `gallery/images/`

The basemap and boundary credits appear in the map's attribution corner, which should stay visible.

## Acknowledgment

This code was developed with the help of Claude (Anthropic). Any errors are my own. ([Sarah Erickson](https://github.com/sarahmariee))
