**# MIKROTIK-H4N5VS**# 🛡️ H4N5VS Mikrotik System Security

**H4N5VS** adalah sistem keamanan jaringan khusus untuk Mikrotik, ditulis dalam PHP, dengan tampilan terminal-hacker kekinian. Mirip antivirus, tapi bukan buat PC — ini buat router! Bisa deteksi DDoS, serangan botnet, brute-force, lalu langsung ambil tindakan. Auto-tendang penjahat jaringan. Cocok buat lo yang cinta kecepatan, benci kejahatan!

---

## 🚀 Analogi Instalasi: Biar Lo Gak Bingung

Bayangin lo lagi masak mi instan...  
- Airnya = Bitnami LAMP Stack  
- Mie-nya = File aplikasi H4N5VS  
- Bumbunya = API key OpenAI + Router Mikrotik  
- Kompornya = Apache + PHP  
- Sendoknya = Composer

Kalau salah masak? Ya rasanya ngaco. Jadi ikutin petunjuknya, chef!

---

## 📋 Prasyarat (Bahan Baku)

- ✅ Bitnami LAMP Stack udah terpasang
- ✅ Akses ke router Mikrotik (RouterOS)
- ✅ OpenAI API Key buat fitur deteksi pintar
- ✅ Skill dasar Linux biar gak panik lihat terminal

---

## 💻 Spesifikasi Minimum

- PHP 7.4+
- MySQL/MariaDB 10.3+
- Apache 2.4+
- RAM 2GB (4GB lebih mantep)
- 10GB ruang disk (biar lega)

---

## 🧙‍♂️ Langkah Instalasi (Masak Mie-nya)

### 1. Install Bitnami LAMP Stack
```bash
chmod +x bitnami-lampstack-[versi]-linux-x64-installer.run
./bitnami-lampstack-[versi]-linux-x64-installer.run

### 2. Masukin Aplikasi ke Panci Apache
```bash
cd /opt/bitnami/apache2/htdocs/
rm index.html
git clone https://your-repo-url.git .
# atau kalau file ZIP
unzip h4n5vs.zip -d .

### 3. Bikin Folder Penting
mkdir -p data logs
chmod 755 data logs
chown -R daemon:daemon data logs

### 4. Pasang Bumbu PHP (Extension & Composer)
sudo /opt/bitnami/php/bin/pecl install openssl mysqli
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
composer install

### 5. Tambahkan SDK OpenAI
composer require openai/openai-php

### 6. Buat File Rahasia (.env)
touch .env
echo "OPENAI_API_KEY=isi_api_key_disini" >> .env
chmod 600 .env
chown daemon:daemon .env

### Edit Apache biar bisa "cium" environment variable:
bash:
nano /opt/bitnami/apache2/conf/httpd.conf
# Tambahkan:
<Directory "/opt/bitnami/apache2/htdocs">
    PassEnv OPENAI_API_KEY
</Directory>
sudo /opt/bitnami/ctlscript.sh restart apache

### 🌐 Bikin Virtual Host (Opsional tapi Keren)
nano /opt/bitnami/apache2/conf/vhosts/h4n5vs-vhost.conf

Isi:
<VirtualHost *:80>
    ServerName yourdomain.com
    DocumentRoot "/opt/bitnami/apache2/htdocs"
    <Directory "/opt/bitnami/apache2/htdocs">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog "logs/h4n5vs-error.log"
    CustomLog "logs/h4n5vs-access.log" combined
</VirtualHost>

## Restart lagi: 
bash:
sudo /opt/bitnami/apache2/bin/apachectl -k restart

## ✅ Verifikasi (Cobain Masuk)
Buka browser: http://IP-Server
Harusnya muncul halaman login H4N5VS

Login Default:

Username: admin

Password: admin123

Langsung ganti ya, jangan kayak default password Indihome.

## 🔒 Keamanan (Pakai Helm & Rompi Anti Peluru)
bash :
find /opt/bitnami/apache2/htdocs -type f -exec chmod 644 {} \;
find /opt/bitnami/apache2/htdocs -type d -exec chmod 755 {} \;
chmod 600 /opt/bitnami/apache2/htdocs/.env

Note : Gunakan SSL (biar HTTPS, bukan HTPSS 😅)


## 🧯 Troubleshooting (Kalau Mie Lo Gak Matang)
Router Gak Terdeteksi?

Cek IP, username, password

Pastikan API aktif di Mikrotik (/ip service enable api)

Port 8728 atau 8729 jangan diblokir

# PHP Extension Hilang?

bash:
sudo /opt/bitnami/php/bin/pecl install extension_name
echo "extension=extension_name.so" >> /opt/bitnami/php/etc/php.ini

Permission Error?
bash:
chown -R daemon:daemon /opt/bitnami/apache2/htdocs

### 🔄 Update Aplikasi
bash:

cp -r /opt/bitnami/apache2/htdocs /opt/bitnami/apache2/htdocs_backup
cd /opt/bitnami/apache2/htdocs
git pull origin main
composer update
cp /opt/bitnami/apache2/htdocs_backup/.env ./
chown -R daemon:daemon .
sudo /opt/bitnami/ctlscript.sh restart apache

### 📄 Lisensi
Proyek ini dilisensikan dengan MIT License. Bebas pakai, asal jangan dipakai buat nyusupin iklan pinjol.

### ❤️ Terima Kasih
Kalau lo sampai di bawah ini, lo adalah pejuang jaringan sejati. Jangan lupa ngopi, dan selamat mengamankan router!

