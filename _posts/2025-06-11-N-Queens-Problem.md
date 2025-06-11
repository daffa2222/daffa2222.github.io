---
layout: N-Queens Problem"
date: 2025-06-10 10:00:00 +0800
categories: backtracking cpp
tags: [c++, backtracking]
---

## Apa itu Activity Selection Problem?
N-Queens Problem adalah masalah klasik dalam bidang kecerdasan buatan dan algoritma backtracking, yang meminta kita untuk menempatkan N ratu pada papan catur ukuran N×N sedemikian rupa sehingga tidak ada dua ratu yang saling menyerang.

Dalam catur, ratu bisa bergerak secara horizontal, vertikal, dan diagonal, sehingga solusi yang sah adalah konfigurasi di mana tidak ada dua ratu dalam satu baris, kolom, atau diagonal yang sama..

## Prinsip Kerja
Solusi klasik menggunakan teknik backtracking:
1. Tempatkan ratu satu per satu di setiap baris, mulai dari baris pertama.
2. Pada setiap baris, coba letakkan ratu di setiap kolom.
3. Setelah menempatkan ratu, periksa apakah posisi itu aman:
- Tidak ada ratu di kolom yang sama.
- Tidak ada ratu di diagonal kiri atas ke kanan bawah.
- Tidak ada ratu di diagonal kanan atas ke kiri bawah.
4. Jika posisi aman, lanjut ke baris berikutnya (rekursi).
5. Jika tidak ada kolom yang cocok di baris tertentu, backtrack ke baris sebelumnya.
6. Ulangi hingga semua ratu berhasil ditempatkan.


## Contoh Permasalahan
Misalkan kita ingin menyelesaikan 4-Queens Problem:
Papan 4×4. Tujuan: tempatkan 4 ratu di posisi yang tidak saling menyerang.
Langkah:
- Letakkan ratu pertama di baris 0, kolom 1 (misalnya).
- Ratu kedua di baris 1, kolom 3 — tidak saling menyerang.
- Ratu ketiga tidak bisa di baris 2 karena semua kolom diserang.
- Backtrack ke baris 1, pindah ratu ke kolom lain.
- Ulangi proses sampai menemukan kombinasi:

Salah satu solusi valid:
- Baris 0 → kolom 1
- Baris 1 → kolom 3
- Baris 2 → kolom 0
- Baris 3 → kolom 2

## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(vector<int>& board, int row, int col, int n) {
    for (int i = 0; i < row; i++) {
        if (board[i] == col || 
            abs(board[i] - col) == abs(i - row))
            return false;
    }
    return true;
}

void solveNQueens(vector<int>& board, int row, int n) {
    if (row == n) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
                cout << (board[i] == j ? "Q " : ". ");
            cout << endl;
        }
        cout << endl;
        return;
    }

    for (int col = 0; col < n; col++) {
        if (isSafe(board, row, col, n)) {
            board[row] = col;
            solveNQueens(board, row + 1, n);
        }
    }
}

int main() {
    int n = 4;
    vector<int> board(n, -1);
    solveNQueens(board, 0, n);
    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
Walau terlihat seperti teka-teki, N-Queens merepresentasikan:
- Masalah penjadwalan: seperti - penempatan tugas tanpa konflik.
- Distribusi tugas paralel: agar proses tidak saling bertabrakan (deadlock).
- Masalah layout chip elektronik: menempatkan komponen agar tidak ada interferensi.
- Penempatan sensor: menghindari area jangkauan yang saling tumpang tindih.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Cocok untuk melatih pemahaman backtracking dan rekursi.
2. Dapat disesuaikan untuk berbagai varian constraint.
3. Sifatnya deterministik dan bisa ditemukan semua solusi.

### Kekurangan:
1. Kompleksitas naik drastis (eksponensial) seiring meningkatnya N.
2. Tidak efisien untuk N sangat besar.
3. Butuh optimisasi tambahan jika ingin performa cepat.

## Kesimpulan
N-Queens Problem adalah contoh sempurna dari permasalahan yang diselesaikan dengan backtracking. Meskipun sederhana dalam definisi, masalah ini mengandung banyak pelajaran penting tentang rekursi, pencarian ruang solusi, dan constraint satisfaction. Solusinya juga memiliki penerapan praktis dalam berbagai bidang teknologi dan optimasi.