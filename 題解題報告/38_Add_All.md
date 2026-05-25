# 38. Add All

## 題目

- 題目連結：<https://onlinejudge.org/external/109/10954.pdf>
- 題意摘要：每次合併兩個數會產生成本，求合併全部數字的最小總成本。

## 參考程式與註解

```cpp
priority_queue<long long, vector<long long>, greater<long long>> pq;
for (long long x : a) pq.push(x);

long long cost = 0;
while (pq.size() > 1) {
    long long x = pq.top(); pq.pop();
    long long y = pq.top(); pq.pop();
    cost += x + y;
    pq.push(x + y);
}
```

## 解題觀念

本題重點：priority_queue、貪心合併、Huffman 思想

- 每次選最小的兩個數合併。
- 合併後的新數字再放回 priority queue。
- 這和 Huffman coding 的貪心策略相同。

複雜度：O(n log n)
