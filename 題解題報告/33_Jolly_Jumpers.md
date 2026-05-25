# 33. Jolly Jumpers

## 題目

- 題目連結：<https://onlinejudge.org/external/100/10038.pdf>
- 題意摘要：判斷相鄰差的絕對值是否剛好包含 1 到 n-1。

## 參考程式與註解

```cpp
vector<bool> seen(n, false);
for (int i = 1; i < n; i++) {
    int diff = abs(a[i] - a[i - 1]);
    if (diff >= 1 && diff <= n - 1) seen[diff] = true;
}

bool ok = true;
for (int d = 1; d <= n - 1; d++) ok &= seen[d];
```

## 解題觀念

本題重點：差值集合、陣列標記

- 計算每對相鄰元素差的絕對值。
- 差值必須在 1 到 n-1 範圍內。
- 用 boolean 陣列標記出現過的差值。

複雜度：O(n)
