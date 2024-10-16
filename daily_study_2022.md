[TOC]

## 2022-09-18

### 一、易忘知识点整理

#### 1. 差分思想

指编程时需要考虑相邻项的差/商等关系，有时会豁然开朗； 

#### 2. const的理解

##### 2.1 修饰变量

```c++
const int* p = 8; // 内容不可变
int* const p = 8; // 指针不可变
const int* const p = 8; // 综合
```

##### 2.2 修饰函数变量

修饰参数时，保证参数不会被修改；

修饰自定义参数时，const &, 不会调用构造函数； 

修饰返回值时，不能作为左值； 

##### 2.3 修饰类成员函数

防止该成员函数修改当前调用对象的值，使其不能改变成员变量的值，提高代码的安全性； 

用mutable int修饰成员变量后，则可以在const成员函数中修改其值；

#### 3. 树状数组（BIT）

点更新、点查询：

```c++
void update(int x, int v) {
    for (; x < LIMIT; x += x & -x) bit[x] += v;
}
int search(int x) {
   	int res = 0; 
    for (; 0 < x; x -= x & -x) res += bit[x];
    return ans;
}
```

区间修改、区间查询：

```c++
void update(int x, int v) {
    int y = x;
    for (; x < LIMIT; x += x & -x) {
        s1[x] += v;
        s2[x] += v * (y - 1);
    }
}
void search(int x) {
    int res = 0, y = x;
    for (; 0 < x; x -= x & -x) res += y * s1[x] - s2[x];
    return ans;
}
```

#### 4. 扫描线算法

待完善；

#### 5. 各容器接口

unordered_map（底层实现是哈系表）的接口函数：

```c++
unordered_map:
	count:
	emplace:
	bucket(i):
	bucket_count:
	bucket_size(i);
	begin(i), end(i) // i是桶号
```

对比：

|                | 插入                                      | 删除                              | 查找                                                         | 赋值            | 其他                                                       |
| -------------- | ----------------------------------------- | --------------------------------- | ------------------------------------------------------------ | --------------- | ---------------------------------------------------------- |
| set \| map     | insert <br />// map可循环赋值             | erase(fit, lit); <br />erase(key) | lower_bound \| upper_bound (返回iter)<br /> count 返回存在次数；<br />[]运算符返回map的值； | map一般用[]赋值 |                                                            |
| vector         | insert <br />push_back <br />emplace_back | erase                             | 排序后用lower_bound\|upper_bound\|[]寻秩访问                 | []              | data()：返回数组 <br />rbegin(): 反向访问 <br />swap: 交换 |
| queue          | push                                      | pop                               | front \| back                                                |                 |                                                            |
| stack          | push                                      | pop                               | top                                                          |                 |                                                            |
| priority_queue | push                                      | pop                               | top                                                          |                 |                                                            |

#### 6. 并查集（循环节）

```c++
// build
for (int i = 0; i < N; ++i) a[i] = i; 
// find
int find(int x) {
    return a[x] = (a[x] == x) ? x : find(a[x]);
}
// merge
void merge(int x, int y) {
    a[find(x)] = find(y);
}

```

#### 7. 大数乘方

对指数二分

```c++
// ll：long long, 求对大素数M的模余
ll bnq(ll a, ll n) {
    ll ans = 1, md = a;
    while (n) {
        if (n & 1) ans = ans * md % M;
        md = md * md % M;
        n >>= 1;
    }
    return ans;
}
```

GCD算法：（奇偶法）

```c++
int gcd(int a, int b) {
    if (a < b) return gcd(b, a);
    if (b == 0) return a;
    if (!(a & 1) && !(b & 1)) return 2 * gcd(a >> 1, b >> 1);
    if (!(a & 1) && (b & 1)) return gcd(a >> 1, b);
    if ((a & 1) && !(b & 1)) return gcd(a, b >> 1);
    return gcd(a - b, b);
}
```

除法模余（逆模余）

```c++
a / b % M = a * (b ^ (M - 2)) % M (M与b互素）
```



#### 8. Trie树数组

顾名思义，用整数数组表示一颗Trie树，方便查询前缀、后缀问题；

```c++
// init
int trie[N][26];
int pos = 0; // 储存trie节点个数,在build中更新
// build 
void build(string s) {
    int p = 0;
    for (int i = 0; i < s.length(); ++i) {
        if (trie[p][s[i]] == 0) trie[p][s[i]] = pos++;
        p = trie[p][s[i]];
    }
}
// search
void find(string s) {
    int p = 0;
    for (int i = 0; i < s.length(); ++i) {
        if (trie[p][s[i]] == 0) return ;
        p = trie[p][s[i]]; // do something
    }
}
```



#### 9. 最小位移中位数算法

Leetcode中的一题；

##### 9.1 Leetcode 1703: [Minimum Adjacent Swaps for K Consecutive Ones](https://leetcode.cn/problems/minimum-adjacent-swaps-for-k-consecutive-ones/)

题目描述：

```
You are given an integer array, nums, and an integer k. nums comprises of only 0's and 1's. In one move, you can choose two adjacent indices and swap their values.

Return the minimum number of moves required so that nums has k consecutive 1's.

Example 1:

Input: nums = [1,0,0,1,0,1], k = 2
Output: 1
Explanation: In 1 move, nums could be [1,0,0,0,1,1] and have 2 consecutive 1's.

Example 2:

Input: nums = [1,0,0,0,0,0,1,1], k = 3
Output: 5
Explanation: In 5 moves, the leftmost 1 can be shifted right until nums = [0,0,0,0,0,1,1,1].

Example 3:

Input: nums = [1,1,0,1], k = 2
Output: 0
Explanation: nums already has 2 consecutive 1's.

Constraints:

    1 <= nums.length <= 105
    nums[i] is 0 or 1.
    1 <= k <= sum(nums)
```

方法：取中位数，时间复杂度为O(n)，证明可以用数学归纳法：

```c++
#define L 100010
int minMoves(vector<int>& nums, int k) {
    if (k == 1) return 0;
    int n = nums.size(), m = 0;
    long long pa[L];
    for (int i = 0; i < n; ++i) if (nums[i]) pa[m++] = i;
    int med = k + 1 >> 1;
    int cm = med;
    long long vl = 0, vr = 0, wl, wr; 
    for (int i = 0; i < med; ++i) vl += i;
    for (int i = 0; i <= k - med; ++i) vr += i;
    wl = vl + med, wr = vr - (k - med);
    long long sl = accumulate(pa, pa + med, 0); 
    long long sr = accumulate(pa + med, pa + k, 0); 
    long long cl = (med * pa[cm - 1] - sl - vl) + (sr - (k - med) * pa[cm - 1] - vr);
    long long cr = (med * pa[cm] - sl - wl) + (sr - (k - med) * pa[cm] - wr);
    long long ans = (k & 1) ? cl : min(cl, cr);
    for (int i = 1; i + k <= m; ++i) {
        cm = i + med;
        sl += pa[cm - 1] - pa[i - 1]; 
        sr += pa[i + k - 1] - pa[cm - 1]; 
        cl = (med * pa[cm - 1] - sl - vl) + (sr - (k - med) * pa[cm - 1] - vr);
        cr = (med * pa[cm] - sl - wl) + (sr - (k - med) * pa[cm] - wr);
        ans = (k & 1) ? min(ans, cl) : min(ans, min(cl, cr));
    }
    return ans;
}
```



#### 10. 内置库函数

__builtin_popcount  // 二进制位中1的个数

__builtin_clz/ctz/ffs // 二进制位中开头|结尾0的个数|第一个1出现位置



#### 11. 遍历mask的所有子集技巧

```c++
for (x = mask; x; x = mask & x - 1)
```

#### 12. 覆盖点的区间个数查询

[add in 2022-10-27]

利用差分的技巧，在区间端点处修改差值，用左区间和表示当前代查询值。

##### 12.1 Leetcode 1674 [Minimum Moves to Make Array Complementary](https://leetcode.cn/problems/minimum-moves-to-make-array-complementary/)

题目描述：

```
You are given an integer array nums of even length n and an integer limit. In one move, you can replace any integer from nums with another integer between 1 and limit, inclusive.

The array nums is complementary if for all indices i (0-indexed), nums[i] + nums[n - 1 - i] equals the same number. For example, the array [1,2,3,4] is complementary because for all indices i, nums[i] + nums[n - 1 - i] = 5.

Return the minimum number of moves required to make nums complementary.

Example 1:

Input: nums = [1,2,4,3], limit = 4
Output: 1
Explanation: In 1 move, you can change nums to [1,2,2,3] (underlined elements are changed).
nums[0] + nums[3] = 1 + 3 = 4.
nums[1] + nums[2] = 2 + 2 = 4.
nums[2] + nums[1] = 2 + 2 = 4.
nums[3] + nums[0] = 3 + 1 = 4.
Therefore, nums[i] + nums[n-1-i] = 4 for every i, so nums is complementary.

Example 2:

Input: nums = [1,2,2,1], limit = 2
Output: 2
Explanation: In 2 moves, you can change nums to [2,2,2,2]. You cannot change any number to 3 since 3 > limit.

Example 3:

Input: nums = [1,2,1,2], limit = 2
Output: 0
Explanation: nums is already complementary.

Constraints:

    n == nums.length
    2 <= n <= 105
    1 <= nums[i] <= limit <= 105
    n is even.
```

计算“覆盖点的区间个数”：

```c++
#define L 200010
int minMoves(vector<int>& nums, int limit) {
    vector<int> ct(L);
    int n = nums.size();
    for (int i = 0; i < n / 2; ++i) {
        int j = n - i - 1;
        int a = min(1 + nums[i], 1 + nums[j]);
        int b = nums[i] + nums[j];
        int c = max(limit + nums[i], limit + nums[j]);
        ct[2] += 2, ct[a] -= 1, ct[b] -= 1, ct[b + 1] += 1, ct[c + 1] += 1;
    }   
    int ans = INT_MAX, s = 0;
    for (int i = 2; i <= 2 * limit; ++i) {
        s += ct[i];
        ans = min(ans, s); 
    }   
    return ans;
}
```



#### 13. string->int方法

```c++
1. atoi, strtol
2. stol
3. stringstream | scanf
```

#### 14. 格雷码与二进制的互换

格雷码转二进制：

```c++
// method 1
int gray2bit(int x) {
    int y = x;
    while (x >>= 1) y ^= x;
    return y;
}

// method 2
int gray2bit2(int x) {
    for (int i = 0; i < 5; ++i) {
        x ^= x >> (1 << i); 
    }   
    return x;
}

// method 3
int gray2bit3(int x) {
    x ^= x >> 16; 
    x ^= x >> 8;
    x ^= x >> 4;
    x ^= x >> 2;
    x ^= x >> 1;
    return x;
}

```



二进制转格雷码：

```c++
int bit2gray(int x) {
    return x ^ (x >> 1);
}
```



#### 15. 线段树、矩阵树、空间树



#### 16. ST算法

```c++
#define N 20 // hold 2^19 numbers
#define M 100000 // data
int st[N][M], orig[M]; // orig is the original data
void build() {
    for (int i = 0; i < M; ++i) st[0][i] = orig[i];
    for (int i = 1; i < N; ++i) {
        for (int j = 0; j < M; ++j) {
            st[i][j] = max(st[i - 1][j], st[i - 1][j + (1 << (i - 1))]); // st[i][j] --- max/min value for range [j, j + (1 << i))
        }
    }
}

// search range [l, r]
void search(int l, int r) {
    int n = __builtin_clz(r - l + 1) - 1;
    return st[n][l] + st[n][r - (1 << n) + 1];
}
```



#### 17. 筛法

```c++
#define N 200000
vector<int> prim, mark(N, 0);
void get_prim() {
    for (int i = 2; i < N; ++i)
        if (!mark[i]) {
            prim.emplace_back(i);
            for (int j = i << 1; j < N; j += i) mark[j] = 1;
        }
}
```



#### 18. 二叉树的遍历

树的遍历

今天复习及背诵树遍历的迭代板方法，以便后续使用。

先序遍历：

```c++
// 先序遍历
void travelPrev(TreeNode* p) {
    stack<TreeNode*> st;
    if (p) st.push(p);
    while (!st.empty()) {
        auto x = st.top(); st.pop();
        while (x) {
            visit(x);
            if (x->right) st.push(x->right);
            x = x->left;
        }
    }
}
```

中序遍历：

```c++
void travelIn(TreeNode* p) {
    stack<TreeNode*> st;
    auto x = p;
    while (true) {
        while (x) st.push(x), x = x->left;
        if (st.empty()) break;
        x = st.top(); st.pop(); visit(x);
        x = x->right;
    }
}
```

后序遍历

```c++
void travelPost(TreeNode* p) {
    stack<TreeNode*> st;
    if (p) st.push(p);
    auto x = p;
    while (!st.empty()) {
        auto f = st.top();
        if (f->left != x && f->right != x) {
            while (f) {
                if (f->left) {
                    if (f->right) st.push(f->right);
                    f = f->left;
                } else f = f->right;
                if (f) st.push(f);
            }
        }
        x = st.top(); st.pop(); visit(x);
    }
}
```

层次遍历

```c++
void travelLevel(TreeNode* p) {
    queue<TreeNode*> q;
    q.push(p); 
    while (!q.empty()) {
        int n = q.size(), i = 0;
        while (i++ < n) {
            auto x = q.front(); q.pop(); visit(x);
            if (x->left) q.push(x->left);
            if (x->right) q.push(x->right);
        }
    }
}
```

#### 19. 排列组合生成方法

背诵排列及组合的生成方法。

