# Search and Filter Data

**Description**: Use search parameters to filter available Planet data based on location, time frame, and specific requirements such as cloud cover percentage. This step helps select data efficiently based on specific analysis needs.

**Input**: Bounding box coordinates, date range, maximum cloud cover percentage

**Expected Output**: 
 1. List of available imagery items matching the criteria

**Code Snippet**:
```python
from planet import DataClient, filters

# Define bounding box, date range, and cloud cover filter
bbox = [-122.5, 37.5, -121.5, 38.5]
date_range = filters.date_range("acquired", gt="2022-01-01", lt="2022-01-31")
cloud_cover = filters.range_filter("cloud_cover", lt=0.1)

# Combine filters
combined_filter = filters.and_filter(
    filters.geom_filter(bbox),
    date_range,
    cloud_cover
)

# Initiate DataClient and search
client = DataClient(auth)
results = client.search(name="PSScene3Band", filter=combined_filter)

print("Number of images found:", len(results))
```
