# 使用动态编程对数字总和为 Y 的[L，R]范围内的数字进行计数

> 原文:[https://www . geeksforgeeks . org/numbers-from-l-r-其数字总和为-y/](https://www.geeksforgeeks.org/count-of-numbers-from-range-l-r-whose-sum-of-digits-is-y/)

**先决条件:** [递归](https://www.geeksforgeeks.org/recursion/)[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/)

给定一个整数 **Y** 和一个范围**【L，R】**，任务是找出给定范围内所有数字的计数，这些数字的总和等于 **Y** 。
**举例:**

> **输入:** L = 0，R = 11，Y = 2
> **输出:**2
> 2->2
> 11->1+1 = 2
> **输入:** L = 500，R = 1000，Y = 6
> **输出:** 3

> **约束:**
> 
> 0 <= L <= R <= 10^18
> 
> 0 <= Y <= 162 *(一个 18 位数能有的最大可能总和是多少)*

**处理方法:**首先将问题一般化，[L，R]可以写成[0，R]–[0，L-1]，即先求出数字和= Y 的[0，R]范围内的所有数字，然后对于[0，L-1]范围，最后减去每个值，得到期望的结果。因此，对于数字的情况，让我们将数字 L 和 R 的数字存储在两个独立的向量中，这样访问它的数字会更容易。然后我们需要一个函数来携带(current_index，flag，sum)。这个函数是我们逻辑的主要部分。初始化 current_index = 0，标志= 0，sum = 0。

假设 R = 462，这个数字有 3 个索引，即 0，1，2。现在检查有多少种方法可以填充第 0 个索引。通过观察，我们可以说我们可以将第 0 个索引填充为 0、1、2、3 和 4。如果我们超过 4，那么我们将形成一个大于 462 的数。

现在，如果你在第 0 个索引中插入了 0，那么第 1 个索引的可能性有多大？答案–0，1，2，3，4，5，6，7，8，9。由于第 0 个索引中有一个数字 0，因此您可以在第 1 个索引中填充 0-9 之间的任何数字。好的，因为你可以在下一个索引中填充任何数字，所以你将 flag = 1。flag = 1 告诉我们，我们有优势填充 0-9 之间的任何内容。同样，为其他指数想一想。

如果我们看到基础条件

if(current _ index = = n){
if(sum = = Y)返回 1；
否则返回 0；

以下是上述方法的实现:

## C++

```
#include<bits/stdc++.h>
using namespace std;

// function to convert digit to vector
vector<int> digitToVec(int n) {
    vector<int> a;
    while (n) {
        a.push_back(n % 10);
        n = n / 10;
    }
    reverse(a.begin(), a.end());
    return a;
}

int Y;    // setting Y as global
int dp[19][2][18 * 9 + 1];    // 3D dp
int func(int ind, int flag, int sum, vector<int> a) {
    if (ind == a.size()) {
        if (sum == Y) return 1;
        else return 0;
    }
    if (dp[ind][flag][sum] != -1) return dp[ind][flag][sum];

      // if flag = 0, I know I can only fill from 0 to a[ind]
    // if flag = 1, I have the advantage to fill from 0 to 9
    int limit = 9;
    if (flag == 0) limit = a[ind];

    int cnt = 0;
    for (int num = 0; num <= limit; num++) {
          // if flag = 0, which means no advantage
          // and I am still filling the same number as a[ind] means giving him no advantage
          // hence the next recursion call flag still stays as 0
        if (flag == 0 && num == a[ind]) {
            cnt += func(ind + 1, 0, sum + num, a);
        }
        else {
            cnt += func(ind + 1, 1, sum + num, a);
        }
    }
    return dp[ind][flag][sum] = cnt;
}

// intermediate function helping to initialize all values of func()
int ans(int n) {
    vector<int> a = digitToVec(n);
    memset(dp, -1, sizeof dp);    // initializing dp as -1
    return func(0, 0, 0, a);
}

// Driver code
int main() {
    int l, r;
    cin >> l >> r >> Y;
    cout << ans(r) - ans(l - 1);
    return 0;
}
```

**Output:** 

```
2
```

现在谈谈最坏情况下的时间复杂度:O(19 * 2 * (18 * 9) * 10)