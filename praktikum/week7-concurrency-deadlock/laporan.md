
# Laporan Praktikum Minggu [X]
Topik: Sinkronisasi Proses dan Masalah Deadlock

---

## Identitas
- **Nama**  : Syahrul Nuzulul Qori
- **NIM**   : 250202969  
- **Kelas** : 1IKRA

---

## Tujuan
>>Mengidentifikasi empat kondisi penyebab deadlock
Mahasiswa mampu mengenali dan menjelaskan empat kondisi dasar yang menyebabkan deadlock terjadi, yaitu:

Mutual Exclusion

Hold and Wait

No Preemption

Circular Wait

>>Menjelaskan mekanisme sinkronisasi menggunakan semaphore atau monitor
Mahasiswa memahami bagaimana semaphore dan monitor digunakan untuk mengontrol akses ke sumber daya bersama sehingga deadlock dapat dicegah.

>>Menganalisis dan memberikan solusi untuk kasus deadlock
Mahasiswa dapat menganalisis penyebab deadlock pada suatu program dan merancang solusi sinkronisasi yang efektif untuk menghilangkan atau mencegah deadlock.

>>Berkolaborasi dalam tim untuk menyusun laporan analisis
Mahasiswa bekerja sama dalam kelompok untuk melakukan eksperimen, berdiskusi, dan menyusun laporan hasil analisis secara komprehensif.

>>Menyajikan hasil studi kasus secara sistematis
Mahasiswa mampu menyusun hasil eksperimen dalam bentuk laporan yang runtut, jelas, dan sesuai kaidah penyusunan laporan ilmiah.

---

## Dasar Teori

1.Sinkronisasi Proses
Proses yang berjalan secara bersamaan (concurrent) harus disinkronkan agar tidak saling mengganggu saat mengakses sumber daya bersama. Tanpa sinkronisasi, dapat terjadi race condition dan deadlock.

2.Deadlock dan Empat Kondisinya
Deadlock adalah kondisi di mana proses saling menunggu tanpa akhir. Deadlock hanya terjadi jika empat kondisi tercapai secara bersamaan:

Mutual Exclusion

Hold and Wait

No Preemption

Circular Wait

3.Semaphore sebagai Mekanisme Sinkronisasi
Semaphore digunakan untuk mengatur jumlah proses yang dapat mengakses sumber daya. Dengan operasi wait() dan signal(), semaphore mencegah proses masuk critical section bersamaan dan dapat digunakan untuk mencegah deadlock.

4.Dining Philosophers Problem sebagai Model Deadlock
Masalah ini menggambarkan bagaimana proses (filosof) dapat saling menunggu sumber daya (garpu) hingga terjadi deadlock. Ini digunakan sebagai studi kasus utama untuk memahami konflik akses sumber daya.

5.Pencegahan Deadlock dengan Aturan Akses
Deadlock dapat dihindari dengan mengubah pola akses sumber daya, misalnya dengan membatasi jumlah proses yang boleh mengakses (semaphore), atau mengubah urutan pengambilan sumber daya sehingga circular wait tidak terbentuk.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
1. **Persiapan Tim**
   - Bentuk kelompok beranggotakan 3–4 orang.  
   - Tentukan ketua dan pembagian tugas (analisis, implementasi, dokumentasi).

2. **Eksperimen 1 – Simulasi Dining Philosophers (Deadlock Version)**
   - Implementasikan versi sederhana dari masalah *Dining Philosophers* tanpa mekanisme pencegahan deadlock.  
   - Contoh pseudocode:
     ```text
     while true:
       think()
       pick_left_fork()
       pick_right_fork()
       eat()
       put_left_fork()
       put_right_fork()
     ```
   - Jalankan simulasi atau analisis alur (boleh menggunakan pseudocode atau diagram alur).  
   - Identifikasi kapan dan mengapa deadlock terjadi.

3. **Eksperimen 2 – Versi Fixed (Menggunakan Semaphore / Monitor)**
   - Modifikasi pseudocode agar deadlock tidak terjadi, misalnya:
     - Menggunakan *semaphore (mutex)* untuk mengontrol akses.
     - Membatasi jumlah filosof yang dapat makan bersamaan (max 4).  
     - Mengatur urutan pengambilan garpu (misal, filosof terakhir mengambil secara terbalik).  
   - Analisis hasil modifikasi dan buktikan bahwa deadlock telah dihindari.

