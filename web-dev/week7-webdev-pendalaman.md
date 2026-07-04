# Minggu 7 — Website & Web Dev Pendalaman
## Core Web Vitals: LCP, INP, CLS

**Periode:** 30 Juni – 5 Juli 2026
**Tema:** Website & Web Dev (Siklus 2 — Pendalaman)
**Anchor topik:** Core Web Vitals — metrik resmi Google untuk pengalaman pengguna

---

## Konsep Utama

### Apa itu Core Web Vitals?
Tiga metrik yang dipakai Google untuk mengukur pengalaman pengguna di website,
bukan sekadar kecepatan loading. Masing-masing mengukur dimensi berbeda dari
perspektif pengguna nyata.

---

### 1. LCP — Largest Contentful Paint
**Mengukur:** Waktu hingga elemen konten terbesar di viewport selesai dirender.
Biasanya: hero image, block teks utama, atau video poster.

**Threshold resmi Google (per web.dev/vitals):**
- Good    : < 2.5 detik
- Needs improvement : 2.5 – 4.0 detik
- Poor    : > 4.0 detik

**Penyebab LCP lambat:**
- Server response time tinggi (TTFB besar)
- Render-blocking resources (CSS/JS yang memblok rendering)
- Gambar tidak dioptimasi (tidak pakai lazy load, tidak dikompres)
- Client-side rendering tanpa SSR/SSG

**Cara cek:** Chrome DevTools > Performance tab > LCP marker

---

### 2. INP — Interaction to Next Paint
**Mengukur:** Latensi dari semua interaksi pengguna (klik, ketuk, keyboard)
selama halaman terbuka — diambil nilai persentil ke-75.

**Catatan penting:** INP menggantikan FID (First Input Delay) secara resmi
pada 12 Maret 2024. FID hanya mengukur interaksi pertama; INP mengukur
semua interaksi sepanjang sesi.

**Threshold resmi Google:**
- Good    : < 200ms
- Needs improvement : 200 – 500ms
- Poor    : > 500ms

**Penyebab INP tinggi:**
- Long tasks di main thread (JavaScript berat)
- Tidak ada input debouncing
- DOM size terlalu besar
- Third-party scripts memblok thread

**Cara cek:** Chrome DevTools > Performance Insights > INP

---

### 3. CLS — Cumulative Layout Shift
**Mengukur:** Total pergeseran layout yang terjadi selama halaman dimuat.
Dihitung dari impact fraction x distance fraction setiap shift.

**Threshold resmi Google:**
- Good    : < 0.1
- Needs improvement : 0.1 – 0.25
- Poor    : > 0.25

**Penyebab CLS tinggi:**
- Gambar/video tanpa dimensi eksplisit (width/height)
- Konten yang diinjeksi secara dinamis di atas konten yang ada
- Web font menyebabkan FOUT (Flash of Unstyled Text)
- Elemen yang diposisikan ulang saat load

**Cara cek:** Chrome DevTools > Performance > Layout Shift regions (warna biru)

---

## Data Audit Nyata — jakarta.telkomuniversity.ac.id

### Lighthouse (Chrome DevTools)
Diuji: Juni 2026

| Kategori       | Skor |
|----------------|------|
| Performance    | 90   |
| Accessibility  | 91   |
| Best Practices | 100  |
| SEO            | 100  |

### GTmetrix
Laporan: 8 Juni 2026
Server uji: Singapura
Browser: Chrome 142 | Lighthouse engine: 12.6.1

| Metrik      | Hasil  | Status |
|-------------|--------|--------|
| Grade       | A      | ✅     |
| Performance | 95%    | ✅     |
| Structure   | 95%    | ✅     |
| LCP         | 1.1s   | ✅     |
| TBT         | 10ms   | ✅     |
| CLS         | 0      | ✅     |

### Kenapa Lighthouse dan GTmetrix bisa beda?
- Lokasi server uji berbeda (GTmetrix: Singapura)
- Kondisi jaringan saat pengujian tidak identik
- GTmetrix menggunakan engine Lighthouse versi tersendiri
- Variasi normal — yang penting pola konsisten, bukan angka identik

---

## Tools untuk Audit Core Web Vitals

| Tool | URL | Keterangan |
|------|-----|------------|
| PageSpeed Insights | pagespeed.web.dev | Gabungan Lab + Field data |
| Chrome DevTools | Built-in Chrome | Detail per metrik, real-time |
| GTmetrix | gtmetrix.com | Test dari berbagai lokasi server |
| WebPageTest | webpagetest.org | Multi-location, waterfall detail |
| Search Console | search.google.com/search-console | Field data dari pengguna nyata |

**Rekomendasi urutan penggunaan:**
1. PageSpeed Insights — cek kondisi awal, cepat
2. Chrome DevTools — debug spesifik per metrik
3. GTmetrix / WebPageTest — validasi dari lokasi berbeda

---

## Referensi

- Core Web Vitals resmi: https://web.dev/articles/vitals
- INP replacing FID: https://web.dev/blog/inp-cwv
- CLS calculation: https://web.dev/articles/cls
- LCP optimization: https://web.dev/articles/optimize-lcp
