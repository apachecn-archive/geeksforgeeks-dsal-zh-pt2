# 任意两个相邻数字之间的绝对差值最多为 K 的数字计数

> 原文:[https://www . geesforgeks . org/numbers-count-up-n-具有任意两个相邻数字之间的最多 k 个绝对差值/](https://www.geeksforgeeks.org/count-of-numbers-upto-n-having-absolute-difference-of-at-most-k-between-any-two-adjacent-digits/)

给定一个**整数 N** ，任务是将任意两个相邻数字之间的绝对差值最多为 **K** 的数字计数到 **N** 。
***注意:**任何数字的整数 0 计数都相当可观。*
**例:**

> **输入:** N = 20，K = 2
> **输出:** 15
> **说明:**
> 所需数字为 0、1、2、3、4、5、6、7、8、9、10、11、12、13、20。请注意，14、15、16、17、18 和 19 的相邻数字的绝对差值都大于 K = 2，因此它们不被计算在内。
> **输入:** N = 30，K = 3
> **输出:** 22
> **说明:**
> 接受除 15、16、17、18、19、26、27、28、29 以外的 30 以内的所有数字。

**天真方法:**思路是迭代到 N，检查 K 的差是否存在的所有数字。如果是，那么计数，否则跳过这个数字，继续迭代。
***时间复杂度:** O(N)*
***辅助空间:** O(1)*
**高效途径:**这个问题可以使用[数字动态规划](https://www.geeksforgeeks.org/digit-dp-introduction/)进行优化。下面是给定问题的详细 dp 状态。

*   在数字 Dp 中，我们认为我们的数字是一个数字序列，所以需要一个状态*位置*，所以标记我们当前处于哪个状态。在每次递归调用中，尝试通过放置一个从 0 到 9 的数字并增加位置来从左到右构建序列。
*   *上一个数字*只存储那些与上一个数字绝对差最多 **K** 的数字。所以，前一个数字需要另一个状态。
*   *紧密*，状态告诉我们试图构建的数字是否已经变得小于 N，这样在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。否则，我们可以在当前位置放置直到 **N** 的数字。
*   初始化一个布尔变量 *Start* ，告知数字是否已经开始。如果数字还没有开始，我们可以通过将数字从 1 放置到当前位置相对紧密的上限来开始数字。否则，不从数字开始向前循环。
*   在每次递归调用中，相对于前一个数字设置当前数字，使它们之间的绝对差值不超过 **K** 。在基本情况下，如果到达最后一个位置，返回 1。

以下是上述方法的实现:

## C++

```
// C++ program to get the count
// of numbers upto N having
// absolute difference at most K
// between any two adjacent digits

#include <bits/stdc++.h>
using namespace std;

// Table to store solution
// of each subproblem
long long dp[1002][10][2][2];

// Function to calculate
// all possible numbers
long long possibleNumbers(
    int pos, int previous, bool tight,
    bool start, string N, int K)
{
    // Check if position reaches end that is
    // is equal to length of N
    if (pos == N.length())
        return 1;

    // Check if the result is
    // already computed
    // simply return it
    if (dp[pos][previous][tight][start] != -1)
        return dp[pos][previous][tight][start];

    int res = 0;

    // Maximum limit upto which we can place
    // digit. If tight is false, means number has
    // already become smaller so we can place
    // any digit, otherwise N[pos]
    int upper_limit
        = (tight)
              ? (N[pos] - '0')
              : 9;

    int new_tight;

    // Check if start is false the number
    // has not started yet
    if (!start) {

        // Check if we do not start
        // the number at pos
        // then recur forward
        res = possibleNumbers(
            pos + 1, previous,
            false, false, N, K);

        // If we start the number
        // we can place any digit
        // from 1 to upper_limit
        for (int i = 1; i <= upper_limit; i++) {

            // Finding the new tight
            new_tight
                = (tight
                   && i == upper_limit)
                      ? 1
                      : 0;
            res += possibleNumbers(
                pos + 1, i, new_tight,
                true, N, K);
        }
    }

    // Condition if the number
    // has already started
    else {

        // We can place digit upto
        // upperbound & absolute difference
        // with previous digit much
        // be atmost K
        for (int i = 0; i <= upper_limit; i++) {

            new_tight = (tight
                         && i == upper_limit)
                            ? 1
                            : 0;
            // Absolute difference atmost K
            if (abs(i - previous) <= K)
                res += possibleNumbers(
                    pos + 1, i,
                    new_tight, true, N, K);
        }
    }

    // Store the solution
    // to this subproblem
    dp[pos][previous][tight][start] = res;

    return dp[pos][previous][tight][start];
}

// Driver code
int main(void)
{

    string N = "20";
    int K = 2;

    // Initialising the
    // table with -1
    memset(dp, -1, sizeof dp);

    // Function call
    cout << possibleNumbers(
                0, 0, true,
                false, N, K)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get the count
// of numbers upto N having
// absolute difference at most K
// between any two adjacent digits
import java.util.*;

class GFG{

// Table to store solution
// of each subproblem
static int [][][][]dp = new int[1002][10][2][2];

// Function to calculate
// all possible numbers
static int possibleNumbers(int pos, int previous,
                           int tight, int start,
                            String N, int K)
{

    // Check if position reaches end
    // that is equal to length of N
    if (pos == N.length())
        return 1;

    // Check if the result is already
    // computed simply return it
    if (dp[pos][previous][tight][start] != -1)
        return dp[pos][previous][tight][start];

    int res = 0;

    // Maximum limit upto which we can
    // place digit. If tight is false,
    // means number has already become
    // smaller so we can place
    // any digit, otherwise N[pos]
    int upper_limit = (tight == 1) ?
                      (N.charAt(pos) - '0') : 9;

    int new_tight;

    // Check if start is false the number
    // has not started yet
    if (start == 0)
    {

        // Check if we do not start
        // the number at pos
        // then recur forward
        res = possibleNumbers(pos + 1, previous,
                              0, 0, N, K);

        // If we start the number
        // we can place any digit
        // from 1 to upper_limit
        for(int i = 1; i <= upper_limit; i++)
        {

            // Finding the new tight
            new_tight = (tight > 0 &&
                         i == upper_limit) ? 1 : 0;
            res += possibleNumbers(pos + 1, i,
                                   new_tight,
                                   1, N, K);
        }
    }

    // Condition if the number
    // has already started
    else
    {

        // We can place digit upto
        // upperbound & absolute difference
        // with previous digit much
        // be atmost K
        for(int i = 0; i <= upper_limit; i++)
        {
            new_tight = (tight > 0 &&
                         i == upper_limit) ? 1 : 0;

            // Absolute difference atmost K
            if (Math.abs(i - previous) <= K)
                res += possibleNumbers(pos + 1, i,
                                       new_tight, 1,
                                       N, K);
        }
    }

    // Store the solution
    // to this subproblem
    dp[pos][previous][tight][start] = res;

    return dp[pos][previous][tight][start];
}

// Driver code
public static void main(String[] args)
{
    String N = "20";
    int K = 2;

    // Initialising the
    // table with -1
    for(int i = 0; i < 1002; i++)
        for(int j = 0; j < 10; j++)
            for(int k = 0; k < 2; k++)
                for(int l = 0; l < 2; l++)
                    dp[i][j][k][l] = -1;

    // Function call
    System.out.print(possibleNumbers(0, 0, 1, 0,
                                     N, K) + "\n");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to get the count of
# numbers upto N having absolute
# difference at most K between any
# two adjacent digits

# Table to store solution
# of each subproblem
dp = [[[[ -1 for i in range(2)]
             for j in range(2)]
             for i in range(10)]
             for j in range(1002)]

# Function to calculate
# all possible numbers
def possibleNumber(pos, previous, tight,
                   start, N, K):

    # Check if position reaches end
    # that is equal to length of N
    if(pos == len(N)):
        return 1

    # Check if the result is
    # already computed
    # simply return it
    if(dp[pos][previous][tight][start] != -1):
        return dp[pos][previous][tight][start]

    res = 0

    # Maximum limit upto which we can place
    # digit. If tight is false, means number has
    # already become smaller so we can place
    # any digit, otherwise N[pos]
    if(tight):
        upper_limit = ord(N[pos]) - ord('0')
    else:
        upper_limit = 9

    # Check if start is false the number
    # has not started yet
    if(not start):

        # Check if we do not start
        # the number at pos
        # then recur forward
        res = possibleNumber(pos + 1, previous,
                             False, False, N, K)

        # If we start the number
        # we can place any digit
        # from 1 to upper_limit
        for i in range(1, upper_limit + 1):

            # Finding the new tight
            if(tight and i == upper_limit):
                new_tight = 1
            else:
                new_tight = 0

            res += possibleNumber(pos + 1, i,
                                  new_tight,
                                  True, N, K)

    # Condition if the number
    # has already started
    else:

        # We can place digit upto
        # upperbound & absolute
        # difference with previous
        # digit much be atmost K
        for i in range(upper_limit + 1):
            if(tight and i == upper_limit):
                new_tight = 1
            else:
                new_tight = 0

            # Absolute difference atmost K
            if(abs(i - previous) <= K):
                res += possibleNumber(pos + 1, i,
                                      new_tight,
                                        True, N, K)

    # Store the solution to this subproblem
    dp[pos][previous][tight][start] = res

    return dp[pos][previous][tight][start]

# Driver code
if __name__ == '__main__':

    N = "20"
    K = 2

    # Function call
    print(possibleNumber(0, 0, True,
                         False, N, K))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to get the count
// of numbers upto N having
// absolute difference at most K
// between any two adjacent digits
using System;

class GFG{

// Table to store solution
// of each subproblem
static int [,,,]dp = new int[1002, 10, 2, 2];

// Function to calculate
// all possible numbers
static int possibleNumbers(int pos, int previous,
                           int tight, int start,
                            String N, int K)
{

    // Check if position reaches end
    // that is equal to length of N
    if (pos == N.Length)
        return 1;

    // Check if the result is already
    // computed simply return it
    if (dp[pos, previous, tight, start] != -1)
        return dp[pos, previous, tight, start];

    int res = 0;

    // Maximum limit upto which we can
    // place digit. If tight is false,
    // means number has already become
    // smaller so we can place
    // any digit, otherwise N[pos]
    int upper_limit = (tight == 1) ?
                      (N[pos] - '0') : 9;

    int new_tight;

    // Check if start is false the number
    // has not started yet
    if (start == 0)
    {

        // Check if we do not start
        // the number at pos
        // then recur forward
        res = possibleNumbers(pos + 1, previous,
                              0, 0, N, K);

        // If we start the number
        // we can place any digit
        // from 1 to upper_limit
        for(int i = 1; i <= upper_limit; i++)
        {

            // Finding the new tight
            new_tight = (tight > 0 &&
                         i == upper_limit) ? 1 : 0;
            res += possibleNumbers(pos + 1, i,
                                   new_tight,
                                   1, N, K);
        }
    }

    // Condition if the number
    // has already started
    else
    {

        // We can place digit upto
        // upperbound & absolute difference
        // with previous digit much
        // be atmost K
        for(int i = 0; i <= upper_limit; i++)
        {
            new_tight = (tight > 0 &&
                         i == upper_limit) ? 1 : 0;

            // Absolute difference atmost K
            if (Math.Abs(i - previous) <= K)
                res += possibleNumbers(pos + 1, i,
                                       new_tight, 1,
                                       N, K);
        }
    }

    // Store the solution
    // to this subproblem
    dp[pos, previous, tight, start] = res;

    return dp[pos, previous, tight, start];
}

// Driver code
public static void Main(String[] args)
{
    String N = "20";
    int K = 2;

    // Initialising the
    // table with -1
    for(int i = 0; i < 1002; i++)
        for(int j = 0; j < 10; j++)
            for(int k = 0; k < 2; k++)
                for(int l = 0; l < 2; l++)
                    dp[i, j, k, l] = -1;

    // Function call
    Console.Write(possibleNumbers(0, 0, 1, 0,
                                  N, K) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
    // Javascript program to get the count
    // of numbers upto N having
    // absolute difference at most K
    // between any two adjacent digits

    // Table to store solution
    // of each subproblem
    let dp = new Array(1002);

    // Function to calculate
    // all possible numbers
    function possibleNumbers(pos, previous, tight, start, N, K)
    {

        // Check if position reaches end
        // that is equal to length of N
        if (pos == N.length)
            return 1;

        // Check if the result is already
        // computed simply return it
        if (dp[pos][previous][tight][start] != -1)
            return dp[pos][previous][tight][start];

        let res = 0;

        // Maximum limit upto which we can
        // place digit. If tight is false,
        // means number has already become
        // smaller so we can place
        // any digit, otherwise N[pos]
        let upper_limit = (tight == 1) ?
                          (N[pos] - '0') : 9;

        let new_tight;

        // Check if start is false the number
        // has not started yet
        if (start == 0)
        {

            // Check if we do not start
            // the number at pos
            // then recur forward
            res = possibleNumbers(pos + 1, previous,
                                  0, 0, N, K);

            // If we start the number
            // we can place any digit
            // from 1 to upper_limit
            for(let i = 1; i <= upper_limit; i++)
            {

                // Finding the new tight
                new_tight = (tight > 0 &&
                             i == upper_limit) ? 1 : 0;
                res += possibleNumbers(pos + 1, i,
                                       new_tight,
                                       1, N, K);
            }
        }

        // Condition if the number
        // has already started
        else
        {

            // We can place digit upto
            // upperbound & absolute difference
            // with previous digit much
            // be atmost K
            for(let i = 0; i <= upper_limit; i++)
            {
                new_tight = (tight > 0 &&
                             i == upper_limit) ? 1 : 0;

                // Absolute difference atmost K
                if (Math.abs(i - previous) <= K)
                    res += possibleNumbers(pos + 1, i,
                                           new_tight, 1,
                                           N, K);
            }
        }

        // Store the solution
        // to this subproblem
        dp[pos][previous][tight][start] = res;

        return dp[pos][previous][tight][start];
    }

    let N = "20";
    let K = 2;

    // Initialising the
    // table with -1
    for(let i = 0; i < 1002; i++)
    {
        dp[i] = new Array(10);
        for(let j = 0; j < 10; j++)
        {
            dp[i][j] = new Array(2);
            for(let k = 0; k < 2; k++)
            {
                dp[i][j][k] = new Array(2);
                for(let l = 0; l < 2; l++)
                {
                    dp[i][j][k][l] = -1;
                }
            }
         }
     }

    // Function call
    document.write(possibleNumbers(0, 0, 1, 0,
                                     N, K) + "</br>");

// This code id contributed by divyeshrsbadiya07.
</script>
```

**Output:** 

```
15
```

***时间复杂度:** O( D * 10 * 2 * 2 * 10)，考虑 N 有 **D** 位数。*