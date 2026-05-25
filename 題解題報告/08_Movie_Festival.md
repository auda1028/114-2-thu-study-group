# 08. Movie Festival

## 題目

- 題目連結：<https://cses.fi/problemset/task/1629/>
- 題意摘要：給定多部電影的開始與結束時間，求最多可以完整看幾部。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vector<pair<int, int>> movies; // {end, start}
    for (int i = 0; i < n; i++) {
        int start, end;
        cin >> start >> end;
        movies.push_back({end, start});
    }

    sort(movies.begin(), movies.end());

    int last_end = 0;
    int ans = 0;
    for (auto [end, start] : movies) {
        if (start >= last_end) {
            // 這部電影與上一部不衝突，可以選。
            ans++;
            last_end = end;
        }
    }

    cout << ans << '\n';
    return 0;
}
```

## 解題觀念

本題重點：區間排程、依結束時間排序、貪心

- 將電影依結束時間由小到大排序。
- 每次選擇目前能看的、最早結束的電影。
- 越早結束，越不會影響後續選擇，因此是貪心最佳策略。

複雜度：O(n log n)