无重复元素的全排列



```c++
// 假设nums已经排好序
void permulate(vector<int> nums, int st) { // 不传引用，这样能得到按顺序的排列，也无须回溯；当然也可以使用传引用+标记的方法，此处仅使用最简洁代码
    if (st == n) do_with_permulate(); // 当前nums数组即为当前排列
    for (int i = st; i < nums.size(); ++i) {
        swap(nums[i], nums[st]);	// 交换当前元素与当前占位元素
        permulate(nums, st + 1); 
    }
}
```

有重复元素的全排列

```c++
// 假设nums已经排好序
void permulate(vector<int> nums, int st) { // 不传引用，这样能得到按顺序的排列，也无须回溯；当然也可以使用传引用+标记的方法，此处仅使用最简洁代码
    if (st == n) do_with_permulate(); // 当前nums数组即为当前排列
    for (int i = st, bf = INT_MIN; i < nums.size(); ++i) {
        if (bf == nums[i]) continue;
        bf = nums[i]; // bf记录上一个占位元素，防止重复
        swap(nums[i], nums[st]);	// 交换当前元素与当前占位元素
        permulate(nums, st + 1); 
    }
}
```

无重复元素生成组合数

1~n的数组生成k个数的组合。

```c++
vector<vector<int>> ans;
vector<int> path;

void gen(int n, int k) {
  if (n < k) return;
  // not select n
  gen(n - 1, k); 
  // backtrack: select n
  path.push_back(n);
  if (k == 1) ans.push_back(path);
  else gen(n - 1, k - 1); 
  path.pop_back();
}

vector<vector<int>> combine(int n, int k) {
  gen(n, k); 
  return ans;
}
```

重复元素生成组合

以leetcode 40（39类似）为i例，主要是回溯的方法。

```c++
vector<vector<int>> ans;
vector<int> path;
map<int,int> dm; // map去重并计数
vector<int> uq; // 保留去重后的结果
int N;

void combine(int tg, int st) {
    if (st == N) return;
    if (tg < uq[st]) return;
    int i = 0;
    for (; i <= dm[uq[st]]; ++i) { // 遍历尝试当前0～元素最大次数，注意加等号
        if (i * uq[st] < tg) combine(tg - i * uq[st], st + 1); 
        else {
            if (i * uq[st] == tg) ans.push_back(path);
            break;
        }
        path.push_back(uq[st]);
    }   
    while (i--) path.pop_back();
}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
  for (auto v: candidates) ++dm[v];
  for (auto [k, v]: dm) uq.emplace_back(k);
  N = dm.size();
  combine(target, 0); 
  return ans;
}

```

