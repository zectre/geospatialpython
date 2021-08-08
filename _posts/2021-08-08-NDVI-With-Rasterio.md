This time we will use band calculation with rasterio and numpy. Our main focus is determine the NDVI value using red and NIR band on Landsat 8 Imagery.
Download and extract Landsat 8 data for this tutorial:
```
!gdown https://drive.google.com/u/2/uc?id=1ip32qmA_Vp60lVGl2IsIlEyu8YFWIkON&export=download
!tar -xvf /content/LC08_L1TP_119065_20210607_20210614_01_T1.tar
```
Install rasterio and earthpy for plotting
```
!pip install earthpy
!pip install rasterio
```
Import packages
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
Open raster band 4 and 5
```
import rasterio
b4 = rasterio.open('/content/LC08_L1TP_119065_20210607_20210614_01_T1_B4.TIF').read(1)
b5 = rasterio.open('/content/LC08_L1TP_119065_20210607_20210614_01_T1_B5.TIF').read(1)
red = b4.astype('float64')
nir = b5.astype('float64')
```
Calculate NDVI value:
```
ndvi=np.where(
    (nir+red)==0., #It will return 0 for No Data value
    0, 
    (nir-red)/(nir+red))
```
Saving to Geotiff with format match with the original data
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
Try to ploy the result
```
ndviplot = rasterio.open('/content/ndvi.tiff').read(1)
ep.plot_bands(ndviplot,
              cmap='RdYlGn',
              title="NDVI")
plt.show()
```
![image](https://user-images.githubusercontent.com/43196730/128625313-fdfd7ab5-644c-4c98-a07d-ce5d1aa7ce21.png)

This will plot NDVI result with legend value bar.


