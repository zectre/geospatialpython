# Memperkenalkan Google Colab
Google Colaboratory atau yang biasa disebut Colab merupakan layanan komputasi awan milik Google yang mampu digunakan untuk menulis dan mengeksekusi perintah dengan bahasa Python pada browser yang digunakan. Keunggulan dari layanan ini adalah:

1. Tidak perlu melakukan konfigurasi untuk mempersiapkan environment yang akan digunakan pada project anda.

2. Memiliki akses untuk menggunakan hardware milik Google. Teknologi coud computing memungkinkan anda untuk mengeksekusi perintah dengan hardware dari penyedia layanan, dalam hal ini Google memberikan pilihan untuk menggunakan GPU ataupun tanpa GPU pada layanannya.

3. Memiliki akses untuk sharing notebook dengan orang lain, sehingga dapat mengerjakan project secara bersama-sama dan membagikannya kepada orang lain untuk digunakan secara langsung.

Oke langsung saja kita coba akses melalui link [https://colab.research.google.com](https://colab.research.google.com)
![colab](https://user-images.githubusercontent.com/43196730/124387101-6db4b100-dd07-11eb-8512-dcb17ffe0ef3.PNG)

Terdapat pilihan untuk mengakses notebook yang telah dibuat sebelumnya maupun untuk membuat notebook baru. Misal kita akan membuat notebook baru maka klik new notebook. Setelah itu klik tombol connect pada sebelah kanan atas sampai terdapat status connected lalu akan muncul indikator RAM dan ukuran disk yang tersisa.
![start](https://user-images.githubusercontent.com/43196730/124387214-d8fe8300-dd07-11eb-93c4-6efba65bb252.PNG)

Google Colab juga menyediakan pilihan untuk mengakses file cloud melalui Google Drive pada panel sebelah kiri. Klik pada gambar folder drive lalu akan muncul autentikasi akun anda. Hal ini sangat berguna jika anda memiliki data yang akan diakses secara cloud dikarenakan layanan Colab ini hanya bisa diakses selama 12 jam pada satu sesi. Untuk mengubah tipe runtime menggunakan GPU atau tidak dapat melalui RUntime > Change Runtime Type lalu pilih GPU sebagai hardware accelerator.
![gpu](https://user-images.githubusercontent.com/43196730/124387231-e87dcc00-dd07-11eb-9c91-15a326471fce.PNG)

Mulai masukan perintah melalui tombol + Code atau bisa dengan shortcut Ctrl+M B. masukan perintah pada kolom code. Seperti pada contoh ini perintah untuk mengetahui versi Python yang digunakan serta lokasi direktori saat itu. Colab menggunakan Linux untuk OS mesinnya, jika ingin menggunakan perintah dasar Linux dapat dengan menambahkan tanda ! pada awal perintah. Jalankan kolom code dengan klik tombol run atau dengan shortcut Ctrl+Enter
![tst](https://user-images.githubusercontent.com/43196730/124387250-f7647e80-dd07-11eb-8594-558a9875d971.PNG)

Selamat mencoba :)
