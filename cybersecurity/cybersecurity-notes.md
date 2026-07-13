# Cybersecurity Notes

> Catatan teknis dari konten IT Insights topik Cybersecurity — Minggu 3
> (Siklus 1, Fondasi) dan Minggu 8 (Siklus 2, Pendalaman). Dokumen ini
> dikonsolidasikan dan terus di-extend setiap kali topik Cybersecurity
> muncul lagi di roadmap, bukan dibuat ulang per minggu.

---

## 1. Human Element dalam Insiden Siber

### Konteks
Verizon Data Breach Investigations Report (DBIR) melaporkan elemen
manusia (human element) — mencakup error, privilege misuse, penggunaan
kredensial curian, dan social engineering — sebagai salah satu
kontributor utama insiden kebocoran data.

**Data terverifikasi per edisi:**
- DBIR 2025: **60%** pelanggaran data melibatkan elemen manusia
- DBIR 2026: **62%** pelanggaran data melibatkan elemen manusia

> **Koreksi dari versi awal:** konten Minggu 3 (Juni 2026) sempat
> menyebut angka "68%" untuk human element. Angka ini tidak akurat dan
> sudah diperbaiki di atas. Jangan gunakan 68% lagi di konten mendatang.

### Kategori "Human Element" menurut DBIR
- **Social engineering** — manipulasi psikologis untuk mendapatkan akses atau informasi
- **Errors** — kesalahan konfigurasi, salah kirim data, misdelivery
- **Misuse** — penyalahgunaan akses oleh orang dalam (insider threat)
- **Stolen credentials** — penggunaan kredensial yang diperoleh dari breach sebelumnya

Penting: angka ini bukan berarti "kesalahan pengguna" semata — ini
mencerminkan bahwa serangan modern memang dirancang untuk mengeksploitasi
perilaku manusia, bukan hanya celah teknis.

