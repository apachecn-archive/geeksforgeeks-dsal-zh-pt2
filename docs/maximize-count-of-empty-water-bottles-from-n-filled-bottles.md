# 从 N 个装满的瓶子中最大化空水瓶的数量

> 原文:[https://www . geeksforgeeks . org/从 n 个装满的瓶子中最大化空水瓶数量/](https://www.geeksforgeeks.org/maximize-count-of-empty-water-bottles-from-n-filled-bottles/)

给定两个整数 **N** 和 **E，**其中 **N** 代表满水瓶的数量， **E** 代表可以换满水瓶的空瓶数量。任务是找到可以倒空的水瓶的最大数量。

**示例:**

> **输入:** N = 9，E = 3
> **输出:** 13
> **说明:**
> 最初有 9 个装满水的瓶子。
> 全部清空，得到 9 个空瓶。因此，计数= **9**
> 然后一次换 3 瓶，换满一瓶。
> 因此，获得 3 个满瓶。
> 然后把那 3 瓶倒空，得到 3 个空瓶。因此，计数= **9 + 3 = 12**
> 那么这 3 瓶就换成 1 满瓶倒空。
> 因此，计数= **9 + 3 + 1** = **13** 。
> 
> **输入:** N = 7，E = 5
> **输出:** 8
> **说明:**
> 清空 7 个装满水的瓶子。因此，计数= **7**
> 然后交换 5 瓶，得到 1 满瓶。然后倒空那个瓶子。
> 因此，计数= **7 + 1** = **8** 。

**方法:**解决问题必须遵循以下步骤:

*   将 **N** 的值存储在一个临时变量中，比如 **a.**
*   初始化一个变量，说 **s，**存储空瓶数，另一个变量，说 **b，**存储交换后剩余的瓶数。
*   现在，迭代直到 **a** 不等于 **0** 并将 **s** 增加 **a** ，因为这将是已清空的最小瓶子数。
*   更新以下值:
    *   **a** 至 **(a + b) / e**
    *   **b** 至**N–(a * e)**
    *   **N** 至 **(a+b)**
*   返回 **s** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// bottles that can be emptied
int maxBottles(int n, int e)
{
    int s = 0, b = 0;
    int a = n;

    // Iterate until a
  // is non-zero
    while (a != 0) {

        // Add the number of
      // bottles that are emptied
        s = s + a;

        // Update a after
        // exchanging empty bottles
        a = (a + b) / e;

        // Stores the number of bottles
        // left after the exchange
        b = n - (a * e);
        n = a + b;
    }

    // Return the answer
    return s;
}

// Driver Code
int main()
{
    int n = 9, e = 3;

    // Function call
    int s = maxBottles(n, e);
    cout << s << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG{

// Function to find the maximum
// bottles that can be emptied
static int maxBottles(int n, int e)
{
    int s = 0, b = 0;
    int a = n;

    // Iterate until a
    // is non-zero
    while (a != 0)
    {

        // Add the number of
        // bottles that are emptied
        s = s + a;

        // Update a after
        // exchanging empty bottles
        a = (a + b) / e;

        // Stores the number of bottles
        // left after the exchange
        b = n - (a * e);
        n = a + b;
    }

    // Return the answer
    return s;
}

// Driver Code
public static void main(String[] args)
{
    int n = 9, e = 3;

    // Function call
    int s = maxBottles(n, e);

    System.out.print(s + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the maximum
# bottles that can be emptied
def maxBottles(n, e):

    s = 0
    b = 0
    a = n

    # Iterate until a
    # is non-zero
    while (a != 0):

        # Add the number of
        # bottles that are emptied
        s = s + a

        # Update a after
        # exchanging empty bottles
        a = (a + b) // e

        # Stores the number of bottles
        # left after the exchange
        b = n - (a * e)
        n = a + b

    # Return the answer
    return s

# Driver Code
if __name__ == '__main__':

    n = 9
    e = 3

    # Function call
    s = maxBottles(n, e)
    print(s)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum
// bottles that can be emptied
static int maxBottles(int n, int e)
{
    int s = 0, b = 0;
    int a = n;

    // Iterate until a
    // is non-zero
    while (a != 0)
    {

        // Add the number of
        // bottles that are emptied
        s = s + a;

        // Update a after
        // exchanging empty bottles
        a = (a + b) / e;

        // Stores the number of bottles
        // left after the exchange
        b = n - (a * e);
        n = a + b;
    }

    // Return the answer
    return s;
}

// Driver Code
public static void Main()
{
    int n = 9, e = 3;

    // Function call
    int s = maxBottles(n, e);

    Console.Write(s + "\n");
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// javascript program for the
// above approach

// Function to find the maximum
// bottles that can be emptied
function maxBottles(n, e)
{
    var s = 0, b = 0;
    var a = n;

    // Iterate until a
    // is non-zero
    while (a != 0)
    {

        // Add the number of
        // bottles that are emptied
        s = s + a;

        // Update a after
        // exchanging empty bottles
        a = (a + b) / e;

        // Stores the number of bottles
        // left after the exchange
        b = n - (a * e);
        n = a + b;
    }

    // Return the answer
    return s;
}

// Driver Code

var n = 9, e = 3;

// Function call
var s = maxBottles(n, e);

document.write(parseInt(s) + "\n");

// This code contributed by Princi Singh

</script>
```

**输出:**

```
13
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)