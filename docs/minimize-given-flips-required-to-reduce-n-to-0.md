# 最小化将 N 减少到 0 所需的给定翻转次数

> 原文:[https://www . geesforgeks . org/minimum-给定翻转-需要将 n 减少到 0/](https://www.geeksforgeeks.org/minimize-given-flips-required-to-reduce-n-to-0/)

给定一个整数 **N** ，任务是通过执行以下操作最少次数将 **N** 的值减少到 **0** :

*   翻转 **N** 二进制表示中最右边的 **(0 <sup>第</sup> )** 位。
*   如果设置了**(I–1)**位，则翻转**I**位，并清除从**(I–2)**到**0**位的所有位。

**示例:**

> **输入:** N = 3
> **输出:** 2
> **说明:**
> N (= 3)的二进制表示为 11
> 由于设置了 N(= 3)的二进制表示中的 0 <sup>第</sup>位，翻转 N 的二进制表示的 1 <sup>第</sup>位将 N 修改为 1(01)。
> 翻转 N(=1)的二进制表示的最右位，将 N 修改为 0(00)。
> 因此，要求的输出为 2
> 
> **输入:**N = 4
> T3】输出: 7

**方法:**根据以下观察结果可以解决问题:

> 1-> 0 = > 1
> 10->11->T1】01->00 =>2+1 = 3
> 100->101->111->110->T4】010->……=>4+2+1 = 7
> 1000->1001-> ->……=>8+7 = 15
> 因此，对于 N = 2 <sup>N</sup> 合计(2<sup>(N+1)</sup>–1)所需操作。
> 如果 N 不是 2 的幂，则递推关系为:
> MinOp(N)= MinOp((1<<cntBit)–1)–MinOp(N –( 1<<(cntBit–1)))
> cntBit = N 的二进制表示中的比特总数。
> MinOp(N)表示将 N 减少到 0 所需的最小操作数。

按照以下步骤解决问题:

*   使用**日志 <sub>2</sub> (N) + 1** 计算 **N** 二进制表示的位数。
*   利用上述递推关系，计算将 **N** 减少到 **0** 所需的最小运算次数。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of
// operations required to Reduce N to 0
int MinOp(int N)
{

    if (N <= 1)
        return N;

    // Stores count of
    // bits in N
    int bit = log2(N) + 1;

    // Recurrence relation
    return ((1 << bit) - 1)
           - MinOp(N - (1 << (bit - 1)));
}

// Driver Code
int main()
{

    int N = 4;
    cout << MinOp(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the minimum count of
// operations required to Reduce N to 0
public static int MinOp(int N)
{
    if (N <= 1)
        return N;

    // Stores count of
    // bits in N
    int bit = (int)(Math.log(N) /
                    Math.log(2)) + 1;

    // Recurrence relation
    return ((1 << bit) - 1) - MinOp(
        N - (1 << (bit - 1)));
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    System.out.println(MinOp(N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the minimum count of
# operations required to Reduce N to 0
import math
def MinOp(N):
    if (N <= 1):
        return N;

    # Stores count of
    # bits in N
    bit = (int)(math.log(N) / math.log(2)) + 1;

    # Recurrence relation
    return ((1 << bit) - 1) - MinOp(N - (1 << (bit - 1)));

# Driver code
if __name__ == '__main__':
    N = 4;

    print(MinOp(N));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the minimum count of
// operations required to Reduce N to 0
public static int MinOp(int N)
{
    if (N <= 1)
        return N;

    // Stores count of
    // bits in N
    int bit = (int)(Math.Log(N) /
                    Math.Log(2)) + 1;

    // Recurrence relation
    return ((1 << bit) - 1) - MinOp(
        N - (1 << (bit - 1)));
}

// Driver code
public static void Main()
{
    int N = 4;

    Console.WriteLine(MinOp(N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to find the minimum count of
// operations required to Reduce N to 0
function MinOp(N)
{
    if (N <= 1)
        return N;

    // Stores count of
    // bits in N
    let bit = (Math.log(N) /
                    Math.log(2)) + 1;

    // Recurrence relation
    return ((1 << bit) - 1) - MinOp(
        N - (1 << (bit - 1)));
}

// Driver code
    let N = 4;
    document.write(MinOp(N));

    // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*