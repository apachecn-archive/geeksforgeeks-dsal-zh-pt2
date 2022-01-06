# 从给定点到达原点所需的最小步数

> 原文:[https://www . geesforgeks . org/从给定点到达原点所需的最小步数/](https://www.geeksforgeeks.org/minimum-number-of-steps-required-to-reach-origin-from-a-given-point/)

给定两个整数 **A** 和 **B** 表示第一象限中一点的坐标，任务是找到到达原点所需的最小步数。从点 **(i，j)** 开始的所有可能的移动是**(I–1，j)，(I，j–1)**或 **(i，j)** ( *停留在相同位置*)。
***注意:**不允许连续两次同向移动。*

**示例:**

> **输入:** A = 4，B = 0
> **输出:** 7
> **说明:**
> 下面是从给定点到原点的运动:
> (4，0) → (3，0) → (3，0)(停留)→ (2，0) → (2，0)(停留)→ (1，0) → (1，0)(停留)→ (0，0)。
> 因此，到达原点需要 7 步。
> 
> **输入:** A = 3，B = 5
> **输出:** 9
> **说明:**
> 下面是从给定点到原点的运动:
> (3，5) → (3，4) → (2，4) → (2，3) → (1，3) → (1，2) → (0，2) → (0，1) → (0，1)(停留)→ (0，0)。
> 因此，到达原点需要 9 步。

**天真的方法:**最简单的方法是[递归](https://www.geeksforgeeks.org/recursion/)。这个想法是递归地考虑从每个点开始的所有可能的移动，并为每个移动计算到达原点所需的最小步数。
***时间复杂度:** O(3 <sup>max(A，B)</sup> )*
***辅助空间:** O(1)*

**高效进场:**优化上述进场，思路是基于这样的观察:如果 x、y 坐标的**绝对差为 1 或 0** ，那么到达原点所需的最小步数为 **(a + b)** 。否则需要**(2 * ABS(a–b)–1)**移动到达 **(k，k)** ，其中 **k** 是 **a，b** 的最小值。

> 因此，从 **(a，b)** 到达原点所需的最小步数等于=(从(k，k)到达(0，0)所需的步数)+从(k，k)到达(0，0)所需的步数)=(2 * ABS(a–b)–1)+(2 * k)

按照以下步骤解决问题:

*   初始化一个变量**和**，它存储从 **(a，b)** 到达原点所需的最小步数。
*   如果 **a** 和 **b** 的绝对差值为 **1** 或 **0** ，则更新 **ans** 为 **(a + b)** 。
*   否则:
    *   求 **a，b** 的最小值，存储在变量 **k** 中。
    *   使用公式，更新**ans =(2 * ABS(a–b)–1)+(2 * k)**。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum moves
// required to reach origin from (a, b)
void findMinMoves(int a, int b)
{
    // Stores the minimum number of moves
    int ans = 0;

    // Check if the absolute
    // difference is 1 or 0
    if (a == b || abs(a - b) == 1) {
        ans = a + b;
    }

    else {

        // Store the minimum of a, b
        int k = min(a, b);

        // Store the maximum of a, b
        int j = max(a, b);

        ans = 2 * k + 2 * (j - k) - 1;
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given co-ordinates
    int a = 3, b = 5;

    // Function Call
    findMinMoves(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to find the minimum moves
  // required to reach origin from (a, b)
  static void findMinMoves(int a, int b)
  {

    // Stores the minimum number of moves
    int ans = 0;

    // Check if the absolute
    // difference is 1 or 0
    if (a == b || Math.abs(a - b) == 1)
    {
      ans = a + b;
    }

    else
    {

      // Store the minimum of a, b
      int k = Math.min(a, b);

      // Store the maximum of a, b
      int j = Math.max(a, b);
      ans = 2 * k + 2 * (j - k) - 1;
    }

    // Print the answer
    System.out.print(ans);
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given co-ordinates
    int a = 3, b = 5;

    // Function Call
    findMinMoves(a, b);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# function to find the minimum moves
# required to reach origin from (a, b)
def findMinMoves(a, b):

    # Stores the minimum number of moves
    ans = 0

    # Check if the absolute
    # difference is 1 or 0
    if (a == b or abs(a - b) == 1):
        ans = a + b
    else:
        # Store the minimum of a, b
        k = min(a, b)

        # Store the maximum of a, b
        j = max(a, b)
        ans = 2 * k + 2 * (j - k) - 1

    # Prthe answer
    print (ans)

# Driver Code
if __name__ == '__main__':

    # Given co-ordinates
    a,b = 3, 5

    # Function Call
    findMinMoves(a, b)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the minimum moves
  // required to reach origin from (a, b)
  static void findMinMoves(int a, int b)
  {

    // Stores the minimum number of moves
    int ans = 0;

    // Check if the absolute
    // difference is 1 or 0
    if (a == b || Math.Abs(a - b) == 1)
    {
      ans = a + b;
    }

    else
    {

      // Store the minimum of a, b
      int k = Math.Min(a, b);

      // Store the maximum of a, b
      int j = Math.Max(a, b);
      ans = 2 * k + 2 * (j - k) - 1;
    }

    // Print the answer
    Console.Write(ans);
  }

  // Driver Code
  public static void Main()
  {
    // Given co-ordinates
    int a = 3, b = 5;

    // Function Call
    findMinMoves(a, b);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to find the minimum moves
// required to reach origin from (a, b)
function findMinMoves(a, b)
{
    // Stores the minimum number of moves
    let ans = 0;

    // Check if the absolute
    // difference is 1 or 0
    if (a == b || Math.abs(a - b) == 1) {
        ans = a + b;
    }

    else {

        // Store the minimum of a, b
        let k = Math.min(a, b);

        // Store the maximum of a, b
        let j = Math.max(a, b);

        ans = 2 * k + 2 * (j - k) - 1;
    }

    // Print the answer
    document.write(ans);
}

// Driver Code

    // Given co-ordinates
    let a = 3, b = 5;

    // Function Call
    findMinMoves(a, b);

</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)