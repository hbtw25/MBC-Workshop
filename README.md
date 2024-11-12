Berikut adalah terjemahan lengkap termasuk bagian referensi untuk tiap ancaman:

# Metasploitable 2

## Konfigurasi

### Langkah 1: Unduh
- Untuk audit pentest ini, kita akan menggunakan instance Metasploit ini:

    https://information.rapid7.com/metasploitable-download.html
    https://sourceforge.net/projects/metasploitable/

    Catatan: Dengan instance yang saya gunakan, kita tidak memiliki kata sandi untuk mengakses server.

### Langkah 2: Produk Virtualisasi
- Ekstrak file
- Gunakan VMWare atau VirtualBox untuk menambahkan VM

### Langkah 3: Konfigurasi Virtual
- Tempatkan mesin pada subnet yang sama dengan mesin penyerang

IP VM Metasploitable 2 adalah 192.168.10.100/24

### Langkah 4: Mulai
- Jalankan kedua VM

### Peringatan
Jangan pernah mengekspos VM Metasploitable ke internet, selalu gunakan secara lokal.

Direkomendasikan menggunakan VM Kali untuk menjalankan serangan, bisa diunduh di sini:
[Kali Offensive Security](https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/#1572305786534-030ce714-cc3b)

## Saatnya Memulai Serangan

---

### Ancaman No. 1: Netcat bindshell – Metasploitable root shell – Port 1524
#### Deskripsi
Shell superuser tersedia di port 1524.
#### Referensi
Tidak ada
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114245936-b3c0d980-9991-11eb-9b8a-a7717ea3fdb4.png)
Masuk sebagai root.
#### Koreksi
Nonaktifkan port ini serta shell jika tidak diperlukan.

---

### Ancaman No. 2: Backdoor FTP – vsftpd 2.3.4 – Port 21
#### Deskripsi
Kerentanan ini terkait dengan backdoor yang ditambahkan pada arsip unduhan VSFTPD antara 30 Juni 2011 dan 1 Juli 2011.
#### Referensi
https://www.rapid7.com/db/modules/exploit/unix/ftp/vsftpd_234_backdoor/
#### Operasi dan Dampak
Menggunakan exploit pada Metasploit dan masuk sebagai root.
![image](https://user-images.githubusercontent.com/44178372/114246273-7f015200-9992-11eb-972b-60d1e7b5b02c.png)
#### Koreksi
Perbarui versi FTP.

---

### Ancaman No. 3: VNC – Port 5900
#### Deskripsi
Kata sandi untuk menghubungkan ke port VNC lemah.
#### Referensi
https://www.rapid7.com/db/modules/auxiliary/scanner/vnc/vnc_login/
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114246477-fcc55d80-9992-11eb-9a8c-1ba9a3d1c1bb.png)
Menggunakan backdoor untuk mendapatkan kata sandi, kemudian login dan mendapatkan antarmuka grafis.
![image](https://user-images.githubusercontent.com/44178372/114246480-fdf68a80-9992-11eb-9a8e-ad5a8fbb49b8.png)

![image](https://user-images.githubusercontent.com/44178372/114246495-08b11f80-9993-11eb-8141-3c774ccfad9d.png)

![image](https://user-images.githubusercontent.com/44178372/114246503-11a1f100-9993-11eb-83e6-7466f1a298eb.png)
#### Koreksi
Ubah kata sandi menjadi yang lebih kuat.

---

### Ancaman No. 4: Layanan “R” – Port 512/513/514
#### Deskripsi
Port TCP 512, 513, dan 514 dapat memungkinkan penyerang masuk jika dikonfigurasi dengan salah. Layanan Remote Shell RSH (rsh, rexec, rlogin) aktif.
#### Referensi
Tidak ada
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114246554-36966400-9993-11eb-9172-d010c5176aa9.png)
Menggunakan perintah rlogin dengan tool rsh-client untuk masuk sebagai root.
#### Koreksi
Nonaktifkan atau gunakan firewall untuk mengamankan layanan ini.

---

### Ancaman No. 5: NFS – Port 2049
#### Deskripsi
Tidak ada autentikasi yang diperlukan untuk melakukan tindakan sensitif pada port 2049.
#### Referensi
Tidak ada
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114246610-53329c00-9993-11eb-87ec-93df83c6b6ab.png)
Menggunakan NFS untuk menambahkan kunci SSH.

![image](https://user-images.githubusercontent.com/44178372/114246615-56c62300-9993-11eb-8b2d-cd0ee85988cc.png)

![image](https://user-images.githubusercontent.com/44178372/114246627-5e85c780-9993-11eb-9566-4232c7725d89.png)
#### Koreksi
Tambahkan autentikasi sebelum mengirimkan file/folder.

---

### Ancaman No. 6: Backdoor IRC – UnrealIRCd – Port 6667
#### Deskripsi
Kerentanan ini terkait dengan port 6667 yang menjalankan daemon UnrealIRCd versi rentan.
#### Referensi
https://www.rapid7.com/db/modules/exploit/unix/irc/unreal_ircd_3281_backdoor/
https://www.cvedetails.com/vulnerability-list/vendor_id-10938/Unrealircd.html
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114246716-9725a100-9993-11eb-926c-c91a9371f919.png)
Masuk sebagai root.
#### Koreksi
Perbarui versi IRC.

---


---

### Ancaman No. 7: Netbios-ssn – Samba smbd 3.X – 4.X – Port 139/445
#### Deskripsi
Kerentanan ini terkait dengan kerentanan eksekusi perintah pada Samba versi 3.0.20 hingga 3.0.25rc3.
#### Referensi
https://www.rapid7.com/db/modules/exploit/multi/samba/usermap_script/
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114246716-9725a100-9993-11eb-926c-c91a9371f919.png)
Menggunakan exploit pada Metasploit dan masuk sebagai root.
#### Koreksi
Perbarui versi Samba.

---

### Ancaman No. 8: Java-rmi – Port 1099
#### Deskripsi
Kerentanan ini terkait dengan konfigurasi RMI registry default yang memungkinkan pengunduhan kelas dari URL jarak jauh.
#### Referensi
https://www.rapid7.com/db/modules/exploit/multi/misc/java_rmi_server/
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114246477-fcc55d80-9992-11eb-9a8c-1ba9a3d1c1bb.png)
Menggunakan exploit pada Metasploit untuk mendapatkan akses superuser.

