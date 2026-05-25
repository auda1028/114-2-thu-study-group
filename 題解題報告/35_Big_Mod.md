# 35. Big Mod

## 題目

- 題目連結：<https://onlinejudge.org/external/3/374.pdf>
- 題意摘要：計算 b^p mod m。

## 參考程式與註解

```cpp
long long mod_pow(long long b, long long p, long long m) {
    long long res = 1 % m;
    b %= m;
    while (p > 0) {
        if (p & 1) res = res * b % m;
        b = b * b % m;
        p >>= 1;
    }
    return res;
}
```

## 解題觀念

本題重點：快速冪、模運算

- 用二分冪將指數運算降為 O(log p)。
- 每次乘法後取模，避免溢位擴大。
- 遞迴或迭代都可以。

複雜度：O(log p)
