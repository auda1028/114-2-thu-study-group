# 34. Hardwood Species

## 題目

- 題目連結：<https://onlinejudge.org/external/102/10226.pdf>
- 題意摘要：統計每種樹名出現比例，依字典序輸出。

## 參考程式與註解

```cpp
map<string, int> cnt;
string name;
int total = 0;

while (getline(cin, name) && name != "") {
    cnt[name]++;
    total++;
}

for (auto [tree, c] : cnt) {
    cout << tree << ' ' << fixed << setprecision(4)
         << 100.0 * c / total << '\n';
}
```

## 解題觀念

本題重點：map 統計、百分比輸出

- 樹名包含空白風險低，但需要用 getline 讀整行。
- map 會依 key 字典序排序。
- 比例為 count / total * 100，通常需固定小數。

複雜度：O(n log n)
