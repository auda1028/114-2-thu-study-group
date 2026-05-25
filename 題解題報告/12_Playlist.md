# 12. Playlist

## 題目

- 題目連結：<https://cses.fi/problemset/task/1141/>
- 題意摘要：給定歌曲序列，求最長的連續片段，使其中每首歌都不重複。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    cin >> n;

    vector<int> song(n);
    for (auto &x : song) cin >> x;

    map<int, int> last_seen;
    int left = 0;
    int ans = 0;

    for (int right = 0; right < n; right++) {
        int id = song[right];

        // 若這首歌在目前視窗內出現過，就把左界跳過上一次的位置。
        if (last_seen.count(id) && last_seen[id] >= left) {
            left = last_seen[id] + 1;
        }

        last_seen[id] = right;
        ans = max(ans, right - left + 1);
    }

    cout << ans << '\n';
    return 0;
}
```

## 解題觀念

本題重點：滑動視窗、map 記錄最後出現位置

- 用 l 表示目前不重複區間的左端。
- 走到 r 時，如果歌曲以前在區間內出現過，就把 l 移到上次位置的下一格。
- 每一步用 r-l+1 更新答案。

複雜度：O(n log n)，若用 unordered_map 平均可接近 O(n)
