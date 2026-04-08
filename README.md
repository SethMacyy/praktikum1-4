
# 🚀 Praktikum 1: PHP Framework (CodeIgniter 4)
**Laporan Praktikum Pemrograman Web - Lab 11**

## 👨‍💻 Profil Mahasiswa
* **Nama:** SURYA PUTRA DARMA JAYA
* **NIM:** 312410405
* **Kelas:** I241C
* **Mata Kuliah:** Pemrograman Web

---

## 🎯 Deskripsi & Tujuan Praktikum
Repositori ini merupakan implementasi dari tugas praktikum pengenalan framework **CodeIgniter 4 (CI4)**. Proyek ini dibangun untuk memahami fundamental pengembangan web modern, meliputi:
1. Instalasi dan konfigurasi *environment* web server lokal.
2. Implementasi pola desain arsitektur **MVC (Model-View-Controller)**.
3. Manajemen URL menggunakan sistem **Routing** CI4.
4. Pembuatan *layout* antarmuka yang dinamis dengan sistem **Templating View**.
5. Kustomisasi UI/UX menggunakan teknik *Glassmorphism* dan *Dark Mode*.

---

## 📁 Struktur Direktori Utama
Fokus pengembangan pada praktikum ini berada pada direktori berikut:
```text
ci4/
├── app/
│   ├── Config/
│   │   └── Routes.php         <-- Konfigurasi rute URL
│   ├── Controllers/
│   │   └── Page.php           <-- Pengendali logika halaman (Controller)
│   └── Views/
│       ├── template/          <-- Folder modular layout
│       │   ├── header.php     <-- Template atas (Navigasi)
│       │   └── footer.php     <-- Template bawah (Sidebar & Footer)
│       ├── about.php          <-- Konten halaman About
│       ├── artikel.php        <-- Konten halaman Artikel
│       └── contact.php        <-- Konten halaman Kontak
├── public/
│   └── style.css              <-- File stylesheet utama (CSS)
└── .env                       <-- Konfigurasi environment aplikasi
````

-----

## 🛠️ Langkah-Langkah Praktikum & Analisa Kode

### Langkah 1: Persiapan Environment & Ekstensi PHP

Framework CodeIgniter 4 membutuhkan beberapa ekstensi PHP aktif agar dapat berjalan, seperti `intl` (untuk pengaturan bahasa) dan `mbstring` (untuk pemrosesan karakter).

  * **Tindakan:** Mengedit file `php.ini` pada modul Apache di XAMPP Control Panel dan menghapus tanda titik koma (`;`) pada ekstensi yang dibutuhkan.

> 

### Langkah 2: Mengaktifkan Mode Debugging (`.env`)

<img width="1920" height="1079" alt="praktikum 1 foto 2" src="https://github.com/user-attachments/assets/b3a61318-9112-4cc6-94b1-fadac798e483" />


Secara bawaan, CI4 berada pada mode *production* yang akan menyembunyikan detail *error* (menampilkan halaman "Whoops\!"). Agar *error* syntax dapat dilacak, mode aplikasi diubah ke *development*.

  * **Tindakan:** Me-rename file `env` menjadi `.env` di *root* folder.
  * **Konfigurasi:** Mengubah baris kode menjadi `CI_ENVIRONMENT = development`.

> 

### Langkah 3: Manajemen Routing (`Routes.php`)

<img width="1920" height="1080" alt="routess php" src="https://github.com/user-attachments/assets/7643904c-dd0b-44a4-999f-41fa94ee2cbb" />


Routing digunakan untuk membersihkan URL. Alih-alih mengakses halaman melalui nama controller (`localhost:8080/page/about`), URL dipersingkat menjadi (`localhost:8080/about`).

  * **Kode Implementasi (`app/Config/Routes.php`):**

<!-- end list -->

```php
$routes->get('/', 'Home::index');
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/artikel', 'Page::artikel'); 
```

> 

### Langkah 4: Pembuatan Controller (`Page.php`)

<img width="1920" height="1080" alt="page php" src="https://github.com/user-attachments/assets/84665a2f-af1d-4f63-bccd-5da9f7de2287" />

Sebagai otak dari pola MVC, Controller bertugas mengelola permintaan dari *user* dan mengirimkan data ke View.

  * **Tindakan:** Membuat file `Page.php`. Di dalamnya, data dinamis (seperti `$title` dan `$content`) dibungkus dalam *array* dan dikirim menggunakan perintah `return view()`.
  * **Kode Implementasi (`app/Controllers/Page.php`):**

<!-- end list -->

```php
public function artikel()
{
    return view('artikel', [
        'title' => 'Halaman Artikel',
        'content' => 'Ini adalah kumpulan artikel menarik yang bisa kamu baca di sini.'
    ]);
}
```

> 

### Langkah 5: Sistem Templating View

<img width="1920" height="1080" alt="viewwss" src="https://github.com/user-attachments/assets/168b22f6-db44-41ec-af64-b81852cbed19" />


Untuk mencegah penulisan kode HTML yang berulang-ulang (DRY - *Don't Repeat Yourself*), *layout* web dipecah menjadi beberapa modul (Header dan Footer). Modul ini kemudian dipanggil di dalam file konten utama.

  * **Kode Implementasi (Contoh pada `artikel.php`):**

<!-- end list -->

```php
<?= $this->include('template/header'); ?>

