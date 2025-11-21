# PRAKTIKUM 8: PHP DATABASE DAN MYSQL 

Nama  : ADINDA AULIA NABILA PUTRI

Nim   : 312410309

Kelas : TI.24.A.4 


# DESKRIPSI 

 Praktikum ini adalah Program sederhana menggunakan PHP dan MySQL untuk mengelola data barang, pengguna bisa menambah, melihat, mengubah dan menghapus data barang, termasuk upload gambar barang. 

# STRUKTUR FOLDER 

  lab8_php_database/ │── index.php │── tambah.php │── ubah.php │── hapus.php │── koneksi.php │── style.css └── gambar/
  
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

# MEMBUAT FILE KONEKSI DATABASE 

 ```
<?php 
$host = "localhost"; 
$user = "root"; 
$pass = ""; 
$db   = "latihan1"; 
 
$conn = mysqli_connect($host, $user, $pass, $db); 
if ($conn == false) 
{ 
    echo "Koneksi ke server gagal."; 
    die(); 
} #else echo "Koneksi berhasil"; 
?>   
```   
   
   Membuat folder ```lab8_php_database``` pada root directory web server (d:\xampp\htdocs) dengan file didalamnya ```koneksi.php```. File ```koneksi.php``` berfungsi untuk menghubungkan aplikasi PHP dengan database MySQL. Di dalam file ini mengatur server seperti host, username, password, dan nama database yang digunakan, yaitu latihan1. Proses koneksi dilakukan menggunakan fungsi ```mysql_connect()```, dan jika koneksi gagal maka program akan menampilkan pesan "koneksi ke server gagal" lalu menghentikan proses. Dengan adanya file ini, aplikasi dapat berjalan dengan baik dan terhubung secara langsung ke MySQL. 

   Berikut hasil pada Browser 

<img width="617" height="173" alt="Screenshot 2025-11-20 203825" src="https://github.com/user-attachments/assets/edbe4cd4-bb18-4060-939c-fa345ff33fcd" />

# MEMBUAT FILE INDEX UNTUK MENAMPILKAN DATA(READ) 

```
<?php
include("koneksi.php");

// query untuk menampilkan data
$sql = "SELECT * FROM data_barang";
$result = mysqli_query($conn, $sql);
?>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Data Barang</title>
<link href="style.css" rel="stylesheet" type="text/css">
</head>
<body>
<div class="container">
    <h1>Data Barang</h1>
    <a href="tambah.php">+ Tambah Barang</a>
    <br><br>
    <table border="1" cellpadding="10" cellspacing="0">
        <tr>
            <th>Gambar</th>
            <th>Nama Barang</th>
            <th>Kategori</th>
            <th>Harga Jual</th>
            <th>Harga Beli</th>
            <th>Stok</th>
            <th>Aksi</th>
        </tr>
        <?php if($result && mysqli_num_rows($result) > 0): ?>
            <?php while($row = mysqli_fetch_assoc($result)): ?>
                <tr>
                    <td>
                        <?php if($row['gambar']): ?>
                            <img src="<?= $row['gambar'];?>" width="80" alt="<?= $row['nama'];?>">
                        <?php else: ?>
                            -
                        <?php endif; ?>
                    </td>
                    <td><?= $row['nama'];?></td>
                    <td><?= $row['kategori'];?></td>
                    <td><?= $row['harga_jual'];?></td>
                    <td><?= $row['harga_beli'];?></td>
                    <td><?= $row['stok'];?></td>
                    <td>
                        <a href="ubah.php?id=<?= $row['id_barang'];?>">Ubah</a> | 
                        <a href="hapus.php?id=<?= $row['id_barang'];?>" onclick="return confirm('Yakin ingin dihapus?')">Hapus</a>
                    </td>
                </tr>
            <?php endwhile; ?>
        <?php else: ?>
            <tr>
                <td colspan="7">Belum ada data</td>
            </tr>
        <?php endif; ?>
    </table>
</div>
</body>
</html><?php
include("koneksi.php");

// query untuk menampilkan data
$sql = "SELECT * FROM data_barang";
$result = mysqli_query($conn, $sql);
?>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Data Barang</title>
<link href="style.css" rel="stylesheet" type="text/css">
</head>
<body>
<div class="container">
    <h1>Data Barang</h1>
    <a href="tambah.php">+ Tambah Barang</a>
    <br><br>
    <table border="1" cellpadding="10" cellspacing="0">
        <tr>
            <th>Gambar</th>
            <th>Nama Barang</th>
            <th>Kategori</th>
            <th>Harga Jual</th>
            <th>Harga Beli</th>
            <th>Stok</th>
            <th>Aksi</th>
        </tr>
        <?php if($result && mysqli_num_rows($result) > 0): ?>
            <?php while($row = mysqli_fetch_assoc($result)): ?>
                <tr>
                    <td>
                        <?php if($row['gambar']): ?>
                            <img src="<?= $row['gambar'];?>" width="80" alt="<?= $row['nama'];?>">
                        <?php else: ?>
                            -
                        <?php endif; ?>
                    </td>
                    <td><?= $row['nama'];?></td>
                    <td><?= $row['kategori'];?></td>
                    <td><?= $row['harga_jual'];?></td>
                    <td><?= $row['harga_beli'];?></td>
                    <td><?= $row['stok'];?></td>
                    <td>
                        <a href="ubah.php?id=<?= $row['id_barang'];?>">Ubah</a> | 
                        <a href="hapus.php?id=<?= $row['id_barang'];?>" onclick="return confirm('Yakin ingin dihapus?')">Hapus</a>
                    </td>
                </tr>
            <?php endwhile; ?>
        <?php else: ?>
            <tr>
                <td colspan="7">Belum ada data</td>
            </tr>
        <?php endif; ?>
    </table>
</div>
</body>
</html>
```

  Membuat file baru di VSCode dengan nama ```index.php```. File ini digunakan untuk menampilkan seluruh data barang dari database. File ini memanggil koneksi database, mengambil data menggunakan query ```SELECT *FROM data_barang```, lalu menampilkannnya dalam bentuk tabel. setiap barang ditampilkan lengkap dengan gambar, nama, katerori, harga jual, harga beli, serta tombol ubah dan hapus untuk mengelola data. Jika tidak ada data, halaman akan menampilkan pesan " Belum ada data". 

  Berikut hasil pada Browser 

