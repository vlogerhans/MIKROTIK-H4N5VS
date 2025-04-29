# PANDUAN INSTALASI "H4N5VS MIKROTIK SYSTEM SECURITY" VERSI KECE ABIS

## Apa Nih Aplikasinya?

Bro, sis! Jadi ceritanya H4N5VS ini tuh aplikasi keamanan buat router Mikrotik lo. Kalo router Mikrotik lo diibaratkan rumah, nah aplikasi ini tuh kayak satpam gaul yang gak cuma jaga, tapi juga punya CCTV canggih, alarm anti maling, plus bisa deteksi maling sebelum masuk! Keren kan?

## Status Pengembangan Aplikasi

Aplikasi H4N5VS ini masih dalam tahap pengembangan aktif. Berikut fitur yang udah bisa dipake dan yang masih on-progress:

### Udah Bisa Dipake ✓
- Sistem login (pake user admin/admin123)
- Halaman konfigurasi router Mikrotik
- Framework dashboard utama dengan panel monitoring

### Masih On Progress 🚧
- Beberapa API endpoint masih dalam tahap pengembangan
- Fungsi AI pattern recognition perlu API key OpenAI
- Beberapa halaman seperti firewall.php, connections.php, settings.php masih dibangun
- Beberapa asset gambar perlu ditambahkan (logo.png)

### Cara Fixing Error Login 🔧
Kalo nemuin error "Call to undefined function authenticate()" pas login, lo bisa tambahin fungsi di file auth.php:

```php
/**
 * Alias for login function
 */
function authenticate($username, $password) {
    return login($username, $password);
}
```

### Cara Fixing Error Dashboard 🔧
Kalo nemuin error "Call to undefined function require_auth()" pas buka dashboard, lo bisa tambahin fungsi di file auth.php:

```php
/**
 * Require authentication or redirect to login page
 */
function require_auth() {
    if (!is_logged_in()) {
        header('Location: login.php');
        exit;
    }
}
```

## Yang Harus Lo Siapin Dulu

- Bitnami LAMP stack (Kayak beli nasi padang, udah komplit sepaket)
- Akses ke router Mikrotik (Ya iyalah, masa mau ngamanin router tetangga)
- API key OpenAI (Ini kayak SIM buat nyetir kecerdasan buatan)
- Dikit-dikit ngerti perintah Linux (Minimal tau bedanya `ls` sama `rm` ya, jangan sampe data lo kehapus gara-gara salah perintah)

## Spek yang Dibutuhin

- PHP 7.4 ke atas (Kayak HP, minimal Android 10 lah ya)
- MySQL/MariaDB 10.3 ke atas (Database buat nyimpen data, jangan pake notes di HP ya)
- Apache 2.4 ke atas (Ini web server, bukan indian yang pake bulu-bulu di kepala)
- RAM 2GB minimal (4GB lebih mantep, kayak kuah bakso, lebih banyak lebih enak)
- Disk space 10GB (Biar gak sesak napas kayak naik motor ber-6 di jalan raya)

## Cara Pasangnya

### 1. Pasang Bitnami LAMP Stack Dulu

Ini kayak pasang pondasi rumah. Kalo pondasinya goyang, ya ntar rumahnya ikutan goyang dangdut.

