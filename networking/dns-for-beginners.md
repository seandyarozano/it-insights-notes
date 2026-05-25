# DNS untuk Pemula: Buku Telepon Internet

> Bagian dari seri IT Insights Notes — penjelasan teknis dalam bahasa sederhana

---

## Apa itu DNS?

DNS (Domain Name System) adalah sistem yang menerjemahkan nama domain
yang mudah diingat manusia (seperti `google.com`) menjadi alamat IP
yang dimengerti komputer (seperti `142.250.185.78`).

**Analoginya:** DNS adalah buku telepon internet.

Saat kamu ketik `google.com` di browser, komputer tidak tahu itu siapa.
DNS yang mencari: *"Oh, google.com itu alamatnya 142.250.185.78 — sampaikan ke sana."*

Tanpa DNS → kamu harus hafal alamat IP setiap website yang ingin dikunjungi.
Tidak ada yang mau melakukan itu.

---

## Cara Kerja DNS — Step by Step

```
Kamu ketik: google.com
      ↓
① Browser cek cache lokal
  → Pernah visit sebelumnya? Pakai yang tersimpan.
  → Belum ada? Lanjut ke langkah berikutnya.
      ↓
② Tanya Recursive Resolver (biasanya dari ISP atau 8.8.8.8)
  → "Hei, siapa itu google.com?"
      ↓
③ Resolver tanya Root Nameserver
  → "Siapa yang bertanggung jawab atas domain .com?"
      ↓
④ Root arahkan ke TLD Nameserver (.com)
  → "Google ada di sini."
      ↓
⑤ TLD arahkan ke Authoritative Nameserver Google
  → "Ini alamat IP-nya: 142.250.185.78"
      ↓
⑥ IP address dikirim ke browser
  → Browser buka google.com menggunakan IP tersebut
      ↓
⑦ Hasil disimpan di cache
  → Kunjungan berikutnya lebih cepat
```

Seluruh proses ini biasanya selesai dalam **20–120 milidetik**.

---

## Komponen Utama DNS

| Komponen | Fungsi | Analogi |
|----------|--------|---------|
| **DNS Resolver** | Perantara antara pengguna dan DNS server | Operator telepon yang bantu carikan nomor |
| **Root Nameserver** | Titik awal pencarian — ada 13 cluster di dunia | Kantor pusat buku telepon |
| **TLD Nameserver** | Mengelola domain seperti `.com`, `.id`, `.net` | Bagian per kategori di buku telepon |
| **Authoritative NS** | Penyimpan data DNS final sebuah domain | Halaman spesifik yang berisi nomor yang dicari |
| **DNS Cache** | Hasil pencarian yang disimpan sementara | Catatan nomor yang sudah pernah dicari |

---

## Jenis-Jenis DNS Record

| Record | Fungsi | Contoh |
|--------|--------|--------|
| **A** | Domain → alamat IPv4 | `google.com → 142.250.185.78` |
| **AAAA** | Domain → alamat IPv6 | `google.com → 2404:6800:4004::200e` |
| **CNAME** | Alias — domain ke domain lain | `www.example.com → example.com` |
| **MX** | Mengarahkan email ke mail server | `@example.com → mail.example.com` |
| **TXT** | Verifikasi dan informasi tambahan | SPF, DKIM, Google verification |
| **NS** | Nameserver yang bertanggung jawab atas domain | `example.com → ns1.cloudflare.com` |
| **PTR** | Kebalikan A record — IP → domain (reverse DNS) | `142.250.185.78 → google.com` |
| **SOA** | Start of Authority — informasi zona DNS | Serial, refresh, retry, expire |

---

## TTL — Time To Live

TTL adalah berapa lama (dalam detik) sebuah DNS record boleh di-cache
sebelum harus dicek ulang ke server.

```
TTL 3600  = cache selama 1 jam
TTL 86400 = cache selama 24 jam
TTL 300   = cache selama 5 menit
```

**Implikasinya:**
- TTL tinggi → perubahan DNS butuh waktu lama untuk menyebar ke seluruh internet
- TTL rendah → perubahan lebih cepat tersebar, tapi lebih banyak query ke server
- Saat mau migrasi server: turunkan TTL ke 300 dulu, baru ganti IP

---

## DNS Publik yang Populer

| Provider | DNS Primer | DNS Sekunder | Keunggulan |
|----------|-----------|--------------|------------|
| Google | 8.8.8.8 | 8.8.4.4 | Cepat, stabil, global |
| Cloudflare | 1.1.1.1 | 1.0.0.1 | Tercepat, privacy-focused |
| OpenDNS | 208.67.222.222 | 208.67.220.220 | Filtering konten |
| Quad9 | 9.9.9.9 | 149.112.112.112 | Blokir malware otomatis |
| DNS Kominfo | 103.71.112.212 | 8.8.8.8 | Server lokal Indonesia |

