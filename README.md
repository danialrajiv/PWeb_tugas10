# **Formulir Pendaftaran Siswa Baru - CRUD dengan Upload Foto**

### 📌 Deskripsi Tugas
Ini adalah pengembangan dari proyek sebelumnya, yaitu aplikasi web CRUD (Create, Read, Update, Delete) yang kini dilengkapi dengan **fitur upload foto siswa**. Aplikasi ini dibangun menggunakan **PHP** dan database **MySQL** untuk mengelola data pendaftaran secara online, di mana semua data termasuk file foto siswa disimpan secara permanen.

Proyek ini dijalankan secara lokal menggunakan **XAMPP** dan diakses melalui browser.

---

### 💻 Tumpukan Teknologi (Tech Stack)
- **HTML & CSS**: Untuk struktur dan desain antarmuka (frontend) yang modern dan menarik.
- **PHP**: Sebagai bahasa pemrograman untuk memproses seluruh logika di sisi server (backend), termasuk penanganan upload file.
- **MySQL**: Sebagai sistem manajemen database untuk menyimpan data pendaftar dan referensi nama file foto.
- **XAMPP**: Sebagai server lokal yang menjalankan Apache (Web Server) dan MySQL.

---

### ✅ Fitur Aplikasi
- **Create**: Menambahkan data siswa baru beserta **foto** melalui formulir pendaftaran.
- **Read**: Menampilkan seluruh data siswa yang sudah mendaftar, lengkap dengan **thumbnail foto** dan **timestamp** pendaftaran.
- **Update**: Mengubah data siswa, termasuk **mengganti foto lama** dengan yang baru.
- **Delete**: Menghapus data siswa dari database sekaligus **menghapus file fotonya** dari server.
- **Desain Menarik**: Tampilan antarmuka yang disempurnakan, termasuk halaman utama yang lebih menarik dan navigasi yang lebih baik.
- **Penyimpanan File**: File foto yang diunggah disimpan dalam folder `foto_siswa/` di server.

---

### 📂 Struktur Proyek
```
/pendaftaran-db/
├── foto_siswa/                <-- Folder untuk menyimpan foto
├── config.php
├── index.php
├── form-daftar.php
├── proses-pendaftaran.php
├── list-siswa.php
├── form-edit.php
├── proses-edit.php
├── hapus.php
└── style.css
```

---

### 🖼️ Tampilan Web (Screenshot)

