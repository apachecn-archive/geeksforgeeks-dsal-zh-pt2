# 给定和的最大尺寸子集

> 原文:[https://www . geesforgeks . org/最大尺寸-子集-给定-总和/](https://www.geeksforgeeks.org/maximum-size-subset-given-sum/)

这是[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)的扩展版本。这里我们需要找到最大大小子集的大小，其和等于给定的和。

**示例:**

```
Input : set[] = {2, 3, 5, 7, 10, 15},
         sum  = 10
Output : 3
The largest sized subset with sum 10
is {2, 3, 5}

Input : set[] = {1, 2, 3, 4, 5}
         sum = 4
Output : 2
```

这是对子集和问题的进一步改进，不仅给出了子集是否可能，而且给出了使用 DP 的最大子集。
要解决子集和问题，使用与[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)中给出的相同的动态规划方法。为了进一步计算最大子集，我们使用另一个 DP 数组(称为“计数数组”)，其中计数[i][j]是的最大值

*   计数[i][j-1]。这里不考虑电流元素。
*   计数[i- X][j-1] + 1。这里，X 是为子集选择的当前元素的值。

## C++

```
// A Dynamic Programming solution for subset
// sum problem+ maximal subset value.
#include<bits/stdc++.h>
using namespace std;

    // Returns size of maximum sized subset
    // if there is a subset of set[] with sun
    // equal to given sum. It returns -1 if there
    // is no subset with given sum.
    int isSubsetSum(int set[], int n, int sum)
    {
        // The value of subset[i][j] will be true if there
        // is a subset of set[0..j-1] with sum equal to i
        bool subset[sum + 1][n + 1];
        int count[sum + 1][n + 1];

        // If sum is 0, then answer is true
        for (int i = 0; i <= n; i++)
        {
            subset[0][i] = true;
            count[0][i] = 0;
        }

        // If sum is not 0 and set is empty,
        // then answer is false
        for (int i = 1; i <= sum; i++)
        {
            subset[i][0] = false;
            count[i][0] = -1;
        }

        // Fill the subset table in bottom up manner
        for (int i = 1; i <= sum; i++)
        {
            for (int j = 1; j <= n; j++)
            {
                subset[i][j] = subset[i][j - 1];
                count[i][j] = count[i][j - 1];
                if (i >= set[j - 1])
                {
                    subset[i][j] = subset[i][j] ||
                                subset[i - set[j - 1]][j - 1];

                    if (subset[i][j])
                        count[i][j] = max(count[i][j - 1],
                                    count[i - set[j - 1]][j - 1] + 1);
                }
            }
        }

        return count[sum][n];
    }

// Driver code
int main()
{
    int set[] = { 2, 3, 5, 10 };
    int sum = 20;
    int n = 4;
    cout<< isSubsetSum(set, n, sum);
}

// This code is contributed by DrRoot_
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming solution for subset
// sum problem+ maximal subset value.
class sumofSub {

    // Returns size of maximum sized subset if there
    // is a subset of set[] with sun equal to given sum.
    // It returns -1 if there is no subset with given sum.
    static int isSubsetSum(int set[], int n, int sum)
    {
        // The value of subset[i][j] will be true if there
        // is a subset of set[0..j-1] with sum equal to i
        boolean subset[][] = new boolean[sum + 1][n + 1];
        int count[][] = new int[sum + 1][n + 1];

        // If sum is 0, then answer is true
        for (int i = 0; i <= n; i++) {
            subset[0][i] = true;
            count[0][i] = 0;
        }

        // If sum is not 0 and set is empty,
        // then answer is false
        for (int i = 1; i <= sum; i++) {
            subset[i][0] = false;
            count[i][0] = -1;
        }

        // Fill the subset table in bottom up manner
        for (int i = 1; i <= sum; i++) {
            for (int j = 1; j <= n; j++) {
                subset[i][j] = subset[i][j - 1];
                count[i][j] = count[i][j - 1];
                if (i >= set[j - 1]) {
                    subset[i][j] = subset[i][j] ||
                       subset[i - set[j - 1]][j - 1];

                    if (subset[i][j])
                        count[i][j] = Math.max(count[i][j - 1],
                             count[i - set[j - 1]][j - 1] + 1);
                }
            }
        }

        return count[sum][n];
    }

    /* Driver program to test above function */
    public static void main(String args[])
    {
        int set[] = { 2, 3, 5, 10 };
        int sum = 20;
        int n = set.length;
        System.out.println(isSubsetSum(set, n, sum));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# A Dynamic Programming solution 
# for subset sum problem+ maximal
# subset value.
# Returns size of maximum sized subset
# if there is a subset of set[] with sun
# equal to given sum. It returns -1 if there
# is no subset with given sum.
def isSubsetSum(arr, n, sum):

    # The value of subset[i][j] will
    # be true if there is a subset of
    # set[0..j-1] with sum equal to i
    subset = [[False for x in range(n + 1)]
                     for y in range (sum + 1)]
    count = [[0 for x in range (n + 1)]
                for y in range (sum + 1)]

    # If sum is 0, then answer is true
    for i in range (n + 1):
        subset[0][i] = True
        count[0][i] = 0

    # If sum is not 0 and set is empty,
    # then answer is false
    for i in range (1, sum + 1):
        subset[i][0] = False
        count[i][0] = -1

    # Fill the subset table in bottom up manner
    for i in range (1, sum + 1):
        for j in range (1, n + 1):
            subset[i][j] = subset[i][j - 1]
            count[i][j] = count[i][j - 1]
            if (i >= arr[j - 1]) :
                subset[i][j] = (subset[i][j] or
                                subset[i - arr[j - 1]][j - 1])

                if (subset[i][j]):
                    count[i][j] = (max(count[i][j - 1],
                                    count[i - arr[j - 1]][j - 1] + 1))
    return count[sum][n]

# Driver code
if __name__ == "__main__":

    arr = [2, 3, 5, 10]
    sum = 20
    n = 4
    print (isSubsetSum(arr, n, sum))

# This code is contributed by Chitranayal
```

## C#

```
// A Dynamic Programming solution for subset
// sum problem+ maximal subset value.
using System;

class sumofSub {

    // Returns size of maximum sized subset
    // if there is a subset of set[] with sun
    // equal to given sum. It returns -1 if there
    // is no subset with given sum.
    static int isSubsetSum(int[] set, int n, int sum)
    {
        // The value of subset[i][j] will be true if there
        // is a subset of set[0..j-1] with sum equal to i
        bool[, ] subset = new bool[sum + 1, n + 1];
        int[, ] count = new int[sum + 1, n + 1];

        // If sum is 0, then answer is true
        for (int i = 0; i <= n; i++) {
            subset[0, i] = true;
            count[0, i] = 0;
        }

        // If sum is not 0 and set is empty,
        // then answer is false
        for (int i = 1; i <= sum; i++) {
            subset[i, 0] = false;
            count[i, 0] = -1;
        }

        // Fill the subset table in bottom up manner
        for (int i = 1; i <= sum; i++) {
            for (int j = 1; j <= n; j++) {
                subset[i, j] = subset[i, j - 1];
                count[i, j] = count[i, j - 1];
                if (i >= set[j - 1]) {
                    subset[i, j] = subset[i, j] ||
                                   subset[i - set[j - 1], j - 1];

                    if (subset[i, j])
                        count[i, j] = Math.Max(count[i, j - 1],
                                      count[i - set[j - 1], j - 1] + 1);
                }
            }
        }

        return count[sum, n];
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] set = { 2, 3, 5, 10 };
        int sum = 20;
        int n = set.Length;
        Console.WriteLine(isSubsetSum(set, n, sum));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript Programming solution for subset
// sum problem+ maximal subset value.

// Returns size of maximum sized subset
// if there is a subset of set[] with
// sun equal to given sum. It returns -1
// if there is no subset with given sum.
function isSubsetSum(set, n, sum)
{

    // The value of subset[i][j] will be
    // true if there is a subset of
    // set[0..j-1] with sum equal to i
    let subset = new Array(sum + 1);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < subset.length; i++)
    {
        subset[i] = new Array(2);
    }
    let count = new Array(sum + 1);

    // Loop to create 2D array using 1D array
    for(var i = 0; i < count.length; i++)
    {
        count[i] = new Array(2);
    }

    // If sum is 0, then answer is true
    for(let i = 0; i <= n; i++)
    {
        subset[0][i] = true;
        count[0][i] = 0;
    }

    // If sum is not 0 and set is empty,
    // then answer is false
    for(let i = 1; i <= sum; i++)
    {
        subset[i][0] = false;
        count[i][0] = -1;
    }

    // Fill the subset table in bottom up manner
    for(let i = 1; i <= sum; i++)
    {
        for(let j = 1; j <= n; j++)
        {
            subset[i][j] = subset[i][j - 1];
            count[i][j] = count[i][j - 1];

            if (i >= set[j - 1])
            {
                subset[i][j] = subset[i][j] ||
                subset[i - set[j - 1]][j - 1];

                if (subset[i][j])
                    count[i][j] = Math.max(count[i][j - 1],
                         count[i - set[j - 1]][j - 1] + 1);
            }
        }
    }
    return count[sum][n];
}

// Driver Code
let set = [ 2, 3, 5, 10 ];
let sum = 20;
let n = set.length;

document.write(isSubsetSum(set, n, sum));

// This code is contributed by sanjoy_62

</script>
```

**输出:**

```
4
```

上述解的时间复杂度为 O(和*n)。