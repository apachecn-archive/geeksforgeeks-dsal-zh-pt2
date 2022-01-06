# 计算数字总和可被 K 整除的范围内的数字，第一个和最后一个数字不同

> 原文:[https://www . geesforgeks . org/count-numbers-in-a-range-digits-sum-by-k-division-first-and-last-digits-differential/](https://www.geeksforgeeks.org/count-numbers-in-a-range-with-digit-sum-divisible-by-k-having-first-and-last-digit-different/)

给定一个以 **L** 和 **R** 形式的范围和一个值 **K** ，任务是计算范围 **L** 到 **R** 之间的数字，使得数字的总和可被 **K** 整除，并且第一个数字不等于数字的最后一个数字。

**示例:**

> **输入:** L = 1，R = 10，K = 2
> **输出:** 0
> **说明:**
> 输入的数字之和可被 2 整除(K = 2)的数字是 2、4、6、8，但所有这些数字的第一个数字等于最后一个数字。因此答案是 0，这意味着没有一个数字满足条件。
> 
> **输入:** L = 10，R = 20，K = 2
> **输出:** 5
> **说明:**
> 数字之和可被 2 整除的数字(K = 2)是 11、13、15、17、19 和 20。但是在 11 中，第一个数字与最后一个数字相匹配。所以排除这个，答案将是 5。

**天真方法:**
解决这个问题的天真方法是检查每个数字是否满足给定的条件。然而，由于数字的范围，这种解决方案的效率会很低。

**高效途径:**
解决这个问题的主要思路是使用[数字动态规划](https://www.geeksforgeeks.org/digit-dp-introduction/)。
过渡需要定义各种状态。因此，我们可以将差压状态定义为:

1.  因为在数字 DP 中，我们认为一个数字是数字的**序列**，所以为了遍历序列，我们需要位置作为状态。我们通常做的是，把每个可能的数字[0，9]放在递归调用中，只要满足所有条件，我们就可以把它放在每个位置来寻找可能的解。
2.  我们需要的第二件事是总和，我们已经建立了序列。由于和可以很大，所以为了更好的空间和时间复杂度，我们可以将和保持为**和模 K** 。所以**之和**就是第二个 DP 状态。
3.  我们需要的第三个东西是**数字**，我们已经把它放在**第一个位置**了。在放置序列的最后一个数字时，我们需要检查它是否等于我们之前放置的第一个数字。这将是第三个 DP 状态。
4.  问题是，每次我们创建一个 N 位序列时，其中 N 是数字上限中的位数，它不会创建 1 if (N=3)，而是创建 001。这里第一个数字是 0，最后一个数字是 1，但这是错误的，因为我们已经创建了一个一位数的数字，其第一个数字等于最后一个数字。因此，我们必须在递归调用中每次都检查这一点。假设我们必须建立一个像 0002 这样的序列，我们需要更新等于 2 的起始数字。所以零前缀应该忽略。为了检查这一点，我们需要一个新的**布尔状态(0 或 1)** 。这是第四个 DP 状态。
5.  我们最不需要的就是检查我们正在构建的数字是否没有超过**上限**。假设我们正在建立一个小于等于 456 的数。我们已经创建了一个像 45 这样的序列，所以在第三位，我们不能在 0 到 9 之间放任何数字。这里我们只能放 0 到 6 的数字。所以为了检查这个界限，我们需要一个额外的**布尔状态**。这是我们最后的 DP 状态。

**算法:**

*   在每个位置，我们计算数字的总和，并删除零的前缀。
*   第一个非零数字将是序列的起始数字。
*   在最后一个位置，我们将检查它是否与起始数字匹配。

下面是上述方法的实现。

## C++

```
// C++ Program to count numbers
// in a range with digit sum
// divisible by K having first
// and last digit different

#include <bits/stdc++.h>
using namespace std;
#define ll long long int

ll K;
ll N;
vector<int> v;
ll dp[20][1000][10][2][2];

void init(ll x)
{
    memset(dp, -1, sizeof(dp));

    // For calculating the upper
    // bound of the sequence.
    v.clear();
    while (x > 0) {
        v.push_back(x % 10);
        x /= 10;
    }

    reverse(v.begin(), v.end());

    N = v.size();
}

ll fun(ll pos, ll sum, ll st, ll check, ll f)
{
    if (pos == N) {

        // checking whether the sum
        // of digits = 0 or not
        // and the corner case
        // as number equal to 1
        return (sum == 0
                and check == 1);
    }

    // If the state is visited
    // then return the answer
    // of this state directly.
    if (dp[pos][sum][st][check][f] != -1)
        return dp[pos][sum][st][check][f];

    ll lmt = 9;

    // for checking whether digit
    // to be placed is up to
    // upper bound at the
    // position pos or upto 9
    if (!f)
        lmt = v[pos];

    ll ans = 0;
    for (int digit = 0; digit <= lmt; digit++) {

        ll nf = f;

        // calculating new digit
        // sum modulo k
        ll new_sum = (sum + digit) % K;

        ll new_check = check;
        ll new_st = st;
        if (f == 0 and digit < lmt)
            nf = 1;

        // check if there is a prefix
        // of 0s and current digit != 0
        if (check == 0 and digit != 0) {

            // Then current digit will
            // be the starting digit
            new_st = digit;

            // Update the boolean flag
            // that the starting digit
            // has been found
            new_check = 1;
        }

        // At n-1, check if current digit
        // and starting digit are the same
        // then no need to calculate this answer.
        if (pos == N - 1
            and new_st == digit)
            continue;

        // Else find the answer
        ans += fun(pos + 1,
                   new_sum,
                   new_st,
                   new_check, nf);
    }

    return dp[pos][sum][st][check][f] = ans;
}

// Function to find the required count
void findCount(int L, int R, int K)
{

    // Setting up the upper bound
    init(R);

    // calculating F(R)
    ll r_ans = fun(0, 0, 0, 0, 0);

    // Setting up the upper bound
    init(L - 1);

    // calculating F(L-1)
    ll l_ans = fun(0, 0, 0, 0, 0);

    cout << r_ans - l_ans;
}

// Driver code
int main()
{
    ll L = 10;
    ll R = 20;
    K = 2;

    findCount(L, R, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count numbers
// in a range with digit sum
// divisible by K having first
// and last digit different
import java.util.*;

class GFG{

static int K;
static int N;
static Vector<Integer> v = new Vector<>();
static int [][][][][]dp = new int[20][1000][10][2][2];

static void init(int x)
{
    for(int i = 0; i < 20; i++)
        for(int j = 0; j < 1000; j++)
            for(int k = 0; k < 10; k++)
                for(int l = 0; l < 2; l++)
                    for(int m = 0; m < 2; m++)
                        dp[i][j][k][l][m] = -1;

    // For calculating the upper
    // bound of the sequence.
    v.clear();
    while (x > 0)
    {
        v.add(x % 10);
        x /= 10;
    }
    Collections.reverse(v);
    N = v.size();
}

static int fun(int pos, int sum,
               int st, int check, int f)
{
    if (pos == N)
    {

        // checking whether the sum
        // of digits = 0 or not
        // and the corner case
        // as number equal to 1
        return (sum == 0 && check == 1) ? 1 : 0;
    }

    // If the state is visited
    // then return the answer
    // of this state directly.
    if (dp[pos][sum][st][check][f] != -1)
        return dp[pos][sum][st][check][f];

    int lmt = 9;

    // for checking whether digit
    // to be placed is up to
    // upper bound at the
    // position pos or upto 9
    if (f == 0)
        lmt = v.get(pos);

    int ans = 0;
    for (int digit = 0; digit <= lmt; digit++)
    {
        int nf = f;

        // calculating new digit
        // sum modulo k
        int new_sum = (sum + digit) % K;

        int new_check = check;
        int new_st = st;
        if (f == 0 && digit < lmt)
            nf = 1;

        // check if there is a prefix
        // of 0s and current digit != 0
        if (check == 0 && digit != 0)
        {

            // Then current digit will
            // be the starting digit
            new_st = digit;

            // Update the boolean flag
            // that the starting digit
            // has been found
            new_check = 1;
        }

        // At n-1, check if current digit
        // and starting digit are the same
        // then no need to calculate this answer.
        if (pos == N - 1 && new_st == digit)
            continue;

        // Else find the answer
        ans += fun(pos + 1, new_sum,
                    new_st, new_check, nf);
    }

    return dp[pos][sum][st][check][f] = ans;
}

// Function to find the required count
static void findCount(int L, int R, int K)
{

    // Setting up the upper bound
    init(R);

    // calculating F(R)
    int r_ans = fun(0, 0, 0, 0, 0);

    // Setting up the upper bound
    init(L - 1);

    // calculating F(L-1)
    int l_ans = fun(0, 0, 0, 0, 0);

    System.out.print(r_ans - l_ans);
}

// Driver code
public static void main(String[] args)
{
    int L = 10;
    int R = 20;
    K = 2;

    findCount(L, R, K);
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count numbers
# in a range with digit sum
# divisible by K having first
# and last digit different
K = 0
N = 0
v = []
dp = [[[[[-1 for i in range(2)]
             for j in range(2)]
             for k in range(10)]
             for l in range(1000)]
             for m in range(20)]

def init(x):

    # For calculating the upper
    # bound of the sequence.
    global K
    global N
    global v
    v = []

    while (x > 0):
        v.append(x % 10)
        x //= 10

    v = v[::-1]

    N = len(v)

def fun(pos, sum, st, check, f):

    global N
    global v

    if (pos == N):

        # Checking whether the sum of
        # digits = 0 or not and the
        # corner case as number equal to 1
        return (sum == 0 and check == 1)

    # If the state is visited
    # then return the answer
    # of this state directly.
    if (dp[pos][sum][st][check][f] != -1):
        return dp[pos][sum][st][check][f]

    lmt = 9

    # For checking whether digit to
    # be placed is up to upper bound
    # at the position pos or upto 9
    if (f == False):
        lmt = v[pos]

    ans = 0
    for digit in range(lmt + 1):
        nf = f

        # Calculating new digit
        # sum modulo k
        new_sum = (sum + digit) % K

        new_check = check
        new_st = st

        if (f == 0 and digit < lmt):
            nf = 1

        # Check if there is a prefix
        # of 0s and current digit != 0
        if (check == 0 and digit != 0):

            # Then current digit will
            # be the starting digit
            new_st = digit

            # Update the boolean flag
            # that the starting digit
            # has been found
            new_check = 1

        # At n-1, check if current digit
        # and starting digit are the same
        # then no need to calculate this answer
        if (pos == N - 1 and new_st == digit):
            continue

        # Else find the answer
        ans += fun(pos + 1, new_sum,
                   new_st, new_check, nf)

        dp[pos][sum][st][check][f] = ans

    return ans

# Function to find the required count
def findCount(L, R, K):

    # Setting up the upper bound
    init(R)

    # calculating F(R)
    r_ans = fun(0, 0, 0, 0, 0)

    # Setting up the upper bound
    init(L - 1)

    # Calculating F(L-1)
    r_ans = 0
    l_ans = fun(0, 0, 0, 0, 0)

    print(l_ans - r_ans)

# Driver code
if __name__ == '__main__':

    L = 10
    R = 20
    K = 2

    findCount(L, R, K)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to count numbers
// in a range with digit sum
// divisible by K having first
// and last digit different
using System;
using System.Collections.Generic;

class GFG{

static int K;
static int N;
static List<int> v = new List<int>();
static int [,,,,]dp = new int[20, 1000, 10, 2, 2];

static void init(int x)
{
    for(int i = 0; i < 20; i++)
       for(int j = 0; j < 1000; j++)
          for(int k = 0; k < 10; k++)
             for(int l = 0; l < 2; l++)
                for(int m = 0; m < 2; m++)
                   dp[i, j, k, l, m] = -1;

    // For calculating the upper
    // bound of the sequence.
    v.Clear();
    while (x > 0)
    {
        v.Add(x % 10);
        x /= 10;
    }
    v.Reverse();
    N = v.Count;
}

static int fun(int pos, int sum, int st, 
               int check, int f)
{
    if (pos == N)
    {

        // Checking whether the sum
        // of digits = 0 or not
        // and the corner case
        // as number equal to 1
        return (sum == 0 && check == 1) ? 1 : 0;
    }

    // If the state is visited
    // then return the answer
    // of this state directly.
    if (dp[pos, sum, st, check, f] != -1)
        return dp[pos, sum, st, check, f];

    int lmt = 9;

    // For checking whether digit
    // to be placed is up to
    // upper bound at the
    // position pos or upto 9
    if (f == 0)
        lmt = v[pos];

    int ans = 0;
    for(int digit = 0; digit <= lmt; digit++)
    {
       int nf = f;

       // Calculating new digit
       // sum modulo k
       int new_sum = (sum + digit) % K;
       int new_check = check;
       int new_st = st;

       if (f == 0 && digit < lmt)
           nf = 1;

       // Check if there is a prefix
       // of 0s and current digit != 0
       if (check == 0 && digit != 0)
       {

           // Then current digit will
           // be the starting digit
           new_st = digit;

           // Update the bool flag
           // that the starting digit
           // has been found
           new_check = 1;
       }

       // At n-1, check if current digit
       // and starting digit are the same
       // then no need to calculate this answer.
       if (pos == N - 1 && new_st == digit)
           continue;

       // Else find the answer
       ans += fun(pos + 1, new_sum,
                  new_st, new_check, nf);
    }
    return dp[pos, sum, st, check, f] = ans;
}

// Function to find the required count
static void findCount(int L, int R, int K)
{

    // Setting up the upper bound
    init(R);

    // Calculating F(R)
    int r_ans = fun(0, 0, 0, 0, 0);

    // Setting up the upper bound
    init(L - 1);

    // calculating F(L-1)
    int l_ans = fun(0, 0, 0, 0, 0);

    Console.Write(r_ans - l_ans);
}

// Driver code
public static void Main(String[] args)
{
    int L = 10;
    int R = 20;
    K = 2;

    findCount(L, R, K);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to count numbers
// in a range with digit sum
// divisible by K having first
// and last digit different
var K;
var N;
var v = [];
var dp = Array.from(Array(20));

function init( x)
{
    for(var i = 0; i< 20;i++)
{
    dp[i] = Array.from(Array(1000),()=>Array(10));

    for(var j =0; j<1000;j++)
    {
        for(var k = 0; k<10;k++)
        {
            dp[i][j][k] = Array.from(Array(2), ()=>Array(2).fill(-1));
        }
    }
}

    // For calculating the upper
    // bound of the sequence.
    v = [];
    while (x > 0)
    {
        v.push(x % 10);
        x = parseInt(x/10);
    }
    v.reverse();
    N = v.length;
}

function fun(pos, sum, st,  check, f)
{
    if (pos == N)
    {

        // Checking whether the sum
        // of digits = 0 or not
        // and the corner case
        // as number equal to 1
        return (sum == 0 && check == 1) ? 1 : 0;
    }

    // If the state is visited
    // then return the answer
    // of this state directly.
    if (dp[pos][sum][st][check][f] != -1)
        return dp[pos][sum][st][check][f];

    var lmt = 9;

    // For checking whether digit
    // to be placed is up to
    // upper bound at the
    // position pos or upto 9
    if (f == 0)
        lmt = v[pos];

    var ans = 0;
    for(var digit = 0; digit <= lmt; digit++)
    {
       var nf = f;

       // Calculating new digit
       // sum modulo k
       var new_sum = (sum + digit) % K;
       var new_check = check;
       var new_st = st;

       if (f == 0 && digit < lmt)
           nf = 1;

       // Check if there is a prefix
       // of 0s and current digit != 0
       if (check == 0 && digit != 0)
       {

           // Then current digit will
           // be the starting digit
           new_st = digit;

           // Update the bool flag
           // that the starting digit
           // has been found
           new_check = 1;
       }

       // At n-1, check if current digit
       // and starting digit are the same
       // then no need to calculate this answer.
       if (pos == N - 1 && new_st == digit)
           continue;

       // Else find the answer
       ans += fun(pos + 1, new_sum,
                  new_st, new_check, nf);
    }
    return dp[pos][sum][st][check][f] = ans;
}

// Function to find the required count
function findCount(L, R, K)
{

    // Setting up the upper bound
    init(R);

    // Calculating F(R)
    var r_ans = fun(0, 0, 0, 0, 0);

    // Setting up the upper bound
    init(L - 1);

    // calculating F(L-1)
    var l_ans = fun(0, 0, 0, 0, 0);

    document.write(r_ans - l_ans);
}

// Driver code
var L = 10;
var R = 20;
K = 2;
findCount(L, R, K);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(18*1000*10*2*2)，接近 O(2*10^6)* 。

**辅助空间:** O(800*1000)