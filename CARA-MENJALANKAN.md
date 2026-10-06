# Cara Menjalankan Tur 360° Nipah Park Mall

Panduan untuk dosen/asisten yang ingin menjalankan proyek ini di komputer sendiri.

## Yang dibutuhkan

- Komputer Windows dengan browser Chrome / Edge terbaru
- Salah satu: **Laragon** / **XAMPP**, atau **Python 3** (pilih salah satu cara di bawah)
- File proyek (folder `UTS KELOMPOK 3` dari zip / hasil `git clone`)

> ⚠️ **Penting:** `index.html` **tidak bisa** dibuka dengan double-click.
> Foto panorama & model 3D akan diblokir browser (aturan keamanan CORS).
> Harus dijalankan lewat **web server** (`http://...`, bukan `file://...`).

## Cara 1 — Laragon (disarankan, sesuai komputer pengembang)

1. Copy folder `UTS KELOMPOK 3` ke `C:\laragon\www\`
   (atau langsung pakai nama folder itu bila sudah ada).
2. Jalankan **Laragon** → klik **Start All** (Apache + MySQL).
3. Laragon otomatis membuat alamat `http://uts-kelompok-3.test/`
   (nama mengikuti nama folder; huruf kecil, spasi jadi `-`).
4. Buka alamat itu di browser → klik **Mulai Tur**.

## Cara 2 — XAMPP

1. Copy folder `UTS KELOMPOK 3` ke `C:\xampp\htdocs\`.
2. Jalankan **XAMPP Control Panel** → **Start** Apache.
3. Buka `http://localhost/UTS KELOMPOK 3/` di browser → klik **Mulai Tur**.

## Cara 3 — Python (tanpa install server tambahan)

1. Buka folder `UTS KELOMPOK 3` di terminal / CMD:
   ```bat
   cd "D:\path\ke\UTS KELOMPOK 3"
   python -m http.server 8000
   ```
2. Buka `http://localhost:8000/` di browser → klik **Mulai Tur**.

## Cara pakai tur

1. Saat web dibuka muncul penjelasan tur → klik **Mulai Tur**.
2. **Seret mouse** (atau geser jari di HP) untuk melihat sekeliling 360°.
3. Pindah titik: klik tombol **Berikutnya / Sebelumnya**,
   klik titik di **mini map** (kiri atas), atau tekan panah kiri/kanan keyboard.
4. Mini map menunjukkan posisi per lantai (Lantai 5: titik 1–4,
   Lantai 4: titik 5–15). Titik yang sudah dikunjungi berubah warna.
5. Objek 3D tampil otomatis di titiknya: Titik 1 (Samy), Titik 5
   (vending machine), Titik 6 (Ainil), Titik 7 (Dimas), Titik 13 (anggun).

## Catatan

- File `assets/objek-samy.glb` (±196 MB) **tidak ada di GitHub**
  (melebihi batas ukuran file GitHub) — ambil dari file zip pengumpulan.
  Tanpa file itu tur tetap jalan, hanya objek di Titik 1 tidak muncul.
- Bila foto/gambar terlihat lama (versi lama), tekan **Ctrl+Shift+R**
  (hard refresh) untuk memuat ulang tanpa cache.
