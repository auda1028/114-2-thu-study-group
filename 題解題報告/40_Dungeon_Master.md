# 40. Dungeon Master

## 題目

- 題目連結：<https://onlinejudge.org/external/5/532.pdf>
- 題意摘要：在 L x R x C 的三維地牢中，從 S 找到 E 的最短逃脫時間。

## 參考程式與註解

```cpp
struct Point { int z, x, y, d; };
int dz[] = {+1, -1, 0, 0, 0, 0};
int dx[] = {0, 0, +1, -1, 0, 0};
int dy[] = {0, 0, 0, 0, +1, -1};

queue<Point> q;
q.push(start);
dungeon[start.z][start.x][start.y] = 'M';

while (!q.empty()) {
    Point cur = q.front(); q.pop();
    for (int i = 0; i < 6; i++) {
        int nz = cur.z + dz[i];
        int nx = cur.x + dx[i];
        int ny = cur.y + dy[i];
        if (out(nz, nx, ny) || dungeon[nz][nx][ny] == '#') continue;
        if (dungeon[nz][nx][ny] == 'E') return cur.d + 1;
        dungeon[nz][nx][ny] = 'M';
        q.push({nz, nx, ny, cur.d + 1});
    }
}
```

## 解題觀念

本題重點：三維 BFS、queue、六方向移動、最短路

- 把狀態設為 (z,x,y,d)，d 是目前距離。
- 六方向陣列分別表示上下、前後、左右。
- BFS 第一次遇到 E 就是最短時間；若走完仍找不到就是 Trapped。

複雜度：O(LRC)
