# 最大化 N 笔交易可能产生的不同利润的数量

> 原文:[https://www . geeksforgeeks . org/最大化 n 交易可能获得的独特利润数/](https://www.geeksforgeeks.org/maximize-count-of-distinct-profits-possible-by-n-transactions/)

给定三个整数 **N、X、**和 **Y** ，分别代表交易总数、最小和最大利润，任务是使用 **X** 和 **Y** 至少找到一次在 **N** ( *N > 1* 交易中可以赚取的不同总利润的计数。

**示例:**

> **输入:** N = 3，X = 13，Y = 15
> **输出:** 3
> **说明:**
> 满足条件的不同可能交易如下:
> 
> *   在前两次交易中，获得的利润是 13。在最后一笔交易中，赚取的利润是 15。所以，赚到的利润总额= 13 + 13 + 15 = 41。
> *   在前两笔交易中，获得的利润分别为 13 英镑和 14 英镑。在最后一笔交易中，赚取的利润是 15。因此，获得的总利润= 13 + 14 + 15 = 42。
> *   在第一笔交易中，赚取的利润是 13。在最后两笔交易中，赚取的利润是 15。所以利润总额= 13 + 15 + 15 = 43。
> 
> 因此，总的独特利润是 3。
> 
> **输入:** N = 2，X = 10，Y = 17
> T3】输出: 1

**方法:**给定的问题可以基于以下观察来解决:

> *   The minimum total profit that can be earned is:
>     *   **S1 =(N-1)* X+Y .**
> *   The maximum total profit that can be earned is:
>     *   **S2 =(N-1)* Y+X .**
> *   It can now be observed that all the total profits will be within the range of **[S1, S2].**

按照以下步骤解决问题:

*   打印数值 **(S2-S1+1)。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count distinct
// profits possible
int numberOfWays(int N, int X, int Y)
{
    // Stores the minimum total profit
    int S1 = (N - 1) * X + Y;

    // Stores the maximum total profit
    int S2 = (N - 1) * Y + X;

    // Return count of distinct profits
    return (S2 - S1 + 1);
}

// Driver code
int main()
{
    // Input
    int N = 3;
    int X = 13;
    int Y = 15;

    // Function call
    cout << numberOfWays(N, X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.Arrays;

class GFG
{

// Function to count distinct
// profits possible
static int numberOfWays(int N, int X, int Y)
{
    // Stores the minimum total profit
    int S1 = (N - 1) * X + Y;

    // Stores the maximum total profit
    int S2 = (N - 1) * Y + X;

    // Return count of distinct profits
    return (S2 - S1 + 1);
}

// Driver code
public static void main(String[] args)
{
    // Input
    int N = 3;
    int X = 13;
    int Y = 15;

    // Function call
    System.out.println(numberOfWays(N, X, Y));
    }
}

// This code is contributed by jana_sayantan.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count distinct
# profits possible
def numberOfWays(N, X, Y):

    # Stores the minimum total profit
    S1 = (N - 1) * X + Y

    # Stores the maximum total profit
    S2 = (N - 1) * Y + X

    # Return count of distinct profits
    return (S2 - S1 + 1)

# Driver code
if __name__ == '__main__':

    # Input
    N = 3
    X = 13
    Y = 15

    # Function call
    print(numberOfWays(N, X, Y))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to count distinct
// profits possible
static int numberOfWays(int N, int X, int Y)
{
    // Stores the minimum total profit
    int S1 = (N - 1) * X + Y;

    // Stores the maximum total profit
    int S2 = (N - 1) * Y + X;

    // Return count of distinct profits
    return (S2 - S1 + 1);
}

// Driver Code
public static void Main()
{
    // Input
    int N = 3;
    int X = 13;
    int Y = 15;

    // Function call
    Console.WriteLine(numberOfWays(N, X, Y));

}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count distinct
// profits possible
function numberOfWays( N, X, Y)
{
    // Stores the minimum total profit
    let S1 = (N - 1) * X + Y;

    // Stores the maximum total profit
    let S2 = (N - 1) * Y + X;

    // Return count of distinct profits
    return (S2 - S1 + 1);
}

// Driver code
    // Input
    let N = 3;
    let X = 13;
    let Y = 15;

    // Function call
    document.write(numberOfWays(N, X, Y));

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)