# 计算可放置在满足给定条件的 M * N 矩形板中的尺寸为 2 * 1 的瓷砖数量

> 原文:[https://www . geeksforgeeks . org/count-dimension-tiles-2-1-可放置在满足给定条件的 m-n-矩形板中/](https://www.geeksforgeeks.org/count-tiles-of-dimensions-2-1-that-can-be-placed-in-an-m-n-rectangular-board-that-satisfies-the-given-conditions/)

给定两个整数 **M** 和 **N** ，任务是找到最小数量的大小为 **2 * 1** 的瓷砖，这些瓷砖可以放置在 M * N 网格上，从而满足以下条件:

1.  每个瓷砖必须完全覆盖木板的 2 个正方形。
2.  任何一对瓷砖都不能重叠。
3.  每个瓷砖必须完全放在木板内。允许接触板的边缘。

如果无法覆盖整个电路板，打印 **-1**

> **输入:** N = 2，M = 4
> **输出:** 4
> **说明:** 4 块 2 * 1 尺寸的瓷砖。将每个图块放在一列中。
> 
> **输入:** N = 3，M = 3
> **输出:** -1

**方法:**按照以下步骤解决问题

1.  如果 **N** 为偶数， **(N / 2) * M** 可以放置瓷砖覆盖整个板材。
2.  如果 **N** 为奇数，则为 2 * 1 个瓦片的瓦片，因为长度为奇数，不能表示为 2 的倍数

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count tiles of dimensions
// 2 x 1 that can be placed in a grid of
// dimensions M * N as per given conditions
int numberOfTiles(int N, int M)
{
    if (N % 2 == 1) {
        return -1;
    }

    // Number of tiles required
    return (N * 1LL * M) / 2;
}

// Driver Code
int main()
{
    int N = 2, M = 4;
    cout << numberOfTiles(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.io.*;

class GFG {

    // Function to count tiles of dimensions
    // 2 x 1 that can be placed in a grid of
    // dimensions M * N as per given conditions
    static int numberOfTiles(int n, int m)
    {
        if (n % 2 == 1) {
            return -1;
        }
        // Number of tiles required
        return (m * n) / 2;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 2, m = 4;
        System.out.println(
            numberOfTiles(n, m));
    }
}
```

## 计算机编程语言

```
# Python Program to implement
# the above approach

# Function to count tiles of dimensions
# 2 x 1 that can be placed in a grid of
# dimensions M * N as per given conditions
def numberOfTiles(N, M):
    if (N % 2 == 1):
        return -1

    # Number of tiles required
    return (N * M) // 2

# Driver Code
N = 2
M = 4
print(numberOfTiles(N, M))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# Program to implement
// the above approach

using System;

public class GFG {

    // Function to tiles of size 2 x 1
    // find the number of tiles that can
    // be placed as per the given conditions
    static int numberOfTiles(int n, int m)
    {
        if (n % 2 == 1) {
            return -1;
        }
        // Number of tiles required
        return (m * n) / 2;
    }

    // Driver Code
    static public void Main()
    {
        int n = 2, m = 4;
        Console.WriteLine(
            numberOfTiles(n, m));
    }
}
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to count tiles of dimensions
// 2 x 1 that can be placed in a grid of
// dimensions M * N as per given conditions
function numberOfTiles(n, m)
{
    if (n % 2 == 1)
    {
        return -1;
    }

    // Number of tiles required
    return (m * n) / 2;
}

// Driver Code
var n = 2, m = 4;

document.write(numberOfTiles(n, m));

// This code is contributed by kirti

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)