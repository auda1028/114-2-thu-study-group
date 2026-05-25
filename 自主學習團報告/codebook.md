# 競程 Code Book

本 code book 以競程常見主題分章，整理解題時可重複使用的模板、判斷方式與代表題目。閱讀時可以先看每章的「適用情境」，再對照程式片段與題型表，理解何時該使用該工具。

## 目錄

| 章節 | 主題 | 代表能力 |
|---|---|---|
| 第一章 | 基礎模板與模擬 | C++ 模板、輸入輸出、stack、queue、字串頻率 |
| 第二章 | 區間與序列處理 | 前綴和、滑動視窗、Kadane、掃描線 |
| 第三章 | 排序、雙指針與貪心 | 排序後掃描、配對、區間排程、自訂排序 |
| 第四章 | 有序資料結構與動態排名 | set、multiset、Fenwick Tree、PBDS |
| 第五章 | 圖論與連通塊 | BFS / Flood Fill、三維 BFS、DSU |
| 第六章 | 數論與大數 | 快速冪、質數表、GCD、大數加法與乘法 |
| 第七章 | 題型辨識與學習路線 | 從題目特徵選擇工具 |
| 第八章 | 40 題知識點索引 | 題目到觀念的對照 |

---

# 第一章 基礎模板與模擬

本章建立競程程式的基本骨架，並整理最常見的模擬題型。這類題目通常不需要複雜資料結構，但很考驗輸入輸出、邊界條件與狀態更新。

代表題目：Weird Algorithm、Parentheses Balance、Rails、Josephus Problem I、Palindrome Reorder、String Reorder。

## 1.1 基本 C++ 競程模板

適用：大多數 CSES / CPE 題目。

```cpp
#include <bits/stdc++.h>
using namespace std;

using ll = long long;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    // solve here
    return 0;
}
```

重點：

- `ios::sync_with_stdio(false); cin.tie(nullptr);` 可加速輸入輸出。
- 計算可能超過 `int` 時使用 `long long`。
- CPE/UVa 常有多組測資，要注意 EOF 或特殊結束條件。

題型判斷：

- 題目要求「照規則做」。
- 資料量不大，或每一步狀態都必須照順序更新。
- 重點常在格式、邊界、終止條件。

## 1.2 Stack 模擬

代表題目：Parentheses Balance、Rails。

```cpp
stack<char> st;
bool ok = true;

for (char c : s) {
    if (c == '(' || c == '[') {
        st.push(c);
    } else {
        if (st.empty()) {
            ok = false;
            break;
        }

        char t = st.top();
        st.pop();

        if ((c == ')' && t != '(') || (c == ']' && t != '[')) {
            ok = false;
            break;
        }
    }
}

ok = ok && st.empty();
```

核心：

- 需要「最近開啟的東西要最先被關閉」時，通常可以想到 stack。
- 括號、車站重排、遞迴狀態、巢狀結構都常用 stack。

## 1.3 Queue / Josephus 模擬

代表題目：Josephus Problem I、Power Crisis。

```cpp
queue<int> q;
for (int i = 1; i <= n; i++) {
    q.push(i);
}

while (!q.empty()) {
    q.push(q.front());
    q.pop();

    cout << q.front() << ' ';
    q.pop();
}
```

核心：

- 適合直接模擬循環淘汰、排隊、BFS 佇列。
- 若 n 很大或 k 可變，需改用 Fenwick Tree 或 ordered set。

## 1.4 回文與字元頻率

代表題目：Palindrome Reorder、String Reorder。

```cpp
vector<int> cnt(26);
for (char c : s) {
    cnt[c - 'A']++;
}

int odd = 0;
for (int x : cnt) {
    if (x % 2) odd++;
}

if (odd > 1) {
    cout << "NO SOLUTION\n";
}
```

核心：

- 回文最多只能有一種字元出現奇數次。
- 頻率表是字串重排題最常見的起手式。
- 若題目問「能不能重新排列」，通常先看每個字元的出現次數。

---

# 第二章 區間與序列處理

本章處理陣列、字串、時間線與連續區間。這類題目常見的關鍵是：不要每次重新掃描整段，而是用前綴和、滑動視窗或累積狀態把複雜度降下來。

