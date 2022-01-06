# 通过交换配对的相同位置的位来最小化前 N-1 个自然数的乘积

> 原文:[https://www . geesforgeks . org/通过交换相同位置的成对位来最小化第一个 n-1 个自然数的乘积/](https://www.geeksforgeeks.org/minimize-product-of-first-n-1-natural-numbers-by-swapping-same-positioned-bits-of-pairs/)

给定一个整数 **N** ，任务是通过任意次数的任意两个数的任意**I**<sup>位的交换，求第一个**N–1**自然数的最小正积，即**【1，(N–1)】**。</sup>

**注:** N 永远是 2 的[完美幂。由于产品可能很大，打印答案模 **10 <sup>9</sup> + 7** 。](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

**示例:**

> **输入:** N = 4
> **输出:** 6
> **解释:**
> 不需要交换位。因此，最小乘积为 1*2*3 = 6。
> 
> **输入:** N = 8
> **输出:** 1512
> **解释:**
> 让数组 arr[]将从 1 到 N 的所有值存储为{1，2，3，4，5，6，7}
> 遵循以下步骤:
> 步骤 1:在元素 2 = (0010)和 5 = (0101)中，交换第 0 位和第 1 位。因此，用 1 代替 2，用 6 代替 5。arr[] = {1，1，3，4，6，6，7}。
> 步骤 2:在元素 3 = (0011)和 4 = (0100)中，交换第 1 位。因此，用 1 代替 3，用 6 代替 4。arr[] = {1，1，1，6，6，6，7}。
> 因此，最小乘积= 1*1*1*6*6*6*7 = 1512 % 1e9+7 = 1512。

**进场:**思路是做一些观察。例如，如果 **N** = **8** 和 **arr[] = {1，2，3，4，5，6，7}** ，观察产品最小必须有三个六，即必须有一个值为**(N–2)**的元素，出现频率为**(1+(N–4)/2)**，必须有三个一，即必须有 **(1 最后将当前乘积乘以**(N-1)**。因此，公式变为:**

> **任意值 N =((N–1)*(N–2)<sup>(N–4)/2+1</sup>)的最小乘积% 1e9 + 7**

按照以下步骤解决问题:

1.  将**和**初始化为 **1** 。
2.  迭代范围**【0，1+(N–4)/2】**。
3.  在每次遍历中，将 **ans** 乘以**N–2**，并将 **ans** 更新为 **ans mod 1e9+7** 。
4.  完成上述步骤后，打印**ans *(N–1)mod 1e 9+7**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

int mod = 1e9 + 7;

// Function to find the minimum product
// of 1 to N - 1 after performing the
// given operations
void minProduct(int n)
{
    // Initialize ans with 1
    int ans = 1;

    // Multiply ans with N-2
    // ((N - 4)/2) times
    for (int i = 1;
         i <= (n - 4) / 2; i++) {
        ans = (1LL * ans
               * (n - 2))
              % mod;
    }

    // Multiply ans with N - 1
    // and N - 2 once
    ans = (1LL * ans
           * (n - 2) * (n - 1))
          % mod;

    // Print ans
    cout << ans << endl;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 8;

    // Function Call
    minProduct(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static int mod = (int)1e9 + 7;

// Function to find the
// minimum product of 1
// to N - 1 after performing
// the given operations
static void minProduct(int n)
{
  // Initialize ans with 1
  int ans = 1;

  // Multiply ans with N-2
  // ((N - 4)/2) times
  for (int i = 1;
           i <= (n - 4) / 2; i++)
  {
    ans = (int)(1L * ans *
               (n - 2)) % mod;
  }

  // Multiply ans with N - 1
  // and N - 2 once
  ans = (int)(1L * ans *
             (n - 2) * (n - 1)) % mod;

  // Print ans
  System.out.print(ans + "\n");
}

// Driver Code
public static void main(String[] args)
{
  // Given Number N
  int N = 8;

  // Function Call
  minProduct(N);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
mod = 1e9 + 7

# Function to find the minimum product
# of 1 to N - 1 after performing the
# given operations
def minProduct(n):

    # Initialize ans with 1
    ans = 1

    # Multiply ans with N-2
    # ((N - 4)/2) times
    for i in range(1, (n - 4) // 2 + 1):
        ans = (ans * (n - 2)) % mod

    # Multiply ans with N - 1
    # and N - 2 once
    ans = (ans * (n - 2) * (n - 1)) % mod

    # Print ans
    print(int(ans))

# Driver Code
if __name__ == '__main__':

    # Given number N
    N = 8

    # Function call
    minProduct(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

static int mod = (int)1e9 + 7;

// Function to find the
// minimum product of 1
// to N - 1 after performing
// the given operations
static void minProduct(int n)
{
  // Initialize ans with 1
  int ans = 1;

  // Multiply ans with N-2
  // ((N - 4)/2) times
  for (int i = 1;
           i <= (n - 4) / 2; i++)
  {
    ans = (int)(1L * ans *
               (n - 2)) % mod;
  }

  // Multiply ans with N - 1
  // and N - 2 once
  ans = (int)(1L * ans *
             (n - 2) *
             (n - 1)) % mod;

  // Print ans
  Console.Write(ans + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  // Given Number N
  int N = 8;

  // Function Call
  minProduct(N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

let mod = 1e9 + 7;

// Function to find the minimum product
// of 1 to N - 1 after performing the
// given operations
function minProduct(n)
{
    // Initialize ans with 1
    let ans = 1;

    // Multiply ans with N-2
    // ((N - 4)/2) times
    for (let i = 1; i <= Math.floor((n - 4) / 2); i++)
    {
        ans = (1 * ans * (n - 2)) % mod;
    }

    // Multiply ans with N - 1
    // and N - 2 once
    ans = (1 * ans * (n - 2) * (n - 1)) % mod;

    // Print ans
    document.write(ans + "<br>");
}

// Driver Code

    // Given Number N
    let N = 8;

    // Function Call
    minProduct(N);

// This code is contributed by Manoj.
</script>
```

**Output**

```
1512
```

***时间复杂度:** O(N)，其中 N 是给定的整数。*
***辅助空间:** O(1)*