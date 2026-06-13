# AI & Produktivitas — Catatan Teknis Minggu 4

> Repo: `seandyarozano/it-insights-notes`
> Folder: `ai-productivity/`
> Filename: `ai-productivity-notes.md`
> Periode: 9–14 Juni 2026

---

## Ringkasan Tema Minggu Ini

**Spine:** Kualitas output AI = kualitas brief, bukan pilihan tools.

Minggu ini membahas bagaimana cara memberikan instruksi (prompt) ke AI secara spesifik berdampak langsung pada kualitas dan kegunaan output — lebih dari sekadar memilih tools mana yang dipakai.

---

## Konsep Teknis: Prompt Engineering Dasar

### Apa itu prompt?

Prompt adalah instruksi natural language yang diberikan ke Large Language Model (LLM) sebelum model menghasilkan output. LLM tidak "mengerti" dalam arti manusiawi — model memprediksi token berikutnya berdasarkan distribusi probabilitas dari training data. Artinya:

- **Konteks yang lebih spesifik** → distribusi probabilitas output lebih sempit → hasil lebih terarah
- **Konteks yang kabur** → model jatuh ke distribusi probabilitas yang paling umum → output generik

Ini secara teknis menjelaskan kenapa brief yang spesifik menghasilkan output lebih baik.

### Komponen prompt yang efektif

Berdasarkan dokumentasi resmi Google (Prompt Design Strategies) dan OpenAI (Prompt Engineering Guide), komponen standar prompt yang menghasilkan output optimal:

```
[PERSONA / ROLE]     → Siapa yang berbicara / konteks diri
[TASK]               → Instruksi spesifik + tujuan
[CONTEXT]            → Informasi latar yang relevan
[FORMAT]             → Bentuk output yang diinginkan
[CONSTRAINT]         → Batasan (panjang, nada, bahasa, dll.)
```

Tidak semua komponen wajib ada di setiap prompt — tapi semakin banyak yang disertakan untuk tugas yang kompleks, semakin konsisten hasilnya.

### Contoh perbandingan prompt

**Prompt tanpa struktur:**
```
Buatkan laporan bulanan tim IT.
```

**Prompt dengan struktur:**
```
Kamu membantu seorang Kepala Seksi IT di perguruan tinggi.

Tugas: Buat template ringkasan laporan bulanan yang bisa diisi 
oleh tiap PIC (person in charge) untuk program kerja mereka.

Konteks: Laporan akan dibaca oleh kepala unit yang tidak berlatar 
belakang IT — bahasa harus mudah dipahami.

Format: Tabel dengan kolom:
- Nama program kerja
- Target bulan ini
- Capaian aktual (%)
- Kendala yang dihadapi
- Rencana tindak lanjut

Batasan: Bahasa Indonesia formal, bukan teknis.
```

**Perbedaan output:** Prompt pertama menghasilkan teks generik. Prompt kedua menghasilkan template tabel yang langsung bisa dipakai tim.

---

## Tools AI yang Dibahas Minggu Ini

| Tool | Use case utama | Model dasar | Catatan |
|------|----------------|-------------|---------|
| **Claude** (Anthropic) | Long-form writing, analisis dokumen, coding iteratif | Claude 3.x / 4.x | Sangat baik untuk instruksi panjang dan kompleks |
| **ChatGPT** (OpenAI) | Percakapan, drafting, brainstorming | GPT-4o | Plugin/tools ecosystem luas |
| **Gemini** (Google) | Integrasi Google Workspace, riset | Gemini 1.5 / 2.x | Native di Google Docs, Sheets, Gmail |
| **Perplexity** | Riset dengan sumber terverifikasi | Multi-model | Menyertakan source citations di free plan |
| **Gamma.app** | Presentasi otomatis dari teks | Proprietary | Free plan tersedia — bukan sepenuhnya gratis |

> **Catatan verifikasi:** Klaim fitur free/berbayar perlu dicek ulang secara berkala karena pricing model tools AI berubah cepat. Terakhir diverifikasi Juni 2026.

---

## Teknis: Cara LLM "Membaca" Prompt

### Tokenisasi

LLM tidak membaca karakter — model membaca *token*. Satu token ≈ 3–4 karakter dalam Bahasa Inggris, bisa berbeda untuk Bahasa Indonesia (cenderung lebih banyak token per kata karena corpus training lebih kecil).

