# 10. Maximum Subarray Sum

## 題目

- 題目連結：<https://cses.fi/problemset/task/1643/>
- 題意摘要：在陣列中找一段非空連續子陣列，使總和最大。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    long long cur = 0;
    long long best = LLONG_MIN;

    for (int i = 0; i < n; i++) {
        long long x;
        cin >> x;

        // 要嘛延續前面的子陣列，要嘛從目前 x 重新開始。
        cur = max(x, cur + x);
        best = max(best, cur);
    }

    cout << best << '\n';
    return 0;
}
```

## 解題觀念

本題重點：Kadane 演算法、動態維護最佳連續區間

- cur 表示「以目前位置結尾」的最大子陣列和。
- 對每個 x，選擇重新從 x 開始，或接在前一段後面。
- best 記錄所有 cur 中的最大值。

複雜度：O(n)
