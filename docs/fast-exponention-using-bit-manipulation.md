# 使用位操作的快速指数运算

> 原文:[https://www . geeksforgeeks . org/fast-indexing-使用位操作/](https://www.geeksforgeeks.org/fast-exponention-using-bit-manipulation/)

给定两个整数 **A** 和 **N** ，任务是计算 **A** 升到幂 **N** (即 **A <sup>N</sup>** )。

**示例:**

> **输入:** A = 3，N = 5
> **输出:** 243
> **说明:**
> 3 升幂 5 = (3*3*3*3*3) = 243
> 
> **输入:** A = 21，N = 4
> **输出:** 194481
> **说明:**
> 21 升幂 4 = (21*21*21*21) = 194481

**天真的做法:**
解决这个问题最简单的做法就是将 **A** 、 **N** 次重复相乘，打印产品。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**
要优化上述方法，思路是使用[位操纵](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)。将整数 **N** 转换为二进制形式，并按照以下步骤操作:

*   初始化**和**存储 A <sup>N</sup> 的最终答案。
*   遍历直到 **N > 0** ，在每次迭代中，对其执行[右移](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)操作。
*   另外，在每次迭代中，将 **A** 与自身相乘并更新。
*   如果设置了电流 [LSB](https://www.geeksforgeeks.org/print-kth-least-significant-bit-number/) ，则将 **A** 的电流值乘以 **ans** 。
*   最后，完成以上步骤后，打印 **ans** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to return a^n
int powerOptimised(int a, int n)
{

    // Stores final answer
    int ans = 1;

    while (n > 0) {

        int last_bit = (n & 1);

        // Check if current LSB
        // is set
        if (last_bit) {
            ans = ans * a;
        }

        a = a * a;

        // Right shift
        n = n >> 1;
    }

    return ans;
}

// Driver Code
int main()
{
    int a = 3, n = 5;

    cout << powerOptimised(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to return a^n
static int powerOptimised(int a, int n)
{

    // Stores final answer
    int ans = 1;

    while (n > 0)
    {
        int last_bit = (n & 1);

        // Check if current LSB
        // is set
        if (last_bit > 0)
        {
            ans = ans * a;
        }

        a = a * a;

        // Right shift
        n = n >> 1;
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int a = 3, n = 5;

    System.out.print(powerOptimised(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return a^n
def powerOptimised(a, n):

    # Stores final answer
    ans = 1

    while (n > 0):
        last_bit = (n & 1)

        # Check if current LSB
        # is set
        if (last_bit):
            ans = ans * a
        a = a * a

        # Right shift
        n = n >> 1

    return ans

# Driver code
if __name__ == '__main__':

    a = 3
    n = 5

    print(powerOptimised(a,n))

# This code is contributed by virusbuddah_
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return a^n
static int powerOptimised(int a, int n)
{

    // Stores readonly answer
    int ans = 1;

    while (n > 0)
    {
        int last_bit = (n & 1);

        // Check if current LSB
        // is set
        if (last_bit > 0)
        {
            ans = ans * a;
        }
        a = a * a;

        // Right shift
        n = n >> 1;
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int a = 3, n = 5;

    Console.Write(powerOptimised(a, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to return a^n
function powerOptimised(a, n)
{

    // Stores final answer
    let ans = 1;

    while (n > 0)
    {
        let last_bit = (n & 1);

        // Check if current LSB
        // is set
        if (last_bit > 0)
        {
            ans = ans * a;
        }

        a = a * a;

        // Right shift
        n = n >> 1;
    }
    return ans;
} 

    // Driver Code

    let a = 3, n = 5;

    document.write(powerOptimised(a, n));

</script>
```

**Output:** 

```
243
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*