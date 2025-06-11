---
layout: post
title: "Breadth-First Search (BFS)"
date: 2025-06-11 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Breadth-First Search (BFS) ?
Breadth-First Search (BFS) adalah algoritma penelusuran (traversal) atau pencarian pada graf atau pohon yang bekerja dengan cara mengeksplorasi semua tetangga (node yang berdekatan) terlebih dahulu sebelum melanjutkan ke tingkat yang lebih dalam.

BFS sering digunakan untuk:

1. Menemukan jalur terpendek dalam graf tak berbobot.
2. Menelusuri semua node pada pohon atau graf.
3. Menyelesaikan masalah antrian atau level-order traversal.

## Prinsip Kerja
BFS bekerja berdasarkan prinsip queue (FIFO - First In First Out):

1. Mulai dari simpul awal (root/start node).
2. Kunjungi node dan masukkan ke dalam antrian.
3. Sambil antrian tidak kosong:
- Ambil node dari depan antrian.
- Tandai sebagai dikunjungi.
- Masukkan semua tetangganya yang belum dikunjungi ke antrian.
4. Ulangi sampai semua node telah dikunjungi atau sampai menemukan target.

Struktur Data yang Digunakan:
- Queue: Menyimpan node yang akan dieksplorasi.
- Visited Array atau Set: Menandai node yang sudah dikunjungi.

## Contoh Permasalahan
Misal ada graf tak berbobot dan tak berarah seperti berikut:
```
      A
     / \
    B   C
   / \   \
  D   E   F
```
Representasi Edge:
```
A - B, A - C, B - D, B - E, C - F
```
Langkah-langkah BFS dari node A:
- Mulai dari A, queue: [A]
- Keluarkan A, masukkan B dan C, queue: [B, C]
- Keluarkan B, masukkan D dan E, queue: -[C, D, E]
-Keluarkan C, masukkan F, queue: [D, E, F]
- Lanjutkan sampai queue kosong.
Urutan kunjungan BFS:
'''
A → B → C → D → E → F
'''

## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

void bfs(int start, vector<vector<int>>& adjList, vector<bool>& visited) {
    queue<int> q;
    q.push(start);
    visited[start] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";

        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    int vertices = 6;
    vector<vector<int>> adjList(vertices);

    // Edge list: A=0, B=1, C=2, D=3, E=4, F=5
    adjList[0] = {1, 2}; // A -> B, C
    adjList[1] = {0, 3, 4}; // B -> A, D, E
    adjList[2] = {0, 5}; // C -> A, F
    adjList[3] = {1}; // D -> B
    adjList[4] = {1}; // E -> B
    adjList[5] = {2}; // F -> C

    vector<bool> visited(vertices, false);

    cout << "BFS traversal mulai dari node A (0): ";
    bfs(0, adjList, visited);

    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Penentuan Jalur Terpendek:
- Google Maps, GPS routing (pada graf jalan yang tidak berbobot).

2. Sosial Media:
-Menemukan "teman dari teman", atau saran koneksi berdasarkan tingkat kedekatan.

3. Web Crawling:
-Mesin pencari menelusuri situs web mulai dari satu URL ke semua link terkait.

4. AI dan Game:
-Menemukan langkah minimum dalam permainan puzzle atau labirin.

5. Sistem Jaringan:
-Penyebaran paket data ke seluruh jaringan secara merata (multicast routing).

## Kelebihan dan Kekurangan
### Kelebihan:
1. Menemukan jalur terpendek dalam graf tak berbobot.

2. Cocok untuk struktur berlevel, seperti pohon dan hirarki.

3. Lebih cepat dalam menjangkau solusi dekat root/start node.

### Kekurangan:
1. Penggunaan memori tinggi, karena semua node pada level tertentu disimpan di memori.

2. Kurang efisien untuk graf besar dan dalam.

3. Tidak cocok untuk graf berbobot (lebih baik gunakan Dijkstra atau A*).

## Kesimpulan
Breadth-First Search (BFS) adalah algoritma penelusuran graf yang sangat berguna untuk eksplorasi dan pencarian jalur minimum dalam graf tak berbobot. Dengan prinsip antrian dan pendekatan level-by-level, BFS memberikan solusi efisien dalam berbagai aplikasi dunia nyata, seperti jaringan sosial, routing, dan AI. Meski memiliki kelemahan dalam penggunaan memori, BFS tetap menjadi fondasi penting dalam dunia algoritma dan struktur data.