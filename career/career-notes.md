# IT Career & Fresh Graduate — Catatan Teknis
> IT Insights · Minggu 5 · Juni 2026  
> Repo: seandyarozano/it-insights-notes

---

## Ringkasan Topik Minggu Ini

Minggu 5 membahas karir IT dari sudut pandang yang jarang diangkat: bukan daftar tools atau sertifikasi, tapi **gap antara pendidikan formal dan ekspektasi dunia kerja** — dan cara fresh graduate menjembataninya secara praktis.

---

## 1. Tiga Jalur Karir IT: Struktur Dasar

Secara umum, jalur karir IT profesional terbagi dalam tiga kategori besar:

### Technical Track
Fokus pada pendalaman keahlian teknis spesifik. Jalur paling banyak dimasuki fresh graduate.

Contoh posisi awal:
- Junior Software Developer / Backend / Frontend
- Junior Network Engineer
- IT Support / Helpdesk (entry point umum)
- Junior Data Analyst / Data Engineer

Pola perkembangan umum (tidak universal — bervariasi per perusahaan dan industri):
```
Junior → Mid-level → Senior → Lead/Principal → Staff/Architect
```

Catatan: pola ini tidak linier dan sangat dipengaruhi oleh ukuran perusahaan, industri, dan seberapa aktif seseorang membangun skill di luar jam kerja.

### Functional IT Track
Menggabungkan pemahaman IT dengan domain industri spesifik. Membutuhkan waktu lebih lama untuk membangun kredibilitas di dua bidang sekaligus, tapi lebih sulit digantikan karena kombinasi tersebut langka.

Contoh posisi:
- IT Business Analyst
- Systems Analyst
- IT Project Coordinator
- ERP Consultant (misal: SAP, Oracle — butuh sertifikasi vendor spesifik)

### Management Track
Bukan jalur langsung dari kampus — tapi penting dipahami sejak awal agar arah pengembangan diri lebih terarah.

Skill yang perlu dibangun paralel sejak posisi junior:
- Project management basics (bisa mulai dari Google Project Management Certificate — perlu verifikasi ketersediaan dan relevansi terbaru secara mandiri)
- Stakeholder communication
- Pemahaman budget dan prioritisasi teknis

---

## 2. Skill Gap: Kampus vs Dunia Kerja

Berdasarkan observasi lapangan di lingkungan kerja IT, beberapa skill yang sering diasumsikan sudah dikuasai fresh graduate tapi ternyata tidak:

### Troubleshooting Mandiri
Kemampuan menghadapi error yang belum pernah dilihat sebelumnya tanpa langsung bertanya ke senior. Ini bukan soal pengetahuan — tapi soal *proses berpikir*:

```
1. Baca error message dengan teliti (bukan skip)
2. Reproduksi masalah secara konsisten
3. Isolasi variabel — apa yang berubah sebelum masalah muncul?
4. Cek log (application log, system log, network log)
5. Search error message + konteks spesifik (bukan hanya copy-paste error)
6. Dokumentasikan temuan, termasuk dead end
```

### Dokumentasi Teknis
Yang dimaksud bukan laporan skripsi — tapi dokumentasi yang bisa dipakai orang lain tanpa harus tanya kamu:

Elemen minimal dokumentasi teknis yang baik:
- **What**: apa yang sistem/script/konfigurasi ini lakukan
- **Why**: kenapa dibuat (konteks bisnis/teknis)
- **How**: cara menjalankan / cara setup
- **Known issues**: limitasi yang sudah diketahui
- **Last updated**: tanggal dan nama

### Version Control Dasar (Git)
Bukan hanya untuk developer. Relevan untuk:
- Pengelolaan konfigurasi server
- Dokumentasi teknis yang berubah seiring waktu
- Kolaborasi tim IT (bukan hanya dev team)

Perintah dasar yang wajib dikuasai fresh graduate IT:

```bash
# Clone repo
git clone https://github.com/username/repo.git

# Cek status perubahan
git status

# Stage perubahan
git add .
git add nama-file.md  # lebih spesifik, lebih aman

# Commit dengan pesan yang deskriptif
git commit -m "feat: tambah dokumentasi setup VPN"

# Push ke remote
git push origin main

# Buat branch baru (hindari kerja langsung di main)
git checkout -b feature/nama-fitur

# Cek log perubahan
git log --oneline

# Lihat perbedaan sebelum commit
git diff
```

