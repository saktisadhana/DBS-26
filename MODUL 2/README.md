# Laporan Praktikum Modul 2

## Indetitas Praktikan

|         **Nama**         |  **NRP**   | **Kode Asisten** | Kelas |
| :----------------------: | :--------: | :--------------: | :---: |
| Putu Putra Sakti Sadhana | 5027251101 |       SEL        |   A   |

---
## Reporting
### Raw Table

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Raw_Tabel.png)

Praktikan diberikan sebuah tabel yang bermaksud untuk mendata penyewaan studio milik "Musica Studio". Bisa dilihat pada kolom `Member_Band` dan juga `Alat_Tambahan` masih terdapat  _multivalued attributes_ (Atribut yang bernilai ganda). 

Sehingga diperlukan normalisasi data agar sistem dapat mengelola data secara baik secara lebih efisien, konsisten, dan terhindar dari anomali data.
### NF1

 Langkah pertama dalam normalisasi database (NF1) adalah dengan memisahkan atribut yang bernilai ganda menjadi _Atomic Value_ (Terpisah menjadi sel masing-masing)

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331220116.png)

Selain itu juga, tabel diatas memenuhi beberapa sifat dari hasil normalisasi pertama (NF1) yaitu:
1. Semua Nilai dalam Kolom Harus Bertipe Sama
	Hal ini bisa dilihat dari format tanggal dan Tarif yang sama. Tetapi ada perubahan kecil yang lakukan yaitu dengan memformatkan data dari atribut `Tarif_Ruang_Per_Jam` dengan menambahkan titik agar lebih bisa terbaca.
2. Setiap Kolom Harus Memiliki Nama yang Unik
	Bisa dilihat tidak ada kolom yang memiliki nama yang sama.
3. Urutan Data Tidak Penting
	Data diurutkan sesuai konsep **Teori Himpunan** (Forex: B005 tidak terletak pada awal baris)
### NF2

Setelah NF1 terdapat langkah selanjutnya yaitu NF2. Pada tahap ini, kita harus memastikan semua atribut non-key memiliki ketergantungan fungsional penuh terhadap Primary Key. Yang dimaksud dengan ketergantungan fungsional penuh adalah kondisi di mana suatu atribut sepenuhnya bergantung pada seluruh bagian dari _Primary Key_, dan bukan hanya pada sebagian dari Primary Key tersebut.

	TL;DR Menghilangkan atribut yang hanya bergatung partial terhadap primary key.


Karena itu kita dapat memisahkan dua atribut yaiu `Alat_Tambahan` dan `Member_Band` menjadi tabel nya masing masing.

#### Detailed Booking

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331233624.png)

`Alat_Tambahan` dipisah menjadi tabelnya sendiri karena atribut tersebut bernilai ganda dan menyebabkan `ID_Booking` ditulis berulang kali sehingga menghilangkan fungsinya sebagai Primary Key tunggal.
#### Detailed Band

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331221442.png)

Sama seperti `Alat_Tambahan` atribut ini dipisah agar `ID_Booking` tidak ditulis berulang kali yang menghilangkan fungsinya sebagai Primary Key tunggal.

#### Booking

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331220645.png)

Bisa dilihat tabel lebih rapi dan terstruktur hanya dengan menghilangkan atribut yang bergantungan parsial terhadap _Primary Key_

	TL;DR Menghilangkan atribut kedalam tabelnya masing masing agar PK Utama (`ID_Booking) tidak tertulis / terdata dua kali dalam tabelnya sendiri.

### NF3

Dalam langkah ini tabel harus menghilangkan seluruh atribut yang tidak berhubungan secara langsung dengan primary key (`ID_Booking`). Dengan melakukan itu tabel entitas `Booking` secara otomatis akan menghilangkan ketergantungan transitif.

Apa yang dimaksud dengan ketergantungan transitif? Secara singkat dengan menggunakan tabel sebagai contoh:
Dalam tabel `Booking` atribut `Tarif_Ruang_Per_Jam` hanya bergantungan / dipengaruhi oleh `Kategori_Ruang`. Karena itu menurut saya hasil akhir dari soal 3 akan terbentuk 7 tabel:

Selain itu saya memilih untuk memisah Alat musik menjadi tabelnya sendiri dan juga menciptakan atribut baru bernama `ID_Alat`. Karena menurut saya sebuah alat musik tentunya bisa digunakan berkali-kali lain hari (Menyebabkan relasi tabel entitas `Booking` dengan `Alat_Musik` many to many)
#### Staff

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331233114.png)
#### Band

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331233717.png)
#### Member_Band

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331233240.png)
#### Ruang

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331232716.png)
#### Alat

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331234321.png)
#### Alat_Booking

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331234417.png)
#### Booking

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Pasted%20image%2020260331234505.png)

---
## Entity Relationship Diagram

![image](https://raw.githubusercontent.com/saktisadhana/DBS-26/main/MODUL%202/Image%20Source/Modul2Prak.drawio.svg)

### Brief Overview

Sesuai dengan jumlah tabel setelah melakukan NF3 saya meciptakan ERD ini
### Entity Relations

#### Staff > Booking

One to Many karena satu staff bisa menangani banyak booking, tetapi booking hany bisa dihandle satu staff.

#### Band > Booking
One to Many karena satu Band bisa melakukan banyak booking, tetapi booking hanya untuk satu band.

#### Member_Band > Band
One to Oner or Many karena satu Member hanya bisa terdiri dari satu band, tetapi band bisa terdiri dari satu atau banyak orang

#### Ruang > Booking
One to Many

#### Alat > Alat_Booking
One to many

#### Alat_Booking > Booking
One to many

