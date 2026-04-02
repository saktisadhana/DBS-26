> Nama: Putu Putra Sakti Sadhana
> NRP: 5027251101
> Kode Asisten: SEL
> Soal 3
# Brief Overview
Menurut saya sesuai dengan study case soal, sistem *database* yang diperlukan memiliki 7 entitas, yaitu:
- Peserta
- Kelas
- Transaksi_Pendaftaran
- Mentor
- Kit_Produksi
- Kit_Bahan 
- Bahan_Baku  
<div class="page-break" style="page-break-before: always;"></div>

---
# Database System
![[Diagram DBS Q3.svg]]
## Peserta
### Penjelasan
Entitas peserta memiliki *primary key* `ID_Peserta` dengan atribut-atribut:

- Nama_Peserta
- Kontak_Peserta, &
- Alamat_Peserta

Hal ini memenuhi perintah soal yang dimana sistem *database* harus "mencatat data Peserta (seperti nama, kontak, dan alamat)". Sesuai juga dengan perintah soal, entitas ini akan berelasi *many to many* dengan entitas `Kelas` namun itu menyababkan terbentuknya sebuah tabel penghubung yang bernama `Transaksi_Pendaftaran`.

> "Karena satu kelas bisa diikuti oleh banyak peserta dan satu peserta bisa mengambil lebih dari satu kelas, Obibi menyadari perlu adanya pencatatan Transaksi Pendaftaran yang rapi."

### Contoh Penerapan Entitas

| ID_Peserta  | Nama_Peserta    | Kontak_Peserta | Alamat_Peserta |
| :---------- | :-------------- | :------------- | :------------- |
| PE001030926 | Widodo Subionto | ...            | Surakarta      |
| PE002030926 | Hachiware Saktu | ...            | Trenggalek     |
| PE001031026 | Naila Sadhana   | ...            | Bali           |
| ...         | ...             | ..             | ..             |

Pada tabel di atas saya memilih untuk mengosongkan Kontak_Peserta karena tidak dispesifikan tipe data dari atribut tersebut dan karena menurut saya `Kontak_Peserta` bisa berkisar dari alamat email hinnga nomer telepon.

Pada tabel contoh penerapan dari entitas `Peserta` saya juga memberikan ide terhadap sistem ID yang dapat digunakan untuk entitas `Peserta` & `Transaksi_Pendaftaran` pada sistem database sesuai dengan soal.

| Nama Entitas | Urutan Hari Itu | Bulan | Hari | Tahun |
| :----------- | :-------------- | :---- | :--- | :---- |
| PE           | 001             | 03    | 09   | 26    |
| ...          | ...             | ...   | ...  | ...   |

Dan mungkin untuk entitas `Kelas`, `Mentor`, & `Kit Produksi` dapat menggunakan sistem ID seperti berikut:

| Nama Entitas | Unique Number |
| ------------ | ------------- |
| ME           | 001           |
| KE           | 038           |
| KP           | 067           |

> [!info] Info Nama Entitas
> ME = `Mentor`
> KE = `Kelas`
> KP = `Kit-Produksi`

### Relasi Entitas

Sesuai dengan yang telah saya jelaskan entitas ini berelasi one to many terhadap entitas `Transaksi_Pendaftaran` karena relasi entitas `Peserta` dengan entitas `Kelas` yang *many to many* menyebabkan harus terbentuk suatu *junction table* yaitu `Transaksi_Pendaftaran`.

## Transaksi_Pendaftaran
### Penjelasan
Sesuai dengan perintah soal yang dimana karena relasi entitas `Peserta` dengan `Kelas` adalah *many to many*, harus terdapat tabel penghubung yang bernama `Transaksi_Pendaftaran`. Pada tabel ini saya memilih untuk membuat primary key dengan nama `ID_Transaksi_Pendaftaran`, dan dengan atribut:

