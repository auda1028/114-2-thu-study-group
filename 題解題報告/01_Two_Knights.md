# 01. Two Knights

## 題目

- 題目連結：<https://cses.fi/problemset/task/1072/>
- 題意摘要：對每個 k x k 棋盤，計算放兩隻騎士且互不攻擊的方法數。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    long long n;
    cin >> n;

    for (long long k = 1; k <= n; k++) {
        // total: 從 k*k 個格子中挑兩格放騎士。
        long long total = (k * k) * (k * k - 1) / 2;

        // attack: 所有 2x3 / 3x2 小矩形中的互攻騎士組合。
        long long attack = 4 * (k - 1) * (k - 2);

        cout << total - attack << '\n';
    }

    return 0;
}
```

## 解題觀念

本題重點：組合數、數學公式、棋盤攻擊位置扣除

- 全部放法是從 k^2 個格子選 2 格，也就是 k^2 * (k^2 - 1) / 2。
- 會互相攻擊的情況只會出現在 2 x 3 或 3 x 2 的矩形中，每個矩形有 2 組攻擊方式。
- 攻擊組數可化成 4 * (k - 1) * (k - 2)，答案就是全部放法扣掉攻擊放法。

複雜度：O(n)
