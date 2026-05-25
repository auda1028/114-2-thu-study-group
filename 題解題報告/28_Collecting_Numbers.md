# 28. Collecting Numbers

## 題目

- 題目連結：<https://cses.fi/problemset/task/2216/>
- 題意摘要：依照原陣列位置收集 1 到 n，求需要幾輪。

## 參考程式與註解

```cpp
vector<int> pos(n + 1);
for (int i = 1; i <= n; i++) {
    int x;
    cin >> x;
    pos[x] = i;
}

int rounds = 1;
for (int x = 2; x <= n; x++) {
    if (pos[x] < pos[x - 1]) rounds++;
}
```

## 解題觀念

本題重點：位置陣列、斷點計數

- 記錄每個數字出現的位置 pos[value]。
- 若 pos[i] < pos[i-1]，代表新的一輪開始。
- 答案初始為 1，再加上所有斷點數量。

複雜度：O(n)
