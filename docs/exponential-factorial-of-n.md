# N 的指数阶乘

> 原文:[https://www.geeksforgeeks.org/exponential-factorial-of-n/](https://www.geeksforgeeks.org/exponential-factorial-of-n/)

给定一个正整数 **N** ，任务是打印 **N** 的[指数阶乘](https://en.wikipedia.org/wiki/Exponential_factorial)。由于输出可以很大，打印答案模数 **1000000007** 。

**示例:**

> **输入:**N = 4
> T3】输出: 262144
> 
> **输入:**N = 3
> T3】输出: 9

**方法:**给定的问题可以基于以下观察来解决:

> 指数阶乘由递归关系定义:
> 
> *   ![a_n=n^{a_{n-1}}               ](img/05829e94b94bcc70e1c5105ee35ce76d.png "Rendered by QuickLaTeX.com")。

按照以下步骤解决问题:

*   初始化一个变量，比如说 **res** 为 **1** 来存储 **N** 的指数因子。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/python-program-to-print-all-positive-numbers-in-a-range/)**【2，N】**，并在每次迭代中将 **res** 更新为**RES = I<sup>RES</sup>% 1000000007。**
*   最后，完成上述步骤后，打印在 **res** 中获得的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find exponential factorial
// of a given number
int ExpoFactorial(int N)
{

    // Stores the exponential factor of N
    int res = 1;
    int mod = 1000000007;

    // Iterate over the range [2, N]
    for (int i = 2; i < N + 1; i++)

        // Update res
        res = (int)pow(i, res) % mod;

    // Return res
    return res;
}

// Driver Code
int main()
{
    // Input
    int N = 4;

    // Function call
    cout << (ExpoFactorial(N));

   // This code is contributed by Potta Lokesh
    return 0;
}

// This code is contributed by lokesh potta
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find exponential factorial
// of a given number
static int ExpoFactorial(int N)
{

    // Stores the exponential factor of N
    int res = 1;
    int mod = 1000000007;

    // Iterate over the range [2, N]
    for(int i = 2; i < N + 1; i++)

        // Update res
        res = (int)Math.pow(i, res) % mod;

    // Return res
    return res;
}

// Driver code
public static void main(String[] args)
{

    // Input
    int N = 4;

    // Function call
    System.out.println((ExpoFactorial(N)));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find exponential factorial
# of a given number

def ExpoFactorial(N):
    # Stores the exponential factor of N
    res = 1
    mod = (int)(1000000007)

    # Iterate over the range [2, N]
    for i in range(2, N + 1):
        # Update res
        res = pow(i, res, mod)

    # Return res
    return res

# Driver Code

# Input
N = 4
# Function call
print(ExpoFactorial(N))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find exponential factorial
// of a given number
static int ExpoFactorial(int N)
{

    // Stores the exponential factor of N
    int res = 1;
    int mod = 1000000007;

    // Iterate over the range [2, N]
    for(int i = 2; i < N + 1; i++)

        // Update res
        res = (int)Math.Pow(i, res) % mod;

    // Return res
    return res;
}

// Driver Code
public static void Main()
{
    // Input
    int N = 4;

    // Function call
    Console.Write(ExpoFactorial(N));

}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find exponential factorial
// of a given number
function ExpoFactorial(N) {

    // Stores the exponential factor of N
    let res = 1;
    let mod = 1000000007;

    // Iterate over the range [2, N]
    for (let i = 2; i < N + 1; i++)

        // Update res
        res = Math.pow(i, res) % mod;

    // Return res
    return res;
}

// Driver Code

// Input
let N = 4;

// Function call
document.write((ExpoFactorial(N)));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
262144
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*