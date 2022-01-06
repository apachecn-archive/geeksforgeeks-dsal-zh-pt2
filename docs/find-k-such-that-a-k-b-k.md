# 找到 K，使得| A–K | = | B–K |

> 原文:[https://www.geeksforgeeks.org/find-k-such-that-a-k-b-k/](https://www.geeksforgeeks.org/find-k-such-that-a-k-b-k/)

给定两个整数 **A** 和 **B** ，其中 **(A ≠ B)** 。任务是找到 **K** 使得**| A–K | = | B–K |**。如果不存在这样的 **K** ，则打印 **-1** 。

**示例:**

> **输入:** A = 2，B = 16
> T3】输出:9
> | 2–9 | = | 16–9 | = 7
> 
> **输入:** A = 5，B = 2
> **输出:** -1

**进场:**给出 **A ≠ B** 。所以让 **A < B** 那么就有三种情况:

*   **K < A:** 这给出了**A–K = B–K**这给出了 **A = B** 这是假的。
*   **K > B:** 这给出了**K–A = K–B**，也是假的。
*   **A ≤ K ≤ B:** 这给出了**K–A = B–K**，这给出了 **2 * K = A + B**

如果 **A + B** 是奇数，那么就没有解。如果 **A + B** 是偶数，那么答案是 **(A + B) / 2** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find k such that
// |a - k| = |b - k|
int find_k(int a, int b)
{
    // If (a + b) is even
    if ((a + b) % 2 == 0)
        return ((a + b) / 2);

    return -1;
}

// Driver code
int main()
{
    int a = 2, b = 16;

    cout << find_k(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find k such that
// |a - k| = |b - k|
static int find_k(int a, int b)
{
    // If (a + b) is even
    if ((a + b) % 2 == 0)
        return ((a + b) / 2);

    return -1;
}

// Driver code
public static void main(String[] args)
{
    int a = 2, b = 16;

    System.out.println(find_k(a, b));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find k such that
# |a - k| = |b - k|
def find_k(a, b) :

    # If (a + b) is even
    if ((a + b) % 2 == 0) :
        return ((a + b) // 2);

    return -1;

# Driver code
if __name__ == "__main__" :

    a = 2; b = 16;

    print(find_k(a, b));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find k such that
// |a - k| = |b - k|
static int find_k(int a, int b)
{
    // If (a + b) is even
    if ((a + b) % 2 == 0)
        return ((a + b) / 2);

    return -1;
}

// Driver code
public static void Main()
{
    int a = 2, b = 16;

    Console.Write(find_k(a, b));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find k such that
// |a - k| = |b - k|
function find_k(a, b)
{

    // If (a + b) is even
    if ((a + b) % 2 == 0)
        return ((a + b) / 2);

    return -1;
}

// Driver code
var a = 2, b = 16;

document.write( find_k(a, b));

// This code is contributed by akshitsaxenaa09

</script>
```

**Output**

```
9
```