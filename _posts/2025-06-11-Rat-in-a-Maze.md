---
layout: post
title: "Rat in a Maze Problem"
date: 2025-06-10 10:00:00 +0800
categories: backtracking cpp
tags: [c++, backtracking]
---

## Apa itu Rat in a Maze Problem?
Rat in a Maze Problem adalah masalah klasik dalam pemrograman menggunakan backtracking, di mana seekor tikus harus menemukan jalan dari posisi awal (biasanya kiri atas) menuju tujuan (biasanya kanan bawah) dalam sebuah maze berbentuk matriks persegi.

## Prinsip Kerja
1. Mulai dari sel awal (0, 0).
2. Pada setiap langkah, cek apakah langkah valid:
- Tidak keluar dari batas.
- Tidak menuju sel yang di-blok (0).
- Belum pernah dikunjungi.
3. Jika valid:
- Tandai sebagai bagian dari solusi.
- Lanjutkan ke arah yang memungkinkan (kanan, bawah, kiri, atas).
- Jika mencapai tujuan, simpan atau tampilkan jalur.
4. Jika tidak ada jalan lanjut, backtrack (mundur dan coba rute lain).

## Contoh Permasalahan
Misalkan kita punya labirin ukuran 4x4:
- Tikus mulai dari posisi (0, 0).
- Hanya bisa melangkah ke bawah atau ke kanan, tidak boleh ke 0 (dinding).
- Ada dinding di posisi (0,1), (0,2), (1,2), (2,0), dan (2,2).

Tikus bisa bergerak sebagai berikut:
- (0,0) ke (1,0)
- (1,0) ke (1,1)
- (1,1) ke (2,1)
- (2,1) ke (3,1)
- (3,1) ke (3,2)
- (3,2) ke (3,3) ✅ (Tujuan)

Jadi jalur lengkap:
(0,0) → (1,0) → (1,1) → (2,1) → (3,1) → (3,2) → (3,3)



## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(int x, int y, vector<vector<int>>& maze, int n, vector<vector<int>>& visited) {
    return x >= 0 && x < n && y >= 0 && y < n &&
           maze[x][y] == 1 && visited[x][y] == 0;
}

bool solveMaze(int x, int y, vector<vector<int>>& maze, int n,
               vector<vector<int>>& visited, vector<vector<int>>& path) {
    if (x == n - 1 && y == n - 1) {
        path[x][y] = 1;
        return true;
    }

    if (isSafe(x, y, maze, n, visited)) {
        visited[x][y] = 1;
        path[x][y] = 1;

        if (solveMaze(x + 1, y, maze, n, visited, path)) return true;
        if (solveMaze(x, y + 1, maze, n, visited, path)) return true;
        if (solveMaze(x - 1, y, maze, n, visited, path)) return true;
        if (solveMaze(x, y - 1, maze, n, visited, path)) return true;

        path[x][y] = 0; // Backtrack
    }

    return false;
}

int main() {
    vector<vector<int>> maze = {
        {1, 0, 0, 0},
        {1, 1, 0, 1},
        {0, 1, 0, 0},
        {1, 1, 1, 1}
    };

    int n = maze.size();
    vector<vector<int>> visited(n, vector<int>(n, 0));
    vector<vector<int>> path(n, vector<int>(n, 0));

    if (solveMaze(0, 0, maze, n, visited, path)) {
        cout << "Jalur ditemukan:\n";
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                cout << path[i][j] << " ";
            }
            cout << endl;
        }
    } else {
        cout << "Tidak ada jalur yang ditemukan.\n";
    }

    return 0;
}

{% endraw %}
```

## Implementasi Dalam Kehidupan
- Navigasi robot: mencari jalur dari titik awal ke tujuan di ruangan dengan rintangan.
- Game AI: NPC mencari jalan keluar dari labirin.
- Pemetaan rute otomatis: seperti sistem GPS yang menghindari jalan buntu.n.

## Kelebihan dan Kekurangan
### Kelebihan:
- Mampu menemukan solusi meskipun rutenya kompleks.
- Bisa dikembangkan untuk menemukan semua solusi.real-time

### Kekurangan:
- Tidak efisien untuk maze besar (kompleksitas eksponensial).
- Banyak percabangan bisa memakan waktu dan memori.

## Kesimpulan
Rat in a Maze mengajarkan konsep penting dalam pencarian solusi menggunakan rekursi dan backtracking. Meski sederhana, konsep ini menjadi dasar algoritma lebih kompleks seperti AI, DFS, dan algoritma pemetaan rute nyata. Menguasainya membuka pemahaman logika pencarian solusi dalam berbagai bidang.