# 20. Trailing Zeros

## 題目

- 題目連結：<https://cses.fi/problemset/task/1618/>
- 題意摘要：計算 n! 的尾端有幾個 0。

## 參考程式與註解

```cpp
long long ans = 0;
for (long long p = 5; p <= n; p *= 5) {
    ans += n / p; // 貢獻一個或多個因數 5
}
cout << ans << '\n';
```

## 解題觀念

本題重點：階乘、質因數 5、數學計數

- 尾端 0 來自 10 = 2 * 5。
- 階乘中 2 的數量遠多於 5，所以只要數 5 的數量。
- n/5 + n/25 + n/125 ... 就是答案。

複雜度：O(log n)