Referensi: [Verizon Data Breach Investigations Report](https://www.verizon.com/business/resources/reports/dbir/)

---

## 2. Update 2026 — Eksploitasi Kerentanan Software Melampaui Pencurian Kredensial

Temuan paling signifikan dari DBIR 2026 (dibanding edisi-edisi
sebelumnya): untuk pertama kalinya dalam 19 tahun sejarah laporan ini,
**eksploitasi kerentanan software (31%)** mengalahkan **pencurian
kredensial (13%)** sebagai vektor akses awal paling umum dalam
pelanggaran data.

Data pendukung dari edisi yang sama:
- Median waktu penambalan kerentanan (time-to-patch) memanjang dari
  **32 hari menjadi 43 hari** dibanding tahun sebelumnya.
- Hanya **26%** kerentanan pada katalog CISA Known Exploited
  Vulnerabilities (KEV) yang berhasil ditambal penuh sepanjang periode
  laporan, turun dari 38% tahun sebelumnya.
- Analisis mencakup lebih dari 31.000 insiden keamanan, dengan sekitar
  22.000 di antaranya terkonfirmasi sebagai breach.

Implikasi praktis: kebiasaan update software (poin yang dibahas di
Minggu 8) sekarang sama pentingnya — kalau bukan lebih penting — dari
kebiasaan password yang jadi fokus utama Minggu 3.

Referensi: [Verizon 2026 Data Breach Investigations Report](https://www.verizon.com/business/resources/reports/dbir/)

---

## 3. Credential Stuffing

### Mekanisme
Credential stuffing adalah serangan otomatis di mana pelaku menggunakan
kombinasi username/password yang bocor dari satu layanan untuk mencoba
login ke layanan lain.

**Alurnya:**
1. Database kredensial dari breach (misalnya breach LinkedIn 2012,
   Adobe 2013, dll.) beredar di dark web
2. Pelaku menggunakan tools otomatis (contoh: Sentry MBA, OpenBullet)
   untuk mencoba kombinasi tersebut secara masif ke target platform lain
3. Karena banyak pengguna memakai password yang sama di banyak
   platform, tingkat keberhasilan bisa signifikan meski persentasenya
   kecil — skala volume yang besar mengkompensasi success rate rendah

### Perbedaan dengan Brute Force
| Credential Stuffing | Brute Force |
|---|---|
| Pakai kredensial nyata yang sudah bocor | Coba semua kombinasi karakter |
| Success rate lebih tinggi | Success rate sangat rendah |
| Susah dideteksi karena pakai credential valid | Lebih mudah dideteksi dari pola request |
| Tidak perlu komputasi besar | Butuh komputasi tinggi |

### Mitigasi
- Password unik per platform (paling efektif)
- Rate limiting pada login endpoint
- CAPTCHA setelah beberapa kali gagal login
- Device fingerprinting
- Deteksi anomali login (lokasi, waktu, device baru)

> Catatan: per DBIR 2026 (lihat bagian 2), credential-based attack
> sudah bukan lagi vektor #1 — tapi tetap relevan sebagai ancaman
> signifikan, terutama dikombinasikan dengan kerentanan software yang
> belum ditambal.

---

## 4. Phishing — Evolusi Teknis

### Phishing Klasik vs Modern

**Klasik (mudah dikenali):**
- Domain mencurigakan (misalnya `paypa1.com`)
- Bahasa buruk, banyak typo
- Generic greeting ("Dear Customer")
- Attachment `.exe` atau `.zip` mencurigakan

**Modern (sulit dikenali):**
- **Spear phishing** — ditargetkan spesifik ke individu, menggunakan
  nama asli, jabatan, dan konteks nyata
- **Homograph attack** — domain menggunakan karakter Unicode yang mirip
  huruf Latin (contoh: `аpple.com` dengan 'а' Cyrillic bukan 'a' Latin)
- **Subdomain spoofing** — `paypal.login.attacker.com` — subdomain
  terlihat legitimate
- **Email spoofing** — memalsukan header `From:` tanpa autentikasi
  SPF/DKIM/DMARC yang ketat

### Cara Cek Domain Lebih Dalam
```bash
# Cek apakah domain punya SPF record
dig TXT domain.com | grep spf

# Cek DMARC policy
dig TXT _dmarc.domain.com

# Cek WHOIS untuk registrasi domain baru
whois domain.com | grep "Creation Date"
```
Domain phishing sering baru dibuat — tanggal registrasi <30 hari adalah
sinyal waspada.

### Teknik Psikologis yang Digunakan
- **Urgency** — "Akun akan diblokir dalam 24 jam"
- **Authority** — Menyamar sebagai atasan, bank, atau institusi resmi
- **Fear** — "Ada aktivitas mencurigakan di akun Anda"
- **Scarcity** — "Konfirmasi segera atau akses dicabut"

Semua dirancang untuk menekan *System 2 thinking* (analitis) dan
mendorong respons *System 1* (otomatis/reaktif).

---

## 5. Two-Factor Authentication (2FA) — Perbandingan Metode

### Hierarki Keamanan 2FA (dari paling lemah ke paling kuat)

| Metode | Mekanisme | Kelemahan Utama |
|---|---|---|
| SMS OTP | Kode dikirim via SMS | SIM swapping, SS7 attack |
| Email OTP | Kode dikirim via email | Bergantung keamanan email itu sendiri |
| TOTP (Authenticator App) | Kode berbasis waktu, offline | Phishing real-time (AiTM attack) |
| Hardware Key (FIDO2/WebAuthn) | Kriptografi public-key, terikat domain | Hilang/rusak; belum semua platform support |

### SIM Swapping — Cara Kerja
1. Pelaku mengumpulkan data korban (nama, nomor HP, tanggal lahir) dari
   media sosial atau breach
2. Menghubungi operator seluler, berpura-pura sebagai pemilik nomor
3. Meminta pemindahan nomor ke SIM card baru
4. Operator yang tidak memverifikasi ketat memindahkan nomor
5. Semua OTP SMS kini masuk ke SIM pelaku

**Mitigasi:** Minta operator untuk pasang PIN/kode tambahan sebelum
perubahan nomor bisa dilakukan.

### TOTP — Cara Kerja
TOTP (Time-based One-Time Password), distandardisasi di **RFC 6238**,
menggunakan:
- **Shared secret** yang di-scan saat setup (QR code)
- **Timestamp** (default time step 30 detik)
- **HMAC-SHA1** untuk generate kode 6 digit

Konsep dasarnya:
```
TOTP = HMAC-SHA1(secret, floor(current_time / 30)) mod 10^6
```

Karena berbasis waktu + secret key lokal, **tidak ada data yang dikirim
lewat jaringan** untuk menghasilkan kode — beda dari SMS OTP yang
transmisinya bisa disadap. Tapi TOTP tetap rentan terhadap **AiTM
(Adversary-in-the-Middle)** phishing yang mencuri session token secara
real-time.

Contoh implementasi sederhana pakai Python (library `pyotp`, untuk
tujuan edukasi memahami cara kerja, bukan untuk produksi):

```python
import pyotp

# Secret key dibuat sekali saat setup akun (biasanya di-encode base32)
secret = pyotp.random_base32()
totp = pyotp.TOTP(secret)

print("Kode TOTP saat ini:", totp.now())
# Kode ini otomatis berubah tiap 30 detik, dihitung dari waktu + secret
```

Referensi: [RFC 6238 — TOTP: Time-Based One-Time Password Algorithm](https://www.rfc-editor.org/rfc/rfc6238)

### FIDO2/WebAuthn — Paling Aman
- Menggunakan kriptografi asymmetric (public/private key)
- Private key **tidak pernah meninggalkan device**
- Verifikasi terikat ke domain spesifik → immune terhadap phishing
- Standard terbuka: https://webauthn.io/

---

## 6. VirusTotal — Cara Kerja Teknis

VirusTotal mengagregasi hasil pemindaian dari 70+ mesin antivirus dan
lebih dari 10 sandbox analisis dinamis dalam satu laporan. Untuk file,
pemeriksaan bisa dilakukan dua cara:

1. **Upload langsung** — file dikirim dan dipindai dari awal.
2. **Lookup berdasarkan hash** (MD5/SHA1/SHA256) — jika file sudah
   pernah diperiksa sebelumnya oleh siapa pun di seluruh dunia, hasilnya
   langsung tersedia tanpa perlu upload ulang. Ini alasan kenapa
   VirusTotal cepat: banyak file umum sudah ada di database mereka.

Contoh pemanggilan API v3 untuk mengecek laporan berdasarkan hash file
(butuh API key gratis dari akun VirusTotal Community):

```bash
curl --request GET \
  --url https://www.virustotal.com/api/v3/files/{sha256_hash} \
  --header 'x-apikey: API_KEY_KAMU'
```

Public API dibatasi 500 request/hari dan 4 request/menit — cukup untuk
penggunaan personal, tidak untuk otomasi skala besar tanpa API
berbayar.

Referensi: [VirusTotal API Reference](https://docs.virustotal.com/reference/overview)

---

## 7. Google Safe Browsing — Cara Kerja Teknis

Safe Browsing bekerja dengan mencocokkan URL terhadap daftar sumber
daya web yang tidak aman (phishing, malware, unwanted software) yang
terus diperbarui Google. Ada dua pendekatan:

- **Lookup API** — aplikasi mengirim URL langsung ke server Google
  untuk dicek statusnya. Simpel, tapi server tahu URL apa saja yang
  kamu cek (implikasi privasi).
- **Update API / hash-based matching** — aplikasi mengunduh daftar hash
  terenkripsi secara lokal, lalu mencocokkan URL secara lokal tanpa
  mengirim URL asli ke server. Lebih privat, tapi implementasinya lebih
  kompleks.

`testsafebrowsing.appspot.com` adalah domain uji resmi milik Google
sendiri — dipakai di contoh resmi mereka untuk keperluan testing,
jadi aman dipakai sebagai demo publik.

Referensi: [Google Safe Browsing — Overview](https://developers.google.com/safe-browsing)

---

## 8. Memeriksa Kebocoran Data — HaveIBeenPwned

### Tentang Platform
**HaveIBeenPwned (HIBP)** dibuat oleh Troy Hunt (Microsoft Regional
Director, security researcher).

- Mengagregasi data dari breach yang sudah dipublikasikan/ditemukan
- Tidak menyimpan password dalam bentuk plaintext
- Untuk Pwned Passwords: menggunakan **k-Anonymity model** — kamu hanya
  mengirim 5 karakter pertama dari hash SHA-1 password, bukan password
  itu sendiri
- Referensi metodologi: https://haveibeenpwned.com/About

### k-Anonymity Model untuk Pwned Passwords
```
# Contoh cara kerja (konseptual):
1. Password diubah ke SHA-1: SHA1("password123") = CBFDAC...
2. Hanya 5 karakter pertama dikirim ke API: "CBFDA"
3. API mengembalikan semua hash yang diawali "CBFDA" beserta frekuensinya
4. Client mencocokkan hash lengkap secara lokal
5. Server tidak pernah tahu password asli atau hash lengkap
```

**API public (gratis):**
```
# Cek apakah password pernah bocor (tanpa kirim password)
curl https://api.pwnedpasswords.com/range/CBFDA
```

---

## 9. Keamanan Wi-Fi Publik

### Risiko Teknis
- **Evil Twin Attack** — pelaku membuat hotspot dengan nama sama
  (misal "Cafe_WiFi") untuk intercept traffic
- **SSL Stripping** — downgrade HTTPS ke HTTP jika implementasi tidak
  menggunakan HSTS
- **Packet Sniffing** — pada jaringan tanpa enkripsi WPA2/WPA3, traffic
  bisa dibaca

### Perlindungan Praktis
- Selalu cek `https://` + ikon gembok sebelum input data sensitif
- Aktifkan **HSTS** di browser (biasanya default di browser modern)
- Untuk aktivitas sensitif: gunakan data seluler sendiri
- Jika harus pakai Wi-Fi publik untuk kerja: gunakan VPN dari provider
  terpercaya

### Catatan tentang VPN
VPN mengenkripsi traffic antara device dan VPN server — bukan antara
VPN server dan tujuan akhir. VPN gratis yang tidak transparan bisa
justru menjadi masalah keamanan baru. Pilih provider yang open source
dan punya audit independen yang dipublikasikan.

---

## Referensi

| Sumber | URL | Ditambahkan | Terverifikasi |
|---|---|---|---|
| Verizon DBIR (2025 & 2026) | https://www.verizon.com/business/resources/reports/dbir/ | Minggu 3 | 13 Juli 2026 |
| VirusTotal API Reference | https://docs.virustotal.com/reference/overview | Minggu 8 | 13 Juli 2026 |
| Google Safe Browsing | https://developers.google.com/safe-browsing | Minggu 8 | 13 Juli 2026 |
| RFC 6238 (TOTP) | https://www.rfc-editor.org/rfc/rfc6238 | Minggu 8 | 13 Juli 2026 |
| HaveIBeenPwned About | https://haveibeenpwned.com/About | Minggu 3 | belum diverifikasi ulang sesi ini |
| HaveIBeenPwned API | https://haveibeenpwned.com/API/v3 | Minggu 3 | belum diverifikasi ulang sesi ini |
| WebAuthn | https://webauthn.io/ | Minggu 3 | belum diverifikasi ulang sesi ini |
| OWASP Credential Stuffing | https://owasp.org/www-community/attacks/Credential_stuffing | Minggu 3 | belum diverifikasi ulang sesi ini |

---

## Changelog

**13 Juli 2026 (Minggu 8 — Pendalaman)**
- Ditambahkan: Bagian 2 (eksploitasi kerentanan software melampaui
  kredensial, data DBIR 2026), Bagian 6 (VirusTotal), Bagian 7 (Google
  Safe Browsing)
- Dikoreksi: angka human element di Bagian 1 — dari "68%" (tidak
  akurat) menjadi 60% (DBIR 2025) dan 62% (DBIR 2026), keduanya
  terverifikasi
- Ditambahkan: contoh implementasi Python (`pyotp`) di Bagian 5 sebagai
  pelengkap pseudocode TOTP yang sudah ada
- Struktur file diputuskan menjadi konsolidasi (bukan file terpisah
  per minggu) — dokumen ini akan terus di-extend setiap topik
  Cybersecurity muncul lagi di roadmap

**1–7 Juni 2026 (Minggu 3 — Fondasi)**
- Versi awal dibuat, mencakup Human Element, Credential Stuffing,
  Phishing Evolution, 2FA Comparison, HaveIBeenPwned, Wi-Fi Security

---

*Bagian dari proyek IT Insights — @seandyarozano*
*Repo: github.com/seandyarozano/it-insights-notes*
*Konten sosial: instagram.com/seandyarozano | threads.net/@seandyarozano*
*Artikel: seandyarozano.staff.telkomuniversity.ac.id*