代表題目：Static Range Sum Queries、Playlist、Distinct Values Subarrays、Maximum Subarray Sum、Restaurant Customers、NCPC D。

## 2.1 前綴和

代表題目：Static Range Sum Queries。

```cpp
vector<long long> pref(n + 1, 0);
for (int i = 1; i <= n; i++) {
    cin >> x;
    pref[i] = pref[i - 1] + x;
}

long long query(int l, int r) {
    return pref[r] - pref[l - 1];
}
```

核心：

- 預處理 O(n)。
- 每次區間和查詢 O(1)。
- 適合「陣列固定不變，查詢很多次」的題目。

題型判斷：

- 題目有很多次 `[l, r]` 查詢。
- 查詢內容是總和、出現次數、某種可累加的值。
- 陣列通常不會被修改。

## 2.2 Sliding Window / 滑動視窗

代表題目：Playlist、Distinct Values Subarrays。

```cpp
map<int, int> cnt;
long long ans = 0;
int l = 0;

for (int r = 0; r < n; r++) {
    cnt[a[r]]++;

    while (cnt[a[r]] > 1) {
        cnt[a[l]]--;
        l++;
    }

    ans += r - l + 1; // 以 r 結尾的合法子陣列數
}
```

核心：

- 右端點持續前進。
- 若條件被破壞，移動左端點直到恢復合法。
- 常用於「不重複」、「最多 k 種」、「總和不超過 x」等連續區間題。

題型判斷：

- 題目要求連續子陣列或連續子字串。
- 區間右端增加後，左端只會往右移，不會回頭。
- 條件可以透過 `map`、`set`、sum、count 維護。

## 2.3 Kadane 最大子陣列和

代表題目：Maximum Subarray Sum。

```cpp
long long best = LLONG_MIN;
long long cur = 0;

for (int i = 0; i < n; i++) {
    long long x;
    cin >> x;

    cur += x;
    best = max(best, cur);

    if (cur < 0) {
        cur = 0;
    }
}
```

核心：

- 若目前累積和變成負數，繼續保留只會拖累後面的答案。
- 要先更新 `best` 再把負數歸零，才能處理全負數測資。

另一種寫法：

```cpp
long long cur = 0;
long long best = LLONG_MIN;

for (long long x : a) {
    cur = max(x, cur + x);
    best = max(best, cur);
}
```

## 2.4 掃描線 / Timeline

代表題目：Restaurant Customers、NCPC D。

```cpp
map<int, long long> diff;

diff[start] += value;
diff[end] -= value;

long long cur = 0, best = 0;
for (auto [time, delta] : diff) {
    cur += delta;
    best = max(best, cur);
}
```

核心：

- 把區間開始視為 +，結束視為 -。
- 按時間排序後累加，就能得到任一時間點的重疊數。
- 若要輸出最大重疊區間，可以在 `cur` 進出最大值時記錄左右端點。

題型判斷：

- 題目給很多區間、時間段、進出場事件。
- 問最大重疊數、某時間點狀態、或狀態變化區間。

---

# 第三章 排序、雙指針與貪心

本章是 CSES Sorting and Searching 最常用的一組技巧。許多題目原本看起來需要枚舉所有組合，但排序後會產生單調性，接著就能用雙指針或貪心策略處理。

代表題目：Apartments、Ferris Wheel、Sum of Two Values、Movie Festival、Missing Coin Sum、Stick Lengths、Children's Game、Add All。

## 3.1 排序與雙指針

代表題目：Apartments、Ferris Wheel、Sum of Two Values。

核心想法：

- 先排序，讓資料有單調性。
- 用左右指針或兩個陣列指針逐步逼近答案。

```cpp
sort(a.begin(), a.end());
int l = 0, r = (int)a.size() - 1;

while (l < r) {
    long long sum = a[l] + a[r];

    if (sum == target) {
        // found
        break;
    } else if (sum < target) {
        l++;
    } else {
        r--;
    }
}
```

解題說明：

排序後，若目前和太小，只能把左指針右移；若太大，只能把右指針左移，因此可以用 O(n) 掃描完成搜尋。

## 3.2 貪心配對

代表題目：Ferris Wheel。

```cpp
sort(w.begin(), w.end());
int l = 0, r = n - 1;
int ans = 0;

while (l <= r) {
    if (w[l] + w[r] <= limit) {
        l++;
    }
    r--;
    ans++;
}
```

