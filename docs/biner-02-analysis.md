# Laporan Analisis Statis - Biner 02 (Monsignors Crackme)

- **Nama Berkas:** hello.exe
- **Tanggal Analisis:** 4 Juli 2026
- **Format Berkas:** PE32+ (Portable Executable 64-bit)

## 1. Identifikasi & Metadata Kriptografis
Karakteristik fisik dan sidik jari biner diekstrak menggunakan ringkasan statis Ghidra CodeBrowser:
* **SHA-256 Hash:** afd242f5fe7f0d8bb6323d812e411763d402fb25c0cbdb5dcaccf4e188950d7f
* **MD5 Hash:** a47fc466d8efba2413395a68d00cfdd1
* **Compiler Target:** gcc:unknown (Platform Windows)
* **Arsitektur:** x86_64 (64-bit Little Endian)

## 2. Ekstraksi String & Indikator Kontekstual
Melalui visualisasi teks statis internal, biner ini memuat beberapa instruksi string literal yang menentukan alur eksekusi program:
* `Enter password: ` (Instruksi penunjuk input pengguna)
* `secret` (String rahasia yang kemungkinan besar merupakan password)
* `Access granted!` (Pesan sukses jika password benar)
* `Access denied!` (Pesan gagal jika password salah)

## 3. Analisis Tabel Impor (Import Table)
Berdasarkan struktur PE yang diekstrak pada lingkungan analisis statis menggunakan Ghidra, program memanggil fungsi eksternal dari DLL (Dynamic-Link Library) utama:
* **`MSVCRT.DLL`**: Menyediakan fungsi runtime standar bahasa C. Fungsi krusial yang digunakan meliputi `printf` (pencetakan teks ke konsol), `scanf` (penerima input string), dan `strcmp` (pembaca kontrol logika pembanding antar dua string).
* **`KERNEL32.DLL`**: Bertanggung jawab atas interaksi tingkat rendah dengan subsistem operasi Windows, termasuk penanganan pengecualian sistem (`SetUnhandledExceptionFilter`) dan manajemen memori dasar (`VirtualProtect`, `VirtualQuery`).

## 4. Alur Logika Dekompilasi & Kesimpulan
Struktur fungsi `main` yang didekompilasi oleh Ghidra memperlihatkan logika if-else tanpa adanya *obfuscation*:
```c
iVar1 = strcmp(local_48, "secret");
if (iVar1 == 0) {
    printf("Access granted!\n");
}

## 5. Lampiran Bukti Analisis (Anotasi)
Hasil analisis statis bisa dilihat pada folder **images**.

!hasil analisis metadata: (biner02-01-metadata,png)
!hasil analisis strings: (biner02-02-strings.png)
!hasil analisis imports: (biner02-03-imports.png) & (biner02-04-imports)
!hasil analisis main decompiler: (biner02-05-decompile)
