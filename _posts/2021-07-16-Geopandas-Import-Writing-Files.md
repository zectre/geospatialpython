## Geopandas Read and Write Data
Geopandas is a great tools for manipulating geospatial data. It can process a lot of geospatial data format like Esri shapefile, Geopackage and GeoJSON.
You can download the example of Semarang City spatial data in Esri shapefile format with this command
```
!gdown https://drive.google.com/u/2/uc?id=1XcPEdwSWysU5PWy2NnFca7QWqQkoMBPC&export=download
!unzip KOTA_SMG.zip
```
You need to install geopandas first, try using pip install geopandas

### Importing and Reading Data
```
import geopandas
smg = geopandas.read_file('/content/KOTA_SMG/ADM_AREA.shp')
smg.head()
```
![image](https://user-images.githubusercontent.com/43196730/125896029-73a7a3f4-c3a7-4279-aa13-0ba113840fbc.png)
You can see the attribute table from the data

If you want to display the data you can use this to plot
```
smg.plot(figsize=(10, 10))
```
![image](https://user-images.githubusercontent.com/43196730/125896139-9565bae5-9a88-4c29-b3b6-bebf09a3bb03.png)


### Writing Geometry Data
You can write/draw your own geometry data with this
```
from shapely.geometry import Polygon

poly = geopandas.GeoSeries([Polygon([(0,0), (2,0), (2,2), (0,2)]),
                              Polygon([(2,2), (4,2), (4,4), (2,4)])])
data = geopandas.GeoDataFrame({'geometry': poly, 'data':[1,2]})
data.plot(figsize=(10, 10))
```
This will write and plot geometry data you just created.
You can save/write your data into files with this:
```
#For Esri Shapefile format
data.to_file("square.shp")
#For GeoJSON format
data.to_file("square.geojson", driver='GeoJSON')
#For Geopackage format
data.to_file("square.gpkg", driver="GPKG")
```
