# Pendakian Slamet

Proyek Laravel untuk reservasi pendakian Gunung Slamet (basis pendaki/admin).

## Setup Cepat
1. Install dependency: `composer install` dan `npm install` (opsional untuk asset).
2. Salin `.env.example` ke `.env`, sesuaikan koneksi DB, lalu `php artisan key:generate`.
3. Migrasi & seed (termasuk enum kewarganegaraan/identitas + dummy berita):  
   `php artisan migrate --seed`
4. Symlink storage (untuk gambar berita/identitas): `php artisan storage:link`.
5. Jalankan server: `php artisan serve`.

## Akun & Alur
- Admin: buat manual lewat seeder `AdminSeeder` (cek `database/seeders/AdminSeeder.php` untuk kredensial).
- Pendaki: registrasi via form; status menunggu verifikasi admin sebelum bisa reservasi.
- Reservasi: pendaki terverifikasi mengisi ketua + anggota (disimpan di JSON `anggota_data`).
- Admin: kelola pendaki, reservasi (termasuk riwayat selesai), blacklist, berita.

## Struktur Singkat
- Route utama: `routes/web.php` (publik, auth, user, admin).
- Layout: `resources/views/layouts/{landing,user,auth,admin}.blade.php`.
- Partial: navbar, hero landing, page hero, realtime, berita, footer di `resources/views/partials`.
- Halaman fitur: `resources/views/pages` (landing/panduan), `berita`, `blacklist`, `peraturan`, `pendakian`, `reservasi`, `pendaki`, `auth`.
- Dokumentasi struktur detail: `docs/STRUKTUR.md`.

## Catatan Teknis
- Kewarganegaraan/Identitas memakai enum (`WNI/WNA`, `KTP/Kartu Pelajar/SIM/Passport/KIAS`) sesuai migrasi `2025_12_10_000000_update_kewarganegaraan_identitas_columns.php`.
- Peringatan composer tentang Flysystem adalah dari paket vendor (tidak memblokir fungsi). Bisa diabaikan atau dibersihkan lewat exclude classmap jika diperlukan.
