# 25. Number Spiral

## 題目

- 題目連結：<https://cses.fi/problemset/task/1071/>
- 題意摘要：給定座標 (y,x)，求 number spiral 上的值。

## 參考程式與註解

```cpp
long long layer = max(x, y);
long long base = layer * layer;
long long ans;

if (layer % 2 == 0) {
    // 偶數層方向與奇數層相反
    ans = (y == layer) ? base - x + 1 : (layer - 1) * (layer - 1) + y;
} else {
    ans = (x == layer) ? base - y + 1 : (layer - 1) * (layer - 1) + x;
}
```

## 解題觀念

本題重點：座標規律、奇偶層公式

- 所在層數為 max(x, y)。
- 每一層最大值是 layer^2。
- 依 layer 奇偶決定方向，再用座標推回答案。

複雜度：O(1) 每筆查詢
