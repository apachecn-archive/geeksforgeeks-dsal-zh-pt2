# 产生相等商和余数的最多 X 和 Y 的整数对的计数

> 原文:[https://www . geeksforgeeks . org/生成等商和余数的整数对计数/](https://www.geeksforgeeks.org/count-of-pairs-of-integers-up-to-x-and-y-that-generates-equal-quotient-and-remainder/)

给定两个整数 **X** 和 **Y** ，任务是统计对的数量 **(m，n)** ，使得 **m / n = m % n** 和 **1 ≤ m ≤ x** 和 **1 ≤ n ≤ y** 。

**示例:**

> **输入:** X = 4，Y = 5
> **输出:** 2
> **说明:**对(3，2)和(4，3)满足条件。
> 
> **输入:** X = 3，Y = 1
> T3】输出: 0

**方法:**给定的问题可以基于以下观察来解决:

*   要满足该条件，分子的形式必须是 **(kn + k)** 。因此， **(kn + k) / n = (kn + k) % n = k.**
*   也暗示着 **k < n** 。故 **k * k < k * n + k < = x.** 故 **k < sqrt(x)** 。
*   因此，分子从 **1** 迭代到 **sqrt(x)** 就足够了。
*   重写 **k * n + k ≤ x** 给我们**n<=(x/k–1)**。另外， **n > k** 和 **n < = y** 不受约束。
*   对于每个可能的分子值，计算可能的分母值并更新总数。

下面是上述方法的实现。

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number
// of pairs satisfying (m / n = m % n)
void countOfPairs(int x, int y)
{
    int count = 0;

    // Iterate from 1 to sqrt(x)
    for (int k = 1; k * k <= x; ++k) {

        // Combining the conditions -
        // 1) n > k
        // 2) n <= y
        // 3) n <= (x/ k -1)
        count += max(0, min(y, x / k - 1) - k);
    }
    cout << count << "\n";
}

// Driver code
int main()
{
    int x = 4;
    int y = 5;
    countOfPairs(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;

class GFG {

    // Function to calculate the number
    // of pairs satisfying (m / n = m % n)
    static void countOfPairs(int x, int y)
    {
        int count = 0;

        // Iterate from 1 to sqrt(x)
        for (int k = 1; k * k <= x; ++k) {

            // Combining the conditions -
            // 1) n > k
            // 2) n <= y
            // 3) n <= (x/ k -1)
            count
                += Math.max(
                    0, Math.min(y, x / k - 1) - k);
        }
        System.out.print(count);
    }
    // Driver code
    public static void main(String[] args)
    {
        int x = 4;
        int y = 5;
        countOfPairs(x, y);
    }
}
```

## 蟒蛇 3

```
# python 3 Program for the above approach
from math import sqrt

# Function to calculate the number
# of pairs satisfying (m / n = m % n)
def countOfPairs(x, y):
    count = 0

    # Iterate from 1 to sqrt(x)
    for k in range(1,int(sqrt(x)) + 1, 1):

        # Combining the conditions -
        # 1) n > k
        # 2) n <= y
        # 3) n <= (x/ k -1)
        count += max(0, min(y, x / k - 1) - k)
    print(int(count))

# Driver code
if __name__ == '__main__':
    x = 4
    y = 5
    countOfPairs(x, y)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# Program for the above approach
using System;

public class GFG {

    // Function to calculate the number
    // of pairs satisfying (m / n = m % n)
    static void countOfPairs(int x, int y)
    {
        int count = 0;

        // Iterate from 1 to sqrt(x)
        for (int k = 1; k * k <= x; ++k) {

            // Combining the conditions -
            // 1) n > k
            // 2) n <= y
            // 3) n <= (x/ k -1)
            count
                += Math.Max(
                    0, Math.Min(y, x / k - 1) - k);
        }
        Console.Write(count);
    }
    // Driver Code
    static public void Main()
    {
        int x = 4;
        int y = 5;
        countOfPairs(x, y);
    }
}
```

## java 描述语言

```
<script>

// JavaScript Program for the above approach

// Function to calculate the number
// of pairs satisfying (m / n = m % n)
function countOfPairs(x, y)
{
    var count = 0;
    var k;
    // Iterate from 1 to sqrt(x)
    for (k = 1; k * k <= x; ++k) {

        // Combining the conditions -
        // 1) n > k
        // 2) n <= y
        // 3) n <= (x/ k -1)
        count += Math.max(0, Math.min(y, x / k - 1) - k);
    }
    document.write(count + "<br>");
}

// Driver code
    var x = 4;
    var y = 5;
    countOfPairs(x, y);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(√X)*
***辅助空间:** O(1)*