![image](https://user-images.githubusercontent.com/44178372/114246891-1d41e780-9994-11eb-907a-c6873cf40542.png)
#### Koreksi
Perbarui versi Java.

---

### Ancaman No. 9: MySQL – Port 3306
#### Deskripsi
MySQL diinstal dengan kata sandi default pada akun root.
#### Referensi
Tidak ada
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114246554-36966400-9993-11eb-9172-d010c5176aa9.png)
Kata sandi default digunakan untuk mengakses database.
#### Koreksi
Ubah kata sandi menjadi lebih kuat.

---

### Ancaman No. 10: Akun Msfadmin
#### Deskripsi
Akun msfadmin memiliki hak istimewa yang berlebihan dan kata sandi yang lemah.
#### Referensi
https://www.cnil.fr/fr/generer-un-mot-de-passe-solide
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114247026-6eea7200-9994-11eb-9794-56a55b8a6fb0.png)

We list all the admins rights of the account.
![image](https://user-images.githubusercontent.com/44178372/114247045-7742ad00-9994-11eb-8340-69b734f40973.png)

We become root.
![image](https://user-images.githubusercontent.com/44178372/114247057-7f025180-9994-11eb-877d-9ec0848d4a89.png)
Kata sandi ditemukan menggunakan teknik brute force, lalu masuk sebagai root.
#### Koreksi
Ganti kata sandi dengan yang lebih kuat dan batasi hak istimewa.

---

### Ancaman No. 11: Telnet – Port 23
#### Deskripsi
Telnet adalah protokol yang tidak terenkripsi, sehingga mengirim data sensitif (nama pengguna dan kata sandi) dalam bentuk teks biasa.
#### Referensi
https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-115.pdf  
https://www.pcisecuritystandards.org/document_library
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114247095-95a8a880-9994-11eb-8207-aae5726aad65.png)
Telnet memungkinkan akses tanpa enkripsi, yang rentan terhadap pengintipan data.
#### Koreksi
Nonaktifkan layanan ini kecuali jika diperlukan.

---

### Ancaman No. 12: SSH – Port 22
#### Deskripsi
Kata sandi akun pengguna dan msfadmin terlalu lemah.
#### Referensi
Tidak ada
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114247150-b670fe00-9994-11eb-858e-3c00db3a3f03.png)

