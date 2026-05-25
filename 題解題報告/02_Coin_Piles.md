# 02. Coin Piles

## 題目

- 題目連結：<https://cses.fi/problemset/task/1754/>
- 題意摘要：每次可從兩堆硬幣中取出 (1,2) 或 (2,1)，判斷是否能剛好清空兩堆。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;
    while (t--) {
        long long a, b;
        cin >> a >> b;

        long long small = min(a, b);
        long long large = max(a, b);

        // 條件 1: 每次移除 3 枚，所以總數要是 3 的倍數。
        // 條件 2: 每次最多從同一堆拿 2 枚，較大堆不能大於較小堆兩倍。
        if ((a + b) % 3 == 0 && large <= 2 * small) {
            cout << "YES\n";
        } else {
            cout << "NO\n";
        }
    }

    return 0;
}
```

## 解題觀念

本題重點：數學不變量、整除條件、最大值限制

- 每一步都會拿掉 3 枚硬幣，因此 a + b 必須能被 3 整除。
- 每一步最多只會從同一堆拿 2 枚，因此較大的那堆不能超過較小那堆的 2 倍。
- 兩個條件同時成立時，就能用兩種操作組合清空。

複雜度：O(t)
