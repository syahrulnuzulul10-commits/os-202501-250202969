
# Laporan Praktikum Minggu 1
Topik: "Arsitektur Sistem Operasi dan Kernel"

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori  
- **NIM**   : 250202969
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
1.Menjelaskan peran sistem operasi dalam arsitektur komputer.

2.Mengidentifikasi komponen utama OS, seperti kernel, system call, device driver, dan file system.

3.Membandingkan model arsitektur sistem operasi, yaitu monolithic kernel, layered approach, dan microkernel.

4.Membuat diagram sederhana arsitektur OS menggunakan alat bantu digital (misalnya draw.io atau Mermaid)

jawaban
1. Menjelaskan konsep dan fungsi system call dalam sistem operasi

Tujuan ini agar mahasiswa memahami bahwa system call adalah jembatan komunikasi antara program aplikasi dan kernel. Program tidak bisa langsung mengakses perangkat keras, sehingga system call digunakan untuk meminta layanan seperti membuka file, membaca data, membuat proses, atau berkomunikasi antarproses. Dengan memahami konsep ini, mahasiswa tahu bagaimana sistem operasi melayani perintah dari aplikasi.

2. Mengidentifikasi jenis-jenis system call dan fungsinya

Mahasiswa diharapkan dapat mengenali beberapa kategori utama system call, seperti:

Process Control: mengatur proses (contoh: fork(), exec(), exit()),

File Management: mengelola file (open(), read(), write()),

Device Management: berhubungan dengan perangkat (ioctl()),

Communication: mengatur komunikasi antarproses (pipe(), socket()).
Tujuan ini penting agar mahasiswa mengetahui fungsi dan peran masing-masing jenis system call dalam sistem operasi.

3. Mengamati alur perpindahan mode eksekusi dari user mode ke kernel mode

Tujuan ini membantu mahasiswa memahami mekanisme transisi antara dua mode CPU:

User mode → tempat program biasa berjalan dengan hak akses terbatas.

Kernel mode → tempat kernel menjalankan operasi dengan hak akses penuh.
Saat system call dipanggil, CPU berpindah dari user mode ke kernel mode agar operasi dapat dilakukan dengan aman dan dikontrol oleh OS.

4. Menggunakan perintah Linux untuk menampilkan dan menganalisis system call

Mahasiswa belajar menggunakan perintah seperti:

strace → untuk melacak system call yang dijalankan oleh suatu program,

dmesg → untuk melihat log aktivitas kernel.
Tujuan ini agar mahasiswa dapat melihat langsung interaksi antara aplikasi dan kernel, sehingga memahami bagaimana sistem operasi bekerja secara nyata, bukan hanya secara teori.

---

## Dasar Teori
Sistem Operasi (OS) merupakan komponen paling penting dalam komputer, karena tanpa OS, perangkat keras tidak dapat digunakan secara efektif oleh pengguna. OS berfungsi sebagai penghubung antara pengguna, aplikasi, dan perangkat keras, sehingga semua komponen komputer dapat bekerja secara terkoordinasi.

Di dalam OS terdapat kernel, yaitu bagian inti yang bertugas mengatur seluruh sumber daya sistem, seperti CPU untuk menjalankan proses, memori untuk penyimpanan sementara, hard disk/SSD untuk penyimpanan data permanen, serta perangkat input/output untuk komunikasi dengan pengguna.

Kernel memastikan bahwa setiap program mendapatkan sumber daya yang dibutuhkan secara adil dan aman, mencegah konflik antarproses, dan menjaga kestabilan sistem. Dengan demikian, sistem operasi memungkinkan komputer berfungsi dengan efisien, stabil, dan mudah digunakan, baik oleh pengguna langsung maupun oleh aplikasi yang berjalan di atasnya.
## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:

<img width="1920" height="1020" alt="syahrul@LAPTOP-FJMJEOG6_ ~ 15_10_2025 12_39_14" src="https://github.com/user-attachments/assets/f81c4c3e-3ba5-4c0c-966f-bd307097eea5" />

---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?
  jawaba
1. Analisis Hasil Percobaan

Perintah yang dijalankan:

whoami → menampilkan pengguna aktif (syahrul).
➜ Menunjukkan lapisan user space sedang aktif, artinya perintah dijalankan pada user mode.

