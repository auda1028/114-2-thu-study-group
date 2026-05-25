# 03. Bit Strings

## 題目

- 題目連結：<https://cses.fi/problemset/task/1617/>
- 題意摘要：計算長度為 n 的 0/1 字串數量，也就是 2^n，並對 1e9+7 取模。

## 參考程式與註解

```cpp
#include <bits/stdc++.h>
using namespace std;

const long long MOD = 1000000007;

long long mod_pow(long long base, long long exp) {
    long long ans = 1;
    base %= MOD;

    while (exp > 0) {
        // 若目前二進位位元是 1，就把這一份 base 乘進答案。
        if (exp & 1) ans = ans * base % MOD;

        // base 變成 base^2，指數往右移一位。
        base = base * base % MOD;
        exp >>= 1;
    }
    return ans;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    long long n;
    cin >> n;
    cout << mod_pow(2, n) << '\n';

    return 0;
}
```

## 解題觀念

本題重點：快速冪、模運算

- 每個位置有 0 或 1 兩種選擇，所以答案為 2^n。
- n 可到 10^6，直接乘也可以，但快速冪更通用。
- 用二進位拆指數，每次平方並取模，避免溢位與大數。

複雜度：O(log n)
