
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

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?
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
