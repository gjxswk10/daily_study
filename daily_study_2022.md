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
}
```

区间更新、区间查询：

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
}
```

#### 4. 扫描线算法

代完善；

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
a / b % M = a * (b ^ M - 2) % M (M与b互素）
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



#### 10. 内置库函数

__builtin_popcount  // 二进制位中1的个数

__builtin_clz/ctz/ffs // 二进制位中开头|结尾0的个数|第一个1出现位置



#### 11. 遍历mask的所有子集技巧

```c++
for (x = mask; x; x = mask & x - 1)
```

#### 12. 重叠区间最小|大和技巧

动态重置区间； 

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
        if (j < 0 || s[j] == s[t]) {
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

### 一、 极大极小问题（一些博弈游戏的策略问题）

各种棋类问题的解答。



### 二、设计符合要求的数据结构

看到要求O(1)时间完成插入、删除、查找的题目，首先要想到哈系表，一般都是哈系表+某种数据结构（向量/链表）等实现。



### 三、容器非常有用的接口prev、next

作用于iterator，返回之前或者之后n个（默认为1）位置的iterator

注意emplace、erase等函数的作用

