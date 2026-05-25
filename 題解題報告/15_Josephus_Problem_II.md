# 15. Josephus Problem II

## 題目

- 題目連結：<https://cses.fi/problemset/task/2163/>
- 題意摘要：n 個小孩圍成一圈，每次跳過 k 個後淘汰一人，輸出完整淘汰順序。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

struct Fenwick {
    int n;
    vector<int> bit;

    Fenwick(int n) : n(n), bit(n + 1, 0) {}

    void add(int idx, int value) {
        for (; idx <= n; idx += idx & -idx) {
            bit[idx] += value;
        }
    }

    int sum(int idx) const {
        int res = 0;
        for (; idx > 0; idx -= idx & -idx) {
            res += bit[idx];
        }
        return res;
    }

    int kth(int k) const {
        int pos = 0;
        // jump 從足夠大的 2 的冪開始，逐步試探答案位置。
        for (int jump = 1 << 20; jump > 0; jump >>= 1) {
            if (pos + jump <= n && bit[pos + jump] < k) {
                k -= bit[pos + jump];
                pos += jump;
            }
        }
        return pos + 1;
    }
};

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    long long k;
    cin >> n >> k;

    Fenwick fw(n);
    for (int i = 1; i <= n; i++) {
        fw.add(i, 1); // 一開始每個人都存活。
    }

    long long current = 0;
    for (int alive = n; alive >= 1; alive--) {
        // current 是目前圈中 0-based 的淘汰位置。
        current = (current + k) % alive;

        int removed = fw.kth((int)current + 1);
        cout << removed << ' ';
        fw.add(removed, -1); // 淘汰後不再存活。
    }

    cout << '\n';
    return 0;
}
```

## 解題觀念

本題重點：Fenwick Tree、order statistic、第 k 個存活者

- 把仍存活的人記為 1，已淘汰的人記為 0。
- Fenwick Tree 可維護目前每個位置是否存活，並查詢前綴存活數。
- 用 kth 找目前第 cur+1 個存活者的位置，淘汰後將該位置加上 -1。

複雜度：O(n log n)
