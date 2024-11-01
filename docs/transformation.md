
# Data Transformation

**Description**: Transform the downloaded images as required, including reprojection, clipping, and converting data formats to meet specific project needs.

**Input**: Downloaded TIFF file, target CRS, bounding box for clipping

**Expected Output**: 
 1. Geospatial data transformed to the target CRS or clipped to a specified area

**Code Snippet**:
```python
import rasterio
from rasterio.warp import calculate_default_transform, reproject, Resampling

# Open the TIFF file and set target CRS
with rasterio.open("downloaded_images/image.tif") as src:
    transform, width, height = calculate_default_transform(
        src.crs, 'EPSG:4326', src.width, src.height, *src.bounds
    )
    kwargs = src.meta.copy()
    kwargs.update({
        'crs': 'EPSG:4326',
        'transform': transform,
        'width': width,
        'height': height
    })

# Reproject and save the output
with rasterio.open("reprojected_image.tif", 'w', **kwargs) as dst:
    for i in range(1, src.count + 1):
    reproject(
    source=rasterio.band(src, i),
    destination=rasterio.band(dst, i),
    src_transform=src.transform,
    src_crs=src.crs,
    dst_transform=transform,
    dst_crs='EPSG:4326',
    resampling=Resampling.nearest
    )
print("Reprojection completed!")
```