<img width="732" height="579" alt="Screenshot 2025-11-21 104256" src="https://github.com/user-attachments/assets/e97cc2ec-9889-40a0-b4c0-0615ff71da25" />

# MENAMBAHKAN DATA(CREATE) 

```
<?php
include_once 'koneksi.php';

if (isset($_POST['submit'])) {
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];

    $gambar = null;
    if (isset($_FILES['file_gambar']) && $_FILES['file_gambar']['error'] == 0) {
        $filename = str_replace(' ', '_', $_FILES['file_gambar']['name']);
        $destination = 'gambar/' . $filename;
        if (move_uploaded_file($_FILES['file_gambar']['tmp_name'], $destination)) {
            $gambar = $destination;
        }
    }

    $sql = "INSERT INTO data_barang (nama, kategori, harga_jual, harga_beli, stok, gambar)
            VALUES ('$nama', '$kategori', '$harga_jual', '$harga_beli', '$stok', '$gambar')";
    mysqli_query($conn, $sql);
    header('Location: index.php');
    exit;
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Tambah Barang</title>
<link href="style.css" rel="stylesheet" type="text/css" />
</head>
<body>
<div class="container">
    <h1>Tambah Barang</h1>
    <form method="post" action="" enctype="multipart/form-data">
        <label>Nama Barang</label><br>
        <input type="text" name="nama" required><br><br>

        <label>Kategori</label><br>
        <select name="kategori" required>
            <option value="Komputer">Komputer</option>
            <option value="Elektronik">Elektronik</option>
            <option value="Hand Phone">Hand Phone</option>
        </select><br><br>

        <label>Harga Jual</label><br>
        <input type="number" name="harga_jual" required><br><br>

        <label>Harga Beli</label><br>
        <input type="number" name="harga_beli" required><br><br>

        <label>Stok</label><br>
        <input type="number" name="stok" required><br><br>

        <label>File Gambar</label><br>
        <input type="file" name="file_gambar"><br><br>

        <input type="submit" name="submit" value="Simpan">
    </form>
</div>
</body>
</html>
```

   Membuat file baru di VSCode dengan nama ```tambah.php```. File ini digunakan untuk menambahkan data barang baru ke dalam database. Pada bagian awal file, sistem memanggil koneksi database dan memeriksa apakah tombol submit telah di tekan. Jika form dikirim, data nama seperti nama barang, kategori, harga jual, harga beli, dan stokk akan diambil dari input pengguna. File ini juga menggunakan proses upload gambar, jika pengguna mengunggah file dan proses upload berhasil, maka gambar akan disimpan ke folder ```gambar/``` dan namanya disimpan ke database. 

   Berikut Hasil pada Browser 

<img width="505" height="593" alt="Screenshot 2025-11-21 105551" src="https://github.com/user-attachments/assets/ec4b53c8-346b-4429-8a79-9a3bc9e97a4b" />

<img width="438" height="607" alt="Screenshot 2025-11-21 105821" src="https://github.com/user-attachments/assets/088d82cb-b5a6-4f1f-b864-2720cb53a53b" />


# MENGUBAH DATA(UPDATE) 

