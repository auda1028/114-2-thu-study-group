# 17. Repetitions

## 題目

- 題目連結：<https://cses.fi/problemset/task/1069/>
- 題意摘要：找 DNA 字串中同一字元連續出現的最大長度。

## 參考程式與註解

```cpp
string s;
cin >> s;

int best = 1, cur = 1;
for (int i = 1; i < (int)s.size(); i++) {
    if (s[i] == s[i - 1]) cur++; // 延續同一段
    else cur = 1;                // 換字元，重新計數
    best = max(best, cur);
}
cout << best << '\n';
```

## 解題觀念

本題重點：字串掃描、連續段長度

- 用 cur 記錄目前連續長度，best 記錄最大值。
- 若目前字元等於前一個，cur 加 1；否則重新從 1 開始。
- 整題只需線性掃描一次。

複雜度：O(n)
