# 06. Ferris Wheel

## 題目

- 題目連結：<https://cses.fi/problemset/task/1090/>
- 題意摘要：每台車最多坐兩人且有重量限制，求最少需要幾台車。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    long long limit;
    cin >> n >> limit;

    vector<long long> w(n);
    for (auto &x : w) cin >> x;
    sort(w.begin(), w.end());

    int l = 0, r = n - 1;
    int gondolas = 0;

    while (l <= r) {
        // 每一輪一定安排目前最重的人 w[r]。
        if (w[l] + w[r] <= limit) {
            // 若最輕的人可以一起坐，就順便配掉。
            l++;
        }
        r--;
        gondolas++;
    }

    cout << gondolas << '\n';
    return 0;
}
```

## 解題觀念

本題重點：排序、雙指針、貪心

- 先排序體重。
- 每次處理最重的小孩，若能和最輕的小孩同坐就配對。
- 如果最重與最輕都不能同坐，最重者只能自己坐一台。

複雜度：O(n log n)
