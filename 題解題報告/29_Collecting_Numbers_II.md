# 29. Collecting Numbers II

## 題目

- 題目連結：<https://cses.fi/problemset/task/2217/>
- 題意摘要：每次交換兩個位置後，快速更新 Collecting Numbers 的輪數。

## 參考程式與註解

```cpp
auto bad = [&](int x) {
    if (x < 1 || x >= n) return 0;
    return pos[x] > pos[x + 1]; // x 和 x+1 跨輪
};

set<int> affected = {a[i] - 1, a[i], a[j] - 1, a[j]};
for (int x : affected) rounds -= bad(x);

swap(a[i], a[j]);
pos[a[i]] = i;
pos[a[j]] = j;

for (int x : affected) rounds += bad(x);
```

## 解題觀念

本題重點：swap 後局部更新、斷點維護

- 輪數取決於相鄰數字 pair (x-1,x) 的位置順序。
- 交換兩個數只會影響它們附近的 pair。
- 用 set 收集受影響 pair，先扣舊貢獻，交換後再加新貢獻。

複雜度：O(log n) 或 O(1) 級別局部更新
