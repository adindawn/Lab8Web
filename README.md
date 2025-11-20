# PRAKTIKUM 8: PHP DATABASE DAN MYSQL 

Nama  : ADINDA AULIA NABILA PUTRI

Nim   : 312410309

Kelas : TI.24.A.4 


# DESKRIPSI 

 Praktikum ini adalah Program sederhana menggunakan PHP dan MySQL untuk mengelola data barang, pengguna bisa menambah, melihat, mengubah dan menghapus data barang, termasuk upload gambar barang. 

# LANGKAH-LANGKAH PRAKTIKUM 

# MEMBUAT DATABASE: STUDI KASUS DATA BARANG 

   Membuat Database di ```CREATE DATABASE``` latihan1 

# MEMBUAT TABEL 

```CREATE TABLE data_barang ( 
id_barang int(10) auto_increment Primary Key, 
kategori varchar(30), 
nama varchar(30), 
gambar varchar(100), 
harga_beli decimal(10,0), 
harga_jual decimal(10,0), 
stok int(4) 
);
```

# MENAMBAHKAN DATA

```INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok) 
VALUES ('Elektronik', 'HP Samsung Android', 'hp_samsung.jpg', 2000000, 2400000, 5), 
('Elektronik', 'HP Xiaomi Android', 'hp_xiaomi.jpg', 1000000, 1400000, 5), 
('Elektronik', 'HP OPPO Android', 'hp_oppo.jpg', 1800000, 2300000, 5);
```
 Berikut hasil Screenshot dari phpMyAdmin 

<img width="857" height="258" alt="Screenshot 2025-11-21 060528" src="https://github.com/user-attachments/assets/13e62718-90ae-4ad5-953b-d8b5feb05532" />
