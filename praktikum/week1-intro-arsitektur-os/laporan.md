
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

4.Membuat diagram sederhana arsitektur OS menggunakan alat bantu digital (misalnya draw.io atau Mermaid).

---

## Dasar Teori
1.Definisi dan Fungsi Sistem Operasi: Sistem operasi adalah perangkat lunak yang mengelola hardware dan software resources, menyediakan interface untuk pengguna, dan memastikan eksekusi program yang efisien.
2.Manajemen Proses: Ini mencakup bagaimana OS menangani proses, termasuk pembuatan, penjadwalan, dan terminasi. Teori penjadwalan seperti FCFS, Round Robin, dll.
3.Manajemen Memori: Bagaimana OS mengalokasikan dan mengelola memori, termasuk paging, segmentation, dan virtual memory.
4.Manajemen File: Sistem file, bagaimana data disimpan, diakses, dan dikelola.
5.Sincronisasi dan Komunikasi Proses: Untuk sistem multiprogramming, termasuk mutex, semaphore, dan interprocess communication.

---

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
  jawaban
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

⚙️ 2. Hubungan dengan Teori Sistem Operasi

Fungsi Kernel:
Kernel adalah inti dari OS yang mengelola sumber daya (CPU, memori, I/O).
Hasil lsmod dan dmesg menunjukkan bahwa kernel menjalankan fungsinya dalam menginisialisasi dan mengatur driver perangkat keras.

System Call:
Ketika kamu menjalankan perintah seperti whoami atau uname, shell memanggil system call agar kernel mengeksekusi instruksi yang berhubungan dengan sistem (misalnya mengambil informasi pengguna atau kernel). Ini menunjukkan interaksi antara user space dan kernel space.

Arsitektur OS:
Lingkungan ini menggunakan arsitektur monolithic kernel (Linux) di mana modul seperti kvm, battery, dan intel_rapl dimuat langsung ke kernel.
Walaupun dijalankan di Windows, kernel Linux-nya tetap berdiri sendiri dalam lapisan virtualisasi (WSL2) — contoh implementasi hybrid architecture antara Linux dan Windows.

🪟 3. Perbedaan di Lingkungan OS Berbeda
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