另一种写法(Leetcode 90)： [leetcode 90](https://leetcode.com/problems/subsets-ii/)

```c++
vector<vector<int>> res;
vector<int> path;

void gen(vector<int> nums, int st) {
  if (st == nums.size()) { res.push_back(path); return; }
  int cnt = 1;
  while (st + cnt < nums.size() && nums[st + cnt] == nums[st]) ++cnt;
  for (int i = 0; i <= cnt; ++i) {
    gen(nums, st + cnt);
    path.push_back(nums[st]);
  }
  for (int i = 0; i <= cnt; ++i) path.pop_back();
}

vector<vector<int>> subsetsWithDup(vector<int>& nums) {
  sort(nums.begin(), nums.end());
  gen(nums, 0); 
  return res;
}
```

一种较好的方法：

```c++
vector<vector<int>> res;
vector<int> ans;

void gen(vector<int>& nums, int tg, int st) {
    if (tg == 0) {
        res.push_back(ans);
        return;
    }   
    for (int i = st; i < nums.size() && nums[i] <= tg; ++i) {
        if (i == st || nums[i] != nums[i - 1]) {
            ans.push_back(nums[i]);
            tg -= nums[i]; // 不把tg - nums[i]写到回溯函数里，这样更快
            gen(nums, tg, i + 1); 
            tg += nums[i];
            ans.pop_back();
        }
    }   
}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
    sort(candidates.begin(), candidates.end());
    gen(candidates, target, 0); 
    return res;
}

```



#### 20. 排列组合综合题

以leetcode 1079题为例。

[leetcode 1079. Letter Tile Possibilities](https://leetcode.com/problems/letter-tile-possibilities/)

很多题经常考的一种组合，人选箱 还是 箱选人。一般情况下，递归函数体里选循环次数少的。

```c++
unordered_map<int,int> dm; 
vector<int> cm; 
int pn = 0, ans, N;
void helper(int r) {
    for (int i = 0; i < cm.size(); ++i) {
        if (dm[cm[i]]) {
            --dm[cm[i]];
            if (r < N) ++ans;
            if (r < N - 1) helper(r + 1); 
            ++dm[cm[i]];
        }
    }   
}
int numTilePossibilities(string tiles) {
    N = tiles.size();
    for (auto c: tiles) ++dm[c];
    for (auto [k, v]: dm) cm.push_back(k);
    pn = 0, ans = 0;
    helper(0);
    return ans;
}
```



#### 21. KMP算法

```c++
// KMP生成自匹配串
vector<int> build_kmp(string s) {
    int n = s.length();
    vector<int> p[n]; 
    int j = 0, t = p[0] = -1;
    while (j < n - 1) {
        if (t < 0 || s[j] == s[t]) {
            ++j, ++t;
            p[j] = p[j] == p[t] ? p[t] : t;
        } else t = p[t];
    }
    return p;
}

// 主函数
int match(string a, string b) {
    int m = a.length(), n = b.length();
    if (m < n) return match(b, a); // 选择较短串为模式串
    vector<int> p = build_kmp(b); 
    int i = 0, j = 0; // 双串各自的指针
    while (i < m && j < n) {
        if (j < 0 || a[i] == b[j]) ++i, ++j;
        else j = p[j];
    }
    return i - j; // 返回最后一次匹配时模式串的初始位置；i - j <= m - n 则表示匹配成功，否则失配
}
```



#### 22. 回文串算法（manacher算法）

最长回文子串算法Manacher算法：

```c++
// 返回arr对应于扩展字符串的回文半径，arr[i] - 1则表示该处的实际最长回文子串
vector<int> mana(string s) {
    int n = s.length(), m = n << 1 | 1;
    string ss(m, '*'); for (int i = 0; i < n; ++i) ss[i<<1|1] = s[i];
    vector<int> arr(m); int C = -1, R = 0;
    for (int i = 0; i < m; ++i) {
        arr[i] = 0 < C * 2 - i ? min(R - i, arr[C * 2 - i]) : 1;
        while (0 <= i - arr[i] && i + arr[i] < m 
            && ss[i + arr[i]] == ss[i - arr[i]]) 
            ++arr[i];
        if (R < arr[i] + i) C = i, R = i + arr[i];
    }   
    return arr;
}

// 例：aacabadefeda 生成arr: 1 2 3 2 1 4 1 2 1 4 1 2 1 2 1 2 1 8 1 2 1 2 1 2 1 
```



#### 23. 读写方法

```
1. scanf, cin: sync_with_stdio(0); // 后者取消控制台同步
2. printf, cout:
3. fread/read: fseek, ftell, rewind; fflush();
4. mmap
5. fwrite
```

#### 24. 水库算法

随即选取链表中的元素：

```c++
class Solution {
    ListNode* head;
public:
    Solution(ListNode* n): head(n) {}
    int getRandom() {
        int ans = head->val;
        ListNode* node = head->next;
        int i = 2;
        while (node) {
            if ((rand() % i) == 0) {
                ans = node->val;
            }
            ++i;
            node = node->next;
        }
        return ans;
    }
};
```



## 2022-09-20

### 一、阶乘背诵

```
4! = 24 
5! = 120
6! = 720
7! = 5040
8! = 40320
9! = 362880
10! = 3628800
11! = 39916800
12! = 479001600
13! = 6227020800
14! = 87178291200
```

### 二、数据结构、算法框架

#### 数据结构：

```
1. 数组
2. 链表
3. 栈
4. 队列
5. 树
6. 图
7. 字典
8. 堆
9. 并查集
10. Trie树
11. 稀疏表
```

#### 算法框架

```
1. 排序算法
2. 遍历/枚举
3. 递归/回溯
4. 分治
5. 二分
6. 搜索（BFS、DFS、记忆化搜索）
7. 双指针
8. 筛法
9. 动态规划
10. 串匹配算法（KMP/BP）
11. 随即算法
12. 贪心算法
13. 位思想
14. 差分思想
15. 上限思想
16. 奇偶思想
```

### 三、nermeric/algorithm有用库函数

```c++
accumulate(nums.begin(),nums.end(),init, func);
partial_sum(nums.begin(),nums.end(),output, func);
iota(nums.begin(),nums.end(),n);
```

### 四、主定理

```
T(n) = aT(n/b) + f(n)
1) o(n^(log_b^a)), f(n) ~ O(T(n));
2) o(n^(log_b^a)lg(n)), f(n) - OO(T(n));
3) O(f(n));
```



### 五、编程经常犯的错误

1. 词不达意型

   1.1 想使用k时写成j，N写成n

   1.2 更换变量名后，忘改原先使用的地方； 

   1.3 变量名使用混乱，经常混用；

   1.4 map的count和[]经常混淆； 

   1.5 ==写成=

   1.6 要做到清楚自己定义的变量，了解函数的输入输出； 

   1.7 输入输出是否加了不必要的东西；

   1.8 定义了全局变量M后，又在int n , M = n / k；以为全局变量设置好了。	

2. 变与不变型

   2.1 循环中哪些值该变，哪些值不该变；是不是把不该变的变了，或者相反；

   2.2 for(auto & v: A) ，注意是否要用引用； 

   2.3 把初始化写到了循环外；

   2.4 回溯的标志清了吗；

   2.5 字符c转成c - 'a'了吗；

   2.6 循环变量++|--了吗？用反了吗？

3. 排序变秩型

   3.1 排序会改变原数组的秩，问问自己，原来的秩需不需要？

4. long long问题

   4.1 问题会出int界限吗？要不要long long？

   4.2 使用long long时，读入、写出、传值、运算、函数传参，是否都正确？

5. 边界问题

   5.1 多带值试代码，尤其是临界值；

   5.2 当临界时，检查循环变量是否符合规律或预期；

   5.3 多分析题目的隐藏条件，如：K是否一定是正数？K是否可以小于当前值；

6. 循环跳层问题

   6.1 一个break可以挑两层吗？你确定跳出的地方正确吗？

7. 模余问题

   7.1 除法不能直接模余；

   7.2 模余不要写+=| *=，最好分开写；

   7.3 时刻注意是否越界；	



## 2022-10-05

### 一、位运算小技巧

判断是否2的次方：

```
n > 0 && n ^ (n - 1) == 0
```

判断是否4的次方（仅有一个位为1，且1出现在奇数位）：在2的基础上，异或0x5555；

```
n > 0 && n ^ (n - 1) == 0 && n & 0x5555
```

交替位二进制数：

```
unsigned int a = n ^ (n >> 1);
return (a ^ (a + 1)) == 0; 
```

### 二、二维排序数组搜索技巧

​		这道题有一个简单的技巧:我们可以从右上角开始查找,若当前值大于待搜索值,我们向左移动一位;若当前值小于待搜索值,我们向下移动一位。如果最终移动到左下角时仍不等于待搜索值,则说明待搜索值不存在于矩阵中。



### 三、单调栈

Leetcode 739. https://leetcode.cn/problems/daily-temperatures/

题目描述：给定数组表示每日温度，求：对应的数组，表示第一次升温的日期。

利用单调栈可以快速求解。

###  四、寻找丢失数组

顾名思义，寻找丢失或者重复数字。一般可使用的技巧有：

1. 改数字法：将对应位置的数字改成负数、0，或者负绝对值等；
2. floyd判圈法



## 2022-10-06

### 一、超级丑数

Leetcode 313: https://leetcode.cn/problems/super-ugly-number/

给定质数数组primes，超级丑数是值质因数全部在primes中的数；

求第n大的超级丑数；

掌握动态规划的做法：

dp[i] = {dp[p1]*a1, dp[p2]*a2,dp[p3]*a3, ... , dp[pn]*an};

### 二、最速下降问题

困扰许久的物理数学问题，虽然一直都清楚答案是摆线，但不清楚是怎么计算出来的？

今天上网搜索得到答案，初步了解了下问题的解法：泛函分析、E-L方程。

### 三、五次方程无公式解

同上，也是困扰许久的问题，初步了解下前人是怎么解决问题的。



## 2022-10-07

对一类特殊但相似问题的思考总结：

### 一、 排列组合（选箱子选人）问题

类似问题容易混淆，容易搞不清楚代码逻辑，宜多做总结。

（add in 2022-10-24)

```
总结：
1. 一般而言，这类问题的解决方法，我称之为以下四类：1)人选箱（递归回溯）；2）箱选人（递归回溯）；3）bitmask技术（结合二分或DP）；4）mask子集技术（DP，递推）；
2. 就运行速度，一般而言：mask子集+DP>bitmask+DP>人选箱>箱选人；这也是建议的解决问题的方法优先顺序。注意：人选箱的剪枝条件越好，运行速度越快，需要多加思考；
3. 一般而言，“箱选人”较“人选箱”的优势在于，箱选人可以更容易结合DP记忆化输出。
4. 当箱选人，箱子（无区别）大小相同，即不放回时，箱选人使用：第n个箱子，服务id为【st, n）范围内的人，速度也很快，且方便DP；
```



（add in 2022-10-22）

#### 1. Leetcode 1723: [Find Minimum Time to Finish All Jobs](https://leetcode.cn/problems/find-minimum-time-to-finish-all-jobs/)

Description:

```
You are given an integer array jobs, where jobs[i] is the amount of time it takes to complete the ith job.

There are k workers that you can assign jobs to. Each job should be assigned to exactly one worker. The working time of a worker is the sum of the time it takes to complete all jobs assigned to them. Your goal is to devise an optimal assignment such that the maximum working time of any worker is minimized.

Return the minimum possible maximum working time of any assignment. 
```

Example:

```
Input: jobs = [1,2,4,7,8], k = 2
Output: 11
Explanation: Assign the jobs the following way:
Worker 1: 1, 2, 8 (working time = 1 + 2 + 8 = 11)
Worker 2: 4, 7 (working time = 4 + 7 = 11)
The maximum working time is 11.

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/find-minimum-time-to-finish-all-jobs
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

问题看起来像是：n个元素分成k组，求：每组和的最大值，使其最小的方案。

方法一：（比较符合我原先思维的解决方案）

方案一是“人选箱”的思路，对每一个id编号的箱子（此处为job），选择一个合适的人去执行它。

```c++
int helper(vector<int>& jobs, int id, vector<int>& load, int k) {
    int n = jobs.size(), m = load.size();
    if (n - id == k) { // 题目规定: k <= n，因此这一条可以判断递归终点，可以计算当前方案的结果
        int res = 0;
        for (int i = id; i < n; ++i) res = max(res, jobs[i]);
        for (int i = 0; i < m; ++i) {
            if (load[i]) res = max(res, load[i]);
            else break;
        }
        return res;
    }   
    int res = INT_MAX;
    for (int i = 0; i < m; ++i) {
        if (0 < i && !load[i - 1]) break;
        int bk = load[i] ? k : k - 1; // 判断剩下的箱子数
        load[i] += jobs[id];
        res = min(res, helper(jobs, id + 1, load, bk)); // 递归回溯
        load[i] -= jobs[id]; // 回溯，清标志
    }   
    return res;
}
int minimumTimeRequired(vector<int>& jobs, int k) {
    vector<int> load(k);
    return helper(jobs, 0, load, k); 
}
```

方法二：二分

因为结果的上下限容易计算，所以核心就是判断：能否有方案使得结果=v可行。

这里比较巧妙且核心的地方就是：用dp计算res=v的方案是否可行。

dp[n] = min(dp(m))，m是n的子集；

这里是“贪心算法”的思想，对于当前数n，取剩余箱子最多，或者一样多时，取剩余值最大的方案。

```c++
bool can_split(vector<int>& jobs, int n, int k, int v) {
    int tot = 1 << n;
    vector<pair<int,int>> dp(tot);
    dp[0] = {k, v}; 
    for (int i = 0; i < tot; ++i) {
        int x = dp[i].first, y = dp[i].second;
        printf("i: %d, x: %d, y: %d\n", i, x, y); 
        for (int j = 0; j < n; ++j) {
            if ((i & (1 << j)) == 0) {
                int now = i | (1 << j);
                int val = jobs[j], xx = x, yy = y;
                if (v < val) return false;
                if (val < y) yy = y - val;
                else if (val == y) --xx, yy = v;
                else --xx, yy = v - val;
                int a = dp[now].first, b = dp[now].second;
                if (a < xx || (a == xx && b < yy)) dp[now] = {xx, yy}; 
            }
        }
    }
    int ax = dp[tot - 1].first, bx = dp[tot - 1].second;
    return ax != 0 || (ax == 0 && bx == v);
}

int minimumTimeRequired(vector<int>& jobs, int k) {
    int n = jobs.size(), s = accumulate(jobs.begin(), jobs.end(), 0);
    int lo = s / k, hi = s + 1;
    while (lo < hi) {
        int md = (lo + hi) >> 1; 
        if (can_split(jobs, n, k, md)) hi = md;
        else lo = md + 1;
    }
    return lo;
}
```

方法三：mask子集技巧

```c++
#define L 10000
#define M 20
vector<vector<int>> dp(L, vector<int>(M));
int helper(int mask, int id, int k, vector<int>& mv) {
    if (dp[mask][id]) return dp[mask][id];
    if (!mask) return dp[mask][id] = INT_MAX;
    if (id + 1 == k) return dp[mask][id] = mv[mask];
    int res = INT_MAX;
    for (int i = mask; i; i = mask & (i - 1)) {
        //PR(i); PR(mask - i); PR(mv[i]);
        int c = max(mv[i], helper(mask - i, id + 1, k, mv));
        res = min(res, c); 
    }   
    return dp[mask][id] = res;
}
int minimumTimeRequired(vector<int>& jobs, int k) {
    int n = jobs.size(), mask = (1 << n); 
    vector<int> mv(mask + 1); 
    for (int i = 1; i < mask; ++i) {
        for (int j = n - 1; 0 <= j; --j) {
            if (i & (1 << j)) {
                mv[i] = mv[i - (1 << j)] + jobs[j];
                break;
            }
        }
    }   
    return helper(mask - 1, 0, k, mv);
}
```

#### 2. Leetcode 857:[Minimum Cost to Hire K Workers](https://leetcode.cn/problems/minimum-cost-to-hire-k-workers/)

问题描述

```
There are n workers. You are given two integer arrays quality and wage where quality[i] is the quality of the ith worker and wage[i] is the minimum wage expectation for the ith worker.

We want to hire exactly k workers to form a paid group. To hire a group of k workers, we must pay them according to the following rules:

    Every worker in the paid group should be paid in the ratio of their quality compared to other workers in the paid group.
    Every worker in the paid group must be paid at least their minimum wage expectation.

Given the integer k, return the least amount of money needed to form a paid group satisfying the above conditions. Answers within 10-5 of the actual answer will be accepted.

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/minimum-cost-to-hire-k-workers
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

样例：

```
Input: quality = [3,1,10,10,1], wage = [4,8,2,2,7], k = 3
Output: 30.66667
Explanation: We pay 4 to 0th worker, 13.33333 to 2nd and 3rd workers separately.

来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/minimum-cost-to-hire-k-workers
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

本质上并非排列组合问题。用优先级队列统计最小和即可：

```c++
double mincostToHireWorkers(vector<int>& quality, vector<int>& wage, int k) {
    int n = quality.size();
    vector<int> qr(n);
    iota(qr.begin(), qr.end(), 0); 
    sort(qr.begin(), qr.end(), [&](int a, int b) {
        return wage[a] * quality[b] < wage[b] * quality[a];
    }); 
    priority_queue<int> q;
    int sum = 0;
    for (int i = 0; i < k; ++i) {
        int rk = qr[i];
        q.push(quality[rk]);
        sum += quality[rk];
    }   
    int p = qr[k - 1]; 
    double res = (double) wage[p] * sum / quality[p];
    for (int i = k; i < n; ++i) {
        int t = q.top(), rk = qr[i]; q.pop();
        sum += quality[rk] - t;
        res = min(res, (double) wage[rk] * sum / quality[rk]);
        q.push(quality[rk]);
    }
    return res;
}
```

#### 3. Leecode 1986:[Minimum Number of Work Sessions to Finish the Tasks](https://leetcode.cn/problems/minimum-number-of-work-sessions-to-finish-the-tasks/)

问题描述：

```
There are n tasks assigned to you. The task times are represented as an integer array tasks of length n, where the ith task takes tasks[i] hours to finish. A work session is when you work for at most sessionTime consecutive hours and then take a break.

You should finish the given tasks in a way that satisfies the following conditions:

    If you start a task in a work session, you must complete it in the same work session.
    You can start a new task immediately after finishing the previous one.
    You may complete the tasks in any order.

Given tasks and sessionTime, return the minimum number of work sessions needed to finish all the tasks following the conditions above.

The tests are generated such that sessionTime is greater than or equal to the maximum element in tasks[i].
```

样例：

```
Input: tasks = [3,1,3,1,1], sessionTime = 8
Output: 2
Explanation: You can finish the tasks in two work sessions.
- First work session: finish all the tasks except the last one in 3 + 1 + 3 + 1 = 8 hours.
- Second work session: finish the last task in 1 hour.
```

方法一、箱选人

顾名思义，考查满足当前箱子的条件，然后递归回溯下一个箱子；比较方便用dp记录状态；

```c++
#define L 20000
#define M 20
int K;
int dp[L][M];
int helper(vector<int>& tasks, int k, int mask) {
    int n = tasks.size(), res = n << 1;
    if (!mask) return k == K ? 0 : 1;
    if (dp[mask][k]) return dp[mask][k];
    for (int i = 0; i < n; ++i) {
        if (mask & (1 << i)) {
            int nmask = mask ^ (1 << i); 
            if (tasks[i] < k) {
                res = min(res, helper(tasks, k - tasks[i], nmask));
            } else if (tasks[i] == k) {
                res = min(res, 1 + helper(tasks, K, nmask));
            } else {
                res = min(res, 1 + helper(tasks, K - tasks[i], nmask));
            }
        }
    }
    return dp[mask][k] = res;
}
int minSessions(vector<int>& tasks, int sessionTime) {
    int n = tasks.size(), mask = 1 << n;
    K = sessionTime;
    memset(dp, 0, sizeof dp);
    return helper(tasks, K, mask - 1);
}
```

方法二：人选箱

顾名思义，考察当前人可用的箱子，然后递归回溯下一个；优点：逻辑比较清楚

此处需要注意，用ans剪枝；

```c++
int M, ans;
int helper(vector<int>& tasks, int id, vector<int>& box, int num) {
    int n = tasks.size();
    if (id == n) { return ans = min(ans, num); }
    int res = n;
    for (int i = 0; i < n; ++i) {
        if (0 < i && !box[i - 1]) break;
        if (tasks[id] + box[i] <= M) {
            int bf = box[i], bnum = box[i] ? num : num + 1;
            if (ans < bnum) continue;
            box[i] += tasks[id];
            res = min(res, helper(tasks, id + 1, box, bnum));
            box[i] = bf; 
        }
    }   
    return res;
}
int minSessions(vector<int>& tasks, int sessionTime) {
    int n = tasks.size();
    M = sessionTime;
    vector<int> box(n);
    ans = n;
    return helper(tasks, 0, box, 0);
}
```

方法三：bitmask技术

```c++
int minSessions(vector<int>& tasks, int sessionTime) {
    int n = tasks.size(), mask = 1 << n;
    vector<pair<int,int>> dp(mask, {n, 0});
    int M = sessionTime;
    dp[0] = {1, M}; 
    for (int i = 0; i < mask; ++i) {
        auto [x, y] = dp[i];
        for (int j = 0; j < n; ++j) {
            int tm = 1 << j;
            if (~i & tm) {
                int now = i ^ tm, v = tasks[j], xx = x, yy = y;
                auto [a, b] = dp[now];
                if (v < yy) yy -= v;
                else if (v == yy) yy = M, ++xx;
                else yy = M - v, ++xx;
                if (xx < a || (xx == a && b < yy)) dp[now] = {xx, yy};
            }
        }
    }
    auto [a, b] = dp[mask - 1];
    return b == M ? a - 1 : a;
}
```

方法四：mask子集技术



#### 4. Leetcode 1799: [Maximize Score After N Operations](https://leetcode.cn/problems/maximize-score-after-n-operations/)

题目描述：

```
You are given nums, an array of positive integers of size 2 * n. You must perform n operations on this array.

In the ith operation (1-indexed), you will:

    Choose two elements, x and y.
    Receive a score of i * gcd(x, y).
    Remove x and y from nums.

Return the maximum score you can receive after performing n operations.

The function gcd(x, y) is the greatest common divisor of x and y.
```

样例1：

```
Input: nums = [1,2]
Output: 1
Explanation: The optimal choice of operations is:
(1 * gcd(1, 2)) = 1
```

样例2：

```
Input: nums = [3,4,6,8]
Output: 11
Explanation: The optimal choice of operations is:
(1 * gcd(3, 6)) + (2 * gcd(4, 8)) = 3 + 8 = 11
```

样例3

```
Input: nums = [1,2,3,4,5,6]
Output: 14
Explanation: The optimal choice of operations is:
(1 * gcd(1, 5)) + (2 * gcd(2, 4)) + (3 * gcd(3, 6)) = 1 + 4 + 9 = 14
```

方法一：箱选人

重点是dp技术，记录mask和结尾箱子的id；

```c++
map<pair<int,int>,int> dp; 
int helper(vector<int>& nums, int mask, int lv) {
    int n = nums.size(), m = n / 2, ans = 0;
    if (!mask) return 0;
    if (dp.count({mask, lv})) return dp[{mask,lv}];
    int ne = __builtin_popcount(mask), id = ne + 1 >> 1;
    for (int i = 0; i < n; ++i) {
        int cn = 1 << i;
        if (mask & cn) {
            int nmask = mask ^ cn; 
            int blv = __gcd(lv, nums[i]);
            int rm = lv ? blv * id + helper(nums, nmask, 0) : helper(nums, nmask, blv);
            ans = max(ans, rm);
        }
    }   
    return dp[{mask,lv}] = ans;
}
int maxScore(vector<int>& nums) {
    int n = nums.size(), m = n / 2, mask = 1 << n;
    return helper(nums, mask - 1, 0); 
}

```

方法二：人选箱，重点是减枝技术和输出注意；

```c++
int com[14];
int helper(vector<int>& nums, int id, vector<vector<int>>& buck) {
    int n = nums.size(), m = n / 2, ans = 0;
    if (id == n) {
        for (int i = 0; i < m; ++i) com[i] = __gcd(buck[i][0], buck[i][1]);
        sort(com, com + m); 
        for (int i = 0; i < m; ++i) ans += (i + 1) * com[i];
        return ans;
    }   
    for (int i = 0; i < m; ++i) {
        int sz = buck[i].size();
        if (sz == 2) continue;
        buck[i].emplace_back(nums[id]);
        ans = max(ans, helper(nums, id + 1, buck));
        buck[i].pop_back();
        if (sz == 0) break;
    }   
    return ans;
}
int maxScore(vector<int>& nums) {
    int n = nums.size(), m = n / 2, mask = 1 << n;
    vector<vector<int>> bucket(m);
    return helper(nums, 0, bucket);
}

```

#### 5. Leetcode 1681: [Minimum Incompatibility](https://leetcode.cn/problems/minimum-incompatibility/)

题目描述：

```
You are given an integer array nums​​​ and an integer k. You are asked to distribute this array into k subsets of equal size such that there are no two equal elements in the same subset.

A subset's incompatibility is the difference between the maximum and minimum elements in that array.

Return the minimum possible sum of incompatibilities of the k subsets after distributing the array optimally, or return -1 if it is not possible.

A subset is a group integers that appear in the array with no particular order.

 

Example 1:

Input: nums = [1,2,1,4], k = 2
Output: 4
Explanation: The optimal distribution of subsets is [1,2] and [1,4].
The incompatibility is (2-1) + (4-1) = 4.
Note that [1,1] and [2,4] would result in a smaller sum, but the first subset contains 2 equal elements.

Example 2:

Input: nums = [6,3,8,1,3,1,2,2], k = 4
Output: 6
Explanation: The optimal distribution of subsets is [1,2], [2,3], [6,8], and [1,3].
The incompatibility is (2-1) + (3-2) + (8-6) + (3-1) = 6.

Example 3:

Input: nums = [5,3,3,6,3,3], k = 3
Output: -1
Explanation: It is impossible to distribute nums into 3 subsets where no two elements are equal in the same subset.

 

Constraints:

    1 <= k <= nums.length <= 16
    nums.length is divisible by k
    1 <= nums[i] <= nums.length
```

方法一：人选箱

```c++
int M, K;
vector<vector<int>> buck;
int helper(vector<int>& nums, int id) {
    int n = nums.size(), ans = 0;
    if (id == n) {
        for (int i = 0; i < K; ++i) ans += *(buck[i].rbegin()) - *(buck[i].begin());
        return ans;
    }   
    ans = INT_MAX;
    for (int i = 0; i < K; ++i) {
        int sz = buck[i].size();
        if (sz == M) continue;
        if (0 < sz && buck[i][sz - 1] == nums[id]) continue;
        buck[i].emplace_back(nums[id]);
        ans = min(ans, helper(nums, id + 1));
        buck[i].pop_back();
        if (sz == 0) break;
    }   
    return ans;
}

int minimumIncompatibility(vector<int>& nums, int k) {
    int n = nums.size(); M = n / k, K = k;
    sort(nums.begin(), nums.end());
    buck = vector<vector<int>>(K);
    int ans = helper(nums, 0); 
    return ans == INT_MAX ? -1 : ans;
}
```

方法二：mask子集

mask子集，用递归容易超时，直接用递推+动态规划比较好。

```c++
int M, K;
int dp[100000];
int minimumIncompatibility(vector<int>& nums, int k) {
    int n = nums.size(), mask = 1 << n; M = n / k, K = k;
    sort(nums.begin(), nums.end());
    memset(dp, -1, sizeof dp);
    for (int i = 0; i < mask; ++i) {
        int no = __builtin_popcount(i);
        if (no == M) {
            int lm = 0, ln = INT_MAX, bf = -1, j = 0;
            for (; j < n; ++j) if (i & (1 << j)) {
                if (nums[j] == bf) break;
                lm = max(lm, nums[j]), ln = min(ln, nums[j]), bf = nums[j];
            }
            if (j == n) {
                dp[i] = lm - ln; 
            }
        }
    }   
    for (int i = 1; i < mask; ++i) {
        int no = __builtin_popcount(i);
        if (no == M) continue;
        if (no % M == 0) {
            for (int j = i; j; j = i & (j - 1)) {
                if (0 <= dp[j] && 0 <= dp[i ^ j]) {
                    int r = dp[j] + dp[i ^ j]; 
                    dp[i] = dp[i] < 0 ? r : min(dp[i], r); 
                }
            }
        }
    }   
    return dp[mask - 1]; 
}
```

#### 6. Leetcode 1655: [Distribute Repeating Integers](https://leetcode.cn/problems/distribute-repeating-integers/)

题目描述：

```
You are given an array of n integers, nums, where there are at most 50 unique values in the array. You are also given an array of m customer order quantities, quantity, where quantity[i] is the amount of integers the ith customer ordered. Determine if it is possible to distribute nums such that:

    The ith customer gets exactly quantity[i] integers,
    The integers the ith customer gets are all equal, and
    Every customer is satisfied.

Return true if it is possible to distribute nums according to the above conditions.

Example 1:

Input: nums = [1,2,3,4], quantity = [2]
Output: false
Explanation: The 0th customer cannot be given two different integers.

Example 2:

Input: nums = [1,2,3,3], quantity = [2]
Output: true
Explanation: The 0th customer is given [3,3]. The integers [1,2] are not used.

Example 3:

Input: nums = [1,1,2,2], quantity = [2,2]
Output: true
Explanation: The 0th customer is given [1,1], and the 1st customer is given [2,2].

Constraints:

    n == nums.length
    1 <= n <= 105
    1 <= nums[i] <= 1000
    m == quantity.length
    1 <= m <= 10
    1 <= quantity[i] <= 105
    There are at most 50 unique values in nums.
```

方法一：人选箱

```c++
int M, N;
unordered_map<int,int> bum;
int buck[50];
bool helper(vector<int>& qu, int id) {
    if (id == M) return true;
    for (int i = 0; i < N; ++i) {
        if (buck[i] < qu[id]) continue;
        buck[i] -= qu[id];
        bool r = helper(qu, id + 1); 
        if (r) return true;
        buck[i] += qu[id];
    }   
    return false;
}
bool canDistribute(vector<int>& nums, vector<int>& quantity) {
    M = quantity.size();
    for (auto& v: nums) bum[v]++;
    N = 0;
    for (auto& [k, v]: bum) buck[N++] = v;
    auto f = [&](int& a, int& b) {
        return b < a;
    };  
    sort(buck, buck + N, f); 
    sort(quantity.begin(), quantity.end(), f); 
    return helper(quantity, 0); 
}
```



未通过方法（箱选人，超时）：

```c++
int N, M;
unordered_map<int,int> bum;
int buck[50];
map<vector<int>,int> dm; 
bool helper(vector<int>& quan, int id, int mask) {
    if (mask == (1 << M) - 1) return true;
    if (id == N) return false;
    if (dm.count({mask,id,buck[id]})) return dm[{mask,id,buck[id]}];
    for (int i = 0; i < M; ++i) {
        if (mask & (1 << i)) continue;
        if (buck[id] < quan[i]) {
            bool r = helper(quan, id + 1, mask);
            if (r) return dm[{mask,id,buck[id]}] = true;
            continue;
        }
        mask ^= (1 << i); 
        buck[id] -= quan[i];
        bool r = helper(quan, id, mask);
        if (r) return dm[{mask,id,buck[id]}]= true;
        buck[id] += quan[i];
        mask ^= (1 << i); 
    }   
    return dm[{mask,id,buck[id]}]= false;
}
bool canDistribute(vector<int>& nums, vector<int>& quantity) {
    M = quantity.size();
    for (auto v: nums) ++bum[v];
    N = 0;
    for (auto [k, v]: bum) buck[N++] = v;
    sort(quantity.begin(), quantity.end(), [&](int& a, int& b){ 
        return b < a;
    }); 
    return helper(quantity, 0, 0); 
}
```



#### 7. Leetcode 1815: [Maximum Number of Groups Getting Fresh Donuts](https://leetcode.cn/problems/maximum-number-of-groups-getting-fresh-donuts/)

问题描述：

```
There is a donuts shop that bakes donuts in batches of batchSize. They have a rule where they must serve all of the donuts of a batch before serving any donuts of the next batch. You are given an integer batchSize and an integer array groups, where groups[i] denotes that there is a group of groups[i] customers that will visit the shop. Each customer will get exactly one donut.

When a group visits the shop, all customers of the group must be served before serving any of the following groups. A group will be happy if they all get fresh donuts. That is, the first customer of the group does not receive a donut that was left over from the previous group.

You can freely rearrange the ordering of the groups. Return the maximum possible number of happy groups after rearranging the groups.

Example 1:

Input: batchSize = 3, groups = [1,2,3,4,5,6]
Output: 4
Explanation: You can arrange the groups as [6,2,4,5,1,3]. Then the 1st, 2nd, 4th, and 6th groups will be happy.

Example 2:

Input: batchSize = 4, groups = [1,3,2,5,2,2,1,6]
Output: 4

Constraints:

    1 <= batchSize <= 9
    1 <= groups.length <= 30
    1 <= groups[i] <= 109
```

方法一：箱选人+DP

这里的DP直接图方便，使用map做秩；实际上可以用最多8进制表示key；这道题如果用“人选箱”则不太好做，数量太大且剪枝不太方便，暂时没想到用“人选箱”的方法。

```c++
int M, BT, SUM;
map<int,int> bm; 
map<pair<map<int,int>,int>,int> dp; 
int helper(int lv) {
    if (SUM == 0) return 0;
    if (dp.count({bm, lv})) return dp[{bm,lv}];
    int ans = 0;
    for (auto& [k, v]: bm) {
        if (!v) continue;
        --SUM; --bm[k];
        int nlv = (k + lv) % BT; 
        ans = max(ans, helper(nlv));
        ++SUM; ++bm[k];
    }   
    if (!lv) ans += 1;
    return dp[{bm,lv}] = ans;
}
int maxHappyGroups(int bt, vector<int>& groups) {
    int n = groups.size();
    for (auto& v: groups) ++bm[v % bt];
    int ans = bm[0];
    bm[0] = 0;
    for (int i = 1; i < bt - i; ++i) {
        int r = min(bm[i], bm[bt - i]);
        bm[i] -= r, bm[bt - i] -= r;
        ans += r;
    }   
    if (~bt & 1) { ans += bm[bt >> 1] >> 1; bm[bt >> 1] %= 2; }
    M = bm.size(), BT = bt; 
    for (auto& [k, v]: bm) SUM += v;
    return ans + helper(0);
}
```

#### 8. Leetcode 40: [Combination Sum II](https://leetcode.cn/problems/combination-sum-ii/)

题目描述：

```
Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.

Each number in candidates may only be used once in the combination.

Note: The solution set must not contain duplicate combinations.

Example 1:

Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]

