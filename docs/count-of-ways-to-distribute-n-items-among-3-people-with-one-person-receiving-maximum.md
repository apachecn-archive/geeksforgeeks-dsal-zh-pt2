# 3 人分配 N 个物品的方式数，最多一人领取

> 原文:[https://www . geesforgeks . org/3 人分发 n 件物品的方式计数，最多接收一人/](https://www.geeksforgeeks.org/count-of-ways-to-distribute-n-items-among-3-people-with-one-person-receiving-maximum/)

给定一个**整数 N** ，任务是找到在 **3** 人中分配 **N** 的方法总数，比如:

*   3 个人中正好有一个人获得**最大物品数**。
*   每人至少得到一件物品。

**例:**

> **输入:** N = 5
> **输出:** 3
> **说明:**
> 3 种方式将物品分发给 3 个人分别是{1，1，3}、{1，3，1}和{3，1，1}。
> 像{1，2，2}或{2，1，2}这样的分布是无效的，因为两个人获得了最大值。
> **输入:** N = 10
> **输出:** 33
> **说明:**
> 对于输入 N = 10 有 33 种分配方式。

**进场:**
要解决上面提到的问题，我们要观察到如果 **N < 4** ，那么这样的分布是不可能的。
对于 **N ≥ 4** 的所有值，按照以下步骤解决问题:

*   3 人分配 N 个项目的方式总数由**(N-1)*(N-2)/2**给出。
*   初始化一个变量 **s = 0** ，该变量存储分配不可行的方式数。
*   迭代两个嵌套循环，其中 **i** 介于**【2，N–3】**和 **j** 之间，范围直到 **i** :
    *   对于每次迭代，检查 **N 是否= 2 * i + j** ，即 2 个人可以接收最大数量的元素
    *   如果是，那么将 **s** 增加 **1** 。如果 **N** 被 **3** 整除，则更新 **s** 为 **3 * s + 1** 。否则，更新至 **3 * s** 。
*   最后，返回**ans–s**作为三人分发 **N** 物品的方式总数。

以下是上述方法的实现:

## C++

```
// C++ program to find the number
// of ways to distribute N item
// among three people such
// that one person always gets
// the maximum value

#include <bits/stdc++.h>
using namespace std;

// Function to find the number
// of ways to distribute N
// items among 3 people
int countWays(int N)
{
    // No distribution
    // possible
    if (N < 4)
        return 0;

    // Total number of ways to
    // distribute N items
    // among 3 people
    int ans = ((N - 1) * (N
                          - 2))
              / 2;

    // Store the number of
    // distributions which
    // are not possible
    int s = 0;

    for (int i = 2; i <= N - 3;
         i++) {
        for (int j = 1; j < i;
             j++) {

            // Count possibilities
            // of two persons
            // receiving the
            // maximum
            if (N == 2 * i + j)
                s++;
        }
    }

    // If N is divisible by 3
    if (N % 3 == 0)
        s = 3 * s + 1;

    else
        s = 3 * s;

    // Return the final
    // count of ways
    // to distribute
    return ans - s;
}

// Driver Code
int main()
{
    int N = 10;
    cout << countWays(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of ways to distribute N item
// among three people such
// that one person always gets
// the maximum value
class GFG{

// Function to find the number
// of ways to distribute N
// items among 3 people
static int countWays(int N)
{
    // No distribution
    // possible
    if (N < 4)
        return 0;

    // Total number of ways to
    // distribute N items
    // among 3 people
    int ans = ((N - 1) * (N - 2)) / 2;

    // Store the number of
    // distributions which
    // are not possible
    int s = 0;

    for (int i = 2; i <= N - 3; i++)
    {
        for (int j = 1; j < i; j++)
        {

            // Count possibilities
            // of two persons
            // receiving the
            // maximum
            if (N == 2 * i + j)
                s++;
        }
    }

    // If N is divisible by 3
    if (N % 3 == 0)
        s = 3 * s + 1;
    else
        s = 3 * s;

    // Return the final
    // count of ways
    // to distribute
    return ans - s;
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;
    System.out.println(countWays(N));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to find the number
# of ways to distribute N item
# among three people such
# that one person always gets
# the maximum value

# Function to find the number
# of ways to distribute N
# items among 3 people
def countWays(N):

    # No distribution
    # possible
    if (N < 4):
        return 0

    # Total number of ways to
    # distribute N items
    # among 3 people
    ans = ((N - 1) * (N - 2)) // 2

    # Store the number of
    # distributions which
    # are not possible
    s = 0

    for i in range( 2, N - 2, 1):
        for j in range( 1, i, 1):

            # Count possibilities
            # of two persons
            # receiving the
            # maximum
            if (N == 2 * i + j):
                s += 1

    # If N is divisible by 3
    if (N % 3 == 0):
        s = 3 * s + 1

    else:
        s = 3 * s

    # Return the final
    # count of ways
    # to distribute
    return ans - s

# Driver Code
N = 10

print (countWays(N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to find the number
// of ways to distribute N item
// among three people such
// that one person always gets
// the maximum value
using System;
class GFG{

// Function to find the number
// of ways to distribute N
// items among 3 people
static int countWays(int N)
{
    // No distribution
    // possible
    if (N < 4)
        return 0;

    // Total number of ways to
    // distribute N items
    // among 3 people
    int ans = ((N - 1) * (N - 2)) / 2;

    // Store the number of
    // distributions which
    // are not possible
    int s = 0;

    for (int i = 2; i <= N - 3; i++)
    {
        for (int j = 1; j < i; j++)
        {

            // Count possibilities
            // of two persons
            // receiving the
            // maximum
            if (N == 2 * i + j)
                s++;
        }
    }

    // If N is divisible by 3
    if (N % 3 == 0)
        s = 3 * s + 1;
    else
        s = 3 * s;

    // Return the final
    // count of ways
    // to distribute
    return ans - s;
}

// Driver Code
public static void Main()
{
    int N = 10;
    Console.Write(countWays(N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript program to find the number
    // of ways to distribute N item
    // among three people such
    // that one person always gets
    // the maximum value

    // Function to find the number
    // of ways to distribute N
    // items among 3 people
    function countWays(N)
    {
        // No distribution
        // possible
        if (N < 4)
            return 0;

        // Total number of ways to
        // distribute N items
        // among 3 people
        let ans = ((N - 1) * (N - 2)) / 2;

        // Store the number of
        // distributions which
        // are not possible
        let s = 0;

        for (let i = 2; i <= N - 3; i++) {
            for (let j = 1; j < i; j++) {

                // Count possibilities
                // of two persons
                // receiving the
                // maximum
                if (N == 2 * i + j)
                    s++;
            }
        }

        // If N is divisible by 3
        if (N % 3 == 0)
            s = 3 * s + 1;

        else
            s = 3 * s;

        // Return the final
        // count of ways
        // to distribute
        return ans - s;
    }

    let N = 10;
    document.write(countWays(N));

</script>
```

**Output:** 

```
33
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*