---

## Studi Kasus: Cloudflare Down — 18 November 2025

Saat Cloudflare mengalami gangguan besar, DNS server mereka ikut terdampak.
Akibatnya:

- ChatGPT, X (Twitter), Spotify tidak bisa diakses
- Browser menampilkan error, seolah website tidak ada
- Padahal server-server tersebut masih berjalan normal

**Yang sebenarnya terjadi:** DNS tidak bisa menerjemahkan nama domain ke IP.
Browser tidak tahu harus ke mana. Website "hilang" dari internet — bukan karena
servernya mati, tapi karena "buku teleponnya" tidak merespons.

Seperti kamu mau telepon seseorang tapi semua kontak di HP kamu tiba-tiba terhapus.
Nomornya masih ada di dunia — tapi kamu tidak bisa menemukannya.

**Pelajaran:** DNS adalah infrastruktur paling kritis tapi paling sering diabaikan.

---

## Perintah Dasar di Terminal

```bash
# Cek DNS record sebuah domain
nslookup google.com

# Lebih detail dengan dig
dig google.com

# Cek record tipe tertentu
dig google.com MX          # cek mail server
dig google.com NS          # cek nameserver
dig google.com TXT         # cek TXT record

# Cek dari DNS server tertentu (bypass DNS default)
dig @8.8.8.8 google.com
dig @1.1.1.1 google.com

# Cek TTL
dig google.com +ttl

# Cek semua record sekaligus
dig google.com ANY

# Reverse DNS lookup (IP → domain)
dig -x 142.250.185.78

# Di Windows (nslookup)
nslookup google.com 8.8.8.8
```

---

## Troubleshooting DNS Umum

### Website tidak bisa dibuka, tapi internet lancar
```bash
# Langkah 1: Cek apakah DNS-nya yang bermasalah
nslookup google.com

# Kalau gagal → masalah DNS
# Coba ganti DNS sementara ke 8.8.8.8

# Langkah 2: Coba akses pakai IP langsung
# Buka browser → ketik IP langsung (contoh: 142.250.185.78)
# Kalau bisa → konfirmasi masalah ada di DNS

# Langkah 3: Flush DNS cache
ipconfig /flushdns          # Windows
sudo dscacheutil -flushcache  # Mac
sudo systemd-resolve --flush-caches  # Linux
```

### DNS lambat
```bash
# Bandingkan waktu respons DNS
dig @8.8.8.8 google.com | grep "Query time"
dig @1.1.1.1 google.com | grep "Query time"
dig @103.71.112.212 google.com | grep "Query time"

# Pilih yang paling kecil angka milidetiknya
```

---

## DNS dan Keamanan

### DNS Spoofing / Cache Poisoning
Penyerang memasukkan data palsu ke DNS cache → pengguna diarahkan
ke website palsu meski mengetik alamat yang benar.

**Perlindungan:** DNSSEC (DNS Security Extensions) — menambah
tanda tangan digital pada DNS record.

### DNS over HTTPS (DoH)
Query DNS dienkripsi menggunakan HTTPS, sehingga ISP tidak bisa
memantau website apa yang kamu kunjungi.

**Cara aktifkan di browser:** Settings → Privacy → DNS over HTTPS → Aktifkan

### DNS Filtering
DNS yang memblokir domain berbahaya sebelum koneksi terjadi.
Cloudflare 1.1.1.1 for Families dan Quad9 menggunakan pendekatan ini.

---

## Kesimpulan

DNS adalah salah satu infrastruktur internet yang paling fundamental —
ada di balik setiap klik, setiap buka aplikasi, setiap kirim email.

Ketika DNS bermasalah, internet terasa "mati" meski koneksinya baik-baik saja.
Memahami DNS membantu kamu:
- Troubleshoot masalah koneksi lebih cepat
- Mengerti kenapa website bisa "hilang" dari internet
- Membuat keputusan lebih baik soal privasi dan keamanan digital

**Sederhananya: DNS adalah pondasi yang menopang internet modern.**

---

## Kaitannya dengan Konten

- Post LinkedIn Minggu 1: [Pelajaran Networking dari Kehidupan Sehari-hari](https://linkedin.com/in/seandyarozano)
- Post LinkedIn Minggu 1 (Kamis): [Cloudflare Down 5,5 Jam — Bukan Di-hack](https://linkedin.com/in/seandyarozano)
- Artikel Medium: [Penyebab Cloudflare Down 18 November 2025](https://medium.com/@seandyarozano)
- File terkait: [`routing-table-explained.md`](./routing-table-explained.md)

---

*IT Insights Notes · [github.com/seandyarozano/it-insights-notes](https://github.com/seandyarozano/it-insights-notes)*