Example 2:

Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]

Constraints:

    1 <= candidates.length <= 100
    1 <= candidates[i] <= 50
    1 <= target <= 30
```

方法一：人选箱：

组合问题与“人选箱、箱选人”类似，需要注意的是：箱子只有一个、有无重复元素、放回还是不放回；

```c++
set<vector<int>> sv; 
vector<int> path;
map<int,int> um; 
void helper(map<int,int>::iterator it, int lv) {
    if (lv == T) { sv.insert(path); return; }
    if (it == um.end()) return;
    auto k = it->first, v = it->second;
    int i = 0;
    for (; i <= v; ++i) {
        if (T < lv + i * k) break;
        helper(next(it), lv + i * k); 
        path.emplace_back(k);
    }   
    while (i--) path.pop_back();
}
vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
    for (auto& v: candidates) um[v]++;
    T = target;
    helper(um.begin(), 0); 
    vector<vector<int>> ans;
    for (auto& v: sv) ans.emplace_back(v);
    return ans;
}
```

方法二：箱选人：只有一个箱子时，箱选人和人选箱时一样的。下面是将候选数组展开的写法：

```c++
vector<vector<int>> res;
vector<int> ans;

void gen(vector<int>& nums, int tg, int st) {
    if (tg == 0) {
        res.push_back(ans);
        return;
    }   
    for (int i = st; i < nums.size() && nums[i] <= tg; ++i) {
        if (i == st || nums[i] != nums[i - 1]) {
            ans.push_back(nums[i]);
            tg -= nums[i]; // 不把tg - nums[i]写到回溯函数里，这样更快
            gen(nums, tg, i + 1); 
            tg += nums[i];
            ans.pop_back();
        }
    }   
}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
    sort(candidates.begin(), candidates.end());
    gen(candidates, target, 0); 
    return res;
}
```



```
1723\857\1986\1799|1681|1655|1815|40
```



### 二、灌水问题、水流问题、矩阵搜索问题

如何确定思路，简化思路；若是DFS/BFS，如何快速写出？



### 三、c++容器list的特殊接口

```
与vector类似的接口：
front()、back()、push_front()、push_back()、pop_front()、pop_back()、insert()、erase()
不同的：
splice()函数
emplace()函数：相当于插入的作用，但只能插入一个元素 (C++ 11的函数）

```



## 2022-10-08

### 一、 （博弈）极大极小问题（一些博弈游戏的策略问题）

各种棋类、决策类问题的解答。

[add in 2022-10-24]

这类问题，简单来说，就是分步决策，每一步可以有不同的优化目标（当然，有时候看起来不同的优化目标可以合并）。

大部分问题可以用：状态转移类DP解决，否则用分步递归+记忆化。

#### 1. Leetcode 1690[Stone Game VII](https://leetcode.cn/problems/stone-game-vii/)

题目描述：

```
Alice and Bob take turns playing a game, with Alice starting first.

There are n stones arranged in a row. On each player's turn, they can remove either the leftmost stone or the rightmost stone from the row and receive points equal to the sum of the remaining stones' values in the row. The winner is the one with the higher score when there are no stones left to remove.

Bob found that he will always lose this game (poor Bob, he always loses), so he decided to minimize the score's difference. Alice's goal is to maximize the difference in the score.

Given an array of integers stones where stones[i] represents the value of the ith stone from the left, return the difference in Alice and Bob's score if they both play optimally.

Example 1:

Input: stones = [5,3,1,4,2]
Output: 6
Explanation: 
- Alice removes 2 and gets 5 + 3 + 1 + 4 = 13 points. Alice = 13, Bob = 0, stones = [5,3,1,4].
- Bob removes 5 and gets 3 + 1 + 4 = 8 points. Alice = 13, Bob = 8, stones = [3,1,4].
- Alice removes 3 and gets 1 + 4 = 5 points. Alice = 18, Bob = 8, stones = [1,4].
- Bob removes 1 and gets 4 points. Alice = 18, Bob = 12, stones = [4].
- Alice removes 4 and gets 0 points. Alice = 18, Bob = 12, stones = [].
The score difference is 18 - 12 = 6.

Example 2:

Input: stones = [7,90,5,1,100,10,10,2]
Output: 122

Constraints:

    n == stones.length
    2 <= n <= 1000
    1 <= stones[i] <= 1000
```

方法：分步DP（当然，状态转移可以合并，这里特别分开写时为了一般化）

```c++
#define L 1010
int da[L][L], db[L][L], sa[L];
int stoneGameVII(vector<int>& stones) {
    int n = stones.size();
    partial_sum(stones.begin(), stones.end(), sa + 1); 
    for (int i = 1; i <= n; ++i) {
        for (int j = 0; j <= n - i; ++j) {
            if ((n - i) & 1) {
                db[i][j] = min(da[i - 1][j] - sa[i + j - 1] + sa[j], da[i - 1][j + 1] - sa[i + j] + sa[j + 1]); // 状态b的转移方程
            }
            else {
                da[i][j] = max(db[i - 1][j] + sa[i + j - 1] - sa[j], db[i - 1][j + 1] + sa[i + j] - sa[j + 1]); // 状态a的转移方程
            }
        }
    }   
    return da[n][0];
}
```



#### 2. Leetcode 1686: [Stone Game VI](https://leetcode.cn/problems/stone-game-vi/)

题目描述：

```
Alice and Bob take turns playing a game, with Alice starting first.

There are n stones in a pile. On each player's turn, they can remove a stone from the pile and receive points based on the stone's value. Alice and Bob may value the stones differently.

You are given two integer arrays of length n, aliceValues and bobValues. Each aliceValues[i] and bobValues[i] represents how Alice and Bob, respectively, value the ith stone.

The winner is the person with the most points after all the stones are chosen. If both players have the same amount of points, the game results in a draw. Both players will play optimally. Both players know the other's values.

Determine the result of the game, and:

    If Alice wins, return 1.
    If Bob wins, return -1.
    If the game results in a draw, return 0.

Example 1:

Input: aliceValues = [1,3], bobValues = [2,1]
Output: 1
Explanation:
If Alice takes stone 1 (0-indexed) first, Alice will receive 3 points.
Bob can only choose stone 0, and will only receive 2 points.
Alice wins.

Example 2:

Input: aliceValues = [1,2], bobValues = [3,1]
Output: 0
Explanation:
If Alice takes stone 0, and Bob takes stone 1, they will both have 1 point.
Draw.

Example 3:

Input: aliceValues = [2,4,3], bobValues = [1,6,7]
Output: -1
Explanation:
Regardless of how Alice plays, Bob will be able to have more points than Alice.
For example, if Alice takes stone 1, Bob can take stone 2, and Alice takes stone 0, Alice will have 6 points to Bob's 7.
Bob wins.
Constraints:

    n == aliceValues.length == bobValues.length
    1 <= n <= 105
    1 <= aliceValues[i], bobValues[i] <= 100
```

双层DP：

```c++
    int stoneGameVI(vector<int>& aliceValues, vector<int>& bobValues) {
        int n = aliceValues.size();
        vector<int> dp(n);
        iota(dp.begin(), dp.end(), 0);
        sort(dp.begin(), dp.end(), [&](int& a, int& b) {
            return aliceValues[a] + bobValues[a] > aliceValues[b] + bobValues[b];
        });
        int ans = 0;
        for (int i = 0; i < n; ++i) ans += (i & 1) ? -bobValues[dp[i]] : aliceValues[dp[i]];
        return 0 < ans ? 1 : (ans ? -1 : 0);
    }
```

[add in 2022-11-15]

### 3. Leetcode 913: [Cat and Mouse](https://leetcode.cn/problems/cat-and-mouse/)

这道题用DP做会超时，本题的主要难点在于0值点的判定；这道题初做的时候想了蛮久，其原因就是，不知道什么状态下可以确定返回0；看了解析后知道，可以根据总步数确定0值点，跟据抽屉原理，步数超过一定值后，按照最优原理，仍然不能确定状态的必然时和局。

但这道题更巧妙的做法是正向DP，根据递归的原则递推，会发现实际上是一个关键路径的算法，非常巧妙。不再赘述，用代码说明问题

```c++
#define L 110
vector<vector<int>> gr;
int dp[L][L][2], dg[L][L][2];
queue<vector<int>> sp;
int catMouseGame(vector<vector<int>>& graph) {
    int n = graph.size();
    // init
    for (int i = 1; i < n; ++i) {
        dp[0][i][0] = dp[0][i][1] = 1;
        vector<int> a({0,i,0}), b({0,i,1});
        sp.push(a);
        sp.push(b);
    }
    for (int i = 1; i < n; ++i) {
        dp[i][i][0] = dp[i][i][1] = 2;
        vector<int> a({i,i,0}), b({i,i,1});
        sp.push(a);
        sp.push(b);
    }   
    for (int i = 0; i < n; ++i) {
        for (int j = 1; j < n; ++j) {
            dg[i][j][0] = graph[i].size();
            dg[i][j][1] = graph[j].size();
            for (auto& v: graph[j]) if (!v) --dg[i][j][1];
        }
    }   
    // key path algorithm
    while (!sp.empty()) {
        auto v = sp.front(); sp.pop();
        auto m = v[0], c = v[1], w = v[2];
        //PRV(v);
        int t = dp[m][c][w];
        //PR(t);
        if (w & 1) { // current is cat, then last is mouse
             for (auto& v: graph[m]) {
                if (dp[v][c][0]) continue;
                if (t == 1) {
                    dp[v][c][0] = 1;
                    sp.push({v,c,0});
                } else {
                    dg[v][c][0]--;
                    if (dg[v][c][0] == 0) {
                        dp[v][c][0] = 2;
                        sp.push({v,c,0});
                    }
                }
            }
        } else {
            for (auto& v: graph[c]) {
                if (!v) continue;
                if (dp[m][v][1]) continue;
                if (t == 2) {
                    dp[m][v][1] = 2;
                    sp.push({m,v,1});
                } else {
                    dg[m][v][1]--;
                    if (dg[m][v][1] == 0) {
                        dp[m][v][1] = 1;
                        sp.push({m,v,1});
                    }
                }
            }
        }
    }
    // final answer
    return dp[1][2][0];
}
```

### 4. Leetcode 1728: [Cat and Mouse II](https://leetcode.cn/problems/cat-and-mouse-ii/)

说是上一题的进阶，但个人感觉这道题更容易做，因为可以用递归+记忆化得到答案。不过写出来确实繁琐，实际上这道题可以沿用关键路径的思想。

需要注意的是审题，题目中强调，只能沿一个方向走n步，而不是任意走n步，这里调试了许久。

```
LC 913\1728|1690|1686
```



### 二、扫描线算法

(add in 2022-10-27) 

扫瞄线算法总结：

```
Foreach(ai):
	percept < ai in queue;
	remove all < ai in queue;
	update new == ai to queue;
```

需要注意的就是，每个新节点可以时起点，也可是终点，需要在每一个端点都判断一次；

#### 1. Leetcode 1705: [Maximum Number of Eaten Apples](https://leetcode.cn/problems/maximum-number-of-eaten-apples/)

题目描述：

```
There is a special kind of apple tree that grows apples every day for n days. On the ith day, the tree grows apples[i] apples that will rot after days[i] days, that is on day i + days[i] the apples will be rotten and cannot be eaten. On some days, the apple tree does not grow any apples, which are denoted by apples[i] == 0 and days[i] == 0.

You decided to eat at most one apple a day (to keep the doctors away). Note that you can keep eating after the first n days.

Given two integer arrays days and apples of length n, return the maximum number of apples you can eat.

Example 1:

Input: apples = [1,2,3,5,2], days = [3,2,1,4,2]
Output: 7
Explanation: You can eat 7 apples:
- On the first day, you eat an apple that grew on the first day.
- On the second day, you eat an apple that grew on the second day.
- On the third day, you eat an apple that grew on the second day. After this day, the apples that grew on the third day rot.
- On the fourth to the seventh days, you eat apples that grew on the fourth day.

Example 2:

Input: apples = [3,0,0,0,0,2], days = [3,0,0,0,0,2]
Output: 5
Explanation: You can eat 5 apples:
- On the first to the third day you eat apples that grew on the first day.
- Do nothing on the fouth and fifth days.
- On the sixth and seventh days you eat apples that grew on the sixth day.

Constraints:

    n == apples.length == days.length
    1 <= n <= 2 * 104
    0 <= apples[i], days[i] <= 2 * 104
    days[i] = 0 if and only if apples[i] = 0.
```

注意到：只要在当天前，把所有失效的苹果除掉或者吃完的苹果去掉即可。

```c++
#define L 40010
int eatenApples(vector<int>& apples, vector<int>& days) {
    int n = apples.size();
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;
    int ans = 0;
    for (int i = 0; i < L; ++i) {
        if (i < n) pq.push({i + days[i], apples[i]});
        if (n <= i && pq.empty()) break;
        while (pq.size()) {
            auto [ld, lv] = pq.top(); pq.pop();
            if (i < ld) {
                --lv, ++ans;
                if (lv) pq.push({ld,lv});
                break;
            }
        }
    }   
    return ans;
}
```

#### 2. Leetcode 1851: [Minimum Interval to Include Each Query](https://leetcode.cn/problems/minimum-interval-to-include-each-query/)

题目描述：

```
You are given a 2D integer array intervals, where intervals[i] = [lefti, righti] describes the ith interval starting at lefti and ending at righti (inclusive). The size of an interval is defined as the number of integers it contains, or more formally righti - lefti + 1.

You are also given an integer array queries. The answer to the jth query is the size of the smallest interval i such that lefti <= queries[j] <= righti. If no such interval exists, the answer is -1.

Return an array containing the answers to the queries.

Example 1:

Input: intervals = [[1,4],[2,4],[3,6],[4,4]], queries = [2,3,4,5]
Output: [3,3,1,4]
Explanation: The queries are processed as follows:
- Query = 2: The interval [2,4] is the smallest interval containing 2. The answer is 4 - 2 + 1 = 3.
- Query = 3: The interval [2,4] is the smallest interval containing 3. The answer is 4 - 2 + 1 = 3.
- Query = 4: The interval [4,4] is the smallest interval containing 4. The answer is 4 - 4 + 1 = 1.
- Query = 5: The interval [3,6] is the smallest interval containing 5. The answer is 6 - 3 + 1 = 4.

Example 2:

Input: intervals = [[2,3],[2,5],[1,8],[20,25]], queries = [2,19,5,22]
Output: [2,-1,4,6]
Explanation: The queries are processed as follows:
- Query = 2: The interval [2,3] is the smallest interval containing 2. The answer is 3 - 2 + 1 = 2.
- Query = 19: None of the intervals contain 19. The answer is -1.
- Query = 5: The interval [2,5] is the smallest interval containing 5. The answer is 5 - 2 + 1 = 4.
- Query = 22: The interval [20,25] is the smallest interval containing 22. The answer is 25 - 20 + 1 = 6.

Constraints:

    1 <= intervals.length <= 105
    1 <= queries.length <= 105
    intervals[i].length == 2
    1 <= lefti <= righti <= 107
    1 <= queries[j] <= 107
```

扫瞄线算法：

```c++
using pri=pair<int,int>;
vector<int> minInterval(vector<vector<int>>& intervals, vector<int>& queries) {
    int n = intervals.size(), m = queries.size();
    vector<int> ans(m, -1);
    vector<pri> nq(m);
    for (int i = 0; i < m; ++i) nq[i] = {queries[i], i}; 
    sort(nq.begin(), nq.end());
    priority_queue<pri,vector<pri>,greater<pri>> pq; 
    sort(intervals.begin(), intervals.end());
    int id = 0, lv = intervals[0][0], a, b, e, l = -1, i = 0;
    while (i < n || !pq.empty()) {
        // get cur point
        if (n <= i) { a = pq.top().second; }
        else if (pq.empty()) a = intervals[i][0];
        else a = min(intervals[i][0], e = pq.top().second);
        // percept a)
        l = (pq.empty()) ? -1 : pq.top().first;
        while (id < m) {
            auto& [xx, yy] = nq[id];
            if (a <= xx) break;
            ans[yy] = l;
            ++id;
        }
        // remove <= a
        while (!pq.empty() && pq.top().second <= a) pq.pop();
        // update new point >= a
        while (i < n && intervals[i][0] == a) {
            b = intervals[i++][1];
            pq.push({b - a + 1, b + 1});
        }
    }   
    return ans;
}
```



(add in 2022-10-30)

##### 3. Leetcode 1353: [Maximum Number of Events That Can Be Attended](https://leetcode.cn/problems/maximum-number-of-events-that-can-be-attended/)

扫瞄线算法，以下按数扫描

```c++
#define L 100010
int maxEvents(vector<vector<int>>& events) {
    multimap<int,int> dm; 
    for (auto& v: events) {
        int a = v[0], b = v[1];
        dm.insert({a, b});
    }   
    priority_queue<int,vector<int>,greater<int>> q;
    int ans = 0;
    auto it = dm.begin();
    for (int i = 1; i < L; ++i) {
        while (it != dm.end() && it->first == i) {
            q.push(it->second);
            ++it;
        }
        while (!q.empty() && q.top() < i) q.pop();
        if (!q.empty()) ++ans, q.pop();
    }   
    return ans;
}
```



### 三、设计符合要求的数据结构

看到要求O(1)时间完成插入、删除、查找的题目，首先要想到哈系表，一般都是哈系表+某种数据结构（向量/链表）等实现。



### 四、容器非常有用的接口prev、next

作用于iterator，返回之前或者之后n个（默认为1）位置的iterator

注意emplace、erase等函数的作用



## 2022-10-10

### 一、图的最短距离问题

#### 1. dijkstra算法

```c++
void dijkstra(int id = 0) { // fill dist array, dist for 0 - n is INT_MAX
    // priority_queue
    using pri = pair<int,int>;
    priority_queue<pri,vector<pri>,greater<pri>> q;
    q.emplace(0, id);
    dist[id] = 0;
    vector<int> st(n, 0); // take down status
    while (!q.empty()) {
        auto [d, u] = q.top(); t.pop();
        if (st[u]) continue;
        st[u] = true;
        for (auto [v, w]: lk[u]) {
            if (d + w < dist[v]) {
                dist[v] = d + w;
                q.push({d + w, v});
            }
        }
    }
}
```



#### 2. Bellman-Ford 算法

```python
procedure BellmanFord(list vertices, list edges, vertex source)
   // 该实现读入边和节点的列表，并向两个数组（distance和predecessor）中写入最短路径信息
 
   // 步骤1：初始化图
   for each vertex v in vertices:
       if v is source then distance[v] := 0
       else distance[v] := infinity
       predecessor[v] := null
 
   // 步骤2：重复对每一条边进行松弛操作
   for i from 1 to size(vertices)-1:
       for each edge (u, v) with weight w in edges:
           if distance[u] + w < distance[v]:
               distance[v] := distance[u] + w
               predecessor[v] := u
 
   // 步骤3：检查负权环
   for each edge (u, v) with weight w in edges:
       if distance[u] + w < distance[v]:
           error "图包含了负权环"
```



### 二、Leetcode 1059

有环图的遍历问题：一定要注意，对已经遍历过的点，追加visited标志，否则会重复访问某一个节点导致超时；



## 2022-10-11

### 一、 Luogu P2894: [USACO08FEB]Hotel G

线段树练习，一上来敲得我有点闷。我本来还挺自信，觉得线段树可以信手拈来，结果一调试，都不知道怎么调试，到底哪出问题了。先把找出来的两个bug记录一下，避免再犯：

#### 1. pushdown()函数没有清除懒惰标记：

```c++
void pushdown(int rk, int ln, int rn, int l, int m, int r) {
    int ls = lson(rk), rs = rson(rk);
    if (lz[rk] == 1) {
        mx[ls] = lf[ls] = rt[ls] = 0, ind[ls] = l, lz[ls] = 1;
        mx[rs] = lf[rs] = rt[rs] = 0, ind[rs] = r, lz[rs] = 1;
    } else {
        mx[ls] = lf[ls] = rt[ls] = ln, ind[ls] = l, lz[ls] = 2;
        mx[rs] = lf[rs] = rt[rs] = rn, ind[rs] = m, lz[rs] = 2;
    }   
    lz[rk] = 0; // <---------------------------------------------------------------this is the key point
}
```



#### 2. 三段式运算优先级搞错

```c++
if (a == l && b == r) {
        if (c == 1) {
            mx[rk] = lf[rk] = rt[rk] = 0, ind[rk] = l, lz[rk] = 1;
        } else {
            mx[rk] = lf[rk] = rt[rk] = r - l, ind[rk] = l, lz[rk] = 2;
        }
        return;
    }
}

