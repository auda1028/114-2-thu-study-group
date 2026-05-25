# 07. Restaurant Customers

## 題目

- 題目連結：<https://cses.fi/problemset/task/1619/>
- 題意摘要：給定每位客人的進出時間，求餐廳同時最多有幾位客人。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vector<pair<int, int>> events;
    for (int i = 0; i < n; i++) {
        int arrive, leave;
        cin >> arrive >> leave;
        events.push_back({arrive, +1});
        events.push_back({leave, -1});
    }

    sort(events.begin(), events.end());

    int current = 0, best = 0;
    for (auto [time, delta] : events) {
        current += delta;
        best = max(best, current);
    }

    cout << best << '\n';
    return 0;
}
```

## 解題觀念

本題重點：掃描線、事件排序

- 把到達時間轉成 +1 事件，離開時間轉成 -1 事件。
- 依時間排序後從左到右累加目前人數。
- 累加過程中的最大值就是答案。

複雜度：O(n log n)
