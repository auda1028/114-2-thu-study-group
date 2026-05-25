# 18. Two Sets

## 題目

- 題目連結：<https://cses.fi/problemset/task/1092/>
- 題意摘要：將 1 到 n 分成兩組，使兩組總和相同。

## 參考程式與註解

```cpp
long long sum = 1LL * n * (n + 1) / 2;
if (sum % 2) {
    cout << "NO\n";
    return;
}

long long need = sum / 2;
vector<int> a, b;
for (int x = n; x >= 1; x--) {
    if (need >= x) {       // 優先把大數放進第一組
        a.push_back(x);
        need -= x;
    } else {
        b.push_back(x);
    }
}
```

## 解題觀念

本題重點：等差級數、奇偶判斷、建構法

- 總和 n(n+1)/2 若為奇數就不可能。
- 可從大到小貪心，把數字放入目前需要補足的那一組。
- 重點是先判斷可行性，再建構其中一組。

複雜度：O(n)
