# 競程題解學習目錄

本資料夾整理 40 題適合作為學習教材的題解。每篇題解皆包含題意摘要、參考程式、解題觀念與時間複雜度，閱讀時建議先理解題型，再對照程式中的關鍵註解。

建議閱讀順序：

1. 先看基礎模擬與數學規律，建立 C++ 實作與邊界判斷能力。
2. 再看排序、雙指針、貪心與區間題，練習從資料特徵選擇演算法。
3. 最後看資料結構、圖論與數論題，整理成可重複使用的 code book 模板。

| 編號 | 題目 | 題目連結 | 主要觀念 | 報告檔 |
|---:|---|---|---|---|
| 01 | Two Knights | [CSES](https://cses.fi/problemset/task/1072/) | 組合數、數學公式、棋盤攻擊位置扣除 | [01_Two_Knights.md](./01_Two_Knights.md) |
| 02 | Coin Piles | [CSES](https://cses.fi/problemset/task/1754/) | 數學不變量、整除條件、最大值限制 | [02_Coin_Piles.md](./02_Coin_Piles.md) |
| 03 | Bit Strings | [CSES](https://cses.fi/problemset/task/1617/) | 快速冪、模運算 | [03_Bit_Strings.md](./03_Bit_Strings.md) |
| 04 | Static Range Sum Queries | [CSES](https://cses.fi/problemset/task/1646/) | 前綴和、區間查詢 | [04_Static_Range_Sum_Queries.md](./04_Static_Range_Sum_Queries.md) |
| 05 | Apartments | [CSES](https://cses.fi/problemset/task/1084/) | 排序、雙指針、貪心配對 | [05_Apartments.md](./05_Apartments.md) |
| 06 | Ferris Wheel | [CSES](https://cses.fi/problemset/task/1090/) | 排序、雙指針、貪心 | [06_Ferris_Wheel.md](./06_Ferris_Wheel.md) |
| 07 | Restaurant Customers | [CSES](https://cses.fi/problemset/task/1619/) | 掃描線、事件排序 | [07_Restaurant_Customers.md](./07_Restaurant_Customers.md) |
| 08 | Movie Festival | [CSES](https://cses.fi/problemset/task/1629/) | 區間排程、依結束時間排序、貪心 | [08_Movie_Festival.md](./08_Movie_Festival.md) |
| 09 | Sum of Two Values | [CSES](https://cses.fi/problemset/task/1640/) | 排序、雙指針、保留原始索引 | [09_Sum_of_Two_Values.md](./09_Sum_of_Two_Values.md) |
| 10 | Maximum Subarray Sum | [CSES](https://cses.fi/problemset/task/1643/) | Kadane 演算法、動態維護最佳連續區間 | [10_Maximum_Subarray_Sum.md](./10_Maximum_Subarray_Sum.md) |
| 11 | Missing Coin Sum | [CSES](https://cses.fi/problemset/task/2183/) | 排序、貪心、可表示區間 | [11_Missing_Coin_Sum.md](./11_Missing_Coin_Sum.md) |
| 12 | Playlist | [CSES](https://cses.fi/problemset/task/1141/) | 滑動視窗、map 記錄最後出現位置 | [12_Playlist.md](./12_Playlist.md) |
| 13 | Concert Tickets | [CSES](https://cses.fi/problemset/task/1091/) | multiset、upper_bound、前驅查詢 | [13_Concert_Tickets.md](./13_Concert_Tickets.md) |
| 14 | Traffic Lights | [CSES](https://cses.fi/problemset/task/1163/) | set 維護切點、multiset 維護區段長度 | [14_Traffic_Lights.md](./14_Traffic_Lights.md) |
| 15 | Josephus Problem II | [CSES](https://cses.fi/problemset/task/2163/) | Fenwick Tree、order statistic、第 k 個存活者 | [15_Josephus_Problem_II.md](./15_Josephus_Problem_II.md) |
| 16 | Weird Algorithm | [Link](https://cses.fi/problemset/task/1068/) | Collatz 序列、while 模擬、long long | [16_Weird_Algorithm.md](./16_Weird_Algorithm.md) |
| 17 | Repetitions | [Link](https://cses.fi/problemset/task/1069/) | 字串掃描、連續段長度 | [17_Repetitions.md](./17_Repetitions.md) |
| 18 | Two Sets | [Link](https://cses.fi/problemset/task/1092/) | 等差級數、奇偶判斷、建構法 | [18_Two_Sets.md](./18_Two_Sets.md) |
| 19 | Palindrome Reorder | [Link](https://cses.fi/problemset/task/1755/) | 字元頻率、回文建構 | [19_Palindrome_Reorder.md](./19_Palindrome_Reorder.md) |
| 20 | Trailing Zeros | [Link](https://cses.fi/problemset/task/1618/) | 階乘、質因數 5、數學計數 | [20_Trailing_Zeros.md](./20_Trailing_Zeros.md) |
| 21 | Missing Number | [Link](https://cses.fi/problemset/task/1083/) | 總和公式、缺漏值 | [21_Missing_Number.md](./21_Missing_Number.md) |
| 22 | Gray Code | [Link](https://cses.fi/problemset/task/2205/) | 位元運算、Gray code、bitset | [22_Gray_Code.md](./22_Gray_Code.md) |
| 23 | Increasing Array | [Link](https://cses.fi/problemset/task/1094/) | 貪心、單調序列、累加補值 | [23_Increasing_Array.md](./23_Increasing_Array.md) |
| 24 | Permutations | [Link](https://cses.fi/problemset/task/1070/) | 建構法、奇偶分組 | [24_Permutations.md](./24_Permutations.md) |
| 25 | Number Spiral | [Link](https://cses.fi/problemset/task/1071/) | 座標規律、奇偶層公式 | [25_Number_Spiral.md](./25_Number_Spiral.md) |
| 26 | Distinct Numbers | [Link](https://cses.fi/problemset/task/1621/) | set 去重 | [26_Distinct_Numbers.md](./26_Distinct_Numbers.md) |
| 27 | Stick Lengths | [Link](https://cses.fi/problemset/task/1074/) | 排序、中位數、絕對距離和 | [27_Stick_Lengths.md](./27_Stick_Lengths.md) |
| 28 | Collecting Numbers | [Link](https://cses.fi/problemset/task/2216/) | 位置陣列、斷點計數 | [28_Collecting_Numbers.md](./28_Collecting_Numbers.md) |
| 29 | Collecting Numbers II | [Link](https://cses.fi/problemset/task/2217/) | swap 後局部更新、斷點維護 | [29_Collecting_Numbers_II.md](./29_Collecting_Numbers_II.md) |
| 30 | Towers | [Link](https://cses.fi/problemset/task/1073/) | multiset、patience sorting | [30_Towers.md](./30_Towers.md) |
| 31 | Josephus Problem I | [Link](https://cses.fi/problemset/task/2162/) | queue、循環淘汰模擬 | [31_Josephus_Problem_I.md](./31_Josephus_Problem_I.md) |
| 32 | Parentheses Balance | [Link](https://onlinejudge.org/external/6/673.pdf) | stack、括號匹配 | [32_Parentheses_Balance.md](./32_Parentheses_Balance.md) |
| 33 | Jolly Jumpers | [Link](https://onlinejudge.org/external/100/10038.pdf) | 差值集合、陣列標記 | [33_Jolly_Jumpers.md](./33_Jolly_Jumpers.md) |
| 34 | Hardwood Species | [Link](https://onlinejudge.org/external/102/10226.pdf) | map 統計、百分比輸出 | [34_Hardwood_Species.md](./34_Hardwood_Species.md) |
| 35 | Big Mod | [Link](https://onlinejudge.org/external/3/374.pdf) | 快速冪、模運算 | [35_Big_Mod.md](./35_Big_Mod.md) |
| 36 | Rank the Languages | [Link](https://onlinejudge.org/external/103/10336.pdf) | BFS / DSU、連通塊、排序輸出 | [36_Rank_the_Languages.md](./36_Rank_the_Languages.md) |
| 37 | Rails | [Link](https://onlinejudge.org/external/5/514.pdf) | stack、queue、車站模擬 | [37_Rails.md](./37_Rails.md) |
| 38 | Add All | [Link](https://onlinejudge.org/external/109/10954.pdf) | priority_queue、貪心合併、Huffman 思想 | [38_Add_All.md](./38_Add_All.md) |
| 39 | Children's Game | [Link](https://onlinejudge.org/external/109/10905.pdf) | 自訂排序、字串拼接最大化 | [39_Childrens_Game.md](./39_Childrens_Game.md) |
| 40 | Dungeon Master | [Link](https://onlinejudge.org/external/5/532.pdf) | 三維 BFS、queue、六方向移動、最短路 | [40_Dungeon_Master.md](./40_Dungeon_Master.md) |

## 主題索引

| 主題 | 對應題目 | 學習重點 |
|---|---|---|
| 數學規律 | 01、02、03、18、20、21、25、27、35 | 公式推導、整除條件、快速冪、座標規律 |
| 字串與頻率 | 17、19、32、34、39 | 線性掃描、字元統計、stack、map、自訂排序 |
| 排序與貪心 | 05、06、08、09、11、23、24、30、38 | 排序後掃描、配對、區間排程、最小合併成本 |
| 區間與序列 | 04、07、10、12、14、28、29 | 前綴和、掃描線、Kadane、滑動視窗、動態維護 |
| 資料結構 | 13、14、15、26、30、31、37 | set、multiset、Fenwick Tree、queue、stack |
| 圖論與搜尋 | 36、40 | BFS、連通塊、三維迷宮最短路 |

這份題解目錄的重點不是記住單一題目的答案，而是學會把題目分類：看到「最短步數」想到 BFS，看到「每次找不超過某值的最大元素」想到 multiset，看到「大量區間查詢」想到前綴和。能建立這種題型辨識能力，才是 code book 最有價值的地方。
