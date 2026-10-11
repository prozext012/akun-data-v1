# Akun YouTube Vault (PWA, satu file)

App penyimpan data akun YouTube (foto, username, email/nomor, password, deskripsi, kategori custom) — bisa di-install jadi aplikasi di HP.

Ini **static site murni** — HTML, CSS, dan JS semuanya jadi satu file `index.html` (gak pakai React/Vite/build step apapun). Cuma 4 hal yang wajib jadi file terpisah karena aturan PWA: `manifest.json`, `sw.js`, dan folder `icons/`.

## Deploy ke Vercel lewat GitHub

1. Push semua file di folder ini ke repo GitHub baru.
2. Buka [vercel.com](https://vercel.com) → **Add New Project** → import repo tadi.
3. Framework Preset: **Other**. Build Command: **kosongkan**. Output Directory: **kosongkan** (biarin default).
4. Deploy. Buka URL-nya di HP.

Gak perlu `npm install`, gak perlu `node_modules`, tinggal upload apa adanya.

## Cara install di HP

- **Android (Chrome)**: buka situsnya, tunggu sebentar, tap menu titik tiga → **Install app**.
- **iOS (Safari)**: tap tombol **Share** → **Add to Home Screen**.

## Struktur project

```
index.html     # seluruh app: HTML + CSS + JS jadi satu
manifest.json  # metadata PWA
sw.js          # service worker (wajib untuk installability)
icons/         # logo app (padlock merah, tema YouTube)
vercel.json    # header cache untuk sw.js & manifest.json
```

## Library eksternal

Dimuat lewat CDN langsung di `index.html`, gak nambah proses build:
- **Tailwind CDN** — styling
- **Lucide (vanilla)** — ikon

## Catatan soal data

Data disimpan di `localStorage` HP/browser tempat app ini diakses — permanen selama gak di-uninstall/clear data, tapi khusus per-device. Pakai fitur **Backup Data** (JSON) di dalam app buat mindahin manual ke device lain.


## Versi Retro + BOT AI

- Tema Retro kertas/krem, jingga, teal, outline tebal, dan animasi interaksi.
- Tombol **BOT AI** di sebelah pencarian membuka halaman chat terpisah.
- Perintah lokal: cari akun, tambah akun dengan username, ubah kategori/durasi/catatan privat, hapus akun dengan konfirmasi, buat/hapus kategori, dan ringkasan jumlah akun.
- Catatan privat AI tidak tampil di kartu akun. Durasi/limit tampil dengan warna kontras.
- Halaman terakhir (Beranda/BOT AI) diingat di perangkat, tombol Back menutup halaman chat kembali ke aplikasi.
- Untuk pertanyaan AI bebas, buka BOT AI → **API** lalu isi endpoint chat completions dan model yang sesuai dokumentasi penyedia. Integrasi menerima format balasan OpenAI-compatible (`choices[0].message.content`) dan beberapa format umum. Endpoint persis SynoxCloud tidak dimasukkan karena alamat endpoint belum tersedia/terverifikasi pada project.

**Catatan privasi:** project ini menyimpan data di localStorage perangkat. Saat menghubungkan API eksternal, konteks akun yang dikirim mencakup username, kontak, kategori, durasi, dan catatan privat; jangan kirim data sensitif ke penyedia yang tidak dipercaya. Untuk deployment publik, gunakan backend/proxy untuk API key rahasia—jangan menaruh key pribadi di frontend.
