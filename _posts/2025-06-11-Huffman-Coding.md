---
layout: post
title: "Huffman Coding"
date: 2025-06-11 10:00:00 +0800
categories: cpp
tags: [c++]
---

## Apa itu Huffman Coding?
Huffman Coding adalah sebuah algoritma kompresi lossless (tanpa kehilangan data) yang digunakan untuk mengurangi ukuran data dengan cara mengganti karakter-karakter dalam data dengan bit-bit yang lebih pendek berdasarkan frekuensi kemunculannya. Semakin sering suatu karakter muncul, semakin pendek kode Huffman-nya.

Dikembangkan oleh David A. Huffman tahun 1952, algoritma ini menghasilkan kode prefix yang artinya tidak ada kode karakter yang menjadi awalan dari kode karakter lainnya.

## Prinsip Kerja
Huffman Coding bekerja berdasarkan prinsip greedy, dengan cara:

1. Hitung frekuensi setiap karakter dalam data.
2. Buat simpul (node) untuk setiap karakter dan frekuensinya.
3. Masukkan semua node ke dalam priority queue (berdasarkan frekuensi).
4. Ambil dua node dengan frekuensi terendah, gabungkan menjadi satu node baru (dengan jumlah frekuensi).
5. Ulangi langkah 4 sampai hanya tersisa satu node → ini menjadi akar pohon Huffman.
6. Dari pohon ini, buat kode biner untuk setiap karakter (kiri = 0, kanan = 1).
7. Gunakan kode ini untuk mengompresi data.

## Contoh Permasalahan
Misalnya kita ingin mengompres string:
"beep boop beer!"

Hitung frekuensi setiap karakter:

- 'b': 3
- 'e': 3
- 'o': 2
- 'p': 2
- ' ': 2
- 'r': 1
- '!': 1

Langkah-langkah:
1. Buat node karakter dan frekuensinya.
2. Masukkan ke priority queue.
3. Gabungkan dua node terendah:
- '!'+‘r’ → node 2
- node 2 + ‘o’ → node 4
- dan seterusnya...
4. Bangun pohon Huffman.
5. Dari pohon, hasilkan kode biner:
- contoh hasil:
'b': 10
'e': 00
'o': 111
'p': 110
'!': 0111
...
6. Gantilah setiap karakter dalam string dengan kodenya → data terkompresi.

## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <queue>
#include <unordered_map>
using namespace std;

struct Node {
    char ch;
    int freq;
    Node *left, *right;
    Node(char c, int f) : ch(c), freq(f), left(nullptr), right(nullptr) {}
};

struct compare {
    bool operator()(Node* l, Node* r) {
        return l->freq > r->freq;
    }
};

void printCodes(Node* root, string str, unordered_map<char, string>& huffmanCode) {
    if (!root) return;
    if (root->ch != '#') huffmanCode[root->ch] = str;
    printCodes(root->left, str + "0", huffmanCode);
    printCodes(root->right, str + "1", huffmanCode);
}

void huffmanCoding(string text) {
    unordered_map<char, int> freq;
    for (char ch : text) freq[ch]++;
    
    priority_queue<Node*, vector<Node*>, compare> pq;
    for (auto pair : freq) {
        pq.push(new Node(pair.first, pair.second));
    }

    while (pq.size() > 1) {
        Node *left = pq.top(); pq.pop();
        Node *right = pq.top(); pq.pop();
        Node *merged = new Node('#', left->freq + right->freq);
        merged->left = left;
        merged->right = right;
        pq.push(merged);
    }

    Node* root = pq.top();
    unordered_map<char, string> huffmanCode;
    printCodes(root, "", huffmanCode);

    cout << "Huffman Codes:\n";
    for (auto pair : huffmanCode)
        cout << pair.first << ": " << pair.second << endl;

    cout << "\nEncoded string:\n";
    for (char ch : text) cout << huffmanCode[ch];
    cout << endl;
}

int main() {
    string text = "beep boop beer!";
    huffmanCoding(text);
    return 0;
}

{% endraw %}
```

## Implementasi Dalam Kehidupan
Huffman Coding digunakan di banyak aplikasi kompresi data:
- File ZIP, GZIP, dan TAR
- JPEG (image compression)
- MP3 (audio compression)
- PNG (image, lossless)
- Compiler: Untuk mengoptimalkan representasi simbol

## Kelebihan dan Kekurangan
### Kelebihan:
1. Lossless compression: Data asli bisa dikembalikan 100%.
2. Efisien untuk data dengan banyak karakter berulang.
3. Kode prefix: Tidak ambigu saat decoding.
4. Struktur fleksibel dan optimal untuk distribusi frekuensi tidak merata.

### Kekurangan:
1. Overhead struktur pohon (harus dikirim bersama data).
2. Kurang efisien untuk data pendek atau frekuensi karakter yang mirip.
3. Tidak mendukung update dinamis (harus membangun ulang pohon untuk perubahan data besar).
4. Tidak ideal untuk data dengan karakter distribusi merata.

## Kesimpulan
Huffman Coding adalah algoritma yang sangat berguna untuk kompresi data lossless. Ia bekerja berdasarkan frekuensi karakter dan membentuk pohon biner optimal yang menghasilkan kode-kode pendek untuk karakter yang sering muncul. Cocok untuk aplikasi kompresi file seperti ZIP, JPEG, dan lainnya. Meskipun memiliki keterbatasan, efisiensi dan akurasinya menjadikannya salah satu algoritma klasik yang masih banyak digunakan hingga kini.