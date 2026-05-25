# 32. Parentheses Balance

## 題目

- 題目連結：<https://onlinejudge.org/external/6/673.pdf>
- 題意摘要：判斷每行括號字串是否平衡。

## 參考程式與註解

```cpp
stack<char> st;
bool ok = true;

for (char c : s) {
    if (c == '(' || c == '[') st.push(c);
    else {
        if (st.empty()) { ok = false; break; }
        char t = st.top(); st.pop();
        if ((c == ')' && t != '(') || (c == ']' && t != '[')) ok = false;
    }
}
ok = ok && st.empty();
```

## 解題觀念

本題重點：stack、括號匹配

- 左括號入 stack，右括號檢查 stack top 是否對應。
- 遇到空 stack 或型態不合就失敗。
- 最後 stack 必須為空。

複雜度：O(n)
