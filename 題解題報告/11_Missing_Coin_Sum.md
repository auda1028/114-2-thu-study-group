# 11. Missing Coin Sum

## 題目

- 題目連結：<https://cses.fi/problemset/task/2183/>
- 題意摘要：給定一些硬幣面額，求無法用子集合湊出的最小正整數。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vector<long long> coins(n);
    for (auto &x : coins) cin >> x;
    sort(coins.begin(), coins.end());

    long long reach = 0; // 目前可以湊出 [1, reach]。
    for (long long x : coins) {
        if (x > reach + 1) break;
        reach += x;
    }

    cout << reach + 1 << '\n';
    return 0;
}
```

## 解題觀念

本題重點：排序、貪心、可表示區間

- 排序硬幣後，維護目前已能表示 [1, reach] 的所有金額。
- 若下一枚硬幣 x <= reach + 1，則可表示範圍延伸到 reach + x。
- 若 x > reach + 1，代表 reach + 1 無法被湊出，就是答案。

複雜度：O(n log n)