- ID_Peserta
- ID_Kelas, &
- Metode Transaksi

> [!info] Info Atribut Entitas `Transaksi_Pendaftaran`
> ID_Transaksi_Pendaftaran = *Primary Key*
> ID_Peserta = *Foreign Key*
> ID_Kelas = *Foreign Key*
> Metode Transaksi = Atribut

bisa dilihat pada diagram diatas terdapat dua *foreign key*: `ID_Peserta` yang berasal dari entitas `Peserta`, & `ID_Kelas` yang bersal dari entitas `Kelas`. Kedua *foreign key* tersebut menurut saya merupakan atribut yang diperlukan oleh entitas ini agar bisa digunakan sesuai dengan tugasnya untuk menjadi tabel penghubung.

Untuk alasan mengapa saya memilih ID (*Primary key* dari kedua entitas tersebut) sebagai *foreign key* dibanding atribut lainnya seperti `Nama_Peserta` atau `Kategori_Kelas`, karena dapat terhindar dari masalah duplikasi seperti berikut:

### Contoh Penerapan Entitas

| ID_Transaksi_Pendaftaran | Nama_Peserta | ID_Kelas | Metode_Transaksi |
| ------------------------ | ------------ | -------- | ---------------- |
| TP001030926              | Sutr         | KE_001   | Transfer         |
| TP002030926              | Sutr         | KE_002   | Transfer         |
| ..                       | ..           | ..       | ..               |

Sistem tidak akan mengetahui apakah ini adalah orang sama yang memilih untuk mengikuti dua kelas, atau dua orang yang berbeda dengan nama yang sama.

Mengetahui itu jika kita membuat `ID_Peserta` sebagai *foreign key* kita dapat mevisualisasikan entitas seperti ini:

| ID_Transaksi_Pendaftaran | ID_Peserta  | ID_Kelas | Metode_Transaksi |
| ------------------------ | ----------- | -------- | ---------------- |
| TP001030926              | PE001030926 | KE_001   | Transfer         |
| TP002030926              | PE002030926 | KE_002   | Transfer         |
| ..                       | ...         | ..       | ..               |

 Dengan perubahan itu sistem *database* akan mengetahui perbedaan antara kedua orang tersebut karena entitas menggunakan `ID_Peserta` suatu atribut yang lebih unik dibanding `Nama_Peserta`.

### Relasi Entitas

Karena relasi dari entitas `Peserta` dengan entitas `Kelas` adalah *many to many*, kita bisa membuat sebuah tabel penghubung untuk menghindari itu. Sesuai dengan perintah soal entitas tabel tersebut adalah `Transaksi_Pendaftaran`.

Setelah terbentuknya entitas tersebut akan terbentuk relasi dengan `Peserta` yang merupakan *one to many* & dengan `Kelas` yang merupakan *many to one*.

## Kelas
### Penjelasan
Sesuai dengan instruksi yang diberikan soal, sistem *database* harus mendata "berbagai jenis Kelas yang ditawarkan (misalnya: Kelas Pemula, Kelas Pro, atau Kelas Mewarnai)","Mentor yang bertugas mengajar.", & "Kit Produksi (bahan baku) yang harus dimiliki peserta untuk setiap kelas tertentu.".

Seperti yang telah saya cantumkan, primary key dari entitas ini adalah `ID_Kelas`, dengan atribut-atribut:
- ID_Kit-Produksi
- ID_Mentor, &
- Kategori_Kelas

Entitas ini memiliki dua *foreign key* yang merupakan `ID_Kit-Produksi` sebagai *primary key* entitas `Kit Produksi` dan `ID_Mentor` yang merupakan *primary key* entitas `Mentor`. Alasan mengapa saya memilih kedua *primary key* melainkan atribut seperti `Nama_Mentor`juga untuk menghindari masalah duplikasi.

### Contoh Penerapan Entitas

