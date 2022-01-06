# 计算将 C 一分为二的方法，并加到 A 和 B 上，使 A 严格大于 B

> 原文:[https://www . geeksforgeeks . org/count-将 c 分成两部分并添加到 a 和 b 中以使 a 严格大于 b 的方法/](https://www.geeksforgeeks.org/count-ways-to-divide-c-in-two-parts-and-add-to-a-and-b-to-make-a-strictly-greater-than-b/)

给定三个整数 **A、B** 和 **C** ，任务是统计将 **C** 分成两部分的方式数，并加上 **A** 和 **B** ，使得 **A 严格大于 B** 。
**示例:**

> **输入:** A = 5，B = 3，C = 4
> **输出:** 3
> 除 C 后 A 和 B 的可能值为:
> A = 7，B = 5 其中 C 分为 2 和 2。
> A = 8，B = 4 其中 C 分为 3 和 1。
> A–9，B = 3，其中 C 分为 4 和 0。
> **输入:** A = 3，B = 5，C = 5
> **输出:** 2

**方法:**仔细观察，这个问题形成以下关系。

*   让 **A** 和 **B** 分别增加 **addA** 和 **addB** 。
*   因此 **addA + addB = C** 并且它应该满足不等式 **A + addA > B + addB** 。
*   现在，既然**addB = C–addA**并把它放在不等式中:

```
A + addA > B + (C - addA)
or, 2addA > C + B - A
or, 2addA >= C + B - A + 1
or, addA >= (C + B - A + 1) / 2
```

*   由于 **addA** 必须为非负数， **addA = max(0，(C+B–A+1)/2)**。
*   除法应该是上限除法，因此我们可以改写为 **addA = max(0，(C+B–A+2)/2)。**
*   让这个值等于 **minAddA** 。由于所有来自**【米纳达，C】**的整数值 **addA** 满足关系 **A + addA > B + addB** ，因此所需的路数等于**最大值(0，C–米纳达+ 1)** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of ways to divide
// C into two parts and add to A and B such
// that A is strictly greater than B
int countWays(int A, int B, int C)
{
    // Minimum value added to A to satisfy
    // the given relation
    int minAddA = max(0, (C + B - A + 2) / 2);

    // Number of different values of A, i.e.,
    // number of ways to divide C
    int count_ways = max(C - minAddA + 1, 0);

    return count_ways;
}

// Driver code
int main()
{
    int A = 3, B = 5, C = 5;

    cout << countWays(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

    // Function to count the number of ways to divide
    // C into two parts and add to A and B such
    // that A is strictly greater than B
    static int countWays(int A, int B, int C)
    {
        // Minimum value added to A to satisfy
        // the given relation
        int minAddA = Math.max(0, (C + B - A + 2) / 2);

        // Number of different values of A, i.e.,
        // number of ways to divide C
        int count_ways = Math.max(C - minAddA + 1, 0);

        return count_ways;
    }

    // Driver code
    public static void main(String args[])
    {
        int A = 3, B = 5, C = 5;

        System.out.println(countWays(A, B, C));
    }
}

// This code is contributed by AbhiThakur
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count the number of ways to divide
# C into two parts and add to A and B such
# that A is strictly greater than B
def countWays(A, B, C):

    # Minimum value added to A to satisfy
    # the given relation
    minAddA = max(0, (C + B - A + 2) // 2)

    # Number of different values of A, i.e.,
    # number of ways to divide C
    count_ways = max(C - minAddA + 1, 0)

    return count_ways

# Driver code
A = 3
B = 5
C = 5
print(countWays(A, B, C))

# This code is contributed by shivanisingh
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to count the number of ways to divide
// C into two parts and add to A and B such
// that A is strictly greater than B
static int countWays(int A, int B, int C)
{
    // Minimum value added to A to satisfy
    // the given relation
    int minAddA = Math.Max(0, (C + B - A + 2) / 2);

    // Number of different values of A, i.e.,
    // number of ways to divide C
    int count_ways = Math.Max(C - minAddA + 1, 0);

    return count_ways;
}

// Driver Code
public static void Main(String[] args)
{
    int A = 3, B = 5, C = 5;

    Console.Write(countWays(A, B, C));
}

}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to count the number of ways to divide
// C into two parts and add to A and B such
// that A is strictly greater than B
function countWays(A, B, C)
{
    // Minimum value added to A to satisfy
    // the given relation
    var minAddA = Math.max(0, parseInt((C + B - A + 2) / 2));

    // Number of different values of A, i.e.,
    // number of ways to divide C
    var count_ways = Math.max(C - minAddA + 1, 0);

    return count_ways;
}

// Driver code
var A = 3, B = 5, C = 5;
document.write( countWays(A, B, C));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
```