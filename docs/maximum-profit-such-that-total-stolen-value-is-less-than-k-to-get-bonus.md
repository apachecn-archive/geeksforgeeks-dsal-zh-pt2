# 总被盗价值小于 K 的最大利润获得奖励

> 原文:[https://www . geeksforgeeks . org/最大利润-总被盗价值低于 k-to-get-bonus/](https://www.geeksforgeeks.org/maximum-profit-such-that-total-stolen-value-is-less-than-k-to-get-bonus/)

给定一个整数 **K** 和一个数组**arr【】**表示可以被盗的数量，任务是选择一个物品子集，使它们的总价值小于 K，以获得奖金金额。

> **奖励金额:**奖励金额将是每被盗一件物品在物品集中可被盗的最大值。
> **奖金金额=(最多 arr[]) *(被盗物品数量)**

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 7
> **输出:** 22
> **说明:**
> 最大可盗值为–5。
> 如果物品被偷了是 1、2 和 4。那么被盗价值总和将小于 k
> 因此，利润总额
> = >每件物品价值+可被盗最大价值
> = > 1 + 5 + 2 + 5 + 4 + 5 = 22
> 
> **输入:** arr[] = {5，2，7，3}，K = 6
> **输出:** 19
> **说明:**
> 如果被盗物品为 2 和 3，最大可盗价值为–7
> 。那么被盗价值总和将小于 k
> 因此，利润总额
> = >每件物品价值+可被盗最大价值
> = > 2 + 7 + 3 + 7 = 19

**方法:**思路是用[排列&组合](https://www.geeksforgeeks.org/permutation-and-combination/)选择元素，使其总和小于 k，因此，考虑每一种可能会得到可能的最大利润。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum stolen value such that
// total stolen value is less than K

#include <bits/stdc++.h>

using namespace std;

// Function to find the maximum
// profit from the given values
int maxProfit(vector<int> value,
                         int N, int K)
{
    sort(value.begin(), value.end());
    int maxval = value[N - 1];
    int maxProfit = 0;
    int curr_val;

    // Iterating over every
    // possible permutation
    do {
        curr_val = 0;
        for (int i = 0; i < N; i++) {
            curr_val += value[i];
            if (curr_val <= K) {
                maxProfit = max(curr_val +
                  maxval * (i + 1), maxProfit);
            }
        }
    } while (next_permutation(
        value.begin(), value.end()));
    return maxProfit;
}

// Driver Code
int main()
{
    int N = 4, K = 6;
    vector<int> values{5, 2, 7, 3};

    // Function Call
    cout << maxProfit(values, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum stolen value such that
// total stolen value is less than K
import java.util.*;
class GFG{

// Function to find the maximum
// profit from the given values
static int maxProfit(int []value,
                     int N, int K)
{
    Arrays.sort(value);
    int maxval = value[N - 1];
    int maxProfit = 0;
    int curr_val;

    // Iterating over every
    // possible permutation
    do {
        curr_val = 0;
        for (int i = 0; i < N; i++) {
            curr_val += value[i];
            if (curr_val <= K) {
                maxProfit = Math.max(curr_val +
                                     maxval * (i + 1),
                                     maxProfit);
            }
        }
    } while (next_permutation(value));
    return maxProfit;
}
static boolean next_permutation(int[] p) {
      for (int a = p.length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
          for (int b = p.length - 1;; --b)
            if (p[b] > p[a]) {
              int t = p[a];
              p[a] = p[b];
              p[b] = t;
              for (++a, b = p.length - 1; a < b; ++a, --b) {
                t = p[a];
                p[a] = p[b];
                p[b] = t;
              }
              return true;
            }
      return false;
    }

// Driver Code
public static void main(String[] args)
{
    int N = 4, K = 6;
    int []values = {5, 2, 7, 3};

    // Function Call
    System.out.print(maxProfit(values, N, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum stolen value such that
# total stolen value is less than K

# Function to find the maximum
# profit from the given values
def maxProfit(value, N, K):

    value.sort()
    maxval = value[N - 1]
    maxProfit = 0

    # Iterating over every
    # possible permutation
    while True:
        curr_val = 0
        for i in range(N):
            curr_val += value[i]

            if (curr_val <= K):
                maxProfit = max(curr_val + maxval *
                                      (i + 1), maxProfit)

        if not next_permutation(value):
            break

    return maxProfit

def next_permutation(p):

    for a in range(len(p) - 2, -1, -1):
        if p[a] < p[a + 1]:
            b = len(p) - 1

            while True:
                if p[b] > p[a]:
                    t = p[a]
                    p[a] = p[b]
                    p[b] = t

                    a += 1
                    b = len(p) - 1

                    while a < b:
                        t = p[a]
                        p[a] = p[b]
                        p[b] = t

                        a += 1
                        b -= 1

                    return True

                b -= 1

    return False

# Driver Code 
N, K = 4, 6
values = [ 5, 2, 7, 3 ]

# Function Call
print(maxProfit(values, N, K))

# This code is contributed by divyesh072019
```

## C#

```
// C# implementation to find the
// maximum stolen value such that
// total stolen value is less than K
using System;

class GFG{

// Function to find the maximum
// profit from the given values
static int maxProfit(int[] value,
                     int N, int K)
{
    Array.Sort(value);
    int maxval = value[N - 1];
    int maxProfit = 0;
    int curr_val;

    // Iterating over every
    // possible permutation
    do
    {
        curr_val = 0;
        for(int i = 0; i < N; i++)
        {
            curr_val += value[i];
            if (curr_val <= K)
            {
                maxProfit = Math.Max(curr_val +
                                     maxval * (i + 1),
                                     maxProfit);
            }
        }
    } while (next_permutation(value));
    return maxProfit;
}

static bool next_permutation(int[] p)
{
    for(int a = p.Length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
            for(int b = p.Length - 1;; --b)
                if (p[b] > p[a])
                {
                    int t = p[a];
                    p[a] = p[b];
                    p[b] = t;

                    for(++a, b = p.Length - 1;
                            a < b; ++a, --b)
                    {
                        t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                    }
                    return true;
                }
    return false;
}

// Driver code  
static void Main()
{
    int N = 4, K = 6;
    int[] values = { 5, 2, 7, 3 };

    // Function call
    Console.WriteLine(maxProfit(values, N, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript implementation to find the
    // maximum stolen value such that
    // total stolen value is less than K

    // Function to find the maximum
    // profit from the given values
    function maxProfit(value, N, K)
    {
        value.sort();
        let maxval = value[N - 1];
        let maxProfit = 0;
        let curr_val;

        // Iterating over every
        // possible permutation
        do
        {
            curr_val = 0;
            for(let i = 0; i < N; i++)
            {
                curr_val += value[i];
                if (curr_val <= K)
                {
                    maxProfit = Math.max(curr_val +
                                         maxval * (i + 1),
                                         maxProfit);
                }
            }
        } while (next_permutation(value));
        return maxProfit;
    }

    function next_permutation(p)
    {
        for(let a = p.length - 2; a >= 0; --a)
            if (p[a] < p[a + 1])
                for(let b = p.length - 1;; --b)
                    if (p[b] > p[a])
                    {
                        let t = p[a];
                        p[a] = p[b];
                        p[b] = t;

                        for(++a, b = p.length - 1;
                                a < b; ++a, --b)
                        {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
        return false;
    }

    let N = 4, K = 6;
    let values = [ 5, 2, 7, 3 ];

    // Function call
    document.write(maxProfit(values, N, K));

</script>
```

**Output:** 

```
19
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)