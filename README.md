| Variable | Isi |
| -------- | --- |
| Nama | RADITYA TANSY LIZARA  |
| NIM | 312310454 |
| Kelas | TI.23.A5 |
| Mata Kuliah | Bahasa Pemrograman |

# Soal Latihan Praktikum
## Data Model Mapping
```
Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

Dosen (kd_ds, nama)

Matakuliah (kd_mk, nama, sks)

JadwalMengajar (kd_ds, kd_mk, hari, jam, ruang)

KRSMahasiswa (nim, kd_mk, kd_ds, semester, nilai)
```
- Buat DDL Script berdasarkan skema ERD tersebut diatas.
- Jalankan script DDL tersebut pada DBMS MySQL.
Langkah-langkahnya :

1. Buat dulu script untuk table Mahasiswa :
```
create table Mahasiswa (
    nim varchar(10) PRIMARY KEY,
    nama varchar(25) NOT NULL,
    jenis_kelamin ENUM('Laki-Laki', 'Perempuan'),
    tgl_lahir DATE,
    jalan varchar(15) NOT NULL,
    kota varchar(15) NOT NULL,
    kodepos varchar(5) NOT NULL,
    no_hp varchar(15) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/c14807e2-4433-4656-932b-c0f815984636)

Tampilkan hasil table :
```
desc Mahasiswa;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/6fd6dae1-a7b8-4f07-9510-58f5f9820f12)


2. Buat script untuk table Dosen :
```
create table Dosen (
    kd_ds varchar(10) PRIMARY KEY,
    nama varchar(35) NOT NULL
    );
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/9e0dcd3f-7161-43ec-ac81-53412c50eb00)


Tampilkan tabel :
```
desc Dosen;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/2877188a-5601-4e54-8943-c9924bf19644)


3. Buat script untuk Mata kuliah :
```
create table Matakuliah (
    kd_mk varchar(10) PRIMARY KEY,
    nama varchar(30) NOT NULL,
    sks INT NOT NULL
    );
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/89fbaa1a-b27c-4b2f-ba95-e8d2115988f9)


Tampilkan table :
```
desc Matakuliah;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/aed13003-18c6-418a-b97e-96004dc7f433)


4. Buat script untuk jadwal mengajar :
```
create table JadwalMengajar (
    kd_ds varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    hari ENUM('Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu', 'Minggu') NOT NULL,
    jam TIME NOT NULL,
    ruang varchar(555) NOT NULL,
    PRIMARY KEY (kd_ds, kd_mk, hari, jam),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk)
    );
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/d4898bac-7902-4a69-ac6b-a3958c0f4e72)

Tampilkan table :
```
desc JadwalMengajar;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/0701f417-d156-492a-b4c2-912e623d7fbb)


5. Buat script untuk KRSMahasiswa :
```
CREATE TABLE KRSMahasiswa (
    nim varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    semester varchar(10) NOT NULL,
    nilai FLOAT NOT NULL,
    PRIMARY KEY (nim, kd_mk),
    FOREIGN KEY (nim) REFERENCES Mahasiswa(nim),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/b8d888d8-c311-41ae-a95c-d753931a10d4)


Tampilkan table :
```
desc KRSMahasiswa;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/7cdf63c6-a983-40fc-ac26-39ebbaf57cde)


