# Minggu 6 — Networking & Infrastruktur Pendalaman (Siklus 2)

**Periode:** 23–29 Juni 2026
**Tema:** Networking & Infrastructure — Siklus 2 (Pendalaman)
**Platform:** LinkedIn, Instagram, Threads, Blog TU

---

## Ringkasan Topik Minggu Ini

Minggu ini membahas networking dari sudut pendalaman — bukan ulang teori dasar,
tapi pattern recognition dan masalah nyata yang sering terjadi di lingkungan
infrastruktur kampus.

Lima angle yang dibahas:
1. ISP-blame reflex — masalah bukan selalu dari provider
2. Switch EOL dan dampaknya ke performa AP
3. Monitoring aktif vs pasif — visibility adalah fondasi
4. Troubleshooting steps yang benar sebelum hubungi helpdesk
5. Mitos-mitos umum tentang jaringan kantor

---

## Konsep Teknis yang Dibahas

### 1. ISP-Blame Reflex (Senin)

Kecenderungan menyalahkan provider saat koneksi bermasalah adalah pola yang
paling umum di lingkungan non-IT. Padahal jalur koneksi panjang:

```
ISP → Router → Switch → Access Point → End Device
```

Masalah bisa terjadi di titik mana saja. Cara validasi cepat:

```bash
# Cek latensi ke gateway lokal dulu sebelum tuduh ISP
ping 192.168.1.1

# Bandingkan latensi ke DNS publik
ping 8.8.8.8

# Traceroute untuk lihat di mana paket mulai lambat
traceroute 8.8.8.8
# Windows:
tracert 8.8.8.8
```

Kalau `ping gateway` sudah lambat → masalah di jaringan internal.
Kalau `ping gateway` bagus tapi `ping 8.8.8.8` lambat → baru mungkin ISP.

---

### 2. Switch EOL dan Dampak ke Access Point (Selasa)

Case study nyata dari PuTI TUJ: switch distribusi berusia >5 tahun dan sudah
End of Life (EOL) menyebabkan performa AP di bawahnya tidak optimal, berujung
pada gangguan koneksi internet pengguna akhir.

**Kenapa EOL berbahaya:**
- Tidak ada patch firmware/security update
- Hardware degradasi: kapasitas switching menurun seiring waktu
- Tidak lagi didukung vendor → tidak ada troubleshooting resmi
- Throughput tidak mencapai spesifikasi karena hardware aging

**Jalur dampak:**
```
Switch Distribusi (EOL) → throughput terbatas
    → Access Point tidak dapat bandwidth penuh
        → User merasakan koneksi lambat / tidak stabil
```

**Solusi yang diambil:** Ganti switch distribusi dengan spesifikasi lebih tinggi.
Hasilnya: performa AP kembali optimal, keluhan user berkurang signifikan.

**Pelajaran:** Lifecycle management perangkat jaringan bukan hanya soal anggaran —
tapi soal risiko operasional. EOL bukan rekomendasi, tapi deadline.

---

### 3. Monitoring Aktif vs Pasif (Rabu)

**Monitoring pasif:** Menunggu ada yang melapor → baru cek.
**Monitoring aktif:** Sistem memantau secara real-time → notifikasi otomatis saat
ada anomali, bahkan sebelum user merasakan dampaknya.

**Implementasi di PuTI TUJ:**
- Tool: PRTG Network Monitor
- Coverage: 4 lokasi kampus, 200+ perangkat aktif
- Notifikasi: Telegram bot — alert langsung ke channel tim IT
- Manfaat: Masalah terdeteksi lebih awal, response time lebih cepat

**Kenapa ini penting:**
Pengguna biasanya tidak lapor masalah kecil — mereka refresh halaman,
restart laptop, dan lanjut bekerja. Tanpa monitoring aktif, masalah
kecil bisa jadi besar sebelum ada yang tahu.

