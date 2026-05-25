# 04. Static Range Sum Queries

## 題目

- 題目連結：<https://cses.fi/problemset/task/1646/>
- 題意摘要：給定陣列與多次 [a,b] 查詢，快速回答區間總和。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, q;
    cin >> n >> q;

    vector<long long> pref(n + 1, 0);
    for (int i = 1; i <= n; i++) {
        long long x;
        cin >> x;
        // pref[i] 代表第 1 個到第 i 個數字的總和。
        pref[i] = pref[i - 1] + x;
    }

    while (q--) {
        int l, r;
        cin >> l >> r;
        // [l, r] = 前 r 個總和 - 前 l-1 個總和。
        cout << pref[r] - pref[l - 1] << '\n';
    }

    return 0;
}
```

## 解題觀念

本題重點：前綴和、區間查詢

- 建立 pref[i] = 前 i 個數字的總和。
- 區間 [l,r] 的和可由 pref[r] - pref[l-1] 得到。
- 預處理一次後，每個查詢都能 O(1) 回答。

複雜度：預處理 O(n)，每次查詢 O(1)
