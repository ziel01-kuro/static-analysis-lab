# static-analysis-lab
Lab analisis statis PE menggunakan tools Reverse Engineering

Repository ini difokuskan untuk mendokumentasikan proses static analysis terhadap sampel biner Portable Executable (PE). Fokus utamanya membuat lab ini adalah melakukan triage atau identifikasi karakteristik biner tanpa mengeksekusi file tersebut secara langsung, supaya bisa mengetahui potensi dan apa yang sampel biner bisa lakukan secara aman.

## Struktur Repositori
repositori ini diatur dengan struktur direktori sebagai berikut:
- `docs/` : Berisi laporan analisis statis mendalam untuk setiap sampel biner dalam format Markdown.
- `scripts/` : Tempat penyimpanan skrip otomatisasi ekstraksi informasi atau otomasi parsing biner.
- `README.md` : Panduan utama dan indeks laboratorium ini.

untuk laporan lab, seluruh laporan analisis statis dapat diakses secara publik pada folder `docs/`.

## Komponen Pengujian Statis
Setiap dokumen laporan di dalam folder `docs/` akan menggunakan standarisasi informasi sebagai berikut:
- **Cryptographic Hash:** Nilai SHA-256 atau MD5 sebagai sidik jari digital biner yang unik.
- **File Type & Architecture:** Detail arsitektur biner (32-bit atau 64-bit) serta jenis kompiler yang digunakan.
- **Suspicious Strings:** Hasil ekstraksi teks teks (via strings/FLOSS) yang mengindikasikan fungsi tersembunyi, dependensi file, atau URL.
- **Import Table:** Analisis terhadap daftar API Windows (DLL) yang diimpor untuk memetakan apa saja kemampuan teknis biner tersebut.
- **Kesimpulan Awal:** Hipotesis awal mengenai tujuan pembuatan biner berdasarkan indikator-indikator statis yang ditemukan.

---
*Kebijakan Etika: Repositori ini tidak mengunggah atau menyimpan file biner (.exe) aktif untuk mematuhi standar keamanan informasi publik dan hukum siber yang berlaku.*
