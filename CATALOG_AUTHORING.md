# Clothing texture authoring guide

For each garment, the PNG blank is 2048 × 2048 sRGB and uses the exact UV coordinates in the matching bundled runtime OBJ. The guide is a separate image at the same pixel dimensions and coordinates. Hide the guide before exporting art.

| Garment | Runtime mesh | UV layout | Blank | Guide |
| --- | --- | --- | --- | --- |
| Hoodie | `outfit_base_hoodie` | `upper-base-v1` | `catalog/v1/templates/hoodie_blank.png` | `catalog/v1/guides/hoodie_uv_guide.png` |
| T-shirt | `outfit_base_tee` | `upper-base-v1` | `catalog/v1/templates/tee_blank.png` | `catalog/v1/guides/tee_uv_guide.png` |
| Jacket | `outfit_base_jacket` | `upper-base-v1` | `catalog/v1/templates/jacket_blank.png` | `catalog/v1/guides/jacket_uv_guide.png` |
| Down jacket | `outfit_base_puffer` | `upper-base-v1` | `catalog/v1/templates/puffer_blank.png` | `catalog/v1/guides/puffer_uv_guide.png` |
| Jeans | `pants_jeans` | `lower-base-v1` | `catalog/v1/templates/jeans_blank.png` | `catalog/v1/guides/jeans_uv_guide.png` |
| Sweatpants | `pants_sweatpants` | `lower-base-v1` | `catalog/v1/templates/sweatpants_blank.png` | `catalog/v1/guides/sweatpants_uv_guide.png` |

## Uploading a design

1. Copy a blank PNG and paint it in an image editor. Keep the canvas 2048 × 2048; artwork should stay within the outlined UV islands.
2. Save the finished opaque sRGB PNG to `catalog/v1/textures/<item-id>/albedo.png`.
3. Compute the checksum in PowerShell: `Get-FileHash .\albedo.png -Algorithm SHA256`.
4. Add an item object to `catalog/v1/manifest.json`:

```json
{
  "id": "hoodie-blue-print",
  "title": "Blue Print Hoodie",
  "category": "upper",
  "meshAsset": "outfit_base_hoodie",
  "uvLayoutID": "upper-base-v1",
  "texturePath": "catalog/v1/textures/hoodie-blue-print/albedo.png",
  "assetVersion": "1.0.0",
  "sha256": "replace-with-64-lowercase-hex-digits"
}
```

5. Commit the PNG and manifest together. In the app, open Closet and tap **Refresh**. Choose the downloaded item under the matching upper or lower section. It is applied to that exact garment mesh and saved locally. Downloaded designs remain available offline and restore after app restart.

An art update that keeps the same item ID must increment `assetVersion` and update the SHA-256. The app uses the version and checksum in its local cache filename, so the updated PNG does not reuse old cached bytes.

## What changes without an app update

A new PNG for a supported mesh/layout pair appears after the user refreshes the catalog. The manifest data never runs as code. App changes are needed only to introduce a new garment mesh, new UV layout, image type, or behavior.

The current shell meshes are designed to receive color and print sheets. Texture art cannot add missing 3D garment features. In particular, the current hoodie mesh has no separate hood surface or hood UV island. Do not paint a hood onto the sheet and expect it to create hood geometry.

The app accepts PNG files up to 2048 × 2048 pixels and 8 MB and requires a valid SHA-256 checksum. Catalog images are downloaded over HTTPS from `raw.githubusercontent.com` under this repository. Face photos, captured face textures, face geometry, camera frames, or device identifiers must never be uploaded here.
