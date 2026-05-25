# 22. Gray Code

## 題目

- 題目連結：<https://cses.fi/problemset/task/2205/>
- 題意摘要：輸出 n 位元 Gray code，使相鄰兩項只差一個 bit。

## 參考程式與註解

```cpp
for (int i = 0; i < (1 << n); i++) {
    int gray = i ^ (i >> 1); // Gray code 公式
    for (int b = n - 1; b >= 0; b--) {
        cout << ((gray >> b) & 1);
    }
    cout << '\n';
}
```

## 解題觀念

本題重點：位元運算、Gray code、bitset

- 第 i 個 Gray code 可由 i ^ (i >> 1) 得到。
- 輸出時要補滿 n 位。
- 這題練習位元運算和二進位表示。

複雜度：O(n * 2^n)