核心：

- 最重的人一定要被安排。
- 如果最重的人能搭配最輕的人，就順便配掉。
- 如果連最輕的人都不能配，最重者只能自己一組。

## 3.3 區間排程貪心

代表題目：Movie Festival。

```cpp
vector<pair<int, int>> seg; // {end, start}
sort(seg.begin(), seg.end());

int last_end = 0;
int ans = 0;

for (auto [end, start] : seg) {
    if (start >= last_end) {
        ans++;
        last_end = end;
    }
}
```

核心：

- 每次選最早結束的活動，可以留下最多時間給後面。
- 這類題目常見關鍵字是「最多可以參加幾個不重疊活動」。

## 3.4 可表示區間貪心

代表題目：Missing Coin Sum。

```cpp
sort(coins.begin(), coins.end());

long long reach = 0; // 目前可以表示 [1, reach]

for (long long x : coins) {
    if (x > reach + 1) {
        break;
    }
    reach += x;
}

cout << reach + 1 << '\n';
```

核心：

- 若已能表示 `[1, reach]`，下一枚硬幣 `x <= reach + 1`，就能延伸成 `[1, reach + x]`。
- 若 `x > reach + 1`，代表 `reach + 1` 無法被湊出。

## 3.5 Priority Queue 貪心合併

代表題目：Add All。

```cpp
priority_queue<long long, vector<long long>, greater<long long>> pq;

for (int i = 0; i < n; i++) {
    long long x;
    cin >> x;
    pq.push(x);
}

long long cost = 0;
while (pq.size() > 1) {
    long long a = pq.top();
    pq.pop();

    long long b = pq.top();
    pq.pop();

    cost += a + b;
    pq.push(a + b);
}
```

核心：

- 每次合併最小兩個，總成本最小。
- 這是 Huffman coding 的經典貪心模型。

## 3.6 自訂排序 Comparator

代表題目：Sort! Sort!! and Sort!!!、Children's Game。

### 多層規則排序

```cpp
int M;

bool cmp(int a, int b) {
    if (a % M != b % M) {
        return a % M < b % M;
    }

    bool odd_a = abs(a % 2);
    bool odd_b = abs(b % 2);

    if (odd_a != odd_b) {
        return odd_a > odd_b;
    }

    if (odd_a) {
        return a > b;
    }
    return a < b;
}
```

### 拼接最大化

```cpp
bool cmp_string(const string& a, const string& b) {
    return a + b > b + a;
}
```

核心：

- comparator 要清楚表達「誰應該排前面」。
- 對字串最大拼接，不能只比較字典序或長度，而要比較 `a+b` 和 `b+a`。

---

# 第四章 有序資料結構與動態排名

本章處理需要動態查詢前驅、後繼、第 k 個元素、區間長度的題目。這類題目通常不能只排序一次，因為資料會一邊查詢一邊更新。

代表題目：Concert Tickets、Traffic Lights、Towers、Josephus Problem II。

## 4.1 `set` / `multiset`

代表題目：Concert Tickets、Traffic Lights、Towers。

### 找不超過 x 的最大值

```cpp
multiset<int> s;

auto it = s.upper_bound(x);
if (it == s.begin()) {
    cout << -1 << '\n';
} else {
    --it;
    cout << *it << '\n';
    s.erase(it);
}
```

### 維護切點與最大區段

```cpp
set<int> points = {0, x};
multiset<int> len = {x};

void add_point(int p) {
    auto r = points.upper_bound(p);
    auto l = prev(r);

    len.erase(len.find(*r - *l));
    len.insert(p - *l);
    len.insert(*r - p);
    points.insert(p);
}
```

核心：

- `set` 負責找左右鄰居。
- `multiset` 負責維護可重複的區段長度。
- 若題目需要刪除單一元素，`erase(it)` 比 `erase(value)` 更安全。

## 4.2 Fenwick Tree / BIT

代表題目：Josephus Problem II、Fenwick Tree 模板。

用途：

- 單點更新。
- 前綴和查詢。
- 透過 prefix sum 找第 k 個仍存在的位置。

