# 对给定范围内的数字进行计数，使偶数的总和大于奇数的总和

> 原文:[https://www . geesforgeks . org/count-numbers-in-给定范围-这样偶数位数的总和大于奇数位数的总和/](https://www.geeksforgeeks.org/count-numbers-in-given-range-such-that-sum-of-even-digits-is-greater-than-sum-of-odd-digits/)

给定两个整数 **L** 和 **R** 表示一个范围【L，R】。任务是找出给定范围[L，R]内偶数位数之和大于奇数位数之和的数字总数。

**示例:**

> **输入:** L=2 R=10
> **输出:** 4
> 具有偶数
> 位数之和大于奇数位数之和的性质的数字是:2，4，6，8
> 
> **输入:**L = 2 R = 17
> T3】输出: 7

**先决条件:** [数字-DP](https://www.geeksforgeeks.org/digit-dp-introduction/)

**方法:**
首先，计算所需的数字，直到 R，即在[0，R]范围内。要得到[L，R]范围内的答案，求解从 0 到 R 的范围，然后减去从 0 到 L–1 的范围内的答案。定义差压状态如下:

*   把数字看作一个数字序列，一个状态是我们当前所处的位置。如果我们处理 10^18.之前的数字，这个位置的值可以从 0 到 18 在每次递归调用中，通过放置一个从 0 到 9 的数字，尝试从左到右构建序列。
*   第一个状态是到目前为止已经放置的**偶数**位数的**和**。
*   第二个状态是到目前为止已经放置的**奇数**位数的**和**。
*   另一个状态是布尔变量**紧密**，它告诉我们试图构建的数字已经变得比 R 小，因此在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。如果数字没有变小，我们可以放置的最大位数限制是 r 中当前位置的位数。

以下是上述方法的实现:

## C++

```
// C++ code to count number in the range
// having the sum of even digits greater
// than the sum of odd digits
#include <bits/stdc++.h>

// as the number can be up to 10^18
#define int long long

using namespace std;

vector<int> v;

int dp[18][180][180][2];

int memo(int index, int evenSum,
                      int oddSum, int tight)
{
    // Base Case

    if (index == v.size()) {
        // check if condition satisfied or not
        if (evenSum > oddSum)
            return 1;
        else
            return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[index][evenSum][oddSum][tight] != -1)
        return dp[index][evenSum][oddSum][tight];

    // Maximum limit upto which we can place
    // digit. If tight is 0, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]

    int limit = (tight) ? v[index] : 9;

    int ans = 0;

    for (int d = 0; d <= limit; d++) {
        int currTight = 0;

        if (d == v[index])
            currTight = tight;

        // if current digit is odd
        if (d % 2 != 0)
            ans += memo(index + 1, evenSum,
                        oddSum + d, currTight);

        // if current digit is even
        else
            ans += memo(index + 1, evenSum + d,
                        oddSum, currTight);
    }

    dp[index][evenSum][oddSum][tight] = ans;
    return ans;
}
// Function to convert n into its
// digit vector and uses memo() function
// to return the required count
int CountNum(int n)
{
    v.clear();
    while (n) {
        v.push_back(n % 10);
        n = n / 10;
    }

    reverse(v.begin(), v.end());

    // Initialize DP
    memset(dp, -1, sizeof(dp));
    return memo(0, 0, 0, 1);
}

// Driver Code

int32_t main()
{
    int L, R;
    L = 2;
    R = 10;
    cout << CountNum(R) - CountNum(L - 1) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count number in the range
// having the sum of even digits greater
// than the sum of odd digits
import java.util.*;

class GFG
{

    static Vector<Integer> v = new Vector<>();

    static int[][][][] dp = new int[18][180][180][2];

    static int memo(int index, int evenSum,
    int oddSum, int tight)
    {
        // Base Case

        if (index == v.size()) 
        {
            // check if condition satisfied or not
            if (evenSum > oddSum) 
            {
                return 1;
            } 
            else
            {
                return 0;
            }
        }

        // If this result is already computed
        // simply return it
        if (dp[index][evenSum][oddSum][tight] != -1) 
        {
            return dp[index][evenSum][oddSum][tight];
        }

        // Maximum limit upto which we can place
        // digit. If tight is 0, means number has
        // already become smaller so we can place
        // any digit, otherwise num[pos]
        int limit = (tight > 0) ? v.get(index) : 9;

        int ans = 0;

        for (int d = 0; d <= limit; d++) 
        {
            int currTight = 0;

            if (d == v.get(index)) 
            {
                currTight = tight;
            }

            // if current digit is odd
            if (d % 2 != 0) 
            {
                ans += memo(index + 1, evenSum,
                        oddSum + d, currTight);
            } // if current digit is even
            else
            {
                ans += memo(index + 1, evenSum + d,
                        oddSum, currTight);
            }
        }

        dp[index][evenSum][oddSum][tight] = ans;
        return ans;
    }
    // Function to convert n into its
    // digit vector and uses memo() function
    // to return the required count

    static int CountNum(int n) 
    {
        v.clear();
        while (n > 0) 
        {
            v.add(n % 10);
            n = n / 10;
        }

        Collections.reverse(v);

        // Initialize DP
        for (int i = 0; i < 18; i++)
        {
            for (int j = 0; j < 180; j++) 
            {
                for (int k = 0; k < 180; k++) 
                {
                    for (int l = 0; l < 2; l++)
                    {
                        dp[i][j][k][l] = -1;
                    }
                }
            }
        }

        return memo(0, 0, 0, 1);
    }

    // Driver Code
    public static void main(String[] args) 
    {
        int L, R;
        L = 2;
        R = 10;
        System.out.println(CountNum(R) - CountNum(L - 1));

    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python code to count number in the range
# having the sum of even digits greater
# than the sum of odd digits

def memo(index, evenSum, oddSum, tight):

    # Base Case
    if index == len(v):

        # check if condition satisfied or not
        if evenSum > oddSum:
            return 1
        else:
            return 0

    # If this result is already computed
    # simply return it
    if dp[index][evenSum][oddSum][tight] != -1:
        return dp[index][evenSum][oddSum][tight]

    # Maximum limit upto which we can place
    # digit. If tight is 0, means number has
    # already become smaller so we can place
    # any digit, otherwise num[index]
    limit = v[index] if tight else 9

    ans = 0

    for d in range(limit + 1):
        currTight = 0

        if d == v[index]:
            currTight = tight

        # if current digit is odd
        if d % 2 != 0:
            ans += memo(index + 1, evenSum, 
                        oddSum + d, currTight)

        # if current digit is even
        else:
            ans += memo(index + 1, evenSum + d, 
                            oddSum, currTight)

    dp[index][evenSum][oddSum][tight] = ans
    return ans

# Function to convert n into its digit vector
# and uses memo() function to return the
# required count
def countNum(n):
    global dp, v

    v.clear()
    num = []
    while n:
        v.append(n % 10)
        n //= 10

    v.reverse()

    # Initialize dp
    dp = [[[[-1, -1] for i in range(180)] for j in range(180)]
        for k in range(18)]
    return memo(0, 0, 0, 1)

# Driver Code
if __name__ == "__main__":
    dp = []
    v = []

    L = 2
    R = 10
    print(countNum(R) - countNum(L - 1))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# code to count number in the range
// having the sum of even digits greater
// than the sum of odd digits
using System.Collections.Generic;
using System;

class GFG
{

    static List<int> v = new List<int>();

    static int [,,,]dp = new int[18,180,180,2];

    static int memo(int index, int evenSum,
    int oddSum, int tight)
    {
        // Base Case

        if (index == v.Count) 
        {
            // check if condition satisfied or not
            if (evenSum > oddSum) 
            {
                return 1;
            } 
            else
            {
                return 0;
            }
        }

        // If this result is already computed
        // simply return it
        if (dp[index,evenSum,oddSum,tight] != -1) 
        {
            return dp[index,evenSum,oddSum,tight];
        }

        // Maximum limit upto which we can place
        // digit. If tight is 0, means number has
        // already become smaller so we can place
        // any digit, otherwise num[pos]
        int limit = (tight > 0) ? v[index] : 9;

        int ans = 0;

        for (int d = 0; d <= limit; d++) 
        {
            int currTight = 0;

            if (d == v[index]) 
            {
                currTight = tight;
            }

            // if current digit is odd
            if (d % 2 != 0) 
            {
                ans += memo(index + 1, evenSum,
                        oddSum + d, currTight);
            } // if current digit is even
            else
            {
                ans += memo(index + 1, evenSum + d,
                        oddSum, currTight);
            }
        }

        dp[index,evenSum,oddSum,tight] = ans;
        return ans;
    }

    // Function to convert n into its
    // digit vector and uses memo() function
    // to return the required count
    static int CountNum(int n) 
    {
        v.Clear();
        while (n > 0) 
        {
            v.Add(n % 10);
            n = n / 10;
        }

        v.Reverse();

        // Initialize DP
        for (int i = 0; i < 18; i++)
        {
            for (int j = 0; j < 180; j++) 
            {
                for (int k = 0; k < 180; k++) 
                {
                    for (int l = 0; l < 2; l++)
                    {
                        dp[i,j,k,l] = -1;
                    }
                }
            }
        }

        return memo(0, 0, 0, 1);
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        int L, R;
        L = 2;
        R = 10;
        Console.WriteLine(CountNum(R) - CountNum(L - 1));

    }
}

/* This code is contributed by PrinciRaj1992 */
```

**Output:**

```
4

```

**时间复杂度:**当 0 < a，b < 10 <sup>18</sup> 时，最多会有 18*(180)*(180)*2 次计算