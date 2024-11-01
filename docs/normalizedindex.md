# Calculate Normalized Index

**Description**:
This section calculates various normalized indices, such as Band Ratio, NDVI (Normalized Difference Vegetation Index), and EVI (Enhanced Vegetation Index), which are useful for analyzing vegetation, water content, and other surface properties. The Band Ratio and NDVI are commonly used to detect vegetation health, while EVI provides enhanced sensitivity in high-biomass areas.

**Input**: 
PlanetScope TIFF file with multispectral image data (containing at least two bands for the Band Ratio and specific bands for NDVI and EVI).

**Expected Output**: 
 1. Normalized Data: Numpy array containing the normalized band ratio.
 2. NDVI: Numpy array with NDVI values, indicating vegetation health.
 3. EVI: Numpy array with EVI values, providing additional vegetation information with improved sensitivity in areas with dense vegetation.

**Code Snippet**:
```python
# Calculate Band Ratio (custom normalized index using specified bands)
with PlanetScope.open(tif_file) as planet_obj:
    # Calculate normalized index (Band Ratio) between bands at indices 0 and 3   
    normalized_idx = planet_obj.normalized_indices(band1_index = 0, band2_index = 3)
    # Check if all values are NaN, indicating potential issues with data or band selection
    print(np.isnan(normalized_idx).all())

# Calculate NDVI (Normalized Difference Vegetation Index)
with PlanetScope.open(tif_file) as planet_obj:   
    # Compute NDVI using the standard NIR and Red bands
    ndvi = planet_obj.ndvi
    print(np.unique(ndvi))

# Calculate EVI (Enhanced Vegetation Index
with PlanetScope.open(tif_file) as planet_obj:   
    # Compute EVI, useful for dense vegetation areas
    evi = planet_obj.evi
    # Print unique EVI values to verify output and detect any unexpected data artifacts
    print(np.unique(evi))
```

