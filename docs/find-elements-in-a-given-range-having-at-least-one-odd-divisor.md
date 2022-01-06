# 找出给定范围内至少有一个奇数除数的元素

> 原文:[https://www . geesforgeks . org/find-elements-in-给定范围-至少有一个奇数除数/](https://www.geeksforgeeks.org/find-elements-in-a-given-range-having-at-least-one-odd-divisor/)

给定两个整数 **N** 和 **M** ，任务是打印范围**【N，M】**中至少有一个奇数除数的所有元素。
**举例:**

> **输入:** N = 2，M = 10
> **输出:** 3 5 6 7 9 10
> **说明:**
> 3，6 有一个奇数除数 3
> 5，10 有一个奇数除数 5
> 7 有一个奇数除数 7
> 9 有两个奇数除数 3，9
> **输入:** N = 15，M = 20
> **输出:**11

**天真法:**
最简单的方法是循环遍历**【1，N】**范围内的所有数字，对于每个元素，检查它是否有奇数除数。
***时间复杂度:**O(N<sup>3/2</sup>)*
**高效进场:**
要优化上述进场，我们需要观察以下细节:

*   [任何是 2 的幂的数](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)都没有任何奇数除数。
*   所有其他元素将至少有一个奇数除数

> **说明:**
> 在[3，10]范围内，至少有一个奇数除数的元素是{3，5，6，7，9，10}，并且{4，8}不包含任何奇数除数。

按照以下步骤解决问题:

*   遍历[N，M]范围，检查每个元素的设置位是否设置在前一个数中，即检查**I&(I–1)**是否等于 **0** 。

*   如果是，那么这个数是 2 的幂，不被考虑。否则，打印数字，因为它不是 2 的幂，并且至少有一个奇数除数。

下面是上述方法的实现。

## C++

```
// C++ program to print all numbers
// with least one odd factor in the
// given range
#include <bits/stdc++.h>
using namespace std;

// Function to prints all numbers
// with at least one odd divisor
int printOddFactorNumber(int n,
                         int m)
{
    for (int i = n; i <= m; i++) {

        // Check if the number is
        // not a power of two
        if ((i > 0)
            && ((i & (i - 1)) != 0))

            cout << i << " ";
    }
}

// Driver Code
int main()
{
    int N = 2, M = 10;
    printOddFactorNumber(N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all numbers
// with least one odd factor in the
// given range
class GFG{

// Function to prints all numbers
// with at least one odd divisor
static int printOddFactorNumber(int n,
                                int m)
{
    for (int i = n; i <= m; i++)
    {

        // Check if the number is
        // not a power of two
        if ((i > 0) && ((i & (i - 1)) != 0))

            System.out.print(i + " ");
    }
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, M = 10;
    printOddFactorNumber(N, M);
}
}

// This code is contributed
// by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to print all numbers
# with least one odd factor in the
# given range

# Function to prints all numbers
# with at least one odd divisor
def printOddFactorNumber(n, m):

    for i in range(n, m + 1):

        # Check if the number is
        # not a power of two
        if ((i > 0) and ((i & (i - 1)) != 0)):
            print(i, end = " ")

# Driver Code
N = 2
M = 10

printOddFactorNumber(N, M)

# This code is contributed by Vishal Maurya
```

## C#

```
// C# program to print all numbers
// with least one odd factor in the
// given range
using System;
class GFG{

// Function to prints all numbers
// with at least one odd divisor
static int printOddFactorNumber(int n,
                                int m)
{
    for (int i = n; i <= m; i++)
    {

        // Check if the number is
        // not a power of two
        if ((i > 0) && ((i & (i - 1)) != 0))

            Console.Write(i + " ");
    }
    return 0;
}

// Driver Code
public static void Main()
{
    int N = 2, M = 10;
    printOddFactorNumber(N, M);
}
}

// This code is contributed
// by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to prints all numbers
// with at least one odd divisor
function printOddFactorNumber(n, m)
{
    for (let i = n; i <= m; i++)
    {

        // Check if the number is
        // not a power of two
        if ((i > 0) && ((i & (i - 1)) != 0))

            document.write(i + " ");
    }
    return 0;
}

// Driver code
    let N = 2, M = 10;
    printOddFactorNumber(N, M);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
3 5 6 7 9 10
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*