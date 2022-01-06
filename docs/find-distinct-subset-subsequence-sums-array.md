# 找出一个数组的所有不同子集(或子序列)和

> 原文:[https://www . geesforgeks . org/find-distinct-subset-subsequence-sums-array/](https://www.geeksforgeeks.org/find-distinct-subset-subsequence-sums-array/)

给定一组整数，找到一个可以从给定集合的子集生成的不同和，并以递增的顺序打印它们。给出了阵元之和很小的结论。

**示例:**

```
Input  : arr[] = {1, 2, 3}
Output : 0 1 2 3 4 5 6
Distinct subsets of given set are
{}, {1}, {2}, {3}, {1,2}, {2,3}, 
{1,3} and {1,2,3}.  Sums of these
subsets are 0, 1, 2, 3, 3, 5, 4, 6
After removing duplicates, we get
0, 1, 2, 3, 4, 5, 6  

Input : arr[] = {2, 3, 4, 5, 6}
Output : 0 2 3 4 5 6 7 8 9 10 11 12 
         13 14 15 16 17 18 20

Input : arr[] = {20, 30, 50}
Output : 0 20 30 50 70 80 100
```

这个问题的**天真解决方案**是生成所有子集，将它们的和存储在一个哈希集中，最后打印哈希集中的所有密钥。

## C++

```
// C++ program to print distinct subset sums of
// a given array.
#include<bits/stdc++.h>
using namespace std;

// sum denotes the current sum of the subset
// currindex denotes the index we have reached in
// the given array
void distSumRec(int arr[], int n, int sum,
                int currindex, unordered_set<int> &s)
{
    if (currindex > n)
        return;

    if (currindex == n)
    {
        s.insert(sum);
        return;
    }

    distSumRec(arr, n, sum + arr[currindex],
                            currindex+1, s);
    distSumRec(arr, n, sum, currindex+1, s);
}

// This function mainly calls recursive function
// distSumRec() to generate distinct sum subsets.
// And finally prints the generated subsets.
void printDistSum(int arr[], int n)
{
    unordered_set<int> s;
    distSumRec(arr, n, 0, 0, s);

    // Print the result
    for (auto i=s.begin(); i!=s.end(); i++)
        cout << *i << " ";
}

// Driver code
int main()
{
    int arr[] = {2, 3, 4, 5, 6};
    int n = sizeof(arr)/sizeof(arr[0]);
    printDistSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print distinct
// subset sums of a given array.
import java.io.*;
import java.util.*;

class GFG
{
    // sum denotes the current sum
    // of the subset currindex denotes
    // the index we have reached in
    // the given array
    static void distSumRec(int arr[], int n, int sum,
                          int currindex, HashSet<Integer> s)
    {
        if (currindex > n)
            return;

        if (currindex == n) {
            s.add(sum);
            return;
        }

        distSumRec(arr, n, sum + arr[currindex],
                    currindex + 1, s);
        distSumRec(arr, n, sum, currindex + 1, s);
    }

    // This function mainly calls
    // recursive function distSumRec()
    // to generate distinct sum subsets.
    // And finally prints the generated subsets.
    static void printDistSum(int arr[], int n)
    {
        HashSet<Integer> s = new HashSet<>();
        distSumRec(arr, n, 0, 0, s);

        // Print the result
        for (int i : s)
            System.out.print(i + " ");
    }

    //Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 5, 6 };
        int n = arr.length;
        printDistSum(arr, n);
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python 3 program to print distinct subset sums of
# a given array.

# sum denotes the current sum of the subset
# currindex denotes the index we have reached in
# the given array
def distSumRec(arr, n, sum, currindex, s):
    if (currindex > n):
        return

    if (currindex == n):
        s.add(sum)
        return

    distSumRec(arr, n, sum + arr[currindex], currindex+1, s)
    distSumRec(arr, n, sum, currindex+1, s)

# This function mainly calls recursive function
# distSumRec() to generate distinct sum subsets.
# And finally prints the generated subsets.
def printDistSum(arr,n):
    s = set()
    distSumRec(arr, n, 0, 0, s)

    # Print the result
    for i in s:
        print(i,end = " ")

# Driver code
if __name__ == '__main__':
    arr = [2, 3, 4, 5, 6]
    n = len(arr)
    printDistSum(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to print distinct
// subset sums of a given array.
using System;
using System.Collections.Generic;

class GFG
{
    // sum denotes the current sum
    // of the subset currindex denotes
    // the index we have reached in
    // the given array
    static void distSumRec(int []arr, int n, int sum,
                        int currindex, HashSet<int> s)
    {
        if (currindex > n)
            return;

        if (currindex == n)
        {
            s.Add(sum);
            return;
        }

        distSumRec(arr, n, sum + arr[currindex],
                    currindex + 1, s);
        distSumRec(arr, n, sum, currindex + 1, s);
    }

    // This function mainly calls
    // recursive function distSumRec()
    // to generate distinct sum subsets.
    // And finally prints the generated subsets.
    static void printDistSum(int []arr, int n)
    {
        HashSet<int> s = new HashSet<int>();
        distSumRec(arr, n, 0, 0, s);

        // Print the result
        foreach (int i in s)
            Console.Write(i + " ");
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 3, 4, 5, 6 };
        int n = arr.Length;
        printDistSum(arr, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program to print distinct
// subset sums of a given array.

    // sum denotes the current sum
    // of the subset currindex denotes
    // the index we have reached in
    // the given array
    function distSumRec(arr,n,sum,currindex,s)
    {
        if (currindex > n)
            return;

        if (currindex == n) {
            s.add(sum);
            return;
        }

        distSumRec(arr, n, sum + arr[currindex],
                    currindex + 1, s);
        distSumRec(arr, n, sum, currindex + 1, s);
    }

    // This function mainly calls
    // recursive function distSumRec()
    // to generate distinct sum subsets.
    // And finally prints the generated subsets.
    function printDistSum(arr,n)
    {
        let s=new Set();
        distSumRec(arr, n, 0, 0, s);
        let s1=[...s]
          s1.sort(function(a,b){return a-b;})
        // Print the result
        for (let [key, value] of s1.entries())
            document.write(value + " ");
    }

    //Driver code
    let arr=[2, 3, 4, 5, 6 ];
    let n = arr.length;
    printDistSum(arr, n);

    // This code is contributed by unknown2108
</script>
```

**输出:**

```
0 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 20
```

上述朴素递归方法的时间复杂度为 O(2 <sup>n</sup> )。

使用动态规划可以提高上述问题的时间复杂度**，尤其是当给定元素的和很小时。我们可以制作一个 dp 表，其中的行包含数组的大小，列的大小是数组中所有元素的总和。**

## C++

```
// C++ program to print distinct subset sums of
// a given array.
#include<bits/stdc++.h>
using namespace std;

// Uses Dynamic Programming to find distinct
// subset sums
void printDistSum(int arr[], int n)
{
    int sum = 0;
    for (int i=0; i<n; i++)
        sum += arr[i];

    // dp[i][j] would be true if arr[0..i-1] has
    // a subset with sum equal to j.
    bool dp[n+1][sum+1];
    memset(dp, 0, sizeof(dp));

    // There is always a subset with 0 sum
    for (int i=0; i<=n; i++)
        dp[i][0] = true;

    // Fill dp[][] in bottom up manner
    for (int i=1; i<=n; i++)
    {
        dp[i][arr[i-1]] = true;
        for (int j=1; j<=sum; j++)
        {
            // Sums that were achievable
            // without current array element
            if (dp[i-1][j] == true)
            {
                dp[i][j] = true;
                dp[i][j + arr[i-1]] = true;
            }
        }
    }

    // Print last row elements
    for (int j=0; j<=sum; j++)
        if (dp[n][j]==true)
            cout << j << " ";
}

// Driver code
int main()
{
    int arr[] = {2, 3, 4, 5, 6};
    int n = sizeof(arr)/sizeof(arr[0]);
    printDistSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print distinct
// subset sums of a given array.
import java.io.*;
import java.util.*;

class GFG {

    // Uses Dynamic Programming to
    // find distinct subset sums
    static void printDistSum(int arr[], int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // dp[i][j] would be true if arr[0..i-1]
        // has a subset with sum equal to j.
        boolean[][] dp = new boolean[n + 1][sum + 1];

        // There is always a subset with 0 sum
        for (int i = 0; i <= n; i++)
            dp[i][0] = true;

        // Fill dp[][] in bottom up manner
        for (int i = 1; i <= n; i++)
        {
            dp[i][arr[i - 1]] = true;
            for (int j = 1; j <= sum; j++)
            {
                // Sums that were achievable
                // without current array element
                if (dp[i - 1][j] == true)
                {
                    dp[i][j] = true;
                    dp[i][j + arr[i - 1]] = true;
                }
            }
        }

        // Print last row elements
        for (int j = 0; j <= sum; j++)
            if (dp[n][j] == true)
                System.out.print(j + " ");
    }

        // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 5, 6 };
        int n = arr.length;
        printDistSum(arr, n);
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 program to prdistinct subset
# Sums of a given array.

# Uses Dynamic Programming to find
# distinct subset Sums
def printDistSum(arr, n):

    Sum = sum(arr)

    # dp[i][j] would be true if arr[0..i-1]
    # has a subset with Sum equal to j.
    dp = [[False for i in range(Sum + 1)]
                 for i in range(n + 1)]

    # There is always a subset with 0 Sum
    for i in range(n + 1):
        dp[i][0] = True

    # Fill dp[][] in bottom up manner
    for i in range(1, n + 1):

        dp[i][arr[i - 1]] = True

        for j in range(1, Sum + 1):

            # Sums that were achievable
            # without current array element
            if (dp[i - 1][j] == True):
                dp[i][j] = True
                dp[i][j + arr[i - 1]] = True

    # Print last row elements
    for j in range(Sum + 1):
        if (dp[n][j] == True):
            print(j, end = " ")

# Driver code
arr = [2, 3, 4, 5, 6]
n = len(arr)
printDistSum(arr, n)

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to print distinct
// subset sums of a given array.
using System;

class GFG {

    // Uses Dynamic Programming to
    // find distinct subset sums
    static void printDistSum(int []arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // dp[i][j] would be true if arr[0..i-1]
        // has a subset with sum equal to j.
        bool [,]dp = new bool[n + 1,sum + 1];

        // There is always a subset with 0 sum
        for (int i = 0; i <= n; i++)
            dp[i,0] = true;

        // Fill dp[][] in bottom up manner
        for (int i = 1; i <= n; i++)
        {
            dp[i,arr[i - 1]] = true;
            for (int j = 1; j <= sum; j++)
            {
                // Sums that were achievable
                // without current array element
                if (dp[i - 1,j] == true)
                {
                    dp[i,j] = true;
                    dp[i,j + arr[i - 1]] = true;
                }
            }
        }

        // Print last row elements
        for (int j = 0; j <= sum; j++)
            if (dp[n,j] == true)
                Console.Write(j + " ");
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 3, 4, 5, 6 };
        int n = arr.Length;
        printDistSum(arr, n);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// Javascript program to print distinct
// subset sums of a given array.

// Uses Dynamic Programming to find
// distinct subset sums
function printDistSum(arr, n)
{
    var sum = 0;
    for(var i = 0; i < n; i++)
        sum += arr[i];

    // dp[i][j] would be true if arr[0..i-1] has
    // a subset with sum equal to j.
    var dp = Array.from(
        Array(n + 1), () => Array(sum + 1).fill(0));

    // There is always a subset with 0 sum
    for(var i = 0; i <= n; i++)
        dp[i][0] = true;

    // Fill dp[][] in bottom up manner
    for(var i = 1; i <= n; i++)
    {
        dp[i][arr[i - 1]] = true;
        for(var j = 1; j <= sum; j++)
        {

            // Sums that were achievable
            // without current array element
            if (dp[i - 1][j] == true)
            {
                dp[i][j] = true;
                dp[i][j + arr[i - 1]] = true;
            }
        }
    }

    // Print last row elements
    for(var j = 0; j <= sum; j++)
        if (dp[n][j] == true)
            document.write(j + " ");
}

// Driver code
var arr = [ 2, 3, 4, 5, 6 ];
var n = arr.length;

printDistSum(arr, n);

// This code is contributed by importantly

</script>
```

**输出:**

```
0 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 20
```

上述方法的时间复杂度是 O(n*sum)，其中 n 是数组的大小，sum 是数组中所有整数的和。

本文由 **Karan Goyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。