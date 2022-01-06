# 生成每行每列乘积为 1 或-1 的矩阵的方式数

> 原文:[https://www . geeksforgeeks . org/生成每行每列乘积为 1 或-1 的矩阵的方法计数/](https://www.geeksforgeeks.org/count-of-ways-to-generate-a-matrix-with-product-of-each-row-and-column-as-1-or-1/)

给定两个整数 **N** 和 **M** ，任务是找出形成大小矩阵 **N * M** 的方法数，只由 1 或-1 组成，这样每行每列的整数乘积等于 1 或-1。

**示例:**

> **输入:** N = 2，M = 2
> **输出:** 4
> **解释:**
> 获取每行和每列乘积的可能方式为 1，而
> {{1，1}、{1，1}}和{-1，-1}、{-1，-1}}
> 获取每行和每列乘积的可能方式为-1，而
> {{1，-1}、{-1，1}}和 途径数= 2 + 2 = 4
> **输入:** N = 3，M = 3
> **输出:** 32
> **说明:**
> 获取产品 as 1 的途径有 16 种，获取产品 as -1 的途径有 16 种。
> 因此，路数= 16 + 16 = 32

**天真的方法:**
解决这个问题最简单的方法是生成所有可能的大小矩阵 **N * M** 并且对于它们中的每一个，计算所有行和列的乘积并且检查它是 1 还是-1。
***时间复杂度:**O(2<sup>N * M</sup>)*
***辅助空间:** O(M*N)*
**高效途径:**
假设，先将 **N-1** 行和先将 **M-1** 列用 1 或-1 填充。现在，每行到 **N-1** 行，每列到 **M-1** 列的乘积要么是 **1** 要么是 **-1** 。总共有 **2** <sup>(N-1) * (M-1)</sup> 种方式组成一个大小为 **(N-1)*(M-1)** 的矩阵，用 1 或-1 填充。根据所需的 N 行和 M 列的乘积，最后一行和最后一列可以相应地填充。
按照步骤解决问题:

*   如果 **N + M** 为**偶数**，
    得到乘积的可能矩阵数为 1 = 2**<sup>(N-1)*(M-1)</sup>**
    得到乘积的可能矩阵数为-1 = 2**<sup>(N-1)*(M-1)</sup>**
*   如果 **N + M** 为**奇数**，
    得到乘积的可能矩阵数为 1 = 2**<sup>(N-1)*(M-1)</sup>**
    得到乘积的可能矩阵数为-1 = 0

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include
using namespace std;

// Function to return the
// number of possible ways
void Solve(int N, int M)
{

    int temp = (N - 1) * (M - 1);
    int ans = pow(2, temp);

    // Check if product can be -1
    if ((N + M) % 2 != 0)
        cout << ans;
    else
        cout << 2 * ans;

    cout << endl;
}
// Driver Code
int main()
{
    int N = 3;
    int M = 3;

    Solve(N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

class GFG{

// Function to return the
// number of possible ways
static void Solve(int N, int M)
{
    int temp = (N - 1) * (M - 1);
    int ans = (int)(Math.pow(2, temp));

    // Check if product can be -1
    if ((N + M) % 2 != 0)
        System.out.print(ans);
    else
        System.out.print(2 * ans);
}

// Driver code
public static void main (String[] args)
{
    int N = 3;
    int M = 3;

    Solve(N, M);
}
}

// This code is contributed by Shubham Prakash
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
# Function to return
# possible number of ways
def Solve(N, M):
  temp = (N - 1) * (M - 1)
  ans = pow(2, temp)

  # Check if product can be -1
  if ((N + M) % 2 != 0):
    print(ans)
    else:
      print(2 * ans)

      # driver code
      if __name__ == '__main__':
        N, M = 3, 3
        Solve(N, M)

# This code is contributed by Sri_srajit
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to return the
// number of possible ways
static void Solve(int N, int M)
{
    int temp = (N - 1) * (M - 1);
    int ans = (int)(Math.Pow(2, temp));

    // Check if product can be -1
    if ((N + M) % 2 != 0)
        Console.Write(ans);
    else
        Console.Write(2 * ans);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 3;
    int M = 3;

    Solve(N, M);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

// Function to return the
// number of possible ways
function Solve(N, M)
{
    let temp = (N - 1) * (M - 1);
    let ans = (Math.pow(2, temp));

    // Check if product can be -1
    if ((N + M) % 2 != 0)
        document.write(ans);
    else
        document.write(2 * ans);
}

// Driver Code

       let N = 3;
    let M = 3;

    Solve(N, M);

</script>
```

**Output:** 

```
32
```

***时间复杂度:** O(log(N*M))*
***辅助空间:** O(1)*