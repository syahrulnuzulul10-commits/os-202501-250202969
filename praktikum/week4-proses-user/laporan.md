
# Laporan Praktikum Minggu [X]
Topik:Manajemen Proses dan User di Linux

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori 
- **NIM**   : 250202969
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menjelaskan konsep proses dan user dalam sistem operasi Linux.  
2. Menampilkan daftar proses yang sedang berjalan dan statusnya.  
3. Menggunakan perintah untuk membuat dan mengelola user.  
4. Menghentikan atau mengontrol proses tertentu menggunakan PID.  
5. Menjelaskan kaitan antara manajemen user dan keamanan sistem.  
---

## Dasar Teori
- User adalah identitas individu yang menggunakan sistem. Setiap user memiliki UID (User ID) sebagai nomor identitas unik.

- Group digunakan untuk mengelompokkan beberapa user agar bisa berbagi izin akses terhadap file atau direktori yang sama.

- Sistem izin di Linux terbagi menjadi tiga kategori: user (pemilik), group (kelompok), dan others (lainnya).

- Hak akses diatur menggunakan mode read (r), write (w), dan execute (x).
  Pengaturan ini menjadi dasar keamanan agar tidak semua pengguna dapat mengubah file atau menjalankan program sembarangan.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).  
   - Pastikan Anda sudah login sebagai user non-root.  
   - Siapkan folder kerja:
     ```
     praktikum/week4-proses-user/
     ```

2. **Eksperimen 1 – Identitas User**
   Jalankan perintah berikut:
   ```bash
   whoami
   id
   groups
   ```
   - Jelaskan setiap output dan fungsinya.  
   - Buat user baru (jika memiliki izin sudo):
     ```bash
     sudo adduser praktikan
     sudo passwd praktikan
     ```
   - Uji login ke user baru.

3. **Eksperimen 2 – Monitoring Proses**
   Jalankan:
   ```bash
   ps aux | head -10
   top -n 1
   ```
   - Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND.  
   - Simpan tangkapan layar `top` ke:
     ```
     praktikum/week4-proses-user/screenshots/top.png
     ```

4. **Eksperimen 3 – Kontrol Proses**
   - Jalankan program latar belakang:
     ```bash
     sleep 1000 &
     ps aux | grep sleep
     ```
   - Catat PID proses `sleep`.  
   - Hentikan proses:
     ```bash
     kill <PID>
     ```
   - Pastikan proses telah berhenti dengan `ps aux | grep sleep`.