| ID_Kelas | ID_Kit-Produksi | ID_Mentor | Kategori_Kelas |
| -------- | --------------- | --------- | -------------- |
| KE_001   | KP_001          | ME_001    | Kelas Pro      |
| KE_002   | KP_002          | ME_002    | Kelas Mewarnai |
| KE_003   | KP_002          | ME_002    | Kelas Mewarnai |
| ...      | ...             | ...       | ...            |

Dapat dilihat gambaran dari penerapan entitas `Kelas` dalam sistem database. Dengan adanya ID_Kelas sebagai *primary key* sistem tidak akan kebingungan akan membedakan jika terdapat dua kelas dengan kategori yang sama.

### Relasi Entitas

Entitas ini berelasi *one to many* terhadap entitas `Transaksi_Pendaftaran` karena relasi entitas `Peserta` dengan entitas `Kelas` yang *many to many* menyebabkan terbentuknya suatu *junction table* yaitu `Transaksi_Pendaftaran`.

## Mentor
### Penjelasan
Sesuai dengan perintah soal, sistem harus mendata "Mentor yang bertugas mengajar.". Disini saya memilih untuk membuat `Mentor` menjadi suatu entitas yang dimana masing masing mentor memiliki ID Unik yang dapat membedakan mentor dengan nama yang sama.

### Contoh Penerapan Entitas

Jika `Mentor` hanya sebuah atribut dalam entitas kelas, terdapat kemungkinan terjadinya masalah duplikasi seperti ini:

| ID_Kelas | ID_Kit-Produksi | Nama_Mentor | Kategori_Kelas |
| -------- | --------------- | ----------- | -------------- |
| KE_001   | KP_001          | Budi        | Kelas Pro      |
| KE_002   | KP_002          | Budi        | Kelas Mewarnai |
| KE_003   | KP_002          | Susionto    | Kelas Mewarnai |

Sesaat sistem ingin mencari berapa banyak kelas yang telah diambil oleh mentor `Budi`, sistem tidak akan bisa membedakan kedua `Budi` tersebut. Padahal kedua `Budi` teresebut berasal dari dua daerah yang beda!

Nah, dengan adanya pemisahan `Mentor` untuk menjadi entitasnya sendiri, skenario tersebut tidak akan bisa terjadi! Bayangkan:

| ID_Mentor | Nama_Mentor              |
| --------- | ------------------------ |
| ME_001    | Budi < Dari Trenggalek   |
| ME_002    | Budi < Dari Tulungaggung |
| ..        | ..                       |
| ME_054    | Usagi                    |

Kedua mentor tersebut yang memiliki nama yang sama akan bisa dibedakan oleh sistem dengan gampang.

### Relasi Entitas

Entitas ini berelasi one to many terhadap entitas `Kelas` karena walau tidak disebutkan secara eksplisit dalam soal, saya menganggap `Mentor` dapat mengambil lebih dari satu kelas .

## Kit Produksi
### Penjelasan
Sesuai dengan kasus soal, sistem juga harus bisa mendata `Kit Produksi` yang diperlukan setiap `Kelas`. Mengetahui itu saya memilih untuk membuat sebuah entitas dengan nama yang sama karena `Kit_Produksi` bisa saja terdiri dari dua atau lebih `Bahan Baku`. Bayangkan:

### Contoh Penerapan Entitas

| ID_Kelas | Kit-Produksi | Kategori_Kelas |
| -------- | ------------ | -------------- |
| KE_001   | Spons        | Kelas Pro      |
| KE_001   | Gabus        | Kelas Pro      |
| KE_001   | Bambu        | Kelas Pro      |
| KE_001   | Cat          | Kelas Pro      |
| KE_002   | Cat          | Kelas Mewarnai |
| ...      | ...          | ...            |

Jika `Kit-Produksi` hanya suatu atribut dari entitas `Kelas`, maka tabel dari entitas tersebut akan terpenuhi dengan clutter yang pasti mengakibatkan redundansi data.

