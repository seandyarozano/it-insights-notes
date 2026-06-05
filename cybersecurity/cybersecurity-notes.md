# Cybersecurity Notes — Minggu 3

> Catatan teknis dari konten IT Insights Minggu 3 (1–7 Juni 2026).
> Versi lebih dalam dari konten sosial — fokus pada mekanisme teknis, bukan hanya awareness.

---

## 1. Human Element dalam Insiden Siber

### Konteks
Verizon Data Breach Investigations Report (DBIR) 2025 melaporkan bahwa lebih dari dua pertiga insiden kebocoran data melibatkan faktor manusia — mencakup error, privilege misuse, penggunaan credential yang dicuri, dan social engineering.

**Sumber:** https://www.verizon.com/business/resources/reports/dbir/

### Kategori "Human Element" menurut DBIR
DBIR membagi human element ke dalam beberapa kategori utama:
- **Social engineering** — manipulasi psikologis untuk mendapatkan akses atau informasi
- **Errors** — kesalahan konfigurasi, salah kirim data, misdelivery
- **Misuse** — penyalahgunaan akses oleh orang dalam (insider threat)
- **Stolen credentials** — penggunaan kredensial yang diperoleh dari breach sebelumnya

Penting: angka ini bukan berarti "kesalahan pengguna" semata — ini mencerminkan bahwa serangan modern memang dirancang untuk mengeksploitasi perilaku manusia, bukan hanya celah teknis.

---

## 2. Credential Stuffing

### Mekanisme
Credential stuffing adalah serangan otomatis di mana pelaku menggunakan kombinasi username/password yang bocor dari satu layanan untuk mencoba login ke layanan lain.

**Alurnya:**
1. Database kredensial dari breach (misalnya breach LinkedIn 2012, Adobe 2013, dll.) beredar di dark web
2. Pelaku menggunakan tools otomatis (contoh: Sentry MBA, OpenBullet) untuk mencoba kombinasi tersebut secara masif ke target platform lain
3. Karena banyak pengguna memakai password yang sama di banyak platform, tingkat keberhasilan bisa signifikan meski persentasenya kecil — skala volume yang besar mengkompensasi success rate rendah

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

---

## 3. Phishing — Evolusi Teknis

### Phishing Klasik vs Modern

**Klasik (mudah dikenali):**
- Domain mencurigakan (misalnya `paypa1.com`)
- Bahasa buruk, banyak typo
- Generic greeting ("Dear Customer")
- Attachment `.exe` atau `.zip` mencurigakan

**Modern (sulit dikenali):**
- **Spear phishing** — ditargetkan spesifik ke individu, menggunakan nama asli, jabatan, dan konteks nyata
- **Homograph attack** — domain menggunakan karakter Unicode yang mirip huruf Latin (contoh: `аpple.com` dengan 'а' Cyrillic bukan 'a' Latin)
- **Subdomain spoofing** — `paypal.login.attacker.com` — subdomain terlihat legitimate
- **Email spoofing** — memalsukan header `From:` tanpa autentikasi SPF/DKIM/DMARC yang ketat

### Cara Cek Domain Lebih Dalam
```bash
# Cek apakah domain punya SPF record
dig TXT domain.com | grep spf

# Cek DMARC policy
dig TXT _dmarc.domain.com

# Cek WHOIS untuk registrasi domain baru
whois domain.com | grep "Creation Date"
```
Domain phishing sering baru dibuat — tanggal registrasi <30 hari adalah sinyal waspada.

### Teknik Psikologis yang Digunakan
- **Urgency** — "Akun akan diblokir dalam 24 jam"
- **Authority** — Menyamar sebagai atasan, bank, atau institusi resmi
- **Fear** — "Ada aktivitas mencurigakan di akun Anda"
- **Scarcity** — "Konfirmasi segera atau akses dicabut"

Semua dirancang untuk menekan *System 2 thinking* (analitis) dan mendorong respons *System 1* (otomatis/reaktif).

---

## 4. Two-Factor Authentication (2FA) — Perbandingan Metode

### Hierarki Keamanan 2FA (dari paling lemah ke paling kuat)

| Metode | Mekanisme | Kelemahan Utama |
|---|---|---|
| SMS OTP | Kode dikirim via SMS | SIM swapping, SS7 attack |
| Email OTP | Kode dikirim via email | Bergantung keamanan email itu sendiri |
| TOTP (Authenticator App) | Kode berbasis waktu, offline | Phishing real-time (AiTM attack) |
| Hardware Key (FIDO2/WebAuthn) | Kriptografi public-key, terikat domain | Hilang/rusak; belum semua platform support |

