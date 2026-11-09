# AI Usage Log

**Tim:** Triaxis
**Proyek:** Membersihkan Data dengan Alasan (M2, Exploratory Data Analysis KMTI21133)
**Terakhir diperbarui:** 19 Oktober 2026

## Ringkasan

Tim memakai AI generatif hanya untuk satu keperluan: **menyusun Laporan M2 (Data Quality Report)** untuk dataset `transaksi_koperasi_2025.csv`. Tidak ada penggunaan AI untuk bagian lain proyek.

## Alat yang dipakai

| Alat | Penyedia | Dipakai oleh |
|---|---|---|
| Claude (claude.ai) | Anthropic | [ISI nama anggota yang menjalankan percakapan] |

## Entri penggunaan

| Tanggal | Tugas | Permintaan inti | Yang dihasilkan AI | Yang dipakai tim | Yang diperiksa atau diubah tim |
|---|---|---|---|---|---|
| 19 Okt 2026 | Mendiagnosis dan membersihkan data koperasi | Membaca data dan template, lalu mengisi Data Quality Report | Profil kualitas data; skrip pembersihan (`clean_koperasi.py`); angka temuan (mis. 52 total tidak cocok, 43 duplikat, rating −999); draf isi Bagian 1–8 dan Lampiran A–B; `cleaning_log.md`; grafik total_bayar | Isi laporan sebagai draf awal | [ISI: mis. memeriksa angka terhadap data, menjalankan ulang skrip] |
| 19 Okt 2026 | Menjawab pertanyaan yang belum terjawab | Meminta jawaban dari bukti di data | Jawaban per pertanyaan beserta status (terjawab atau perlu konfirmasi) | Status ✅ atau ⬜ pada tiap pertanyaan | [ISI] |
| 19 Okt 2026 | Merumuskan pertanyaan payung | Meminta 1 pertanyaan utama dan 3 turunan | Usulan pertanyaan utama dan tiga pertanyaan turunan | Seluruh usulan dimasukkan ke laporan | [ISI: apakah diubah] |
| 19 Okt 2026 | Menyusun sitasi dan asal data | Memberi tautan e-learning sebagai sumber | Kalimat sitasi dan isian provenans | Kalimat sitasi | Nama dosen, tanggal pengambilan, dan lisensi diisi tim sendiri |

## Yang diisi tim sendiri (bukan AI)

- Nama tim, anggota, pembagian peran, dan judul proyek
- Tautan repositori, status repositori, dan pengaturan `.gitignore`
- Nama dosen pada sitasi, tanggal pengambilan, dan lisensi
- Keputusan akhir atas setiap usulan pembersihan

## Catatan tanggung jawab

AI dipakai sebagai pembantu menyusun draf dan menghitung. Seluruh angka dan keputusan pada laporan menjadi tanggung jawab tim. Asumsi yang dibuat AI (misalnya `total_bayar` yang salah pada 52 baris, bukan jumlah) tercantum di Bagian 6 laporan sebagai hal yang perlu dikonfirmasi ke pemilik data.

## Bagian lain proyek

Tidak ada penggunaan AI generatif pada bagian lain proyek selain yang tercantum di atas.
