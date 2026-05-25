# 24. Permutations

## 題目

- 題目連結：<https://cses.fi/problemset/task/1070/>
- 題意摘要：排列 1 到 n，使任兩相鄰數的差都不是 1。

## 參考程式與註解

```cpp
if (n == 2 || n == 3) {
    cout << "NO SOLUTION\n";
} else {
    for (int i = 2; i <= n; i += 2) cout << i << ' ';
    for (int i = 1; i <= n; i += 2) cout << i << ' ';
}
```

## 解題觀念

本題重點：建構法、奇偶分組

- n=2 或 n=3 無解。
- 可先輸出偶數，再輸出奇數。
- 奇偶分組可避免大多數相鄰差為 1 的情況。

複雜度：O(n)
