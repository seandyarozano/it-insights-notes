# Kenapa Website Lambat Padahal Internet Kencang?

> Bagian dari seri IT Insights Notes — penjelasan teknis dalam bahasa sederhana

---

## Inti Masalahnya

Banyak orang salah kaprah: kalau website lambat, yang disalahkan adalah internet.

Padahal internet dan kecepatan website adalah **dua hal yang berbeda**.

Analoginya: bayangkan kamu pesan makanan online. Kurirnya sudah ngebut, jalan tol kosong.
Tapi dapur restorannya kewalahan — masaknya 1 jam. Salah kurirnya? Tidak.

Begitu juga dengan website. Ada **3 lapisan** yang menentukan kecepatan:

---

## 3 Lapisan Kecepatan Website

### 1. Koneksi Internet (Si Kurir)
Ini bagian yang kita kontrol — sinyal, bandwidth, WiFi.
Kalau lapisan ini yang lambat → semua website ikut lambat.

**Cara cek:** buka speedtest.net. Kalau hasilnya >10 Mbps, internet bukan masalahnya.

### 2. Server Response Time (Si Dapur)
Seberapa cepat server website "memasak" dan mengirim data ke browser.

Ini paling sering jadi biang kerok — tapi paling sering diabaikan.

**Metrik yang diukur:** TTFB (Time To First Byte) — waktu dari request dikirim sampai byte pertama diterima.
- TTFB bagus: < 200ms
- TTFB perlu perhatian: 200ms – 500ms
- TTFB buruk: > 500ms

### 3. Render Time (Si Plating)
Seberapa berat halaman yang harus diproses oleh browser — gambar besar,
script berlebihan, font yang tidak dioptimasi.

**Yang memperlambat render:**
- JavaScript blocking (script diload sebelum konten)
- CSS yang tidak di-minify
- Gambar tanpa lazy loading
- Font dari CDN eksternal tanpa preconnect

---

## 5 Penyebab Paling Umum

### 1. Gambar Tidak Dikompres
Upload foto 5MB langsung ke website = server kerja keras setiap ada pengunjung.

**Solusi:**
- Kompres dulu pakai [Squoosh](https://squoosh.app) atau [TinyPNG](https://tinypng.com)
- Gunakan format **WebP** — 25–35% lebih kecil dari JPEG dengan kualitas sama
- Tambahkan atribut `loading="lazy"` pada semua `<img>` di bawah fold

```html
<!-- Sebelum -->
<img src="foto-produk.jpg">

<!-- Sesudah -->
<img src="foto-produk.webp" loading="lazy" width="800" height="600" alt="Foto produk">
```

### 2. Terlalu Banyak Plugin
WordPress dengan 20+ plugin = website bisa 40% lebih lambat.

Setiap plugin menambah:
- HTTP request tambahan
- CSS dan JS yang di-load meski tidak dipakai
- Query database ekstra

**Solusi:** audit plugin dengan [Query Monitor](https://wordpress.org/plugins/query-monitor/).
Hapus plugin yang tidak aktif digunakan. Target: maksimal 10–15 plugin esensial.

### 3. Font Load dari Server Eksternal
Google Fonts tanpa optimasi menambah waktu loading karena browser harus:
1. Connect ke fonts.googleapis.com
2. Download CSS font
3. Connect ke fonts.gstatic.com
4. Download file font
5. Baru render teks

**Solusi:**
```html
<!-- Tambahkan preconnect di <head> -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```
Atau self-host font menggunakan [google-webfonts-helper](https://gwfh.mranftl.com).

### 4. Script Iklan Pihak Ketiga
Setiap script iklan (Google Ads, Meta Pixel, dll.) menambah:
- 1–3 HTTP request
- Parsing JavaScript yang memblokir render
- Potensi layout shift yang mengganggu pengguna

**Solusi:** load script iklan secara async atau defer:
```html
<!-- Tambahkan defer atau async -->
<script src="ads.js" defer></script>
<script src="pixel.js" async></script>
```

### 5. Hosting Tanpa CDN
Server shared hosting di luar Indonesia + tidak ada CDN = data harus
jalan ribuan kilometer sebelum sampai ke pengunjung lokal.

**Solusi:**
- Gunakan CDN seperti Cloudflare (gratis), BunnyCDN, atau Fastly
- Pilih hosting dengan edge server di Asia Tenggara
- Aktifkan caching di level server (Nginx, Varnish)

---

## Cara Diagnosa Cepat

### PageSpeed Insights (Gratis)
Buka [pagespeed.web.dev](https://pagespeed.web.dev) → masukkan URL → dapatkan skor 0–100.

| Skor | Status | Tindakan |
|------|--------|----------|
| 90–100 | 🟢 Bagus | Pertahankan |
| 50–89 | 🟡 Perlu perhatian | Perbaiki isu prioritas tinggi |
| 0–49 | 🔴 Buruk | Audit menyeluruh diperlukan |

### GTmetrix
[gtmetrix.com](https://gtmetrix.com) — lebih detail dari PageSpeed, bisa lihat waterfall chart setiap resource.

### WebPageTest
[webpagetest.org](https://webpagetest.org) — test dari berbagai lokasi dan koneksi, cocok untuk audit mendalam.

---

## Core Web Vitals — Metrik Google 2025

Google menggunakan 3 metrik utama untuk menilai performa halaman:

| Metrik | Singkatan | Ukur Apa | Target |
|--------|-----------|----------|--------|
| Largest Contentful Paint | LCP | Seberapa cepat konten utama muncul | < 2,5 detik |
| Interaction to Next Paint | INP | Seberapa responsif halaman saat diklik | < 200ms |
| Cumulative Layout Shift | CLS | Seberapa stabil layout saat loading | < 0,1 |

**Catatan:** INP menggantikan FID (First Input Delay) sejak Maret 2024.

---

## Quick Wins — Bisa Dilakukan Hari Ini

1. **Aktifkan kompresi Gzip/Brotli** di server — kurangi ukuran file 60–80%
2. **Tambahkan browser caching** — pengunjung yang balik tidak perlu download ulang
3. **Minify CSS dan JS** — hapus spasi dan komentar yang tidak perlu
4. **Gunakan lazy loading** untuk semua gambar dan iframe
5. **Pasang Cloudflare** (gratis) — CDN, caching, dan proteksi DDoS sekaligus

---

## Kaitannya dengan Konten

- Post LinkedIn Minggu 2: [Mengapa Website Lambat Padahal Internet Kencang?](https://linkedin.com/in/seandyarozano)
- Carousel Instagram: 5 Alasan Website Lambat
- Analogi yang dipakai: kurir (internet) · dapur (server) · plating (render)

---

*IT Insights Notes · [github.com/seandyarozano/it-insights-notes](https://github.com/seandyarozano/it-insights-notes)*
