# Read Data

**Description**:
This section loads a PlanetScope TIFF image file and reads its associated metadata and quality data. The goal is to load the primary data array, quality data (e.g., UDM data for quality control), and metadata for further analysis

**Input**: 
- A PlanetScope TIFF file, assumed to be in GeoTIFF format, containing remote sensing imagery and associated metadata.

**Expected Output**: 
  1. data_array: Numpy array or similar data structure containing the image data from the TIFF file.
  2. udm_data_array: Numpy array containing quality data (e.g., an Unusable Data Mask [UDM]) for the image.
  3. metadata: Dictionary or structured object containing image metadata, including spatial resolution, acquisition date, sensor details, etc.

**Code Snippet**:
```python
# Path to the tif file
tif_file = "/path_to_planetscope.tif"
# Load data 
with PlanetScope.open(tif_file) as planet_obj:
    # Display file paths to verify that data, metadata, and QA files are loaded correctly
    print(planet_obj.data_file_path) # Path to main image data
    print(planet_obj.metadata_file_path) # Path to metadata information
    print(planet_obj.qa_file_path) # Path to quality assurance data
    # Load the primary data array
    data_array = planet_obj.data
    # Load quality data, such as UDM (Unusable Data Mask), to assess data validity
    udm_data_array = planet_obj.quality_data
    # Load metadata, including acquisition information and spatial resolution
    metadata = planet_obj.metadata
```
