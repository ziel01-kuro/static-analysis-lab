# Laporan Analisis Statis - Biner 01 (Minesweeper)

- **Nama Berkas:** winmine.exe
- **Tanggal Analisis:** 5 Juli 2026
- **Format Berkas:** PE32 (Portable Executable 32-bit)

## 1. Identifikasi & Metadata Kriptografis
Karakteristik fisik dan sidik jari biner diekstrak menggunakan ringkasan statis Ghidra CodeBrowser:
* **SHA-256 Hash:** [Nilai Hash SHA-256 Berkas]
* **MD5 Hash:** [Nilai Hash MD5 Berkas]
* **Compiler Target:** Microsoft Visual Studio 2012 (v110) (Platform Windows)
* **Arsitektur:** x86 (32-bit Little Endian)

## 2. Ekstraksi String & Indikator Kontekstual
Melalui visualisasi teks statis internal, biner ini memuat beberapa instruksi string literal yang menentukan alur eksekusi program:
* `Minesweeper` (Nama jendela utama aplikasi)
* `SetTimer` & `KillTimer` (Referensi tekstual terhadap fungsi kontrol waktu internal)

## 3. Analisis Tabel Impor (Import Table)
Berdasarkan struktur PE yang diekstrak pada lingkungan analisis statis menggunakan Ghidra, program memanggil fungsi eksternal dari DLL (Dynamic-Link Library) utama:
* **`USER32.DLL`**: Mengendalikan elemen antarmuka grafis (GUI), penanganan jendela (*windowing*), penangkapan input klik, serta memuat fungsi API krusial `SetTimer` dan `KillTimer`.
* **`KERNEL32.DLL`**: Bertanggung jawab atas interaksi tingkat rendah dengan subsistem operasi Windows, termasuk manajemen memori dasar dan kontrol daur hidup proses eksekusi biner.
* **`GDI32.DLL`**: Berperan dalam merender komponen grafis visual pada papan permainan, termasuk warna kotak penutup, angka indikator kedekatan, dan ikon komponen ranjau.
* **`MSVCRT.DLL`**: Menyediakan fungsi runtime standar bahasa C untuk menangani operasi komputasi matematika internal di dalam program.

## 4. Alur Logika Dekompilasi & Kesimpulan
Struktur fungsi `FUN_0100384f` yang didekompilasi oleh Ghidra memperlihatkan logika if-else tanpa adanya *obfuscation*:
```c
void __cdecl FUN_0100384f(UINT_PTR param_1, UINT param_2, TIMERPROC param_3)
{
  UINT_PTR uVar1;
  byte unaff_BL;
  HWND unaff_retaddr;

  uVar1 = SetTimer(unaff_retaddr, param_1, param_2, param_3);
  if (uVar1 == 0) {
    FUN_01003950(4);
  }
  
  if ((DAT_01005000 & unaff_BL) == 0) {
    DAT_0100511c = -2;
    DAT_01005118 = -2;
  }
  
  if (DAT_01005144 == 0) {
    if (((~(DAT_01005340)[DAT_01005118 + DAT_0100511c * 0x20] & 0x40) == 0) && 
       (((&DAT_01005340)[DAT_01005118 + DAT_0100511c * 0x20] & 0x1f) != 0xe)) {
       FUN_01003512(DAT_01005118, DAT_0100511c);
    }
  }
  else {
    FUN_010035b7(DAT_01005118, DAT_0100511c);
  }
  FUN_01002913(DAT_01005160);
  return;
}
```

## 5. Lampiran Bukti Analisis (Anotasi)
Hasil analisis statis bisa dilihat pada folder **images/biner-01-images**.

* Hasil analisis metadata: (biner01-01-metadata.png)
* Hasil analisis imports: (biner01-02-imports-overview.png)
* Hasil analisis imports SetTimer: (biner01-03-imports-settimer.png)
* Hasil analisis logic SetTimer: (biner01-04-logic-settimer.png)
* Hasil analisis logic KillTimer: (biner01-05-logic-killtimer.png) & (biner01-06-logic-killtimer.png)