
# Laporan Praktikum Minggu 5
Topik:  Penjadwalan CPU (FCFS dan SJF)

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori
- **NIM**   : 250202969 
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
1.CPU Scheduling adalah mekanisme sistem operasi untuk menentukan urutan eksekusi proses.

2.FCFS mengeksekusi proses berdasarkan kedatangan paling awal.

3.SJF memilih proses dengan burst time paling pendek terlebih dahulu.

4.Waiting Time (WT) adalah waktu proses menunggu sebelum dieksekusi.

5.Turnaround Time (TAT) adalah total waktu dari proses tiba hingga selesai.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
1. **Siapkan Data Proses**
   Gunakan tabel proses berikut sebagai contoh (boleh dimodifikasi dengan data baru):
   | Proses | Burst Time | Arrival Time |
   |:--:|:--:|:--:|
   | P1 | 6 | 0 |
   | P2 | 8 | 1 |
   | P3 | 7 | 2 |
   | P4 | 3 | 3 |

2. **Eksperimen 1 – FCFS (First Come First Served)**
   - Urutkan proses berdasarkan *Arrival Time*.  
   - Hitung nilai berikut untuk tiap proses:
     ```
     Waiting Time (WT) = waktu mulai eksekusi - Arrival Time
     Turnaround Time (TAT) = WT + Burst Time
     ```
   - Hitung rata-rata Waiting Time dan Turnaround Time.  
   - Buat Gantt Chart sederhana:  
     ```
     | P1 | P2 | P3 | P4 |
     0    6    14   21   24
     ```

| Proses | Burst Time | Arrival Time | Star Time | Finis Time |WT | TAT|
   |:--:|:--:|:--:|:--:|:--:|:--:|:--:|
   | P1 | 6 | 0 | 0 | 6 | 0 | 6 |
   | P2 | 8 | 1 | 6 | 14 | 5 | 13 |
   | P3 | 7 | 2 | 14 | 21 | 12 | 19 |
   | P4 | 3 | 3 | 21 | 24 | 18 | 21 |

   rata-rata Waiting Time (WT) = 8,75

   rata-rata Turnaround Time (TAT) = 14,75

   Gantt Chart:

    | P1 | P2 | P3 | P4 |
     0    6    14   21   24

3. **Eksperimen 2 – SJF (Shortest Job First)**
   - Urutkan proses berdasarkan *Burst Time* terpendek (dengan memperhatikan waktu kedatangan).  
   - Lakukan perhitungan WT dan TAT seperti langkah sebelumnya.  

| Proses | Burst Time | Arrival Time | Star Time | Finis Time |WT | TAT|
   |:--:|:--:|:--:|:--:|:--:|:--:|:--:|
   | P4 | 3 | 3 | 3 | 6 | 0 | 3 |
   | P1 | 6 | 0 | 6  | 12  | 6  |  12 |
   | P3 | 7 | 2 | 12 | 19 | 10 | 17 |
   | P2 | 8 | 1 | 19  | 27 | 18  | 26 |
   
   rata-rata Waiting Time (WT) = 8,5
   rata-rata Turnaround Time (TAT) = 14,5

Gantt Chart:

    | P1 | P2 | P3 | P4 |
     0    6    12   19   27

   - Bandingkan hasil FCFS dan SJF pada tabel berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | FCFS | 8,75 | 14,75 | Sederhana dan mudah diterapkan | Tidak efisien untuk proses panjang |
     | SJF | 8,5 | 14,5 | Optimal untuk job pendek | Menyebabkan *starvation* pada job panjang |



4. **Eksperimen 3 – Visualisasi Spreadsheet (Opsional)**
   - Gunakan Excel/Google Sheets untuk membuat perhitungan otomatis:
     - Kolom: Arrival, Burst, Start, Waiting, Turnaround, Finish.
     - Gunakan formula dasar penjumlahan/subtraksi.
   - Screenshot hasil perhitungan dan simpan di:
     ```
     praktikum/week5-scheduling-fcfs-sjf/screenshots/
     ```

5. **Analisis**
1.SJF lebih unggul karena menghasilkan WT dan TAT lebih rendah.

2.FCFS cocok untuk sistem sederhana tetapi tidak ideal bila banyak proses panjang.

3.SJF sangat efisien tetapi rawan membuat proses panjang menunggu terlalu lama.

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 5 - CPU Scheduling FCFS & SJF"
   git push origin main
   ```

---

## Hasil Eksekusi


---

## Analisis
- Bandingkan hasil rata-rata WT dan TAT antara FCFS & SJF.  
- Jelaskan kondisi kapan SJF lebih unggul dari FCFS dan sebaliknya.  
- Tambahkan kesimpulan singkat di akhir laporan. 

---

## Kesimpulan
- SJF memberikan performa yang lebih baik dibanding FCFS pada data ini.

- FCFS hanya cocok untuk sistem yang tidak membutuhkan efisiensi tinggi.

- Burst time mempengaruhi besar kecilnya waiting time dan turnaround time.

---

## D. Tugas & Quiz
### Tugas
1. Hitung *waiting time* dan *turnaround time* dari minimal 2 skenario FCFS dan SJF.  
2. Sajikan hasil perhitungan dalam tabel perbandingan (FCFS vs SJF).  
3. Analisis kelebihan dan kelemahan tiap algoritma.  
4. Simpan seluruh hasil dan analisis ke `laporan.md`.  

**JAWABAN**

1. 
2. <img width="1499" height="642" alt="Cuplikan layar 2025-11-12 185547" src="https://github.com/user-attachments/assets/14f65dc6-9e92-4d81-a759-20fb5b85b5f8" />

3. 
   
(1.) FCFS (First Come First Served)

Kelebihan:

- Sederhana dan mudah diimplementasikan.
- Adil dalam urutan kedatangan (tidak ada proses yang dilewati).
- Cocok untuk sistem batch (pekerjaan datang berurutan).

Kelemahan:

- Dapat menyebabkan waktu tunggu lama untuk proses pendek yang datang setelah proses panjang (convoy effect).
- Tidak efisien untuk sistem interaktif.
- Tidak mempertimbangkan prioritas atau waktu eksekusi proses.
 
 (2.) SJF (Shortest Job First)

Kelebihan:

- Memberikan rata-rata waktu tunggu dan waktu tinggal paling rendah.
- Efisien untuk sistem dengan banyak proses pendek.
- Mengoptimalkan pemanfaatan CPU.

Kelemahan:

- Sulit diterapkan karena lama burst time harus diketahui terlebih dahulu.
- Dapat menyebabkan starvation untuk proses yang panjang.
- Tidak cocok untuk sistem waktu nyata (real-time) yang memerlukan respon cepat untuk semua proses.



### Quiz
Tuliskan jawaban di bagian **Quiz** pada laporan:
1. Apa perbedaan utama antara FCFS dan SJF?  
2. Mengapa SJF dapat menghasilkan rata-rata waktu tunggu minimum?  
3. Apa kelemahan SJF jika diterapkan pada sistem interaktif?  

**jawaban**

1.Perbedaan FCFS dan SJF: FCFS berdasarkan kedatangan pertama, SJF berdasarkan burst time terpendek.

2.Mengapa SJF menghasilkan waktu tunggu minimum? Karena selalu mengeksekusi proses paling cepat terlebih dahulu.

3.Kelemahan SJF di sistem interaktif: Proses panjang dapat mengalami starvation.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