uname -a → menampilkan informasi lengkap kernel.
➜ Hasilnya menunjukkan:

Linux LAPTOP-FJMJEOG6 6.6.87.2-microsoft-standard-WSL2 ...


Ini berarti sistem menggunakan kernel Linux versi 6.6.87.2 yang berjalan di atas WSL2 (Windows Subsystem for Linux 2).

lsmod | head → menampilkan modul kernel yang aktif.
➜ Modul seperti kvm_amd, battery, crc32c_intel menunjukkan driver kernel yang dimuat secara dinamis untuk mendukung perangkat keras dan virtualisasi.

dmesg | head → menampilkan pesan awal kernel saat boot.
➜ Terlihat bahwa kernel mendeteksi CPU dan memori dari BIOS serta melakukan inisialisasi sistem — ini adalah bagian dari proses booting kernel.

2. Hubungan dengan Teori Sistem Operasi

Fungsi Kernel:
Kernel adalah inti dari OS yang mengelola sumber daya (CPU, memori, I/O).
Hasil lsmod dan dmesg menunjukkan bahwa kernel menjalankan fungsinya dalam menginisialisasi dan mengatur driver perangkat keras.

System Call:
Ketika kamu menjalankan perintah seperti whoami atau uname, shell memanggil system call agar kernel mengeksekusi instruksi yang berhubungan dengan sistem (misalnya mengambil informasi pengguna atau kernel). Ini menunjukkan interaksi antara user space dan kernel space.

Arsitektur OS:
Lingkungan ini menggunakan arsitektur monolithic kernel (Linux) di mana modul seperti kvm, battery, dan intel_rapl dimuat langsung ke kernel.
Walaupun dijalankan di Windows, kernel Linux-nya tetap berdiri sendiri dalam lapisan virtualisasi (WSL2) — contoh implementasi hybrid architecture antara Linux dan Windows.

3. Perbedaan di Lingkungan OS Berbeda
Aspek	Linux (WSL2 / Native)	Windows
Kernel	Menggunakan kernel Linux monolithic	Kernel Windows (NT Kernel)
System Call	Menggunakan syscall Linux (POSIX) seperti uname(), getuid()	Menggunakan Windows API (Win32, NTAPI)
Manajemen Modul	Modul dapat dimuat/dilepas dinamis (lsmod, modprobe)	Driver dikelola oleh Device Manager
Interface CLI	Menggunakan bash shell	Menggunakan Command Prompt atau PowerShell
Akses Hardware	Langsung diatur oleh kernel Linux	Diatur oleh Windows NT Kernel

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.
Poin 1: Dari praktikum, kita melihat bahwa sistem operasi sangat penting dalam mengelola sumber daya hardware secara efisien.
Poin 2: Implementasi algoritma seperti penjadwalan proses membantu memahami konsep teoretis dan dampaknya pada performa.
Poin 3: Praktikum ini menunjukkan pentingnya keamanan dan efisiensi dalam desain OS.

---

## Quiz
1. Sebutkan tiga fungsi utama sistem operasi. 
   **Jawaban:**  Tiga fungsi utama sistem operasi adalah Manajemen Sumber Daya, Manajemen Proses dan File, serta Penyediaan Antarmuka Pengguna.
2. Jelaskan perbedaan antara kernel mode dan user mode.
   **Jawaban:**  tiga fungsi utama sistem operasi adalah Manajemen Sumber Daya (mengelola perangkat keras seperti CPU dan memori), Manajemen Proses dan File (mengelola eksekusi program dan sistem berkas), serta Penyediaan Antarmuka Pengguna (menyediakan cara bagi pengguna untuk berinteraksi dengan komputer)
3. Sebutkan contoh OS dengan arsitektur monolithic dan microkernel.
   **Jawaban:**  Contoh sistem operasi (OS) dengan arsitektur monolitik adalah Linux dan UNIX tradisional.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini? saya sangat bingung ketika dikasih tugas pertama dan saya gatau cara mengerjakan tugas yang dari dosen
- Bagaimana cara Anda mengatasinya? saya harus belajar entah entah dari teman/otodidak semoga saya bisa mengerjakan tugas-tugas selanjutnya
  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
