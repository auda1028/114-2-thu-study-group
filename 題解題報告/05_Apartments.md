# 05. Apartments

## 題目

- 題目連結：<https://cses.fi/problemset/task/1084/>
- 題意摘要：申請者有理想房間大小，房間大小若落在可接受誤差內就能分配，求最多配對數。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m;
    long long k;
    cin >> n >> m >> k;

    vector<long long> want(n), house(m);
    for (auto &x : want) cin >> x;
    for (auto &x : house) cin >> x;

    sort(want.begin(), want.end());
    sort(house.begin(), house.end());

    int i = 0, j = 0, ans = 0;
    while (i < n && j < m) {
        if (abs(want[i] - house[j]) <= k) {
            // 目前申請者可以接受目前房間，完成一組配對。
            ans++;
            i++;
            j++;
        } else if (house[j] < want[i] - k) {
            // 房間太小，不可能給後面的申請者，換下一間。
            j++;
        } else {
            // 房間太大，目前申請者無法接受，換下一位申請者。
            i++;
        }
    }

    cout << ans << '\n';
    return 0;
}
```

## 解題觀念

本題重點：排序、雙指針、貪心配對

- 將申請者需求與房間大小都排序。
- 若目前房間太小，換下一間房；若目前房間太大，換下一位申請者。
- 若大小差距在 k 內就配對，兩邊指針都往後。

複雜度：O(n log n + m log m)
