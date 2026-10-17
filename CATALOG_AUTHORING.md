# Author a clothing texture

1. Choose `catalog/v1/guides/upper-base-v1.png` or `lower-base-v1.png`.
2. Paint a 1024 x 1024 opaque sRGB PNG inside the cyan UV islands. Keep the same layout ID; do not edit the app mesh UVs.
3. Add the file at `catalog/v1/textures/<item-id>/albedo.png`.
4. Add an entry to `catalog/v1/manifest.json` with `id`, `title`, `meshAsset`, `uvLayoutID`, `texturePath`, and lowercase SHA-256.
5. For upper layouts, use one of `outfit_base_tee`, `outfit_base_hoodie`, `outfit_base_jacket`, or `outfit_base_puffer` and `upper-base-v1`.
6. For lower layouts, use `pants_jeans` or `pants_sweatpants` and `lower-base-v1`.
7. Commit the PNG and manifest together. The app refreshes the public manifest, downloads a selected PNG over HTTPS, verifies its checksum, and caches it on-device.

The app permits PNGs up to 2048 x 2048 and 8 MB. Do not upload face scans, face images, face textures, biometric geometry, camera frames, or private device information. Do not commit third-party art without permission.