![image](https://user-images.githubusercontent.com/44178372/114247156-b8d35800-9994-11eb-9b6a-cb402e58f950.png)

![image](https://user-images.githubusercontent.com/44178372/114247159-ba9d1b80-9994-11eb-94ff-262c9f176aa3.png)
Kata sandi yang lemah memungkinkan akses root yang tidak aman.
#### Koreksi
Ubah kata sandi menjadi kata sandi yang kuat.

---

### Ancaman No. 13: PostgreSQL – PostgreSQL DB 8.3.0 - 8.3.7 – Port 5432
#### Deskripsi
Kata sandi akun postgres masih menggunakan kata sandi default.
#### Referensi
Tidak ada
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114247192-cc7ebe80-9994-11eb-9b06-9744c63d5cce.png)

![image](https://user-images.githubusercontent.com/44178372/114247194-cdafeb80-9994-11eb-9242-1299f9e37ccb.png)

![image](https://user-images.githubusercontent.com/44178372/114247197-cf79af00-9994-11eb-94e4-cbb720eab85b.png)
Akses mudah menggunakan kata sandi default memungkinkan kendali pada basis data PostgreSQL.
#### Koreksi
Ubah kata sandi default ke yang lebih kuat.

---

### Ancaman No. 14: HTTP – Port 80
#### Deskripsi
Terdapat halaman phpinfo.php yang menampilkan informasi sensitif versi PHP.
#### Referensi
https://www.rapid7.com/db/modules/exploit/multi/http/php_cgi_arg_injection/
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114247297-0ea80000-9995-11eb-9ab2-41d70f78b2cf.png)

![image](https://user-images.githubusercontent.com/44178372/114247302-110a5a00-9995-11eb-9da1-6c83a4a5aa55.png)
Versi PHP memungkinkan eksekusi exploit melalui Metasploit, memungkinkan akses sebagai pengguna www-data.

![image](https://user-images.githubusercontent.com/44178372/114247337-25e6ed80-9995-11eb-9840-3f54714f7e6e.png)

![image](https://user-images.githubusercontent.com/44178372/114247350-2d0dfb80-9995-11eb-9b52-1ccd73d0397c.png)
#### Koreksi
Perbarui versi PHP dan hapus halaman phpinfo.php.

---

### Ancaman No. 15: Versi Kernel
#### Deskripsi
Versi Kernel sudah usang dan memiliki beberapa kerentanan.
#### Referensi
https://www.cvedetails.com/vulnerability-list/vendor_id-33/product_id-47/version_id-123221/Linux-Linux-Kernel-2.6.24.html
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114247409-529b0500-9995-11eb-8ade-e45ffaff2b79.png)
![image](https://user-images.githubusercontent.com/44178372/114247426-59c21300-9995-11eb-8026-f2dd3b89ff71.png)
Versi Kernel yang teridentifikasi rentan terhadap beberapa exploit yang memungkinkan akses root.
#### Koreksi
Perbarui versi Kernel.

---

### Ancaman No. 16: SMTP – Port 25
#### Deskripsi
Port SMTP tidak terlindungi dengan baik.
#### Referensi
https://www.rapid7.com/db/modules/auxiliary/scanner/smtp/smtp_enum/
#### Operasi dan Dampak
![image](https://user-images.githubusercontent.com/44178372/114247483-79593b80-9995-11eb-9c22-345a98f48a81.png)

![image](https://user-images.githubusercontent.com/44178372/114247486-7b22ff00-9995-11eb-9ca4-81c59d069694.png)
Port ini memungkinkan enumerasi pengguna yang dapat disalahgunakan.
#### Koreksi
Lindungi port 25 menggunakan firewall atau nonaktifkan jika tidak diperlukan.

---


