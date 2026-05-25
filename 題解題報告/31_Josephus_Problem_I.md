# 31. Josephus Problem I

## 題目

- 題目連結：<https://cses.fi/problemset/task/2162/>
- 題意摘要：n 個小孩圍成一圈，每次跳過一人並淘汰下一人，輸出淘汰順序。

## 參考程式與註解

```cpp
queue<int> q;
for (int i = 1; i <= n; i++) q.push(i);

while (!q.empty()) {
    q.push(q.front()); // 跳過的人移到隊尾
    q.pop();

    cout << q.front() << ' '; // 淘汰下一人
    q.pop();
}
```

## 解題觀念

本題重點：queue、循環淘汰模擬

- queue 適合模擬環狀隊伍。
- 先把跳過的人丟到隊尾，再淘汰隊首。
- 每個人進出 queue 常數次。

複雜度：O(n)