4. **Eksperimen 3 – Analisis Deadlock**
   - Jelaskan empat kondisi deadlock dari versi pertama dan bagaimana kondisi tersebut dipecahkan pada versi fixed.  
   - Sajikan hasil analisis dalam tabel seperti contoh berikut:

     | Kondisi Deadlock | Terjadi di Versi Deadlock | Solusi di Versi Fixed |
     |------------------|---------------------------|------------------------|
     | Mutual Exclusion | Ya (satu garpu hanya satu proses) | Gunakan semaphore untuk kontrol akses |
     | Hold and Wait | Ya | Hindari proses menahan lebih dari satu sumber daya |
     | No Preemption | Ya | Tidak ada mekanisme pelepasan paksa |
     | Circular Wait | Ya | Ubah urutan pengambilan sumber daya |

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua diagram, screenshot simulasi, dan hasil diskusi di:
     ```
     praktikum/week7-concurrency-deadlock/screenshots/
     ```
   - Tuliskan laporan kelompok di `laporan.md` (format IMRaD singkat: *Pendahuluan, Metode, Hasil, Analisis, Diskusi*).

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 7 - Sinkronisasi Proses & Deadlock"
   git push origin main
   ```
---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
<img width="1898" height="1066" alt="Cuplikan layar 2025-11-26 183127" src="https://github.com/user-attachments/assets/436c6261-4aae-48e0-b52a-c74c722e90e7" />

<img width="1916" height="1078" alt="Cuplikan layar 2025-11-26 183207" src="https://github.com/user-attachments/assets/44237098-211b-4cb3-82f3-b8babb9f1671" />


---

## Eksperimen 1

Simulasi Dining Philosophers (Deadlock Version)
```
import threading
import time

# Buat 5 garpu (fork) sebagai resource
forks = [threading.Lock() for _ in range(5)]

def philosopher(i):
    left = forks[i]
    right = forks[(i + 1) % 5]

    while True:
        print(f"Philosopher {i} sedang berpikir...")
        time.sleep(1)

        left.acquire()     # Ambil garpu kiri
        print(f"Philosopher {i} mengambil garpu KIRI")

        right.acquire()    # Ambil garpu kanan → bisa menyebabkan deadlock
        print(f"Philosopher {i} mengambil garpu KANAN")

        print(f"Philosopher {i} mulai makan...")
        time.sleep(1)

        left.release()
        right.release()

for i in range(5):
    t = threading.Thread(target=philosopher, args=(i,))
    t.start()

```


## Eksperimen 2
Versi Fixed (Menggunakan Semaphore / Monitor)
FIXED VERSION — Semaphore (Mutex Global)
```
import threading
import time

forks = [threading.Lock() for _ in range(5)]

# Batasi hanya 4 filosof yang boleh mencoba makan
room = threading.Semaphore(4)

def philosopher(i):
    left = forks[i]
    right = forks[(i + 1) % 5]

    while True:
        print(f"Philosopher {i} sedang berpikir...")
        time.sleep(1)

        room.acquire()   # masuk ke ruang makan, max 4 orang

        left.acquire()
        right.acquire()

        print(f"Philosopher {i} mulai makan...")
        time.sleep(1)

        left.release()
        right.release()
        room.release()   # keluar dari ruang makan

for i in range(5):
    t = threading.Thread(target=philosopher, args=(i,))
    t.start()

