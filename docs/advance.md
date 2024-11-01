# Exploring Other Functions from `rasterio` and `rio-xarray`

**Description**: This example demonstrates how to use the `rio-xarray` and `rasterio` libraries to perform common geospatial operations on raster data. It includes reprojecting the coordinate reference system, clipping the raster to a bounding box, and resampling the raster resolution.

- **Input**:
  - `ras1`: Input raster in an initial coordinate reference system.
  - `tif_file`: Path to a TIFF file used for resampling.
  - `bbox`: Bounding box coordinates (`minx`, `miny`, `maxx`, `maxy`) for clipping the raster.

- **Expected Output**:
  - `ras1_lonlat`: Raster reprojected to the EPSG:4326 coordinate reference system.
  - `clipped`: Raster clipped to the specified bounding box.
  - Resampled raster saved as `resampled_raster.tif` in the specified directory.

**Code Snippet**:

```python
# Reprojection
ras1_lonlat = ras1.rio.reproject("EPSG:4326")
print(ras1_lonlat)

# Clip the raster
from shapely.geometry import box

minx, miny, maxx, maxy = -90.32, 31.33, -89.90, 31.15
bbox = box(minx, miny, maxx, maxy)
clipped = ras1_lonlat.rio.clip([bbox], crs="EPSG:4326")

# Resample
from rasterio.enums import Resampling

scale_factor = 0.75
with rasterio.open(tif_file) as src:
    data = src.read(
        out_shape=(
            src.count,
            int(src.height * scale_factor),
            int(src.width * scale_factor)
        ),
        resampling=Resampling.bilinear
    )

    profile = src.profile
    profile.update(
        width=data.shape[2],
        height=data.shape[1]
    )

    with rasterio.open("VendorUtil_Planet/NewData/resampled_raster.tif", "w", **profile) as dst:
        dst.write(data)

print("Success: Resample saved")
