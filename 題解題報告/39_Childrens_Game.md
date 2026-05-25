# 39. Children's Game

## 題目

- 題目連結：<https://onlinejudge.org/external/109/10905.pdf>
- 題意摘要：排列一組數字字串，使拼接後的整體數字最大。

## 參考程式與註解

```cpp
bool cmp(const string& a, const string& b) {
    return a + b > b + a; // 誰放前面能讓拼接結果更大
}

sort(v.begin(), v.end(), cmp);
for (string s : v) cout << s;
cout << '\n';
```

## 解題觀念

本題重點：自訂排序、字串拼接最大化

- 不能只按字典序或長度排序。
- 比較 a+b 與 b+a，決定誰應該放前面。
- 排序後依序輸出即可。

複雜度：O(n log n * 字串長度)