```

## Eksperimen 3

| **Kondisi Deadlock** | **Terjadi pada Versi Deadlock**                         | **Solusi pada Versi Fixed**                                          |
| -------------------- | ------------------------------------------------------- | -------------------------------------------------------------------- |
| **Mutual Exclusion** | Ya, setiap garpu hanya dapat digunakan satu filosof     | Tetap terjadi (normal), tidak perlu dihilangkan                      |
| **Hold and Wait**    | Ya, filosof memegang 1 garpu dan menunggu garpu lainnya | Dihilangkan dengan semaphore / aturan pembatasan                     |
| **No Preemption**    | Ya, garpu tidak bisa direbut paksa                      | Ada mekanisme pelepasan (semaphore), sumber daya dilepas kembali     |
| **Circular Wait**    | Ya, semua filosof saling menunggu melingkar             | Dihilangkan dengan membatasi 4 filosof / mengubah urutan ambil garpu |

---

## Analisis
>>Eksperimen 1 – Versi Deadlock (Tanpa Mekanisme Sinkronisasi)
Tujuan

Mengamati bagaimana deadlock bisa terjadi ketika beberapa proses mengakses sumber daya bersama tanpa aturan.

Hasil

Setiap filosof mengambil garpu kiri terlebih dahulu.

Setelah itu setiap filosof mencoba mengambil garpu kanan, tetapi garpu kanan mereka sedang dipegang filosofi di sebelahnya.

Semua filosof menunggu selamanya → program macet.

Tidak ada output lanjutan setelah mencoba mengambil garpu kanan.

Analisis

Deadlock terjadi karena seluruh kondisi deadlock terpenuhi:

Mutual Exclusion – Garpu hanya bisa dipegang satu filosof.

Hold and Wait – Filosof memegang 1 garpu dan menunggu garpu lain.

No Preemption – Garpu tidak bisa dipaksa untuk dilepaskan.

Circular Wait – Filosof 0 menunggu 1, 1 menunggu 2, … 4 menunggu 0.

Kesimpulan Eksperimen 1

Deadlock benar-benar terjadi pada sistem tanpa sinkronisasi, sehingga semua thread/jalur eksekusi berhenti.

>>Eksperimen 2 – Versi Fixed (Menggunakan Semaphore)
Tujuan

Memperbaiki deadlock menggunakan mekanisme sinkronisasi agar proses berjalan lancar.

Hasil

Filosof dapat makan secara bergantian.

Program berjalan terus dan tidak macet.

Tidak ada proses yang menahan garpu tanpa bisa melanjutkan.

Output menunjukkan siklus thinking → eating → thinking yang stabil.

Analisis

Deadlock berhasil dicegah karena:

Semaphore membatasi hanya 4 filosof yang boleh mengakses garpu bersamaan.
→ Circular wait tidak pernah terbentuk.

Filosof dilewatkan/ditahan sebelum mengambil garpu jika jumlah maksimal tercapai.

Tidak semua filosof memegang satu garpu pada saat yang sama → hold and wait dihilangkan.

Kesimpulan Eksperimen 2

Dengan penerapan sinkronisasi (semaphore), sistem berhasil menghindari deadlock dan memberikan akses yang lebih aman serta adil.

>>Eksperimen 3 – Analisis Kondisi Deadlock (Deadlock vs Fixed)
Tujuan

Mengidentifikasi kondisi deadlock dan bagaimana solusi fixed mengatasi setiap kondisi tersebut.

Hasil Analisis
Kondisi Deadlock	Versi Deadlock	Versi Fixed (Semaphore)
Mutual Exclusion	Terjadi	Tetap terjadi (wajar)
Hold and Wait	Terjadi	Tidak terjadi (karena semaphore membatasi akses)
No Preemption	Terjadi	Sumber daya bisa dilepas sebelum makan (via semaphore)
Circular Wait	Terjadi	Tidak terjadi (lingkaran pecah karena max 4 filosof)
Analisis

Versi deadlock memenuhi keempat syarat deadlock, sehingga deadlock terjadi.

Versi fixed menghilangkan dua kondisi (Hold and Wait + Circular Wait), sehingga deadlock tidak bisa muncul.

Ini membuktikan teori Coffman: hilangkan satu kondisi saja sudah cukup untuk mencegah deadlock.

Kesimpulan Eksperimen 3

Eksperimen berhasil menunjukkan perbedaan antara sistem yang rawan deadlock dan sistem yang sudah diberi mekanisme sinkronisasi.

---

## Kesimpulan
1.Versi awal Dining Philosophers menyebabkan deadlock karena seluruh kondisi deadlock terpenuhi: mutual exclusion, hold and wait, no preemption, dan circular wait. Akibatnya, semua filosof saling menunggu garpu dan tidak ada proses yang dapat melanjutkan eksekusi.

2.Deadlock berhasil dihilangkan pada versi fixed dengan menerapkan mekanisme sinkronisasi seperti semaphore/mutex, membatasi jumlah filosof yang makan, atau mengubah urutan pengambilan garpu sehingga circular wait terputus.

3.Praktikum ini menunjukkan bahwa sinkronisasi yang benar sangat penting untuk memastikan proses dapat berjalan secara bersamaan (concurrency) tanpa konflik atau kebuntuan sumber daya.

---

## Quiz
1.Sebutkan empat kondisi utama penyebab deadlock.
2.Mengapa sinkronisasi diperlukan dalam sistem operasi?
3.Jelaskan perbedaan antara semaphore dan monitor.
3
## jawaban
>>Eksperimen 1 – Versi Deadlock

Pada eksperimen pertama, program menunjukkan bahwa tanpa mekanisme sinkronisasi, para filosof akan saling menunggu garpu yang tidak pernah dilepas. Semua proses berhenti dan tidak ada filosof yang dapat makan.
Kesimpulan: Deadlock terjadi karena semua kondisi deadlock terpenuhi (mutual exclusion, hold and wait, no preemption, circular wait).

>>Eksperimen 2 – Versi Fixed (Dengan Sinkronisasi)

Pada eksperimen kedua, penggunaan semaphore membatasi jumlah filosof yang boleh mengambil garpu secara bersamaan. Hal ini memutus rantai circular wait sehingga proses dapat berjalan dengan lancar.
Kesimpulan: Deadlock berhasil dicegah, dan seluruh filosof dapat makan secara bergantian. Program berjalan stabil dan tidak macet.

>>Eksperimen 3 – Analisis Kondisi Deadlock

Eksperimen ini menunjukkan perbedaan mendasar antara versi deadlock dan versi fixed. Versi deadlock memenuhi semua kondisi penyebab deadlock, sedangkan versi fixed berhasil menghilangkan beberapa di antaranya (terutama hold and wait dan circular wait).
Kesimpulan: Dengan menghilangkan minimal satu kondisi deadlock, sistem dapat mencegah kebuntuan dan memastikan proses berjalan aman serta efisien.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
