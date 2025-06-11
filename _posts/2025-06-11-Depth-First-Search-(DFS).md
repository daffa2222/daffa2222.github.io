---
layout: post
title: "Depth-First Search (DFS)"
date: 2025-06-11 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Activity Selection Problem?
Depth-First Search (DFS) adalah algoritma penelusuran (traversal) atau pencarian pada graf atau pohon yang menjelajahi sedalam mungkin satu jalur sebelum kembali dan menjelajahi jalur lain. DFS sering digunakan untuk mengeksplorasi semua simpul dan sisi graf, dan sangat berguna dalam mendeteksi siklus, pencarian komponen, dan pemrosesan topologi.


## Prinsip Kerja
DFS menggunakan prinsip LIFO (Last In First Out), yang biasanya diimplementasikan menggunakan rekursi (stack implicit) atau menggunakan stack secara eksplisit.

Langkah-langkah DFS:
1. Mulai dari simpul awal (start/root).
2. Tandai simpul sebagai dikunjungi.
3. Kunjungi satu tetangga yang belum dikunjungi, lalu ulangi proses dari sana (masuk lebih dalam).
4. Jika semua tetangga telah dikunjungi, kembali ke simpul sebelumnya.
5. Lanjutkan sampai semua simpul telah dikunjungi atau target ditemukan.



## Contoh Permasalahan
Graf:
```
      A
     / \
    B   C
   / \   \
  D   E   F

```
Representasi Edges:
```
A - B, A - C, B - D, B - E, C - F
```
DFS dari node A:
1. Mulai dari A
2. Masuk ke B
3. Masuk ke D (tidak punya tetangga yang belum dikunjungi)
4. Kembali ke B, masuk ke E
5. Kembali ke A, masuk ke C, lalu ke F

Urutan Kunjungan:
```
A → B → D → E → C → F
```
(urutan bisa berbeda tergantung urutan tetangga)
## Implementasi (C++)
Versi Rekursif:
```
cpp
{% raw %}
#include <iostream>
#include <vector>

using namespace std;

void dfs(int node, vector<vector<int>>& adjList, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " ";

    for (int neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, adjList, visited);
        }
    }
}

int main() {
    int vertices = 6;
    vector<vector<int>> adjList(vertices);

    // A=0, B=1, C=2, D=3, E=4, F=5
    adjList[0] = {1, 2};     // A -> B, C
    adjList[1] = {0, 3, 4};  // B -> A, D, E
    adjList[2] = {0, 5};     // C -> A, F
    adjList[3] = {1};        // D -> B
    adjList[4] = {1};        // E -> B
    adjList[5] = {2};        // F -> C

    vector<bool> visited(vertices, false);

    cout << "DFS traversal dari node A (0): ";
    dfs(0, adjList, visited);

    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
DFS diterapkan dalam berbagai bidang:
1. Pemecahan Maze atau Labirin: DFS mengeksplorasi semua jalan secara mendalam.
2. Sistem File dan Direktori: Menelusuri struktur folder menggunakan DFS.
3. AI dan Game: Untuk menyelesaikan puzzle atau eksplorasi kemungkinan secara mendalam.
4. Pendeteksian Siklus: Dalam sistem dependency (misalnya compiler atau sistem build).
5. Topological Sorting: Dalam pemrosesan ketergantungan tugas (misalnya A harus selesai sebelum B).
6. Analisis Komponen Terhubung: Dalam jaringan atau relasi sosial.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Menggunakan memori lebih sedikit dibanding BFS pada graf lebar.
2. Mudah diimplementasikan secara rekursif.
3. Cocok untuk eksplorasi lengkap seperti pencarian semua solusi.
4. Dapat digunakan untuk banyak analisis graf: pendeteksian siklus, topological sort, dll.

### Kekurangan:
1. Tidak menjamin jalur terpendek (tidak cocok untuk pencarian jarak minimum).
2. Bisa masuk ke jalur sangat dalam yang tidak efektif.
3. Rentan stack overflow pada graf besar atau terlalu dalam (jika rekursif).


## Kesimpulan
Depth-First Search (DFS) adalah algoritma penting dalam dunia pemrograman dan ilmu komputer. Dengan strategi penelusuran yang masuk ke dalam terlebih dahulu, DFS sangat berguna untuk mengeksplorasi graf dan pohon secara menyeluruh. Meski tidak efisien untuk mencari jalur terpendek, kekuatan DFS terletak pada kemampuannya untuk menemukan semua kemungkinan atau menyelidiki struktur dalam graf, serta mendukung berbagai algoritma lanjutan.