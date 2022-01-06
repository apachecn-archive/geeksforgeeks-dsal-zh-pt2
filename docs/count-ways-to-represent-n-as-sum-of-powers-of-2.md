# 计数方式表示 N 为 2 的幂之和

> 原文:[https://www . geeksforgeeks . org/count-way-to-representative-n-as-sum-of-2/](https://www.geeksforgeeks.org/count-ways-to-represent-n-as-sum-of-powers-of-2/)

给定一个整数 **N** ，任务是统计将 **N** 表示为 2 的[次幂之和的方式数。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

***例:***

> **输入:** N = 4
> **输出:** 4
> **解释:**使用 2 的幂获得和 N 的所有可能方法是{4，2+2，1+1+1+1，2+1+1}。
> 
> **输入:** N = 5
> **输出:** 4
> **说明:**使用 2 的幂得到和 N 的所有可能方式是{4 + 1，2+2 + 1，1+1+1+1 + 1，2+1+1 + 1}

**天真法:**解决问题最简单的方法是 g 生成所有值小于 **N** 的 2 的幂，并将所有组合打印到代表的和 **N** 。

**高效方法:**优化上述方法，思路是使用[递归](https://www.geeksforgeeks.org/recursion/)。定义一个函数 **f(N，K)** ，该函数表示将 **N** 表示为 2 的幂之和，所有数的幂都小于或等于 K，其中**K**(=**log<sub>2</sub>(N)**)是满足**2<sup>K</sup>≤<sup>N</sup>**的 2 的最大幂。

> **If (power(2，K) ≤ N) :**
> *f(N，K)= f(N–power(2，K)，K) + f(N，K–1)*//检查 power(2，K)是否可以是数字之一。
> **否则:**
> *f(N，K)=f(N，K–1)*
> **基本情况:**
> 
> *   **If (N = 0)** f(N，K)=1(只存在一种可能的方式来表示 N)
> *   **If (k==0)** f(N，K)=1(通过取 2 <sup>0</sup> 只存在 1 种可能的方式来表示 N)

下面是上述方法的实现:

## C++

```
// C++ program for above implementation
#include <bits/stdc++.h>
using namespace std;
int numberOfWays(int n, int k)
{

    // Base Cases
    if (n == 0)
        return 1;

    if (k == 0)
        return 1;

    // Check if 2^k can be used as
    // one of the numbers or not
    if (n >= pow(2, k)) {
        int curr_val = pow(2, k);
        return numberOfWays(n - curr_val, k)
               + numberOfWays(n, k - 1);
    }
    // Otherwise
    else

        // Count number of  ways to
        // N using 2 ^ k - 1
        return numberOfWays(n, k - 1);
}

// Driver Code
int main()
{
    int n = 4;
    int k = log2(n);

    cout << numberOfWays(n, k) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{
static int numberOfWays(int n, int k)
{

    // Base Cases
    if (n == 0)
        return 1;
    if (k == 0)
        return 1;

    // Check if 2^k can be used as
    // one of the numbers or not
    if (n >= (int)Math.pow(2, k))
    {
        int curr_val = (int)Math.pow(2, k);
        return numberOfWays(n - curr_val, k)
               + numberOfWays(n, k - 1);
    }

    // Otherwise
    else

        // Count number of  ways to
        // N using 2 ^ k - 1
        return numberOfWays(n, k - 1);
}

// Driver code
public static void main(String[] args)
{
    int n = 4;
    int k = (int)(Math.log(n) / Math.log(2));
     System.out.println(numberOfWays(n, k));
}
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python3 program for above implementation
from math import log2
def numberOfWays(n, k):

    # Base Cases
    if (n == 0):
        return 1
    if (k == 0):
        return 1

    # Check if 2^k can be used as
    # one of the numbers or not
    if (n >= pow(2, k)):
        curr_val = pow(2, k)
        return numberOfWays(n - curr_val, k) + numberOfWays(n, k - 1)

    # Otherwise
    else:

        # Count number of  ways to
        # N using 2 ^ k - 1
        return numberOfWays(n, k - 1)

# Driver Code
if __name__ == '__main__':
    n = 4
    k = log2(n)

    print(numberOfWays(n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{
static int numberOfWays(int n, int k)
{

    // Base Cases
    if (n == 0)
        return 1;
    if (k == 0)
        return 1;

    // Check if 2^k can be used as
    // one of the numbers or not
    if (n >= (int)Math.Pow(2, k))
    {
        int curr_val = (int)Math.Pow(2, k);
        return numberOfWays(n - curr_val, k)
               + numberOfWays(n, k - 1);
    }

    // Otherwise
    else

        // Count number of  ways to
        // N using 2 ^ k - 1
        return numberOfWays(n, k - 1);
}

// Driver code
public static void Main(String[] args)
{
    int n = 4;
    int k = (int)(Math.Log(n) / Math.Log(2));
     Console.WriteLine(numberOfWays(n, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for above implementation

function numberOfWays(n, k)
{

    // Base Cases
    if (n == 0)
        return 1;

    if (k == 0)
        return 1;

    // Check if 2^k can be used as
    // one of the numbers or not
    if (n >= Math.pow(2, k)) {
        let curr_val = Math.pow(2, k);
        return numberOfWays(n - curr_val, k)
            + numberOfWays(n, k - 1);
    }
    // Otherwise
    else

        // Count number of ways to
        // N using 2 ^ k - 1
        return numberOfWays(n, k - 1);
}

// Driver Code

    let n = 4;
    let k = Math.log2(n);

    document.write(numberOfWays(n, k) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O((logN+K) <sup>K</sup> ，其中 K 为 log<sub>2</sub>(N)*
***辅助空间:** O(1)*