```cpp
struct Fenwick {
    int n;
    vector<long long> bit;

    Fenwick(int n) : n(n), bit(n + 1, 0) {}

    void add(int i, long long v) {
        for (; i <= n; i += i & -i) {
            bit[i] += v;
        }
    }

    long long sum(int i) {
        long long res = 0;
        for (; i > 0; i -= i & -i) {
            res += bit[i];
        }
        return res;
    }

    int kth(long long k) {
        int pos = 0;
        for (int jump = 1 << 20; jump; jump >>= 1) {
            if (pos + jump <= n && bit[pos + jump] < k) {
                k -= bit[pos + jump];
                pos += jump;
            }
        }
        return pos + 1;
    }
};
```

解題說明：

BIT 利用 `i & -i` 找到每個節點負責的區間，因此能在 O(log n) 完成更新與查詢。Josephus II 中可以把每個仍存活的人記為 1，被淘汰後改為 0，再用第 k 個 1 找到下一個淘汰者。

## 4.3 Ordered Set / PBDS

代表題目：動態排名查詢。

```cpp
#include <ext/pb_ds/assoc_container.hpp>
using namespace __gnu_pbds;

template <class T>
using ordered_set = tree<T, null_type, less<T>, rb_tree_tag,
    tree_order_statistics_node_update>;

ordered_set<int> os;
os.insert(10);
os.insert(20);

auto it = os.find_by_order(1);      // 第 0-based 的元素
int smaller = os.order_of_key(20);  // 小於 20 的元素數量
```

核心：

- `find_by_order(k)`：找第 k 小。
- `order_of_key(x)`：找小於 x 的數量。
- 適合處理動態排名與第 k 名查詢。

Fenwick Tree 與 PBDS 比較：

| 工具 | 適合情況 | 限制 |
|---|---|---|
| Fenwick Tree | index 範圍固定、要做前綴和或第 k 個 1 | 需要能把資料映射成 1-based index |
| PBDS | 動態插入刪除、查排名、第 k 小 | GNU extension，不是所有編譯器都有 |

---

# 第五章 圖論與連通塊

本章處理格子圖、區域計數、迷宮最短路與連通塊。Rank the Languages 可以用 BFS 或 DSU 兩種方式解，適合用來比較「搜尋走訪」與「集合合併」的差異；Dungeon Master 則是三維 BFS 的代表題。

代表題目：Rank the Languages (BFS)、Rank the Languages (DSU)、c124. 00532 - Dungeon Master。

## 5.1 BFS / Flood Fill

代表題目：Rank the Languages (BFS)。

```cpp
int dx[4] = {1, -1, 0, 0};
int dy[4] = {0, 0, 1, -1};

queue<pair<int, int>> q;
q.push({sx, sy});
vis[sx][sy] = true;

while (!q.empty()) {
    auto [x, y] = q.front();
    q.pop();

    for (int d = 0; d < 4; d++) {
        int nx = x + dx[d];
        int ny = y + dy[d];

        if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
        if (vis[nx][ny]) continue;
        if (grid[nx][ny] != grid[sx][sy]) continue;

        vis[nx][ny] = true;
        q.push({nx, ny});
    }
}
```

核心：

- 從一個起點擴張到整個連通區。
- 記得檢查邊界、是否走過、是否符合條件。
- 適合一次找完整區域，並在過程中標記 visited。

## 5.2 三維 BFS / Dungeon Master

代表題目：c124. 00532 - Dungeon Master。

題型特徵：

- 迷宮有三個維度，例如樓層 `L`、列 `R`、欄 `C`。
- 每一步可往六個方向移動：上、下、前、後、左、右。
- 問從起點 `S` 到出口 `E` 的最短時間。
- 因為每一步成本相同，所以 BFS 第一次到達出口就是最短路。

