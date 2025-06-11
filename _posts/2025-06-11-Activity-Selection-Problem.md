---
layout: post
title: "Activity Selection Problem"
date: 2025-06-11 10:00:00 +0800
categories: greedy cpp
tags: [c++, greedy]
---

## Apa itu Activity Selection Problem?
Activity Selection Problem (Masalah Pemilihan Aktivitas) adalah masalah optimasi klasik dalam ilmu komputer, khususnya dalam algoritma greedy (serakah). Masalah ini bertujuan untuk memilih jumlah maksimum aktivitas yang saling tidak tumpang tindih (non-overlapping) dari satu set aktivitas yang memiliki waktu mulai dan waktu selesai.

Tujuan:
Memaksimalkan jumlah aktivitas yang dapat dilakukan oleh seseorang atau satu sumber daya tanpa adanya benturan waktu antara aktivitas satu dan lainnya.

## Prinsip Kerja
Masalah ini diselesaikan menggunakan Greedy Algorithm, yaitu dengan selalu memilih aktivitas yang selesai paling awal terlebih dahulu. Strategi ini digunakan karena aktivitas yang selesai lebih cepat akan memberi lebih banyak ruang waktu bagi aktivitas-aktivitas berikutnya.

Langkah-langkah greedy:
1. Urutkan aktivitas berdasarkan waktu selesai (end time).
2. Pilih aktivitas pertama (dengan waktu selesai paling cepat).
3. Bandingkan aktivitas berikutnya, jika waktu mulainya ≥ waktu selesai aktivitas sebelumnya, maka pilih.
4. Ulangi sampai akhir..

## Contoh Permasalahan
Bayangkan kamu adalah seorang koordinator acara di sebuah gedung serbaguna. Dalam satu hari, banyak komunitas ingin menyewa gedung tersebut untuk kegiatan mereka. Namun, karena hanya ada satu ruangan, kamu harus memilih jadwal kegiatan yang tidak saling tumpang tindih agar sebanyak mungkin komunitas bisa menggunakan ruangan itu.

Ada enam komunitas yang mengajukan permintaan dengan jadwal sebagai berikut:
- Komunitas A ingin menggunakan ruangan dari pukul 1 sampai 3
- Komunitas B dari pukul 0 sampai 4
- Komunitas C dari pukul 5 sampai 9
- Komunitas D dari pukul 5 sampai 7
- Komunitas E dari pukul 8 sampai 9
- Komunitas F dari pukul 2 sampai 6
Tugas kamu adalah memilih sebanyak mungkin komunitas yang bisa menggunakan ruangan tanpa ada jadwal yang bertabrakan.
### Langkah Penyelesaian

1. Urutkan berdasarkan waktu selesai: A1(3), A2(4), A6(6), A4(7), A3(9), A5(9)
2. Pilih A1 → selesai pukul 3
3. A2 dimulai sebelum A1 selesai → lewati
4. A6 dimulai pukul 2 < 3 → lewati
5. A4 dimulai pukul 5 ≥ 3 → pilih
6. A3 dimulai pukul 5 < 7 → lewati
7. A5 dimulai pukul 8 ≥ 7 → pilih

Aktivitas Terpilih: A1, A4, A5

## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Activity {
    int start, end;
};

// Comparator untuk sorting berdasarkan waktu selesai
bool compare(Activity a, Activity b) {
    return a.end < b.end;
}

void selectActivities(vector<Activity>& activities) {
    sort(activities.begin(), activities.end(), compare);
    
    cout << "Aktivitas yang dipilih:\n";
    int lastEnd = -1;
    
    for (auto act : activities) {
        if (act.start >= lastEnd) {
            cout << "Mulai: " << act.start << ", Selesai: " << act.end << "\n";
            lastEnd = act.end;
        }
    }
}

int main() {
    vector<Activity> activities = {
        {1, 4}, {3, 5}, {0, 6}, {5, 7}, {8, 9}, {5, 9}
    };
    
    selectActivities(activities);
    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Penjadwalan Ruang Rapat: Memilih jadwal rapat yang tidak tumpang tindih untuk ruangan terbatas.
2. Penjadwalan Mesin Produksi: Mengatur urutan kerja mesin dengan waktu penggunaan minimum tanpa konflik.
3. Penyiaran Acara Televisi: Menentukan siaran mana yang akan ditayangkan tanpa tumpang tindih.
4. Reservasi Kamar Hotel/Studio: Menyusun jadwal seefisien mungkin agar bisa menerima lebih banyak klien.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Efisien (kompleksitas waktu O(n log n) setelah sorting)
2. Mudah diimplementasikan
3. Cocok untuk kasus penjadwalan real-time

### Kekurangan:
1. Tidak selalu menghasilkan solusi optimal jika masalah dimodifikasi (misalnya ada bobot/profit di tiap aktivitas).
2. Terbatas pada kasus tanpa konflik (aktivitas saling bebas).

## Kesimpulan
Activity Selection Problem adalah contoh klasik penggunaan greedy algorithm dalam dunia komputasi. Dengan memilih aktivitas yang selesai paling awal, kita dapat mengatur penjadwalan secara efisien dan optimal dalam banyak situasi nyata yang hanya melibatkan satu sumber daya. Meskipun memiliki keterbatasan, pendekatan ini tetap menjadi solusi cepat dan akurat untuk banyak jenis masalah penjadwalan dasar.