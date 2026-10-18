# Mini Me Fashion Catalog

Public, image-only catalog for user-created clothing textures. The iPhone app reads a versioned manifest, downloads only the selected PNG over HTTPS, verifies its SHA-256, stores it in the app’s private Documents directory, and restores the saved upper and lower selections locally. Face scans and other biometric data are never sent to this repository.

## Author a design

1. Open `catalog/v1/templates/` and choose one of the five 2048 × 2048 blank PNGs: hoodie, tee, jacket, down jacket (puffer), jeans, or sweatpants.
2. Keep the matching `catalog/v1/guides/<garment>_uv_guide.png` beside the canvas in your image editor as a temporary guide layer. Hide or remove that guide layer before exporting the finished PNG.
3. Export an opaque sRGB PNG at 1024 or 2048 pixels per side. Do not change UV coordinates, crop the canvas, or resize one axis independently.
4. Add the PNG as `catalog/v1/textures/<stable-item-id>/albedo.png`.
5. Add an item to `catalog/v1/manifest.json`. Use the exact mesh and UV layout shown in `catalog/v1/layouts.json`, set a new `assetVersion`, and compute lowercase SHA-256 with `Get-FileHash <file> -Algorithm SHA256` in PowerShell.
6. Commit the PNG and manifest to this public repository. Open Closet in Mini Me, tap **Refresh**, then select the design in the matching upper- or lower-body group.

Example item: **Midnight Signal Hoodie**. It is a real 2048 PNG in the manifest and can be selected by the app. It was drawn on the actual front-body UV region of the shipped hoodie mesh.

## Supported runtime meshes

- Upper: `outfit_base_tee`, `outfit_base_hoodie`, `outfit_base_jacket`, `outfit_base_puffer` use `upper-base-v1`.
- Lower: `pants_jeans`, `pants_sweatpants` use `lower-base-v1`.

The four upper meshes have identical UV coordinates and face index lists. The jeans and sweatpants meshes also have identical UV coordinates and face index lists. Pixel-raster comparison found no overlapping UV islands within either layout. A texture item still targets one exact mesh; to offer the same art on another garment, add another manifest item for that mesh and layout. Upper and lower choices are saved independently.

## Geometry limits

A PNG changes fabric color and printed artwork on an existing mesh. It cannot create a hood, collar, zipper, pocket, quilt channel, fold or new garment silhouette. The current hoodie shell has no separate hood geometry or hood UV island; jacket and puffer shells share the same base topology and UV layout. Those structural upgrades need a new clothing mesh integration and app build.

The catalog permits only PNG texture data; app code validates the supported mesh/layout pair, HTTPS path, image dimensions and checksum. Do not upload face scans, face photographs, face textures, biometric geometry, camera frames, device identifiers, or artwork you do not have permission to publish.
