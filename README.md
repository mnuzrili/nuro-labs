<p align="center">
  <img src="assets/logo/logo-mark.png" alt="Nuro Labs" height="72">
</p>

<h1 align="center">Nuro Labs</h1>

<p align="center">
  Landing page profil web developer: satu halaman tanpa scroll, model 3D interaktif, dan portofolio proyek.
</p>

Situs statis yang di-host gratis di GitHub Pages. Tidak ada proses build, cukup satu file `index.html` beserta aset di folder `assets/`.

## Fitur

- **One page tanpa scroll**: tiga halaman (Beranda, Portofolio, Kontak) berpindah di tempat lewat menu, tombol, atau panah kiri/kanan di keyboard.
- **URL per halaman**: `#beranda`, `#porto`, dan `#kontak` bisa dibagikan langsung.
- **Model 3D** di Beranda (`.glb`), lengkap dengan layar loading dan cadangan mockup bila gagal dimuat.
- **Kartu proyek** dengan gambar rasio 16:9, otomatis memakai mockup berwarna bila gambar belum ada.
- **Responsif**: model 3D hanya tampil di layar lebar, di HP kartu proyek berbentuk daftar.

## Teknologi

- [Tailwind CSS](https://tailwindcss.com) via CDN
- [Alpine.js](https://alpinejs.dev) untuk interaksi
- [`<model-viewer>`](https://modelviewer.dev) dari Google untuk model 3D
- Font Bricolage Grotesque dan Instrument Sans dari Google Fonts

## Struktur folder

```
.
├── index.html
├── README.md
└── assets/
    ├── logo/
    │   └── logo-mark.png
    ├── 3d/
    │   └── logo.glb
    └── projects/
        └── ...gambar proyek (16:9)
```

## Menjalankan di lokal

Jangan buka `index.html` dengan klik dua kali. Browser memblokir pemuatan file `.glb` dari `file://`, jadi jalankan server lokal di folder proyek:

```bash
php -S localhost:8000
# atau
npx serve
```

Lalu buka `http://localhost:8000`.

## Mengubah konten

| Yang diubah                      | Lokasi di `index.html`                                            |
| -------------------------------- | ----------------------------------------------------------------- |
| Judul dan teks Beranda           | Bagian `<!-- Beranda -->`                                         |
| Daftar proyek                    | Array `projects` di `<script>` paling bawah                       |
| Kontak (WhatsApp, email, GitHub) | Bagian `<!-- Kontak -->`                                          |
| Warna                            | `tailwind.config` di `<head>` (`brand`, `ink`, `mist`, `line`)    |
| Menu atau halaman                | Array `pages`, lalu tambahkan `<section x-show="page === '...'">` |

### Menambah proyek

Tambahkan objek baru di array `projects`:

```js
{
  title: "Nama Proyek",
  color: "#0061FE",                    // warna cadangan bila gambar belum ada
  image: "assets/projects/nama.jpg",   // rasio 16:9, mis. 1280x720
  desc: "Deskripsi singkat proyek.",
  tech: "Laravel · MySQL",
  url: "https://contoh.com",
}
```

Gunakan WebP atau JPG yang dikompres, idealnya di bawah sekitar 200 KB per gambar.

### Model 3D

Ganti file di `assets/3d/logo.glb`, atau ubah atribut `src` pada `<model-viewer>`. Sudut awal kamera diatur lewat `camera-orbit` (format: `theta phi jarak`). Untuk mencari sudut yang pas, putar model di browser lalu jalankan di console:

```js
document.querySelector("model-viewer").getCameraOrbit().toString();
```

Jika `.glb` dikompres dengan Meshopt, konfigurasi decoder-nya sudah ada di `<head>` dan harus tetap berada sebelum skrip `model-viewer`.

## Deploy ke GitHub Pages

1. Buat repository **Public** di GitHub. Nama `username.github.io` menghasilkan situs di `https://username.github.io`, nama lain menghasilkan `https://username.github.io/nama-repo/`.
2. Push dari lokal:
   ```bash
   git init
   git add .
   git commit -m "Landing page Nuro Labs"
   git branch -M main
   git remote add origin https://github.com/USERNAME/NAMA-REPO.git
   git push -u origin main
   ```
3. Buka **Settings → Pages**, pilih **Deploy from a branch**, branch `main`, folder `/ (root)`, lalu **Save**.
4. Tunggu 1–2 menit. Progres bisa dilihat di tab **Actions**.

Untuk update berikutnya cukup `git add .`, `git commit -m "..."`, dan `git push`.

## Catatan

- Tulis path aset **tanpa garis miring di depan** (`assets/...`, bukan `/assets/...`) agar tetap jalan bila repo bukan `username.github.io`.
- GitHub Pages membedakan huruf besar dan kecil pada nama file. `Logo.glb` dan `logo.glb` dianggap berbeda.
- Tailwind lewat CDN menampilkan peringatan di console. Itu normal untuk situs kecil, dan bisa diganti dengan Tailwind CLI bila ingin CSS yang lebih ringan.
- Nomor WhatsApp, email, dan link GitHub di bagian Kontak masih placeholder.

## Lisensi

Hak cipta &copy; Nuro Labs. Seluruh hak dilindungi.
