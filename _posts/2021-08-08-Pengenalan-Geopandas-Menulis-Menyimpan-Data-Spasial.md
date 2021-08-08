# Menulis dan Menyimpan Data Spasial dengan Geopandas
Geopandas merupakan tools python yang berguna untuk manipulasi data spasial. Geopandas dapat memproses banyak format data spasial seperti Shapefile Esri, Geopackage QGIS, serta GeoJSON. Pada kali ini kita coba dengan contoh data vektor Kota Semarang dengan format shapefile.
Download contoh data:
```
!gdown https://drive.google.com/u/2/uc?id=1XcPEdwSWysU5PWy2NnFca7QWqQkoMBPC&export=download
!unzip KOTA_SMG.zip
```
Untuk install geopandas, dapat menggunakan pip dengan command pip install geopandas

## Import dan Membaca Data Spasial
Kita dapat melakukan import spasial data dengan geopandas menggunakan geopandas.read_file('data') misal data shp Semarang kita sebut dengan smg. Kita juga dapat melihat isi tabel atributnya.
```
import geopandas
smg = geopandas.read_file('/content/KOTA_SMG/ADM_AREA.shp')
smg.head()
```
![image](https://user-images.githubusercontent.com/43196730/125896029-73a7a3f4-c3a7-4279-aa13-0ba113840fbc.png)

Untuk melihat tampilan data dapat kita lakukan plotting dengan cara berikut:
```
smg.plot(figsize=(10, 10))
```
![image](https://user-images.githubusercontent.com/43196730/125896139-9565bae5-9a88-4c29-b3b6-bebf09a3bb03.png)

## Menulis/Menyimpan Data
Anda dapat menyimpan data geometri yang telah dibuat, misalkan kita akan membuat data geometri seperti berikuit:
```
from shapely.geometry import Polygon

poly = geopandas.GeoSeries([Polygon([(0,0), (2,0), (2,2), (0,2)]),
                              Polygon([(2,2), (4,2), (4,4), (2,4)])])
data = geopandas.GeoDataFrame({'geometry': poly, 'data':[1,2]})
data.plot(figsize=(10, 10))
```
Tampilan data yang kita buat misalkan seperti di atas, lalu kita dapat menyimpannya ke dalam beberapa format data spasial seperti berikut:
```
#For Esri Shapefile format
data.to_file("square.shp")
#For GeoJSON format
data.to_file("square.geojson", driver='GeoJSON')
#For Geopackage format
data.to_file("square.gpkg", driver="GPKG")
```
