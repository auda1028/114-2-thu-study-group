# 23. Increasing Array

## 題目

- 題目連結：<https://cses.fi/problemset/task/1094/>
- 題意摘要：每次可把某元素加 1，求使陣列非遞減的最少操作數。

## 參考程式與註解

```cpp
long long ans = 0;
long long prev;
cin >> prev;

for (int i = 1; i < n; i++) {
    long long x;
    cin >> x;
    if (x < prev) ans += prev - x; // 補到 prev
    else prev = x;                 // 更新目前最大值
}
```

## 解題觀念

本題重點：貪心、單調序列、累加補值

- 從左到右掃描，維護目前至少需要達到的值。
- 若 a[i] 小於前一個值，就補到前一個值。
- 每一步做最小必要調整就是全域最小。

複雜度：O(n)
