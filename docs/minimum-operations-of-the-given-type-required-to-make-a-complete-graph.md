# 制作完整图形所需的给定类型的最少操作

> 原文:[https://www . geeksforgeeks . org/制作完整图形所需的给定类型的最小操作数/](https://www.geeksforgeeks.org/minimum-operations-of-the-given-type-required-to-make-a-complete-graph/)

给定 **N** 顶点，其中 **N** 为**偶数**。最初，任何顶点之间都没有边。
您可以进行如下操作:

*   **在单次操作**中，可以将总节点分为两组，并且可以针对 **u** 和 **v** 的所有可能值绘制边缘 **(u，v)** ，使得 **u** 和 **v** 都属于不同的组。

任务是找到将这些顶点转换成[完整图形](http://mathworld.wolfram.com/CompleteGraph.html)所需的最小给定操作数。
**例:**

> **输入:** N = 4
> **输出:** 2
> 操作 1:组= [1，2]，[3，4]所有可能的边都将是{1-4，1-3，2-3，2-4}。
> 操作 2:组= [1，3]，[2，4]所有可能的边都将是{1-4，1-3，2-3，2-4，1-2，3-4}。
> 图形现在是一个完整的图形。
> **输入:** N = 10
> **输出:** 4

**方法:**当每对顶点之间有一条边时，一个图将被称为完全图。这里的问题可以通过[各个击破](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)的方式解决。要执行最少数量的操作，将顶点分成两组，每组有 **N / 2** 个顶点，并绘制所有可能的边。现在观察，我们必须在现在处于同一组的顶点之间创建边。所以我们会把它们分成两半，放在不同的组里。
这些步骤将被重复，直到所有的边都被画出，即最大 **⌈对数 2(N) ⌉** 次，因为操作将把边分成大小相等的两半。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return
// the minimum number of steps required
int minOperations(int N)
{
    double x = log2(N);

    int ans = ceil(x);

    return ans;
}

// Driver Code
int main()
{
    int N = 10;
    cout << minOperations(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to return the minimum
    // number of steps required
    static int minOperations(int N)
    {
        double x = Math.log(N) / Math.log(2);

        int ans = (int)(Math.ceil(x));

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 10;
        System.out.println(minOperations(N));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import log2, ceil

# Function to return the minimum
# number of steps required
def minOperations(N):
    x = log2(N)

    ans = ceil(x)

    return ans

# Driver Code
if __name__ == '__main__':
    N = 10
    print(minOperations(N))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the minimum
// number of steps required
static int minOperations(int N)
{
    double x = Math.Log(N, 2);

    int ans = (int)(Math.Ceiling(x));

    return ans;
}

// Driver Code
static void Main()
{
    int N = 10;
    Console.WriteLine(minOperations(N));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum number
// of steps required
function minOperations($N)
{
    $x = log($N, 2);

    $ans = ceil($x);

    return $ans;
}

// Driver Code
$N = 10;
echo minOperations($N);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return the minimum
    // number of steps required
    function minOperations(N)
    {
        var x = Math.log(N) / Math.log(2);
        var ans = parseInt( (Math.ceil(x)));
        return ans;
    }

    // Driver Code   
    var N = 10;
    document.write(minOperations(N));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
4
```