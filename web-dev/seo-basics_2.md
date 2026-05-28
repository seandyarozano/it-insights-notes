# SEO Basics — Catatan Teknis
> Catatan pendamping konten IT Insights Minggu 2
> Fokus: SEO teknis yang relevan untuk developer dan praktisi IT

---

## Apa itu SEO Teknis?

SEO (Search Engine Optimization) punya dua sisi:

| Sisi | Contoh | Siapa yang urus |
|------|--------|-----------------|
| **Content SEO** | Kata kunci, kualitas artikel, judul | Writer / marketer |
| **Technical SEO** | Kecepatan, struktur HTML, indexing | Developer / IT |

Catatan ini fokus ke sisi teknis — hal-hal yang bisa dikontrol dari sisi kode dan infrastruktur.

---

## Bagaimana Google Menemukan dan Menilai Website

Proses sederhana yang perlu dipahami:

```
Crawling → Indexing → Ranking
```

1. **Crawling** — Googlebot "mengunjungi" halaman kamu lewat link
2. **Indexing** — Konten disimpan dan dianalisis di database Google
3. **Ranking** — Halaman diberi peringkat berdasarkan ratusan faktor

**Faktor teknis yang memengaruhi ranking:**
- Kecepatan halaman (Core Web Vitals)
- Mobile-friendliness
- HTTPS (keamanan)
- Struktur URL yang bersih
- Tidak ada broken links
- Sitemap dan robots.txt yang benar

---

## Core Web Vitals dan SEO

Sejak update Google 2021, Core Web Vitals menjadi faktor ranking resmi.

| Metrik | Target | Dampak ke UX |
|--------|--------|--------------|
| LCP (Largest Contentful Paint) | < 2.5 detik | Konten utama lambat muncul = user kabur |
| INP (Interaction to Next Paint) | < 200ms | Klik tidak responsif = frustrasi |
| CLS (Cumulative Layout Shift) | < 0.1 | Layout geser saat loading = salah klik |

> LCP dan CLS berdampak langsung ke **bounce rate** (orang yang langsung keluar). Bounce rate tinggi memberi sinyal negatif ke Google.

---

## Struktur HTML yang Baik untuk SEO

### Heading Hierarchy
```html
<h1>Judul Utama Halaman</h1>     <!-- Hanya 1 per halaman -->
  <h2>Sub Topik Besar</h2>
    <h3>Detail dari Sub Topik</h3>
  <h2>Sub Topik Besar Lain</h2>
```

**Aturan penting:**
- Hanya ada **1 tag `<h1>`** per halaman
- Urutan hierarki tidak boleh dilewati (h1 → h2 → h3, bukan h1 → h3)
- Heading bukan untuk styling — gunakan CSS untuk itu

### Meta Tags Penting
```html
<head>
  <!-- Title: tampil di tab browser dan hasil pencarian -->
  <title>Judul Halaman | Nama Website</title>

  <!-- Description: tampil di bawah judul di hasil pencarian -->
  <meta name="description" content="Deskripsi singkat 150-160 karakter. Ini yang dilihat user sebelum klik.">

  <!-- Canonical: mencegah duplicate content -->
  <link rel="canonical" href="https://example.com/halaman-ini/">

  <!-- Open Graph: tampilan saat dibagikan di media sosial -->
  <meta property="og:title" content="Judul untuk Media Sosial">
  <meta property="og:description" content="Deskripsi untuk Media Sosial">
  <meta property="og:image" content="https://example.com/thumbnail.jpg">
</head>
```

---

## robots.txt dan sitemap.xml

### robots.txt
File di root domain yang memberitahu crawler mana yang boleh/tidak boleh diakses.

```
# Contoh robots.txt sederhana
User-agent: *
Allow: /
Disallow: /admin/
Disallow: /private/

Sitemap: https://example.com/sitemap.xml
```

> **Hati-hati:** `Disallow: /` (tanpa path) berarti MELARANG semua crawler. Ini sering jadi kesalahan yang tidak disadari.

### sitemap.xml
Peta halaman yang membantu Google menemukan semua konten.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
    <lastmod>2026-05-01</lastmod>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://example.com/blog/</loc>
    <lastmod>2026-05-20</lastmod>
    <priority>0.8</priority>
  </url>
</urlset>
```

Untuk WordPress: plugin **Yoast SEO** atau **Rank Math** generate sitemap otomatis.

---

## HTTPS dan Keamanan

HTTPS bukan hanya untuk toko online — Google menjadikannya faktor ranking sejak 2014.

**Cek status:** Lihat ikon gembok di address bar browser.

**Cara aktifkan:** Hampir semua hosting modern menyediakan SSL gratis via **Let's Encrypt**. Di cPanel biasanya ada menu "SSL/TLS" atau "Let's Encrypt".

---

## URL yang SEO-Friendly

```
# Buruk
https://example.com/p=123
https://example.com/halaman?id=456&cat=7

# Baik
https://example.com/tips-website-cepat/
https://example.com/blog/seo-untuk-pemula/
```

**Prinsip URL yang baik:**
- Menggunakan kata-kata yang deskriptif
- Huruf kecil semua
- Pemisah dengan tanda `-` (bukan `_`)
- Singkat tapi informatif
- Tidak ada karakter khusus yang tidak perlu

---

## Tools SEO Teknis Gratis

| Tool | Fungsi |
|------|--------|
| [Google Search Console](https://search.google.com/search-console) | Pantau indexing, error crawl, performa di pencarian |
| [PageSpeed Insights](https://pagespeed.web.dev) | Cek Core Web Vitals |
| [Screaming Frog](https://www.screamingfrog.co.uk/seo-spider/) | Audit teknis seluruh website (free hingga 500 URL) |
| [GTmetrix](https://gtmetrix.com) | Analisis performa + rekomendasi |
| [Ahrefs Webmaster Tools](https://ahrefs.com/webmaster-tools) | Backlink + error teknis (free untuk pemilik website) |

---

## Checklist SEO Teknis Dasar

- [ ] Website menggunakan HTTPS
- [ ] Satu `<h1>` per halaman
- [ ] Meta title dan description diisi semua halaman (title 50-60 karakter, description 150-160 karakter)
- [ ] robots.txt ada dan tidak memblokir halaman penting
- [ ] sitemap.xml ada dan sudah di-submit ke Google Search Console
- [ ] Tidak ada broken links (cek dengan Screaming Frog atau Ahrefs)
- [ ] Website mobile-friendly (cek di [search.google.com/test/mobile-friendly](https://search.google.com/test/mobile-friendly))
- [ ] Core Web Vitals dalam batas baik (cek di Google Search Console)
- [ ] Gambar punya attribute `alt` yang deskriptif
- [ ] URL menggunakan format yang bersih dan deskriptif

---

## Referensi

- [Google Search Central Documentation](https://developers.google.com/search/docs)
- [Core Web Vitals — web.dev](https://web.dev/vitals/)
- [Google Search Console Help](https://support.google.com/webmasters)
- [MDN — SEO](https://developer.mozilla.org/en-US/docs/Glossary/SEO)

---

*Catatan ini dibuat sebagai pendamping konten LinkedIn & Instagram Minggu 2 — IT Insights series oleh [@seandyarozano](https://github.com/seandyarozano)*
