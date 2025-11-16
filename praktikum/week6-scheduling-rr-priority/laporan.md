
# Laporan Praktikum Minggu [X]
Topik: [Tuliskan judul topik, misalnya "Arsitektur Sistem Operasi dan Kernel"]

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori
- **NIM**   : 250202969
- **Kelas** : 1IKRA

---

## Tujuan
Tuliskan tujuan praktikum minggu ini.  
Contoh:  
1.Memahami cara kerja algoritma Round Robin dan Priority Scheduling dalam mengatur eksekusi proses pada CPU.

2.Menghitung waiting time dan turnaround time untuk setiap proses pada kedua algoritma.

3.Membandingkan performa kedua algoritma berdasarkan hasil perhitungan dan Gantt Chart.

4.Menganalisis pengaruh time quantum pada Round Robin dan pengaruh prioritas pada Priority Scheduling.

5.Meningkatkan pemahaman tentang manajemen proses pada sistem operasi, khususnya mekanisme antrian CPU agar eksekusi lebih efisien dan adil.

---

## Dasar Teori
1. Penjadwalan CPU (CPU Scheduling)

Penjadwalan CPU adalah mekanisme sistem operasi untuk menentukan proses mana yang akan dieksekusi CPU pada suatu waktu. Tujuannya untuk mengoptimalkan penggunaan CPU, meminimalkan waiting time, dan memberikan pengalaman sistem yang responsif.

Proses memiliki atribut:

Arrival Time (AT)

Burst Time (BT)

Priority (opsional)

Waiting Time (WT)

Turnaround Time (TAT)

Dengan rumus:

TAT = Finish Time – Arrival Time

WT = Turnaround Time – Burst Time

2. Round Robin (RR) Scheduling

Round Robin adalah algoritma penjadwalan preemptive yang membagikan waktu CPU secara merata menggunakan time quantum.

Cara kerja:

Proses disusun dalam antrian FIFO.

Setiap proses diberi jatah waktu (quantum) misalnya 2, 3, atau 5.

Jika waktu eksekusi belum selesai, proses dipindahkan ke belakang antrian.

Kelebihan:

Sangat adil untuk proses interaktif.

Tidak ada proses yang menunggu terlalu lama.

Kekurangan:

Terlalu banyak konteks switching jika quantum terlalu kecil.

3. Priority Scheduling

Algoritma yang mengeksekusi proses berdasarkan prioritas (angka kecil = prioritas tinggi).

Terdapat dua jenis:

Non-preemptive: proses berjalan sampai selesai.

Preemptive: proses dapat dihentikan jika ada proses lain dengan prioritas lebih tinggi datang.

Kelebihan:

Proses penting dapat dieksekusi lebih cepat.

Kekurangan:

Dapat menyebabkan starvation untuk proses prioritas rendah.

4. Perbandingan Kedua Algoritma
Algoritma	Karakteristik
RR	Adil, cocok untuk sistem time-sharing, preemptive, dipengaruhi quantum.
Priority	Efisien untuk proses penting, dapat menyebabkan starvation, urutan tergantung nilai prioritas.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
1. **Siapkan Data Proses**
   Gunakan contoh data berikut (boleh dimodifikasi sesuai kebutuhan):
   | Proses | Burst Time | Arrival Time | Priority |
   |:--:|:--:|:--:|:--:|
   | P1 | 5 | 0 | 2 |
   | P2 | 3 | 1 | 1 |
   | P3 | 8 | 2 | 4 |
   | P4 | 6 | 3 | 3 |

2. **Eksperimen 1 – Round Robin (RR)**
   - Gunakan *time quantum (q)* = 3.  
   - Hitung *waiting time* dan *turnaround time* untuk tiap proses.  

   | Proses |   CT   | Arivaal| TAT(ct-at) |	WT(TAT-bt) |
   | :----: | :----: | :----: | :--------: | :--------: |
   |   P1   |	 14   |    0   |	14-0=14   |	14-5=9     |
   |   P2   |   6 	|    1	|  6-1=5	    | 5-3=2      |
   |   P3	|   22   |	  2   |	22-2=20   |	20-8=12    |
   |   P4	|   20   |    3	|  20-3=17   |	17-6=11    |
Rata rata TAT:14
Rata rata WT :8,5

   - Simulasikan eksekusi menggunakan Gantt Chart (manual atau spreadsheet).  
     ```
     | P1 | P2 | P3 | P4 | P1 | P3 | P4 | P3 |
     0    3    6    9   12   14   17   20   22
     ```
   - Catat sisa *burst time* tiap putaran.
   
   | waktu | Brust | sisa waktu|
   |:-----:|:-----:|:---------:|
   | 0-3   | 5-3=0 | P1 sisa 2 |
   | 3-6   | 3-3=0 | 2 selesai |
   | 6-9   | 8-3=5 | P3 sisa 5 |
   | 9-12  | 6-3=3 | P4 sisa 3 |
   | 12-14 | 2 < 3 | P1 selesai|
   | 14-17 | 5-3=0 | P3 sisa 2 |
   | 17-20 | 3-3=0 | P4 selesai|
   | 20-22 | 2 < 3 | P3 selesai|
   

3. **Eksperimen 2 – Priority Scheduling (Non-Preemptive)**
   - Urutkan proses berdasarkan nilai prioritas (angka kecil = prioritas tinggi).  
   - Lakukan perhitungan manual untuk:
     ```
     WT[i] = waktu mulai eksekusi - Arrival[i]
     TAT[i] = WT[i] + Burst[i]o
     ```
   - Buat tabel perbandingan hasil RR dan Priority.