```cpp
struct Point {
    int z;
    int x;
    int y;
    int d;
};

int dz[] = {+1, -1,  0,  0,  0,  0};
int dx[] = { 0,  0, +1, -1,  0,  0};
int dy[] = { 0,  0,  0,  0, +1, -1};

char dungeon[31][31][31];

int bfs(int L, int R, int C, Point start) {
    queue<Point> q;
    q.push(start);
    dungeon[start.z][start.x][start.y] = 'M'; // 標記已走過

    while (!q.empty()) {
        Point cur = q.front();
        q.pop();

        for (int i = 0; i < 6; i++) {
            int nz = cur.z + dz[i];
            int nx = cur.x + dx[i];
            int ny = cur.y + dy[i];

            if (nz < 0 || nz >= L) continue;
            if (nx < 0 || nx >= R) continue;
            if (ny < 0 || ny >= C) continue;
            if (dungeon[nz][nx][ny] == '#') continue;
            if (dungeon[nz][nx][ny] == 'M') continue;

            if (dungeon[nz][nx][ny] == 'E') {
                return cur.d + 1;
            }

            dungeon[nz][nx][ny] = 'M';
            q.push({nz, nx, ny, cur.d + 1});
        }
    }

    return -1;
}
```

輸出格式：

```cpp
int ans = bfs(L, R, C, start);

if (ans >= 0) {
    cout << "Escaped in " << ans << " minute(s).\n";
} else {
    cout << "Trapped!\n";
}
```

核心：

- 2D BFS 的四方向改成 3D BFS 的六方向。
- `Point` 裡除了座標，也可一起存目前距離 `d`。
- 可直接把走過的格子改成標記字元，例如 `M`，等同 visited 陣列。
- BFS 適合無權重最短路；若移動成本不同，就不能直接用普通 BFS。

常見錯誤：

- 忘記檢查三個維度的邊界。
- 忘記標記 visited，導致同一格反覆進 queue。
- 讀入多層迷宮時沒有正確處理每一層每一列。
- 找到 `E` 後沒有立即回傳，或距離少加 1。

## 5.3 DSU / Union-Find

代表題目：Rank the Languages (DSU)。

```cpp
struct DSU {
    vector<int> parent, sz;

    DSU(int n) : parent(n), sz(n, 1) {
        iota(parent.begin(), parent.end(), 0);
    }

    int find(int x) {
        if (parent[x] == x) {
            return x;
        }
        return parent[x] = find(parent[x]);
    }

    void unite(int a, int b) {
        a = find(a);
        b = find(b);

        if (a == b) return;

        if (sz[a] < sz[b]) {
            swap(a, b);
        }

        parent[b] = a;
        sz[a] += sz[b];
    }
};
```

核心：

- 將「相鄰且同類」的格子合併成同一集合。
- 路徑壓縮與依大小合併可讓操作接近 O(1)。
- 適合先處理所有關係，再統計有幾個集合。

BFS 與 DSU 比較：

| 方法 | 優點 | 適合題型 |
|---|---|---|
| BFS / DFS | 寫法直觀，從起點走完整區域 | 格子 flood fill、迷宮、區域大小 |
| 三維 BFS | 可處理多層迷宮最短路 | Dungeon Master、3D grid |
| DSU | 合併關係後可快速查同集合 | 動態合併、連通塊統計、離線處理 |

---

# 第六章 數論與大數

本章整理競程常見數學工具。這些題目通常看起來像單純計算，但直接算會溢位或太慢，因此要用快速冪、質數表、GCD 或大數陣列。

代表題目：Bit Strings、Big Mod、Divisors、Prime Cuts、exam3、Fibonacci Freeze、Uncle Jack。

## 6.1 快速冪與模運算

代表題目：Bit Strings、Big Mod。

```cpp
long long mod_pow(long long a, long long e, long long mod) {
    long long res = 1 % mod;
    a %= mod;

    while (e > 0) {
        if (e & 1) {
            res = res * a % mod;
        }

        a = a * a % mod;
        e >>= 1;
    }

    return res;
}
```

核心：

- 將指數二進位拆解。
- 每次平方，複雜度 O(log e)。
- 每次乘法後取模，避免數字爆掉。

## 6.2 質數表與因數個數

代表題目：Divisors、Prime Cuts。

```cpp
vector<int> primes;
vector<bool> is_prime(N + 1, true);

void sieve() {
    is_prime[0] = is_prime[1] = false;

    for (int i = 2; i <= N; i++) {
        if (!is_prime[i]) continue;

        primes.push_back(i);

        if ((long long)i * i <= N) {
            for (long long j = 1LL * i * i; j <= N; j += i) {
                is_prime[j] = false;
            }
        }
    }
}

int count_divisors(long long x) {
    int ans = 1;

    for (long long p : primes) {
        if (p * p > x) break;

        int cnt = 0;
        while (x % p == 0) {
            x /= p;
            cnt++;
        }

        ans *= cnt + 1;
    }

    if (x > 1) {
        ans *= 2;
    }

    return ans;
}
```

