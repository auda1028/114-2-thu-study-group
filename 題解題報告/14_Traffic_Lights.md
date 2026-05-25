# 14. Traffic Lights

## 題目

- 題目連結：<https://cses.fi/problemset/task/1163/>
- 題意摘要：在道路上依序加入紅綠燈，每次加入後輸出最長無紅綠燈區段。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int x, n;
    cin >> x >> n;

    set<int> lights = {0, x};
    multiset<int> lengths = {x};

    for (int i = 0; i < n; i++) {
        int p;
        cin >> p;

        // 找到 p 右邊第一個紅綠燈，以及左邊相鄰紅綠燈。
        auto right = lights.upper_bound(p);
        auto left = prev(right);

        // 原本 [left, right] 這段被切開，所以先刪掉舊長度。
        lengths.erase(lengths.find(*right - *left));
        lengths.insert(p - *left);
        lengths.insert(*right - p);
        lights.insert(p);

        cout << *lengths.rbegin() << ' ';
    }

    cout << '\n';
    return 0;
}
```

## 解題觀念

本題重點：set 維護切點、multiset 維護區段長度

- 用 set 存目前所有紅綠燈位置，方便找新位置左右鄰居。
- 用 multiset 存所有區段長度，方便取得最大長度。
- 插入新點時，原本一段 [l,r] 被拆成 [l,p] 與 [p,r]。

複雜度：O(n log n)
