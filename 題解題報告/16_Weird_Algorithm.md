# 16. Weird Algorithm

## 題目

- 題目連結：<https://cses.fi/problemset/task/1068/>
- 題意摘要：從 n 開始，若為偶數除以 2，若為奇數乘 3 加 1，直到變成 1。

## 參考程式與註解

```cpp
long long n;
cin >> n;

while (true) {
    cout << n << ' ';
    if (n == 1) break;        // 到 1 就結束
    if (n % 2 == 0) n /= 2;   // 偶數規則
    else n = 3 * n + 1;       // 奇數規則
}
```

## 解題觀念

本題重點：Collatz 序列、while 模擬、long long

- 每一步只依照目前 n 的奇偶決定下一個狀態。
- 過程中數值可能暫時變大，因此使用 long long。
- 這題是練習 while 終止條件與連續輸出的基本模擬題。

複雜度：O(序列長度)
