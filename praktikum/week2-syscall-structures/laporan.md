
# Laporan Praktikum Minggu 2
Topik: Arsitektur Sistem Operasi dan Kernel

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori  
- **NIM**   : 250202969
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
1.Menjelaskan konsep dan fungsi system call dalam sistem operasi.
2.Mengidentifikasi jenis-jenis system call dan fungsinya.
3.Mengamati alur perpindahan mode user ke kernel saat system call terjadi.
4.Menggunakan perintah Linux untuk menampilkan dan menganalisis system call.
jawaban
. Konsep dan Fungsi System Call dalam Sistem Operasi

System call adalah mekanisme komunikasi antara program aplikasi (user mode) dan kernel (kernel mode).
Program tidak bisa langsung mengakses perangkat keras karena alasan keamanan, sehingga system call digunakan untuk meminta layanan dari sistem operasi, seperti membuka file, membuat proses, atau membaca data.

Fungsinya:

Menjadi antarmuka aman antara aplikasi dan kernel.

Mengatur akses sumber daya seperti file, memori, dan perangkat I/O.

Menyediakan layanan sistem standar tanpa harus tahu detail perangkat keras.

2. Jenis-Jenis System Call dan Fungsinya

System call dibagi menjadi beberapa kategori utama:

Kategori	Contoh System Call	Fungsi Utama
Process Control	fork(), exec(), wait(), exit()	Mengatur pembuatan dan pengelolaan proses.
File Management	open(), read(), write(), close()	Mengakses dan memanipulasi file.
Device Management	ioctl(), read(), write()	Mengatur interaksi dengan perangkat keras.
Communication	pipe(), socket(), send(), recv()	Mengatur komunikasi antarproses atau jaringan.
Information Maintenance	getpid(), time(), uname()	Mengambil informasi sistem dan status proses.
3. Alur Perpindahan Mode User ke Kernel Saat System Call Terjadi

Saat aplikasi memanggil system call, CPU melakukan transisi dari user mode ke kernel mode agar kernel bisa menjalankan tugas dengan hak akses penuh.

Urutan alurnya:

Program di user mode memanggil fungsi (misalnya printf() → write()).

Fungsi ini memicu trap atau interrupt ke kernel.

CPU berpindah ke kernel mode dan menjalankan layanan yang diminta.

Kernel mengembalikan hasilnya ke aplikasi dan kembali ke user mode.

- Proses ini memastikan keamanan dan kestabilan sistem karena hanya kernel yang boleh mengakses perangkat keras langsung.

4. Menggunakan Perintah Linux untuk Menampilkan dan Menganalisis System Call
Perintah	Fungsi / Hasil
strace ls	Menampilkan daftar system call yang dijalankan saat perintah ls dijalankan.
strace -e trace=open,read,write,close cat /etc/passwd	Menelusuri system call yang digunakan untuk operasi file.
`dmesg	tail -n 10`

- Dengan perintah strace, kita dapat melihat system call mana saja yang dipanggil oleh suatu program.
- Dengan dmesg, kita bisa mengamati aktivitas kernel, yang berbeda dari output program biasa.



---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.
Peran Sistem Operasi (OS):
Sistem operasi adalah perantara antara pengguna dan perangkat keras komputer yang mengatur penggunaan sumber daya seperti CPU, memori, file, dan perangkat input/output agar bekerja secara efisien dan aman.

Konsep System Call:
System call merupakan mekanisme utama komunikasi antara program aplikasi dan kernel, yang memungkinkan aplikasi melakukan operasi seperti membaca file, membuat proses, atau mengakses perangkat tanpa langsung berhubungan dengan hardware.

Mode Eksekusi – User Mode & Kernel Mode:
Sistem operasi membagi eksekusi menjadi dua mode:

User mode: tempat program biasa berjalan dengan hak akses terbatas.

Kernel mode: dijalankan oleh sistem operasi dengan hak akses penuh terhadap perangkat keras.
Transisi antar mode terjadi saat program memanggil system call.

Kategori System Call:
System call dibagi menjadi beberapa kelompok utama, yaitu:

Process Control (mengelola proses)

File Management (operasi file)

Device Management (interaksi dengan perangkat)

Communication (komunikasi antarproses)

Analisis Melalui Percobaan (strace & dmesg):
Percobaan dengan perintah strace dan dmesg digunakan untuk mengamati aktivitas system call dan log kernel, sehingga mahasiswa dapat memahami alur kerja sistem operasi saat melayani permintaan dari aplikasi.

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
strace ls
strace -e trace=open,read,write,close cat /etc/passwd
dmesg | tail -n 10
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
<img width="1919" height="1024" alt="Cuplikan layar 2025-10-15 194612" src="https://github.com/user-attachments/assets/8e694378-61f0-4fb6-abb2-64ff39dc0c00" />


---


## Analisis
1). Analisis bagaimana file dibuka, dibaca, dan ditutup oleh kernel.
2). Amati log kernel yang muncul. Apa bedanya output ini dengan output dari program biasa?
jawaban
1). Proses Pembukaan File (open)

Saat perintah cat /etc/passwd dijalankan, kernel pertama kali memanggil system call open() atau openat() untuk membuka file /etc/passwd.

Pada tahap ini, kernel memeriksa:

Apakah file ada di lokasi yang diminta,

Apakah user memiliki izin untuk membacanya,

Dan jika berhasil, kernel memberikan file descriptor (biasanya angka 3) ke proses cat.
- Makna: file berhasil dibuka dan siap diakses oleh program.

2. Proses Pembacaan File (read)

Setelah file berhasil dibuka, kernel menjalankan system call read() berulang kali.

