---
layout: post
title: "Kahn’s Algorithm"
date: 2025-06-10 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Kahn’s Algorithm?
Kahn’s Algorithm adalah algoritma untuk melakukan Topological Sorting pada sebuah Directed Acyclic Graph (DAG). Topological sorting adalah urutan linear dari simpul-simpul dalam sebuah graf sedemikian rupa sehingga untuk setiap sisi dari simpul u ke simpul v, u muncul sebelum v dalam urutan tersebut.

Kahn’s Algorithm dikembangkan oleh Arthur B. Kahn dan menggunakan pendekatan berbasis BFS (Breadth-First Search) untuk menyusun topological order dari graf yang tidak memiliki siklus.nya.

## Prinsip Kerja
Prinsip kerja Kahn’s Algorithm:
1. Hitung indegree (jumlah sisi masuk) untuk setiap simpul.
2. Masukkan semua simpul dengan indegree 0 ke dalam sebuah queue.
3. Selama queue tidak kosong:
- Ambil simpul dari depan queue dan tambahkan ke hasil topological sort.
- Kurangi indegree dari semua tetangganya sebesar 1.
- Jika indegree tetangga menjadi 0, masukkan ke dalam queue.
4. Jika semua simpul telah diproses, maka urutan topologis valid.
5. Jika tidak, maka graf mengandung siklus dan topological sort tidak mungkin.

## Contoh Permasalahan
Bayangkan kamu mengembangkan modul aplikasi, dan setiap modul memiliki ketergantungan.

Modul dan ketergantungan:
- Modul A tidak memiliki ketergantungan.
- Modul B tergantung pada A.
- Modul C tergantung pada A.
- Modul D tergantung pada B dan C.
- Modul E tergantung pada D.

Secara hubungan:
```
A → B  
A → C  
B → D  
C → D  
D → E
```
Langkah-langkah menyelesaikan dengan Kahn’s Algorithm:
1. Mulai dengan mencari simpul tanpa ketergantungan → hanya A.
2. Masukkan A ke urutan, lalu kurangi ketergantungan B dan C.
3. Sekarang B dan C tidak memiliki ketergantungan → tambahkan ke antrian.
4. Proses B → kurangi ketergantungan D.
5. Proses C → D kini tidak punya ketergantungan → tambahkan ke antrian.
6. Proses D → kurangi ketergantungan E.
7. E kini bebas → tambahkan.

8. Hasil urutan topologi:
A → B → C → D → E (atau A → C → B → D → E, tergantung urutan queue)

## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

void kahnTopoSort(int V, vector<vector<int>>& adj) {
    vector<int> indegree(V, 0);
    for (int u = 0; u < V; u++) {
        for (int v : adj[u]) indegree[v]++;
    }

    queue<int> q;
    for (int i = 0; i < V; i++) {
        if (indegree[i] == 0) q.push(i);
    }

    vector<int> topo;
    while (!q.empty()) {
        int u = q.front(); q.pop();
        topo.push_back(u);
        for (int v : adj[u]) {
            if (--indegree[v] == 0) q.push(v);
        }
    }

    if (topo.size() != V) cout << "Graf mengandung siklus\n";
    else {
        cout << "Urutan Topologis: ";
        for (int node : topo) cout << node << " ";
        cout << endl;
    }
}

int main() {
    int V = 5;
    vector<vector<int>> adj(V);
    adj[0] = {1, 2};  // A → B, C
    adj[1] = {3};     // B → D
    adj[2] = {3};     // C → D
    adj[3] = {4};     // D → E

    kahnTopoSort(V, adj);
    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Penyusunan jadwal kuliah: mata kuliah wajib diselesaikan dulu.
2. Sistem build software: urutan kompilasi file yang saling bergantung.
3. Dependency resolution: sistem seperti npm, pip, apt.
4. Sistem workflow industri: langkah yang bergantung satu sama lain.

## Kelebihan dan Kekurangan
### Kelebihan:
- Deteksi siklus dengan mudah.
- Sederhana dan efisien (O(V + E)).
- Cocok untuk graf besar dan kompleks.

### Kekurangan:
- Tidak cocok untuk graf dengan siklus.
- Hasil tidak unik, tergantung urutan queue.
- Hanya bekerja untuk DAG.

## Kesimpulan
Kahn’s Algorithm adalah solusi praktis dan efisien untuk menyusun urutan eksekusi dalam graf tanpa siklus. Dengan pendekatan berbasis indegree dan queue, algoritma ini sangat cocok untuk aplikasi nyata seperti dependency resolver, build system, dan penjadwalan kompleks. Sifatnya yang deterministik dan kemampuan deteksi siklus menjadikannya salah satu algoritma penting dalam ilmu komputer terapan.

