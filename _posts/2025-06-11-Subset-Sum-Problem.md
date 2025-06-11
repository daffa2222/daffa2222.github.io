---
layout: post
title: "Subset Sum Problem"
date: 2025-06-10 10:00:00 +0800
categories: backtracking cpp
tags: [c++, backtracking]
---

## Apa itu Subset Sum Problemm?
Subset Sum Problem adalah salah satu masalah klasik dalam ilmu komputer dan teori himpunan. Diberikan sebuah himpunan bilangan bulat dan sebuah nilai target sum, masalahnya adalah menentukan apakah ada subhimpunan dari himpunan tersebut yang jumlah elemennya sama dengan sum.

Masalah ini tergolong NP-complete, dan menjadi dasar dari banyak problem kombinatorik lainnya, seperti Knapsack Problem.

## Prinsip Kerja
Secara umum, prinsip kerjanya adalah:
- Mengecek setiap kombinasi elemen dalam array untuk melihat apakah jumlahnya sama dengan sum.
- Ini dapat dilakukan dengan:
- Rekursi/backtracking: Mengeksplorasi semua subset.
- Dynamic Programming: Menyimpan hasil perhitungan untuk menghindari pengulangan.
-Pendekatan bitmasking (pada array kecil).

Strateginya adalah:
Untuk setiap elemen, kita punya dua pilihan:
- Gunakan elemen tersebut (kurangi sum).
- Lewatkan elemen tersebut (lanjut ke elemen berikutnya).
## Contoh Permasalahan
Masalah:
Diberikan array A = {3, 34, 4, 12, 5, 2} dan target sum = 9.
Apakah ada subset dari A yang jumlahnya 9?

Penyelesaian:
Coba subset:

- {3, 4, 2} → jumlah = 9 ✅
- {4, 5} → jumlah = 9 ✅
- {12} → jumlah = 12 ❌
- {34} → terlalu besar ❌

Jadi jawabannya: YA, subset seperti {4, 5} atau {3, 4, 2} valid.

## Implementasi (C++)
```
cpp
{% raw %}
#include <iostream>
#include <vector>
using namespace std;

bool isSubsetSum(vector<int>& arr, int sum) {
    int n = arr.size();
    vector<vector<bool>> dp(n+1, vector<bool>(sum+1, false));

    // Inisialisasi: sum = 0 bisa dicapai dengan subset kosong
    for (int i = 0; i <= n; i++)
        dp[i][0] = true;

    // Proses pengisian DP table
    for (int i = 1; i <= n; i++) {
        for (int s = 1; s <= sum; s++) {
            if (arr[i-1] > s)
                dp[i][s] = dp[i-1][s];
            else
                dp[i][s] = dp[i-1][s] || dp[i-1][s - arr[i-1]];
        }
    }

    return dp[n][sum];
}

int main() {
    vector<int> arr = {3, 34, 4, 12, 5, 2};
    int sum = 9;

    if (isSubsetSum(arr, sum))
        cout << "Terdapat subset dengan jumlah " << sum << endl;
    else
        cout << "Tidak ada subset dengan jumlah " << sum << endl;

    return 0;
}
{% endraw %}
```

## Implementasi Dalam Kehidupan
1. Kriptografi: Digunakan dalam algoritma knapsack-based encryption.
2. Perencanaan keuangan: Menentukan kombinasi aset yang mencapai target tertentu.
3. Manajemen sumber daya: Menentukan kombinasi sumber daya terbatas untuk memenuhi kebutuhan spesifik.
4. Pemecahan puzzle: Game dan aplikasi yang melibatkan pemilihan elemen dengan batasan jumlah.

## Kelebihan dan Kekurangan
### Kelebihan:
1. Konsep dasar yang sangat penting dalam pemrograman dinamis.
2. Relevan dengan banyak masalah nyata dan algoritma optimasi.
3. Solusi dinamis efisien untuk ukuran array dan sum yang kecil hingga sedang.

### Kekurangan:
1. Kompleksitas tinggi secara eksponensial pada pendekatan rekursif.
2. Pendekatan DP membutuhkan ruang memori O(n*sum).
3. Tidak optimal untuk kasus dengan elemen sangat besar atau sum tinggi.


## Kesimpulan
Subset Sum Problem adalah masalah penting dan fundamental dalam ilmu komputer. Ia menjadi basis untuk berbagai permasalahan lain seperti knapsack, partisi, dan optimasi kombinatorik. Meskipun memiliki kompleksitas tinggi, dengan pemrograman dinamis atau pendekatan heuristik, masalah ini bisa diselesaikan secara efisien pada ukuran input terbatas.

