# 通过 N 个平面相交形成的最大直线相交数

> 原文:[https://www . geeksforgeeks . org/最大线交叉数-n 面交叉形成的贯通线/](https://www.geeksforgeeks.org/maximum-number-of-line-intersections-formed-through-intersection-of-n-planes/)

给定 N 架飞机。任务是找到通过 N 个平面的交点可以形成的最大直线交点数。
**例:**

> **输入:** N = 3
> **输出:** 3
> **输入:** N = 5
> **输出:** 10

**方法:**
假设有 N 个平面，使得没有 3 个平面相交于一条相交线，也没有 2 个平面相互平行。在保留上述两个条件的同时，向该空间添加第 N+1 个平面应该是可能的。在这种情况下，该平面将与 N 个平面中的每一个相交成“N”条不同的线。
因此，“第 N+1”个平面可以向相交线的总数添加“N”条新线。同样，第 N 个平面最多可以添加“N-1”条不同的相交线。因此，很容易看出，对于“N”个平面，最大相交线数可能是:

```
(N-1) + (N-2) +...+ 1 = N*(N-1)/2
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the above pproach
#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number of
// intersections possible
int countIntersections(int n)
{
    return n * (n - 1) / 2;
}

// Driver Code
int main()
{
    int n = 3;

    cout << countIntersections(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to count maximum number of
    // intersections possible
    static int countIntersections(int n)
    {
        return n * (n - 1) / 2;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 3;

        System.out.println(countIntersections(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above pproach

# Function to count maximum number of
# intersections possible
def countIntersections(n):
    return n * (n - 1) // 2

# Driver Code
n = 3

print(countIntersections(n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to count maximum number of
    // intersections possible
    static int countIntersections(int n)
    {
        return n * (n - 1) / 2;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int n = 3;

        Console.WriteLine(countIntersections(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to count maximum number of
// intersections possible
function countIntersections(n)
{
    return n * (n - 1) / 2;
}

// Driver Code
var n = 3;
document.write(countIntersections(n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(1)