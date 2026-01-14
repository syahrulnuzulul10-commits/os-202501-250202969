
# Laporan Praktikum Minggu XII
Topik: Virtualisasi Menggunakan Virtual Machine

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori  
- **NIM**   : 250202969  
- **Kelas** : IKRA

---

## Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menginstal perangkat lunak virtualisasi (VirtualBox/VMware).  
2. Membuat dan menjalankan sistem operasi guest di dalam VM.  
3. Mengatur konfigurasi resource VM (CPU, RAM, storage).  
4. Menjelaskan mekanisme proteksi OS melalui virtualisasi.  
5. Menyusun laporan praktikum instalasi dan konfigurasi VM secara sistematis.
   
---

## Dasar Teori
1. Virtualisasi Sistem Operasi
Virtualisasi memungkinkan satu perangkat keras fisik menjalankan beberapa sistem operasi secara bersamaan melalui mesin virtual (Virtual Machine).

2. Host OS dan Guest OS
Host OS adalah sistem operasi utama yang berjalan langsung pada perangkat keras, sedangkan guest OS berjalan di lingkungan virtual yang terisolasi.

3. Hypervisor
Hypervisor merupakan perangkat lunak yang mengelola dan membagi resource perangkat keras kepada guest OS serta menjaga isolasi antar sistem.

4. Konfigurasi Resource Virtual
Resource seperti CPU, RAM, dan storage dapat diatur sesuai kebutuhan, dan penggunaannya dibatasi oleh hypervisor.

5. Isolasi dan Keamanan Sistem
Virtualisasi menyediakan isolasi antara host dan guest OS, sehingga meningkatkan keamanan dan stabilitas sistem.

---

## Langkah Praktikum
Ketentuan Teknis
- Virtualisasi dapat menggunakan **VirtualBox** atau **VMware**.  
- Sistem operasi guest bebas (Linux Ubuntu direkomendasikan).  
- Praktikum dapat dilakukan secara **kelompok kecil (2–3 orang)**.

Struktur folder (sesuaikan dengan template repo):
```
praktikum/week12-virtual-machine/
├─ code/
│  └─ catatan_konfigurasi.txt (opsional)
├─ screenshots/
│  ├─ instalasi_vm.png
│  ├─ konfigurasi_resource.png
│  └─ os_guest_running.png
└─ laporan.md
```
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
![Screenshot hasil](screenshots/example.png)

---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Quiz
1. [Pertanyaan 1]  
   **Jawaban:**  
2. [Pertanyaan 2]  
   **Jawaban:**  
3. [Pertanyaan 3]  
   **Jawaban:**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
