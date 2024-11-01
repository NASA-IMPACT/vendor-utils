### Calculate Surface Reflectance

**Description**:  
Calculates the surface reflectance from PlanetScope imagery files. This function opens a PlanetScope `.tif` file to access the reflectance coefficient and the shape of the surface reflectance data array.

- **Input**:  
  - `tif_file` (str): Path to the PlanetScope `.tif` file containing the image data.

- **Expected Output**:  
  - `reflectance_coefficient` (float): The reflectance coefficient for the given PlanetScope image.
  - `surface_reflectance.shape` (tuple): A tuple representing the dimensions of the surface reflectance data array, typically indicating the number of rows and columns.

**Code Snippet**:

```python
with PlanetScope.open(tif_file) as planet_obj:
    print(planet_obj.reflectance_coefficient)

with PlanetScope.open(tif_file) as planet_obj:
    print(planet_obj.surface_reflectance.shape)
