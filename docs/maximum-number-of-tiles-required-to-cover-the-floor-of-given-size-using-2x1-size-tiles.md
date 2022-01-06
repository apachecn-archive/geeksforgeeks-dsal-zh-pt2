# 使用 2×1 尺寸瓷砖覆盖给定尺寸地板所需的最大瓷砖数量

> 原文:[https://www . geeksforgeeks . org/需要覆盖给定尺寸地板的最大瓷砖数量-使用 2x1 尺寸的瓷砖/](https://www.geeksforgeeks.org/maximum-number-of-tiles-required-to-cover-the-floor-of-given-size-using-2x1-size-tiles/)

给定尺寸为 **MxN** 的地板和尺寸为 **2×1** 的瓷砖，任务是找到尺寸为 **MxN** 的地板所需的最大瓷砖数量。
***注意:**瓷砖可以水平放置，也可以垂直放置，两块瓷砖不得重叠。*

**示例:**

> **输入:** M = 2，N = 4
> **输出:** 4
> **说明:**
> 需要 4 块瓷砖铺地。
> 
> **输入:** M = 3，N = 3
> **输出:** 4
> **说明:**
> 需要 4 块瓷砖铺地。

**进场:**

1.  如果 **N** 是**甚至**，那么任务就是放置 m 排 **(N/2)** 数量的瓷砖覆盖整个地板。
2.  否则如果 **N** 为**奇数**，则按照上一点中讨论的相同方式覆盖 **M** 行直到**N–1**(偶数)列，并将 **(M/2)** 数量的瓷砖放在最后一列。如果 **M 和 N 都是奇数**，则地板的一个单元保持未被覆盖。
3.  因此，瓷砖的最大数量是**地板((M * N) / 2)** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of tiles required to cover the floor
// of size m x n using 2 x 1 size tiles
void maximumTiles(int n, int m)
{
    // Print the answer
    cout << (m * n) / 2 << endl;
}

// Driver Code
int main()
{
    // Given M and N
    int M = 3;
    int N = 4;

    // Function Call
    maximumTiles(N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum number
// of tiles required to cover the floor
// of size m x n using 2 x 1 size tiles
static void maximumTiles(int n, int m)
{

    // Print the answer
    System.out.println((m * n) / 2);
}

// Driver code
public static void main (String[] args)
{

    // Given M and N
    int M = 3;
    int N = 4;

    // Function call
    maximumTiles(N, M);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum number
# of tiles required to cover the floor
# of size m x n using 2 x 1 size tiles
def maximumTiles(n, m):

    # Prthe answer
    print(int((m * n) / 2));

# Driver code
if __name__ == '__main__':

    # Given M and N
    M = 3;
    N = 4;

    # Function call
    maximumTiles(N, M);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum number
// of tiles required to cover the floor
// of size m x n using 2 x 1 size tiles
static void maximumTiles(int n, int m)
{

    // Print the answer
    Console.WriteLine((m * n) / 2);
}

// Driver code
public static void Main(String[] args)
{

    // Given M and N
    int M = 3;
    int N = 4;

    // Function call
    maximumTiles(N, M);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum number
// of tiles required to cover the floor
// of size m x n using 2 x 1 size tiles
function maximumTiles(n, m)
{

    // Print the answer
    document.write((m * n) / 2);
}

// Driver Code

     // Given M and N
    let M = 3;
    let N = 4;

    // Function call
    maximumTiles(N, M);

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)