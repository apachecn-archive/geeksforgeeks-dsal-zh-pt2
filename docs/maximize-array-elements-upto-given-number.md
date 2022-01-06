# 将数组元素最大化至给定数量

> 原文:[https://www . geesforgeks . org/maximum-array-elements-up-给定-number/](https://www.geeksforgeeks.org/maximize-array-elements-upto-given-number/)

给定一个整数数组、一个数字和一个最大值，任务是计算可以从数组元素中获得的最大值。从开始遍历的数组中的每个值都可以与从先前索引中获得的结果相加或相减，以便在任何时候结果都不小于 0 且不大于给定的最大值。对于索引 0，取等于给定数字的先前结果。如果没有可能的答案，打印-1。

**示例:**

```
Input : arr[] = {2, 1, 7}
        Number = 3
        Maximum value = 7
Output : 7
The order of addition and subtraction
is: 3(given number) - 2(arr[0]) - 
1(arr[1]) + 7(arr[2]).

Input : arr[] = {3, 10, 6, 4, 5}
        Number = 1
        Maximum value = 15
Output : 9
The order of addition and subtraction
is: 1 + 3 + 10 - 6 - 4 + 5
```

[Recommended : Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org)

**先决条件:** [动态编程](https://www.geeksforgeeks.org/dynamic-programming/) | [递归](https://www.geeksforgeeks.org/recursion/)。
**天真法:**用递归求最大值。在每个索引位置都有两个选择，要么将当前数组元素添加到迄今为止从先前元素获得的值中，要么从迄今为止从先前元素获得的值中减去当前数组元素。从索引 0 开始，从给定的数字中加或减 arr[0]，并递归调用下一个索引和更新的数字。遍历整个数组时，将更新后的数字与目前获得的数字的最大值进行比较。

**以下是上述方法的实施:**

## C++

```
// CPP code to find maximum
// value of number obtained by
// using array elements recursively.
#include <bits/stdc++.h>
using namespace std;

// Utility function to find maximum possible value
void findMaxValUtil(int arr[], int n, int num,
                    int maxLimit, int ind, int& ans)
{
    // If entire array is traversed, then compare
    // current value in num to overall maximum
    // obtained so far.
    if (ind == n) {
        ans = max(ans, num);
        return;
    }

    // Case 1: Subtract current element from value so
    // far if result is greater than or equal to zero.
    if (num - arr[ind] >= 0)
    {
        findMaxValUtil(arr, n, num - arr[ind],
                       maxLimit, ind + 1, ans);
    }

    // Case 2 : Add current element to value so far
    // if result is less than or equal to maxLimit.
    if (num + arr[ind] <= maxLimit)
    {
        findMaxValUtil(arr, n, num + arr[ind],
                       maxLimit, ind + 1, ans);
    }
}

// Function to find maximum possible
// value that can be obtained using
// array elements and given number.
int findMaxVal(int arr[], int n,
               int num, int maxLimit)
{
    // variable to store maximum value
    // that can be obtained.
    int ans = 0;

    // variable to store current index position.
    int ind = 0;

    // call to utility function to find maximum
    // possible value that can be obtained.
    findMaxValUtil(arr, n, num, maxLimit, ind, ans);

    return ans;
}

// Driver code
int main()
{
    int num = 1;
    int arr[] = { 3, 10, 6, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int maxLimit = 15;

    cout << findMaxVal(arr, n, num, maxLimit);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find maximum
// value of number obtained by
// using array elements recursively.
import java.io.*;
import java.lang.*;

public class GFG {

    // variable to store maximum value
    // that can be obtained.
    static int ans;

    // Utility function to find maximum
    // possible value
    static void findMaxValUtil(int []arr, int n, int num,
                              int maxLimit, int ind)
    {

        // If entire array is traversed, then compare
        // current value in num to overall maximum
        // obtained so far.
        if (ind == n) {
            ans = Math.max(ans, num);
            return;
        }

        // Case 1: Subtract current element from value so
        // far if result is greater than or equal to zero.
        if (num - arr[ind] >= 0)
        {
            findMaxValUtil(arr, n, num - arr[ind],
                            maxLimit, ind + 1);
        }

        // Case 2 : Add current element to value so far
        // if result is less than or equal to maxLimit.
        if (num + arr[ind] <= maxLimit)
        {
            findMaxValUtil(arr, n, num + arr[ind],
                          maxLimit, ind + 1);
        }
    }

    // Function to find maximum possible
    // value that can be obtained using
    // array elements and given number.
    static int findMaxVal(int []arr, int n,
                             int num, int maxLimit)
    {

        // variable to store current index position.
        int ind = 0;

        // call to utility function to find maximum
        // possible value that can be obtained.
        findMaxValUtil(arr, n, num, maxLimit, ind);

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int num = 1;
        int []arr = { 3, 10, 6, 4, 5 };
        int n = arr.length;
        int maxLimit = 15;

        System.out.print(findMaxVal(arr, n, num,
                                        maxLimit));
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 code to find maximum
# value of number obtained by
# using array elements recursively.

# Utility def to find
# maximum possible value

# variable to store maximum value
# that can be obtained.
ans = 0;
def findMaxValUtil(arr, n, num, maxLimit, ind):
    global ans

    # If entire array is traversed,
    # then compare current value
    # in num to overall maximum
    # obtained so far.
    if (ind == n) :
        ans = max(ans, num)
        return

    # Case 1: Subtract current element
    # from value so far if result is
    # greater than or equal to zero.
    if (num - arr[ind] >= 0) :
        findMaxValUtil(arr, n, num - arr[ind],
                            maxLimit, ind + 1)

    # Case 2 : Add current element to
    # value so far if result is less
    # than or equal to maxLimit.
    if (num + arr[ind] <= maxLimit) :
        findMaxValUtil(arr, n, num + arr[ind],
                            maxLimit, ind + 1)

# def to find maximum possible
# value that can be obtained using
# array elements and given number.
def findMaxVal(arr, n, num, maxLimit) :
    global ans
    # variable to store
    # current index position.
    ind = 0

    # call to utility def to
    # find maximum possible value
    # that can be obtained.
    findMaxValUtil(arr, n, num, maxLimit, ind)
    return ans

# Driver code
num = 1
arr = [3, 10, 6, 4, 5]
n = len(arr)
maxLimit = 15

print (findMaxVal(arr, n, num, maxLimit))

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# code to find maximum
// value of number obtained by
// using array elements recursively.
using System;
using System.Collections.Generic;

class GFG {

    // Utility function to find maximum
    // possible value
    static void findMaxValUtil(int []arr, int n, int num,
                      int maxLimit, int ind, ref int ans)
    {

        // If entire array is traversed, then compare
        // current value in num to overall maximum
        // obtained so far.
        if (ind == n) {
            ans = Math.Max(ans, num);
            return;
        }

        // Case 1: Subtract current element from value so
        // far if result is greater than or equal to zero.
        if (num - arr[ind] >= 0)
        {
            findMaxValUtil(arr, n, num - arr[ind],
                            maxLimit, ind + 1, ref ans);
        }

        // Case 2 : Add current element to value so far
        // if result is less than or equal to maxLimit.
        if (num + arr[ind] <= maxLimit)
        {
            findMaxValUtil(arr, n, num + arr[ind],
                          maxLimit, ind + 1, ref ans);
        }
    }

    // Function to find maximum possible
    // value that can be obtained using
    // array elements and given number.
    static int findMaxVal(int []arr, int n,
                             int num, int maxLimit)
    {

        // variable to store maximum value
        // that can be obtained.
        int ans = 0;

        // variable to store current index position.
        int ind = 0;

        // call to utility function to find maximum
        // possible value that can be obtained.
        findMaxValUtil(arr, n, num, maxLimit, ind,
                                           ref ans);

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int num = 1;
        int []arr = { 3, 10, 6, 4, 5 };
        int n = arr.Length;
        int maxLimit = 15;

        Console.Write(findMaxVal(arr, n, num,
                                        maxLimit));
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find maximum
// value of number obtained by
// using array elements recursively.

// Utility function to find
// maximum possible value
function findMaxValUtil($arr, $n,
                        $num, $maxLimit,
                        $ind, &$ans)
{
    // If entire array is traversed,
    // then compare current value
    // in num to overall maximum
    // obtained so far.
    if ($ind == $n)
    {
        $ans = max($ans, $num);
        return;
    }

    // Case 1: Subtract current element
    // from value so far if result is
    // greater than or equal to zero.
    if ($num - $arr[$ind] >= 0)
    {
        findMaxValUtil($arr, $n,
                       $num - $arr[$ind],
                       $maxLimit, $ind + 1,
                       $ans);
    }

    // Case 2 : Add current element to
    // value so far if result is less
    // than or equal to maxLimit.
    if ($num + $arr[$ind] <= $maxLimit)
    {
        findMaxValUtil($arr, $n,
                       $num + $arr[$ind],
                       $maxLimit, $ind + 1,
                       $ans);
    }
}

// Function to find maximum possible
// value that can be obtained using
// array elements and given number.
function findMaxVal($arr, $n,
                    $num, $maxLimit)
{
    // variable to store maximum value
    // that can be obtained.
    $ans = 0;

    // variable to store
    // current index position.
    $ind = 0;

    // call to utility function to
    // find maximum possible value
    // that can be obtained.
    findMaxValUtil($arr, $n, $num,
                   $maxLimit, $ind, $ans);

    return $ans;
}

// Driver code
$num = 1;
$arr = array(3, 10, 6, 4, 5);
$n = count($arr);
$maxLimit = 15;

echo (findMaxVal($arr, $n, $num, $maxLimit));

//This code is contributed by Manish Shaw
//(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript code to find maximum
// value of number obtained by
// using array elements recursively.

// variable to store maximum value
// that can be obtained.
let ans = 0;

// Utility function to find maximum
// possible value
function findMaxValUtil(arr, n, num, maxLimit, ind)
{

    // If entire array is traversed, then
    // compare current value in num to
    // overall maximum obtained so far.
    if (ind == n)
    {
        ans = Math.max(ans, num);
        return;
    }

    // Case 1: Subtract current element
    // from value so far if result is
    // greater than or equal to zero.
    if (num - arr[ind] >= 0)
    {
        findMaxValUtil(arr, n, num - arr[ind],
                     maxLimit, ind + 1);
    }

    // Case 2 : Add current element to value so far
    // if result is less than or equal to maxLimit.
    if (num + arr[ind] <= maxLimit)
    {
        findMaxValUtil(arr, n, num + arr[ind],
                     maxLimit, ind + 1);
    }
}

// Function to find maximum possible
// value that can be obtained using
// array elements and given number.
function findMaxVal(arr, n, num, maxLimit)
{

    // Variable to store current index position.
    let ind = 0;

    // Call to utility function to find maximum
    // possible value that can be obtained.
    findMaxValUtil(arr, n, num, maxLimit, ind);

    return ans;
}

// Driver code
let num = 1;
let arr = [ 3, 10, 6, 4, 5 ];
let n = arr.length;
let maxLimit = 15;

document.write(findMaxVal(arr, n, num,
                          maxLimit));

// This code is contributed by mukesh07  

</script>
```

**Output:** 

```
9
```

**时间复杂度:** O(2^n).

**注:**对于 n < = 20 的小数值，此解有效。但是随着阵列大小的增加，这将不是最佳解决方案。

一个有效的解决方案是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。请注意，每一步的值都被限制在 0 和最大极限之间，因此，所需的最大值也将在此范围内。在每个索引位置，将 arr[i]添加到结果中或从结果中减去后，结果的新值也将位于此范围内。让我们尝试反向构建解决方案。假设要求的最大可能值为 x，其中 0 ≤ x ≤ maxLimit。该值 x 是通过将 arr[n-1]加到所获得的值或从所获得的值中减去 arr[n-1]直到索引位置 n-2 而获得的。对于在索引位置 n-2 获得的值，可以给出相同的理由，即它依赖于索引位置 n-3 的值，以此类推。得到的递归关系可以表示为:

```
Check can x be obtained from arr[0..n-1]:
   Check can x - arr[n-1] be obtained from arr[0..n-2] 
   || Check can x + arr[n-1] be obtained from arr[0..n-2]
```

如果可以使用 arr[0]获得值 j，则可以创建一个布尔 DP 表，其中 dp[i][j]为 1..i]如果不是，则为 0。对于每个索引位置，从 j = 0 开始，移动到 maxLimit 值，并如上所述将 dp[i][j]设置为 0 或 1。当 i = n-1 且 dp[n-1][j] = 1 时，通过找到最大 j，找到在索引位置 n-1 可以获得的最大可能值。

## C++

```
// C++ program to find maximum value of
// number obtained by using array
// elements by using dynamic programming.
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum possible
// value of number that can be
// obtained using array elements.
int findMaxVal(int arr[], int n,
               int num, int maxLimit)
{
    // Variable to represent current index.
    int ind;

    // Variable to show value between
    //  0 and maxLimit.
    int val;

    // Table to store whether a value can
    // be obtained or not upto a certain index.
    // 1\. dp[i][j] = 1 if value j can be
    //    obtained upto index i.
    // 2\. dp[i][j] = 0 if value j cannot be
    //    obtained upto index i.
    int dp[n][maxLimit+1];

    for(ind = 0; ind < n; ind++)
    {
        for(val = 0; val <= maxLimit; val++)
        {
            // Check for index 0 if given value
            // val can be obtained by either adding
            // to or subtracting arr[0] from num.
            if(ind == 0)
            {
                if(num - arr[ind] == val ||
                    num + arr[ind] == val)
                {
                    dp[ind][val] = 1;
                }
                else
                {
                    dp[ind][val] = 0;
                }
            }
            else
            {
                // 1\. If arr[ind] is added to
                // obtain given val then val-
                // arr[ind] should be obtainable
                // from index ind-1.
                // 2\. If arr[ind] is subtracted to
                // obtain given val then val+arr[ind]
                // should be obtainable from index ind-1.
                // Check for both the conditions.
                if(val - arr[ind] >= 0 &&
                   val + arr[ind] <= maxLimit)
                {
                    // If either of one condition is true,
                    // then val is obtainable at index ind.
                    dp[ind][val] = dp[ind-1][val-arr[ind]] ||
                                     dp[ind-1][val+arr[ind]];
                }
                else if(val - arr[ind] >= 0)
                {
                    dp[ind][val] = dp[ind-1][val-arr[ind]];
                }
                else if(val + arr[ind] <= maxLimit)
                {
                    dp[ind][val] = dp[ind-1][val+arr[ind]];
                }
                else
                {
                    dp[ind][val] = 0;
                }
            }
        }
    }

    // Find maximum value that is obtained
    // at index n-1.
    for(val = maxLimit; val >= 0; val--)
    {
        if(dp[n-1][val])
        {
            return val;
        }
    }

    // If no solution exists return -1.
    return -1;
}

// Driver Code
int main()
{
    int num = 1;
    int arr[] = {3, 10, 6, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    int maxLimit = 15;

    cout << findMaxVal(arr, n, num, maxLimit);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// value of number obtained by
// using array elements by using
// dynamic programming.
import java.io.*;

class GFG
{

    // Function to find maximum
    // possible value of number
    // that can be obtained
    // using array elements.
    static int findMaxVal(int []arr, int n,
                          int num, int maxLimit)
    {

        // Variable to represent
        // current index.
        int ind;

        // Variable to show value
        // between 0 and maxLimit.
        int val;

        // Table to store whether
        // a value can be obtained
        // or not upto a certain
        // index 1\. dp[i,j] = 1 if
        // value j can be obtained
        // upto index i.
        // 2\. dp[i,j] = 0 if value j
        // cannot be obtained upto index i.
        int [][]dp = new int[n][maxLimit + 1];

        for(ind = 0; ind < n; ind++)
        {
            for(val = 0; val <= maxLimit; val++)
            {
                // Check for index 0 if given
                // value val can be obtained
                // by either adding to or
                // subtracting arr[0] from num.
                if(ind == 0)
                {
                    if(num - arr[ind] == val ||
                       num + arr[ind] == val)
                    {
                        dp[ind][val] = 1;
                    }
                    else
                    {
                        dp[ind][val] = 0;
                    }
                }
                else
                {
                    // 1\. If arr[ind] is added
                    // to obtain given val then
                    // val- arr[ind] should be
                    // obtainable from index
                    // ind-1.
                    // 2\. If arr[ind] is subtracted
                    // to obtain given val then
                    // val+arr[ind] should be
                    // obtainable from index ind-1.
                    // Check for both the conditions.
                    if(val - arr[ind] >= 0 &&
                        val + arr[ind] <= maxLimit)
                    {

                        // If either of one condition
                        // is true, then val is
                        // obtainable at index ind.
                        if(dp[ind - 1][val - arr[ind]] == 1
                        || dp[ind - 1][val + arr[ind]] == 1)
                            dp[ind][val] = 1;

                    }
                    else if(val - arr[ind] >= 0)
                    {
                        dp[ind][val] = dp[ind - 1][val -
                                                   arr[ind]];
                    }
                    else if(val + arr[ind] <= maxLimit)
                    {
                        dp[ind][val] = dp[ind - 1][val +
                                                   arr[ind]];
                    }
                    else
                    {
                        dp[ind][val] = 0;
                    }
                }
            }
        }

        // Find maximum value that
        // is obtained at index n-1.
        for(val = maxLimit; val >= 0; val--)
        {
            if(dp[n - 1][val] == 1)
            {
                return val;
            }
        }

        // If no solution
        // exists return -1.
        return -1;
    }

    // Driver Code
    public static void main(String args[])
    {
        int num = 1;
        int []arr = new int[]{3, 10, 6, 4, 5};
        int n = arr.length;
        int maxLimit = 15;

        System.out.print(findMaxVal(arr, n,
                                    num, maxLimit));
    }
}

// This code is contributed
// by Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find maximum
# value of number obtained by
# using array elements by using
# dynamic programming.

# Function to find maximum
# possible value of number
# that can be obtained
# using array elements.
def findMaxVal(arr, n, num, maxLimit):

    # Variable to represent
    # current index.
    ind = -1;

    # Variable to show value
    # between 0 and maxLimit.
    val = -1;

    # Table to store whether
    # a value can be obtained
    # or not upto a certain
    # index 1\. dp[i,j] = 1 if
    # value j can be obtained
    # upto index i.
    # 2\. dp[i,j] = 0 if value j
    # cannot be obtained upto index i.
    dp = [[0 for i in range(maxLimit + 1)] for j in range(n)];

    for ind in range(n):
        for val in range(maxLimit + 1):

            # Check for index 0 if given
            # value val can be obtained
            # by either adding to or
            # subtracting arr[0] from num.
            if (ind == 0):
                if (num - arr[ind] == val or num + arr[ind] == val):
                    dp[ind][val] = 1;
                else:
                    dp[ind][val] = 0;

            else:

                # 1\. If arr[ind] is added
                # to obtain given val then
                # val- arr[ind] should be
                # obtainable from index
                # ind-1.
                # 2\. If arr[ind] is subtracted
                # to obtain given val then
                # val+arr[ind] should be
                # obtainable from index ind-1.
                # Check for both the conditions.
                if (val - arr[ind] >= 0 and val + arr[ind] <= maxLimit):

                    # If either of one condition
                    # is True, then val is
                    # obtainable at index ind.
                    if (dp[ind - 1][val - arr[ind]] == 1 or
                        dp[ind - 1][val + arr[ind]] == 1):
                        dp[ind][val] = 1;

                elif (val - arr[ind] >= 0):
                    dp[ind][val] = dp[ind - 1][val - arr[ind]];
                elif (val + arr[ind] <= maxLimit):
                    dp[ind][val] = dp[ind - 1][val + arr[ind]];
                else:
                    dp[ind][val] = 0;

    # Find maximum value that
    # is obtained at index n-1.
    for val in range(maxLimit, -1, -1):
        if (dp[n - 1][val] == 1):
            return val;

    # If no solution
    # exists return -1.
    return -1;

# Driver Code
if __name__ == '__main__':
    num = 1;
    arr = [3, 10, 6, 4, 5];
    n = len(arr);
    maxLimit = 15;

    print(findMaxVal(arr, n, num, maxLimit));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find maximum value of
// number obtained by using array
// elements by using dynamic programming.
using System;

class GFG {

    // Function to find maximum possible
    // value of number that can be
    // obtained using array elements.
    static int findMaxVal(int []arr, int n,
                    int num, int maxLimit)
    {

        // Variable to represent current index.
        int ind;

        // Variable to show value between
        // 0 and maxLimit.
        int val;

        // Table to store whether a value can
        // be obtained or not upto a certain
        // index 1\. dp[i,j] = 1 if value j
        // can be obtained upto index i.
        // 2\. dp[i,j] = 0 if value j cannot be
        // obtained upto index i.
        int [,]dp = new int[n,maxLimit+1];

        for(ind = 0; ind < n; ind++)
        {
            for(val = 0; val <= maxLimit; val++)
            {
                // Check for index 0 if given
                // value val can be obtained
                // by either adding to or
                // subtracting arr[0] from num.
                if(ind == 0)
                {
                    if(num - arr[ind] == val ||
                        num + arr[ind] == val)
                    {
                        dp[ind,val] = 1;
                    }
                    else
                    {
                        dp[ind,val] = 0;
                    }
                }
                else
                {
                    // 1\. If arr[ind] is added
                    // to obtain given val then
                    // val- arr[ind] should be
                    // obtainable from index
                    // ind-1.
                    // 2\. If arr[ind] is subtracted
                    // to obtain given val then
                    // val+arr[ind] should be
                    // obtainable from index ind-1.
                    // Check for both the conditions.
                    if(val - arr[ind] >= 0 &&
                         val + arr[ind] <= maxLimit)
                    {

                        // If either of one condition
                        // is true, then val is
                        // obtainable at index ind.
                        if(dp[ind-1,val-arr[ind]] == 1
                        || dp[ind-1,val+arr[ind]] == 1)
                            dp[ind,val] = 1;

                    }
                    else if(val - arr[ind] >= 0)
                    {
                        dp[ind,val] = dp[ind-1,val-arr[ind]];
                    }
                    else if(val + arr[ind] <= maxLimit)
                    {
                        dp[ind,val] = dp[ind-1,val+arr[ind]];
                    }
                    else
                    {
                        dp[ind,val] = 0;
                    }
                }
            }
        }

        // Find maximum value that is obtained
        // at index n-1.
        for(val = maxLimit; val >= 0; val--)
        {
            if(dp[n-1,val] == 1)
            {
                return val;
            }
        }

        // If no solution exists return -1.
        return -1;
    }

    // Driver Code
    static void Main()
    {
        int num = 1;
        int []arr = new int[]{3, 10, 6, 4, 5};
        int n = arr.Length;
        int maxLimit = 15;

        Console.Write(
             findMaxVal(arr, n, num, maxLimit));
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum value of
// number obtained by using array
// elements by using dynamic programming.

// Function to find maximum possible
// value of number that can be
// obtained using array elements.
function findMaxVal($arr, $n, $num,
                         $maxLimit)
{
    // Variable to represent
    // current index.
    $ind;

    // Variable to show value between
    // 0 and maxLimit.
    $val;

    // Table to store whether a value can
    // be obtained or not upto a certain index.
    // 1\. dp[i][j] = 1 if value j can be
    //             obtained upto index i.
    // 2\. dp[i][j] = 0 if value j cannot be
    //                obtained upto index i.
    $dp[$n][$maxLimit + 1] = array();

    for($ind = 0; $ind < $n; $ind++)
    {
        for($val = 0;
            $val <= $maxLimit; $val++)
        {
            // Check for index 0 if given value
            // val can be obtained by either adding
            // to or subtracting arr[0] from num.
            if($ind == 0)
            {
                if($num - $arr[$ind] == $val ||
                   $num + $arr[$ind] == $val)
                {
                    $dp[$ind][$val] = 1;
                }
                else
                {
                    $dp[$ind][$val] = 0;
                }
            }
            else
            {
                // 1\. If arr[ind] is added to
                // obtain given val then val-
                // arr[ind] should be obtainable
                // from index ind-1.
                // 2\. If arr[ind] is subtracted to
                // obtain given val then val+arr[ind]
                // should be obtainable from index ind-1.
                // Check for both the conditions.
                if($val - $arr[$ind] >= 0 &&
                   $val + $arr[$ind] <= $maxLimit)
                {
                    // If either of one condition is true,
                    // then val is obtainable at index ind.
                    $dp[$ind][$val] = $dp[$ind - 1][$val - $arr[$ind]] ||
                                      $dp[$ind - 1][$val + $arr[$ind]];
                }
                else if($val - $arr[$ind] >= 0)
                {
                    $dp[$ind][$val] = $dp[$ind - 1][$val - $arr[$ind]];
                }
                else if($val + $arr[$ind] <= $maxLimit)
                {
                    $dp[$ind][$val] = $dp[$ind - 1][$val + $arr[$ind]];
                }
                else
                {
                    $dp[$ind][$val] = 0;
                }
            }
        }
    }

    // Find maximum value that is obtained
    // at index n-1.
    for($val = $maxLimit; $val >= 0; $val--)
    {
        if($dp[$n - 1][$val])
        {
            return $val;
        }
    }

    // If no solution exists return -1.
    return -1;
}

// Driver Code
$num = 1;
$arr = array(3, 10, 6, 4, 5);
$n = sizeof($arr);
$maxLimit = 15;

echo findMaxVal($arr, $n, $num, $maxLimit);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum value of
// number obtained by using array
// elements by using dynamic programming.

// Function to find maximum possible
// value of number that can be
// obtained using array elements.
function findMaxVal(arr, n, num, maxLimit)
{
    // Variable to represent current index.
    var ind;

    // Variable to show value between
    //  0 and maxLimit.
    var val;

    // Table to store whether a value can
    // be obtained or not upto a certain index.
    // 1\. dp[i][j] = 1 if value j can be
    //    obtained upto index i.
    // 2\. dp[i][j] = 0 if value j cannot be
    //    obtained upto index i.
    var dp = Array.from( Array(n), () => Array(maxLimit+1));

    for(ind = 0; ind < n; ind++)
    {
        for(val = 0; val <= maxLimit; val++)
        {
            // Check for index 0 if given value
            // val can be obtained by either adding
            // to or subtracting arr[0] from num.
            if(ind == 0)
            {
                if(num - arr[ind] == val ||
                    num + arr[ind] == val)
                {
                    dp[ind][val] = 1;
                }
                else
                {
                    dp[ind][val] = 0;
                }
            }
            else
            {
                // 1\. If arr[ind] is added to
                // obtain given val then val-
                // arr[ind] should be obtainable
                // from index ind-1.
                // 2\. If arr[ind] is subtracted to
                // obtain given val then val+arr[ind]
                // should be obtainable from index ind-1.
                // Check for both the conditions.
                if(val - arr[ind] >= 0 &&
                   val + arr[ind] <= maxLimit)
                {
                    // If either of one condition is true,
                    // then val is obtainable at index ind.
                    dp[ind][val] = dp[ind-1][val-arr[ind]] ||
                                     dp[ind-1][val+arr[ind]];
                }
                else if(val - arr[ind] >= 0)
                {
                    dp[ind][val] = dp[ind-1][val-arr[ind]];
                }
                else if(val + arr[ind] <= maxLimit)
                {
                    dp[ind][val] = dp[ind-1][val+arr[ind]];
                }
                else
                {
                    dp[ind][val] = 0;
                }
            }
        }
    }

    // Find maximum value that is obtained
    // at index n-1.
    for(val = maxLimit; val >= 0; val--)
    {
        if(dp[n-1][val])
        {
            return val;
        }
    }

    // If no solution exists return -1.
    return -1;
}

// Driver Code
var num = 1;
var arr = [3, 10, 6, 4, 5];
var n = arr.length;
var maxLimit = 15;

document.write( findMaxVal(arr, n, num, maxLimit));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
9
```

**时间复杂度:** O(n*maxLimit)，其中 n 是数组的大小，maxLimit 是给定的最大值。
**辅助空间:** O(n*maxLimit)，n 是数组的大小，maxLimit 是给定的最大值。
**优化:**所需空间可以减少到 O(2*maxLimit)。请注意，在每个索引位置，我们只使用前一行的值。因此，我们可以创建一个包含两行的表，其中一行存储上一次迭代的结果，另一行存储当前迭代的结果。