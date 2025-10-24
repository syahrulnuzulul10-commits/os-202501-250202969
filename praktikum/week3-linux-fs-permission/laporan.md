
# Laporan Praktikum Minggu 3
Topik: Manajemen File dan Permission di Linux

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori
- **NIM**   : 250202969
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  

1.Memahami struktur sistem file di Linux — Mahasiswa mampu mengenali hierarki direktori, navigasi antar folder, dan perintah dasar seperti ls, pwd, cd, dan cat.

2.Menguasai pengaturan hak akses file (permission) — Mahasiswa dapat menggunakan perintah chmod untuk mengubah izin akses (read, write, execute) pada file dan direktori.

3.Mempelajari pengaturan kepemilikan file (ownership) — Mahasiswa mampu menggunakan perintah chown untuk mengubah pemilik dan grup dari suatu file atau direktori.

4.Menganalisis fungsi dan hasil eksekusi perintah Linux — Mahasiswa dapat menjelaskan output yang dihasilkan dari setiap perintah dan kaitannya dengan manajemen file sistem.

5.Menerapkan dokumentasi dan manajemen versi menggunakan Git — Mahasiswa dapat membuat laporan hasil praktikum dengan struktur yang benar dan mengunggahnya ke repositori Git secara tepat waktu.

---

## Dasar Teori
1.Sistem Berkas (File System) di Linux
Linux menggunakan struktur file sistem hierarkis yang dimulai dari direktori root /. Semua file dan direktori diakses melalui jalur (path) tertentu. Pemahaman struktur ini penting untuk navigasi, manajemen file, dan konfigurasi sistem.

2.Permission (Hak Akses File)
Setiap file dan direktori di Linux memiliki tiga jenis izin akses: read (r), write (w), dan execute (x). Izin ini dibagi menjadi tiga kelompok pengguna: owner, group, dan others. Kombinasi ketiganya menentukan siapa yang dapat membaca, menulis, atau mengeksekusi file.

3.Perintah chmod (Change Mode)
chmod digunakan untuk mengubah hak akses file. Izin dapat diatur menggunakan mode simbolik (misalnya u+x) atau numerik (misalnya chmod 755 file). Pengaturan yang tepat penting untuk menjaga keamanan dan mencegah akses tidak sah.

4.Perintah chown (Change Owner)
chown digunakan untuk mengubah kepemilikan file atau direktori. Setiap file memiliki owner dan group. Hanya pengguna dengan hak administratif (root) yang dapat mengganti kepemilikan file orang lain.

5.Keamanan dan Manajemen Akses di Linux
Kombinasi antara permission (chmod) dan ownership (chown) merupakan dasar sistem keamanan file Linux. Pengaturan yang benar memastikan file penting hanya dapat diakses oleh pengguna yang berwenang, sehingga melindungi integritas dan kerahasiaan data.

---

## Langkah Praktikum
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).
   - Pastikan folder kerja berada di dalam direktori repositori Git praktikum:
     ```
     praktikum/week3-linux-fs-permission/
     ```

2. **Eksperimen 1 – Navigasi Sistem File**
   Jalankan perintah berikut:
   ```bash
   pwd
   ls -l
   cd /tmp
   ls -a
   ```
   - Jelaskan hasil tiap perintah.
   - Catat direktori aktif, isi folder, dan file tersembunyi (jika ada).

3. **Eksperimen 2 – Membaca File**
   Jalankan perintah:
   ```bash
   cat /etc/passwd | head -n 5
   ```
   - Jelaskan isi file dan struktur barisnya (user, UID, GID, home, shell).

4. **Eksperimen 3 – Permission & Ownership**
   Buat file baru:
   ```bash
   echo "Hello <NAME><NIM>" > percobaan.txt
   ls -l percobaan.txt
   chmod 600 percobaan.txt
   ls -l percobaan.txt
   ```
   - Analisis perbedaan sebelum dan sesudah chmod.  
   - Ubah pemilik file (jika memiliki izin sudo):
   ```bash
   sudo chown root percobaan.txt
   ls -l percobaan.txt
   ```
   - Catat hasilnya.

