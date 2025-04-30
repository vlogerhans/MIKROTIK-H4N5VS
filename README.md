
# 🤖 H4N5VS - Mikrotik System Security  
**Aplikasi monitoring dan keamanan router Mikrotik**  
*Biar nggak ada yang numpang nonton bokep lewat WiFi lu, Pak!*

---

## 🎤 Opening dulu ya, Pak...

“Zaman sekarang, yang nyerang bukan cuma mantan... tapi juga botnet, DDoS, sama bocah warnet yang iseng pake LOIC! 😤”  
Makanya, kenalin: **H4N5VS**, sistem keamanan router Mikrotik yang bakal bikin WiFi Bapak kayak rumah... penuh pengawasan! 👮‍♂️📡

---

## ⚙️ Fitur Utama

- 👀 **Monitoring real-time:** Pantau router kayak mantau grup WA keluarga.
- 🛡️ **Deteksi serangan:** DDoS, botnet, & IP mencurigakan. Ibarat satpam siber.
- 💥 **Mitigasi otomatis:** Kalo ada yang aneh, langsung tendang!
- 🔍 **IP Checker:** Tau siapa yang ngintip, meskipun pakai VPN KW.
- 📊 **Dashboard Keren:** Warna neon, font terminal, vibes Matrix.
- 📁 **Log Lengkap:** Semua kejadian terekam. Replay siap.

---

## 🧪 Cara Pakai (Lokal Server: XAMPP/Bitnami)

### Persyaratan
- PHP 7.4+
- Apache/Nginx (bukan kipas angin)
- Koneksi internet

### Instalasi

```bash
git clone https://github.com/username/h4n5vs-mikrotik-security.git
```

Atau ekstrak manual, kayak zaman 4Shared.

### Konfigurasi Web Server

1. Copy ke `htdocs`
2. Arahkan server ke folder
3. Buat folder log:

```bash
mkdir logs
chmod 755 logs
```

---

## 🚀 Jalankan Aplikasi

Buka browser:

```
http://localhost/h4n5vs/
```

**Login:**
- Username: `admin`
- Password: `admin123`  
(Jangan lupa ganti, ntar diserobot anak warnet 😆)

---

## 🔌 Hubungkan Router Mikrotik

Isi:
- IP Router
- Username Router
- Password Router

Terus klik *Connect*  
Langsung bisa monitoring kayak FBI.

---

## 🌑 Tema Hacker Mode

> Buat mata adem dan kelihatan lebih "pro"

- `dashboard.php` = versi default
- `dashboard-new.php` = mode terminal gelap

Ubah arahkan di `index.php` kalau mau default dark mode.

---

## 📂 Struktur Folder

```
/
├── api/
├── assets/
├── includes/
├── logs/
├── config.php
├── dashboard.php
├── dashboard-new.php
├── index.php
├── login.php
└── logout.php
```

---

## 🧪 Mode Demo

Nggak punya Mikrotik? Bisa test mode dummy.  
Pakai data simulasi. Serasa punya jaringan NASA.

---

## 🎨 Kustomisasi

- `assets/css/style.css` → mode biasa
- `assets/css/dark-theme.css` → mode terminal gelap

Mau warna neon pink? Silakan, Pak. Asal jangan font Comic Sans aja ya.

---

## 🔐 Tips Keamanan

- Ganti password default
- Aktifkan HTTPS
- Batasi IP akses
- Update RouterOS & API secara rutin

---

## 🤝 Kontribusi

Mau bantu? Bikin fitur? Kirim pull request.  
Mari bangun firewall digital Nusantara bersama-sama.

---

## 📜 Lisensi

MIT License  
Bebas pakai, asal jangan dijual di Tokped 🤣
