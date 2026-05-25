# 27. Stick Lengths

## 題目

- 題目連結：<https://cses.fi/problemset/task/1074/>
- 題意摘要：把所有木棍調成同一長度，求最小總調整量。

## 參考程式與註解

```cpp
sort(a.begin(), a.end());
long long med = a[n / 2];
long long ans = 0;

for (long long x : a) {
    ans += llabs(x - med); // 往中位數靠攏
}
cout << ans << '\n';
```

## 解題觀念

本題重點：排序、中位數、絕對距離和

- 最小化絕對距離和時，最佳目標是中位數。
- 排序後取中間元素作為目標。
- 累加每個數與中位數的距離。

複雜度：O(n log n)
