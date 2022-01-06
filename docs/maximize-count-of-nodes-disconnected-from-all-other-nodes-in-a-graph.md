# 最大化图中与所有其他节点断开的节点数

> 原文:[https://www . geeksforgeeks . org/最大化图中所有其他节点断开的节点数/](https://www.geeksforgeeks.org/maximize-count-of-nodes-disconnected-from-all-other-nodes-in-a-graph/)

给定两个整数 **N** 和 **E** ，它们表示一个[无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)的节点数和边数，任务是最大化不连接到图中任何其他节点的节点数，而不使用任何自循环。

**示例:**

> **输入:** N = 5，E = 1
> **输出:** 3
> **解释:**
> 因为图中只有一条边可以用来连接两个节点。
> 因此，**三**节点保持断开状态。
> 
> **输入:** N = 5，E = 2
> T3】输出: 2

**方法:**该方法基于这样的思想，即为了最大化断开节点的数量，直到每两个不同的节点连接起来，新节点才会被添加到图中。下面是解决这个问题的步骤:

1.  初始化两个变量 **curr** 和 **rem** 分别存储连接的节点和未分配的边。
2.  如果 **rem** 变为 0，则所需答案为**N–curr**。
3.  否则，将**电流**的值增加 1。
4.  因此，当前步骤中保持每两个不同节点连接所需的最大边数是 **min(rem，curr)** 。从**雷**中减去，增加 **curr** 。
5.  重复此过程，直到 **rem** 降至零。
6.  最后打印**N–curr**。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function which returns
// the maximum number of
// isolated nodes
int maxDisconnected(int N, int E)
{
    // Used nodes
    int curr = 1;

    // Remaining edges
    int rem = E;

    // Count nodes used
    while (rem > 0) {
        rem = rem
              - min(
                    curr, rem);
        curr++;
    }

    // If given edges are non-zero
    if (curr > 1) {
        return N - curr;
    }
    else {
        return N;
    }
}

// Driver Code
int main()
{
    // Given N and E
    int N = 5, E = 1;

    // Function Call
    cout << maxDisconnected(N, E);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Function which returns
// the maximum number of
// isolated nodes
static int maxDisconnected(int N, int E)
{

    // Used nodes
    int curr = 1;

    // Remaining edges
    int rem = E;

    // Count nodes used
    while (rem > 0)
    {
        rem = rem - Math.min(
                    curr, rem);
        curr++;
    }

    // If given edges are non-zero
    if (curr > 1)
    {
        return N - curr;
    }
    else
    {
        return N;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given N and E
    int N = 5, E = 1;

    // Function call
    System.out.print(maxDisconnected(N, E));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function which returns
# the maximum number of
# isolated nodes
def maxDisconnected(N, E):

    # Used nodes
    curr = 1

    # Remaining edges
    rem = E

    # Count nodes used
    while (rem > 0):
        rem = rem - min(curr, rem)
        curr += 1

    # If given edges are non-zero
    if (curr > 1):
        return N - curr
    else:
        return N

# Driver Code
if __name__ == '__main__':

    # Given N and E
    N = 5
    E = 1

    # Function call
    print(maxDisconnected(N, E))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function which returns
// the maximum number of
// isolated nodes
static int maxDisconnected(int N,
                           int E)
{   
  // Used nodes
  int curr = 1;

  // Remaining edges
  int rem = E;

  // Count nodes used
  while (rem > 0)
  {
    rem = rem - Math.Min(curr, rem);
    curr++;
  }

  // If given edges are non-zero
  if (curr > 1)
  {
    return N - curr;
  }
  else
  {
    return N;
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given N and E
  int N = 5, E = 1;

  // Function call
  Console.Write(maxDisconnected(N, E));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of
// the above approach

// Function which returns
// the maximum number of
// isolated nodes
function maxDisconnected(N,E)
{
    // Used nodes
    let curr = 1;

    // Remaining edges
    let rem = E;

    // Count nodes used
    while (rem > 0)
    {
        rem = rem - Math.min(
                    curr, rem);
        curr++;
    }

    // If given edges are non-zero
    if (curr > 1)
    {
        return N - curr;
    }
    else
    {
        return N;
    }
}

// Driver Code

// Given N and E
let N = 5, E = 1;

// Function call
document.write(maxDisconnected(N, E));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(E)*
T5**辅助空间:** O(1)