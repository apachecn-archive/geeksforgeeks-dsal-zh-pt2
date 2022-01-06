# 找出所有 N 以内的既有五边形又有六边形的数字

> 原文:[https://www . geeksforgeeks . org/find-all-numbers-up-n-哪些都是五边形和六边形/](https://www.geeksforgeeks.org/find-all-numbers-up-to-n-which-are-both-pentagonal-and-hexagonal/)

给定一个整数 **N** ，任务是查找到 **N** 为止的所有数字，既有[五边形](https://www.geeksforgeeks.org/hexagonal-number/)也有[六边形](https://www.geeksforgeeks.org/hexagonal-number/)。
**例:**

> **输入:** N = 1000
> **输出:** 1
> **输入:** N = 100000
> **输出:** 1，40755

**进场:**

*   为了解决这个问题，我们正在生成直到 **N** 的所有五边形数字，并检查它们是否是六边形数字。
*   计算公式 **i <sup>th</sup> 五边形数**:T4

> **I *(3 * I–1)/2**

*   要检查一个五边形数字，比如说 **pn** ，是不是六边形数字:

> **( 1 + sqrt(8 * pn + 1 ) ) / 4** 需要是自然数

以下是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print numbers upto N
// which are both pentagonal as well
// as hexagonal numbers
void pen_hex(long long n)
{
    long long pn = 1;
    for (long long int i = 1;; i++) {

        // Calculate i-th pentagonal number
        pn = i * (3 * i - 1) / 2;

        if (pn > n)
            break;

        // Check if the pentagonal number
        // pn is hexagonal or not
        long double seqNum
            = (1 + sqrt(8 * pn + 1)) / 4;

        if (seqNum == long(seqNum))
            cout << pn << ", ";
    }
}

// Driver Program
int main()
{
    long long int N = 1000000;
    pen_hex(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function to print numbers upto N
// which are both pentagonal as well
// as hexagonal numbers
static void pen_hex(long n)
{
    long pn = 1;
    for(long i = 1; i < n; i++)
    {

        // Calculate i-th pentagonal number
        pn = i * (3 * i - 1) / 2;

        if (pn > n)
            break;

        // Check if the pentagonal number
        // pn is hexagonal or not
        double seqNum = (1 + Math.sqrt(
                        8 * pn + 1)) / 4;

        if (seqNum == (long)seqNum)
            System.out.print(pn + ", ");
    }
}

// Driver code
public static void main(String[] args)
{
    long N = 1000000;
    pen_hex(N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program of the above approach
import math

# Function to print numbers upto N
# which are both pentagonal as well
# as hexagonal numbers
def pen_hex(n):

    pn = 1
    for i in range(1, N):

        # Calculate i-th pentagonal number
        pn = (int)(i * (3 * i - 1) / 2)

        if (pn > n):
            break

        # Check if the pentagonal number
        # pn is hexagonal or not
        seqNum = (1 + math.sqrt(8 * pn + 1)) / 4

        if (seqNum == (int)(seqNum)):
            print(pn, end = ", ")

# Driver Code
N = 1000000

pen_hex(N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program of the above approach 
using System;
using System.Collections.Generic;

class GFG{        

// Function to print numbers upto N
// which are both pentagonal as well
// as hexagonal numbers
static void pen_hex(long n)
{
    long pn = 1;
    for(long i = 1;; i++)
    {

        // Calculate i-th pentagonal number
        pn = i * (3 * i - 1) / 2;

        if (pn > n)
            break;

        // Check if the pentagonal number
        // pn is hexagonal or not
        double seqNum = (1 + Math.Sqrt(
                         8 * pn + 1)) / 4;

        if (seqNum == (long)(seqNum))
        {
            Console.Write(pn + ", ");
        }
    }
}

// Driver Code        
public static void Main (string[] args)
{        
    long N = 1000000;

    pen_hex(N);
}        
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function to print numbers upto N
// which are both pentagonal as well
// as hexagonal numbers
function pen_hex(n)
{
    var pn = 1;
    for(i = 1; i < n; i++)
    {

        // Calculate i-th pentagonal number
        pn = parseInt(i * (3 * i - 1) / 2);

        if (pn > n)
            break;

        // Check if the pentagonal number
        // pn is hexagonal or not
        var seqNum = (1 + Math.sqrt(
                        8 * pn + 1)) / 4;

        if (seqNum == parseInt(seqNum))
            document.write(pn + ", ");
    }
}

// Driver code
var N = 1000000;
pen_hex(N);

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
1, 40755,
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*