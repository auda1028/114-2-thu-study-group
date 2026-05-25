# 09. Sum of Two Values

## 題目

- 題目連結：<https://cses.fi/problemset/task/1640/>
- 題意摘要：在陣列中找兩個不同位置，使兩個值相加等於目標 x。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    long long target;
    cin >> n >> target;

    vector<pair<long long, int>> a;
    for (int i = 1; i <= n; i++) {
        long long x;
        cin >> x;
        a.push_back({x, i}); // 同時記錄原始位置。
    }

    sort(a.begin(), a.end());

    int l = 0, r = n - 1;
    while (l < r) {
        long long sum = a[l].first + a[r].first;
        if (sum == target) {
            cout << a[l].second << ' ' << a[r].second << '\n';
            return 0;
        } else if (sum < target) {
            l++;
        } else {
            r--;
        }
    }

    cout << "IMPOSSIBLE\n";
    return 0;
}
```

## 解題觀念

本題重點：排序、雙指針、保留原始索引

- 排序後用左右指針檢查目前和。
- 若和太小，左指針右移；若和太大，右指針左移。
- 因為輸出要原始位置，所以排序前要把 index 一起存下來。

複雜度：O(n log n)
