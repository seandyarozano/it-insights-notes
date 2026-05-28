# Website Performance Notes
> Catatan teknis dari konten IT Insights Minggu 2 — Website & SEO
> Topik: Mengapa website lambat padahal internet sudah kencang?

---

## 3 Lapisan Kecepatan Website

Website yang lambat bukan selalu salah koneksi internet. Ada 3 lapisan yang perlu dipahami:

| Lapisan | Nama Analogi | Penjelasan |
|--------|--------------|------------|
| 1 | Koneksi Internet ("Si Kurir") | Sinyal, bandwidth, WiFi. Kalau ini lambat → semua website ikut lambat |
| 2 | Server Response ("Si Dapur") | Seberapa cepat server memproses dan mengirim data. Sering diabaikan |
| 3 | Render Time ("Si Plating") | Seberapa berat halaman diproses browser: gambar, script, font. Ini yang bisa dioptimasi |

**Insight penting:** Mayoritas masalah "website lambat" berasal dari lapisan 2 dan 3 — bukan dari koneksi internet pengguna.

---

## 5 Penyebab Umum Website Lambat

### 1. Gambar Tidak Dikompres
- Upload foto 5MB langsung ke website → server bekerja keras setiap ada pengunjung
- **Solusi:** Kompres gambar sebelum upload. Gunakan format **WebP** (lebih kecil dari JPG/PNG dengan kualitas serupa)
- Tools: [Squoosh](https://squoosh.app), [TinyPNG](https://tinypng.com), plugin Smush (WordPress)

### 2. Terlalu Banyak Plugin (WordPress)
- WordPress dengan 20+ plugin = potensi 40% lebih lambat dari seharusnya
- Setiap plugin menambah request HTTP dan kode yang harus dieksekusi
- **Solusi:** Audit dan hapus plugin yang tidak aktif atau bisa digantikan native CSS/HTML

### 3. Font Load dari Server Luar
- Google Fonts tanpa optimasi menambah waktu loading sebelum teks muncul di layar (render-blocking)
- **Solusi:** Self-host font atau gunakan `font-display: swap` + preconnect

```html
<!-- Preconnect untuk Google Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

### 4. Iklan Pihak Ketiga Berat
- Script iklan yang loading bersamaan dapat memblokir konten utama untuk muncul di layar
- **Solusi:** Lazy load iklan, batasi jumlah script ads, pertimbangkan async/defer

```html
<!-- Load script iklan secara async -->
<script async src="ads-script.js"></script>
```

### 5. Hosting Murah Tanpa CDN
- Server shared hosting di luar negeri + tidak ada CDN = data harus jalan jauh sebelum sampai ke pengunjung Indonesia
- **Solusi:** Gunakan CDN lokal (Cloudflare free tier sudah cukup) atau hosting dengan edge server di Indonesia

---

## Core Web Vitals — Metrik yang Digunakan Google

Google menggunakan tiga metrik utama untuk menilai pengalaman pengguna:

| Metrik | Singkatan | Target | Arti |
|--------|-----------|--------|------|
| Largest Contentful Paint | LCP | < 2.5 detik | Seberapa cepat konten utama muncul |
| Interaction to Next Paint | INP | < 200ms | Seberapa responsif halaman saat diklik |
| Cumulative Layout Shift | CLS | < 0.1 | Seberapa stabil layout (tidak geser-geser) |

> **Catatan:** Google menggunakan Core Web Vitals sebagai salah satu faktor ranking SEO. Website yang lambat bisa kalah di hasil pencarian.

---

## Fakta Penting (Data Referensi)

- **53%** pengguna mobile meninggalkan halaman jika loading lebih dari 3 detik
- **7%** penurunan konversi untuk setiap 1 detik keterlambatan loading
- Durasi ideal loading halaman: **di bawah 2 detik** untuk pengalaman yang baik

> ⚠️ Catatan: Angka di atas sering dikutip di industri web performance. Verifikasi ke sumber primer (Google Web Dev, Think with Google) sebelum menggunakannya dalam konteks formal.

---

## Tools Gratis untuk Cek Performa Website

| Tool | URL | Fungsi |
|------|-----|--------|
| PageSpeed Insights | [pagespeed.web.dev](https://pagespeed.web.dev) | Skor 0-100 + rekomendasi spesifik |
| GTmetrix | [gtmetrix.com](https://gtmetrix.com) | Waterfall chart + analisis detail |
| WebPageTest | [webpagetest.org](https://webpagetest.org) | Test dari lokasi server berbeda |
| Chrome DevTools | F12 → Network | Real-time profiling di browser |

**Cara baca skor PageSpeed:**
- **90+** → Website cepat ✅
- **50–89** → Perlu optimasi ⚠️
- **< 50** → Segera perbaiki ❌

---

## Checklist Optimasi Dasar

- [ ] Kompres semua gambar (target < 200KB per gambar)
- [ ] Konversi gambar ke format WebP
- [ ] Aktifkan caching browser
- [ ] Gunakan CDN (minimal Cloudflare free)
- [ ] Audit dan hapus plugin tidak terpakai (WordPress)
- [ ] Tambahkan `preconnect` untuk resource eksternal (Google Fonts, dll)
- [ ] Aktifkan GZIP/Brotli compression di server
- [ ] Cek skor PageSpeed — target minimal 70+

---

## Referensi

- [Google Web Dev — Core Web Vitals](https://web.dev/vitals/)
- [PageSpeed Insights](https://pagespeed.web.dev)
- [MDN — Web Performance](https://developer.mozilla.org/en-US/docs/Web/Performance)
- [Cloudflare Learning Center](https://www.cloudflare.com/learning/)

---

*Catatan ini dibuat sebagai pendamping konten LinkedIn & Instagram Minggu 2 — IT Insights series oleh [@seandyarozano](https://github.com/seandyarozano)*
