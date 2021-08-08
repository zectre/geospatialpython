# Menghitung Nilai NDVI dengan Rasterio
Perhitungan band pada data raster dapat kita lakukan dengan rasterio dan numpy yang merupakan package Python yang sangat berguna dalam pengolahan raster. Fokus kali ini adalah menghitung nilai NDVI menggunakan band red dan NIR pada citra Landsat 8.
Download dan ekstrak data landsat 8 untuk contoh kali ini:
```
!gdown https://drive.google.com/u/2/uc?id=1ip32qmA_Vp60lVGl2IsIlEyu8YFWIkON&export=download
!tar -xvf /content/LC08_L1TP_119065_20210607_20210614_01_T1.tar
```
Install package python yang kita perlukan
```
!pip install earthpy
!pip install rasterio
```
Import package
```
import os
import numpy as np
import matplotlib.pyplot as plt
import rasterio as rio
from rasterio.plot import show
from rasterio.plot import show_hist
from shapely.geometry import Polygon, mapping
import earthpy as et
import earthpy.spatial as es
import earthpy.plot as ep

from matplotlib.colors import ListedColormap
import matplotlib.colors as colors
```
Buka raster band 4 dan 5 dengan rasterio
```
import rasterio
b4 = rasterio.open('/content/LC08_L1TP_119065_20210607_20210614_01_T1_B4.TIF').read(1)
b5 = rasterio.open('/content/LC08_L1TP_119065_20210607_20210614_01_T1_B5.TIF').read(1)
red = b4.astype('float64')
nir = b5.astype('float64')
```
Hitung nilai NDVI dengan rumus seperti biasa:
```
ndvi=np.where(
    (nir+red)==0., #It will return 0 for No Data value
    0, 
    (nir-red)/(nir+red)
```
Menyimpan hasil perhitungan tersebut ke dalam format geotiff sesuai dengan data asli landsat
```
b4data = rasterio.open('/content/LC08_L1TP_119065_20210607_20210614_01_T1_B4.TIF')
ndviTiff = rasterio.open('/content/ndvi.tiff','w',driver='Gtiff',
                          width = b4data.width, 
                          height = b4data.height, 
                          count=1, crs=b4data.crs, 
                          transform=b4data.transform, 
                          dtype='float64')
ndviTiff.write(ndvi,1)
ndviTiff.close()
```
Kita coba lihat hasilnya dengan plotting menggunakan cara berikut:
```
ndviplot = rasterio.open('/content/ndvi.tiff').read(1)
ep.plot_bands(ndviplot,
              cmap='RdYlGn',
              title="NDVI")
plt.show()
```
![image](https://user-images.githubusercontent.com/43196730/128625313-fdfd7ab5-644c-4c98-a07d-ce5d1aa7ce21.png)

Selamat mencoba! 
