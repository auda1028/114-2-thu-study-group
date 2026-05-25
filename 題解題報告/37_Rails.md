# 37. Rails

## 題目

- 題目連結：<https://onlinejudge.org/external/5/514.pdf>
- 題意摘要：判斷目標車廂排列是否能透過一個中轉站 stack 形成。

## 參考程式與註解

```cpp
stack<int> st;
int next_in = 1, idx = 0;

while (next_in <= n) {
    st.push(next_in++);
    while (!st.empty() && st.top() == target[idx]) {
        st.pop();
        idx++;
    }
}
cout << (idx == n ? "Yes" : "No") << '\n';
```

## 解題觀念

本題重點：stack、queue、車站模擬

- 依序把 1..n 推入 stack。
- 每次 stack top 等於目標序列目前車廂時就 pop。
- 最後若所有目標都被取出，代表可行。

複雜度：O(n) 每組序列
