# 36. Rank the Languages

## 題目

- 題目連結：<https://onlinejudge.org/external/103/10336.pdf>
- 題意摘要：統計地圖上每種語言有幾個連通區域，並依數量排序。

## 參考程式與註解

```cpp
queue<pair<int,int>> q;
q.push({sx, sy});
vis[sx][sy] = true;

while (!q.empty()) {
    auto [x, y] = q.front(); q.pop();
    for (int d = 0; d < 4; d++) {
        int nx = x + dx[d], ny = y + dy[d];
        if (out(nx, ny) || vis[nx][ny]) continue;
        if (grid[nx][ny] != grid[sx][sy]) continue;
        vis[nx][ny] = true;
        q.push({nx, ny});
    }
}
```

## 解題觀念

本題重點：BFS / DSU、連通塊、排序輸出

- BFS 做法：從未訪問格子出發，把同字母連通區走完。
- DSU 做法：相鄰同字母格子 union，最後統計 root。
- 輸出要依數量降序、字母升序排序。

複雜度：O(RC log RC)