// 上述一开始写成：
if (a == 1 && b == r) {          // <-------------------------------this expression is wrong
    c == 1 ? mx[rk] = lf[rk] = rt[rk] = 0, ind[rk] = l, lz[rk] = 1 : mx[rk] = lf[rk] = rt[rk] = r - l, ind[rk] = l, lz[rk] = 2;
} 
```



### 二、模余定理

#### 1. 卢卡斯定理

$$
C_m^n \equiv C_{m\%p}^{n\%p} * C_{m/p}^{n/p} (mod \ p)
$$

#### 2. 线性逆元定理

$$
i^{-1}\equiv -\lfloor \frac{p}{i} \rfloor \times (p \% i)^{-1} (mod \ p)
$$



## 2022-10-12

### 一、 Luogu P2894: [USACO08FEB]Hotel G

今天发现的新bug：

1. pushup时，当最大值出现在左孩子处，未考虑到rson(rk)在右孩子处可能扩展的问题。
2. 题目要求：输出可以出租房屋的最小id，并非是最大连续零区间最左端id，因此需要搜索；
3. query()中，有忘记加if (lazy[rk]) pushdown() 了，谨记之；

总算是过了，记住教训。



## 2022-10-13

### 一、Leetcode 天堂硅谷·数字经济算法编程大赛

#### 1. 题目-02. 销售出色区间

```
给你一份销售数量表 sales，上面记录着某一位销售员每天成功推销的产品数目。

