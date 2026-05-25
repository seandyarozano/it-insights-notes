# SEO Basics: Bukan Sulap, Tapi Sains

> Bagian dari seri IT Insights Notes — penjelasan teknis dalam bahasa sederhana

---

## Apa itu SEO?

SEO (Search Engine Optimization) adalah proses mengoptimasi website agar
muncul di posisi teratas hasil pencarian Google — secara organik, tanpa bayar iklan.

Kata kuncinya: **organik**. SEO bukan iklan. Hasilnya tidak instan.
Tapi kalau dilakukan benar, efeknya bertahan bertahun-tahun.

Analoginya seperti **merapikan toko agar mudah ditemukan dan dipercaya**.
Iklan itu seperti pasang spanduk di jalan — begitu bayarnya berhenti, lalu lintas berhenti.
SEO seperti reputasi toko yang sudah dikenal orang — tidak hilang meski kamu tidak bayar.

---

## Cara Kerja Google (Sangat Disederhanakan)

```
1. CRAWLING
   Googlebot (robot Google) menjelajahi internet
   mengikuti link dari halaman ke halaman.
         ↓
2. INDEXING
   Halaman yang ditemukan dianalisis dan disimpan
   dalam database besar Google (index).
         ↓
3. RANKING
   Saat seseorang search, Google memilih halaman
   paling relevan dari index → ditampilkan di SERP.
```

**SERP** = Search Engine Results Page = halaman hasil pencarian.

---

## 3 Pilar SEO

### 1. Technical SEO
Memastikan website bisa di-crawl dan di-index dengan benar.

Yang termasuk technical SEO:
- **Kecepatan halaman** — Google memprioritaskan website yang cepat
- **Mobile-friendly** — > 60% pencarian dari mobile
- **HTTPS** — website tanpa SSL certificate dipenalti
- **Sitemap XML** — peta website untuk membantu Googlebot
- **Robots.txt** — instruksi halaman mana yang boleh di-crawl
- **Core Web Vitals** — LCP, INP, CLS (lihat: why-websites-are-slow.md)

### 2. On-Page SEO
Optimasi konten dan elemen HTML di dalam halaman.

| Elemen | Fungsi | Best Practice |
|--------|--------|---------------|
| Title Tag | Judul yang muncul di SERP | 50–60 karakter, mengandung keyword utama |
| Meta Description | Deskripsi di bawah judul SERP | 120–160 karakter, mengandung CTA |
| H1 | Heading utama halaman | Hanya satu per halaman, mengandung keyword |
| H2/H3 | Subheading | Mengandung keyword sekunder dan LSI |
| URL Slug | Alamat halaman | Pendek, deskriptif, pakai tanda hubung |
| Alt Text | Deskripsi gambar | Deskriptif, mengandung keyword jika relevan |
| Internal Link | Link ke halaman lain di website | Membantu distribusi "link juice" |

**Contoh Title Tag yang baik:**
```
❌ Home - Toko Online Kami
✓ Sepatu Lari Pria Terbaik 2025 | Toko Sepatu XYZ Cirebon
```

### 3. Off-Page SEO
Sinyal dari luar website yang membangun otoritas dan kepercayaan.

**Backlink** adalah yang paling penting:
- Link dari website lain ke website kamu = "suara" kepercayaan
- Kualitas > kuantitas: 1 backlink dari media besar > 100 dari website spam
- Cara dapat backlink natural: buat konten yang layak dikutip

**Faktor off-page lainnya:**
- Brand mention (disebut tanpa link pun dihitung)
- Social signals (share di media sosial)
- Google Business Profile (untuk bisnis lokal)

---

## Keyword Research — Fondasi SEO

Sebelum menulis konten, cari tahu apa yang dicari orang.

### Jenis Keyword

| Jenis | Contoh | Volume | Persaingan |
|-------|--------|--------|------------|
| Short-tail | "sepatu lari" | Sangat tinggi | Sangat ketat |
| Long-tail | "sepatu lari pria untuk aspal murah" | Rendah | Rendah |
| Local | "toko sepatu lari Cirebon" | Sedang | Rendah |
| Question | "apa sepatu lari terbaik untuk pemula" | Sedang | Sedang |

