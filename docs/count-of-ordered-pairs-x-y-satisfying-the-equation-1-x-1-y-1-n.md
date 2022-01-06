# 满足等式 1/X + 1/Y = 1/N 的有序对(X，Y)的计数

> 原文:[https://www . geesforgeks . org/有序对计数-x-y-满足-等式-1-x-1-y-1-n/](https://www.geeksforgeeks.org/count-of-ordered-pairs-x-y-satisfying-the-equation-1-x-1-y-1-n/)

给定一个正整数 **N** ，任务是找到有序对的数量 **(X，Y)** ，其中 **X** 和 **Y** 都是正整数，使得它们满足方程 **1/X + 1/Y = 1/N** 。

**示例:**

> **输入:** N = 5
> **输出:** 3
> **说明:**只有 3 对{(30，6)，(10，10)，(6，30)}满足给定方程。
> 
> **输入:**N = 360
> T3】输出: 105

**进场:**
按照步骤解决问题:

*   用给定的方程求解 X。

> 1/X + 1/Y = 1/N
> = > 1/X = 1/N – 1/Y
> = > 1/X = （Y – N） / NY
> = > X = NY / （Y – N）
> 
> X = [ 纽约 / （Y – N） ] * （1）
> 
> => X = [纽约 / （Y – N） ] * [1 – N/Y + N/Y]
> 
> = > x =[ny/(y-n)]*[(y-n)/y+n/y]
> 
> = > X = N+N<sup>2</sup>/(Y–N)

*   因此，可以观察到，要有一个正整数 **X** ，当**N<sup>2</sup>T5】除以**(Y–N)**时的余数需要为 **0** 。**
*   可以观察到 **Y** 的最小值可以是 **N + 1** (这样分母**Y–N>0)**而 **Y** 的最大值可以是 **N <sup>2</sup> + N** 这样 N<sup>2</sup>/(Y–N)保持正整数 **≥ 1** 。
*   然后迭代 **Y** 的最大和最小可能值，对于**N<sup>2</sup>%(Y–N)= 0**的 **Y** 的每个值，递增**计数**。
*   最后，返回**计数**作为有序对的数量。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of ordered
// positive integer pairs (x,y) such
// that  they satisfy the equation
void solve(int n)
{
    // Initialize answer variable
    int ans = 0;

// Iterate over all possible values of y
    for (int y = n + 1; y <= n * n + n; y++) {

        // For valid x and y,
        // (n*n)%(y - n) has to be 0
        if ((n * n) % (y - n) == 0) {

            // Increment count of ordered pairs
            ans += 1;
        }
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int n = 5;
    // Function call
    solve(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find number of ordered
// positive integer pairs (x,y) such
// that they satisfy the equation
static void solve(int n)
{

    // Initialize answer variable
    int ans = 0;

    // Iterate over all possible values of y
    for(int y = n + 1; y <= n * n + n; y++)
    {

        // For valid x and y,
        // (n*n)%(y - n) has to be 0
        if ((n * n) % (y - n) == 0)
        {

            // Increment count of ordered pairs
            ans += 1;
        }
    }

    // Print the answer
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;

    // Function call
    solve(n);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find number of ordered
# positive integer pairs (x,y) such
# that they satisfy the equation
def solve(n):

    # Initialize answer variable
    ans = 0

    # Iterate over all possible values of y
    y = n + 1
    while(y <= n * n + n):

        # For valid x and y,
        # (n*n)%(y - n) has to be 0
        if ((n * n) % (y - n) == 0):

            # Increment count of ordered pairs
            ans += 1

        y += 1

    # Print the answer
    print(ans)

# Driver Code
n = 5

# Function call
solve(n)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find number of ordered
// positive integer pairs (x,y) such
// that they satisfy the equation
static void solve(int n)
{

    // Initialize answer variable
    int ans = 0;

    // Iterate over all possible values of y
    for(int y = n + 1; y <= n * n + n; y++)
    {

        // For valid x and y,
        // (n*n)%(y - n) has to be 0
        if ((n * n) % (y - n) == 0)
        {

            // Increment count of ordered pairs
            ans += 1;
        }
    }

    // Print the answer
    Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;

    // Function call
    solve(n);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to find number of ordered
    // positive integer pairs (x,y) such
    // that they satisfy the equation
    function solve(n) {

        // Initialize answer variable
        var ans = 0;

        // Iterate over all possible values of y
        for (y = n + 1; y <= n * n + n; y++) {

            // For valid x and y,
            // (n*n)%(y - n) has to be 0
            if ((n * n) % (y - n) == 0) {

                // Increment count of ordered pairs
                ans += 1;
            }
        }

        // Print the answer
        document.write(ans);
    }

    // Driver Code

        var n = 5;

        // Function call
        solve(n);

// This code contributed by umadevi9616
</script>
```

**输出:**

```
3
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*