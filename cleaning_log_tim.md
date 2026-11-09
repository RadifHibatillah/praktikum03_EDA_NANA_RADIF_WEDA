# Cleaning Log

**Tim:** \[Triaxis\] **Dataset:** dataset.csv (data akademik mahasiswa dengan kolom Target; 4.424 baris × 35 kolom) **Baris mentah:** 4.424 \=\> **baris bersih:** 4.424 (tidak ada baris dibuang) **Terakhir diperbarui:** 19 Oktober 2026

> Sumber angka: keluaran Bagian 10 notebook Pertemuan 4 (sembilan pemeriksaan pada `df_tim`). Tanda **\[ISI n\]** berarti angkanya belum ada di keluaran notebook dan harus dihitung dari `dataset.csv` (kode penghitungnya ada di bagian "Cara melengkapi" di bawah).

---

## Urutan langkah

> Urutan ini bukan selera. Langkah yang dikerjakan terlalu awal membuat langkah berikutnya salah. Hapus baris yang tidak Anda perlukan, tetapi jangan mengubah urutannya tanpa alasan.

| \# | Langkah | Kolom | Baris terdampak | Keputusan | Alasan |
| :---- | :---- | :---- | :---- | :---- | :---- |
| 1 | Perbaiki tipe data | Seluruh kolom (29 int, 5 float, 1 object) | 0 | Tidak ada konversi yang diperlukan. Kolom kode (Marital status, Application mode, Course, Nacionality, kualifikasi dan pekerjaan orang tua) tetap berupa angka di data olahan, tetapi diperlakukan sebagai kategori saat analisis | Tidak ada kolom angka yang tersimpan sebagai teks (pemeriksaan 7 tidak menemukan kolom curiga) dan tidak ada kolom tanggal. Kode seperti Course 1–17 bukan ukuran: rata-rata dan korelasinya tidak bermakna, sehingga cukup ditandai di kamus data tanpa mengubah nilainya |
| 2 | Buang spasi pada kolom teks | Target (satu-satunya kolom teks) | 0 | Tidak ada perubahan | Jumlah nilai unik Target sama (3) sebelum dan sesudah `strip().lower()`, jadi tidak ada varian spasi atau kapitalisasi |
| 3 | Placeholder menjadi kosong | Curricular units 1st sem (grade), Curricular units 2nd sem (grade) | \[ISI n sem 1\] dan \[ISI n sem 2\] baris bernilai 0 | Nilai 0 diubah menjadi kosong (NaN) **hanya bila** evaluations pada semester yang sama juga 0\. Nilai 0 dengan evaluations \> 0 dibiarkan dan dihitung terpisah (\[ISI n\]) | Nilai grade terkecil yang sah adalah 9,8 (sem 1\) dan 10,0 (sem 2); tidak ada nilai di antara 0 dan angka itu, jadi 0 bukan skor rendah melainkan penanda "tidak ada nilai". Contoh di data: baris 0 (enrolled 0, evaluations 0, grade 0\) dan baris 2 (enrolled 6, evaluations 0, approved 0, grade 0). Efeknya terlihat di ringkasan: rata-rata 10,64 jauh di bawah median 12,29 (sem 1). Mempertahankan 0 menarik rata-rata ke bawah dan menyamakan "tidak dinilai" dengan "nilai nol". Teks placeholder tidak ada (pemeriksaan 3\) |
| 4 | Seragamkan kategori | Target | 0 | Tidak ada perubahan | Target hanya punya 3 nilai unik dan konsisten; tidak ada sinonim atau salah ketik yang perlu diputuskan manual |
| 5 | Tangani duplikat | Seluruh kolom; kunci \[Age at enrollment, Gender, Course\] | 0 duplikat persis; 3.742 baris "duplikat" menurut kunci | Tidak ada baris dibuang | Duplikat persis 0\. Hitungan 3.742 menurut kunci bukan duplikat nyata: kunci itu terdiri dari tiga atribut berkardinalitas rendah (usia, jenis kelamin, jurusan), bukan identitas. Dataset tidak punya ID mahasiswa, sehingga tidak ada kunci primer yang bisa dipakai untuk menguji duplikat nyaris |
| 6 | Tangani nilai mustahil | Age at enrollment, grade sem 1 dan 2, enrolled sem 1, Inflation rate, approved vs enrolled sem 1, International vs Nacionality | 0 | Tidak ada baris atau nilai diubah | Tujuh aturan diuji dan semuanya 0 pelanggaran: usia \< 16 atau \> 100 (rentang aktual 17–70); grade \< 0 atau \> 20 (maksimum 18,88 dan 18,57); enrolled negatif; inflasi \> 50% (rentang −0,8 sampai 3,7); approved \> enrolled; International \= 1 dengan Nacionality \= 1 |
| 7 | Tangani nilai kosong | Seluruh kolom | 0 kosong sejati; \[ISI n\] kosong baru dari langkah 3 | Tidak diisi (tanpa imputasi) | Pemeriksaan 2 menemukan 0 sel kosong. Kosong baru pada grade berarti "tidak ada nilai"; mengisinya dengan median akan menciptakan nilai bagi mahasiswa yang tidak dievaluasi dan meratakan perbedaan antar kelompok Target |
| 8 | Buat kolom turunan | ada\_nilai\_sem1, ada\_nilai\_sem2 (usulan) | 4.424 | \[ISI: dibuat atau tidak\] Penanda boolean apakah grade tersedia | Agar mahasiswa yang tidak dinilai tetap dapat dianalisis sebagai kelompok sendiri dan perubahan di langkah 3 dapat diaudit |