Masing-masing pemanggilan read() membaca sejumlah byte (misalnya 4096 byte) dari file dan menyimpannya sementara di buffer memori.

Data yang terbaca merupakan isi sebenarnya dari file /etc/passwd, seperti:

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin


- Makna: kernel mengirimkan potongan isi file ke program cat, yang kemudian menampilkannya ke layar.

3. Proses Penulisan ke Layar (write)

Setelah data dibaca, program cat memanggil system call write() untuk menampilkan hasil bacaan ke terminal (stdout).

Kernel kemudian menulis data tersebut ke perangkat tampilan (biasanya /dev/tty atau terminal emulator).

- Makna: kernel mengatur agar data dari file ditampilkan ke pengguna melalui perangkat output.

4. Penutupan File (close)

Setelah semua isi file selesai dibaca dan ditampilkan, kernel memanggil system call close() untuk menutup file descriptor yang sebelumnya dibuka.

Ini melepaskan sumber daya yang digunakan oleh file tersebut agar bisa digunakan oleh proses lain.

- Makna: file ditutup dengan aman, dan kernel memastikan tidak ada kebocoran sumber daya.

  2).1. Isi Log Kernel

Pada gambar, dmesg menampilkan beberapa pesan seperti:

kvm_amd: Nested Paging enabled
kvm_amd: Hyper-V Direct TLB Flush enabled
systemd-journald: File ... corrupted or uncleanly shut down
WSL: ERROR: CheckConnection: getaddrinfo() failed
TCP: eth0: Driver has suspect GRO implementation
mini_init: drop_caches: 1


Pesan-pesan ini berasal dari kernel, bukan dari aplikasi pengguna. Log ini menunjukkan:

Aktivitas modul kernel seperti kvm_amd (virtualisasi AMD),

Pesan kesalahan sistem (getaddrinfo() failed, file journal corrupted),

Informasi tentang driver jaringan dan memori (drop_caches, eth0),

Proses inisialisasi sistem seperti systemd-journald.

- Artinya, log ini berisi peristiwa dan status sistem pada level kernel, bukan output hasil dari perintah aplikasi biasa.

2. Perbedaan dengan Output Program Biasa
Aspek	Log Kernel (dmesg)	Output Program Biasa (mis. ls, cat)
Sumber Output	Dari kernel space (inti sistem operasi)	Dari user space (program pengguna)
Isi Output	Pesan sistem, error driver, status perangkat keras	Hasil eksekusi program (daftar file, isi teks, dll.)
Tujuan	Digunakan untuk diagnostik dan debugging sistem	Digunakan untuk interaksi langsung dengan pengguna
Akses	Membutuhkan hak akses lebih tinggi (kadang root)	Dapat dijalankan oleh pengguna biasa
3. Makna dari Hasil Percobaan

Perintah dmesg memperlihatkan bahwa kernel:

Mencatat aktivitas internal sistem operasi (seperti inisialisasi driver dan error log).

Memberikan laporan status sistem yang tidak terlihat oleh program biasa.

Menunjukkan bahwa kernel bekerja di belakang layar mengatur seluruh perangkat dan proses di sistem.

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.
1.System call adalah penghubung antara program pengguna dan kernel yang memungkinkan program menjalankan fungsi sistem seperti membaca file atau membuat proses dengan aman.

2.Setiap system call menyebabkan perpindahan dari user mode ke kernel mode, agar operasi dilakukan di level sistem tanpa membahayakan stabilitas komputer.

3.Melalui perintah seperti strace dan dmesg, dapat diamati bagaimana sistem operasi menangani permintaan aplikasi, sehingga kita memahami cara kerja internal OS dalam mengatur sumber daya dan keamanan sistem.

---

## Quiz
1. Apa fungsi utama system call dalam sistem operasi?  
   **Jawaban:** Fungsi utama system call adalah sebagai antarmuka (interface) antara program aplikasi (user mode) dengan kernel sistem operasi (kernel mode).
System call memungkinkan program untuk meminta layanan dari kernel seperti membaca/menulis file, membuat proses baru, mengakses memori, atau berkomunikasi antarproses, tanpa harus mengakses perangkat keras secara langsung. 
2. Sebutkan 4 kategori system call yang umum digunakan.
   **Jawaban:**  Empat kategori utama system call adalah:

Kategori	Contoh	Fungsi
1. Process Control	fork(), exec(), wait(), exit()	Mengatur pembuatan dan eksekusi proses.
2. File Management	open(), read(), write(), close()	Mengakses dan memanipulasi file.
3. Device Management	ioctl(), read(), write()	Mengatur dan berinteraksi dengan perangkat I/O.
4. Communication	pipe(), socket(), send(), recv()	Mengatur komunikasi antarproses atau jaringan.

(Tambahan lain yang kadang disebut: Information Maintenance → getpid(), time(), dll.)
3. Mengapa system call tidak bisa dipanggil langsung oleh user program? 
   **Jawaban:**  System call tidak dapat dipanggil langsung karena:

Keamanan: Mencegah program pengguna mengakses atau mengubah data kernel dan perangkat keras secara langsung.

Stabilitas sistem: Akses langsung dapat menyebabkan crash, korupsi data, atau konflik antarproses.

Proteksi mode CPU: CPU memiliki dua mode — user mode dan kernel mode.

Program biasa hanya berjalan di user mode dengan izin terbatas.

System call dijalankan di kernel mode agar sistem tetap aman dan terkontrol.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  masih kebingungan dengan sistem oprasi
- Bagaimana cara Anda mengatasinya?  akan saya usahakan untuk belajar dan bisa memahami sistem operasi

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
