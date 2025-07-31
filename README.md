NAMA: Dilan Fajar Rafael
NIM: 20240801150

UAS STRUKTUR DATA


- Sistem Manajemen Donasi -

Sistem ini dibuat untuk membantu organisasi atau lembaga sosial dalam mengelola proses donasi secara digital, mulai dari pengumpulan, verifikasi, hingga pelaporan donasi yang diterima.

Tujuan

Membangun **Sistem Manajemen Donasi** berbasis web yang:

- Memudahkan pengelolaan donasi dari berbagai kampanye
- Memantau aktivitas donatur
- Menyediakan proses verifikasi pembayaran
- Meningkatkan transparansi dan efisiensi

---

 Implementasi Singkat

- **Framework**: Laravel 12
- **Admin Panel**: Filament
- **Struktur Data yang Diimplementasikan**:
  - **Array**: Untuk menyimpan data campaign, donatur, dan statistik
  - **Stack**: Untuk menyusun riwayat proses donasi (history stack)
  - **Queue**: Untuk antrian verifikasi pembayaran
  - **Tree**: Untuk mengelompokkan campaign berdasarkan kategori
  - **Graph**: Untuk koneksi antar relasi data
  - **Search**: Untuk mencari data donasi, kampanye, dan donatur
  - **MVC**: Menggunakan struktur Model-View-Controller Laravel

Manfaat Sistem

Bagi Admin
- Memantau seluruh aktivitas donasi dan kampanye
- Memproses verifikasi pembayaran dengan mudah
- Mendapatkan grafik dan statistik langsung di dashboard

Bagi Donatur
- Bisa memilih dan berdonasi ke kampanye yang diinginkan
- Melihat riwayat donasi yang pernah dilakukan
- Mendapat notifikasi status pembayaran

Bagi Organisasi
- Menampilkan transparansi laporan kepada publik
- Menyusun dan mengatur banyak kampanye dengan lebih rapi
- Meningkatkan kepercayaan publik terhadap sistem donasi

Keterkaitan Data

| Tabel            | Relasi                            | Deskripsi                                                                |
|------------------|-----------------------------------|--------------------------------------------------------------------------|
| `Donor`          | hasMany `Donation`                | Satu donatur bisa memiliki banyak donasi                                 |
| `Campaign`       | hasMany `Donation`                | Satu kampanye bisa menerima banyak donasi                                |
| `Donation`       | belongsTo `Donor`, `Campaign`     | Setiap donasi terhubung ke donatur dan kampanye tertentu                 |
| `Donation`       | hasOne `Payment`                  | Donasi akan memiliki satu pembayaran                                     |
| `Payment`        | hasOne `PendingPayment`           | Pembayaran masuk ke dalam antrian pending                                |
| `Payment`        | hasMany `PaymentHistory`          | Riwayat perubahan status pembayaran dicatat di sini                      |



Alur Kerja Sistem

1. Donatur mendaftar / login ke sistem
2. Donatur memilih kampanye yang ingin didukung
3. Donatur mengisi form donasi dan mengirim pembayaran
4. Sistem mencatat data ke tabel `donations` dan `payments`
5. Data pembayaran masuk ke `PendingPayment` (queue)
6. Admin memverifikasi pembayaran
7. Hasil verifikasi dicatat ke `PaymentHistory`
8. Dashboard menampilkan data statistik dan grafik

Contoh Fitur di Dashboard

- Total Donatur
- Total Donasi
- Grafik donasi per kampanye (Line/Bar Chart)
- Riwayat donasi terbaru
- Notifikasi verifikasi donasi masuk
  
