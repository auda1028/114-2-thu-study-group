# 13. Concert Tickets

## 題目

- 題目連結：<https://cses.fi/problemset/task/1091/>
- 題意摘要：每位顧客有最高可接受票價，要賣給他不超過預算且最接近預算的票。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m;
    cin >> n >> m;

    multiset<int> tickets;
    for (int i = 0; i < n; i++) {
        int price;
        cin >> price;
        tickets.insert(price);
    }

    while (m--) {
        int budget;
        cin >> budget;

        // 第一張大於 budget 的票；答案要在它前面。
        auto it = tickets.upper_bound(budget);
        if (it == tickets.begin()) {
            cout << -1 << '\n';
        } else {
            --it;
            cout << *it << '\n';
            tickets.erase(it);
        }
    }

    return 0;
}
```

## 解題觀念

本題重點：multiset、upper_bound、前驅查詢

- 票價可能重複，所以使用 multiset。
- `upper_bound(x)` 找到第一個大於 x 的票，往前一格就是不超過 x 的最大票價。
- 票賣出後要從 multiset 中刪掉該張票。

複雜度：O((n+m) log n)