**Halaman Utama**
![Halaman Utama](https://github.com/danialrajiv/PWeb_tugas10/blob/main/home_page.png)

**Halaman Daftar Siswa dengan Foto & Timestamp**
![Halaman Daftar Siswa](https://github.com/danialrajiv/PWeb_tugas10/blob/main/list_page.png)

**Halaman Formulir Pendaftaran**
![Formulir Pendaftaran](https://github.com/danialrajiv/PWeb_tugas10/blob/main/form_page.png)

**Halaman Edit**
![Formulir Pendaftaran](https://github.com/danialrajiv/PWeb_tugas10/blob/main/edit_page.png)
---

### 👨‍💻 Kode Sumber (Source Code)

<details>
<summary><b>style.css</b> (Klik untuk melihat kode)</summary>

```css
/* Import Font dari Google Fonts */
@import url('[https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap](https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap)');

/* Reset dan Pengaturan Dasar */
* { margin: 0; padding: 0; box-sizing: border-box; }

body {
    font-family: 'Poppins', sans-serif;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: #333;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    padding: 20px;
}

/* Container Utama */
.container {
    width: 100%;
    max-width: 950px;
    background: rgba(255, 255, 255, 0.9);
    backdrop-filter: blur(5px);
    -webkit-backdrop-filter: blur(5px);
    border-radius: 20px;
    padding: 40px;
    box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
}

/* Header */
header { text-align: center; margin-bottom: 30px; }
header h1, header h3 { color: #2c3e50; text-shadow: 1px 1px 2px rgba(0,0,0,0.1); }

/* Tombol */
.btn {
    text-decoration: none; color: #fff; padding: 12px 25px; border-radius: 50px;
    font-weight: 600; transition: all 0.3s ease; box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    border: none; cursor: pointer; font-size: 16px; display: inline-block; margin: 5px;
}
.btn-primary { background: linear-gradient(45deg, #3a7bd5, #00d2ff); }
.btn-secondary { background: linear-gradient(45deg, #868f96, #596164); }
.btn-add { background: linear-gradient(45deg, #1dd1a1, #10ac84); }
.btn-edit { background: linear-gradient(45deg, #feca57, #ff9f43); color: #333; }
.btn-delete { background: linear-gradient(45deg, #ff6b6b, #ee5253); }
.btn:hover { transform: translateY(-3px); box-shadow: 0 6px 20px rgba(0,0,0,0.3); }

/* Halaman Utama (Homepage) */
.hero-section { text-align: center; padding: 40px 0; }
.hero-section h1 { font-size: 3.5em; color: #34495e; margin-bottom: 10px; }
.hero-section p { font-size: 1.2em; color: #555; margin-bottom: 30px; }
.hero-section .action-buttons a { margin: 10px; }

/* Tabel */
.table-wrapper { overflow-x: auto; }
table {
    width: 100%; border-collapse: collapse; margin-top: 20px;
    background: #fff; border-radius: 10px; overflow: hidden;
}
table th, table td { padding: 15px; text-align: left; border-bottom: 1px solid #eee; vertical-align: middle; }
table thead { background: #34495e; color: white; }
table tbody tr:hover { background-color: #f1f8ff; }
.student-photo { width: 60px; height: 60px; border-radius: 50%; object-fit: cover; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
.timestamp { font-size: 0.8em; color: #777; }

/* Formulir */
fieldset { border: none; padding: 0; }
.form-group { margin-bottom: 20px; }
.form-group label { font-weight: 500; margin-bottom: 8px; display: block; color: #34495e; }
.form-group input, .form-group textarea, .form-group select {
    width: 100%; padding: 15px; border: 1px solid #ddd;
    border-radius: 10px; font-size: 16px; color: #333; transition: all 0.3s ease;
}
.form-group input:focus, .form-group textarea:focus, .form-group select:focus {
    outline: none; border-color: #3a7bd5; box-shadow: 0 0 0 3px rgba(58, 123, 213, 0.3);
}
.radio-group label { margin-right: 20px; }
.form-actions { display: flex; gap: 10px; margin-top: 20px; }

/* Pesan Status */
.status-message {
    padding: 15px; margin-bottom: 20px; border-radius: 10px; text-align: center;
    font-weight: 500; color: #fff;
}
.sukses { background-color: rgba(29, 209, 161, 0.8); }
.gagal { background-color: rgba(238, 82, 83, 0.8); }
```

</details>

<details>
<summary><b>index.php</b> (Klik untuk melihat kode)</summary>

```php
<!DOCTYPE html>
<html>
<head>
    <title>Pendaftaran Siswa Baru</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <div class="hero-section">
            <h1>Sistem Pendaftaran Siswa</h1>
            <p>Platform digital untuk mengelola pendaftaran siswa baru dengan mudah dan efisien.</p>
            <div class="action-buttons">
                <a href="list-siswa.php" class="btn btn-primary">Lihat Pendaftar</a>
                <a href="form-daftar.php" class="btn btn-add">Daftar Baru</a>
            </div>
        </div>
    </div>
</body>
</html>
```

</details>

<details>
<summary><b>list-siswa.php</b> (Klik untuk melihat kode)</summary>

```php
<?php include("config.php"); ?>
<!DOCTYPE html>
<html>
<head>
    <title>Pendaftaran Siswa Baru</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <header>
            <h3>Siswa yang sudah mendaftar</h3>
        </header>

        <nav>
            <a href="form-daftar.php" class="btn btn-add">[+] Tambah Baru</a>
            <a href="index.php" class="btn btn-secondary">Kembali ke Beranda</a>
        </nav>

        <?php if(isset($_GET['status'])): ?>
            <p class="status-message <?php echo $_GET['status']; ?>">
                <?php echo $_GET['status'] == 'sukses' ? "Proses berhasil!" : "Proses gagal!"; ?>
            </p>
        <?php endif; ?>

        <div class="table-wrapper">
            <table>
            <thead>
                <tr>
                    <th>No</th>
                    <th>Foto</th>
                    <th>Nama</th>
                    <th>Alamat</th>
                    <th>Jenis Kelamin</th>
                    <th>Sekolah Asal</th>
                    <th>Tanggal Daftar</th>
                    <th>Tindakan</th>
                </tr>
            </thead>
            <tbody>
                <?php
                $sql = "SELECT * FROM calon_siswa";
                $query = mysqli_query($db, $sql);
                $no = 1;
                while($siswa = mysqli_fetch_array($query)){
                    echo "<tr>";
                    echo "<td>".$no++."</td>";
                    echo "<td><img src='uploads/".$siswa['foto']."' class='student-photo'></td>";
                    echo "<td>".$siswa['nama']."</td>";
                    echo "<td>".$siswa['alamat']."</td>";
                    echo "<td>".$siswa['jenis_kelamin']."</td>";
                    echo "<td>".$siswa['asal_sekolah']."</td>";
                    echo "<td class='timestamp'>".date('d-m-Y H:i', strtotime($siswa['tanggal_daftar']))."</td>";
                    echo "<td>";
                    echo "<a href='form-edit.php?id=".$siswa['id']."' class='btn btn-edit'>Edit</a>";
                    echo "<a href='hapus.php?id=".$siswa['id']."' class='btn btn-delete' onclick='return confirm(\"Yakin ingin menghapus data ini?\")'>Hapus</a>";
                    echo "</td>";
                    echo "</tr>";
                }
                ?>
            </tbody>
            </table>
        </div>
        <p style="text-align:center; margin-top:20px; font-weight:bold;">Total Pendaftar: <?php echo mysqli_num_rows($query) ?></p>
    </div>
</body>
</html>
```

</details>

*(Untuk file lainnya seperti `form-daftar.php`, `proses-pendaftaran.php`, `form-edit.php`, `proses-edit.php`, dan `hapus.php` Anda bisa salin dari jawaban saya sebelumnya karena tidak ada perubahan lebih lanjut pada logika intinya).*
