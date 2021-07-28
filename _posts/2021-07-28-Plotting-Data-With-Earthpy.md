## PLOTTING RASTER DATA WITH EARTHPY

### WHAT IS EARTHPY?
Earthpy is a python tool that makes it easier to plot/work with spatial data both raster and vector. In this tutorial we will try to plot RGB color composite from Landsat 8 imagery with vector boundary inside.

Download raster and vector data for this demo:
```
!gdown https://drive.google.com/u/2/uc?id=1ip32qmA_Vp60lVGl2IsIlEyu8YFWIkON&export=download
!tar -xvf /content/LC08_L1TP_119065_20210607_20210614_01_T1.tar
!gdown https://drive.google.com/u/0/uc?id=1bZ5NOqDCcuAvMHESVX4XOhJGFO66yKdm&export=download
!unrar x KAB_REMBANG.rar
```

Make sure you've installed earthpy, geopandas and rasterio for this time, you can use pip instead.
```
!pip install earthpy
!pip install geopandas
!pip install rasterio
```

Then import these packages
```
import os
from glob import glob
import matplotlib.pyplot as plt
import rasterio as rio
from rasterio.plot import plotting_extent
import geopandas as gpd
import earthpy as et
import earthpy.spatial as es
import earthpy.plot as ep
```

Next you can import Landsat data (for this demo we will only plot natural composite) band 2, 3, 4
```
# Get list of bands and sort by ascending band number
landsat_bands_data_path = "/content/LC08_L1TP_119065_20210607_20210614_01_T1_B*[2-4]*.TIF"
stack_band_paths = glob(landsat_bands_data_path)
stack_band_paths.sort()

# Create image stack and apply nodata value for Landsat
arr_st, meta = es.stack(stack_band_paths, nodata=-9999)
```
Using earthpy to plot the band composite by using band 2, 3, 4 landsat. We've ordered it ascending by band number so we use rgb=(2,1,0) because python start from 0
```
# Create figure with one plot
fig, ax = plt.subplots(figsize=(12, 12))

# Plot red, green, and blue bands, respectively
ep.plot_rgb(arr_st, rgb=(2, 1, 0), ax=ax, title="Landsat 8 RGB Image")
plt.show()
```
![image](https://user-images.githubusercontent.com/43196730/127327509-d37575a3-8aa0-480d-a15e-dc03bd7a31f5.png)


We need to stretch for clear image
```
# Create figure with one plot
fig, ax = plt.subplots(figsize=(12, 12))

# Plot bands with stretched applied
ep.plot_rgb(
    arr_st,
    rgb=(2, 1, 0),
    ax=ax,
    stretch=True,
    str_clip=0.5,
    title="Landsat 8 RGB Image Stretched",
)
plt.show()
```
![image](https://user-images.githubusercontent.com/43196730/127327541-4dee6587-581c-443d-bdf4-3271c13e1697.png)



Next we will try to plot the boundary vector data from Rembang Regency. We import it by using geopandas.
```
# Open polygon boundary using GeoPandas
bound = gpd.read_file('/content/REMBANG/ADMINISTRASIDESA_AR_25K.shp')

# Reproject boundary to match CRS of the Landsat images
with rio.open(stack_band_paths[0]) as raster_crs:
    raster_profile = raster_crs.profile
    bound_utm49S = bound.to_crs(raster_profile["crs"])
```
We will plot the image and vector boundary together
```
# Create raster extent for the plot
extent = plotting_extent(arr_st[0], raster_profile["transform"])

# Create figure with one plot
fig, ax = plt.subplots(figsize=(12, 12))

# Plot boundary with high zorder for contrast
bound_utm49S.boundary.plot(ax=ax, color="red", zorder=10)

# Plot CIR image using the raster extent
ep.plot_rgb(
    arr_st,
    rgb=(2, 1, 0),
    ax=ax,
    stretch=True,
    extent=extent,
    str_clip=0.5,
    title="Landsat 8 CIR Image with Rembang Regency Boundary",
)
plt.show()
```

![image](https://user-images.githubusercontent.com/43196730/127327561-ced128c6-1b68-41ea-aeb5-3fbdf1282f91.png)


Happy Plotting! :)