5. **Eksperimen 4 – Analisis Hierarki Proses**
   Jalankan:
   ```bash
   pstree -p | head -20
   ```
   - Amati hierarki proses dan identifikasi proses induk (`init`/`systemd`).  
   - Catat hasilnya dalam laporan.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 4 - Manajemen Proses & User"
   git push origin main
   ```

---

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
<img width="1376" height="715" alt="Cuplikan layar 2025-10-29 104707" src="https://github.com/user-attachments/assets/1ca03b90-1c40-425b-a901-f6af834f8456" />
<img width="1460" height="733" alt="Cuplikan layar 2025-10-29 104739" src="https://github.com/user-attachments/assets/c938b5f7-85c3-4059-a328-05edb1aeac5a" />
<img width="1269" height="705" alt="Cuplikan layar 2025-10-29 105048" src="https://github.com/user-attachments/assets/6a0f5b59-2a76-4251-ab63-a50848f38fa1" />
<img width="1444" height="693" alt="Cuplikan layar 2025-10-29 105104" src="https://github.com/user-attachments/assets/d10f7f97-20e7-4024-930e-b167ceb8c3f3" />

---

## Analisis
1. eksperimen 2: Jelaskan setiap output dan fungsinya (whoami, id, groups)
2. eksperimen 3: Jelaskan kolom penting seperti PID, USER, %CPU, %MEM, COMMAND
3. eksperimen 4: Catat PID proses sleep
4. eksperimen 5: Amati hierarki proses dan identifikasi proses induk (init/systemd)

  **jawaban**
- Eksperimen 2 — Perintah Dasar User (whoami, id, groups)
  Perintah dan Output:


whoami
Output contoh:
syahrul

Fungsi & Penjelasan:


Menampilkan nama user yang sedang login atau aktif di terminal.


Berguna untuk memastikan identitas pengguna saat mengelola hak akses.


Contoh: jika hasilnya root, berarti kamu sedang memiliki hak administrator.




id
Output contoh:
uid=1000(syahrul) gid=1000(syahrul) groups=1000(syahrul),27(sudo)

Fungsi & Penjelasan:


Menampilkan UID (User ID), GID (Group ID), dan daftar grup yang dimiliki user.


uid=1000 → Nomor identitas unik pengguna.


gid=1000 → Nomor grup utama user.


groups=... → Grup tambahan yang diikuti (contohnya sudo berarti user bisa menjalankan perintah superuser).




groups
Output contoh:
syahrul : syahrul sudo

Fungsi & Penjelasan:


Menampilkan nama-nama grup yang user tergabung di dalamnya.


Berguna untuk menentukan hak akses ke file/direktori, karena Linux mengatur izin berdasarkan user, group, dan others.



Kesimpulan Eksperimen 2:
Ketiga perintah ini membantu mengenali identitas dan hak akses pengguna dalam sistem Linux, yang penting sebelum menjalankan perintah administratif atau manajemen proses.

- Eksperimen 3 — Melihat Daftar Proses (ps/top)
Perintah umum:
ps aux

atau
top

- Kolom Penting dan Artinya:
KolomArtiKeteranganUSERPemilik prosesMenunjukkan siapa yang menjalankan proses (root atau user biasa).PIDProcess IDNomor unik proses, digunakan untuk mengontrol (kill, trace, dll).%CPUPersentase penggunaan CPUMenunjukkan seberapa besar beban CPU dari proses tersebut.%MEMPersentase penggunaan memoriMenunjukkan banyaknya RAM yang digunakan proses.COMMANDNama perintah yang dijalankanMenunjukkan program atau perintah yang sedang berjalan.
- Kesimpulan Eksperimen 3:
Perintah ps dan top digunakan untuk memantau proses aktif di sistem. Kolom-kolom ini membantu mengidentifikasi proses yang menghabiskan sumber daya paling besar dan siapa pemiliknya.

- Eksperimen 4 — Menjalankan Proses Sleep dan Mencatat PID
  Perintah:
sleep 1000 &

 Penjelasan:


Simbol & artinya menjalankan perintah di background (tidak menghalangi terminal).


Terminal akan menampilkan PID dari proses sleep.


Contoh output:
[1] 2456

Artinya:


[1] adalah nomor job (urutan background job di shell).


2456 adalah PID (Process ID) dari proses sleep.


Jika kamu jalankan:
ps aux | grep sleep

akan terlihat baris seperti:
syahrul   2456  0.0  0.0   2572   600 pts/0    S    12:30   0:00 sleep 1000

- Kesimpulan Eksperimen 4:
PID proses sleep adalah 2456 (contoh), dan ini bisa digunakan untuk memeriksa atau menghentikan proses (misal kill 2456). Eksperimen ini menunjukkan bagaimana sistem memberi nomor unik untuk setiap proses.

- Eksperimen 5 — Melihat Hierarki Proses (pstree)
  Perintah:
pstree -p

Penjelasan:


Menampilkan struktur pohon proses dari sistem operasi.


Setiap proses ditampilkan dengan nama dan PID-nya.


Contoh potongan output:
systemd(1)─┬─NetworkManager(567)
            ├─sshd(876)
            ├─gnome-terminal-(2000)─┬─bash(2050)───sleep(2456)
            └─cron(650)

 Interpretasi:


systemd(1) → proses induk pertama yang dijalankan oleh kernel saat boot (PID 1).


Semua proses lain (termasuk sleep) adalah anak (child) dari proses lain (mis. bash).


Jalur systemd → gnome-terminal → bash → sleep menunjukkan urutan hierarki proses.


- Kesimpulan Eksperimen 5:
Proses induk tertinggi adalah init atau systemd (PID 1). Semua proses lain merupakan turunannya. Ini menunjukkan bagaimana Linux membentuk hubungan induk-anak antarproses untuk mengatur eksekusi dan pengelolaan sumber daya.

- Rangkuman Singkat
EksperimenFokusKesimpulan Utama2Perintah userMengetahui identitas dan hak akses user aktif3Monitoring prosesMemahami kolom penting pada daftar proses4PID proses sleepMengetahui cara kerja proses background dan PID5Hierarki prosesMengetahui hubungan induk-anak antar proses, dengan systemd sebagai induk utama


---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

# D. Tugas & Quiz
---
### Tugas
1. Dokumentasikan hasil semua perintah dan jelaskan fungsi tiap perintah.
   
|  No | Perintah                                                                    | Contoh Output                                                                                                  | Fungsi / Penjelasan                                                        |                                                               |
| :-: | :-------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------- | ------------------------------------------------------------- |
|  1  | `whoami`                                                                    | `syahrul`                                                                                                      | Menampilkan nama pengguna (user) yang sedang aktif di terminal.            |                                                               |
|  2  | `id`                                                                        | `uid=1000(syahrul) gid=1000(syahrul) groups=1000(syahrul),27(sudo)`                                            | Menampilkan **UID**, **GID**, dan daftar **grup** yang dimiliki user.      |                                                               |
|  3  | `groups`                                                                    | `syahrul : syahrul sudo`                                                                                       | Menampilkan daftar grup yang diikuti oleh user saat ini.                   |                                                               |
|  4  | `ps aux`                                                                    | Menampilkan daftar semua proses di sistem dengan kolom **USER**, **PID**, **%CPU**, **%MEM**, dan **COMMAND**. | Digunakan untuk melihat proses aktif dan penggunaan sumber daya.           |                                                               |
|  5  | `top`                                                                       | Tampilan dinamis daftar proses dan penggunaan CPU/memori.                                                      | Digunakan untuk memantau performa sistem secara real-time.                 |                                                               |
|  6  | `sleep 1000 &`                                                              | `[1] 2456`                                                                                                     | Menjalankan proses `sleep` di background dan menampilkan PID (Process ID). |                                                               |
|  7  | `ps aux                                                                     | grep sleep`                                                                                                    | `syahrul 2456 0.0 0.0 2572 600 pts/0 S 12:30 0:00 sleep 1000`              | Menampilkan proses `sleep` dan PID-nya untuk dicek statusnya. |
|  8  | `kill 2456`                                                                 | (tidak ada output, proses berhenti)                                                                            | Mengirim sinyal `SIGTERM` untuk menghentikan proses dengan PID tertentu.   |                                                               |
|  9  | `pstree -p`                                                                 | Menampilkan hierarki proses dengan PID.                                                                        | Digunakan untuk melihat hubungan induk–anak antar proses di sistem.        |                                                               |
|  10 | `git add .`<br>`git commit -m "laporan minggu 4"`<br>`git push origin main` | (Pesan konfirmasi commit/push)                                                                                 | Menyimpan dan mengunggah laporan ke repositori Git.                        |                                                               |

2. Gambarkan hierarki proses dalam bentuk diagram pohon (`pstree`) di laporan.

<img width="1201" height="520" alt="diagram pohon" src="https://github.com/user-attachments/assets/102c6c00-5af4-4ede-a413-89c577e88dee" />

3. Jelaskan hubungan antara user management dan keamanan sistem Linux.
-User management adalah lapisan keamanan pertama dalam sistem Linux yang mengatur siapa boleh melakukan apa, menjaga integritas dan kestabilan sistem.
4. Upload laporan ke repositori Git tepat waktu.
## Quiz
1.Apa fungsi dari proses init atau systemd dalam sistem Linux?
-init atau systemd adalah proses pertama (PID 1) yang dijalankan oleh kernel saat sistem booting.
-Tugasnya adalah menginisialisasi sistem, menjalankan service (daemon), serta menjadi induk bagi semua proses lain.
-Jika systemd mati, maka seluruh sistem juga akan berhenti.
2.Apa perbedaan antara `kill` dan `killall`?
- kill menargetkan proses tertentu berdasarkan PID.
- killall menargetkan semua proses berdasarkan nama program.
3.Mengapa user `root` memiliki hak istimewa di sistem Linux?
- User root memiliki hak istimewa karena berperan sebagai superuser yang memiliki kendali penuh terhadap sistem Linux.
  
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
