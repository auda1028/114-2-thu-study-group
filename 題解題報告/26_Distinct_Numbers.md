# 26. Distinct Numbers

## 題目

- 題目連結：<https://cses.fi/problemset/task/1621/>
- 題意摘要：計算輸入的 n 個數中有幾個不同的值。

## 參考程式與註解

```cpp
set<int> s;
for (int i = 0; i < n; i++) {
    int x;
    cin >> x;
    s.insert(x); // 重複值不會增加大小
}
cout << s.size() << '\n';
```

## 解題觀念

本題重點：set 去重

- set 會自動去除重複元素。
- 全部插入後，set 大小就是不同數字數量。
- 也可排序後計算相鄰變化次數。

複雜度：O(n log n)
