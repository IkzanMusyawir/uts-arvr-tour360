# Tur 360° Nipah Park Mall Makassar (A-Frame)

Tur panorama 360° interaktif **Nipah Park Mall Makassar**, dari **Lantai 5** turun ke
**Lantai 4**, lalu berjalan menyusuri titik 5–15. Ada **mini map 2 lantai**, navigasi
halus ala Google Maps, dan **4 objek 3D**. Dibuat dengan [A-Frame](https://aframe.io/).

## Fitur

- **15 titik panorama** — mulai Lantai 5 (titik 1–4) lalu Lantai 4 (titik 5–15)
- **Modal sambutan** — penjelasan tur + statistik + panduan kontrol
- **Mini map 2 lantai** — rute bertingkat, tag lantai otomatis, titik yang sudah
  dikunjungi berubah warna, titik aktif berdenyut
- **Fly-through transition** — zoom-in cepat + crossfade ala Google Maps
- **Device rotation tracking** — di HP, putar perangkat untuk melihat sekeliling
- **Keyboard support** — panah kiri/kanan, Enter/Space di node map, Esc tutup modal
- **4 objek 3D**: Samy (Titik 1), vending machine (Titik 5), Ainil (Titik 6), anggun (Titik 13)
- **Boundary guard** — Titik 15 tidak berputar balik ke Titik 1 (muncul notifikasi)
- **Aksesibilitas** — aria-live, fokus keyboard, `prefers-reduced-motion`, kontras teks

## Desain

- **Style:** Immersive dark + spatial glass (backdrop blur), cocok untuk tur VR
- **Warna:** latar deep navy `#0A0E27`, aksen sky `#38BDF8`, sorot gold `#F5B301`
- **Font:** Cinzel (judul) + Josefin Sans (isi)
- **Breakpoint:** 375px, 560px, 768px, 1024px, 1440px

## Cara menjalankan (untuk teman yang baru clone)

> ⚠️ **Wajib pakai web server.** Buka `index.html` langsung (double-click) **tidak
> bisa** — foto & model 3D akan diblokir browser karena aturan CORS.

### 1. Clone repo

```bash
git clone https://github.com/IkzanMusyawir/uts-arvr-tour360.git
cd uts-arvr-tour360
```

### 2. Jalankan lewat web server (pilih salah satu)

**Cara A — Python (paling gampang):**
```bash
python -m http.server 8000
```
Lalu buka **http://localhost:8000** di browser (Chrome/Edge).

**Cara B — XAMPP / Laragon:**
- Copy folder ini ke `htdocs` (XAMPP) atau `www` (Laragon).
- Contoh: `C:\laragon\www\uts-arvr`
- Buka **http://localhost/uts-arvr** atau **http://uts-arvr.test** (Laragon).

**Cara C — VS Code (ekstensi "Live Server"):**
- Klik kanan `index.html` → **Open with Live Server**.

### 3. Selesai

Modal sambutan muncul → klik **Mulai Tur** → jelajahi lewat tombol / mini map.

## Struktur

```
.
├── index.html                              # seluruh aplikasi (satu file)
├── foto/                                   # 15 panorama 360 (equirectangular 2:1)
│   └── 1.jpg … 15.jpg
└── assets/                                 # model 3D (.glb)
    ├── vendine_mechine.glb                 # -> Titik 3
    ├── objek-ainil.glb                     # -> Titik 6
    └── objek-anggun.glb                    # -> Titik 9
```

## Menambah / mengubah objek 3D

1. Taruh file `.glb` ke folder `assets/`
2. Buka `index.html`, cari array `OBJEK3D`, isi/ubah sesuai kebutuhan:

```js
const OBJEK3D = [
  { model: "assets/namamodel.glb", titik: 2, pos: [0, 1.0, -2.5], rot: [0, 0, 0], scale: 1 },
  //        ^ path file            ^ tampil di Titik 3 (0=Tx1, 14=Tx15)
  ...
];
```

| Field | Arti |
|-------|------|
| `model` | path file `.glb` (`null` = slot kosong, tidak dirender) |
| `titik` | index titik tempat muncul (**0 = Titik 1**, 1 = Titik 2, … 14 = Titik 15) |
| `pos` | posisi `[x, y, z]` — x: kiri/kanan, y: naik/turun, z: jauh/dekat |
| `rot` | rotasi `[x, y, z]` dalam derajat |
| `scale` | perbesaran (model fotogrametri biasanya perlu nilai kecil, mis. `0.08`) |

### Cara cari posisi & rotasi yang pas (alat bantu slider)

Kalau mau mengatur posisi/rotasi objek sambil melihat langsung:

1. Tambahkan panel slider di `index.html` (sisi teman kamu bisa minta file panelnya).
2. Geser slider sampai objek pas di tempat yang diinginkan.
3. Salin angka di kotak hijau → tempel ke array `OBJEK3D`.

## Mengganti foto

Timpa `foto/N.jpg`, lalu **naikkan** `VERSI_FOTO` di `index.html` supaya browser
tidak memakai versi lama dari cache:

```js
const VERSI_FOTO = 2;   // -> 3, 4, ... setiap kali foto diganti
```

## Menyesuaikan animasi fly-through

Di dalam `keTitik()` pada `index.html`:
- `FOV_PUNCAK = 20` — makin kecil, zoom makin dalam
- `-1.6 * e` — jarak dolly maju kamera
- `DUR = 520` — durasi transisi (ms)

## Cara berkontribusi (edit & kirim balik)

```bash
git add -A
git commit -m "pesan perubahan"
git push
```

Kalau bukan collaborator, **Fork** dulu repo-nya di GitHub, baru buat **Pull Request**.
