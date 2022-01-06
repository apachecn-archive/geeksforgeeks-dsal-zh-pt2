# Enneacontahexagon 数字

> 原文:[https://www.geeksforgeeks.org/enneacontahexagon-numbers/](https://www.geeksforgeeks.org/enneacontahexagon-numbers/)

给定一个数字 **N** ，任务是找到 **N <sup>第</sup>T5【恩内阿空塔十六宫】号。** 

> Enneacontahexagon 数是一类图形数。它有一个 96 边的多边形，叫做 Enneacontahexagon。第 N 个 Enneacontahexagon 数字计数是 96 个点的数量，所有其他点都被一个公共共享角包围并形成一个图案。最初的几个数字是 **1，96，285，568，945，1416，…**

**例:**

> **输入:** N = 2
> **输出:** 96
> **解释:**
> 第二个 Enneacontahexagonol 数是 96。
> **输入:** N = 3
> **输出:** 285

**方法:**第 N 个 Enneacontahexagon 数由公式给出:

*   s 边多边形的第 n 项= ![\frac{((s-2)n^2 - (s-4)n)}{2}  ](img/3e1c344c528b24a9b43d5ebf5753c187.png "Rendered by QuickLaTeX.com")

*   因此 96 边多边形的第 n 项是

> ![Tn =\frac{((96-2)n^2 - (96-4)n)}{2} =\frac{(94^2 - 92)}{2} ](img/a66c17be0b28039c80256462be19e942.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现:

## C++

```
// C++ implementation for
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the Nth
// Enneacontahexagon Number
int EnneacontahexagonNum(int n)
{
    return (94 * n * n - 92 * n) / 2;
}

// Driver Code
int main()
{
    int n = 3;
    cout << EnneacontahexagonNum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th
// Enneacontahexagon Number
class GFG{

// Function to find the nth
// Enneacontahexagon Number
static int enneacontahexagonNum(int n)
{
    return (94 * n * n - 92 * n) / 2;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    System.out.print(enneacontahexagonNum(n));
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation for
# above approach

# Function to find the Nth
# Enneacontahexagon Number
def EnneacontahexagonNum(n):

    return (94 * n * n - 92 * n) // 2;

# Driver Code
n = 3;
print(EnneacontahexagonNum(n));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to find N-th
// Enneacontahexagon Number
using System;
class GFG{

// Function to find the nth
// Enneacontahexagon Number
static int enneacontahexagonNum(int n)
{
    return (94 * n * n - 92 * n) / 2;
}

// Driver code
public static void Main()
{
    int n = 3;
    Console.Write(enneacontahexagonNum(n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to find N-th
// Enneacontahexagon Number

    // Function to find the nth
    // Enneacontahexagon Number
    function EnneacontahexagonNum( n) {
        return (94 * n * n - 92 * n) / 2;
    }

    // Driver code

        let n = 3;
        document.write(EnneacontahexagonNum(n));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
285
```

**参考资料:**[https://en . Wikipedia . org/wiki/eneacontahexagon](https://en.wikipedia.org/wiki/Enneacontahexagon)