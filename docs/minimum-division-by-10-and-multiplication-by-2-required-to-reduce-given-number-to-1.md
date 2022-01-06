# 将给定数减少到 1 所需的最小除 10 和乘 2

> 原文:[https://www . geeksforgeeks . org/将给定数字减 1 所需的最小除以 10 再乘以 2/](https://www.geeksforgeeks.org/minimum-division-by-10-and-multiplication-by-2-required-to-reduce-given-number-to-1/)

给定一个整数 **N** ，任务是将 **N** 减少到 **1** 的最小操作数，包括乘以 **2** 和除以 **10** 。如果无法获得 **1** ，则打印**-1”**。

**示例:**

> **输入:** N = 5
> **输出:** 2
> **说明:**
> 下面是执行的操作:
> **第一次操作:**N 乘以 2。因此，N = 5 * 2 = 10。
> **第 2 次运算:**N 除以 10。因此，N = 10/10 = 1。
> 因此，所需的最小操作次数为 2。
> 
> **输入:** N = 4
> **输出:** -1

**方法:**思路是检查给定数字 M 的[质因数。如果给定的数字除了 **2** 和 **5** 之外还有**质因数**，则不可能通过给定的操作将给定的数字减少到 **1** 。如果 **2** 的计数超过了 **5** 的计数，那么**不可能**将 **N** 降低到 **1** ，因为 **2**](https://www.geeksforgeeks.org/prime-factor/) 的所有[幂都不能降低。
按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

*   计算 **N** 的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)中存在的 **2** 的数量并将其存储在变量中，比如 **cnt2** ，并将 **N** 更新为**N/2<sup>CNT 2</sup>T13】。**
*   计算 **N** 的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)中存在的 **5** 的数量，并将其存储在变量中，比如 **cnt5** ，并将 **N** 更新为**N/5<sup>CNT 5</sup>T13】。**
*   完成上述步骤后，如果 **N** 为 **1** 和 **cnt2 ≤ cnt5** ，则所需的最小步骤数为**2 * CNT 5–CNT 2**。
*   否则，打印**-1”**为 **N** 不能用给定的操作还原为 **1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// operations required to reduce N to 1
int minimumMoves(int n)
{

    // Stores count of powers of 2 and 5
    int cnt2 = 0, cnt5 = 0;

    // Calculating the primefactors 2
    while (n % 2 == 0) {
        n /= 2;
        cnt2++;
    }

    // Calculating the primefactors 5
    while (n % 5 == 0) {
        n /= 5;
        cnt5++;
    }

    // If n is 1 and cnt2 <= cnt5
    if (n == 1 && cnt2 <= cnt5) {

        // Return the minimum operations
        return 2 * cnt5 - cnt2;
    }

    // Otherwise, n can't be reduced
    else
        return -1;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 25;

    // Function Call
    cout << minimumMoves(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum number
// operations required to reduce N to 1
static int minimumMoves(int n)
{

    // Stores count of powers of 2 and 5
    int cnt2 = 0, cnt5 = 0;

    // Calculating the primefactors 2
    while (n % 2 == 0)
    {
        n /= 2;
        cnt2++;
    }

    // Calculating the primefactors 5
    while (n % 5 == 0)
    {
        n /= 5;
        cnt5++;
    }

    // If n is 1 and cnt2 <= cnt5
    if (n == 1 && cnt2 <= cnt5)
    {

        // Return the minimum operations
        return 2 * cnt5 - cnt2;
    }

    // Otherwise, n can't be reduced
    else
        return -1;
}

// Driver Code
public static void main(String[] args)
{

    // Given Number N
    int N = 25;

    // Function Call
    System.out.print(minimumMoves(N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# operations required to reduce N to 1
def minimumMoves(n):

    # Stores count of powers of 2 and 5
    cnt2 = 0
    cnt5 = 0

    # Calculating the primefactors 2
    while (n % 2 == 0):
        n //= 2
        cnt2 += 1

    # Calculating the primefactors 5
    while (n % 5 == 0):
        n //= 5
        cnt5 += 1

    # If n is 1 and cnt2 <= cnt5
    if (n == 1 and cnt2 <= cnt5):

        # Return the minimum operations
        return 2 * cnt5 - cnt2

    # Otherwise, n can't be reduced
    else:
        return -1

# Driver Code
if __name__ == '__main__':

    # Given Number N
    N = 25

    # Function Call
    print(minimumMoves(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// operations required to reduce N to 1
static int minimumMoves(int n)
{

    // Stores count of powers of 2 and 5
    int cnt2 = 0, cnt5 = 0;

    // Calculating the primefactors 2
    while (n % 2 == 0)
    {
        n /= 2;
        cnt2++;
    }

    // Calculating the primefactors 5
    while (n % 5 == 0)
    {
        n /= 5;
        cnt5++;
    }

    // If n is 1 and cnt2 <= cnt5
    if (n == 1 && cnt2 <= cnt5)
    {

        // Return the minimum operations
        return 2 * cnt5 - cnt2;
    }

    // Otherwise, n can't be reduced
    else
        return -1;
}

// Driver Code
public static void Main()
{

    // Given Number N
    int N = 25;

    // Function Call
    Console.WriteLine(minimumMoves(N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the minimum number
// operations required to reduce N to 1
function minimumMoves(n)
{

    // Stores count of powers of 2 and 5
    let cnt2 = 0, cnt5 = 0;

    // Calculating the primefactors 2
    while (n % 2 == 0)
    {
        n /= 2;
        cnt2++;
    }

    // Calculating the primefactors 5
    while (n % 5 == 0)
    {
        n /= 5;
        cnt5++;
    }

    // If n is 1 and cnt2 <= cnt5
    if (n == 1 && cnt2 <= cnt5)
    {

        // Return the minimum operations
        return 2 * cnt5 - cnt2;
    }

    // Otherwise, n can't be reduced
    else
        return -1;
}

    // Driver Code

    // Given Number N
    let N = 25;

    // Function Call
    document.write(minimumMoves(N));

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*