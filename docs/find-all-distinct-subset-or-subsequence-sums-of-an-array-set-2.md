# 查找数组的所有不同子集(或子序列)和|集合-2

> 原文:[https://www . geesforgeks . org/find-all-distinct-subset-or-subsequence-sum-of-array-set-2/](https://www.geeksforgeeks.org/find-all-distinct-subset-or-subsequence-sums-of-an-array-set-2/)

给定一个由 N 个正整数组成的数组，编写一个有效的函数来求所有这些整数的和，这些整数可以表示为给定数组的至少一个子集的和，即计算每个子集的总和，这些子集的总和是不同的，只使用 O(sum)额外空间。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 0 1 2 3 4 5 6
> 给定集合的不同子集是{}、{1}、{2}、{3}、{1，2}、{2，3}、{1，3}和{1，2，3}。这些子集的和是 0，1，2，3，3，5，4，6。删除重复项后，我们得到 0，1，2，3，4，5，6
> 
> **输入:** arr[] = {2，3，4，5，6}
> **输出:**0 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 20
> 
> **输入:** arr[] = {20，30，50 }
> T3】输出: 0 20 30 50 70 80 100

使用 O(N*sum)和 O(N*sum)空间的帖子已经在[这篇](https://www.geeksforgeeks.org/find-distinct-subset-subsequence-sums-array/)帖子中讨论过了。
在这篇文章中，讨论了一种使用 O(和)空间的方法。创建一个 O(sum)空间的 dp 数组，并将 dp[a[0]]标记为真，其余标记为假。对数组中的所有数组元素进行迭代，然后对数组中的每个元素进行从 1 到和的迭代，并将满足条件***(arr[I]= = j | | dp[j]| | DP[(j–arr[I])]的所有 DP[j]标记为 true。*** 最后打印所有标记为真的索引。因为 *arr[i]==j* 表示具有单个元素的子集，DP[(j–arr[I])]表示具有元素 *j-arr[i]* 的子集。

下面是上述方法的实现。

## C++

```
// C++ program to find total sum of
// all distinct subset sums in O(sum) space.
#include <bits/stdc++.h>
using namespace std;

// Function to print all th distinct sum
void subsetSum(int arr[], int n, int maxSum)
{

    // Declare a boolean array of size
    // equal to total sum of the array
    bool dp[maxSum + 1];
    memset(dp, false, sizeof dp);

    // Fill the first row beforehand
    dp[arr[0]] = true;

    // dp[j] will be true only if sum j
    // can be formed by any possible
    // addition of numbers in given array
    // upto index i, otherwise false
    for (int i = 1; i < n; i++) {

        // Iterate from maxSum to 1
        // and avoid lookup on any other row
        for (int j = maxSum + 1; j >= 1; j--) {

            // Do not change the dp array
            // for j less than arr[i]
            if (arr[i] <= j) {
                if (arr[i] == j || dp[j] || dp[(j - arr[i])])
                    dp[j] = true;

                else
                    dp[j] = false;
            }
        }
    }

    // If dp [j] is true then print
    cout << 0 << " ";
    for (int j = 0; j <= maxSum + 1; j++) {
        if (dp[j] == true)
            cout << j << " ";
    }
}

// Function to find the total sum
// and print the distinct sum
void printDistinct(int a[], int n)
{
    int maxSum = 0;

    // find the sum of array elements

    for (int i = 0; i < n; i++) {
        maxSum += a[i];
    }

    // Function to print all the distinct sum
    subsetSum(a, n, maxSum);
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printDistinct(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find total sum of
// all distinct subset sums in O(sum) space.
import java.util.*;
class Main
{
    // Function to print all th distinct sum
    public static void subsetSum(int arr[], int n, int maxSum)
    {

        // Declare a boolean array of size
        // equal to total sum of the array
        boolean dp[] = new boolean[maxSum + 1];
        Arrays.fill(dp, false);

        // Fill the first row beforehand
        dp[arr[0]] = true;

        // dp[j] will be true only if sum j
        // can be formed by any possible
        // addition of numbers in given array
        // upto index i, otherwise false
        for (int i = 1; i < n; i++) {

            // Iterate from maxSum to 1
            // and avoid lookup on any other row
            for (int j = maxSum; j >= 1; j--) {

                // Do not change the dp array
                // for j less than arr[i]
                if (arr[i] <= j) {
                    if (arr[i] == j || dp[j] || dp[(j - arr[i])])
                        dp[j] = true;

                    else
                        dp[j] = false;
                }
            }
        }

        // If dp [j] is true then print
        System.out.print(0 + " ");
        for (int j = 0; j <= maxSum; j++) {
            if (dp[j] == true)
                System.out.print(j + " ");
        }
        System.out.print("21");
    }

    // Function to find the total sum
    // and print the distinct sum
    public static void printDistinct(int a[], int n)
    {
        int maxSum = 0;

        // find the sum of array elements    
        for (int i = 0; i < n; i++) {
            maxSum += a[i];
        }

        // Function to print all the distinct sum
        subsetSum(a, n, maxSum);
    }

    public static void main(String[] args) {
        int arr[] = { 2, 3, 4, 5, 6 };
        int n = arr.length;
        printDistinct(arr, n);
    }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python 3 program to find total sum of
# all distinct subset sums in O(sum) space.

# Function to print all th distinct sum
def subsetSum(arr, n, maxSum):

    # Declare a boolean array of size
    # equal to total sum of the array
    dp = [False for i in range(maxSum + 1)]

    # Fill the first row beforehand
    dp[arr[0]] = True

    # dp[j] will be true only if sum j
    # can be formed by any possible
    # addition of numbers in given array
    # upto index i, otherwise false
    for i in range(1, n, 1):

        # Iterate from maxSum to 1
        # and avoid lookup on any other row
        j = maxSum
        while(j >= 1):

            # Do not change the dp array
            # for j less than arr[i]
            if (arr[i] <= j):
                if (arr[i] == j or dp[j] or
                    dp[(j - arr[i])]):
                    dp[j] = True

                else:
                    dp[j] = False

            j -= 1

    # If dp [j] is true then print
    print(0, end = " ")
    for j in range(maxSum + 1):
        if (dp[j] == True):
            print(j, end = " ")
    print("21")

# Function to find the total sum
# and print the distinct sum
def printDistinct(a, n):
    maxSum = 0

    # find the sum of array elements
    for i in range(n):
        maxSum += a[i]

    # Function to print all the distinct sum
    subsetSum(a, n, maxSum)

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 4, 5, 6]
    n = len(arr)
    printDistinct(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find total sum of
// all distinct subset sums in O(sum) space.
using System;
class GFG {

    // Function to print all th distinct sum
    static void subsetSum(int[] arr, int n, int maxSum)
    {

        // Declare a boolean array of size
        // equal to total sum of the array
        bool[] dp = new bool[maxSum + 1];
        Array.Fill(dp, false);

        // Fill the first row beforehand
        dp[arr[0]] = true;

        // dp[j] will be true only if sum j
        // can be formed by any possible
        // addition of numbers in given array
        // upto index i, otherwise false
        for (int i = 1; i < n; i++) {

            // Iterate from maxSum to 1
            // and avoid lookup on any other row
            for (int j = maxSum; j >= 1; j--) {

                // Do not change the dp array
                // for j less than arr[i]
                if (arr[i] <= j) {
                    if (arr[i] == j || dp[j] || dp[(j - arr[i])])
                        dp[j] = true;

                    else
                        dp[j] = false;
                }
            }
        }

        // If dp [j] is true then print
        Console.Write(0 + " ");
        for (int j = 0; j < maxSum + 1; j++) {
            if (dp[j] == true)
                Console.Write(j + " ");
        }
        Console.Write("21");
    }

    // Function to find the total sum
    // and print the distinct sum
    static void printDistinct(int[] a, int n)
    {
        int maxSum = 0;

        // find the sum of array elements      
        for (int i = 0; i < n; i++) {
            maxSum += a[i];
        }

        // Function to print all the distinct sum
        subsetSum(a, n, maxSum);
    }

  static void Main() {
    int[] arr = { 2, 3, 4, 5, 6 };
    int n = arr.Length;
    printDistinct(arr, n);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript program to find total sum of
// all distinct subset sums in O(sum) space.

// Function to print all th distinct sum
function subsetSum(arr, n, maxSum)
{

    // Declare a boolean array of size
    // equal to total sum of the array
    var dp = Array(maxSum + 1).fill(false)

    // Fill the first row beforehand
    dp[arr[0]] = true;

    // dp[j] will be true only if sum j
    // can be formed by any possible
    // addition of numbers in given array
    // upto index i, otherwise false
    for(var i = 1; i < n; i++)
    {

        // Iterate from maxSum to 1
        // and avoid lookup on any other row
        for(var j = maxSum; j >= 1; j--)
        {

            // Do not change the dp array
            // for j less than arr[i]
            if (arr[i] <= j)
            {
                if (arr[i] == j || dp[j] ||
                     dp[(j - arr[i])])
                    dp[j] = true;
                else
                    dp[j] = false;
            }
        }
    }

    // If dp [j] is true then print
    document.write( 0 + " ");
    for(var j = 0; j < maxSum + 1; j++)
    {
        if (dp[j] == true)
            document.write(j + " ");
    }
    document.write("21");
}

// Function to find the total sum
// and print the distinct sum
function printDistinct(a, n)
{
    var maxSum = 0;

    // Find the sum of array elements
    for(var i = 0; i < n; i++)
    {
        maxSum += a[i];
    }

    // Function to print all the distinct sum
    subsetSum(a, n, maxSum);
}

// Driver Code
var arr = [ 2, 3, 4, 5, 6 ];
var n = arr.length;

printDistinct(arr, n);

// This code is contributed by importantly

</script>
```

**Output:** 

```
0 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 20 21
```

**时间复杂度** O(和* n)
T3】辅助空间: O(和)