# Routing Table: Peta Perjalanan Data di Jaringan Komputer

> Bagian dari seri IT Insights Notes — penjelasan teknis dalam bahasa sederhana

---

## Apa itu Routing Table?

Routing table adalah daftar "petunjuk arah" yang dimiliki setiap perangkat jaringan
(router, komputer, server). Isinya: ke mana paket data harus dikirim berdasarkan
alamat IP tujuannya.

**Analoginya:** bayangkan kamu datang ke hajatan besar tapi tidak kenal siapapun.
Kamu butuh seseorang yang tahu: "meja makan ada di sayap kiri, kamar mandi di
belakang, tuan rumah ada di panggung." Orang itu adalah routing table.

Tanpa routing table → komputer bingung → data nyasar → tidak sampai tujuan.

---

## Cara Kerja Routing Table

Setiap kali komputer ingin mengirim data, ia bertanya ke routing table:

```
"Saya mau kirim data ke 192.168.2.50.
 Harus lewat mana?"

Routing table menjawab:
"Jaringan 192.168.2.0/24 → lewat gateway 192.168.1.1,
 gunakan interface eth0."
```

Proses ini terjadi dalam milidetik, untuk setiap paket data yang dikirim.

---

## Komponen Utama Routing Table

| Kolom | Fungsi | Contoh |
|-------|--------|--------|
| **Destination** | Alamat jaringan tujuan | 192.168.2.0/24 |
| **Gateway** | Pintu keluar menuju jaringan lain | 192.168.1.1 |
| **Interface** | Kartu jaringan yang digunakan | eth0, wlan0 |
| **Metric** | "Biaya" jalur — makin kecil makin diprioritaskan | 100, 200 |
| **Flags** | Status route (U=Up, G=Gateway, H=Host) | UG, UH |

---

## Jenis-Jenis Routing

### Static Routing
Dikonfigurasi manual oleh admin jaringan. Tidak berubah kecuali diubah secara manual.

**Cocok untuk:**
- Jaringan kecil dengan topologi sederhana
- Koneksi point-to-point
- Backup route

**Kelebihan:** ringan, mudah diprediksi, tidak ada overhead protokol  
**Kekurangan:** tidak adaptif — kalau jalur mati, tidak otomatis cari jalur lain

### Dynamic Routing
Router saling berbagi informasi jalur secara otomatis menggunakan protokol routing.

**Protokol yang umum digunakan:**

| Protokol | Singkatan | Digunakan Untuk |
|----------|-----------|-----------------|
| OSPF | Open Shortest Path First | Jaringan enterprise internal |
| BGP | Border Gateway Protocol | Antar ISP, routing internet global |
| RIP | Routing Information Protocol | Jaringan kecil, sudah jarang dipakai |
| EIGRP | Enhanced IGRP | Jaringan Cisco |

**Kelebihan:** adaptif — otomatis cari jalur alternatif jika ada yang mati  
**Kekurangan:** lebih berat, butuh konfigurasi lebih kompleks

### Default Route
Route "catch-all" — kalau tidak ada route yang cocok, kirim ke sini.
Biasanya menuju ke internet gateway.

```
Destination: 0.0.0.0/0 → Gateway: 192.168.1.1
```

Ini seperti plang "Ke kota lain → ikuti jalan ini" di pintu keluar kampung.

---

## Analogi Kehidupan Nyata

| Konsep IT | Analogi |
|-----------|---------|
| Routing table | Peta + buku tamu hajatan |
| Gateway | Pintu gerbang kampung |
| Static route | Rute yang sudah dihapal sejak kecil |
| Dynamic route | GPS yang update jalur otomatis |
| Metric | Jarak tempuh — pilih yang paling dekat |
| Default route | "Kalau tidak tahu, tanya di kantor desa" |
| Packet loss | Kurir nyasar, paket tidak sampai |

---

## Perintah Dasar di Terminal

```bash
# Lihat routing table di Linux/Mac
ip route show

# Alternatif (lebih lama tapi masih umum)
route -n

# Lihat routing table di Windows
route print

# Tambah static route di Linux
sudo ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0

# Hapus static route di Linux
sudo ip route del 192.168.2.0/24

# Tambah default route
sudo ip route add default via 192.168.1.1

# Cek jalur yang dilalui paket (seperti GPS yang tunjukkan rute)
traceroute google.com          # Linux/Mac
tracert google.com             # Windows
```

---

## Contoh Output Routing Table

```
$ ip route show

default via 192.168.1.1 dev eth0 proto dhcp metric 100
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.50
172.16.0.0/16 via 192.168.1.254 dev eth0 metric 200
```

**Cara bacanya:**
- Baris 1: semua traffic yang tidak dikenali → ke 192.168.1.1 (internet gateway)
- Baris 2: jaringan lokal → langsung, tidak perlu gateway
- Baris 3: jaringan 172.16.x.x → lewat 192.168.1.254 (mungkin VPN atau kantor cabang)

---

## Kenapa Ini Penting?

**Untuk IT practitioner:**
- Troubleshooting koneksi yang tidak bisa akses jaringan tertentu
- Konfigurasi VLAN dan segmentasi jaringan
- Setup VPN dan koneksi antar kantor cabang

**Untuk semua orang:**
- Memahami kenapa kadang bisa akses website tapi tidak bisa ping server internal
- Mengerti kenapa VPN mengubah jalur traffic kamu
- Paham kenapa "ganti DNS" tidak sama dengan "ganti routing"

---

## Kesimpulan

Routing table adalah otak di balik perjalanan data di jaringan.
Setiap paket yang kamu kirim — dari WhatsApp, email, streaming video —
melewati proses pencarian routing table dalam milidetik.

Sederhananya: **tanpa routing table yang benar, data tidak tahu harus ke mana.**

---

## Kaitannya dengan Konten

- Post LinkedIn Minggu 1: [Pelajaran Networking dari Kehidupan Sehari-hari](https://linkedin.com/in/seandyarozano)
- Analogi yang dipakai: datang ke hajatan tanpa kenal siapapun = komputer tanpa routing table
- File terkait: [`dns-for-beginners.md`](./dns-for-beginners.md)

---

*IT Insights Notes · [github.com/seandyarozano/it-insights-notes](https://github.com/seandyarozano/it-insights-notes)*