**Tips:** untuk website baru, targetkan **long-tail dan local keyword** dulu.
Lebih mudah ranking, lebih targeted, konversinya lebih tinggi.

### Tools Keyword Research Gratis
- **Google Search Console** — lihat keyword yang sudah bawa traffic
- **Google Keyword Planner** — butuh akun Google Ads
- **Ubersuggest** (free tier) — estimasi volume dan difficulty
- **AnswerThePublic** — keyword berbentuk pertanyaan
- **Google Autocomplete** — ketik keyword di Google, lihat saran

---

## Mitos SEO yang Sering Dipercaya

### ❌ "SEO bisa hasilkan ranking #1 dalam seminggu"
Tidak ada jaminan ranking dan tidak ada shortcut yang aman.
Hasil SEO organik butuh **3–6 bulan minimum** untuk terlihat signifikan.

### ❌ "Makin banyak keyword, makin bagus"
**Keyword stuffing** justru dipenalti Google. Satu keyword utama per halaman,
ditulis secara natural, jauh lebih efektif.

### ❌ "Meta keyword masih penting"
Google sudah **mengabaikan meta keyword** sejak 2009. Fokus ke title tag
dan meta description.

### ❌ "Beli backlink itu aman kalau tidak ketahuan"
Skema link berbayar melanggar Google Webmaster Guidelines.
Risikonya: penalti manual yang menghilangkan website dari index Google.

### ❌ "SEO itu sekali setting, selesai"
SEO adalah proses berkelanjutan. Algoritma Google update ratusan kali per tahun.
Konten yang tidak diperbarui bisa turun ranking.

---

## SEO untuk Pemula — Mulai dari Mana?

### Prioritas 1 (Minggu 1–2): Technical Foundation
- [ ] Pastikan website HTTPS
- [ ] Daftarkan ke Google Search Console
- [ ] Submit sitemap XML
- [ ] Cek mobile-friendliness: [search.google.com/test/mobile-friendly](https://search.google.com/test/mobile-friendly)
- [ ] Cek kecepatan di PageSpeed Insights

### Prioritas 2 (Minggu 3–4): On-Page Basics
- [ ] Optimasi title tag dan meta description setiap halaman
- [ ] Pastikan setiap halaman punya satu H1
- [ ] Tambahkan alt text ke semua gambar
- [ ] Buat URL yang deskriptif (bukan /page?id=123)

### Prioritas 3 (Bulan 2+): Konten dan Backlink
- [ ] Buat konten berkualitas secara konsisten
- [ ] Target long-tail keyword yang spesifik
- [ ] Bangun backlink dari direktori bisnis lokal
- [ ] Daftarkan ke Google Business Profile

---

## Tools SEO yang Wajib Tahu

| Tool | Fungsi | Harga |
|------|--------|-------|
| Google Search Console | Monitor performa di Google | Gratis |
| Google Analytics 4 | Analisis traffic website | Gratis |
| PageSpeed Insights | Cek kecepatan dan Core Web Vitals | Gratis |
| Screaming Frog (free) | Crawl website, cari broken link | Gratis s/d 500 URL |
| Ahrefs Webmaster Tools | Backlink dan keyword check | Gratis (limited) |
| Ubersuggest | Keyword research dan audit | Gratis (limited) |

---

## Perbedaan SEO vs SEM vs Social Media

| Aspek | SEO | SEM (Google Ads) | Social Media |
|-------|-----|-------------------|--------------|
| Biaya | Waktu + tenaga | Bayar per klik | Waktu + tenaga |
| Hasil | 3–6 bulan | Instan | Instan tapi volatile |
| Durasi | Jangka panjang | Berhenti jika tidak bayar | Tergantung algoritma |
| Intent | High (orang sedang cari) | High | Low–Medium |
| Terbaik untuk | Brand authority, konten | Promosi produk cepat | Awareness, engagement |

---

## Kaitannya dengan Konten

- Post LinkedIn Minggu 2: "SEO Bukan Sulap, Tapi Sains"
- Topik lanjutan: Core Web Vitals, Local SEO, SEO untuk UKM Indonesia
- Referensi: [Google Search Central](https://developers.google.com/search/docs)

---

*IT Insights Notes · [github.com/seandyarozano/it-insights-notes](https://github.com/seandyarozano/it-insights-notes)*
