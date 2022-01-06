# 数字 DP |简介

> 原文:[https://www.geeksforgeeks.org/digit-dp-introduction/](https://www.geeksforgeeks.org/digit-dp-introduction/)

先决条件:[如何求解一个动态规划问题？](https://www.geeksforgeeks.org/solve-dynamic-programming-problem/)
有很多类型的问题要求计算两个整数之间的整数数量' **x** '比如说' **a** '和' **b** '这样 x 满足一个可以与其位数相关的特定属性。
所以，如果我们说 **G(x)** 告诉 1 到 x(含)之间的这类整数个数，那么 a 和 b 之间的这类整数个数可以由**G(b)–G(a-1)**给出。这时数字 **DP** (动态编程)开始动作。所有满足上述性质的整数计数问题都可以用数字微分法来解决。

**关键概念:**

*   假设给定的数字 x 有 n 个数字。数字 DP 的主要思想是首先将数字表示为数字 t[]的数组。假设 a 我们有**t<sub>n</sub>t<sub>n-1</sub>t<sub>n-2</sub>…t<sub>2</sub>t<sub>1</sub>**作为十进制表示，其中**t<sub>I</sub>(0<I<= n)**表示从右数第 I 位数字。最左边的数字 t <sub>n</sub> 是最高有效数字。

*   现在，以这种方式表示给定的数字后，我们生成小于给定数字的数字，并同时使用 DP 进行计算，如果该数字满足给定的属性。我们 ***开始生成位数= 1 的整数，然后一直到位数= n，位数小于 n 的整数可以通过将最左边的位数设置为零来分析。***

**例题:**
给定两个整数 **a** 和 **b** 。您的任务是打印
a 和 b 之间的整数中出现的所有数字的总和。
例如，如果 a = 5，b = 11， 那么答案是 38 (5 + 6 + 7 + 8 + 9 + 1 + 0 + 1 + 1)
**约束条件**:1<= a<b<= 10^18
现在我们看到，如果我们已经计算了具有 n-1 个数字的状态的答案，即， **t<sub>n-1</sub>t<sub>n-2</sub>…t<sub>2</sub>t<sub>1</sub>**而我们需要为有 n 个数字的状态计算答案**t<sub>n</sub>t<sub>n-1</sub>t<sub>n-2</sub>…t<sub>2</sub>t<sub>1</sub>T34】。 因此，很明显，我们可以使用先前状态的结果，而不是重新计算它。因此，它遵循重叠属性。
我们来想一想这个 DP 的状态
我们的 DP 状态会是 **dp(idx，紧，和)**
**1) idx****

*   它讲述了给定整数中从右开始的索引值

**2)紧**

*   这将显示当前数字范围是否受限。如果当前数字的
    范围不受限制，那么它将从 0 跨越到 9(包括 0 和 9)，否则它将从 0 跨越到数字【idx】(包括 0 和 9)。
    **例**:考虑我们的极限整数为 3245，我们需要计算 G(3245)
    指数:4 3 2 1
    位数:3 2 4 5

**无限制范围:**
现在假设到现在生成的整数是:3 1 * * ( *是空的地方，要插入数字组成整数)。

```
  index  : 4 3 2 1  
  digits : 3 2 4 5
 generated integer: 3 1 _ _ 
```

在这里，我们看到索引 2 的范围不受限制。现在索引 2 可以有 0 到 9(包括 0 和 9)的数字。
对于无限制范围**紧= 0**
**受限范围:**
现在假设到目前为止生成的整数是:3 2 * *(“*”是一个空的地方，要插入数字形成整数)。

```
  index  : 4 3 2 1  
  digits : 3 2 4 5
 generated integer: 3 2 _ _ 
```

在这里，我们看到指数 2 有一个有限的范围。现在，索引 2 只能有从 0 到 4(包括 0 和 4)的数字
对于受限范围**紧密= 1**
**3)总和**

*   此参数将存储生成的从 msd 到 idx 的整数的位数总和。

*   考虑到整数中的 18 位数字，此参数总和的最大值可以是 9*18 = 162