## Soal Latihan Praktikum
Berdasarkan table Mahasiswa pada praktikum sebelumnya: (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

Isi data pada table tersebut sebanyak minimal 5 record data. Tampilkan semua isi/record tabel!

- Ubah data tanggal lahir Mahasiswa yang bernama Ari menjadi: 1979-08-31!

- Tampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja!

- Hapus Mahasiswa yang bernama Dina!

- Tampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita!

- Tampilkan data nama dan alamat Mahasiswa saja dari tabel tersebut

- Tampilkan data Mahasiswa terurut berdasarkan nama.

1. Mengisi tabel dengan minimal 5 record data :
```
insert into Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) values 
-> (11223344,"ari santoso","Laki-laki","1998-10-12","","Bekasi","","",""), 
-> (11223345,"ario talib","Laki-laki","1999-11-16","","Cikarang","","",""), 
-> (11223346,"dina marlina","Perempuan","1997-12-01","","Karawang","","",""), 
-> (11223347,"lisa ayu","perempuan","1996-01-02","","Bekasi","","",""), 
-> (11223348,"tiara wahidah","perempuan","1980-02-05","","Bekasi","","",""), 
-> (11223349,"anton sinaga","laki-laki","1988-03-10","","Cikarang","","","");
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/11346277-0e2a-42d8-84bf-f46e1230afbe)


2. Menampilkan semua isi/record pada tabel bisa menggunakan kode berikut :
```
select*from Mahasiswa;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/540b48ac-e827-4af4-9d17-9b3269af8045)


3. Mengubah data tanggal lahir Mahasiswa yang bernama Ari menjadi : 1979-08-31 menggunakan kode berikut :
```
update Mahasiswa set tgl_lahir='1979-08-31' where nim=11223344;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/31226df7-ea7b-4907-b02a-2a68eaeed153)


4. Menampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja dengan cara sebagai berikut :
```
select*from Mahasiswa where nim=11223344;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/f1b75d63-306d-4425-8701-030348f1d31b)


5. Menghapus Mahasiswa yang bernama Dina dengan cara sebagai berikut:
```
delete from Mahasiswa where nim=11223346;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/22c0d7f9-0d2b-4f1b-ae57-c17341530611)


6. Menampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2 dengan cara sebagai berikut :
```
select*from Mahasiswa where tgl_lahir<='1996-1-2';
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/f8028556-a9eb-4991-91a7-41d5db5e8aee)


7. Menampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan dengan cara sebagai berikut :
```
select*from Mahasiswa where kota='bekasi' and jenis_kelamin='Perempuan';
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/4d21d2a1-af86-41fd-a497-747d2c6ee779)


8. Menampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita dengan cara sebagai berikut :
```
select * from Mahasiswa where kota='Bekasi' and jenis_kelamin='Laki-laki' 
or tgl_lahir<='2002-4-22' 
and jenis_kelamin='Perempuan';
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/e21572b2-62fe-491b-9de0-d6376cd67233)


9. Menampilkan data nama dan jalan Mahasiswa saja dari tabel tersebut dengan cara sebagai berikut :
```
select nama, jalan from Mahasiswa;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/8e16ac44-8f2c-452f-bf19-5666bdc6f9e0)


10. Menampilkan data Mahasiswa terurut berdasarkan nama dengan cara sebagai berikut :
```
select*from Mahasiswa -> order by nama asc;
```
![image](https://github.com/RadityaTansyLizara/PRAKTIKUM2SQL/assets/147571863/492b646f-3b67-44c6-a4b1-c8f72f4330b2)


### Apa bedanya penggunaan BETWEEN dan penggunaan operator >= dan <= ?

(misal: tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11')

(misal: tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11')

Jawaban nya :

operator BETWEEN adalah cara yang lebih ringkas dan efisien untuk memilih nilai dalam suatu rentang, sedangkan operator >= dan <= memberikan lebih banyak fleksibilitas dalam menentukan rentang.

### Berikan kesimpulan anda!

Perintah DML digunakan untuk melakukan berbagai operasi pada data dalam database, seperti memasukkan, memperbarui, dan menghapus data. perintah DML sangat penting untuk mengelola data dalam database. Perintah INSERT digunakan untuk menambah data baru, perintah UPDATE digunakan untuk mengubah data yang sudah ada, dan perintah DELETE digunakan untuk menghapus data. Operator ANTARA dan operator >= dan <= digunakan untuk memfilter data dalam rentang tertentu. Memahami sintaksis dan fungsionalitas perintah ini sangat penting untuk manajemen database yang efektif.