1. Download dulu Bitnami LAMP dari [websitenya Bitnami](https://bitnami.com/stack/lamp)
2. Jadiin file installernya bisa dieksekusi:
   ```
   chmod +x bitnami-lampstack-[versi]-linux-x64-installer.run
   ```
   
   Ini ibarat ngasih "izin" ke file buat dijalanin. Kayak security klub malam yang ngasih stempel tangan.

3. Jalanin installernya:
   ```
   ./bitnami-lampstack-[versi]-linux-x64-installer.run
   ```
   
   Ini kayak nendang ban buat ngecek anginnya, tapi kali ini beneran jalan.

4. Ikutin petunjuknya sampe beres. Gampang banget, tinggal klik "Next, Next, Next" kayak install game bajakan.

### 2. Setting Aplikasinya

1. Masuk ke folder root Apache:
   ```
   cd /opt/bitnami/apache2/htdocs/
   ```
   
   Ini tuh kayak masuk ke kamar kosan lo, tempat utama buat naruh barang-barang.

2. Buang file index.html bawaannya:
   ```
   rm index.html
   ```
   
   Ibarat lo buang poster idol K-Pop dari kamar kosan yang ditinggalin penghuni sebelumnya.

3. Clone atau copy file aplikasinya ke root:
   ```
   git clone https://your-repository-url.git .
   ```
   
   Atau kalo punya file ZIP:
   ```
   unzip h4n5vs.zip -d .
   ```
   
   Ini kayak lo mindahin semua barang-barang lo ke kamar kosan baru.

4. Bikin direktori yang dibutuhin dengan izin yang bener:
   ```
   mkdir -p data logs
   chmod 755 data logs
   chown -R daemon:daemon data logs
   ```
   
   Ini kayak bikin lemari baru di kamar kosan, tapi pastiin kuncinya ada, gak bisa sembarangan dibuka sama orang.

5. Install ekstensi PHP yang dibutuhin:
   ```
   sudo /opt/bitnami/php/bin/pecl install openssl mysqli
   ```
   
   Anggep aja ini kayak pasang fitur-fitur tambahan di HP baru lo.

6. Install Composer (kalo belum ada):
   ```
   curl -sS https://getcomposer.org/installer | php
   mv composer.phar /usr/local/bin/composer
   ```
   
   Composer itu kayak asisten pribadi yang bantuin lo belanja kebutuhan coding.

7. Install dependensi PHP:
   ```
   composer install
   ```
   
   Ini ibarat belanja bulanan di supermarket. Composer yang bayarin, lo tinggal masukin ke kulkas.

### 3. Install OpenAI PHP SDK

1. Pake Composer buat install OpenAI PHP SDK:
   ```
   composer require openai/openai-php
   ```
   
   Ini ibarat lo nyuruh asisten lo buat beli otak AI. "Mas, tolong beliin otak AI yang bisa nebak-nebak serangan hacker dong!"

### 4. Setting Variabel Lingkungan

1. Bikin file .env di root aplikasi:
   ```
   touch .env
   ```
   
   Ini kayak bikin catetan rahasia yang bakal disimpen di bawah bantal.

2. Tambahin OpenAI API key ke file .env:
   ```
   echo "OPENAI_API_KEY=API_KEY_LO_TARUH_SINI" >> .env
   ```
   
   Anggep ini kayak nulis password ATM lo. JANGAN SAMPE KETAUAN ORANG!

3. Update izin filenya:
   ```
   chmod 600 .env
   chown daemon:daemon .env
   ```
   
   Ini ibarat naruh catetan password ATM lo di safe deposit box, bukan di mading kampus.

4. Biar PHP bisa akses variabel lingkungan, edit file konfigurasi Apache:
   ```
   nano /opt/bitnami/apache2/conf/httpd.conf
   ```
   
   Ini kayak ngasih tau satpam kalo si anu boleh masuk, soalnya dia temen lo.

5. Tambahin konfigurasi ini buat ngasih akses ke variabel lingkungan:
   ```
   <Directory "/opt/bitnami/apache2/htdocs">
       PassEnv OPENAI_API_KEY
   </Directory>
   ```
   
   Anggep ini kayak ngasih list tamu undangan ke satpam apartemen.

6. Restart Apache:
   ```
   sudo /opt/bitnami/ctlscript.sh restart apache
   ```
   
   Ini kayak nyuruh satpam pulang dulu terus balik lagi bawa list tamu yang udah diupdate.

### 5. Konfigurasi Apache (kalo perlu)

1. Bikin konfigurasi virtual host baru:
   ```
   nano /opt/bitnami/apache2/conf/vhosts/h4n5vs-vhost.conf
   ```
   
   Ini ibarat bikin surat izin pesta di kosan lo.

2. Tambahin konfigurasi berikut:
   ```
   <VirtualHost *:80>
       ServerName domainlo.com
       DocumentRoot "/opt/bitnami/apache2/htdocs"
       
       <Directory "/opt/bitnami/apache2/htdocs">
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>
       
       ErrorLog "logs/h4n5vs-error.log"
       CustomLog "logs/h4n5vs-access.log" combined
   </VirtualHost>
   ```
   
   Mirip kayak lo nulis alamat lengkap di surat undangan, biar gak ada yang nyasar.

3. Aktifin virtual host dan restart Apache:
   ```
   sudo /opt/bitnami/apache2/bin/apachectl -k restart
   ```
   
   Kayak lo ngasih surat izin ke RT dan ngerefresh keamanan kompleks.

### 6. Cek Hasil Instalasi

1. Buka browser dan kunjungi alamat IP server atau domain lo

2. Harusnya lo udah liat halaman login H4N5VS

3. Login pake kredensial default:
   - Username: admin
   - Password: admin123
   
   Ini ibarat kunci master pertama kali masuk kosan baru. GANTI SEGERA!

4. Setelah login, lo perlu konfigurasi pengaturan koneksi router Mikrotik

   Anggep ini kayak lo ngehubungin CCTV ke HP lo, biar bisa mantau dari mana aja.

### 7. Tips Keamanan

1. Ganti kredensial login default secepatnya setelah login pertama
   
   Ini kayak ganti gembok kosan baru, masa pake gembok yang kuncinya dipegang semua orang?

2. Atur izin file yang bener:
   ```
   find /opt/bitnami/apache2/htdocs -type f -exec chmod 644 {} \;
   find /opt/bitnami/apache2/htdocs -type d -exec chmod 755 {} \;
   ```
   
   Ibarat mastiin semua jendela dan pintu udah kekunci dengan bener.

3. Amanin file .env lo:
   ```
   chmod 600 /opt/bitnami/apache2/htdocs/.env
   ```
   
   Ini kayak nyimpen nomer pin ATM di tempat yang super rahasia.

4. Pertimbangkan pake HTTPS dengan ngonfigurasi sertifikat SSL
   
   Anggep ini kayak upgrade dari satpam biasa jadi satpam bersenjata lengkap.

5. Rutin update aplikasi dan dependensinya
   
   Ini kayak rutin ganti password, biar makin aman terus.

## Troubleshooting (Kalo Ada Masalah)

### Gak Bisa Konek ke Router

1. Cek IP, username, dan password router lo (Ini kayak mastiin alamat tujuan sebelum nyasar)
2. Pastiin API service aktif di router Mikrotik lo (Satpam gak bisa kerja kalo belum dibangunin)
3. Cek port yang dibutuhin (8728 untuk API, 8729 untuk secure API) udah kebuka (Ini kayak mastiin pintu rumah gak digembok dari dalem)

### PHP Extensions Hilang

Kalo nemu error PHP extension gak ada, install pake:
```
sudo /opt/bitnami/php/bin/pecl install nama_extension
```

Terus tambahin extension ke file php.ini:
```
echo "extension=nama_extension.so" >> /opt/bitnami/php/etc/php.ini
```

Ini kayak HP lo gak bisa main game berat, terus lo download RAM tambahan (walaupun sebenernya gak bisa gitu sih).

### Masalah Izin File

Kalo nemu error izin, pastiin user Apache punya akses yang bener:
```
chown -R daemon:daemon /opt/bitnami/apache2/htdocs
```

Kayak ngasih duplikat kunci kosan ke pacar biar bisa masuk kapan aja (tapi hati-hati bro).

### Masalah OpenAI API

1. Cek API key lo udah bener di file .env (Ini kayak mastiin PIN ATM yang lo inget)
2. Pastiin Apache bisa akses variabel lingkungan (Satpam bisa baca list tamu)
3. Cek log API buat pesan error spesifik (Buka rekaman CCTV pas maling masuk)

## Bantuan

Kalo nemu masalah yang gak ada di panduan troubleshooting ini, silakan kontak support di support@h4n5vs.com atau buka issue di repositori GitHub project ini. Kayak nanya ke pawang hujan pas lagi banjir.

## Update Aplikasi

Buat update aplikasi ke versi terbaru:

1. Backup dulu instalasi lo yang sekarang:
   ```
   cp -r /opt/bitnami/apache2/htdocs /opt/bitnami/apache2/htdocs_backup
   ```
   
   Kayak fotokopi KTP sebelum nyerahin yang asli ke resepsionis hotel.

2. Masuk ke direktori aplikasi:
   ```
   cd /opt/bitnami/apache2/htdocs
   ```
   
   Kayak masuk ke rumah sendiri, tapi hati-hati ada renovasi.

3. Ambil perubahan terbaru (kalo pake Git):
   ```
   git pull origin main
   ```
   
   Ibarat lo update status hubungan di sosmed.

4. Update dependensi:
   ```
   composer update
   ```
   
   Kayak grocery shopping bulanan.

5. Restore file .env kalo perlu:
   ```
   cp /opt/bitnami/apache2/htdocs_backup/.env /opt/bitnami/apache2/htdocs/
   ```
   
   Ibarat balikin foto kenangan ke dompet baru setelah ganti dompet.

6. Benerin izin:
   ```
   chown -R daemon:daemon /opt/bitnami/apache2/htdocs
   ```
   
   Kayak mastiin semua pintu kebuka pake kunci yang sama.

7. Restart Apache:
   ```
   sudo /opt/bitnami/ctlscript.sh restart apache
   ```
   
   Ibarat reboot otak lo setelah begadang coding.

## Fungsi-Fungsi Utama Aplikasi (Biar Lo Paham)

### RouterOS API
Ini kayak TRANSLATOR antara bahasa Mikrotik sama bahasa aplikasi kita. Kalo dibayangin, RouterOS API itu kayak translator di PBB. Mikrotik ngomong pake bahasa alien, aplikasi kita ngomong pake bahasa PHP, terus RouterOS API ini yang menterjemahkan. "Eh bro, router lo bilang ada 999+ upaya login gagal nih, kayaknya ada yang mau bobol password!"

### AI Pattern Recognition
Kalo ini kayak detektif swasta yang super jenius. Tau gak detektif di film-film yang bisa nebak pelaku pembunuhan cuma dari lipatan baju korban? Nah AI kita gini! Dia cuma liat pola traffic data, langsung bisa bilang "Ini mah DDoS attack nih, gaya-gayanya anak 4chan lagi gabut malem Minggu."

### Traffic Monitoring
Ibarat lo jadi polisi yang mangkal di lampu merah. Semua kendaraan (data) yang lewat, lo catat: "Wah si B 1234 XX ngebut nih, B 5678 YY lampunya mati, B 9012 ZZ platnya kotor gak kebaca." Gitu, tapi yang dicatat bukan plat nomor tapi IP address dan port.

### Threat Mitigation
Ini JAGOAN kita! Kayak lo panggil Satria Baja Hitam pas diserang monster. Begitu aplikasi deteksi ada serangan, mitigation engine langsung bereaksi: "SIAP BOS! Firewall rule udah dipasang, IP penyerang diblokir, lubang keamanan ditambal, beres dah!"

### Dashboard
Dashboard itu kayak kokpit pesawat tapi buat keamanan jaringan. Pilot bisa tau mesin nomer 2 overheat dari lampu merah yang nyala, nah admin jaringan juga bisa tau "wah traffik tiba-tiba naik 500%, nih pasti ada yang DDoS!" dari dashboard H4N5VS yang kece abis.

## License

H4N5VS Mikrotik System Security dilisensikan di bawah Lisensi MIT. Lihat file LICENSE untuk detail. Intinya, jangan jual aplikasi ini tapi bilangnya buatan lo sendiri ya! Itu namanya nyolong, gak berkah!