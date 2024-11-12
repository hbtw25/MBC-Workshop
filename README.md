
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
![image](https://user-images.githubusercontent.com/44178372/114246503-11a1f100-9993-11eb-83e6-7466f1a298eb.png)
Kata sandi ditemukan menggunakan teknik brute force, lalu masuk sebagai root.
#### Koreksi
Ganti kata sandi dengan yang lebih kuat dan batasi hak istimewa.

---

Apakah format ini sudah lengkap dan sesuai kebutuhan?
