# Plotting Data Spasial dengan Rentangan Nilai
Peta merupakan sebuah media untuk menyampaikan informasi mengenai lokasi di permukaan bumi beserta data pelengkapnya. 
Pada tahap ini kita akan belajar tentang plotting data spasial dan data sekunder mengenai informasi suatu wilayah. Pada contoh kali ini kita akan menggunakan data shapefile Kota Semarang beserta data jumlah populasi pada setiap kecamatan (bukan data asli).
Import data shapefile Kota Semarang dari link google drive berikut:
<pre><code>!gdown https://drive.google.com/u/2/uc?id=1XcPEdwSWysU5PWy2NnFca7QWqQkoMBPC&export=download
!unzip KOTA_SMG.zip
smg = gpd.read_file("KOTA_SMG/ADM_AREA.shp")
smg.head()
</code></pre>
Setelah itu kemudian akan muncul tabel isi dari shp Kota Semarang.
Dapat dilihat kemudian muncul tabel atribut di mana belum terdapat data populasi tiap kecamatan. Download data populasi dari link berikut
<pre><code>!gdown https://drive.google.com/u/2/uc?id=1v-ChS7wT8QtRY5pqVO8IOqVuhN6z3JCg&export=download
district_pop = pd.read_csv("/content/population.csv")
district_pop.head()
</code></pre>
Kemudian data csv tersebut (district_pop) digabungkan dengan data spasial wilayah Kota Semarang (smg), data gabungan tersebut misalkan disebut dengan pop_district dengan kolom yang sama yaitu kolom kecamatan (WADMKC).
<pre><code>pop_district = smg.merge(district_pop, left_on="WADMKC", right_on="WADMKC")
pop_district.head()
</code></pre>
Setelah itu dapat dilihat tabel atribut yang telah bergabung.
![image](https://user-images.githubusercontent.com/43196730/124479232-44138c80-ddd0-11eb-8dc3-27955eadfc39.png)
Maka data spasial telah memiliki data jumlah populasi di dalamnya. Untuk plotting data dapat dengan perintah berikut
Dengan matplotlib
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

Dengan menggunakan geoplot

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

Selamat mencoba!
Happy mapping :)