Konvensi pesan commit yang umum dipakai (Conventional Commits):
```
feat:     fitur baru
fix:      perbaikan bug
docs:     perubahan dokumentasi
chore:    maintenance, tidak ada perubahan fungsional
refactor: refactoring kode tanpa perubahan behaviour
```

---

## 3. Membangun Portofolio IT Tanpa Pengalaman Kerja

### Kontribusi Open Source
Tidak harus langsung membuat fitur baru. Entry point yang realistis:

- **Good first issue**: cari label ini di GitHub — biasanya issue yang dirancang untuk kontributor baru
- **Dokumentasi**: banyak project open source kekurangan dokumentasi yang baik
- **Bug report**: melaporkan bug dengan reproduksi steps yang jelas sudah merupakan kontribusi

Cara cari project yang ramah kontributor baru:
```
# Di GitHub, gunakan filter search:
good-first-issues:>5 language:python  # ganti bahasa sesuai keahlian
```

Atau gunakan: https://goodfirstissue.dev (perlu verifikasi ketersediaan)

### Proyek dengan Pengguna Nyata
Yang membedakan proyek portofolio yang kuat: ada pengguna nyata yang bergantung padanya, meski hanya 3 orang.

Ide realistis untuk fresh graduate IT:
- Website sederhana untuk UMKM / organisasi nirlaba di sekitar kamu
- Script otomatisasi untuk kebutuhan organisasi kampus (backup, laporan, notifikasi)
- Dashboard monitoring sederhana untuk kebutuhan internal komunitas

Yang harus ada di README setiap proyek portofolio:
```markdown
## Tentang Proyek Ini
[Masalah apa yang diselesaikan]

## Pengguna Aktual
[Siapa yang pakai, berapa orang, sejak kapan]

## Tech Stack
[Apa yang dipakai dan kenapa]

## Setup
[Cara menjalankan — step by step]

## Screenshots / Demo
[Bukti visual bahwa ini berjalan]
```

---

## 4. Hal yang Menentukan Karir Jangka Panjang

### Komunikasi Teknis ke Non-Teknis
Skill ini tidak diajarkan di kampus tapi sangat dibutuhkan di dunia kerja. Strukturnya sederhana:

```
SITUASI → DAMPAK → OPSI → REKOMENDASI
```

Contoh konkret — melaporkan downtime ke atasan non-teknis:

❌ Buruk:
"Server mengalami high CPU usage karena memory leak di aplikasi dan perlu restart service."

✅ Lebih baik:
"Sistem tadi lambat selama ±20 menit karena ada bagian program yang tidak melepas memori dengan benar. 
Sudah ditangani dengan restart layanan. Dampak: user tidak bisa login selama periode itu. 
Kami sedang investigasi akar masalah dan akan update dalam 2 jam."

### Rasa Ingin Tahu sebagai Sistem
Teknologi berubah cepat — tidak mungkin dikuasai semua dari kampus. Yang membedakan bukan berapa banyak yang dikuasai, tapi seberapa cepat bisa belajar hal baru.

Sistem belajar yang sustainable untuk fresh graduate IT:
- **1 topik baru per bulan** — dalam, bukan melebar ke mana-mana
- **Learning in public** — tulis apa yang dipelajari (blog, GitHub notes, LinkedIn)
- **Terapkan segera** — project kecil lebih efektif dari kursus tanpa output

---

## 5. Sumber Referensi

- Stack Overflow Developer Survey 2024 — https://survey.stackoverflow.co/2024/ (data skill dan salary global)
- roadmap.sh — https://roadmap.sh (visual roadmap per jalur karir IT: frontend, backend, devops, dll) — perlu verifikasi ketersediaan
- GitHub Skills — https://skills.github.com (pembelajaran Git dan GitHub interaktif) — perlu verifikasi ketersediaan
- Artikel blog terkait: https://seandyarozano.staff.telkomuniversity.ac.id

---

## Catatan Teknis Tambahan

File ini adalah catatan teknis yang lebih dalam dari konten IT Insights Minggu 5. Konten publik (LinkedIn, Instagram, Threads, Blog TU) membahas topik yang sama dengan angle yang lebih accessible untuk audience umum.

Untuk konten minggu sebelumnya:
- `networking/` → Minggu 1: routing table, DNS
- `web-dev/` → Minggu 2: website performance, SEO basics
- `cybersecurity/` → Minggu 3: credential stuffing, 2FA, phishing
- `ai-productivity/` → Minggu 4: prompt engineering, AI tools

---

*Diperbarui: Juni 2026 | @seandyarozano*
