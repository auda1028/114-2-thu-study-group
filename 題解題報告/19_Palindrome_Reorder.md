# 19. Palindrome Reorder

## 題目

- 題目連結：<https://cses.fi/problemset/task/1755/>
- 題意摘要：重新排列字串，使其成為回文；若不可能則輸出 NO SOLUTION。

## 參考程式與註解

```cpp
vector<int> cnt(26);
for (char c : s) cnt[c - 'A']++;

int odd = 0, mid = -1;
for (int i = 0; i < 26; i++) {
    if (cnt[i] % 2) odd++, mid = i;
}
if (odd > 1) cout << "NO SOLUTION\n";

string left;
for (int i = 0; i < 26; i++) {
    left += string(cnt[i] / 2, char('A' + i));
}
string right = left;
reverse(right.begin(), right.end());
```

## 解題觀念

本題重點：字元頻率、回文建構

- 回文最多只能有一個字元出現奇數次。
- 每個字元一半放左邊，另一半反向放右邊。
- 奇數次字元放在中間。

複雜度：O(n + 26)