核心：

- 若 `n = p1^a1 * p2^a2 * ...`，因數個數為 `(a1+1)(a2+1)...`。
- 若要對很多數做質因數分解，先建質數表會比較有效率。

## 6.3 GCD 與差值不變量

代表題目：exam3、分數約分題。

```cpp
long long gcd_ll(long long a, long long b) {
    a = abs(a);
    b = abs(b);

    while (b) {
        long long t = a % b;
        a = b;
        b = t;
    }

    return a;
}
```

核心：

- GCD 可用於約分。
- 多個數與第一個數的差值 GCD，常代表可共同平移或週期化的單位。
- 若題目出現「共同間距」、「最小單位」、「全部變成同餘」，可以先想 GCD。

## 6.4 大數加法

代表題目：Fibonacci Freeze。

```cpp
vector<int> add_big(const vector<int>& a, const vector<int>& b) {
    vector<int> res;
    int carry = 0;

    for (int i = 0; i < (int)a.size() || i < (int)b.size() || carry; i++) {
        int sum = carry;

        if (i < (int)a.size()) {
            sum += a[i];
        }
        if (i < (int)b.size()) {
            sum += b[i];
        }

        res.push_back(sum % 10);
        carry = sum / 10;
    }

    return res;
}
```

核心：

- 以反向 digit vector 儲存大數，最低位放在 index 0。
- 加法時逐位處理 carry。
- Fibonacci 大數題可以先預處理整張表。

## 6.5 大數乘小整數

代表題目：Uncle Jack。

```cpp
vector<int> multiply_small(vector<int> digits, int b) {
    int carry = 0;

    for (int i = 0; i < (int)digits.size(); i++) {
        long long cur = 1LL * digits[i] * b + carry;
        digits[i] = cur % 10;
        carry = cur / 10;
    }

    while (carry) {
        digits.push_back(carry % 10);
        carry /= 10;
    }

    return digits;
}
```

核心：

- 適合處理 `b^p` 類型的大數。
- 若 p 很大，可以再搭配快速冪思想優化。

---

# 第七章 題型辨識與學習路線

學習時可以依照下面的順序建立解題能力：

1. 基礎能力：C++ 模板、模擬、stack、queue、字串頻率。
2. 區間能力：前綴和、滑動視窗、Kadane、掃描線。
3. 排序與貪心：雙指針、配對、區間排程、可表示區間、自訂排序。
4. 資料結構：set、multiset、Fenwick Tree、PBDS。
5. 圖論：BFS/Flood Fill、三維 BFS、DSU。
6. 數學工具：快速冪、質數表、GCD、大數。

## 題型辨識整理

| 題目特徵 | 優先想到的工具 |
|---|---|
| 多次區間和查詢 | 前綴和 |
| 連續子陣列且左右界單調 | 滑動視窗 |
| 最大連續和 | Kadane |
| 區間重疊、進出場時間 | 掃描線 |
| 兩數和、配對、兩個排序序列 | 排序 + 雙指針 |
| 最多不重疊活動 | 依結束時間排序 + 貪心 |
| 每次找不超過 x 的最大值 | multiset + upper_bound |
| 動態找第 k 個存活者 | Fenwick Tree / PBDS |
| 格子連通區 | BFS / DFS / DSU |
| 三維迷宮最短路 | 三維 BFS |
| 大指數取模 | 快速冪 |
| 因數個數、質數範圍 | 質數表 + 質因數分解 |
| 數字超過 long long | 大數陣列 |

學習重點不只是背模板，而是看到題目時能判斷「資料是否需要排序」、「區間是否能滑動」、「是否需要快速找前驅/後繼」、「是否是連通塊」、「是否需要維護第 k 個元素」。這些判斷能力就是競程解題能力成長的核心。

---

# 第八章 40 題知識點索引

本章將 40 題依照主要知識點整理成索引，方便讀者從題目回查對應的演算法主題。若遇到不熟的觀念，可以先看表格找到代表題，再回到前面章節閱讀模板。