我们认为当销售员同一天推销的产品数目大于 8 个的时候，那么这一天就是「成功销售的一天」。

所谓「销售出色区间」，意味在这段时间内，「成功销售的天数」是严格 大于「未成功销售的天数」。

请你返回「销售出色区间」的最大长度。
```



这道题一开始思路错了，以为二分能搞定，结果捣腾半天无果。

其实这里有个转换，记[0,i)区间中出色数为C[i]，则区间[i,j)为出色区间的充要条件是：

$2*C[i]-2*C[j] > i - j$

因此，移位即：

$2*C[i]-i>2*C[j]-j$

至此，最关键的问题就搞定了。



#### 2. 题目-03. 重复的彩灯树

```
有一棵结构为二叉树的圣诞树 root 挂满了彩灯，各节点值表示彩灯的颜色。

如果两棵子树具有 相同的结构 和 相同的彩灯颜色分布，则它们是 重复 的。

请返回这棵树上所有 重复的子树。


树中的结点数在[1,6000]范围内。
-200 <= Node.val <= 200

```

这道题咋一看很简单，但实际做起来并非那么回事。

1. 一开始想到，左右孩子都试一遍不久好了？结果不对，答案要求：重复节点只能输出一个！这，难道要一个个对树节点去重？
2. 想到，后序遍历，并且给节点打上标记，不就不用判断重复节点了？确实，但结果超时了； 
3. 为避免超时，貌似只能先序遍历，然后一次打出所有子节点。但结果，还是有重复节点的问题。
4. 回到后续遍历，给节点打上并查集标记，在查找是否相同的函数isSame()中，借用这些标记更快输出，最终通过。

总结一下，就是不断调整思路，加速输出策略，用字典法记录重复的问题。



#### 3. 题目-04. 补给覆盖

```
已知有一片呈二叉树的道路，我们要在道路上的一些节点设置补给站支援。

补给站可以设置在任意节点上，每个补给站可以使距离自身小于等于 1 个单位的节点获得补给。

若要使道路的所有节点均能获得补给，请返回所需设置的补给站最少数量。
```

这题思路不难想，就是动态规划搞定就完事了。我的思路是定义如下状态：

$dp(p,f,c)$表示：对于当前节点p，假设其父节点取值$f\in\{0,1\}$，该结点取值$c\in\{0,1\}$,则不难计算递推公式，写出来有些复杂，省略。

#### 4. 学习别人的思想方法

##### 4.1 题目-02. 销售出色区间

```python
class Solution:
    def longestESR(self, sales: List[int]) -> int:
        pre = dict({0: -1})
        res = cursum = 0

        for i, h in enumerate(sales):
            cursum += 1 if h > 8 else -1
            if cursum > 0:
                res = i + 1
            if cursum - 1 in pre:
                res = max(res, i - pre[cursum - 1])
            pre.setdefault(cursum, i)
        return res
