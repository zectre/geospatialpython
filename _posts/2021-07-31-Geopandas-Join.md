## Geopandas Join 
While using geopandas you are processing a lot of spatial data. There are many spatial data and you need to manipulate it for your own purpose of your projects. You can join between spatial datas into one. With geopandas you are able to join by using spatial location and by attribute.
Before try this thing you need to install geopandas with its dependencies first.
```
!pip install pandas fiona shapely pyproj rtree geopandas
```
Download the Semarang City dataset:
```
!gdown https://drive.google.com/u/2/uc?id=1XcPEdwSWysU5PWy2NnFca7QWqQkoMBPC&export=download
!unzip KOTA_SMG.zip
!gdown https://drive.google.com/u/2/uc?id=1v-ChS7wT8QtRY5pqVO8IOqVuhN6z3JCg&export=download
```

You can import and view the table from data by this
```
import geopandas as gpd
import pandas as pd
smg = gpd.read_file("KOTA_SMG/ADM_AREA.shp") #semarang city shp
smg.head()
subdistrict_pop = pd.read_csv("/content/population.csv")
subdistrict_pop.head()
```
### Join by Attribute
In this case we have population data for each subdistrict in Semarang. We will join the spatial data (smg) with population data (subdistrict_pop) so we can have population information inside the spatial data. You can join with merge feature.
```
pop_subdistrict = smg.merge(subdistrict_pop, on="WADMKC") #this will merge features based on column WADMKC
pop_subdistrict.head()
```
It will have populasi data from population csv data.
### Join by Spatial Location
For this we will add subdistrict name into hospital spatial data from Semarang City data. Those data are not in the same CRS so we need to change it first.
```
hospital=gpd.read_file('KOTA_SMG/RUMAHSAKIT_PT_25K.shp')
hospital.head()
hosp=hospital.to_crs("EPSG:4326")
hospital_loc = gpd.sjoin(hosp, smg, how='inner', op='intersects')
hospital_loc.head()
```
For spatial join, in geopandas you can set how= with 'inner', 'left', or 'right' so it will look based on the features from left and right data, and op for operation. You can set op with 'intersects', 'contains', 'within', 'touches', 'crosses', and 'overlaps'
