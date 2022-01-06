# 找出 K 的所有可能值，使得从 K 开始的前 N 个数之和为 G

> 原文:[https://www . geeksforgeeks . org/find-k 的所有可能值-这样第一个 n 个数字的总和-从 k 开始-is-g/](https://www.geeksforgeeks.org/find-all-possible-values-of-k-such-that-the-sum-of-first-n-numbers-starting-from-k-is-g/)

给定一个正整数 **G** ，任务是求 **K** 的数值个数，使得从 **K** 开始的第一个 **N** 个数的[和为 **G** ，即**(K+(K+1)+……+(K+N–1))= G**，其中 **N** 可以是任意正整数。](https://www.geeksforgeeks.org/find-given-number-sum-first-n-natural-numbers/)

**示例:**

> **输入:** G = 10
> **输出:** 2
> **解释:**
> 以下是 K 的可能值:
> 
> 1.  **K = 1，N = 4:**{ 1，2，3，4}之和为 10(= G)。
> 2.  **K = 10，N = 1:**10 的和为 10(= G)。
> 
> 因此，有两个可能的 k 值。因此，打印 2。
> 
> **输入:**G = 15
> T3】输出: 2

**天真法:**解决给定问题最简单的方法是检查从 **1** 到 **G** 的 **K** 的每一个值，如果满足给定条件，则计算 **K** 的这个值。检查完 **K** 的所有可能值后，打印总计数。

***时间复杂度:**O(G<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过观察数学关系来解决，对于 **K** 的任何值:

> = >(K)+(K+1)+(K+2)+……+(K+N–1)= G
> =>N * K+(1+2+3+4+……+N–1)= G
> =>G = N * K+(N *(N–1))/2

因此，数值**K = G/N –( N–1)/2**。从上述关系可以得出结论， **K** 的可能值存在的条件和唯一条件是:

*   **N** 为 **G** 的因子，即 **(G % N) == 0** 。
*   **N** 应为奇数即 **(N % 2) == 1** 。

按照以下步骤解决问题:

*   初始化变量，说**计数**为 **0** ，存储 **K** 的结果计数值。
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，√G】**，并执行以下任务:
    *   如果 **g%i** 等于 **0** ，那么如果 **i** 不等于 **g/i** ，那么如果 **i%2** 等于 **1** ，那么将**的数值加上**再乘以 **1** ，如果 **(g/i)%2** 等于 **1** ，那么相加
    *   否则，如果 **i%2** 等于 **1** ，那么将**计数**的值加 **1** 。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count the value
// of K such that sum of the first N
// numbers from K is G
void findValuesOfK(int g)
{
    // Stores the total count of K
    int count = 0;

    // Iterate till square root of g
    for (int i = 1; i * i <= g; i++) {

        // If the number is factor of g
        if (g % i == 0) {

            // If the second factor is
            // not equal to first factor
            if (i != g / i) {

                // Check if two factors
                // are odd or not
                if (i & 1) {
                    count++;
                }
                if ((g / i) & 1) {
                    count++;
                }
            }

            // If second factor is the
            // same as the first factor
            // then check if the first
            // factor is odd or not
            else if (i & 1) {
                count++;
            }
        }
    }

    // Print the resultant count
    cout << count;
}

// Driver Code
int main()
{
    int G = 125;
    findValuesOfK(G);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find the count the value
    // of K such that sum of the first N
    // numbers from K is G
    static void findValuesOfK(int g)
    {

        // Stores the total count of K
        int count = 0;

        // Iterate till square root of g
        for (int i = 1; i * i <= g; i++) {

            // If the number is factor of g
            if (g % i == 0) {

                // If the second factor is
                // not equal to first factor
                if (i != g / i) {

                    // Check if two factors
                    // are odd or not
                    if (i % 2 == 1) {
                        count++;
                    }
                    if ((g / i) % 2 == 1) {
                        count++;
                    }
                }

                // If second factor is the
                // same as the first factor
                // then check if the first
                // factor is odd or not
                else if (i % 2 == 1) {
                    count++;
                }
            }
        }

        // Print the resultant count
        System.out.println(count);
    }

  // Driver code
    public static void main(String[] args)
    {
        int G = 125;
        findValuesOfK(G);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from math import sqrt

# Function to find the count the value
# of K such that sum of the first N
# numbers from K is G
def findValuesOfK(g):

    # Stores the total count of K
    count = 0

    # Iterate till square root of g
    for i in range(1,int(sqrt(g)) + 1, 1):

        # If the number is factor of g
        if (g % i == 0):

            # If the second factor is
            # not equal to first factor
            if (i != g // i):

                # Check if two factors
                # are odd or not
                if (i & 1):
                    count += 1
                if ((g // i) & 1):
                    count += 1

            # If second factor is the
            # same as the first factor
            # then check if the first
            # factor is odd or not
            elif (i & 1):
                count += 1

    # Print the resultant count
    print(count)

# Driver Code
if __name__ == '__main__':
    G = 125
    findValuesOfK(G)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the count the value
// of K such that sum of the first N
// numbers from K is G
static void findValuesOfK(int g)
{

    // Stores the total count of K
    int count = 0;

    // Iterate till square root of g
    for(int i = 1; i * i <= g; i++)
    {

        // If the number is factor of g
        if (g % i == 0)
        {

            // If the second factor is
            // not equal to first factor
            if (i != g / i)
            {

                // Check if two factors
                // are odd or not
                if (i % 2 == 1)
                {
                    count++;
                }
                if ((g / i) % 2 == 1)
                {
                    count++;
                }
            }

            // If second factor is the
            // same as the first factor
            // then check if the first
            // factor is odd or not
            else if (i % 2 == 1)
            {
                count++;
            }
        }
    }

    // Print the resultant count
    Console.WriteLine(count);
}

// Driver code
public static void Main()
{
    int G = 125;

    findValuesOfK(G);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
    // Function to find the count the value
    // of K such that sum of the first N
    // numbers from K is G
    function findValuesOfK(g)
    {

        // Stores the total count of K
        var count = 0;

        // Iterate till square root of g
        for (var i = 1; i * i <= g; i++) {

            // If the number is factor of g
            if (g % i == 0) {

                // If the second factor is
                // not equal to first factor
                if (i != g / i) {

                    // Check if two factors
                    // are odd or not
                    if (i % 2 == 1) {
                        count++;
                    }
                    if ((g / i) % 2 == 1) {
                        count++;
                    }
                }

                // If second factor is the
                // same as the first factor
                // then check if the first
                // factor is odd or not
                else if (i % 2 == 1) {
                    count++;
                }
            }
        }

        // Print the resultant count
        document.write(count);
    }

  // Driver code
        var G = 125;
        findValuesOfK(G);

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(√G)*
***辅助空间:** O(1)*