```

看别人的思路真是简洁明了，再反过来看自己的代码，真是惨不忍睹，又臭又长；哎，好打击啊（^-^)。

别人牢牢抓住了：出色区间，>8的数一定大于<8的数，分析[0,i]到[0,j]的变化即可，不像我，就会把问题复杂化。

##### 4.2 题目-03. 重复的彩灯树

```python
function lightDistribution(root: TreeNode | null): Array<TreeNode | null> {
   const counter = new Map<string, TreeNode[]>()
  const res: TreeNode[] = []
  dfs(root)
  for (const nodes of counter.values()) {
    if (nodes.length > 1) res.push(nodes[0])
  }

  return res

  function dfs(root: TreeNode | null): string {
    if (!root) return ''

    const left = dfs(root.left)
    const right = dfs(root.right)
    const key = `${root.val}#${left}#${right}`
    !counter.has(key) && counter.set(key, [])
    counter.get(key)!.push(root)
    return key
  }
};
```

别人的思路与我大体相似，也是后续遍历加字典加速，但用了一个字符串去重的巧妙思路，学到了！我当时也想来个数组去重来着，可惜没实践。

##### 4.3 题目-04. 补给覆盖

```python
function minSupplyStationNumber(root: TreeNode | null): number {
let res = 0
  const dfs = (root) => {

    if (!root) return 1
    const left = dfs(root.left)
    const right = dfs(root.right)


    if (left === 0 || right === 0) {
      res++
      return 2
    }


    if (left === 2 || right === 2) {
      return 1
    }


    return 0
  }

```

看看别人这代码，多简洁，而我的确长篇大论。不敢相信，两个代码居然做的是一件事情。

我是从上往下分析的，考虑当前节点如何由子节点表示。而题中思路则相反，考虑如何直接由子节点状态得到父节点。

学会正反两方向思考，打开思维逻辑！



## 2022-10-21

### 一、Minimum Adjacent Swaps for K Consecutive Ones

Leetcode Biweekly-Contest-42

```

```

### 二、Minimum Move To make Array complementary

1674



## 2022-10-22

### 一、Leetcode 周赛316

#### 1. 使数组相等的最小开销（第三题，总6216）

问题描述：

```
给你两个下标从 0 开始的数组 nums 和 cost ，分别包含 n 个 正 整数。

你可以执行下面操作 任意 次：

    将 nums 中 任意 元素增加或者减小 1 。

对第 i 个元素执行一次操作的开销是 cost[i] 。

请你返回使 nums 中所有元素 相等 的 最少 总开销。
```

样例1：

```
输入：nums = [1,3,5,2], cost = [2,3,1,14]
输出：8
解释：我们可以执行以下操作使所有元素变为 2 ：
- 增加第 0 个元素 1 次，开销为 2 。
- 减小第 1 个元素 1 次，开销为 3 。
- 减小第 2 个元素 3 次，开销为 1 + 1 + 1 = 3 。
总开销为 2 + 3 + 3 = 8 。
这是最小开销。
```

样例2：

```
输入：nums = [2,2,2,2,2], cost = [4,2,8,1,3]
输出：0
解释：数组中所有元素已经全部相等，不需要执行额外的操作。
```

思路：

不难想到思路，考虑取值为每一个节点即可，一次变化取最小值。

这道题主要在debug过程，调了近一个小时！！！记录下debug过程

1) 递推关系写错，和应该减上一个秩对应的两倍；

2) 忘记排序，递推的贪心算法，当且尽当数组有序的情况下才生效；

3) 由于用iota记录秩数组进行排序，所以当前秩为rk[i]，上一个秩为rk[i-1]，而非i - 1;

4) 初始化0忘记转换成rk[0]了；

总之，还是形成最终代码太慢，要加快coding速度！！！

最终形成代码：

```c++
long long minCost(vector<int>& nums, vector<int>& cost) {
    int n = nums.size();
    vector<int> rk(n);
    iota(rk.begin(), rk.end(), 0); 
    sort(rk.begin(), rk.end(), [&](int a, int& b){ 
        return nums[a] < nums[b];
    }); 
    long long sb = accumulate(cost.begin(), cost.end(), 0LL); 
    long long sa = 0;
    for (int i = 0; i < n; ++i) sa += (long long)nums[i] * cost[i];
    long long ans = sa - (long long)nums[rk[0]] * sb; 
    for (int i = 1; i < n; ++i) {
        int t = rk[i], b = rk[i - 1]; 
        sa -= 2 * (long long)nums[b] * cost[b];
        sb -= 2 * cost[b];
        ans = min(ans, sa - (long long)nums[t] * sb);
    }   
    return ans;
}
```

#### 2. 使数组相似的最少操作次数（第四题，总6217）

题目描述：

```
给你两个正整数数组 nums 和 target ，两个数组长度相等。

在一次操作中，你可以选择两个 不同 的下标 i 和 j ，其中 0 <= i, j < nums.length ，并且：

    令 nums[i] = nums[i] + 2 且
    令 nums[j] = nums[j] - 2 。

如果两个数组中每个元素出现的频率相等，我们称两个数组是 相似 的。

请你返回将 nums 变得与 target 相似的最少操作次数。测试数据保证 nums 一定能变得与 target 相似。
```

样例1：

```
输入：nums = [8,12,6], target = [2,14,10]
输出：2
解释：可以用两步操作将 nums 变得与 target 相似：
- 选择 i = 0 和 j = 2 ，nums = [10,12,4] 。
- 选择 i = 1 和 j = 2 ，nums = [10,14,2] 。
2 次操作是最少需要的操作次数。
```

样例2：

```
输入：nums = [1,2,5], target = [4,1,3]
输出：1
解释：一步操作可以使 nums 变得与 target 相似：
- 选择 i = 1 和 j = 2 ，nums = [1,4,3] 。
```

样例3：

```
输入：nums = [1,1,1,1,1], target = [1,1,1,1,1]
输出：0
解释：数组 nums 已经与 target 相似。
```

思路：

这题咋一看很难，一开始想时没有思路，因为我以为题目中的操作必须要i < j；后来注意到无序后，才知道要排序搞定；

然后注意到样例2，排序后貌似也很困惑，之后不难想到，由于是加2，所以奇偶性不变，所以，数组分成奇数和偶数两半，再统计差值，搞定。

代码：

```c++
pair<int,int> stn(vector<int>& nums) {
    int n = nums.size(), i = 0, j = 0;
    while (j < n) {
        while (i < n && (nums[i] & 1)) ++i;
        j = max(j, i + 1); 
        while (j < n && !(nums[j] & 1)) ++j;  // debug 1
        if (j < n) swap(nums[i++], nums[j++]);
    }   
    i = 0;
    for (; i < n && (nums[i] & 1); ++i);
    sort(nums.begin(), nums.begin() + i); 
    sort(nums.begin() + i, nums.end());
    return { i, n - i };
}
long long makeSimilar(vector<int>& nums, vector<int>& target) {
    int n = nums.size();
    auto [a, b] = stn(nums); auto [c, d] = stn(target);
    long long ans = 0;
    for (int i = 0; i < n; ++i) ans += (nums[i] < target[i]) ? target[i] - nums[i] : 0;
    return ans / 2;
}
```

Debug：

1. 一开始debug 1那行仅写了if ()判断奇数才加J，导致死循环；



## 2022-10-28

### 一、Leetcode杯LCCUP 2022 秋季

#### 第四题：[二叉树灯饰](https://leetcode.cn/contest/season/2022-fall/problems/U7WvvU/)

解答方法很明显，动态规划即可。

这道题值得注意的是运行速度。一开始写的是如下递归方式：

```c++
int helper(TreeNode* p, int st); // 对应于树节点p状态st，返回数值（操作次数）ans
```

于是，每一次函数运行，需要调用新的子函数8次；

```c++
for (int i = 0; i < 4; ++i) {
    l[i] = helper(p->left, i);
    r[i] = helper(p->right, i);
}
```

这样做，运行速度是极慢的，结果也是超时的；

应当换成以下做法：

定义函数:

```c++
vector<int> helper(TreeNode* p); // 对应于树节点p，返回4个状态对应的操作次数向量
```

这样，只需要调用两次子函数即可：

```c++
l = helper(p->left), r = helper(p->right);
```

*********

记住：递归函数应当控制子函数调用次数，越少越好，一般来说，2次为宜；

## 2022-10-29

一些曾经耗时较长、逻辑写不清楚的题：

### 一、Leetocode 1654: [Minimum Jumps to Reach Home](https://leetcode.cn/problems/minimum-jumps-to-reach-home/)

这道题一开始总是从常规动态规划的角度入手，但可惜的是，一遍遍历并不能解决问题。主要难点有二：

1. 问题的本质实际上是搜索，而非线性递推；
2. 问题存在一个上限，这个上限其实是max(f + a + b, x + b);;

明白这两点后，这道题就不那么难了

```c++
#define L 40005
int fb[L];
int dp[L][2];
int minimumJumps(vector<int>& forbidden, int a, int b, int x) {
    memset(fb, 0, sizeof fb);
    for (auto v: forbidden) fb[v] = 1;
    queue<pair<int,int>> q;
    memset(dp, -1, sizeof dp);
    q.push({0, 0});
    dp[0][0] = 0;
    dp[1][0] = 0;
    while (!q.empty()) {
        auto f = q.front();
        q.pop();
        if (f.first + a < L && !fb[f.first + a] && dp[f.first + a][0] == -1) {
            q.push({f.first + a, 0});
            dp[f.first + a][0] = dp[f.first][f.second] + 1;
        }
        if (f.second == 0 && 0 <= f.first - b && !fb[f.first - b] && dp[f.first - b][1] == -1) {
            q.push({f.first - b, 1});
            dp[f.first - b][1] = dp[f.first][0] + 1;
        }
    }   
    if (dp[x][0] == -1 && dp[x][1] == -1) return -1; 
    if (dp[x][0] == -1) dp[x][0] = INT_MAX;
    if (dp[x][1] == -1) dp[x][1] = INT_MAX;
    return min(dp[x][0], dp[x][1]);
}
```

### 二、Leetcode 1647: [Minimum Deletions to Make Character Frequencies Unique](https://leetcode.cn/problems/minimum-deletions-to-make-character-frequencies-unique/)

按频次排序即可解决，需要注意的是，当前一个频率减到0时，下一个不是-1，依然是0；

```c++
int minDeletions(string s) {
    int a[26];
    memset(a, 0, sizeof a);
    for (auto& v: s) a[v - 'a']++;
    sort(a, a + 26, greater<int>());
    int ans = 0;
    for (int i = 1; i < 26; ++i) {
        if (0 <= a[i - 1] && a[i - 1] <= a[i]) {
            int m = max(0, a[i - 1] - 1);
            ans += a[i] - m;
            a[i] = m;
        }
    }
    return ans;
}
```

### 三、Leetcode 1648: [Sell Diminishing-Valued Colored Balls](https://leetcode.cn/problems/sell-diminishing-valued-colored-balls/)

思路很简单，二分就能搞定。

```c++
#define MOD 1000000007
int OD; 
long long helper(vector<int>& inv, int num) {
    long long ans = 0;
    for (auto& v: inv) if (num <= v) ans += v - num + 1;
    return ans;
}
int maxProfit(vector<int>& inventory, int orders) {
    int l = 1, r = MOD;
    OD = orders;
    while (l < r) {
        int m = l + r >> 1;
        if (helper(inventory, m) < OD) r = m;
        else l = m + 1;
    }   
    long long ans = 0, num = 0;
    for (auto& v: inventory) {
        if (l <= v) ans += (long long)(v + l) * (v - l + 1) >> 1, num += v - l + 1;
    }   
    ans += (orders - num) * (l - 1); 
    return ans % MOD;
}
```

### 四、Leetcode 1625: [Lexicographically Smallest String After Applying Operations](https://leetcode.cn/problems/lexicographically-smallest-string-after-applying-operations/)

第一次做的时候总在考虑规律，试图一下子看出来最小值的规律，实际上并不用如此，唯暴力算法尔！

方法一：队列加字典，简单粗暴

```c++
void _add(string& s, int a) {
    for (int i = 0; i < s.length(); ++i) {
        if (i & 1) {
            int v = s[i] - '0';
            s[i] = '0' + (v + a) % 10; 
        }
    }   
}
void _rotate(string& s, int b) {
    int n = s.length();
    s = s.substr(n - b, b) + s.substr(0, n - b); 
}
string findLexSmallestString(string s, int a, int b) {
    int n = s.length();
    unordered_set<string> ss({s});
    queue<string> qs({s});
    string ans = s;
    while (!qs.empty()) {
        auto f = qs.front(); qs.pop();
        ans = min(ans, f); 
        for (int i = 1; i <= 10; ++i) {
            _add(f, a); 
            if (!ss.count(f)) qs.push(f), ss.insert(f);
        }
        _rotate(f, b); 
        if (!ss.count(f)) qs.push(f), ss.insert(f);
    }   
    return ans;
}
```

方法二：全部遍历

```c++
string findLexSmallestString(string s, int a, int b) {
    int t = 0, d = 0, sl = s.length();
    string cp = s, ss = s;
    int n = sl; 
    for (int i = 0; i < 10; ++i) { // for odd bit
        for (int j = 0; j < sl; ++j) if (j & 1) s[j] = ('9' < s[j] + a) ? s[j] + a - 10 : s[j] + a;
        ss = s;
        if (b & 1) {
            for (int j = 0; j < 10; ++j) { // for even bit
                for (int k = 0; k < sl; ++k) if (!(k & 1)) ss[k] = ('9' < ss[k] + a) ? ss[k] + a - 10 : ss[k] + a; 
                for (int k = 0; k < sl; ++k) {
                    //PR(ss);
                    ss = ss.substr(n - b, b) + ss.substr(0, n - b); 
                    if (ss.compare(cp) < 0) cp = ss; 
                }
            }
        } else {
            for (int k = 0; k < sl; ++k) {
                ss = ss.substr(n - b, b) + ss.substr(0, n - b); 
                if (ss.compare(cp) < 0) cp = ss; 
            }
        }
    }   
    return cp; 
}
```



## 2022-10-30

### 一、Leetcode 双周赛90

#### 第四题：下一个更大元素 IV（总Leetcode 6227)

思路一开始想到了，从后往前遍历，只要返回第二大的秩就好，但一开始没意识到可以通过线段树搞定，并且箱拓展思维，想试试从前往后遍历如何。

然后，按顺序遍历的想，貌似可以用双指针搞定？一激动，吭哧吭哧地玛了大半代码后，想到了反例，此路不通，时间也浪费了大半。

回到从后往前遍历，思考了很久，发现可以用线段树搞定；于是写了个非递归线段树，但写完才发现，无法从上到下的搜索，决定了非递归的方法无法返回第一个大于当前数的数的位置；有浪费了好久时间；

最后，才用递归线段树的方法解决了这道题，调试完成再到最终通过，超时了18分钟。

```c++
#define L 100010
#define M L << 2
#define lson(x) ((x)<<1)
#define rson(x) ((x)<<1|1)
int sg[M], K;
void update(int id, int v, int l, int r, int rk) {
    if (r - l == 1) { sg[rk] = v; return; }
    int m = l + r >> 1;
    if (id < m) update(id, v, l, m, lson(rk));
    else update(id, v, m, r, rson(rk));
    sg[rk] = max(sg[lson(rk)], sg[rson(rk)]);
}
int search(int a, int b, int v, int l, int r, int rk) {
    if (b <= a || sg[rk] <= v) return L;
    if (r - l == 1) return l;
    int m = l + r >> 1, ans = L;
    if (a < m) ans = search(a, min(m, b), v, l, m, lson(rk));
    if (ans < L) return ans;
    if (m < b) ans = search(max(a, m), b, v, m, r, rson(rk));
    return ans;
}
vector<int> secondGreaterElement(vector<int>& nums) {
    int n = nums.size();
    int i = 0, j = 0;
    vector<int> ans(n);
    for (int i = n - 1; 0 <= i; --i) {
        int id = search(i + 1, n, nums[i], 0, n, 1); 
        int nid = search(id + 1, n, nums[i], 0, n, 1); 
        ans[i] = nid < n ? nums[nid] : -1; 
        update(i, nums[i], 0, n, 1); 
    }   
    return ans;
}
```

别人的思维方法：对秩排序，按大小顺序检索！！！

```c++
    vector<int> secondGreaterElement(vector<int>& a) {
        auto cmp = [&](int i, int j) {
            if (a[i] != a[j]) return a[i] > a[j];
            return i < j;
        };
        int n = a.size();
        vector <int> id(n);
        for (int i = 0; i < n; i++) id[i] = i;
        sort(id.begin(), id.end(), cmp);
        vector <int> ans(n, -1);
        set <int> all;
        for (int i = 0; i < n; i++) {
            int j = id[i];
            auto it = all.lower_bound(j);
            if (it != all.end()) {
                ++it;
                if (it != all.end()) ans[j] = a[*it];
            }
            all.insert(j);
        }
        return ans;
    }
```



### 二、Leetcode 周赛317

#### 1. 第四题：移除子树后的二叉树高度(总Leetcode 6223)

这道题主要浪费时间点在两方面：

* 关键点1：主要关键在于叶节点，删除一个子数对总高度的影响，实际上可以简化到对应叶节点的变化。这个关键点让我想了很久才想到，到最终形成解题思路，只剩半小时不到了； 
* 用线段树维护不断查询的区间；与昨晚（见上，双周90最后一题）恰好相反，为了避免麻烦，直接用非递归方法实现（因为错误的以为，非递归能搞定的，递归的写法也一定能搞定）。但码完代码后才发现，悲剧了，因为我直接在原树上建线段树，但原树的高度是可以$10^5$级别的，很明显，秩超了；

最终，用非递归的方式实现了，关键点就在于，把所有叶节点抽出来建树；当然，抽出来后同样可以用递归线段树解决，但从形式上来讲，非递归更加自然些。

```c++
#define L 100010
#define LL L<<1
#define lson(x) (x<<1)
#define rson(x) (x<<1|1)
int tot = 0, M;
int dt[L], sg[LL];
pair<int,int> rg[L];
void build(TreeNode* p, int dpt) {
    if (!p) return;
    if (!p->left && !p->right) { 
        rg[p->val] = {tot, tot + 1}; 
        sg[tot++] = dpt;
        dt[p->val] = dpt; 
        return; 
    }   
    build(p->left, dpt + 1); 
    build(p->right, dpt + 1); 
    int l = p->left ? rg[p->left->val].first : rg[p->right->val].first;
    int r = p->right ? rg[p->right->val].second : rg[p->left->val].second;
    rg[p->val] = {l, r};
    dt[p->val] = dpt;
}
void build_tree() {
    M = 1; while (M < tot + 2) M <<= 1;
    for (int i = M + tot; M < i; --i) sg[i] = sg[i - M - 1];
    sg[M] = 0;
    for (int i = M + tot + 1; i < M * 2; ++i) sg[i] = 0;
    for (int i = M - 1; 0 < i; --i) 
        sg[i] = max(sg[lson(i)], sg[rson(i)]);
}
int search(int l, int r) {
    int ans = 0, s = M + l, t = M + r + 1;
    for (; s ^ t ^ 1; s >>= 1, t >>= 1) { 
        if (~s & 1) ans = max(ans, sg[s ^ 1]);
        if (t & 1) ans = max(ans, sg[t ^ 1]);
    }
    return ans;
}
vector<int> treeQueries(TreeNode* root, vector<int>& queries) {
    build(root, 0);
    build_tree();
    int m = queries.size();
    vector<int> ans(m);
    for (int i = 0; i < m; ++i) {
        int bv = queries[i];
        auto [l, r] = rg[bv];
        int res = dt[bv] - 1;
        int lr = search(0, l);
        res = max(lr, res);
        int rr = search(r, tot);
        res = max(rr, res);
        ans[i] = res;
    }
    return ans;
}
```



### 三、总结（双90、单317）

最需要改进的是思考问题的方式，想到思路，形成解题方案，码完代码加调试，整个速度都太慢。今天这两题，明显感觉到思路太慢，一方面不够果断，想到一个方向后，因为想法太多，又跑去试另一种；另一方面，没有形成有效的解题思维，解决问题的手段不多，先暴力再优化的思想没有贯彻，总是在想取巧的方法。

对此，作如下思维优化，警醒自己，时刻保持高效的思维方式，提高思维速度。

```
1. 答案不明显时，遵循“先暴力，后优化“的思路，抓主问题的关键点；
2. 直奔答案。从答案反推，与第一点呼应，强调自己始终奔着答案去，而不是想些无助于答案、有的没的的优化；
3. 坚决果断。想到一种可以在规定时间内完成的方法，应大胆实现；不宜东一敲，西一锤，两边取巧，结果适得其反；
4. 线段树的认识：重点1：二叉树不等于线段树，直接在二叉树上建线段树不可取；重点2：搞清楚递归和非递归线段树的区别，二者的“能”与“不能”。
```



## 2022-11-14

### 一、Leetcode 周赛318

这期周赛的思路都比算太难想，除了最后一题的DP要稍微思考以下外；这周的题目主要侧重数据结构的考察。

#### 1. 第三题：[Total Cost to Hire K Workers](https://leetcode.cn/problems/total-cost-to-hire-k-workers/)

这题，我的做法是，使用两个优先级队列模拟选人操作，思路没有问题，主要是debug破费了一些时间，包括初始化两个队列，如何选择确定，队列相遇时如何再选直至满足题目的元素个数等等，几乎每一步都出了bug，调了半天。继续加油，锻炼思维的严谨性，提高代码编写正确性和速度。

#### 2. 第四题：[Minimum Total Distance Traveled](https://leetcode.cn/problems/minimum-total-distance-traveled/)

这题毫无疑问。用动态规划搞定，一开始以为是二维问题，定义$DP[i][j]$即可搞定，写了一遍后才发现是三维问题，需要定义$DP[i][j][k]$,表示：对于工厂i，考虑将以$j$结尾的后$k$个元素放入其中的最优组合方案。递推公式不难写出，不再赘述。我的问题还是：知道用什么方法，但形成解决方案直到码完代码，所需时间还是太长。

### 二、Leetcode 双周赛91

这次双周赛的题目，从思路上来说，颇有些难度，即使第二题，也要用DP来解决；所幸这次，前三题我依旧像往常一样快速解决。

#### 1. 第二题：[Count Ways To Build Good Strings](https://leetcode.cn/problems/count-ways-to-build-good-strings/)

想到用DP来做就不算难了，毕竟递推公式很容易写出。

#### 2. 第三题：[Most Profitable Path in a Tree](https://leetcode.cn/problems/most-profitable-path-in-a-tree/)

这道题，我的思路是：先走b，然后记录b经过的节点和时间，然后走a，遍历整棵树，返回最大值；因为需要父节点信息，所以要BFS建立节点信息。

这道题主要的debug点在于，b不经过的其他节点都应当赋值为最大时间，而不是0。

#### 3. 第四题：[Split Message Based on Limit](https://leetcode.cn/problems/split-message-based-on-limit/)

思路对于目前的我来说还是很容易想到，二分！但问题还是，30分钟的时间内无法码完代码并调试完成，主要在于，这道题需要处理的子问题有些多。

总之，再保证正确性的基础上，我还需要加速加速再加速！



### 三、Leetcode 周赛319

四道题的思路都不难想到，问题还是：完成代码太慢。

#### 1. 第三题：[Minimum Number of Operations to Sort a Binary Tree by Level](https://leetcode.cn/problems/minimum-number-of-operations-to-sort-a-binary-tree-by-level/)

这道题我用了并查集，但实际上并无必要，暴力即可，时间复杂度是一样的。主要考点是BFS。

#### 2. 第四题：[Maximum Number of Non-overlapping Palindrome Substrings](https://leetcode.cn/problems/maximum-number-of-non-overlapping-palindrome-substrings/)

我的做法是：Manacher‘s Algorithm + 贪心算法

问题是：处理贪心队列时，破费了一些时间，对于边界没有定义清楚，导致来回修改进队数据。

看别人的做法，直接用DP全部搞定。

```c++
class Solution {
    int f[2005];
    bool b[2005][2005];
public:
    int maxPalindromes(string s, int k) {
        int n=s.size(),i,j;
        for(i=0;i<n;i++)b[i][i]=1;
        for(i=0;i+1<n;i++)b[i][i+1]=s[i]==s[i+1];
        for(i=n-1;~i;i--)for(j=i;j<n;j++)if(i==j)b[i][j]=1;
        else if(i+1==j)b[i][j]=s[i]==s[j];
        else b[i][j]=s[i]==s[j]&&b[i+1][j-1];
        for(i=k;i<=n;i++)for(f[i]=f[i-1],j=0;j+k<=i;j++)if(b[j][i-1])f[i]=max(f[i],f[j]+1);
        return f[n];
    }
};
```



## 2020-11-19

### 一、人工智能基本算法复习

#### 1. A*算法

可以看成是BFS的扩展，主要是决定哪些节点应当优先被扩展。
$$
f(n) = g(n) + h(n)，其中，g(n)表示从起点到节点n的距离，h(n)表示从节点n到终点的启发函数-路径估计，f(n)表示节点n的耗散值。
$$
总的来说，就是按照f(n)从小到大依次选取路径。

```c++
while(OPEN!=NULL)
{
    从OPEN表中取f(n)最小的节点n;
    if(n节点==目标节点)
        break;
    for(当前节点n的每个子节点X)
    {
        计算f(X);
        if(XinOPEN)
            if(新的f(X)<OPEN中的f(X))
            {
                把n设置为X的父亲;
                更新OPEN表中的f(n);
            }
        if(XinCLOSE)
            continue;
        if(Xnotinboth)
        {
            把n设置为X的父亲;
            求f(X);
            并将X插入OPEN表中;//还没有排序
        }
    }//endfor
    将n节点插入CLOSE表中;
    按照f(n)将OPEN表中的节点排序;//实际上是比较OPEN表内节点f的大小，从最小路径的节点向下进行。
}//endwhile(OPEN!=NULL)
```



#### 2. AO\*算法（与或图的A*算法）

与A*算法想似的思想，在与或图中，我们无法直接判断一个节点的价值，此时对应的应该是与或图中的一个子图结构，我们给这个子图打分，就是所谓的AO\*算法。

每次扩展的都是一个子图结构，标记的是子图的连接符，直到原节点被标记成solved，算法终止。

```
PROCEDURE AO*
	建立一个只由根节点构成的搜索图G
		s的费用：q(s) := h(s), G' := G.
		如果s是目标，标记s为SOLVED.
	Until s被标记为SOLVED, do:
	begin:
		在G'中，从s出发，选择一个非终止的叶节点n。
		扩展n及其所有后继，连接至G上。
			对于每一个不曾在G中出现的后继nj，q(nj) := h(nj)；
			如果这些后继中某些节点是终止节点，则用SOLVED标记。
		S := {n};建立一个只由n构成的单元素集合S。
		Untile S变空，do:
		begin:
			从S中删除节点m，满足m在G中的后继不出现在S中
			按以下步骤修改m的费用q(m）：
				对于每一从m出发的指向节点集合{n1,n2,...,nk}的连接符，
				计算：
					qi(m) = ci + q(n1) + ... + q(nk);
				取q(m)为qi(m)中的最小值，并：
					1) 将指针标记加到该最小值的连接符上；
					2) 如果本次标记不同以往，抹去之前的标记（修改G‘）；
					3）如果这个连接符指向的所有节点都是SOLVED，标记m为SOLVED；
				如果m标记为SOLVED，或者m的费用与之前不同，则：
					把m的所有有指针标记连接的父节点加到S中。
		end
	end
