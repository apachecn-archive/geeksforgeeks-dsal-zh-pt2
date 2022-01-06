# 使前缀和的相邻元素对的乘积为负的最小运算

> 原文:[https://www . geeksforgeeks . org/最小操作-生成相邻元素对的乘积-前缀-和-负数/](https://www.geeksforgeeks.org/minimum-operations-to-make-product-of-adjacent-element-pair-of-prefix-sum-negative/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[ ]** ，考虑一个[数组**前缀[ ]**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) ，其中**前缀【I】**是 **arr** 的第一个 **i** 元素之和。任务是找到修改给定数组所需的最小操作数，使得**前缀**数组中任意两个相邻元素的乘积为负。在一个操作中，您可以将任何元素的值递增或递减 1。

> **输入:** arr[] = {1，-3，1，0}
> **输出:** 4
> **说明:**序列可以通过 4 次运算转化为 1，-2，2，-2，前缀之和为 1，-1，1，-1，满足所有条件。
> 
> **输入:**arr[]= {-1 4 3 2-5 4 }
> T3】输出: 8

**方法:**想法是尝试两种独立的可能性，要么偶数长度前缀和为正，要么奇数长度前缀和为负，反之亦然。按照以下步骤解决问题:

*   初始化一个变量**RES =**[**INT _ MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)来存储最小操作数。
*   [使用变量 **r.** 遍历范围](https://www.geeksforgeeks.org/range-based-loop-c/)【0，1】
    *   初始化变量 **ans = 0** 和 **sum = 0** 分别存储总操作数和当前前缀和。
    *   [使用变量 **i、**遍历范围](https://www.geeksforgeeks.org/range-based-loop-c/)【0，N-1】
        *   将**arr【I】**加到 **sum** 的值上。
        *   如果 **(i+r)** 的[值为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，如果**和**不为正，则将**和+1** 加到**和**上，并将**和**的值更新为 1。
        *   否则，如果 [**(i+r)** 为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，如果**和**不为负数，则将**和+1** 加到**和**上，将**和**的值更新为-1。
    *   将 res 值更新为最小值(res，ans)。
*   完成上述步骤后，打印 **res** 的值。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum operations
// needed to make the product of any
// two adjacent elements in prefix
// sum array negative
void minOperations(vector<int> a)
{
    // Stores the minimum operations
    int res = INT_MAX;
    int N = a.size();

    for (int r = 0; r < 2; r++) {
        // Stores the prefix sum
        // and number of operations
        int sum = 0, ans = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {
            // Update the value of sum
            sum += a[i];
            // Check if i+r is odd
            if ((i + r) % 2) {

                // Check if prefix sum
                // is not positive
                if (sum <= 0) {

                    // Update the value of
                    // ans and sum
                    ans += -sum + 1;
                    sum = 1;
                }
            }
            else {

                // Check if prefix sum is
                // not negative
                if (sum >= 0) {
                    // Update the value of
                    // ans and sum
                    ans += sum + 1;
                    sum = -1;
                }
            }
        }

        // Update the value of res
        res = min(res, ans);
    }

    // Print the value of res
    cout << res;
}

// Driver Code
int main()
{
    vector<int> a{ 1, -3, 1, 0 };

    minOperations(a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find minimum operations
// needed to make the product of any
// two adjacent elements in prefix
// sum array negative
static void minOperations(ArrayList<Integer> a)
{

    // Stores the minimum operations
    int res = Integer.MAX_VALUE;
    int N = a.size();

    for(int r = 0; r < 2; r++)
    {

        // Stores the prefix sum
        // and number of operations
        int sum = 0, ans = 0;

        // Traverse the array
        for(int i = 0; i < N; i++)
        {

            // Update the value of sum
            sum += a.get(i);

            // Check if i+r is odd
            if ((i + r) % 2 == 1)
            {

                // Check if prefix sum
                // is not positive
                if (sum <= 0)
                {

                    // Update the value of
                    // ans and sum
                    ans += -sum + 1;
                    sum = 1;
                }
            }
            else
            {

                // Check if prefix sum is
                // not negative
                if (sum >= 0)
                {

                    // Update the value of
                    // ans and sum
                    ans += sum + 1;
                    sum = -1;
                }
            }
        }

        // Update the value of res
        res = Math.min(res, ans);
    }

    // Print the value of res
    System.out.print(res);
}

// Driver Code
public static void main(String args[])
{
    ArrayList<Integer> a = new ArrayList<Integer>();
    a.add(1);
    a.add(-3);
    a.add(1);
    a.add(0);

    minOperations(a);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# python code for the above approach
# // Function to find minimum operations
# // needed to make the product of any
# // two adjacent elements in prefix
# // sum array negative
def minOperations(a):

    #Stores the minimum operations
    res = 100000000000
    N = len(a)
    for r in range(0,2):

        # Stores the prefix sum
        # and number of operations
        sum = 0
        ans = 0

        # Traverse the array
        for i in range (0,N):

            # Update the value of sum
            sum += a[i]

            # Check if i+r is odd
            if ((i + r) % 2):

                # Check if prefix sum
                # is not positive
                if (sum <= 0):

                    # Update the value of
                    # ans and sum
                    ans += -sum + 1
                    sum = 1
            else:

                 # Check if prefix sum is
                # not negative
                if (sum >= 0):

                    # Update the value of
                    # ans and sum
                    ans += sum + 1;
                    sum = -1;

        # Update the value of res
        res = min(res, ans)

    # // Print the value of res
    print(res)

    # Driver code
a = [1, -3, 1, 0]
minOperations(a);

# This code is contributed by Stream_Cipher
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find minimum operations
// needed to make the product of any
// two adjacent elements in prefix
// sum array negative
static void minOperations(List<int> a)
{

    // Stores the minimum operations
    int res = Int32.MaxValue;
    int N = a.Count;

    for (int r = 0; r < 2; r++)
    {

        // Stores the prefix sum
        // and number of operations
        int sum = 0, ans = 0;

        // Traverse the array
        for (int i = 0; i < N; i++)
        {

            // Update the value of sum
            sum += a[i];

            // Check if i+r is odd
            if ((i + r) % 2 == 1) {

                // Check if prefix sum
                // is not positive
                if (sum <= 0) {

                    // Update the value of
                    // ans and sum
                    ans += -sum + 1;
                    sum = 1;
                }
            }
            else {

                // Check if prefix sum is
                // not negative
                if (sum >= 0) {
                    // Update the value of
                    // ans and sum
                    ans += sum + 1;
                    sum = -1;
                }
            }
        }

        // Update the value of res
        res = Math.Min(res, ans);
    }

    // Print the value of res
    Console.Write(res);
}

// Driver Code
public static void Main()
{
    List<int> a = new List<int>(){ 1, -3, 1, 0 };

    minOperations(a);
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find minimum operations
// needed to make the product of any
// two adjacent elements in prefix
// sum array negative
function minOperations(a)
{
    // Stores the minimum operations
   let res =Number.MAX_VALUE;
   let N = a.length;

    for (let r = 0; r < 2; r++) {
        // Stores the prefix sum
        // and number of operations
       let sum = 0, ans = 0;

        // Traverse the array
        for (let i = 0; i < N; i++) {
            // Update the value of sum
            sum += a[i];
            // Check if i+r is odd
            if ((i + r) % 2) {

                // Check if prefix sum
                // is not positive
                if (sum <= 0) {

                    // Update the value of
                    // ans and sum
                    ans += -sum + 1;
                    sum = 1;
                }
            }
            else {

                // Check if prefix sum is
                // not negative
                if (sum >= 0) {
                    // Update the value of
                    // ans and sum
                    ans += sum + 1;
                    sum = -1;
                }
            }
        }

        // Update the value of res
        res = Math.min(res, ans);
    }

    // Print the value of res
    document.write(res);
}

// Driver Code

    let a = [1, -3, 1, 0 ];

    minOperations(a);

  // This code is contributed by Potta Lokesh

</script>
```

**Output**

```
4
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)