---

## Peta keputusan manual

Penyeragaman yang **tidak bisa diputuskan mesin**: sinonim, salah ketik, penggabungan kategori. Kolom terakhir adalah yang paling penting — dari mana Anda tahu penggabungan itu benar?

| Nilai asal | Diubah menjadi | Dasar keputusan |
| :---- | :---- | :---- |
| grade sem 1 \= 0 dengan evaluations sem 1 \= 0 | (kosong) | Nilai sah terkecil 9,8; 0 tidak berada pada sebaran skor sungguhan, dan tidak ada evaluasi yang bisa menghasilkan skor |
| grade sem 2 \= 0 dengan evaluations sem 2 \= 0 | (kosong) | Nilai sah terkecil 10,0; alasan sama |
| grade \= 0 dengan evaluations \> 0 | tidak diubah | Mungkin nilai nol sungguhan; tidak ada dasar untuk menghapusnya. \[ISI n baris\] |

Tidak ada penyeragaman teks yang diperlukan.

---

## Yang sengaja TIDAK diubah

Sama pentingnya dengan yang diubah. Masalah yang Anda temukan tetapi putuskan untuk dibiarkan, beserta alasannya dan akibatnya bagi analisis.

| Masalah | Mengapa dibiarkan | Akibat bagi analisis |
| :---- | :---- | :---- |
| 3.742 baris "duplikat" menurut kunci \[Age at enrollment, Gender, Course\] | Kunci bukan identitas; tidak ada ID mahasiswa | Duplikat nyaris tidak dapat dideteksi; diasumsikan setiap baris adalah satu mahasiswa |
| Age at enrollment maksimum 70 tahun | Nilai sah secara logis dan bukan placeholder | Menjadi pencilan pada analisis usia; perlu uji dengan dan tanpa nilai ekstrem |
| Nama kolom "Nacionality" (salah eja) | Mengikuti nama asli di sumber agar kode dan dokumentasi tetap cocok | Harus ditulis persis di seluruh kode |
| Nilai kolom kode (Course, Application mode, kualifikasi, pekerjaan orang tua) berupa angka tanpa label | Tidak ada kamus data untuk menerjemahkan | Tidak boleh dirata-ratakan; interpretasi hasil per kategori menunggu kamus data |
| Unemployment rate, Inflation rate, GDP berulang pada banyak baris (misalnya baris 0 dan 2 identik) | Nilai makroekonomi per periode, bukan per mahasiswa | Bukan galat; tetapi baris-baris dalam periode yang sama tidak independen |
| grade \= 0 dengan evaluations \> 0 | Lihat peta keputusan manual | Tetap sebagai 0 di data olahan |

---

## Pertanyaan yang belum terjawab

Hal yang perlu dikonfirmasi ke pemilik data atau dosen. Tuliskan meskipun belum ada jawabannya; daftar ini menjadi bagian "Keterbatasan" pada laporan M2.

- [ ] Apakah Application order \= 0 sah, dan apa artinya dibanding 1?  
- [ ] Apakah usia 70 tahun saat mendaftar adalah data nyata atau galat entri?  
- [ ] Apakah setiap baris mewakili satu mahasiswa unik, mengingat tidak ada ID?  
- [ ] Apa skala resmi grade (diasumsikan 0–20 dari maksimum teramati 18,88)?

---

## Dampak keseluruhan

| Ukuran | Sebelum | Sesudah | Catatan |
| :---- | :---- | :---- | :---- |
| Jumlah baris | 4.424 | 4.424 | Tidak ada baris dibuang |
| Jumlah kolom | 35 | 35&nbsp;&nbsp; |  |
| Total sel kosong | 0 | 0 | Naik karena nilai 0 pada grade yang menyamar sebagai angka kini dinyatakan kosong |
| Baris duplikat | 0 | 0 |  |
| Kategori pada kolom kunci | Target: 3 | Target: 3 | Tidak ada penyeragaman |

---

## Reproduktibilitas

- [x] Notebook berjalan dari awal sampai akhir setelah *Restart and run all*  
- [x] Pembersihan dibungkus dalam satu fungsi, bukan tersebar di banyak sel  
- [x] `data/raw/` tidak berubah dan tidak ikut diunggah  
- [x] Hasil tersimpan di `data/processed/`  
- [x] `python cek_m2.py` berjalan tanpa status GAGAL