# SQL Server Spatial data types

Follow this 5-minute demonstration on SQL Server Spatial data types step-by-step guide to  use and see how it works:

### 1. Introduction to Spatial Data Types
- **Point**: Represents a single point in a coordinate system.
- **LineString**: Represents a line between two or more points.
- **Polygon**: Represents a shape with three or more points forming a closed ring.

### 2. Setup: Create a Spatial Data Table

Assuming you are logged in, create a new table using this command. This example uses the geography type (versus the geometry type) and is based on a round-earth coordinate system, making it suitable for global geographical data.

```sql
CREATE TABLE SpatialDemo (
    ID int PRIMARY KEY,
    GeomPoint geography,
    GeomLine geography,
    GeomPolygon geography
);
```

The *geometry* data type in SQL Server is designed to store and process planar, or flat-earth, spatial data, which is best used for local or project-specific spatial data.

### 3. Inserting Spatial Data
- **Insert a Point**
  ```sql
  INSERT INTO SpatialDemo (ID, GeomPoint)
  VALUES (1, geography::STPointFromText('POINT(-74.006 40.7128)', 4326));
  ```
- **Insert a LineString**
  ```sql
  INSERT INTO SpatialDemo (ID, GeomLine)
  VALUES (2, geography::STLineFromText('LINESTRING(-74.006 40.7128, -73.935242 40.730610)', 4326));
  ```
- **Insert a Polygon**
  ```sql
  INSERT INTO SpatialDemo (ID, GeomPolygon)
  VALUES (3, geography::STPolyFromText('POLYGON((-74.006 40.7128, -73.935242 40.730610, -73.9 40.7, -74.006 40.7128))', 4326));
  ```

### 4. Querying Spatial Data
- **Find a Point within a certain distance**
  ```sql
  SELECT ID FROM SpatialDemo
  WHERE GeomPoint.STDistance(geography::STPointFromText('POINT(-73.935242 40.730610)', 4326)) < 10000;
  ```
- **Determine if a Point is inside a Polygon**
  ```sql
  SELECT ID FROM SpatialDemo
  WHERE GeomPolygon.STContains(geography::STPointFromText('POINT(-74.006 40.7128)', 4326)) = 1;
  ```
- **Calculate the Length of a LineString**
  ```sql
  SELECT ID, GeomLine.STLength() FROM SpatialDemo
  WHERE ID = 2;
  ```

### 5. Visualizing the Data (Optional)
- If you have a tool that can visualize these spatial types (like SSMS), show the shapes on a map.

### 6. Conclusion
- Briefly summarize the capabilities of SQL Server Spatial data types and their applications.

This demonstration will give a concise yet comprehensive overview of how spatial data can be created, manipulated, and queried in SQL Server. Other database types are similar, particularly PostgreSQL/PostGIS. 