```



#### 3. 分枝定界法与$\alpha$-$\beta$剪枝

简单来说，与之前做过的“人选箱”加界限类似，在搜索过程中不断确定答案的界限，对于超过界限的搜索方向直接剪掉，就是所谓的分枝定界法。

而博弈-棋类问题中，一般对应极大极小策略，这时候用定界法实际上是确定上下两个界限，这就是所谓的$\alpha-\beta$剪枝。



#### 4. 遗传算法

遗传算法的[基本运算](https://baike.baidu.com/item/基本运算?fromModule=lemma_inlink)过程如下： [2] 

（1）初始化：设置进化代数计数器t=0，设置最大进化代数T，随机生成M个个体作为初始群体P(0)。 [2] 

（2）个体评价：计算群体P(t)中各个个体的[适应度](https://baike.baidu.com/item/适应度?fromModule=lemma_inlink)。 [2] 

（3）[选择运算](https://baike.baidu.com/item/选择运算?fromModule=lemma_inlink)：将选择算子作用于群体。选择的目的是把优化的个体直接遗传到下一代或通过配对交叉产生新的个体再遗传到下一代。选择操作是建立在群体中个体的[适应度](https://baike.baidu.com/item/适应度?fromModule=lemma_inlink)评估基础上的。 [2] 

（4）交叉运算：将交叉算子作用于群体。遗传算法中起核心作用的就是交叉算子。 [2] 

（5）[变异运算](https://baike.baidu.com/item/变异运算?fromModule=lemma_inlink)：将变异算子作用于群体。即是对群体中的个体串的某些[基因座](https://baike.baidu.com/item/基因座?fromModule=lemma_inlink)上的基因值作变动。群体P(t)经过选择、交叉、[变异运算](https://baike.baidu.com/item/变异运算?fromModule=lemma_inlink)之后得到下一代群体P(t+1)。 [2] 

（6）终止条件判断：若t=T,则以进化过程中所得到的具有最大[适应度](https://baike.baidu.com/item/适应度?fromModule=lemma_inlink)个体作为[最优解](https://baike.baidu.com/item/最优解?fromModule=lemma_inlink)输出，终止计算。 [2] 

[遗传操作](https://baike.baidu.com/item/遗传操作?fromModule=lemma_inlink)包括以下三个基本遗传[算子](https://baike.baidu.com/item/算子?fromModule=lemma_inlink)(genetic operator):选择(selection)；交叉(crossover)；[变异](https://baike.baidu.com/item/变异?fromModule=lemma_inlink)(mutation)。 [1] 



#### 5. 模拟退火算法

```
(1) 初始化：初始温度T(充分大)，初始解状态S(是算法迭代的起点)，每个T值的迭代次数L
(2) 对k=1, …, L做第(3)至第6步：
(3) 产生新解S′
(4) 计算增量ΔT=C(S′)-C(S)，其中C(S)为评价函数
(5) 若ΔT<0则接受S′作为新的当前解，否则以概率exp(-ΔT/T)接受S′作为新的当前解.
(6) 如果满足终止条件则输出当前解作为最优解，结束程序。
终止条件通常取为连续若干个新解都没有被接受时终止算法。
(7) T逐渐减少，且T->0，然后转第2步。
```



## 2022-11-20

### 一、Leetcode  周赛320

#### 第二题（总6242）：二叉搜索树最近节点查询 

这道题走了一点弯路，一开始直接在树上搜索最金节点，结果显然是超时的；

转换思路，化为排序数组查询，显然会更快，此时已经可以通过了；

其实还可以更近一步，对待查询数组排序，按从小到大查询再输出，显然会更快。

#### 第三题（总6243）：到达首都的最少油耗

这道题想歪了。第一个想法是：从最深节点开始，每次往上（父节点方向）数seats次，这些节点同乘一辆车；依次类推，这样的贪心策略会是最好的吗？

显然，结果错了，考虑:

vector<vector<int>> n = {{0,1},{0,2},{1,3},{1,4}}; int s = 5;

的情形；可以知道，正确的做法是，再每一个节点出判断：再该节点处标记油耗p和总人数n，由下往上递推，才能得到正确的答案；

#### 第四题（总6244）：完美分割的方案数

这道题倒是不难，有点类似与字典-字符串，动态规划，一遍过，就是形成解决方案还是太慢。

