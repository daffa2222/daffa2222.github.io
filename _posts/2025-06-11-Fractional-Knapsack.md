---
layout: post
title: "Fractional Knapsack"
date: 2025-06-11 10:00:00 +0800
categories: greedy cpp
tags: [c++, greedy]
---

## Apa itu Fractional Knapsack?
Fractional Knapsack adalah varian dari masalah Knapsack (Ransel) di mana kita boleh mengambil sebagian (fraksi) dari suatu item. Tujuannya adalah memaksimalkan nilai total dari item-item yang dimasukkan ke dalam knapsack (tas) yang memiliki batasan kapasitas berat tertentu.

Berbeda dengan 0/1 Knapsack yang mengharuskan kita mengambil seluruh item atau tidak sama sekali, dalam fractional knapsack kita bisa mengambil sebagian dari item, misalnya setengah atau sepertiga dari berat suatu item.

## Prinsip Kerja
Fractional Knapsack diselesaikan menggunakan algoritma greedy, berdasarkan nilai per satuan berat (value/weight) dari tiap item.

Langkah-langkah:
1. Hitung value/weight untuk semua item.
2. Urutkan item berdasarkan value/weight dari yang tertinggi ke terendah.
3. Masukkan item ke dalam knapsack dari yang memiliki value/weight tertinggi:
- Jika item bisa masuk sepenuhnya, ambil seluruhnya.
- Jika tidak, ambil sebagian sesuai sisa kapasitas.
4. Ulangi sampai kapasitas knapsack habis.

## Contoh Permasalahan
Kapasitas tas: 50 kg
Barang:
- 10 kg, nilai 60 (6 poin/kg)
- 20 kg, nilai 100 (5 poin/kg)
- 30 kg, nilai 120 (4 poin/kg)

Langkah:
- Ambil seluruh barang 1 → sisa 40 kg → nilai 60
- Ambil seluruh barang 2 → sisa 20 kg → tambah nilai 100
- Ambil 20 kg dari barang 3 (2/3 bagian) → tambah nilai 80
Total nilai: 60 + 100 + 80 = 240

## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Item {
    int value, weight;
    
    // constructor
    Item(int v, int w) : value(v), weight(w) {}
};

// Perbandingan berdasarkan value/weight
bool cmp(Item a, Item b) {
    double r1 = (double)a.value / a.weight;
    double r2 = (double)b.value / b.weight;
    return r1 > r2;
}

double fractionalKnapsack(int capacity, vector<Item>& items) {
    sort(items.begin(), items.end(), cmp);
    
    double totalValue = 0.0;
    
    for (Item item : items) {
        if (capacity >= item.weight) {
            capacity -= item.weight;
            totalValue += item.value;
        } else {
            totalValue += item.value * ((double)capacity / item.weight);
            break;
        }
    }
    
    return totalValue;
}

int main() {
    vector<Item> items = {{60, 10}, {100, 20}, {120, 30}};
    int capacity = 50;

    double maxValue = fractionalKnapsack(capacity, items);
    cout << "Nilai maksimum yang dapat dibawa: " << maxValue << endl;

    return 0;
}

{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Transportasi dan Logistik: Mengangkut sebagian muatan ketika truk/kapal sudah mencapai batas kapasitas.
2. Penyimpanan data atau cache: Memilih potongan data yang paling bernilai untuk dimuat dalam ruang terbatas.
3. Distribusi sumber daya: Seperti bahan makanan, energi, atau obat yang bisa dibagi-bagi untuk memaksimalkan efisiensi.
4. Manajemen portofolio investasi: Mengalokasikan dana ke berbagai aset berdasarkan rasio return/risiko (seperti value/weight).

## Kelebihan dan Kekurangan
### Kelebihan:
1. Cepat dan efisien: Kompleksitas waktu O(n log n) karena pengurutan.
2. Hasil optimal: Karena sifat greedy sesuai dengan struktur fractional.
3. Sederhana untuk diimplementasikan.
4. Cocok untuk kasus nyata di mana barang bisa dibagi.

### Kekurangan:
1. Tidak bisa digunakan untuk masalah 0/1 Knapsack (barang tidak dapat dibagi).
2. Tidak mencerminkan semua kondisi nyata (misalnya jika barang tidak bisa dibagi seperti laptop atau kursi).
3. Tidak dapat digunakan jika ada keterbatasan integritas atau ko

## Kesimpulan
Fractional Knapsack adalah solusi optimal untuk masalah pemilihan item dengan batas kapasitas ketika setiap item bisa dibagi. Pendekatan greedy dengan memilih item berdasarkan rasio nilai terhadap berat membuatnya sangat efisien dan cocok untuk berbagai kasus nyata yang menuntut efisiensi dan fleksibilitas. Namun, untuk masalah di mana barang tidak bisa dibagi, pendekatan ini tidak relevan, dan kita harus menggunakan algoritma lain seperti 0/1 Knapsack (Dynamic Programming).

