# 将 X 转换为 Y 的最大质数

> 原文:[https://www . geesforgeks . org/maximum-prime-moves-convert-x-to-y/](https://www.geeksforgeeks.org/maximum-prime-moves-to-convert-x-to-y/)

给定两个整数 **X** 和 **Y** ，任务是使用以下操作将 **X** 转换为 **Y 【T7:】**

1.  将任意质数加到 **X** 上。
2.  从 **Y** 中减去任意质数。

如果无法将 **X** 转换为 **Y** ，则打印 **-1** 所需的最大操作次数。
**举例:**

> **输入:** X = 2，Y = 4
> **输出:** 1
> 2 - > 4
> **输入:** X = 5，Y = 6
> **输出:** -1
> 给定操作不可能将 5 转换为 6
> 。

**进场:**由于任务是最大化作业，所以每次作业都必须给 **X** 加上最小可能值。由于该值必须是质数，因此可以使用最少的两个质数，即 **2** 和 **3** ，因为它们都是质数，并且可以覆盖偶数和奇数奇偶校验。现在有三种情况:

*   如果 **X > Y** 那么答案将是 **-1** ，因为给定的操作无法使 **X** 等于 **Y** 。
*   如果 **X = Y** 那么答案就是 **0** 。
*   如果 **X < Y** 那么计算**P = Y–X**并且，
    *   如果 **P = 1** ，则答案为 **-1** ，因为 **1** 不是素数，不能加减。
    *   如果 **P** 是偶数，那么 **2** 可以重复加到 X，答案就是 **P / 2**
    *   如果 **P** 为偶数，那么将 **3** 加到 **X** 上，然后将 **2** 再次重复加到新的 **X** 上，使其等于 **Y** ，在这种情况下，结果将是**1+((P–3)/2)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum operations
// required to convert X to Y
int maxOperations(int X, int Y)
{

    // X cannot be converted to Y
    if (X > Y)
        return -1;

    int diff = Y - X;

    // If the difference is 1
    if (diff == 1)
        return -1;

    // If the difference is even
    if (diff % 2 == 0)
        return (diff / 2);

    // Add 3 to X and the new
    // difference will be even
    return (1 + ((diff - 3) / 2));
}

// Driver code
int main()
{
    int X = 5, Y = 16;

    cout << maxOperations(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum operations
// required to convert X to Y
static int maxOperations(int X, int Y)
{

    // X cannot be converted to Y
    if (X > Y)
        return -1;

    int diff = Y - X;

    // If the difference is 1
    if (diff == 1)
        return -1;

    // If the difference is even
    if (diff % 2 == 0)
        return (diff / 2);

    // Add 3 to X and the new
    // difference will be even
    return (1 + ((diff - 3) / 2));
}

// Driver code
public static void main(String []args)
{
    int X = 5, Y = 16;

    System.out.println(maxOperations(X, Y));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum operations
# required to convert X to Y
def maxOperations(X, Y) :

    # X cannot be converted to Y
    if (X > Y) :
        return -1;

    diff = Y - X;

    # If the difference is 1
    if (diff == 1) :
        return -1;

    # If the difference is even
    if (diff % 2 == 0) :
        return (diff // 2);

    # Add 3 to X and the new
    # difference will be even
    return (1 + ((diff - 3) // 2));

# Driver code
if __name__ == "__main__" :

    X = 5; Y = 16;

    print(maxOperations(X, Y));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;                   

class GFG
{

// Function to return the maximum operations
// required to convert X to Y
static int maxOperations(int X, int Y)
{

    // X cannot be converted to Y
    if (X > Y)
        return -1;

    int diff = Y - X;

    // If the difference is 1
    if (diff == 1)
        return -1;

    // If the difference is even
    if (diff % 2 == 0)
        return (diff / 2);

    // Add 3 to X and the new
    // difference will be even
    return (1 + ((diff - 3) / 2));
}

// Driver code
public static void Main(String []args)
{
    int X = 5, Y = 16;

    Console.WriteLine(maxOperations(X, Y));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum operations
// required to convert X to Y
function maxOperations(X, Y)
{

    // X cannot be converted to Y
    if (X > Y)
        return -1;

    let diff = Y - X;

    // If the difference is 1
    if (diff == 1)
        return -1;

    // If the difference is even
    if (diff % 2 == 0)
        return (diff / 2);

    // Add 3 to X and the new
    // difference will be even
    return (1 + ((diff - 3) / 2));
}

// Driver code

    let X = 5, Y = 16;

    document.write(maxOperations(X, Y));

// This code is contributed by _saurabh_jaiswal   

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(1)