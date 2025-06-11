---
layout: post
title: "Dijkstra’s Algorithm"
date: 2025-06-11 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Dijkstra’s Algorithm?
ADijkstra’s Algorithm adalah algoritma pencarian jalur terpendek dari satu simpul sumber ke semua simpul lainnya dalam graf berbobot positif. Dikembangkan oleh Edsger W. Dijkstra pada tahun 1956, algoritma ini merupakan salah satu algoritma paling efisien dan banyak digunakan untuk pemodelan jarak dan rute terpende

## Prinsip Kerja
Inti dari algoritma:
1. Mulai dari simpul awal.
2. Selalu pilih simpul dengan jarak terkecil yang belum dikunjungi.
3. Perbarui jarak semua tetangga simpul tersebut.
4. Tandai simpul tersebut sebagai sudah dikunjungi.
5. Ulangi hingga semua simpul telah dikunjungi atau jarak minimum ke simpul tujuan telah ditemukan.

Struktur data yang biasa digunakan:
1. Array/Map jarak (distance[]):  Menyimpan jarak minimum dari sumber ke setiap node.
2. Priority Queue (Min Heap): Memilih simpul dengan jarak terkecil dengan cepat.
3. Visited Set / Array: Menandai node yang telah diproses.

## Contoh Permasalahan
Graf Berbobot:
```
Graf:
    A
  / | \
(1)(4)(2)
 /  |  \
B---C---D
 \     /
 (5) (1)
   \ /
    E

```
Representasi:
```
A-B (1), A-C (4), A-D (2)
B-C (3), C-D (2)
B-E (5), D-E (1)
```
Tujuan:
Temukan jarak terpendek dari A ke semua simpul.

Langkah-Langkah Dijkstra:
1. Mulai dari A, set distance[A] = 0, yang lain ∞

2. Pilih A (min jarak), perbarui:
- B = 1
- C = 4
- D = 2
3. Pilih B (min jarak 1), update C = min(4, 1+3) = 4
4. Pilih D (jarak 2), update E = min(∞, 2+1) = 3
5. Pilih E (3), update B (sudah lebih kecil), tidak diubah
6. Pilih C (4), semua sudah dikunjungi

Hasil akhir:
- A: 0
- B: 1
- C: 4
- D: 2
- E: 3




## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <vector>
#include <queue>
#include <utility>
#include <climits>

using namespace std;

typedef pair<int, int> pii;

void dijkstra(int start, vector<vector<pii>>& adj, vector<int>& dist) {
    priority_queue<pii, vector<pii>, greater<pii>> pq;
    dist[start] = 0;
    pq.push({0, start});

    while (!pq.empty()) {
        int currDist = pq.top().first;
        int u = pq.top().second;
        pq.pop();

        for (auto [v, weight] : adj[u]) {
            if (dist[v] > currDist + weight) {
                dist[v] = currDist + weight;
                pq.push({dist[v], v});
            }
        }
    }
}

int main() {
    int V = 5; // Jumlah simpul (A=0, B=1, C=2, D=3, E=4)
    vector<vector<pii>> adj(V);

    // Menambahkan edges: adj[u].push_back({v, weight});
    adj[0].push_back({1, 1}); // A-B
    adj[0].push_back({2, 4}); // A-C
    adj[0].push_back({3, 2}); // A-D
    adj[1].push_back({2, 3}); // B-C
    adj[1].push_back({4, 5}); // B-E
    adj[2].push_back({3, 2}); // C-D
    adj[3].push_back({4, 1}); // D-E

    vector<int> dist(V, INT_MAX);
    dijkstra(0, adj, dist);

    char labels[] = {'A', 'B', 'C', 'D', 'E'};
    for (int i = 0; i < V; i++) {
        cout << "Jarak dari A ke " << labels[i] << ": " << dist[i] << endl;
    }

    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
Dijkstra digunakan di banyak aplikasi:
1. Navigasi dan GPS: Menemukan rute tercepat atau terpendek.
2. Jaringan komputer: Routing data melalui jalur tercepat (misalnya OSPF protocol).
3. Sistem transportasi: Menentukan rute paling efisien antar titik.
4. Game AI: Menentukan jalur terpendek antar karakter atau objek.
5. Pencarian jalur optimal dalam graf seperti peta, jaringan distribusi listrik, dll

## Kelebihan dan Kekurangan
### Kelebihan:
1. Efisien untuk graf berbobot positif.
2. Menjamin solusi optimal (jarak minimum).
3. Dapat dimodifikasi untuk menghentikan lebih awal jika hanya mencari jarak ke satu simpul.

### Kekurangan:
1. Tidak mendukung bobot negatif (gunakan Bellman-Ford untuk itu).
2. Kurang efisien untuk graf sangat besar jika tidak menggunakan struktur data seperti Fibonacci Heap.
3. Tidak skalabel untuk graf dinamis (edge sering berubah), memerlukan rekalkulasi.



## Kesimpulan
Dijkstra’s Algorithm adalah solusi klasik dan efisien untuk menemukan jalur terpendek dari satu titik ke titik lain dalam graf berbobot positif. Dengan prinsip greedy dan penggunaan struktur data seperti priority queue, algoritma ini mampu menghasilkan solusi optimal dalam berbagai bidang praktis. Walaupun memiliki keterbatasan seperti ketidakmampuan menangani bobot negatif, Dijkstra tetap menjadi algoritma fundamental yang wajib dikuasai oleh siapa saja yang belajar algoritma dan graf.