5. **Eksperimen 4 – Dokumentasi**
   - Ambil screenshot hasil terminal dan simpan di:
     ```
     praktikum/week3-linux-fs-permission/screenshots/
     ```
   - Tambahkan analisis hasil pada `laporan.md`.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 3 - Linux File System & Permission"
   git push origin main
   ```

---
## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
 ```bash
   pwd
   ls -l
   cd /tmp
   ls -a
   ```
 ```bash
   cat /etc/passwd | head -n 5
   ```
```bash
   echo "Hello <NAME><NIM>" > percobaan.txt
   ls -l percobaan.txt
   chmod 600 percobaan.txt
   ls -l percobaan.txt
   ```
 ```bash
   sudo chown root percobaan.txt
   ls -l percobaan.txt
   ```

---
  

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:

<img width="1220" height="768" alt="Cuplikan layar 2025-10-22 163637" src="https://github.com/user-attachments/assets/1dbc37d8-3729-49f7-98d5-abb8ac006133" />

---

## Eksperimen 1
1. Perintah: pwd
   Memiliki fungsi untuk menampilkan direktori kerja (current working directory) tempat user berada saat ini.

Hasil:
```bash
/home/syahrul
```
Analisis:
Menunjukkan bahwa user sedang berada di direktori home milik pengguna bernama ervitadwyn.

2. Perintah: ls -l
   Memiliki fungsi menampilkan daftar isi direktori dalam format panjang (long listing), yang mencakup:
   -Jenis file dan izin (permission)
   -Jumlah link
   -Pemilik (owner)
   -Grup
   -Ukuran file (byte)
   -Tanggal dan waktu modifikasi
   -Nama file atau folder

Hasil:
```bash
-rw-r--r-- 1 syahrul syahrul ... percobaan.txt
```
Analisis:
Isi folder hanya ada satu file yaitu percobaan.txt, dengan izin:
-Pemilik: baca dan tulis (rw-)
-Grup: baca (r--)
-Lainnya: baca (r--)

3. Perintah: cd /tmp
   Memiliki fungsi untuk berpindah ke direktori sementara (temporary directory) milik sistem Linux.

Hasil:
Tidak ada pesan error, artinya perintah berhasil dijalankan.
-Direktori aktif sekarang: /tmp

4. Perintah: ls -a
   Memiliki fungsi menampilkan semua isi direktori, termasuk file tersembunyi (yang diawali dengan tanda titik .).

Hasil:
```bash
.  
..  
.X11-unix  
snap-private-tmp  
systemd-private-...  
```
| Perintah  | Fungsi                                                                 | Contoh Output                                          | Penjelasan                                  |
| --------- | ---------------------------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------- |
| `pwd`     | Menampilkan direktori aktif (current directory)                        | `/home/syahrul/praktikum/week3-linux-fs-permission`    | Menunjukkan di folder mana kamu bekerja     |
| `ls -l`   | Menampilkan daftar file secara detail (izin, pemilik, ukuran, tanggal) | `-rw-r--r-- 1 syahrul syahrul 20 Oct 24 percobaan.txt` | Terdapat 10 karakter izin: `rw-r--r--`      |
| `cd /tmp` | Pindah ke folder `/tmp`                                                | —                                                      | Direktori sementara sistem                  |
| `ls -a`   | Menampilkan semua file termasuk yang tersembunyi (`.` dan `..`)        | `. .. log.txt cache.tmp`                               | File tersembunyi diawali dengan titik (`.`) |

---
## Eksperimen 2
Perintah:
```bash
cat /etc/passwd | head -n 5
```
Memiliki fungsi untuk menampilkan isi file /etc/passwd yang berisi daftar semua user (pengguna) yang terdaftar di sistem Linux.
| head -n 5 → hanya menampilkan 5 baris pertama dari isi file tersebut.
seperti :
```bash
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```
Struktur Setiap Baris /etc/passwd

Setiap baris berisi informasi tentang satu akun pengguna dengan 7 kolom yang dipisahkan oleh tanda titik dua (:):
|  No | Kolom       | Nama Field            | Keterangan                                                                                                            |
| :-: | :---------- | :-------------------- | :-------------------------------------------------------------------------------------------------------------------- |
|  1  | `root`      | **Username**          | Nama akun pengguna (login name).                                                                                      |
|  2  | `x`         | **Password**          | Dulu berisi password terenkripsi, sekarang digantikan dengan `x` karena password disimpan di file lain `/etc/shadow`. |
|  3  | `0`         | **UID (User ID)**     | Nomor identitas unik untuk pengguna. UID 0 = superuser (root).                                                        |
|  4  | `0`         | **GID (Group ID)**    | Nomor identitas grup utama pengguna.                                                                                  |
|  5  | `root`      | **GECOS / Deskripsi** | Keterangan singkat (biasanya nama lengkap atau info tambahan).                                                        |
|  6  | `/root`     | **Home Directory**    | Lokasi direktori utama milik pengguna.                                                                                |
|  7  | `/bin/bash` | **Login Shell**       | Shell default yang dijalankan ketika user login (contohnya Bash).         


Contoh Analisis Tiap Baris:

| Baris | Username | UID | GID   | Home Directory    | Shell                                             | Keterangan                                 |
| :---: | :------- | :-- | :---- | :---------------- | :------------------------------------------------ | :----------------------------------------- |
|   1   | root     | 0   | 0     | /root             | /bin/bash                                         | Superuser, memiliki akses penuh ke sistem. |
|   2   | daemon   | 1   | 1     | /usr/sbin/nologin | Tidak bisa login, digunakan untuk layanan sistem. |                                            |
|   3   | bin      | 2   | 2     | /usr/sbin/nologin | Akun sistem untuk menjalankan program biner.      |                                            |
|   4   | sys      | 3   | 3     | /usr/sbin/nologin | Akun sistem untuk proses sistem internal.         |                                            |
|   5   | sync     | 4   | 65534 | /bin/sync         | Akun sistem khusus untuk perintah sinkronisasi.   |                                            |

Kesimpulan:
File /etc/passwd menyimpan data semua akun pengguna di sistem, termasuk akun sistem dan akun manusia.
Setiap baris berisi informasi login, identitas, dan konfigurasi shell pengguna yang digunakan saat sistem berjalan.

## Eksperimen 3

1. Membuat File Baru
```bash
echo "Hello <NAME><NIM>" > percobaan.txt
```
Berfungsi membuat file bernama percobaan.txt dan menuliskan teks Hello <NAME><NIM> ke dalamnya.
Hasilnya file baru percobaan.txt berhasil dibuat di direktori aktif.

Isi file:
Hello <NAME><NIM>

2. Melihat Detail File (Sebelum chmod)
```bash  
ls -l percobaan.txt
```
Contoh hasil:
```bash  
-rw-r--r-- 1 syahrul syahrul 27 Oct 22 16:33 percobaan.txt
```
Analisis hak akses (-rw-r--r--):
- User (syahrul): dapat membaca dan menulis file (rw-)
- Group: hanya dapat membaca (r--)
- Others: hanya dapat membaca (r--)
Artinya semua pengguna bisa membaca file ini, tapi hanya pemilik yang bisa mengubah isinya.

3. Mengubah Hak Akses File
```bash  
chmod 600 percobaan.txt
```
Berfungsi mengatur izin file agar hanya pemilik yang bisa membaca dan menulis file.

4. Melihat Detail File (Sesudah chmod)
```bash  
ls -l percobaan.txt
```
Contoh hasil:
```bash  
-rw------- 1 syahrul syahrul 27 Oct 22 oct 16:33 percobaan.txt
```
Analisis perubahan:
Sebelum chmod 600	Sesudah chmod 600	Perubahan
-rw-r--r--	-rw-------	Grup dan pengguna lain tidak lagi bisa membaca file.

- Kesimpulan perubahan:
chmod 600 memperketat keamanan file agar hanya pemilik (owner) yang dapat mengaksesnya (membaca/menulis), sementara pengguna lain tidak punya izin apa pun.

5. Mengubah Pemilik File (dengan sudo)
```bash
sudo chown root percobaan.txt
```
Berfungsi mengubah pemilik file menjadi root (administrator sistem).

6. Melihat Detail File (Setelah chown)
```bash
ls -l percobaan.txt
```
Contoh hasil:
```bash
-rw------- 1 root syahrul 27 Oct 22 16:33 percobaan.txt
```

Analisis hasil:

Kolom	Sebelum chown	Sesudah chown	Keterangan
Owner	ervitadwyn	root	File kini dimiliki oleh user root
Group	ervitadwyn	ervitadwyn	Grup tetap sama
Permission	rw-------	rw-------	Tidak berubah (masih hanya owner yang bisa akses)

Kesimpulan Akhir Percobaan
No	Perintah	Fungsi	Hasil	Kesimpulan

1.	echo "Hello <NAME><NIM>" > percobaan.txt	Membuat file baru	File percobaan.txt berisi teks Hello	File berhasil dibuat

2.	ls -l percobaan.txt	Menampilkan detail file	-rw-r--r-- ervitadwyn	Semua user bisa membaca file

3.	chmod 600 percobaan.txt	Mengubah izin file	-rw-------	Hanya pemilik bisa membaca/menulis

4.	sudo chown root percobaan.txt	Mengubah pemilik file	owner = root	File menjadi milik user root

5.	ls -l percobaan.txt (akhir)	Melihat hasil akhir	-rw------- 1 root ervitadwyn ...	File kini hanya bisa diakses oleh root

## Analisis
1.Makna Hasil Percobaan
---

Dari seluruh percobaan yang dilakukan, dapat dipahami bahwa sistem operasi Linux memiliki mekanisme pengaturan file yang sangat terstruktur dan aman.

Melalui perintah pwd, ls, dan cd, pengguna dapat melakukan navigasi sistem file secara hierarkis, yang menggambarkan bahwa Linux menggunakan model direktori tunggal yang berakar pada direktori root (/).

Perintah cat /etc/passwd menunjukkan bagaimana Linux menyimpan data pengguna dalam file teks sistem yang mudah dibaca, tetapi dilindungi oleh hak akses tertentu agar tidak disalahgunakan.

Perintah chmod dan chown menunjukkan bahwa setiap file di Linux memiliki tiga lapisan izin akses (owner, group, others). Dengan mengubah nilai permission (misalnya rw-r--r-- menjadi rw-------), pengguna dapat mengatur siapa yang boleh membaca, menulis, atau mengeksekusi file tersebut.

Ketika izin diubah menjadi 600, hanya pemilik file yang dapat mengaksesnya — hal ini mencerminkan penerapan prinsip keamanan berbasis otorisasi pengguna (user-based access control).

Makna utama dari hasil percobaan ini adalah bahwa pengelolaan hak akses di Linux tidak hanya bergantung pada pengguna, tetapi juga dikontrol langsung oleh kernel, sehingga mencegah modifikasi atau akses tidak sah terhadap file sistem.

2.Hubungan Hasil dengan Teori (Kernel, System Call, dan Arsitektur OS)
   ---

Secara teoretis, kernel adalah inti dari sistem operasi yang bertugas mengatur semua sumber daya perangkat keras dan memberikan layanan dasar bagi program pengguna. Ketika pengguna menjalankan perintah seperti chmod, chown, atau ls, perintah tersebut tidak langsung mengakses perangkat keras, melainkan mengirimkan permintaan ke kernel melalui system call.

Contohnya:

Saat pengguna menjalankan chmod 600 percobaan.txt, shell akan memanggil system call chmod(). Kernel kemudian mengubah metadata izin file pada sistem berkas (file system) sesuai permintaan.

Saat chown root percobaan.txt dijalankan, shell memanggil system call chown(), dan kernel memperbarui identitas pemilik file di tabel inode (struktur data file system).

Proses ini menunjukkan bahwa semua perubahan yang terjadi di sistem file Linux dikendalikan oleh kernel melalui interface system call, bukan oleh program pengguna secara langsung.
Dengan demikian, hasil percobaan mendukung teori bahwa kernel bertindak sebagai penghubung antara user space dan hardware, memastikan keamanan serta stabilitas sistem operasi.

Arsitektur Linux yang berbasis monolitik kernel juga memungkinkan semua fungsi manajemen file — seperti izin, kepemilikan, dan keamanan — dilakukan secara efisien di tingkat kernel, tanpa perlu interaksi tambahan dari sistem eksternal.

3.Perbedaan Hasil di Lingkungan OS Berbeda (Linux vs Windows)
   ---

Jika percobaan serupa dilakukan di sistem operasi Windows, hasil dan konsep yang diperoleh akan berbeda secara signifikan:

| Aspek                            | Linux                                                                                                          | Windows                                                                                    |
| :------------------------------- | :------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------- |
| **Model izin akses**             | Menggunakan sistem *owner–group–others* dengan kode numerik (mis. 755, 600)                                    | Menggunakan *Access Control List (ACL)* yang berisi daftar pengguna dan izin spesifik      |
| **Pengelolaan kepemilikan file** | Diatur melalui `chown` dan dikontrol kernel                                                                    | Diatur melalui *Properties → Security → Owner*                                             |
| **Implementasi kernel**          | *Monolithic kernel* – semua fungsi (file system, permission, process management) dijalankan langsung di kernel | *Hybrid kernel* – beberapa fungsi keamanan dan manajemen file dilakukan di level user mode |
| **Perintah kontrol izin**        | `chmod`, `chown`, `ls -l`                                                                                      | GUI (klik kanan → Properties) atau `icacls` di CMD                                         |
| **Fokus keamanan**               | Sederhana, efisien, berbasis pengguna                                                                          | Lebih kompleks, berbasis objek dan grup pengguna                                           |

Dengan demikian, Linux lebih transparan dan efisien dalam pengelolaan izin karena setiap tindakan berbasis terminal langsung terhubung ke kernel, sementara Windows lebih fleksibel dan berorientasi GUI, tetapi memerlukan lapisan tambahan untuk manajemen izin.

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Quiz
1. Apa fungsi dari perintah chmod?
 **Jawaban:**
chmod digunakan untuk mengubah hak akses (permission) pada file atau direktori di Linux. Dengan perintah ini, pengguna dapat menentukan siapa yang boleh membaca (r), menulis (w), atau mengeksekusi (x) file tersebut — baik untuk pemilik (owner), grup (group), maupun pengguna lain (others).

2. Apa arti dari kode permission rwxr-xr--?
 **Jawaban:**
Kode rwxr-xr-- menunjukkan hak akses sebagai berikut:

Owner: rwx → dapat membaca, menulis, dan mengeksekusi.

Group: r-x → dapat membaca dan mengeksekusi, tapi tidak dapat menulis.

Others: r-- → hanya dapat membaca.
Jadi, hanya pemilik file yang dapat mengedit file tersebut, sedangkan grup dan pengguna lain hanya bisa membacanya (grup bisa menjalankannya juga).

3. Jelaskan perbedaan antara chown dan chmod.
**Jawaban:**  
chmod digunakan untuk mengubah hak akses (permission) terhadap file atau direktori.

chown digunakan untuk mengubah kepemilikan (ownership) file atau direktori, yaitu siapa pemiliknya (user) dan grupnya.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
