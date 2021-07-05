# Plotting Data Spasial dengan Python
Kali ini kita akan membahas mengenai plotting data geospasial dengan python
Importing data shapefile
Misal kita akan mencoba untuk import data spasial berformat shapefile untuk wilayah Kota Semarang. File shp Kota Semarang dapat diunduh dengan cara berikut
<pre><code>!gdown https://drive.google.com/u/2/uc?id=1XcPEdwSWysU5PWy2NnFca7QWqQkoMBPC&export=download
!unzip KOTA_SMG.zip
</code></pre>

Untuk melakukan import dengan menggunakan perintah 
<pre><code>smg = gpd.read_file("KOTA_SMG/ADM_AREA.shp")
smg.head()
</code></pre>
Setelah itu akan tampak tabel atribut dari data spasial tersebut.
![image](https://user-images.githubusercontent.com/43196730/124477542-5260a900-ddce-11eb-8216-f3fa25add80c.png)

## Plotting Data Shp
Untuk melakukan plotting menggunakan geoplot bisa dengan perintah ini
<pre><code>gplt.polyplot(smg) #sesuai dengan data yg akan diplot
plt.title('Semarang City') #judul peta
plt.axis('on') #on/off sumbu x dan y
</code></pre>
Hasil plotting akan memunculkan judul sesuai plt.title serta memunculkan sumbi x dan y dengan menyalakan plt.axis
![image](https://user-images.githubusercontent.com/43196730/124477652-745a2b80-ddce-11eb-81ed-a1f235249704.png)

## Plotting daerah tertentu
Misalkan dari daerah Kota Semarang kita ingin melakukan plot hanya wilayah Kecamatan Gajahmungkur. Di sini kita misalkan Kecamatan Gajahmungkur adalah gjh maka: 
<pre><code>gjh=smg[smg.WADMKC=="Gajah Mungkur"].plot() #WADMKC adalah kolom data kecamatan
Gjh.plot
</code></pre>
Kemudian akan muncul hasil plotting untuk wilayah Kecamatan Gajahmungkur saja

![image](https://user-images.githubusercontent.com/43196730/124477873-bc794e00-ddce-11eb-95a7-a676a10af715.png)


Happy plotting :)