**Metrik yang perlu dipantau minimal:**
- Uptime per perangkat
- Latensi antar node
- Packet loss rate
- Utilisasi bandwidth per segment
- Status port switch

**Tools open source alternatif (tidak wajib berbayar):**
- Zabbix — `https://www.zabbix.com`
- Nagios — `https://www.nagios.org`
- LibreNMS — `https://www.librenms.org`

---

### 4. Troubleshooting Steps Sebelum Hubungi Helpdesk (Kamis)

Flowchart sederhana untuk user non-IT saat mengalami masalah koneksi:

```
Koneksi bermasalah?
    │
    ▼
Cek perangkat lain di lokasi yang sama
    │
    ├─ Semua perangkat bermasalah? → Kemungkinan masalah jaringan/AP
    │                                 Hubungi IT helpdesk
    │
    └─ Hanya perangkat kamu? → Lanjut...
        │
        ▼
    Restart network adapter (bukan full restart laptop)
        │
        ├─ Solved? → Done
        │
        └─ Masih bermasalah?
            │
            ▼
        Forget WiFi network → reconnect ulang
            │
            ├─ Solved? → Done
            │
            └─ Masih bermasalah? → Baru hubungi IT helpdesk
                                   dengan info: perangkat apa,
                                   lokasi mana, sejak kapan
```

**Kenapa ini penting untuk tim IT:**
Setiap tiket yang masuk butuh waktu respons. Kalau user sudah lakukan
langkah dasar ini sebelum lapor, tim IT bisa fokus ke masalah yang
benar-benar butuh intervensi teknis.

---

### 5. Lima Mitos Jaringan Kantor (Jumat + Artikel Blog)

| # | Mitos | Fakta |
|---|-------|-------|
| 01 | Internet lambat = salah provider | Masalah bisa di mana saja di jalur jaringan internal |
| 02 | WiFi = jaringan sesungguhnya | WiFi hanya antarmuka — infrastruktur kabel yang menentukan |
| 03 | Tidak ada keluhan = aman | User diam bukan berarti tidak ada masalah |
| 04 | Tambah bandwidth = beres | Latensi dan packet loss tidak ikut naik dengan bandwidth |
| 05 | IT cukup 1 orang | Tanggung jawab tim IT terlalu kompleks untuk 1 orang |

**Artikel blog lengkap:**
`https://seandyarozano.staff.telkomuniversity.ac.id` (Sabtu, 28 Juni 2026)

---

## Referensi

- PRTG Network Monitor: `https://www.paessler.com/prtg`
- Zabbix open source monitoring: `https://www.zabbix.com`
- Nagios open source monitoring: `https://www.nagios.org`
- LibreNMS (alternatif Zabbix): `https://www.librenms.org`

> **Catatan:** Verifikasi semua URL di atas sebelum dijadikan referensi publik.
> URL bisa berubah sewaktu-waktu.

---

## Konten yang Diproduksi Minggu Ini

| Platform | Format | Topik |
|----------|--------|-------|
| LinkedIn | Anchor post | ISP-blame + pola diagnosis jaringan |
| LinkedIn | Post pendek | Monitoring aktif — PRTG + Telegram bot |
| LinkedIn | Post opini | 5 Mitos Jaringan Kantor |
| Instagram | Carousel (Varian C) | Case study switch EOL |
| Instagram | Reels (Varian A) | Monitoring jaringan — demo visual |
| Instagram | Infografis (Varian B) | 5 Mitos Jaringan Kantor |
| Threads | Prompt Breakdown (5 hari) | Senin–Jumat, rotasi ChatGPT/Gemini |
| Threads | Pure-Threads (Selasa, Kamis) | F1 Observasi Lapangan, F4 Realita vs Ekspektasi |
| Threads | Utas [1/5]–[5/5] | 5 Mitos Jaringan Kantor |
| Blog TU | Artikel SEO | 5 Mitos Jaringan Kantor (~900 kata) |
