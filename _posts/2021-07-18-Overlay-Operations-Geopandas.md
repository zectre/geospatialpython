## Overlay Operations with Geopandas
When processing spatial data you will find that you need more than one data. You can use spatial overlay operations to unite more than one data, substract the difference between two spatial location, and many more. 
This time we will use Semarang City districts with random spatial data next to the city.
You can download the dataset with this
```
!gdown https://drive.google.com/u/2/uc?id=1XcPEdwSWysU5PWy2NnFca7QWqQkoMBPC&export=download
!unzip KOTA_SMG.zip
!gdown https://drive.google.com/u/2/uc?id=1w38Et4lS55a7LkjkIDiaI1OHDIyWU9--&export=download
!unzip union.zip
```
We will use smg as Semarang City data and vector for random spatial data. Import the data and plot to see the display.
```
import geopandas
smg = geopandas.read_file('/content/KOTA_SMG/ADM_AREA.shp')
vector = geopandas.read_file('union.gpkg')

ax = smg.plot(figsize=(10,10))

vector.plot(ax=ax, color='green', alpha=0.5)
```
![image](https://user-images.githubusercontent.com/43196730/126060085-ced9a9cd-59ef-4780-a575-37cc389974bf.png)

Overlay operations in geopandas we will learn are intersection, union, symmetric_difference, difference, identity that we can use it by filling 'how' argument. We can also merge spatial features with same data field by using dissolve.

### Intersection
Intersection will get the result from the intersect location between spatial data. From this data this will get result from the intersection between Semarang City and vector data.
You can use this operation by using 'intersection' for how in geopandas.overlay.
```
import geopandas
intersect = geopandas.overlay(smg, vector, how='intersection')
intersect
ax = intersect.plot(figsize=(10,10))

smg.plot(ax=ax, facecolor='none', edgecolor='k');

vector.plot(ax=ax, facecolor='none', edgecolor='k');
```
![image](https://user-images.githubusercontent.com/43196730/126060207-7a7b3f5b-be31-43a6-a02f-1cdd6e9915f6.png)


### Union
Union operation will get the result from merging between spatial data. The result is area for Semarang City and vector data merged.
You can use this operation by using 'union' for how in geopandas.overlay.
```
union = geopandas.overlay(smg, vector, how='union')
union
ax = union.plot(figsize=(10,10))

smg.plot(ax=ax, facecolor='none', edgecolor='k');

vector.plot(ax=ax, facecolor='none', edgecolor='k');
```
![image](https://user-images.githubusercontent.com/43196730/126060243-8c8c6acf-8104-4dca-b8ea-e060e3999805.png)


### Symmetrical Difference
This operation will get the area for all inside the spatial data expect the intersection.
You can use this operation by using 'symmetric_difference' for how in geopandas.overlay.
```
sym_diff = geopandas.overlay(smg, vector, how='symmetric_difference')
sym_diff
ax = diff.plot(figsize=(10,10))

smg.plot(ax=ax, facecolor='none', edgecolor='k');
vector.plot(ax=ax, facecolor='none', edgecolor='k');
```
![image](https://user-images.githubusercontent.com/43196730/126060298-51d5f39f-e006-4705-bdff-e0c63e8f06e8.png)


### Difference
This operation will result the area for the first data without the overlay area between the first and second data.
You can use this operation by using 'difference' for how in geopandas.overlay.
```
diff = geopandas.overlay(smg, vector, how='difference')
diff
ax = diff.plot(figsize=(10,10))

smg.plot(ax=ax, facecolor='none', edgecolor='k');
vector.plot(ax=ax, facecolor='none', edgecolor='k');
```
![image](https://user-images.githubusercontent.com/43196730/126060301-7b5091fe-cc10-47c5-8098-7d67fdae4beb.png)

### Identity
This operation is often used for spatial data with more than one features inside. The result is the surface of data 1 but with geometries from overlaying data 1 and data 2
```
id = geopandas.overlay(smg, vector, how='identity')
id
ax = id.plot(figsize=(10,10))

smg.plot(ax=ax, facecolor='none', edgecolor='k');
vector.plot(ax=ax, facecolor='none', edgecolor='k');
```
![image](https://user-images.githubusercontent.com/43196730/126060371-c9a6f7c5-dfc5-4bbf-8529-e516698ec94c.png)


### Dissolve
This operation is not using argument 'how= ' with overlay operations in geopandas. Dissolve will merge features with same data on the selected field. For this example we will dissolve sub-districts into district. 
WADMKK contains sub-district names. We can dissolve it by using:
```
city = smg.dissolve(by='WADMKK')

city.plot();
city.head()
```
![image](https://user-images.githubusercontent.com/43196730/126060436-27f87485-e263-4589-bb1d-789d110a07ce.png)

The results are Semarang City and Kendal district.