**状态关系:**
状态关系的基本思路很简单。我们以自上而下的方式制定 dp。
假设我们在拥有指数 idx 的 **msd** 。所以最初总和是 0。
因此，我们将使用其范围内的数字来填充索引处的数字。假设它的范围是从 0 到 k (k < =9，取决于紧密值)，从下一个状态中获取答案，索引= idx-1，sum =上一个 sum +选择的数字。

```
int ans = 0;
for (int i=0; i<=k; i++) {
   ans += state(idx-1, newTight, sum+i)
}

state(idx,tight,sum) = ans;
```

**如何计算 new 紧绷值？**
一个状态的新紧值取决于它之前的状态。如果前一状态的紧值是 1，并且选择的 idx 处的数字是数字[idx](即限制整数中 idx 处的数字)，那么只有我们的新紧值将是 1，因为只有这样，它才表明到目前为止形成的数字是限制整数的前缀。

```
// digitTaken is the digit chosen
// digit[idx] is the digit in the limiting 
//            integer at index idx from right
// previouTight is the tight value form previous 
//              state

newTight = previousTight & (digitTake == digit[idx])
```

**以上实现的 C++代码**:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// Given two integers a and b. The task is to print
// sum of all the digits appearing in the
// integers between a and b
#include "bits/stdc++.h"
using namespace std;

// Memoization for the state results
long long dp[20][180][2];

// Stores the digits in x in a vector digit
long long getDigits(long long x, vector <int> &digit)
{
    while (x)
    {
        digit.push_back(x%10);
        x /= 10;
    }
}

// Return sum of digits from 1 to integer in
// digit vector
long long digitSum(int idx, int sum, int tight,
                          vector <int> &digit)
{
    // base case
    if (idx == -1)
       return sum;

    // checking if already calculated this state
    if (dp[idx][sum][tight] != -1 and tight != 1)
        return dp[idx][sum][tight];

    long long ret = 0;

    // calculating range value
    int k = (tight)? digit[idx] : 9;

    for (int i = 0; i <= k ; i++)
    {
        // calculating newTight value for next state
        int newTight = (digit[idx] == i)? tight : 0;

        // fetching answer from next state
        ret += digitSum(idx-1, sum+i, newTight, digit);
    }

    if (!tight)
      dp[idx][sum][tight] = ret;

    return ret;
}

// Returns sum of digits in numbers from a to b.
int rangeDigitSum(int a, int b)
{
    // initializing dp with -1
    memset(dp, -1, sizeof(dp));

    // storing digits of a-1 in digit vector
    vector<int> digitA;
    getDigits(a-1, digitA);

    // Finding sum of digits from 1 to "a-1" which is passed
    // as digitA.
    long long ans1 = digitSum(digitA.size()-1, 0, 1, digitA);

    // Storing digits of b in digit vector
    vector<int> digitB;
    getDigits(b, digitB);

    // Finding sum of digits from 1 to "b" which is passed
    // as digitB.
    long long ans2 = digitSum(digitB.size()-1, 0, 1, digitB);

    return (ans2 - ans1);
}

// driver function to call above function
int main()
{
    long long a = 123, b = 1024;
    cout << "digit sum for given range : "
         << rangeDigitSum(a, b) << endl;
    return 0;
}
```

**输出:**

```
digit sum for given range : 12613
```

**时间复杂度** :
总共有 idx * sum *紧密状态，我们正在执行 0 到 9 次迭代来访问每个状态。因此，时间复杂度为**O(10 * idx * sum *紧)**。在这里，我们观察到 64 位无符号整数的**紧** = 2 和 **idx** 最大可以是 18，而且总和最大为 9*18 ~ 200。因此，总体而言，我们有 10*18*200*2 ~ 10^5 迭代，可以在 **0.01 秒**内轻松执行。
上述问题也可以用简单递归解决，无需任何记忆。上述问题的递归解可以在[这里](https://www.geeksforgeeks.org/count-sum-of-digits-in-numbers-from-1-to-n/)找到。我们将很快在未来的帖子中添加更多关于数字 dp 的问题。
本文由 [**尼提什·库马尔**](https://www.linkedin.com/in/nk17kumar) 供稿。如果你喜欢极客博客并想投稿，你也可以用 write.geeksforgeeks.org 写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。