### SIM Swapping — Cara Kerja
1. Pelaku mengumpulkan data korban (nama, nomor HP, tanggal lahir) dari media sosial atau breach
2. Menghubungi operator seluler, berpura-pura sebagai pemilik nomor
3. Meminta pemindahan nomor ke SIM card baru
4. Operator yang tidak memverifikasi ketat memindahkan nomor
5. Semua OTP SMS kini masuk ke SIM pelaku

**Mitigasi:** Minta operator untuk pasang PIN/kode tambahan sebelum perubahan nomor bisa dilakukan.

### TOTP — Cara Kerja
TOTP (Time-based One-Time Password) menggunakan:
- **Shared secret** yang di-scan saat setup (QR code)
- **Timestamp** (biasanya interval 30 detik)
- **HMAC-SHA1** untuk generate kode 6 digit

Karena berbasis waktu dan tidak dikirim lewat jaringan, jauh lebih sulit diintersep. Tapi tetap rentan terhadap **AiTM (Adversary-in-the-Middle)** phishing yang mencuri session token secara real-time.

```
# Konsep sederhana TOTP (bukan implementasi production):
TOTP = HMAC-SHA1(secret, floor(current_time / 30)) mod 10^6
```

### FIDO2/WebAuthn — Paling Aman
- Menggunakan kriptografi asymmetric (public/private key)
- Private key **tidak pernah meninggalkan device**
- Verifikasi terikat ke domain spesifik → immune terhadap phishing
- Standard terbuka: https://webauthn.io/

---

## 5. Memeriksa Kebocoran Data — HaveIBeenPwned

### Tentang Platform
**HaveIBeenPwned (HIBP)** dibuat oleh Troy Hunt (Microsoft Regional Director, security researcher).

- Mengaggregasi data dari breach yang sudah dipublikasikan/ditemukan
- Tidak menyimpan password dalam bentuk plaintext
- Untuk Pwned Passwords: menggunakan **k-Anonymity model** — kamu hanya mengirim 5 karakter pertama dari hash SHA-1 password, bukan password itu sendiri
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

## 6. Keamanan Wi-Fi Publik

### Risiko Teknis
- **Evil Twin Attack** — pelaku membuat hotspot dengan nama sama (misal "Cafe_WiFi") untuk intercept traffic
- **SSL Stripping** — downgrade HTTPS ke HTTP jika implementasi tidak menggunakan HSTS
- **Packet Sniffing** — pada jaringan tanpa enkripsi WPA2/WPA3, traffic bisa dibaca

### Perlindungan Praktis
- Selalu cek `https://` + ikon gembok sebelum input data sensitif
- Aktifkan **HSTS** di browser (biasanya default di browser modern)
- Untuk aktivitas sensitif: gunakan data seluler sendiri
- Jika harus pakai Wi-Fi publik untuk kerja: gunakan VPN dari provider terpercaya

### Catatan tentang VPN
VPN mengenkripsi traffic antara device dan VPN server — bukan antara VPN server dan tujuan akhir. VPN gratis yang tidak transparan bisa justru menjadi masalah keamanan baru. Pilih provider yang open source dan punya audit independen yang dipublikasikan.

---

## Referensi

| Sumber | URL | Catatan |
|---|---|---|
| Verizon DBIR 2025 | https://www.verizon.com/business/resources/reports/dbir/ | Laporan tahunan — verifikasi edisi terbaru |
| HaveIBeenPwned About | https://haveibeenpwned.com/About | Metodologi dan tentang platform |
| HaveIBeenPwned API | https://haveibeenpwned.com/API/v3 | Dokumentasi API publik |
| WebAuthn | https://webauthn.io/ | Demo dan penjelasan FIDO2 |
| OWASP Credential Stuffing | https://owasp.org/www-community/attacks/Credential_stuffing | Referensi teknis |

---

*Bagian dari proyek IT Insights — @seandyarozano*
*Repo: github.com/seandyarozano/it-insights-notes*
*Konten sosial: instagram.com/seandyarozano | threads.net/@seandyarozano*
*Artikel: seandyarozano.staff.telkomuniversity.ac.id*
