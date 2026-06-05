# IT Insights Notes

Catatan teknis dari proyek konten **IT Insights** milik [@seandyarozano](https://github.com/seandyarozano).

Repo ini berisi versi teknis dan lebih dalam dari topik-topik yang dibahas di konten sosial mingguan — bukan copy-paste dari caption, tapi penjelasan mekanisme, referensi, dan snippet yang bisa langsung dipakai.

---

## Tentang IT Insights

**IT Insights** adalah proyek personal branding sekaligus edukasi publik oleh Seandy Arandiant Rozano — IT Section Head di Pusat Teknologi Informasi Telkom University Jakarta.

> "Teknologi bukan untuk orang IT saja."

Konten diterbitkan setiap minggu dengan topik berputar dalam 5 tema: Networking, Website & SEO, Cybersecurity, AI & Produktivitas, dan IT Career.

---

## Platform

| Platform | Link |
|---|---|
| LinkedIn | [linkedin.com/in/seandyarozano](https://www.linkedin.com/in/seandyarozano/) |
| Instagram | [instagram.com/seandyarozano](https://www.instagram.com/seandyarozano/) |
| Threads | [threads.net/@seandyarozano](https://www.threads.net/@seandyarozano) |
| Blog | [seandyarozano.staff.telkomuniversity.ac.id](https://seandyarozano.staff.telkomuniversity.ac.id) |

---

## Struktur Repo

```
it-insights-notes/
├── networking/          → Minggu 1, 6, 11
├── web-dev/             → Minggu 2, 7, 12
├── cybersecurity/       → Minggu 3, 8, 13
├── ai-productivity/     → Minggu 4, 9, 14
└── career/              → Minggu 5, 10, 15
```

---

## Progres Konten

### Siklus 1 — Fondasi (Minggu 1–5)

#### ✅ Minggu 1 — Networking & Infrastructure
**Periode:** 19–25 Mei 2026

| File | Topik |
|---|---|
| `networking/routing-table-explained.md` | Routing table untuk pemula — cara jaringan memilih jalur |
| `networking/dns-for-beginners.md` | DNS: buku telepon internet |

**Topik yang dibahas di konten sosial:**
- Broadcast vs unicast — analogi "teriak di ruangan vs bisik langsung"
- TCP Three-Way Handshake — bangun kepercayaan sebelum transaksi
- Packet loss — evaluasi jalur, bukan tambah frekuensi
- Cloudflare down 5,5 jam — satu konfigurasi salah bisa matikan internet sebagian dunia
- DNS dan routing table dijelaskan dengan analogi sehari-hari

**Artikel blog:**
- [Penyebab Cloudflare Down 18 November 2025](https://seandyarozano.staff.telkomuniversity.ac.id/penyebab-cloudflare-down-18-november-2025-bukan-serangan-hanya-satu-file-yang-membengkak/)
- [Routing Table Adalah: Pengertian, Fungsi, dan Cara Kerjanya](https://seandyarozano.staff.telkomuniversity.ac.id/routing-table-adalah-pengertian-fungsi-dan-cara-kerjanya-di-jaringan-komputer/)
- [Apa yang Jaringan Komputer Ajarkan Tentang Cara Kita Berkoneksi](https://seandyarozano.staff.telkomuniversity.ac.id/apa-yang-jaringan-komputer-ajarkan-tentang-cara-kita-berkoneksi/)

---

#### ✅ Minggu 2 — Website & SEO
**Periode:** 26 Mei – 1 Juni 2026

| File | Topik |
|---|---|
| `web-dev/website-performance-notes.md` | Core Web Vitals, PageSpeed, optimasi performa |
| `web-dev/seo-basics.md` | Dasar SEO teknis untuk pemula |

**Topik yang dibahas di konten sosial:**
- 3 lapisan kecepatan website: Si Kurir (internet), Si Dapur (server), Si Plating (render browser)
- 5 penyebab website lambat: gambar tidak dikompres, terlalu banyak plugin, font dari server luar, iklan berat, hosting tanpa CDN
- Demo PageSpeed Insights — website Telkom University Jakarta: skor 94/100
- Tool gratis: [pagespeed.web.dev](https://pagespeed.web.dev)

**Artikel blog:**
- [Kenapa Website Lambat Padahal Internet Kencang? Ini 5 Penyebabnya](https://seandyarozano.staff.telkomuniversity.ac.id/kenapa-website-lambat-padahal-internet-kencang-ini-5-penyebabnya/)

---

#### ✅ Minggu 3 — Cybersecurity
**Periode:** 1–7 Juni 2026

| File | Topik |
|---|---|
| `cybersecurity/cybersecurity-notes.md` | Human element, credential stuffing, phishing, 2FA, HIBP, Wi-Fi publik |

**Topik yang dibahas di konten sosial:**
- Human element dalam insiden siber — data Verizon DBIR 2025
- Credential stuffing — bahaya pakai password sama di banyak platform (analogi satu kunci semua pintu)
- Phishing modern — bukan "pangeran Nigeria" lagi, tapi spear phishing yang sangat meyakinkan
- Social engineering — kepanikan sebagai senjata psikologis
- 2FA: perbandingan SMS OTP vs authenticator app vs hardware key
- Demo HaveIBeenPwned — cek apakah email sudah bocor
- 5 kebiasaan digital yang diam-diam berbahaya

**Artikel blog:**
- [Ancaman Siber Sehari-hari yang Sering Kita Abaikan](https://seandyarozano.staff.telkomuniversity.ac.id/ancaman-siber-sehari-hari-yang-sering-kita-abaikan/)

---

### 🔲 Minggu 4 — AI & Produktivitas
*(Mulai: 8 Juni 2026)*

Topik yang akan dibahas:
- AI sebagai tools, bukan pengganti manusia
- Prompt engineering = skill komunikasi ke mesin
- Cara kerja LLM dengan analogi sederhana
- Tools AI yang benar-benar berguna vs yang overhype

---

### 🔲 Minggu 5 — IT Career & Fresh Graduate
*(Mulai: 15 Juni 2026)*

Topik yang akan dibahas:
- Fresh graduate IT vs senior developer — perbedaan mindset, bukan hanya skill
- Roadmap karir IT untuk yang baru mulai
- Skill IT yang dibutuhkan dunia kerja vs yang diajarkan di kampus
- Cara bangun portofolio IT tanpa pengalaman kerja

---

## Referensi Utama per Tema

| Tema | Referensi Terpercaya |
|---|---|
| Networking | [Cisco Networking Academy](https://www.netacad.com/), [RFC Editor](https://www.rfc-editor.org/) |
| Website & SEO | [web.dev](https://web.dev/), [PageSpeed Insights](https://pagespeed.web.dev/) |
| Cybersecurity | [Verizon DBIR](https://www.verizon.com/business/resources/reports/dbir/), [OWASP](https://owasp.org/), [HaveIBeenPwned](https://haveibeenpwned.com/) |
| AI & Produktivitas | [Anthropic Research](https://www.anthropic.com/research), [OpenAI Blog](https://openai.com/blog) |
| IT Career | [roadmap.sh](https://roadmap.sh/) |

---

## Prinsip Repo Ini

- **Akurasi dulu** — semua angka dan klaim dikaitkan ke sumber yang bisa diverifikasi
- **Bukan copy-paste konten sosial** — ini versi teknis yang lebih dalam
- **Referensi aktif** — link diverifikasi sebelum push
- **Update rutin** — push setiap Sabtu setelah artikel blog tayang

---

*Last updated: 7 Juni 2026 — Minggu 3 (Cybersecurity) selesai*
*Dibuat oleh [@seandyarozano](https://github.com/seandyarozano) | IT Section Head, Telkom University Jakarta*
