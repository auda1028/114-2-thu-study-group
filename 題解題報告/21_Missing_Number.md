# 21. Missing Number

## 題目

- 題目連結：<https://cses.fi/problemset/task/1083/>
- 題意摘要：1 到 n 中缺少一個數，找出缺少的是哪一個。

## 參考程式與註解

```cpp
long long expected = 1LL * n * (n + 1) / 2;
long long actual = 0;

for (int i = 0; i < n - 1; i++) {
    long long x;
    cin >> x;
    actual += x;
}
cout << expected - actual << '\n';
```

## 解題觀念

本題重點：總和公式、缺漏值

- 完整總和為 n(n+1)/2。
- 讀入 n-1 個數並累加。
- 完整總和減去實際總和就是缺少的數。

複雜度：O(n)