<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->include('template/footer'); ?>
```

> 

### Langkah 6: Desain Antarmuka (CSS)

<img width="1920" height="1080" alt="css" src="https://github.com/user-attachments/assets/0347f39c-b1df-4e16-9cd5-d8fa300a7caa" />

Untuk mempercantik tampilan, ditambahkan file CSS independen di folder `public`. Desain secara spesifik menggunakan skema **Dark Mode** (\#0f172a) dengan efek **Glassmorphism** (`backdrop-filter: blur(16px);`) pada pembungkus (*container*) utama dan aksen teks menyala (*neon text-shadow*) pada judul *header*.

> 

-----

## ✨ Hasil Akhir Tampilan Website (Browser Output)

Setelah semua konfigurasi selesai, server lokal dijalankan melalui CLI dengan perintah `php spark serve`. Berikut adalah dokumentasi hasil *rendering* antarmuka dari beberapa rute halaman yang telah dibuat:

### 1\. Halaman Artikel (`localhost:8080/artikel`)

<img width="928" height="629" alt="praktikum1" src="https://github.com/user-attachments/assets/3b76de4a-be78-41eb-b409-c8484a257754" />


Menampilkan struktur *layout* yang sudah terintegrasi sempurna. Header di bagian atas, konten utama di kiri, *sidebar* di kanan, dan *footer* di bawah.

> 

### 2\. Halaman About (`localhost:8080/about`)

<img width="1904" height="932" alt="about" src="https://github.com/user-attachments/assets/f7993717-ebdd-4020-8aed-b4714d53f6ab" />

Menampilkan deskripsi singkat mengenai proyek web praktikum yang sedang dikerjakan. Data *title* dan konten berhasil dipassing secara dinamis dari Controller.

> 

### 3\. Halaman Kontak (`localhost:8080/contact`)

<img width="1912" height="924" alt="contak" src="https://github.com/user-attachments/assets/15aa3717-8dba-425b-9a09-e97bdb485cdc" />


Menampilkan halaman form interaktif yang *styling*-nya disesuaikan agar menyatu dengan tema antarmuka *Dark Mode*.

> 

-----

# 🚀 Praktikum 2: Framework Lanjutan (CRUD Database)
**Laporan Praktikum Pemrograman Web - Lab 11 (Lanjutan)**

---

## 🎯 Tujuan Praktikum
Praktikum kedua ini berfokus pada pengembangan aplikasi web dinamis dengan CodeIgniter 4. Tujuan utamanya meliputi:
1. Memahami dan mengimplementasikan konsep dasar **Model** pada arsitektur MVC.
2. Memahami alur kerja **CRUD (Create, Read, Update, Delete)** menggunakan database MySQL.
3. Mampu memisahkan *routing* dan tampilan antara halaman publik (*User*) dan halaman pengelola (*Admin*).

---

## 🛠️ Langkah-Langkah Praktikum & Dokumentasi

Berikut adalah dokumentasi dari tahapan implementasi fitur CRUD pada proyek portal berita sederhana ini:

### 1. Persiapan Database & Struktur Tabel
Langkah pertama adalah menyiapkan media penyimpanan data. Database `lab11_ci` dibuat menggunakan MySQL melalui phpMyAdmin. Di dalamnya, dibuat tabel `artikel` yang berisi kolom-kolom untuk menampung data ID, Judul, Isi, Gambar, Status, dan Slug artikel.

<img width="1255" height="451" alt="xampp" src="https://github.com/user-attachments/assets/019ec169-d24f-44ba-b097-8c74212d27bc" />

### 2. Konfigurasi Koneksi Database (`.env`)
Agar CodeIgniter 4 dapat berkomunikasi dengan database MySQL, konfigurasi dilakukan pada file `.env`. Variabel *environment* untuk koneksi database diaktifkan dan disesuaikan nilainya (hostname, database, username).

<img width="1915" height="1074" alt="env" src="https://github.com/user-attachments/assets/106b99d2-292a-4d31-a7cd-04af9991c01e" />

### 3. Pembuatan Model & Controller (Logika CRUD)
* **Model (`ArtikelModel.php`):** Dibuat untuk mendefinisikan tabel yang digunakan (`artikel`) dan *field* apa saja yang diizinkan untuk dimanipulasi (*allowed fields*).
* **Controller (`Artikel.php`):** Dibuat untuk menangani *request* dari *user*. Di dalamnya terdapat fungsi-fungsi CRUD seperti `index()` untuk membaca data (*Read*), `add()` untuk menambah data (*Create*), `edit()` untuk mengubah data (*Update*), dan `delete()` untuk menghapus data (*Delete*).

<img width="274" height="656" alt="artikel dan artikel model" src="https://github.com/user-attachments/assets/e89d269e-250f-440b-9251-598c1d7d8802" />


---


## ✨ Hasil Implementasi Antarmuka (Views)

Aplikasi telah terbagi menjadi dua sisi utama: **Halaman Publik (User)** dan **Halaman Dasbor (Admin)**. Antarmuka tetap mempertahankan desain *Dark Mode* dan *Glassmorphism*.

### 🖥️ Sisi Pengguna (Halaman Publik)

**A. Halaman Daftar Artikel (`/artikel`)**
Halaman ini menampilkan seluruh data artikel yang ditarik dari database. Jika data kosong, akan muncul pesan "Belum ada data".

<img width="1917" height="1034" alt="halaman artikel" src="https://github.com/user-attachments/assets/8b15bc6c-972d-4ebb-9504-05b9efb7f8f2" />


**B. Halaman Detail Artikel (`/artikel/nama-slug`)**
Ketika judul artikel diklik, sistem menggunakan sistem *Routing* berbasis variabel *slug* untuk memanggil data spesifik dari satu artikel dan menampilkannya secara penuh.

<img width="1912" height="1028" alt="artikel pertaman" src="https://github.com/user-attachments/assets/aa459dda-7dab-4d1b-8af1-e5ac5b241593" />

### ⚙️ Sisi Pengelola (Halaman Admin)

**C. Dasbor Manajemen Artikel (`/admin/artikel`)**
Halaman dasbor yang menampilkan tabel data artikel. Di sini Administrator dapat melihat status artikel serta melakukan aksi *Ubah* atau *Hapus* pada data terkait.

<img width="1920" height="1032" alt="admin artikel" src="https://github.com/user-attachments/assets/9adae79e-e9f1-4345-ba55-5d56dd9d0ab3" />


**D. Form Tambah Data / Create (`/admin/artikel/add`)**
Halaman yang berisi *form* input untuk memasukkan artikel baru ke dalam database. Data yang dikirim akan divalidasi terlebih dahulu oleh *Controller* sebelum di-*insert*.

<img width="1920" height="1030" alt="form add" src="https://github.com/user-attachments/assets/febcd117-19e6-482b-9df4-9acc6a5605f0" />

**E. Form Ubah Data / Update (`/admin/artikel/edit/id`)**
Halaman *form* yang secara otomatis menarik data lama dari database berdasarkan ID artikel yang dipilih, sehingga Admin dapat mengubah teks judul maupun isinya, lalu memperbarui datanya di database.

<img width="1920" height="1030" alt="edit" src="https://github.com/user-attachments/assets/159a12df-55c9-4591-a0f2-befe0e5b467d" />

---

# 🚀 Praktikum 3: View Layout dan View Cell (CodeIgniter 4)
**Laporan Praktikum Pemrograman Web - Lab 11 (Lanjutan)**


## 🎯 Tujuan Praktikum
Praktikum ketiga ini bertujuan untuk meningkatkan modularitas dan kerapian struktur *view* pada aplikasi CodeIgniter 4. Fokus utamanya meliputi:
1. Memahami dan mengimplementasikan konsep **View Layout** (Template Utama).
2. Memisahkan struktur kerangka halaman (*header*, *footer*, *sidebar*) dari konten spesifik menggunakan method `extend()` dan `section()`.
3. Memahami dan mengimplementasikan **View Cell** untuk merender komponen UI secara modular dan dinamis (seperti *widget* "Artikel Terkini").

---

## 🛠️ Langkah-Langkah Praktikum & Dokumentasi

Berikut adalah dokumentasi implementasi fitur View Layout dan View Cell:

### 1. Modifikasi Database (Penambahan Kolom `created_at`)
Untuk mendukung fitur "Artikel Terkini" yang akan dibuat menggunakan View Cell, struktur tabel `artikel` perlu dimodifikasi. Kolom baru bernama `created_at` (dengan tipe data DATETIME dan nilai *default* CURRENT_TIMESTAMP) ditambahkan melalui phpMyAdmin agar sistem dapat mendeteksi dan mengurutkan artikel berdasarkan waktu pembuatannya.

<img width="1920" height="1026" alt="xampp" src="https://github.com/user-attachments/assets/e59eba4c-9a4e-42c0-882e-76a895cd0260" />


### 2. Pembuatan View Layout Utama (`main.php`)
Sebuah file kerangka utama dibuat di `app/Views/layout/main.php`. File ini menggabungkan elemen statis (*header*, *navigasi*, *sidebar*, *footer*) menjadi satu template master. Konten dinamis dari halaman lain akan disuntikkan ke bagian spesifik menggunakan perintah `<?= $this->renderSection('content') ?>`.

<img width="1840" height="1080" alt="layout,main php" src="https://github.com/user-attachments/assets/48c1cea9-87b3-4f36-a8bd-a3fe747a4649" />

### 3. Pembuatan Class View Cell (`ArtikelTerkini.php`)
View Cell bertindak sebagai komponen independen. Sebuah *class* dibuat di `app/Cells/ArtikelTerkini.php`. *Class* ini memiliki metode `render()` yang bertugas mengambil 5 data artikel terbaru (diurutkan berdasarkan `created_at` secara *Descending*) dari `ArtikelModel`, lalu mengirimkannya ke *view* komponen.

<img width="1919" height="1080" alt="cels,artikel terkini" src="https://github.com/user-attachments/assets/aa5a297a-c9c3-40d9-bb3b-8df85e7088e7" />

### 4. Pembuatan View untuk Komponen Cell
Tampilan khusus untuk *widget* "Artikel Terkini" dibuat di `app/Views/components/artikel_terkini.php`. *View* ini menerima data dari *class* Cell dan me-render daftar judul artikel dalam format *list*.

<img width="1920" height="1080" alt="component,artikel terkini" src="https://github.com/user-attachments/assets/6e7752c2-b636-4947-b565-36fca528c565" />

---

# 🚀 Praktikum 4: Framework Lanjutan (Modul Login & Autentikasi)
**Laporan Praktikum Pemrograman Web - Lab 11 (Lanjutan)**

## ✨ Hasil Implementasi Antarmuka

Dengan penerapan View Layout, kode pada halaman spesifik menjadi jauh lebih ringkas karena tidak perlu lagi memanggil *header* dan *footer* secara manual. Selain itu, pemanggilan View Cell berhasil menampilkan data artikel terbaru di *sidebar* tanpa harus menulis logika pengambilan data berulang kali di setiap *controller*.

### 🖥️ Hasil Akhir Halaman Utama (Home)
Halaman ini (`localhost:8080/`) telah diperbarui untuk menggunakan *layout* utama dan menampilkan widget "Artikel Terkini" di area *sidebar* kanan.

<img width="1920" height="1025" alt="halaman biasa" src="https://github.com/user-attachments/assets/453cea8f-b368-43f1-a99b-fa2b0870f8b2" />

### 🖥️ Hasil Akhir Halaman Daftar Artikel
Halaman daftar artikel (`localhost:8080/artikel`) juga beradaptasi dengan *layout* yang sama, mempertahankan konsistensi desain secara keseluruhan.

<img width="1920" height="1034" alt="halaman artikel" src="https://github.com/user-attachments/assets/c845f4f8-0627-4775-9263-2a33699a621a" />


---

## 📚 Kesimpulan

Praktikum ini berhasil mengimplementasikan dasar-dasar CodeIgniter 4. Pemisahan komponen menggunakan konsep **MVC** terbukti membuat struktur kode menjadi jauh lebih rapi, terorganisir, dan mudah dikembangkan (*scalable*). Sistem modular pada bagian **View** (*templating header-footer*) sangat mengefisiensikan penulisan kode antarmuka.

## 📸 Dokumentasi & Fitur Aplikasi

Berikut adalah alur penggunaan aplikasi mulai dari pendaftaran akun, login, hingga manajemen artikel.

### 1. Halaman Pendaftaran Akun (Register)
Pengguna baru dapat membuat akun melalui halaman ini. Password akan dienkripsi secara otomatis menggunakan `password_hash` sebelum disimpan ke database.

![Halaman Register]

<img width="1920" height="1080" alt="Buat Akun Berita" src="https://github.com/user-attachments/assets/1f8d2c9b-1d00-40a5-9c06-0090e8eb594d" />


### 2. Halaman Login
Halaman masuk untuk User dan Admin. Sistem akan membedakan hak akses (Role) secara otomatis.
- **Admin**: Diarahkan ke Dashboard Manajemen.
- **User**: Diarahkan ke Halaman Utama Berita.

![Halaman Login]

<img width="1919" height="1080" alt="Login Berita" src="https://github.com/user-attachments/assets/391120e4-3428-453a-ae2a-23bf2f026052" />


### 3. Dashboard Admin (Manajemen Artikel)
Admin memiliki akses penuh untuk melakukan **CRUD** (Create, Read, Update, Delete) pada artikel berita. Tampilan dashboard didesain elegan dengan tabel data.

![Dashboard Admin]

<img width="1920" height="1080" alt="Akun Admin Dashboard" src="https://github.com/user-attachments/assets/f9be36e2-acc8-4973-8cd2-b17911a92006" />


### 4. Edit Artikel (Admin)
Fitur untuk mengubah judul atau isi konten berita yang sudah ada. Formulir ini mengambil data lama dan menampilkannya agar mudah diedit.

![Edit Artikel]

<img width="1920" height="1080" alt="Edit admin" src="https://github.com/user-attachments/assets/68502f7e-c8b2-4240-a421-fbcec848025f" />


### 5. Halaman Utama User (Berita Terkini)
Setelah login, User akan melihat daftar berita terbaru dengan tampilan kartu (Card View) yang responsif. Tombol "Area Admin" tidak akan muncul di sini.

![Dashboard User]

<img width="1918" height="1077" alt="Akun User Dashboard" src="https://github.com/user-attachments/assets/60190cc7-d7a2-4bd4-aae9-59d7088b4f5c" />

### 6. Membaca Artikel (Detail Berita)
Halaman ini menampilkan isi lengkap berita ketika tombol "Baca Selengkapnya" diklik.

![Detail Berita]

<img width="1920" height="1080" alt="Menu Selengkap nya" src="https://github.com/user-attachments/assets/8656d02e-1290-4396-91d9-e5f676499fd3" />


### 7. Halaman Tentang Kami (About)
Halaman informasi profil website dan tim pengembang. Menggunakan desain kartu kaca (Glassmorphism) tanpa foto profil sesuai permintaan.

![Tentang Kami]

<img width="1920" height="1080" alt="About User" src="https://github.com/user-attachments/assets/ca29e8f0-e22f-4495-9c4f-1023a0ccdc40" />


### 8. Halaman Kontak (Contact Us)
Fitur bagi pengunjung untuk melihat informasi kontak atau mengirim pesan kepada pengelola website.

![Kontak Kami]


<img width="1920" height="1080" alt="Contack Akun user" src="https://github.com/user-attachments/assets/916053ab-da43-4bd8-b7c1-3163c1b95a6a" />

---
**© 2026 SURYA PUTRA DARMA JAYA - Universitas Pelita Bangsa**