|Proses|	BT | AT |PRIO|	ST |	WT(ST-AT)	|TAT(WT+BT)|
|:----:|:--:|:--:|:--:|:--:|:------------:|:--------:|
|  P1  |	 5 | 0  |  2 |	0  |	   0        | 	  5     |
|  P2  |	 3 | 1  |  1 |	5  | 	   4        |	  7     |
|  P4  |	 6 | 3  |  3 |	8  |	   5        |	  11    |
|  P3  |	 8 | 2  |  4 |	14 |     12       |    20    |

Rata rata WT  :5,25
Rata rata TAT :10,75

4. **Eksperimen 3 – Analisis Variasi Time Quantum (Opsional)**
   - Ubah *quantum* menjadi 2 dan 5.  
   - Amati perubahan nilai rata-rata *waiting time* dan *turnaround time*.  

Quantum 2
|Proses|	CT | AT |BT | TAT | WT |
|:----:|:--:|:--:|:-:|:---:|:--:|
|  P1  |	18 |  0 | 5 |	18 |  13|
|  P2  |	13 |	1 | 3 |	12 |	9 |
|  P3  |	24 |	2 | 8 |	22 |	14|
|  P4  |	22 |  3 | 6 |	19 |	13|
|Rata-rata  |    |   ||17.75|12.25|

Quantum 5
|Proses|	CT | AT |BT | TAT | WT |
|:----:|:--:|:--:|:-:|:---:|:--:|
|  P1  |	5  |  0 | 5 |	5  |  0 |
|  P2  |	8  |	1 | 3 |	7  |	4 |
|  P3  |	21 |	2 | 8 |	19 |	11|
|  P4  |	22 |  3 | 6 |	19 |	13|
|Rata-rata  |    |  || 12.5|  7 |




   - Buat tabel perbandingan efek *quantum*.

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua hasil tabel dan screenshot ke:
     ```
     praktikum/week6-scheduling-rr-priority/screenshots/
     ```
   - Buat tabel perbandingan seperti berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | RR | 8,5 | 14 | Adil terhadap semua proses | Tidak efisien jika quantum tidak tepat |
     | Priority | 5,25 | 10,75 | Efisien untuk proses penting | Potensi *starvation* pada prioritas rendah |

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 6 - CPU Scheduling RR & Priority"
   git push origin main
   ```


---


---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
1.Algoritma Round Robin (RR) menunjukkan bahwa pembagian waktu berbasis time quantum membuat setiap proses mendapatkan kesempatan eksekusi secara merata. Namun, performa sangat bergantung pada besar kecilnya quantum. Quantum terlalu kecil menyebabkan banyak context switching sehingga sistem kurang efisien, sedangkan quantum terlalu besar membuat RR hampir menyerupai FCFS.

2.Algoritma Priority Scheduling mengeksekusi proses berdasarkan tingkat prioritas. Proses dengan prioritas tinggi selesai lebih cepat, sehingga sangat cocok untuk sistem yang membutuhkan penanganan proses penting secara segera. Namun, algoritma ini memiliki risiko starvation, yaitu proses prioritas rendah dapat menunggu terlalu lama jika proses prioritas tinggi terus berdatangan.

3.Berdasarkan perhitungan WT dan TAT, RR cenderung memberikan fairness, sedangkan Priority unggul pada respons cepat untuk proses penting. Nilai rata-rata WT dan TAT berbeda karena kedua algoritma memiliki tujuan berbeda—RR fokus pada keadilan, Priority fokus pada urgensi.

4.Dari hasil eksperimen, terlihat bahwa pemilihan algoritma penjadwalan harus disesuaikan dengan kebutuhan sistem. Jika membutuhkan keadilan → RR, sedangkan jika membutuhkan prioritas tinggi → Priority.

---

## Kesimpulan
1.Round Robin memberikan pembagian waktu CPU yang lebih merata dan cocok untuk sistem interaktif, tetapi performanya sangat dipengaruhi oleh besar kecilnya time quantum.

2.Priority Scheduling mampu memprioritaskan proses tertentu sehingga lebih efisien untuk kebutuhan real-time, tetapi dapat menimbulkan starvation pada proses prioritas rendah.

3.Hasil perhitungan menunjukkan bahwa setiap algoritma memiliki kelebihan dan kekurangan, sehingga tidak ada satu algoritma yang paling baik untuk semua situasi.

---

## Quiz
1. Apa perbedaan utama antara Round Robin dan Priority Scheduling?

Round Robin: menggunakan time quantum dan memberikan jatah waktu yang sama kepada semua proses → adil, preemptive.

Priority Scheduling: memilih proses berdasarkan prioritas (angka lebih kecil = lebih penting) → tidak selalu adil, risiko starvation.

2. Apa pengaruh besar/kecilnya time quantum terhadap performa sistem?

Quantum kecil: proses sering diputus (preemption tinggi), context switching banyak, CPU menjadi kurang efisien.

Quantum besar: mirip FCFS, proses lama bisa mendominasi CPU, fairness berkurang.

Waktu yang optimal harus menyeimbangkan efisiensi dan respons sistem.

3. Mengapa algoritma Priority dapat menyebabkan starvation?

Karena proses dengan prioritas rendah dapat terus tertunda jika selalu ada proses baru dengan prioritas lebih tinggi yang masuk ke sistem. Akibatnya, proses prioritas rendah mungkin tidak pernah mendapatkan giliran eksekusi.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
