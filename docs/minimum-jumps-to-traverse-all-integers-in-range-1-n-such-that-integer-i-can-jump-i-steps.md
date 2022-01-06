# 遍历[1，N]范围内所有整数的最小跳数，这样整数 I 可以跳 I 步

> 原文:[https://www . geesforgeks . org/最小跳转遍历范围内的所有整数-1-n-这样整数-I-可以跳转-i-steps/](https://www.geeksforgeeks.org/minimum-jumps-to-traverse-all-integers-in-range-1-n-such-that-integer-i-can-jump-i-steps/)

给定一个整数 **N，**任务是通过选择任意整数找到访问范围**【1，N】**中所有整数的最小步数，并在每次 **i <sup>th</sup>** 跳转时跳转 **i** 步数。

注意:可以多次重新访问一个整数。

**示例:**

> **输入:** N = 6
> **输出:** 3
> **解释:**
> 以下方式之一是:
> 先从第一个数字开始，访问整数{1，2，4}。
> 现在从第二个数字开始，访问整数{2，3，5}
> 现在从最后一个数字开始，访问它。
> 因此，在总共 3 个步骤中，可以访问范围[1，6]中的所有数字。这也是所需的最小步骤数。
> 
> **输入:**N = 4
> T3】输出: 2

**天真方法:**给定的问题可以基于以下观察来解决:

> *   The size of the jump increases in each step, so some numbers remain invisible in one step.
> *   Starting from the first digit and performing the jump, it can be observed that **The maximum size of the jump** is the total number of steps required to access each digit. Just like in a move, people can't access every number between two unaccessed numbers.

按照以下步骤解决问题:

*   初始化两个变量，比如**计数= 1** 和 **res = 0。**
*   遍历范围**【1，N】**，通过**计数**增加 **i** ，将 **res** 更新为**res =最大(RES，计数)**，通过 **1** 增加**计数**。
*   完成上述步骤后，打印**RES**

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to find minimum steps
int minSteps(int N)
{
    // Initialize count and result
    int count = 1, res = 0;

    // Traverse over the range [1, N]
    for (int i = 1; i <= N; i += count) {
        // Update res
        res = max(res, count);
        // Increment count
        count++;
    }

    // Return res
    return res;
}

// Driver Code
int main()
{
    // Input
    int N = 6;

    // Function call
    cout << minSteps(N) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Utility function to find minimum steps
  static int minSteps(int N)
  {

    // Initialize count and result
    int count = 1, res = 0;

    // Traverse over the range [1, N]
    for (int i = 1; i <= N; i += count)
    {

      // Update res
      res = Math.max(res, count);

      // Increment count
      count++;
    }

    // Return res
    return res;
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Input
    int N = 6;

    // Function call

    System.out.println(minSteps(N) );
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Utility function to find minimum steps
def minSteps(N):

    # Initialize count and result
    count = 1
    res = 0

    # Traverse over the range [1, N]
    for i in range(1, N + 1, count):

        # Update res
        res = max(res, count)

        # Increment count
        count += 1

    # Return res
    return res

# Driver Code
if __name__ == '__main__':

    # Input
    N = 6

    # Function call
    print(minSteps(N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Utility function to find minimum steps
  static int minSteps(int N)
  {

    // Initialize count and result
    int count = 1, res = 0;

    // Traverse over the range [1, N]
    for (int i = 1; i <= N; i += count)
    {

      // Update res
      res = Math.Max(res, count);

      // Increment count
      count++;
    }

    // Return res
    return res;
  }

// Driver Code
public static void Main()
{
    // Input
    int N = 6;

    // Function call

    Console.Write(minSteps(N) );
}
}
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Utility function to find minimum steps
function minSteps(N) {
  // Initialize count and result
  let count = 1,
    res = 0;

  // Traverse over the range [1, N]
  for (let i = 1; i <= N; i += count) {
    // Update res
    res = Math.max(res, count);
    // Increment count
    count++;
  }

  // Return res
  return res;
}

// Driver Code

// Input
let N = 6;

// Function call
document.write(minSteps(N));

</script>
```

**Output**

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)

**高效方法:** [](https://www.geeksforgeeks.org/greedy-algorithms/)上述步骤可以根据以下观察进行优化:

> *   Suppose an array arr[] is **arr [] = {1,1,2,2,3,3,3, ...** The idea now is to find the number **k** , which is the maximum size of one step.
> *   In the above array, self, 1 appears twice, 2 appears three times, 3 appears four times and so on. ([T0】 K-1) 【T1) will appear **k** times.
> *   Now let **k** occur **c** times, then the total number of occurrences must be equal to **n.**
>     *   **2+3+4+…，+K+c = N**
>     *   **c = N–2–3–4-…K…..(一)**
> *   Then we need to find the maximum **k** and **c ≥ 1** which satisfy the equation (I), and then
>     *   t38]k<sup>2</sup>+k–2×n≤0。
> *   阿九**k =(-1+√1+8×n)]/2**

按照以下步骤解决问题:

*   打印数值 **(-1 + √(1 + 8 *N)) / 2** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to find minimum steps
int minSteps(int N)
{
    int res = (sqrt(1 + 8 * N) - 1) / 2;
    return res;
}

// Driver code
int main()
{
    // Input integer
    int N = 6;

    // Function call
    cout << minSteps(N) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.lang.Math;

class GFG{

// Utility function to find minimum steps
static int minSteps(int N)
{
    int res = ((int)Math.sqrt(1 + 8 * N) - 1) / 2;
    return res;
}

// Driver code
public static void main (String[] args)
{

    // Input integer
    int N = 6;

    // Function call
    System.out.println(minSteps(N) + "\n");
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

from math import sqrt
# Utility function to find minimum steps
def minSteps(N):
    res = int((sqrt(1 + 8 * N) - 1) // 2)
    return res

# Driver code
if __name__ == '__main__':
    # Input integer
    N = 6

    # Function call
    print(minSteps(N))
```

## C#

```
// Java implementation of the above approach
using System;
class GFG
{

// Utility function to find minimum steps
static int minSteps(int N)
{
    int res = ((int)Math.Sqrt(1 + 8 * N) - 1) / 2;
    return res;
}

// Driver code
public static void Main (String[] args)
{

    // Input integer
    int N = 6;

    // Function call
    Console.Write(minSteps(N) + "\n");
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

// Utility function to find minimum steps
function minSteps(N)
{
    var res = parseInt((Math.sqrt(1 + 8 * N) - 1) / 2);
    return res;
}

// Driver code

// Input integer
var N = 6;

// Function call
document.write(minSteps(N));

// This code contributed by shikhasingrajput
</script>
```

**Output**

```
3
```

**时间复杂度:***O*(1)
T5】辅助空间: O(1)