# 从(1，1)

开始达到 N 的最小移动次数

> 原文:[https://www . geesforgeks . org/最小移动次数-到达-n-从-1-1 开始/](https://www.geeksforgeeks.org/minimum-number-of-moves-to-reach-n-starting-from-1-1/)

给定一个整数 **N** 和一个无限表，其中 **i <sup>第</sup>T5】行和 **j <sup>第</sup>T9】列包含值 **i *j** 。任务是从单元格 **(1，1)** 开始，找到到达包含 **N** 的单元格的最小移动次数。
**注:**从 **(i，j)** 开始只有 **(i + 1，j)** 和 **(i，j + 1)**
**例:****** 

> **输入:** N = 10
> **输出:** 5
> (1，1)—>(2，1)—>(2，2)—>(2，3)—>(2，4)—>(2，5)
> **输入:** N = 7
> **输出:** 6

**接近:**注意，任何细胞 **(i，j)** 都可以在**I+j–2**步中到达。因此，仅需要一对 **(i，j)****I * j = N**来最小化 **i + j** 。通过找到所有可能的配对 **(i，j)** 并在 **O(√N)** 中检查，就可以找到。为此，不失一般性，可以假设 **i ≤ j** 、 **i ≤ √N** ，因为 **N = i * j ≥ i <sup>2</sup>** 。所以 **√N ≥ i <sup>2</sup>** 即 **√N ≥ i** 。
因此，从 **1** 到 **√N** 迭代 **i** 的所有可能值，在所有可能的对 **(i，j)** 中，选择**I+j–2**的最低值，这就是所需答案。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of moves required to reach the cell
// containing N starting from (1, 1)
int min_moves(int n)
{
    // To store the required answer
    int ans = INT_MAX;

    // For all possible values of divisors
    for (int i = 1; i * i <= n; i++) {

        // If i is a divisor of n
        if (n % i == 0) {

            // Get the moves to reach n
            ans = min(ans, i + n / i - 2);
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int n = 10;

    cout << min_moves(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum number
// of moves required to reach the cell
// containing N starting from (1, 1)
static int min_moves(int n)
{
    // To store the required answer
    int ans = Integer.MAX_VALUE;

    // For all possible values of divisors
    for (int i = 1; i * i <= n; i++)
    {

        // If i is a divisor of n
        if (n % i == 0)
        {

            // Get the moves to reach n
            ans = Math.min(ans, i + n / i - 2);
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 10;

    System.out.println(min_moves(n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

from math import sqrt

# Function to return the minimum number
# of moves required to reach the cell
# containing N starting from (1, 1)
def min_moves(n) :

    # To store the required answer
    ans = sys.maxsize;

    # For all possible values of divisors
    for i in range(1, int(sqrt(n)) + 1) :

        # If i is a divisor of n
        if (n % i == 0) :

            # Get the moves to reach n
            ans = min(ans, i + n // i - 2);

    # Return the required answer
    return ans;

# Driver code
if __name__ == "__main__" :

    n = 10;

    print(min_moves(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum number
// of moves required to reach the cell
// containing N starting from (1, 1)
static int min_moves(int n)
{
    // To store the required answer
    int ans = int.MaxValue;

    // For all possible values of divisors
    for (int i = 1; i * i <= n; i++)
    {

        // If i is a divisor of n
        if (n % i == 0)
        {

            // Get the moves to reach n
            ans = Math.Min(ans, i + n / i - 2);
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;

    Console.WriteLine(min_moves(n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the minimum number
    // of moves required to reach the cell
    // containing N starting from (1, 1)
    function min_moves(n)
    {
        // To store the required answer
        let ans = Number.MAX_VALUE;

        // For all possible values of divisors
        for (let i = 1; i * i <= n; i++)
        {

            // If i is a divisor of n
            if (n % i == 0)
            {

                // Get the moves to reach n
                ans = Math.min(ans, i + parseInt(n / i, 10) - 2);
            }
        }

        // Return the required answer
        return ans;
    }

    let n = 10;

    document.write(min_moves(n));

</script>
```

**Output:** 

```
5
```