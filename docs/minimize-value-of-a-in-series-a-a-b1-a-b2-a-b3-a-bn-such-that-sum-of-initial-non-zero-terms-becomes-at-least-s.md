# 最小化系列 a、a/b^1、a/b^2、a/b^3、…、a/b^n 中 a 的值，使得初始非零项的总和至少为 S

> 原文:[https://www . geesforgeks . org/minimum-value-in-series-a-B1-a-B2-a-B3-a-bn-这样初始非零项之和至少变成-s/](https://www.geeksforgeeks.org/minimize-value-of-a-in-series-a-a-b1-a-b2-a-b3-a-bn-such-that-sum-of-initial-non-zero-terms-becomes-at-least-s/)

给定两个整数 **b** 和 **S** 。任务是找到“ **a** 的最小值，使得初始非零项的**和**等于或大于“ **S** ”。

> a、a/b <sup>1</sup> 、a/b <sup>2</sup> 、a/b <sup>3</sup> 、…………。，a/b <sup>n</sup>

**示例:**

> **输入:** b = 2，S = 4
> T3】输出:3
> T6】说明:
> 
> *   设 a = 1，S = 1/2<sup>0</sup>+1/2<sup>1</sup>= 1+0 = 1<4。
> *   设 a =2，S = 2/2<sup>0</sup>+2/2<sup>1</sup>+2/2<sup>2</sup>= 2+1+0 = 3<4。
> *   设 a = 3，S = 3/2<sup>0</sup>+3/2<sup>1</sup>+3/2<sup>2</sup>= 3+1+0 = 4 = S
> 
> 所以，a = 3 就是答案。
> 
> **输入:** b = 8，S = 25
> T3】输出: 23

**方法:**这个问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到答案来解决。显然，如果数字“ **a** 是一个答案，那么每个数字 **n > a** 也是一个答案，因为数值只会变得更多，但我们需要找到最小的**1。所以，要查一些数字**‘a’**我们可以用题本身给出的公式。按照以下步骤解决问题:**

*   将变量 **a** 初始化为 **1，低**初始化为 **0** ，高**初始化为**s****
*   [循环遍历](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到**低**小于等于**高**并执行以下任务:
    *   将变量**中间**初始化为**低**和**高的平均值。**
    *   将 **x** 初始化为 **b** ，将**求和**为**中间。**
    *   [循环遍历](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到**中/x** 大于 **0** ，执行以下任务:
        *   将**中间/x** 的值加到变量**和**上。
        *   将数值 **b** 乘以变量**x**
    *   如果**之和**大于等于 **S** ，则将 **a** 设置为**中**，将**高**设置为**中 1。**
    *   否则将**低电平**设为**中间+1。**
*   执行上述步骤后，打印 **a** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum value
// of numerator such that sum of certain
// terms in the given series become
// equal or greater than X
int findMinNumerator(int b, int S)
{

    // Variable to store the ans
    // initialized with 1 which
    // can be the minimum answer
    int a = 1;
    int low = 0, high = S;

    // Iterate till low is less or
    // equal to high
    while (low <= high) {

        // Find the mid value
        int mid = (low + high) / 2;
        int x = b, sum = mid;

        // While mid / x is greater than
        // 0 keep updating sum and x
        while (mid / x > 0) {
            sum += mid / x;
            x *= b;
        }

        // If sum is greater than S,
        // store mid in ans and update
        // high to search other minimum
        if (sum >= S) {
            a = mid;
            high = mid - 1;
        }

        // Else update low as (mid + 1)
        else if (sum < S) {
            low = mid + 1;
        }
    }

    // Return the answer
    return a;
}

// Driver Code
int main()
{
    int b = 2, S = 4;

    cout << findMinNumerator(b, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG
{
// Function to find the minimum value
// of numerator such that sum of certain
// terms in the given series become
// equal or greater than X
static int findMinNumerator(int b, int S)
{

    // Variable to store the ans
    // initialized with 1 which
    // can be the minimum answer
    int a = 1;
    int low = 0, high = S;

    // Iterate till low is less or
    // equal to high
    while (low <= high) {

        // Find the mid value
        int mid = (low + high) / 2;
        int x = b, sum = mid;

        // While mid / x is greater than
        // 0 keep updating sum and x
        while (mid / x > 0) {
            sum += mid / x;
            x *= b;
        }

        // If sum is greater than S,
        // store mid in ans and update
        // high to search other minimum
        if (sum >= S) {
            a = mid;
            high = mid - 1;
        }

        // Else update low as (mid + 1)
        else if (sum < S) {
            low = mid + 1;
        }
    }

    // Return the answer
    return a;
}

// Driver Code
public static void main(String args[])
{
    int b = 2, S = 4;
    System.out.println(findMinNumerator(b, S));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum value
# of numerator such that sum of certain
# terms in the given series become
# equal or greater than X
def findMinNumerator(b, S):

    # Variable to store the ans
    # initialized with 1 which
    # can be the minimum answer
    a = 1
    low = 0
    high = S

    # Iterate till low is less or
    # equal to high
    while (low <= high):

        # Find the mid value
        mid = (low + high) // 2
        x = b
        sum = mid

        # While mid / x is greater than
        # 0 keep updating sum and x
        while (mid // x > 0):
            sum += mid // x
            x *= b

        # If sum is greater than S,
        # store mid in ans and update
        # high to search other minimum
        if (sum >= S):
            a = mid
            high = mid - 1

        # Else update low as (mid + 1)
        elif (sum < S):
            low = mid + 1

    # Return the answer
    return a

# Driver Code
if __name__ == "__main__":

    b = 2
    S = 4

    print(findMinNumerator(b, S))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

public class GFG
{
// Function to find the minimum value
// of numerator such that sum of certain
// terms in the given series become
// equal or greater than X
static int findMinNumerator(int b, int S)
{

    // Variable to store the ans
    // initialized with 1 which
    // can be the minimum answer
    int a = 1;
    int low = 0, high = S;

    // Iterate till low is less or
    // equal to high
    while (low <= high) {

        // Find the mid value
        int mid = (low + high) / 2;
        int x = b, sum = mid;

        // While mid / x is greater than
        // 0 keep updating sum and x
        while (mid / x > 0) {
            sum += mid / x;
            x *= b;
        }

        // If sum is greater than S,
        // store mid in ans and update
        // high to search other minimum
        if (sum >= S) {
            a = mid;
            high = mid - 1;
        }

        // Else update low as (mid + 1)
        else if (sum < S) {
            low = mid + 1;
        }
    }

    // Return the answer
    return a;
}

// Driver Code
public static void Main()
{
    int b = 2, S = 4;
    Console.Write(findMinNumerator(b, S));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum value
        // of numerator such that sum of certain
        // terms in the given series become
        // equal or greater than X
        function findMinNumerator(b, S) {

            // Variable to store the ans
            // initialized with 1 which
            // can be the minimum answer
            let a = 1;
            let low = 0, high = S;

            // Iterate till low is less or
            // equal to high
            while (low <= high) {

                // Find the mid value
                let mid = Math.floor((low + high) / 2);
                let x = b, sum = mid;

                // While mid / x is greater than
                // 0 keep updating sum and x
                while (Math.floor(mid / x) > 0) {
                    sum += mid / x;
                    x *= b;
                }

                // If sum is greater than S,
                // store mid in ans and update
                // high to search other minimum
                if (sum >= S) {
                    a = mid;
                    high = mid - 1;
                }

                // Else update low as (mid + 1)
                else if (sum < S) {
                    low = mid + 1;
                }
            }

            // Return the answer
            return a;
        }

        // Driver Code
        let b = 2, S = 4;
        document.write(findMinNumerator(b, S));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
3
```

***时间复杂度:**O(log<sup>2</sup>N)*
*T8】辅助空间: O(1)*