# Read Quality Flag

**Description**:
This section accesses and extracts various quality flags from a PlanetScope image file, such as cloud, snow, and shadow masks. These flags help identify specific conditions in each pixel, allowing for data quality assessment and filtering of undesirable areas.

**Input**:
 - A PlanetScope TIFF file with associated quality assurance (QA) data (e.g., UDM2), and latitude and longitude coordinates for a point of interest.

**Expected Output**:
1. udm_data: Numpy array containing the quality mask values, representing different quality flags like cloud cover, snow presence, shadows, etc.
2. Quality mask information for a specified point (latitude, longitude) that indicates the data quality at that specific location.
3. Dictionary of available quality flags and their corresponding band indices in the UDM2 GeoTIFF file.
    
**Code Snippet**:
```python
# Accessing different quality masks
udm_data_array  # The primary UDM data array containing quality information # Accessing UDM (Unusable Data Mask) data

udm_data = udm_data_array.values  # Numpy array format of quality mask data # Convert UDM data to numpy array format for further analysis

with PlanetScope.open(tif_file) as planet_obj: # Extract quality flags for a specific point by providing latitude and longitude
    # Print quality information at a specific geographic point
    print(planet_obj.get_quality_from_point(lat=28.866933958061644, lon=-97.90677761357139))

# Available Quality flags and their corresponding band indices in the UDM2 GeoTIFF
udm_band_indices = udm_data_array.attrs.get("bands_indices")  # Dictionary mapping quality flags to band indices
print("Available Quality Flags and Band Indices:", udm_band_indices)

# Extract individual quality masks, each representing a specific condition
with PlanetScope.open(tif_file) as planet_obj:    
    # Obtain the "clear" mask, marking areas without clouds or haze
    clear_mask = planet_obj.get_quality_mask("clear")
    
    # Obtain the "cloud" mask, indicating cloud-covered areas
    cloud_mask = planet_obj.get_quality_mask("cloud")
    
    # Obtain the "snow" mask, highlighting areas covered by snow
    snow_mask = planet_obj.get_quality_mask("snow")
    
    # Obtain the "shadow" mask, marking regions in shadow
    shadow_mask = planet_obj.get_quality_mask("shadow")
    
    # Obtain the "haze_light" and "haze_heavy" masks, differentiating light and heavy haze
    haze_light_mask = planet_obj.get_quality_mask("haze_light")
    haze_heavy_mask = planet_obj.get_quality_mask("haze_heavy")
    
    # Obtain the "confidence" mask, which may indicate the confidence level of the data quality
    confidence_mask = planet_obj.get_quality_mask("confidence")
```
