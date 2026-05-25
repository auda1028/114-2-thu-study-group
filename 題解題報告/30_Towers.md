# 30. Towers

## 題目

- 題目連結：<https://cses.fi/problemset/task/1073/>
- 題意摘要：依序放方塊，每個方塊只能放在比它大的塔頂，求最少塔數。

## 參考程式與註解

```cpp
multiset<int> top;
for (int x : a) {
    auto it = top.upper_bound(x); // 第一個比 x 大的塔頂
    if (it != top.end()) top.erase(it);
    top.insert(x);
}
cout << top.size() << '\n';
```

## 解題觀念

本題重點：multiset、patience sorting

- 用 multiset 維護每座塔目前的塔頂。
- 對每個方塊找第一個大於它的塔頂。
- 若找到就替換塔頂，否則新增一座塔。

複雜度：O(n log n)