Dengan adanya entitas `Kit-Produksi` seperti ini:

| ID_Kit-Produksi | Nama_Kit-Produksi  |
| --------------- | ------------------ |
| KP_001          | Kit_Kelas-Pro      |
| KP_002          | Kit_Kelas-Mewarnai |
| ...             | ...                |

Tidak akan terjadi redundansi data karena sistem *database* sudah dapat mengetahui perbedaan dari `Kit-Produksi` yang diperlukan suatu kelas. Salah satu contoh case yang cocok adalah saat terdapat dua kelas yang memerlukan kit yang sama, sistem tidak akan mencatat nilai yang sama. Bayangkan:

| ID_Kelas | ID_Kit-Produksi | Kategori_Kelas |
| -------- | --------------- | -------------- |
| KE_001   | KP_001          | Kelas Pro      |
| KE_002   | KP_001          | Kelas Pro      |
| KE_003   | KP_002          | Kelas Mewarnai |

Sebelumnya, jika `Kit-Produksi` hanyalah suatu atribut biasa dalam entitas `Kelas`, sistem akan terpaksa menyimpan nama bahan secara langsung dan berulang.

Selain itu, sesuai dengan premis yang telah saya ciptakan, dimana suatu `Kit-Produksi` dapat terdiri dari beberapa `Bahan-Baku` dan juga sebaliknya diamana suatu `Bahan-Baku` dapat muncul di beberapa `Kit-Produksi`, harus terdapat suatu tabel penghubung.

### Relasi Entitas

Entitas ini berelasi *one to many* terhadap entitas `Kelas` karena walau dalam soal tidak disebutkan secara eksplisit, saya mengambil asumpsi bahwa suatu `Kit-Produksi` dapat diperlukan oleh lebih dari satu `Kelas` tetapi bukan sebaliknya yang dimana terdapat suatu kelas yang memperlukan lebih dari satu `Kit-Produksi`.

Bisa dilihat juga, karena relasi entitas `Kit-Produksi` dengan `Bahan-Baku` yang *many to many* , harus diperlukan suatu tabel penghubung, dan disini relasi `Kit-Produksi` dengan tabel penghubung tersebut (`Kit_Bahan`) adalah *one to many*.

## Kit_Bahan
### Penjelasan
Karena relasi antara `Kit-Produksi` dengan `Bahan-Baku` yang many to many, harus terdapat sebuah tabel penghubung, dan disini saya memilih untuk menciptakan suatu entitas dengan nama tabel `Kit_Bahan`.

### Contoh Penerapan Entitas

| ID_Kit_Bahan | ID_Kit-Produksi | ID_Bahan-Baku |
| ------------ | --------------- | ------------- |
| KB001        | KP_001          | BB001         |
| KB002        | KP_001          | BB002         |
| KB003        | KP_002          | BB001         |
### Relasi Entitas
Dengan entitas `Kit-Produksi` & `Bahan-Baku`, entitas ini memiliki relasi *many to one*.

## Bahan Baku

### Penjelasan
Berdasarkan asumsi saya yang dimana suatu `Kit_Produksi` dapat memilki lebih dari satu `Bahan-Baku`, entitas ini harus memiliki table seperti:

### Contoh Penerapan Entitas

| ID_Bahan-Baku | Nama_Bahan-Baku |
| ------------- | --------------- |
| BB001         | Cat             |
| BB002         | Spons           |
| ...           | ...             |

Dengan ini jika terdapat sebuah `Bahan-Baku` yang diperlukan oleh dua `Kit-Produksi` sistem tidak akan mencatat `Bahan-Baku` tersebut dua kali melainkan hanya ID unik bahan tersebut. Menghilangkan kemungkinan terjadinya redudansi.

### Relasi Entitas
Dengan entitas `Kit_Bahan`, entitas ini memiliki relasi *one to many*.
