# PRAKTIKUM 2: APLIKASI PHP DASAR - FORM PENDAFTARAN EVENT 

# 📃 Identitas Diri

- **Nama**             : Revalina Adelia
- **NPM**              : 4523210091
- **Mata Kuliah**      : Pemrograman Berbasis Web (A)
- **Dosen Pengampu**   : Adi Wahyu Pribadi, S.Si., M.Kom.

Aplikasi ini dibuat untuk memenuhi tugas praktikum dasar PHP. Aplikasi ini merupakan form pendaftaran sederhana untuk sebuah event aktif.

## Deskripsi & Fitur

Aplikasi ini mencakup implementasi dari beberapa konsep dasar PHP, yaitu:
- **Variabel, Global Variabel, dan Konstanta**: Untuk menyimpan data dan konfigurasi.
- **Fungsi**: Digunakan untuk modularisasi kode, khususnya untuk validasi.
- **Penanganan Form (POST)**: Menerima dan memproses data yang dikirim dari form HTML.
- **Validasi dengan Regex**: Memastikan format input email dan tanggal lahir (DD-MM-YYYY) sudah benar.
- **Operasi File**: Menyimpan setiap pendaftar yang valid ke dalam file `pendaftar.txt`.
- **Menampilkan Data**: Membaca data dari `pendaftar.txt` dan menampilkannya dalam bentuk tabel.

## A. Bagian 1: Instalasi $ Konfigurasi Laragon

## B. Bagian 2: Membangun Aplikasi Pendaftaran Event

**1. Membuat File Utama dan Tampilan Form**

Di bagian ini, kita membuat tampilan awal berupa form pendaftaran menggunakan HTML. Caranya dengan membuat folder **praktikum-1**, buat satu file bernama **index.php**. Lalu buka file index.php dan tulis kode HTML berikut untuk membuat form pendaftaran.

<img width="1112" height="476" alt="Membuat File Utama dan Tampilan Form (1)" src="https://github.com/user-attachments/assets/cd1c538d-b0b4-4e66-abf7-331b44f26168" />

<img width="830" height="536" alt="Membuat File Utama dan Tampilan Form (2)" src="https://github.com/user-attachments/assets/6ebddf22-23cf-45a6-a154-f722d5d24434" />

<img width="222" height="61" alt="Membuat File Utama dan Tampilan Form (3)" src="https://github.com/user-attachments/assets/dfc72190-dbb8-4df7-8342-27e176fe0fe7" />

a. Struktur Dasar HTML

   -	Baris **<!DOCTYPE html>** sampai **</html>** adalah kerangka utama halaman web.
  
   -	Di bagian **<head>**, ada pengaturan judul halaman, charset (supaya teks bisa terbaca dengan benar), dan CSS untuk mempercantik tampilan.

b. CSS Styling

   -	Aturan CSS seperti **body { … } dan .form-group { … }** mengatur tampilan agar lebih rapi.

   -	Misalnya, **input[type=”text”] { width: 100%; }** membuat kotak input memanjang sesuai lebar form.

   -	**button { … }** memberi warna biru dan efek klik pada tombol.

c. Form Pendaftaran

   -	Bagian **<form action=”index.php” method=”POST”> … </form>** adalah form yang dipakai untuk   mengirim data ke server.
   -	Atribut **action=”index.php”** artinya data akan dikirim ke file ini sendiri.
   -	Atribut **method=”POST”** artinya data akan dikirim ke file ini sendiri.
   -	Atribut **method=”POST”** artinya data dikirim lewat metode POST (lebih aman dibanding GET, karena data tidak terlihat di URL).

d. Input Form

   -	Ada tiga input utama: **Nama Lengkap, Email,** dan **Tanggal Lahir**.
   
   -	Semua input diberi atribut required agar wajib diisi sebelum dikirim

e. Tombol Kirim

   **<button type=”submit”>Daftar Sekarang</button>** dipakai untuk mengirimkan data ke server.

**2. Menambahkan Logika PHP**

Di bagian ini, kita menambahkan kode PHP untuk mengolah data dari form yang sudah dibuat tadi. Tambahkan blok kode PHP ini di paling atas file **index.php**, sebelum **<!DOCTYPE html>**.

<img width="881" height="683" alt="Menambahkan Logika PHP (1)" src="https://github.com/user-attachments/assets/6ff6e727-bd73-477c-a614-e5c939e715b8" />

<img width="920" height="740" alt="Menambahkan Logika PHP (2)" src="https://github.com/user-attachments/assets/84652af8-0308-410f-a4b5-fa4034d22959" />

a.	Konstanta (Constant)

-	define(‘NAMA_EVENT’, ‘Belajar PHP 2025’); -> menyimpan nama event.

-	define(‘FILE_PENDAFTARAN’, ‘pendaftar.txt’); -> nama file tempat data peserta akan disimpan.

-	Constant dipakai karena nilainya tetap dan tidak akan berubah selama program berjalan.

b.	Variabel Global untuk Status

-	$status_message -> untuk menyimpan pesan sukses.

-	$error_messages = [] -> untuk menyimpan pesan error jika ada kesalahan input.

c.	Fungsi Validasi

-	validateEmail($email) -> mengecek apakah email sesuai format standar (pakai regex).

-	validate($date) -> mengecek apakah tanggal sesuai format DD-MM-YYYY.

d.	Cek Metode POST

