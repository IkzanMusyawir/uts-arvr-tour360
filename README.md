# Tur 360° + Objek 3D (A-Frame)

Tur panorama 360° dengan **15 titik** lokasi, mini map, dan slot untuk **5 objek 3D**
(diisi menyusul). Dibuat dengan [A-Frame](https://aframe.io/) — berjalan langsung di browser.

## Demo

Jalankan lewat web server (wajib — `file://` tidak bisa karena CORS):

```bash
# Python
python -m http.server 8000
#  -> buka http://localhost:8000

# atau taruh di htdocs XAMPP/Laragon, mis.:
#   C:\laragon\www\uts-arvr  ->  http://uts-arvr.test/
```

## Fitur

- **15 titik panorama** — navigasi lewat tombol Berikutnya/Sebelumnya
- **Mini map** (kiri atas) — klik titik untuk lompat ke lokasi mana pun
- **Fly-through transition** — zoom-in cepat + crossfade ala Google Maps saat pindah titik
- **Device rotation tracking** — di HP, putar perangkat untuk melihat sekeliling
- **Slot objek 3D** — siap diisi 5 model `.glb` di titik berbeda (lihat di bawah)
- **Boundary guard** — Titik 15 tidak berputar balik ke Titik 1, muncul notifikasi

## Struktur

```
.
├── index.html      # seluruh aplikasi (satu file)
├── foto/           # 15 panorama 360 (equirectangular 2:1)
│   └── 1.jpg … 15.jpg
└── assets/         # taruh file .glb objek 3D di sini
```

## Menambah objek 3D

1. Taruh file `.glb` ke folder `assets/`
2. Buka `index.html`, cari array `OBJEK3D`, isi bagian `model`:

```js
const OBJEK3D = [
  { model: "assets/namamodel.glb", titik: 2, pos: [0, 1.0, -2.5], rot: [0, 0, 0], scale: 1 },
  //        ^ path file            ^ tampil di Titik 3 (0=Tx1, 14=Tx15)
  ...
];
```
Objek hanya muncul di titik yang ditentukan. Selama `model: null`, tidak ada yang dirender.

## Mengganti foto

Timpa `foto/N.jpg`, lalu **naikkan** `VERSI_FOTO` di `index.html` supaya browser
tidak memakai versi lama dari cache:

```js
const VERSI_FOTO = 2;   // -> 3, 4, ... setiap kali foto diganti
```

## Menyesuaikan animasi

Di dalam `keTitik()` pada `index.html`:
- `FOV_PUNCAK = 20` — makin kecil, zoom makin dalam
- `-1.6 * e` — jarak dolly maju kamera
- `DUR = 520` — durasi transisi (ms)