## 8.1 40 題總表

| 編號 | 題目 | 類型 | 核心知識點 |
|---:|---|---|---|
| 01 | Two Knights | CSES / 數學 | 組合數、攻擊狀態扣除、公式推導 |
| 02 | Coin Piles | CSES / 數學 | 不變量、整除條件、最大值限制 |
| 03 | Bit Strings | CSES / 數論 | 快速冪、模運算 |
| 04 | Static Range Sum Queries | CSES / 區間 | 前綴和、O(1) 區間查詢 |
| 05 | Apartments | CSES / 排序 | 排序、雙指針、誤差範圍配對 |
| 06 | Ferris Wheel | CSES / 貪心 | 左右指針、最重者優先配對 |
| 07 | Restaurant Customers | CSES / 掃描線 | 事件排序、最大同時人數 |
| 08 | Movie Festival | CSES / 貪心 | 區間排程、依結束時間排序 |
| 09 | Sum of Two Values | CSES / 搜尋 | 排序、雙指針、保留原索引 |
| 10 | Maximum Subarray Sum | CSES / DP 思想 | Kadane、最大連續子陣列 |
| 11 | Missing Coin Sum | CSES / 貪心 | 可表示區間、最小不可湊金額 |
| 12 | Playlist | CSES / 滑動視窗 | 最長不重複連續區間、map 記錄最後位置 |
| 13 | Concert Tickets | CSES / 有序集合 | multiset、upper_bound、前驅查詢 |
| 14 | Traffic Lights | CSES / 有序集合 | set 找左右鄰居、multiset 維護最大區段 |
| 15 | Josephus Problem II | CSES / 動態排名 | Fenwick Tree、找第 k 個存活者 |
| 16 | Weird Algorithm | CSES / 模擬 | Collatz 序列、while 模擬、long long |
| 17 | Repetitions | CSES / 字串 | 線性掃描、連續段長度 |
| 18 | Two Sets | CSES / 建構 | 等差級數、奇偶性、貪心分組 |
| 19 | Palindrome Reorder | CSES / 字串 | 字元頻率、回文建構、奇數次判斷 |
| 20 | Trailing Zeros | CSES / 數論 | 階乘質因數、計算 5 的個數 |
| 21 | Missing Number | CSES / 數學 | 總和公式、缺漏值 |
| 22 | Gray Code | CSES / 位元 | `i ^ (i >> 1)`、二進位輸出 |
| 23 | Increasing Array | CSES / 貪心 | 單調序列、最小補值 |
| 24 | Permutations | CSES / 建構 | 奇偶分組、避免相鄰差 1 |
| 25 | Number Spiral | CSES / 數學 | 座標層數、奇偶方向公式 |
| 26 | Distinct Numbers | CSES / 集合 | set 去重、不同值計數 |
| 27 | Stick Lengths | CSES / 數學 + 排序 | 中位數、最小絕對距離和 |
| 28 | Collecting Numbers | CSES / 序列 | 位置陣列、斷點計數 |
| 29 | Collecting Numbers II | CSES / 動態維護 | swap 後局部更新、受影響 pair |
| 30 | Towers | CSES / 有序集合 | multiset、patience sorting 思想 |
| 31 | Josephus Problem I | CSES / 模擬 | queue、循環淘汰 |
| 32 | Parentheses Balance | CPE/UVa / Stack | stack、括號匹配 |
| 33 | Jolly Jumpers | CPE/UVa / 陣列 | 差值集合、boolean 標記 |
| 34 | Hardwood Species | CPE/UVa / Map | map 統計、百分比輸出、字典序 |
| 35 | Big Mod | CPE/UVa / 數論 | 快速冪、mod |
| 36 | Rank the Languages | CPE/UVa / 圖論 | BFS / DSU、連通塊統計、排序輸出 |
| 37 | Rails | CPE/UVa / Stack | stack 模擬、車站重排 |
| 38 | Add All | CPE/UVa / 貪心 | priority_queue、最小合併成本、Huffman 思想 |
| 39 | Children's Game | CPE/UVa / 排序 | 自訂 comparator、字串拼接最大化 |
| 40 | Dungeon Master | CPE/UVa / 圖論 | 三維 BFS、六方向移動、最短路 |