Implikasi praktis:
- Prompt panjang = lebih banyak token = lebih mahal di API berbayar
- Kata-kata Bahasa Indonesia tertentu di-tokenize berbeda antar model
- Context window (batas maksimum input+output) dihitung dalam token, bukan karakter

### Temperature & Determinisme

Parameter `temperature` mengontrol seberapa "kreatif" atau "acak" output model:

```
temperature = 0.0  → deterministik, output hampir selalu sama
temperature = 0.7  → balanced (default kebanyakan model)
temperature = 1.0+ → sangat kreatif, bisa tidak konsisten
```

Untuk tugas yang butuh konsistensi (laporan, template, data extraction) → gunakan temperature rendah.
Untuk brainstorming dan konten kreatif → temperature lebih tinggi lebih baik.

*Catatan: parameter ini tidak tersedia di chat interface standar (ChatGPT, Claude.ai) — hanya di API.*

### Context Window — Batas yang Sering Diabaikan

Setiap model punya batas maksimum token yang bisa diproses dalam satu sesi:

| Model | Context window (approx.) |
|-------|--------------------------|
| GPT-4o | 128K token |
| Claude 3.5 Sonnet | 200K token |
| Gemini 1.5 Pro | 1M token |

Implikasi: untuk dokumen sangat panjang, pilih model dengan context window besar. Kalau dokumen melebihi batas, model akan "lupa" bagian awal percakapan.

---

## Iterasi sebagai Metode Kerja

Satu hal yang sering diabaikan: AI bukan mesin one-shot. Output terbaik hampir selalu hasil dari beberapa putaran iterasi:

```
Draft pertama → identifikasi yang kurang → revisi prompt → draft kedua → dst.
```

Contoh workflow iterasi yang dipakai untuk membangun dashboard monitoring kinerja tim (kasus nyata Minggu 4):

```
Iterasi 1: Minta struktur dasar → hasilnya terlalu generik
Iterasi 2: Tambah konteks spesifik (siapa usernya, data apa yang diinput) → lebih baik
Iterasi 3: Minta penyesuaian tampilan dan logika filter → mendekati kebutuhan
```

Total: 3 hari iterasi untuk dashboard yang fungsional dan langsung dipakai aktif — tanpa background pengembangan aplikasi.

**Key insight:** Semakin spesifik brief di iterasi pertama, semakin sedikit putaran yang dibutuhkan.

---

## Referensi

| Sumber | URL | Catatan |
|--------|-----|---------|
| OpenAI Prompt Engineering Guide | `platform.openai.com/docs/guides/prompt-engineering` | Dokumentasi resmi, perlu akun OpenAI untuk akses penuh |
| Google — Prompt Design Strategies | `ai.google.dev/gemini-api/docs/prompting-strategies` | Dokumentasi resmi Google AI for Developers, diperbarui Juni 2026 |
| Google Workspace Gemini Prompt Guide | `workspace.google.com/learning/content/gemini-prompt-guide` | Lebih accessible, tidak butuh akun developer |
| Anthropic — Prompt Engineering | `docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview` | Dokumentasi resmi Claude |

> **Catatan:** Semua URL diverifikasi aktif per Juni 2026. Cek ulang sebelum membagikan ke orang lain — dokumentasi AI berubah cepat.

---

## Konten Minggu Ini (Referensi Lintas Platform)

- **LinkedIn anchor (Senin):** Transformation story — dashboard monitoring kinerja tim PuTI TUJ dibangun dengan AI tanpa background dev
- **Instagram Carousel (Selasa):** 5 Tools AI yang Benar-Benar Kerja (ChatGPT, Claude, Gemini, Perplexity, Gamma)
- **LinkedIn pendek (Rabu):** Prompt engineering sebagai skill komunikasi ke mesin
- **Threads Prompt Breakdown:** Rotasi ChatGPT (Sen/Rab/Kam) dan Gemini (Sel/Kam) — tema brief AI untuk komunikasi profesional
- **LinkedIn opini (Jumat):** AI & Produktivitas — list/opini
- **Blog TU (Sabtu):** [Cara Brief AI yang Efektif](https://seandyarozano.staff.telkomuniversity.ac.id) — artikel SEO lengkap

---

*Catatan teknis ini adalah versi lebih dalam dari konten IT Insights Minggu 4. Untuk versi yang lebih mudah dibaca, kunjungi [seandyarozano.staff.telkomuniversity.ac.id](https://seandyarozano.staff.telkomuniversity.ac.id)*