```
<?php
include_once 'koneksi.php';

$id = $_GET['id'] ?? null;
if (!$id) {
    die("ID tidak ditemukan");
}

// ambil data lama
$sql = "SELECT * FROM data_barang WHERE id_barang='$id'";
$result = mysqli_query($conn, $sql);
$data = mysqli_fetch_assoc($result);

if (!$data) die("Data tidak tersedia");

if (isset($_POST['submit'])) {
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];

    $gambar = $data['gambar'];
    if (isset($_FILES['file_gambar']) && $_FILES['file_gambar']['error'] == 0) {
        $filename = str_replace(' ', '_', $_FILES['file_gambar']['name']);
        $destination = 'gambar/' . $filename;
        if (move_uploaded_file($_FILES['file_gambar']['tmp_name'], $destination)) {
            $gambar = $destination;
        }
    }

    $sql_update = "UPDATE data_barang SET 
                    nama='$nama', 
                    kategori='$kategori', 
                    harga_jual='$harga_jual', 
                    harga_beli='$harga_beli', 
                    stok='$stok', 
                    gambar='$gambar'
                   WHERE id_barang='$id'";
    mysqli_query($conn, $sql_update);
    header('Location: index.php');
    exit;
}

// fungsi untuk selected option
function is_select($var, $val) {
    return $var == $val ? 'selected' : '';
}
?>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Ubah Barang</title>
<link href="style.css" rel="stylesheet" type="text/css">
</head>
<body>
<div class="container">
    <h1>Ubah Barang</h1>
    <form method="post" action="" enctype="multipart/form-data">
        <label>Nama Barang</label><br>
        <input type="text" name="nama" value="<?= $data['nama']; ?>" required><br><br>

        <label>Kategori</label><br>
        <select name="kategori" required>
            <option value="Komputer" <?= is_select($data['kategori'], 'Komputer'); ?>>Komputer</option>
            <option value="Elektronik" <?= is_select($data['kategori'], 'Elektronik'); ?>>Elektronik</option>
            <option value="Hand Phone" <?= is_select($data['kategori'], 'Hand Phone'); ?>>Hand Phone</option>
        </select><br><br>

        <label>Harga Jual</label><br>
        <input type="number" name="harga_jual" value="<?= $data['harga_jual']; ?>" required><br><br>

        <label>Harga Beli</label><br>
        <input type="number" name="harga_beli" value="<?= $data['harga_beli']; ?>" required><br><br>

        <label>Stok</label><br>
        <input type="number" name="stok" value="<?= $data['stok']; ?>" required><br><br>

        <label>File Gambar</label><br>
        <input type="file" name="file_gambar"><br>
        <?php if($data['gambar']): ?>
            <img src="<?= $data['gambar']; ?>" width="100" alt="<?= $data['nama']; ?>">
        <?php endif; ?><br><br>

        <input type="submit" name="submit" value="Simpan">
    </form>
</div>
</body>
</html>
```

   Membuat file baru di VSCode dengan nama ```ubah.php```. File ini berfungsi sebagai halaman untuk meperbarui data barang berdasarkan ID yang dipilih dari halaman utama. Pengguna dapat mengubah nama barang, kategori, harga jual, harga beli, stok dan juga menggati gambar. 

   Berikut hasil pada Browser 

<img width="523" height="684" alt="Screenshot 2025-11-21 061345" src="https://github.com/user-attachments/assets/ea9151f1-c643-4c74-93f6-7a127e3f64e1" />

# MENGHAPUS DATA(DELETE) 

```
<?php
error_reporting(E_ALL);
ini_set('display_errors', 1);

include_once 'koneksi.php';

// Ambil ID dari URL
$id = $_GET['id'] ?? null;

if (!$id) {
    die("Error: ID tidak ditemukan di URL");
}

// Cek apakah data dengan ID tersebut ada
$cek = mysqli_query($conn, "SELECT * FROM data_barang WHERE id_barang='$id'");
if (!$cek) {
    die("Error query cek data: " . mysqli_error($conn));
}
if (mysqli_num_rows($cek) == 0) {
    die("Error: Data dengan ID $id tidak ditemukan");
}

// Hapus data
$sql = "DELETE FROM data_barang WHERE id_barang='$id'";
$result = mysqli_query($conn, $sql);

if (!$result) {
    die("Error menghapus data: " . mysqli_error($conn));
}

// Jika berhasil, redirect ke index.php
header('Location: index.php');
exit;
?>
```

  Membuat file baru di VSCode dengan nama ```hapus.php```. File ini digunakan untuk menghapus data barang dari database berdasarkan ID yang dikirim melalui URL. Pada bagian awal, file ini mengambil ID dan melakukan pengecekan untuk memastikan ID tersebut benar-benar ada dalam database. Jika data ditemukan, sistem menjalankan query ```DELETE``` untuk menghapus baris data sesuai ID yang dipilih. File ini juga melengkapi dengan pengecekkan error, sehingga apabila terjadin kessalahan pada proses query, pesan error akan langsung ditampilkan. 

  Berikut hasil pada Browser 

<img width="663" height="659" alt="Screenshot 2025-11-21 105955" src="https://github.com/user-attachments/assets/4ef7bf59-d5ea-4e85-9db5-b5cb063032e0" />

<img width="670" height="660" alt="Screenshot 2025-11-21 111725" src="https://github.com/user-attachments/assets/ba3bd043-8923-4a94-a675-e1bd2f69c368" />

<img width="670" height="601" alt="Screenshot 2025-11-21 111758" src="https://github.com/user-attachments/assets/dc5875b1-9f0e-4a84-b762-d125461ada6a" />
