# Plotting Spatial Data with Its Value 
Map is a media to give information about location in earth surface with the data on it.
From this step we will learn about plotting spatial data that have values inside it and plot the choropleth map. In this example we will use shapefile data from Semarang City and csv data of population data each district (not real data).
Import shapefile data:
<pre><code>!gdown https://drive.google.com/u/2/uc?id=1XcPEdwSWysU5PWy2NnFca7QWqQkoMBPC&export=download
!unzip KOTA_SMG.zip
smg = gpd.read_file("KOTA_SMG/ADM_AREA.shp")
smg.head()
</code></pre>
Next it will show the table from shapefile data Semarang City.
We can see the attribute table but it doesn't have population data inside. We can download population dara here:
<pre><code>!gdown https://drive.google.com/u/2/uc?id=1v-ChS7wT8QtRY5pqVO8IOqVuhN6z3JCg&export=download
district_pop = pd.read_csv("/content/population.csv")
district_pop.head()
</code></pre>
The csv data (district_pop) combines with spatial data (smg), the merger of the data we name it as pop_district with using same column (WADMKC)
<pre><code>pop_district = smg.merge(district_pop, left_on="WADMKC", right_on="WADMKC")
pop_district.head()
</code></pre>
The merged table will be like this
![image](https://user-images.githubusercontent.com/43196730/124479232-44138c80-ddd0-11eb-8dc3-27955eadfc39.png)
So the spatial data now contains population data inside. Plotting this data you can use this command:
Using matplotlibL
<pre><code>feature = 'Populasi'
vmin, vmax = 0, 30000   #min max bar
fig, ax = plt.subplots(1, figsize=(20, 12))
pop_district.plot(column=feature, cmap='Greens', linewidth=0.8, ax=ax, edgecolor='0.8')
ax.set_title('Population in Semarang for each Districts') #INPUT YOUR TITLE
ax.axis('on')
sm = plt.cm.ScalarMappable(cmap='Greens', norm=plt.Normalize(vmin=vmin, vmax=vmax))
sm._A = []
cbar = fig.colorbar(sm);
</code></pre>
![image](https://user-images.githubusercontent.com/43196730/124479377-67d6d280-ddd0-11eb-937f-8ad0d4bae93b.png)

Using geoplot:

<pre><code>import geoplot as gplt
import geoplot.crs as gcrs
import geopandas as gpd
gplt.choropleth(pop_district,
               hue='Populasi',
               cmap='Greens',
               legend=True,
               )
plt.title("Population in Semarang")
plt.axis('on')
</code></pre>

![image](https://user-images.githubusercontent.com/43196730/124479459-8210b080-ddd0-11eb-9015-883ca96481a6.png)

Happy mapping :)
