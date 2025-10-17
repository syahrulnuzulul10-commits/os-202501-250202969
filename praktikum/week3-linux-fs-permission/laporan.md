
# Laporan Praktikum Minggu 3
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori
- **NIM**   : 2502020969
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.

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
1. Apa fungsi dari perintah chmod?
 **Jawaban:**
chmod digunakan untuk mengubah hak akses (permission) pada file atau direktori di Linux. Dengan perintah ini, pengguna dapat menentukan siapa yang boleh membaca (r), menulis (w), atau mengeksekusi (x) file tersebut — baik untuk pemilik (owner), grup (group), maupun pengguna lain (others).

3. Apa arti dari kode permission rwxr-xr--?
 **Jawaban:**
Kode rwxr-xr-- menunjukkan hak akses sebagai berikut:

Owner: rwx → dapat membaca, menulis, dan mengeksekusi.

Group: r-x → dapat membaca dan mengeksekusi, tapi tidak dapat menulis.

Others: r-- → hanya dapat membaca.
Jadi, hanya pemilik file yang dapat mengedit file tersebut, sedangkan grup dan pengguna lain hanya bisa membacanya (grup bisa menjalankannya juga).
4. Jelaskan perbedaan antara chown dan chmod.
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
