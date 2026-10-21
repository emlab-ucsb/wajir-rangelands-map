# Wajir rangelands scrolling map

An interactive scrolling map for the emLab blog post *What pastoralists in Wajir told us about rangeland resilience* by Kathy Baylis and Heather Lahr. As readers scroll, the map moves from Kenya's national parks and Nairobi to Wajir County, then out to the long-distance migration of herds toward Mozambique.

The whole map is a single file, `index.html`, with no build step.

## Publish with GitHub Pages

1. Put `index.html` and `README.md` in the root of this repository on the `main` branch.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to "Deploy from a branch," choose `main` and `/ (root)`, then click **Save**.
4. After a minute or two, the map is live at `https://<org-name>.github.io/<repo-name>/`.

Pages is free for public repositories. A private repository needs a paid GitHub plan to use Pages.

## Embed in Drupal

Paste this into the blog body, replacing the URL with the live Pages address:

```html
<iframe src="https://<org-name>.github.io/<repo-name>/"
        title="Interactive map: from Kenya's national parks to Wajir County and the migration of herds"
        width="100%" height="700"
        style="border:0;" loading="lazy"></iframe>
```

If the iframe disappears after saving, switch the text format to **Full HTML**, or ask a site admin to allow `<iframe>` in the usual format.

Readers scroll inside the map box itself. A height of 600–800 px works well.

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

## Credits and data

- Basemap: [OpenFreeMap](https://openfreemap.org), © [OpenMapTiles](https://openmaptiles.org), data © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors
- Map library: [MapLibre GL JS](https://maplibre.org) 4.7.1 (BSD-3-Clause), loaded from jsDelivr
- Wajir County and Kenya boundaries: [geoBoundaries](https://www.geoboundaries.org) (source: RCMRD GeoPortal), public domain
- Mozambique boundary: [geoBoundaries](https://www.geoboundaries.org) (source: OpenStreetMap contributors), Open Database License 1.0
- Typeface: Literata via Google Fonts (SIL Open Font License)

The basemap and boundary credits appear in the map's attribution corner, which should stay visible.

## Acknowledgment

This code was developed with the help of Claude (Anthropic). Any errors are my own. ([Sarah Erickson](https://github.com/sarahmariee))
