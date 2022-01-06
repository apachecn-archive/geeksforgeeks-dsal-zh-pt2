# 将 N 减少到 0 所需的最小操作次数

> 原文:[https://www . geesforgeks . org/最小操作数-需要将 n 减少到 0/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-reduce-n-to-0/)

给定一个**整数 N** ，任务是通过执行以下两个操作来计算将 **N** 的值减少到 **0** 所需的最小步数:

*   考虑整数 **A** 和 **B** 其中 **N = A * B** (A！= 1 和 B！= 1)，将 **N** 降低至 **min(A，B)**
*   将 **N** 的值减少 **1**

**示例:**

> **输入:** N = 3
> **输出:** 3
> **说明:**
> 涉及的步数为 3 - > 2 - > 1 - > 0
> 因此，需要的最小步数为 3。
> 
> **输入:** N = 4
> **输出:** 3
> **说明:**
> 涉及的步骤有 4- > 2- > 1- > 0。
> 因此，最少需要 3 步。

**天真方法:**想法是使用动态规划的概念。按照以下步骤解决问题:

*   这个问题的简单解决方法是用每个可能的值替换 **N** ，直到不为 0。
*   当 **N** 达到 0 时，将**步数**与目前得到的**最小值**进行比较，得到最优答案。
*   最后，打印计算出的**最小步数**。

> 插图:
> 
> N = 4，
> 
> *   在应用第一个规则时，4 的因子是**【1，2，4】。**
>     因此，所有可能的配对( **a、b** )都是( **1** * 4)、( **2** * 2)、( **4** * 1)。
>     只有满足条件的配对( **a！=1 和 b！=1)** 为 **(2，2)** 。因此，将 **4 减为 2** 。
>     最后，在 **3** 步骤(4 - > 2 - > 1 - > 0)中将 **N** 降低至 **0**
> *   在应用第二个规则时，需要的步骤是 **4** 、(4 - > 3 - > 2 - > 1 - > 0)。
>     
> 
> ```
> Recursive tree for N = 4 is
>                   4
>                 /   \
>                3     2(2*2)
>                |      |
>                2      1
>                |      |
>                1      0
>                |
>                0
> ```
> 
> *   因此，将 N 降至 0 所需的最小步数为 **3** 。

因此，关系是:

> f(N) = 1 + min( f(N-1)，min(f(x))，其中 **N % x == 0** 和 **x** 在范围**【2，K】**内，其中 **K = sqrt(N)**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// steps required to reduce n
int downToZero(int n)
{
    // Base case
    if (n <= 3)
        return n;

    // Allocate memory for storing
    // intermediate results
    vector<int> dp(n + 1, -1);

    // Store base values
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 2;
    dp[3] = 3;

    // Stores square root
    // of each number
    int sqr;
    for (int i = 4; i <= n; i++) {

        // Compute square root
        sqr = sqrt(i);

        int best = INT_MAX;

        // Use rule 1 to find optimized
        // answer
        while (sqr > 1) {

            // Check if it perfectly divides n
            if (i % sqr == 0) {
                best = min(best, 1 + dp[sqr]);
            }

            sqr--;
        }

        // Use of rule 2 to find
        // the optimized answer
        best = min(best, 1 + dp[i - 1]);

        // Store computed value
        dp[i] = best;
    }

    // Return answer
    return dp[n];
}

// Driver Code
int main()
{
    int n = 4;
    cout << downToZero(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to count the minimum
// steps required to reduce n
static int downToZero(int n)
{

    // Base case
    if (n <= 3)
        return n;

    // Allocate memory for storing
    // intermediate results
    int []dp = new int[n + 1];
    for(int i = 0; i < n + 1; i++)
        dp[i] = -1;

    // Store base values
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 2;
    dp[3] = 3;

    // Stores square root
    // of each number
    int sqr;
    for(int i = 4; i <= n; i++)
    {

        // Compute square root
        sqr = (int)Math.sqrt(i);

        int best = Integer.MAX_VALUE;

        // Use rule 1 to find optimized
        // answer
        while (sqr > 1)
        {

            // Check if it perfectly divides n
            if (i % sqr == 0)
            {
                best = Math.min(best, 1 + dp[sqr]);
            }
            sqr--;
        }

        // Use of rule 2 to find
        // the optimized answer
        best = Math.min(best, 1 + dp[i - 1]);

        // Store computed value
        dp[i] = best;
    }

    // Return answer
    return dp[n];
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;
    System.out.print(downToZero(n));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math
import sys

# Function to count the minimum
# steps required to reduce n
def downToZero(n):

    # Base case
    if (n <= 3):
        return n

    # Allocate memory for storing
    # intermediate results
    dp = [-1] * (n + 1)

    # Store base values
    dp[0] = 0
    dp[1] = 1
    dp[2] = 2
    dp[3] = 3

    # Stores square root
    # of each number
    for i in range(4, n + 1):

        # Compute square root
        sqr = (int)(math.sqrt(i))

        best = sys.maxsize

        # Use rule 1 to find optimized
        # answer
        while (sqr > 1):

            # Check if it perfectly divides n
            if (i % sqr == 0):
                best = min(best, 1 + dp[sqr])

            sqr -= 1

        # Use of rule 2 to find
        # the optimized answer
        best = min(best, 1 + dp[i - 1])

        # Store computed value
        dp[i] = best

    # Return answer
    return dp[n]

# Driver Code
if __name__ == "__main__":

    n = 4

    print(downToZero(n))

# This code is contributed by chitranayal   
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the minimum
// steps required to reduce n
static int downToZero(int n)
{

    // Base case
    if (n <= 3)
        return n;

    // Allocate memory for storing
    // intermediate results
    int []dp = new int[n + 1];
    for(int i = 0; i < n + 1; i++)
        dp[i] = -1;

    // Store base values
    dp[0] = 0;
    dp[1] = 1;
    dp[2] = 2;
    dp[3] = 3;

    // Stores square root
    // of each number
    int sqr;
    for(int i = 4; i <= n; i++)
    {

        // Compute square root
        sqr = (int)Math.Sqrt(i);

        int best = int.MaxValue;

        // Use rule 1 to find optimized
        // answer
        while (sqr > 1)
        {

            // Check if it perfectly divides n
            if (i % sqr == 0)
            {
                best = Math.Min(best, 1 + dp[sqr]);
            }
            sqr--;
        }

        // Use of rule 2 to find
        // the optimized answer
        best = Math.Min(best, 1 + dp[i - 1]);

        // Store computed value
        dp[i] = best;
    }

    // Return answer
    return dp[n];
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    Console.Write(downToZero(n));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
    // Javascript Program to implement
    // the above approach

    // Function to count the minimum
    // steps required to reduce n
    function downToZero(n)
    {
        // Base case
        if (n <= 3)
            return n;

        // Allocate memory for storing
        // intermediate results
        let dp = new Array(n + 1)
        dp.fill(-1);

        // Store base values
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;

        // Stores square root
        // of each number
        let sqr;
        for (let i = 4; i <= n; i++) {

            // Compute square root
            sqr = Math.sqrt(i);

            let best = Number.MAX_VALUE;

            // Use rule 1 to find optimized
            // answer
            while (sqr > 1) {

                // Check if it perfectly divides n
                if (i % sqr == 0) {
                    best = Math.min(best, 1 + dp[sqr]);
                }

                sqr--;
            }

            // Use of rule 2 to find
            // the optimized answer
            best = Math.min(best, 1 + dp[i - 1]);

            // Store computed value
            dp[i] = best;
        }

        // Return answer
        return dp[n];
    }

    let n = 4;
    document.write(downToZero(n));

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N * sqrt(N))*
T5**辅助空间:** O(N)

**高效方法:**思路是观察用 N '代替 N 是可能的，其中 N' = min(a，b) (N = a * b) (a！= 1 和 b！= 1).

*   如果 **N 为偶数**，那么除 **N** 的最小值为 **2** 。因此，直接计算 **f(N) = 1 + f(2) = 3。**
*   如果 **N 为奇数**，则通过 **1** 将其减少 **N** ，即**N = N–1**。应用与偶数相同的逻辑。因此，对于奇数，所需的最小步数为 **4** 。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// steps required to reduce n
int downToZero(int n)
{
    // Base case
    if (n <= 3)
        return n;

    // Return answer based on
    // parity of n
    return n % 2 == 0 ? 3 : 4;
}

// Driver Code
int main()
{
    int n = 4;
    cout << downToZero(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG{

// Function to find the minimum
// steps required to reduce n
static int downToZero(int n)
{
    // Base case
    if (n <= 3)
        return n;

    // Return answer based on
    // parity of n
    return n % 2 == 0 ? 3 : 4;
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;
    System.out.println(downToZero(n));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to find the minimum
# steps required to reduce n
def downToZero(n):

    # Base case
    if (n <= 3):
        return n;

    # Return answer based on
    # parity of n
    if(n % 2 == 0):
        return 3;
    else:
        return 4;

# Driver Code
if __name__ == '__main__':
    n = 4;
    print(downToZero(n));

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to find the minimum
// steps required to reduce n
static int downToZero(int n)
{
    // Base case
    if (n <= 3)
        return n;

    // Return answer based on
    // parity of n
    return n % 2 == 0 ? 3 : 4;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    Console.WriteLine(downToZero(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript Program to implement
    // the above approach

    // Function to find the minimum
    // steps required to reduce n
    function downToZero(n)
    {
        // Base case
        if (n <= 3)
            return n;

        // Return answer based on
        // parity of n
        return n % 2 == 0 ? 3 : 4;
    }

    let n = 4;
    document.write(downToZero(n));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)