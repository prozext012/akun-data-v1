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
