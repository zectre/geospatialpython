# Plotting Geospatial Data with Python
This time we will learn about plotting geospatial data with Python

Importing data (shapefile)
On this example we import geospatial data with shapefile format for area of Semarang City. Shp data that I already uploaded can be downloaded with this command
<pre><code>!gdown https://drive.google.com/u/2/uc?id=1XcPEdwSWysU5PWy2NnFca7QWqQkoMBPC&export=download
!unzip KOTA_SMG.zip
</code></pre>

To import the data you can run this command
<pre><code>smg = gpd.read_file("KOTA_SMG/ADM_AREA.shp")
smg.head()
</code></pre>
Next it will show the attribute table from that data
![image](https://user-images.githubusercontent.com/43196730/124477542-5260a900-ddce-11eb-8216-f3fa25add80c.png)

## Plotting Shp Data
To plot shp data you can use this command
<pre><code>gplt.polyplot(smg) #your data
plt.title('Semarang City') #map title
plt.axis('on') #on/off axis
</code></pre>
The plotting result will show map title as written in plt.title and show x and y axis with turning on plt.axis
![image](https://user-images.githubusercontent.com/43196730/124477652-745a2b80-ddce-11eb-81ed-a1f235249704.png)

## Plotting Certain Area
The steps above you can plot the whole area from the data. But what if you only want to plot certain data, like only a district from a city?. In this example we will try to plot Gajahmungkur district only. We can make example Gajahmungkur district as gjh, so we can type: 
<pre><code>gjh=smg[smg.WADMKC=="Gajah Mungkur"].plot() #WADMKC is column from the table that contains district names
gjh.plot
</code></pre>
It will show only Gajah Mungkur district.

![image](https://user-images.githubusercontent.com/43196730/124477873-bc794e00-ddce-11eb-95a7-a676a10af715.png)


Happy plotting :)