-	if ($_SERVER[“REQUEST_METHOD”] == “POST”) { … } -> memastikan bahwa kode hanya berjalan jika form dikirim.

-	Artinya, saat pengguna baru membuka halaman tanpa mengisi form, bagian ini tidak dijalankan.

e.	Mengambil Data Form

-	Data dari form diambil dengan $_POST[‘nama’], $_POST[‘email’], $_POST[‘tanggal_lahir’].

-	Fungsi htmlspecialchars() dipakai untuk mencegah input berbahaya (misalnya script).

f.	Validasi Data

-	Mengecek apakah ada field kosong.

-	Mengecek format email.

-	Mengecek format tanggal.

-	Jika ada yang salah, pesan error dimasukkan ke array $error_messages.

g.	Menyimpan Data ke File

-	Jika tidak ada error, data diformat menjadi string dengan ; sebagai pemisah:
Nama;Email;TanggalLahir

-	Lalu disimpan ke file pendaftar.txt dengan file_put_contents(…, FILE_APPEND).

-	FILE_APPEND memastikan data baru tidak menimpa data lama, tapi ditambahkan di bawahnya.

h.	Pesan Sukses

Jika berhasil, pengguna akan melihat pesan seperti:

Terima kasih, Reva! Pendaftaran Anda untuk event Belajar PHP 2025 berhasil.

**3. Menampilkan Pesan Status dan Daftar Peserta**

1. Menampilkan Pesan Status dan Pesan Kesalahan

Letakkan kode PHP ini di bawah tag <body> dan sebelum tag <h1>. Kode berikut digunakan untuk menampilkan notifikasi berupa pesan sukses maupun daftar kesalahan setelah pengguna melakukan suatu aksi, misalnya pengisian formular:

<img width="609" height="351" alt="Menampilkan Pesan Status" src="https://github.com/user-attachments/assets/5656c79c-a7be-4296-9130-d749675ad62a" />

-	**if (!empty($status_message))**: kondisi ini memeriksa apakah variable $status_message berisi data.
Jika iya, maka pesan tersebut ditampilkan di dalam tag **<p>** dengan class success. Umumnya pesan ini menandakan proses berhasil dilakukan.

-	**if (!empty($error_messages))**: kondisi ini memeriksa apakah terdapat pesan kesalahan di dalam array $error_messages.
Jika ada, maka seluruh pesan kesalahan ditampilkan di dalam elemen **<u1>** menggunakan perulangan **foreach**. Dengan demikian, pengguna dapat mengetahui kesalahan apa yang terjadi.

-	Dengan car aini, sistem dapat memberikan umpan balik yang jelas, baik berupa konfirmasi keberhasilan maupun daftar kesalahan yang harus diperbaiki.


2. Menampilkan Daftar Peserta

Kode berikut digunakan untuk menampilkan seluruh data peserta yang tersimpan di dalam file teks (misalnya **pendaftar.txt**) dalam bentuk tabel. Perintah ini diletakkan di bawah **<h2>Daftar Peserta yang Sudah Mendaftar</h2>**. 

<img width="979" height="732" alt="Menampilkan Daftar Peserta" src="https://github.com/user-attachments/assets/f4aaec40-859e-457f-8400-ac1e7baf17fe" />

-	**file_exists(FILE_PENDAFTARAN)**: digunakan untuk memastikan bahwa file data peserta benar-benar tersedia.

a.	Jika file tersedia, maka seluruh isi file dibaca menggunakan fungsi **file()**. Setiap baris dalam file akan menjadi satu elemen array.

b.	Perulangan **foreach** digunakan untuk menampilkan setiap baris data. Data tersebut dipisahkan dengan fungsi **explode(‘;’, $data)** agar masing-masing informasi (nama, email, tanggal lahir) dapat diproses secara terpisah.

-	Data peserta kemudian ditampilkan dalam bentuk baris tabel **<tr>** dan kolom **<td>**. 

-	Jika file belum tersedia atau kosong, sistem menampilkan pesan “Belum ada pendaftar” sebagai pengganti isi tabel.

-	Fungsi **htmlspecialchars()** digunakan untuk mengamankan tampilan data agar input yang berisi kode HTML tidak dieksekusi sebagai perintah, tetapi tetap ditampilkan sebagai teks biasa.

## C. Bagian 3: Pengumpulan Tugas via GitHub
**Tampilan Awal Form**

<img width="1920" height="1080" alt="Tampilan Awal Form" src="https://github.com/user-attachments/assets/267d60fd-6259-4009-bf81-001a12a68e21" />

**Tampilan setelah Pendaftaran Berhasil**

<img width="1920" height="1080" alt="Mengisi Pendaftaran dengan Benar" src="https://github.com/user-attachments/assets/03e83860-9f28-46b7-b431-46a60549cd1d" />

<img width="1920" height="1080" alt="Hasil Sukses setelah Pendaftaran Benar" src="https://github.com/user-attachments/assets/854e5b6d-90ae-4951-90b5-a53cf7d321ff" />

**Contoh Pesan Error Validasi**

<img width="1920" height="1080" alt="Mengisi Tanggal Lahir dengan Format yang Salah" src="https://github.com/user-attachments/assets/8020a152-3123-4095-aacc-720576f79041" />

<img width="1920" height="1080" alt="Pesan Error terhadap Tanggal Lahir" src="https://github.com/user-attachments/assets/b8ac0f4e-e5a6-410b-aa3a-bd4936d8e2f2" />
