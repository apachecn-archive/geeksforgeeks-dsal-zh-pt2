# 从 1 到 N 最大化所有可能对的 GCD

> 原文:[https://www . geeksforgeeks . org/maximize-gcd-of-all-可能性-pairs-from-1-n/](https://www.geeksforgeeks.org/maximize-gcd-of-all-possible-pairs-from-1-to-n/)

给定一个整数 **N** (？2)，任务是通过范围**【1，N】**中的整数找到所有可能的对中的最大 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。

**示例:**

> **输入:** N = 5
> **输出:** 2
> **解释:**
> GCD(1，2) : 1
> GCD(1，3) : 1
> GCD(1，4) : 1
> GCD(1，5) : 1
> GCD(2，3) : 1
> GCD(2，4):**2**T16】GCD(2，5) : 1
> 
> **输入:** N = 6
> **输出:** 3
> **说明:**对(3，6)的 GCD 最大。

**天真法:**
解决问题最简单的方法是[从**【1，N】**生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，计算每对的 **GCD** 。最后，打印获得的最大 GCD。
***时间复杂度:**O(N<sup>2</sup>logN)*
***辅助空间:** O(1)*

**高效方法:**
按照以下步骤解决问题:

*   由于所有对都是不同的，因此，对于任何具有 GCD **g** 的对 **{a，b}** ，无论是 **a** 还是 **b** 都大于 **g** 。
*   考虑到 **b** 是更大的数字， **b？2g** ，因为 **2g** 是大于它的 **g** 的最小倍数。
*   既然 **b** 不能超过 **N** ，和 **2g？N** 。
*   因此， **g？楼层(n/2)** 。
*   因此，当配对选择为 **(floor(n/2)，2*floor(n/2))时，可获得的最大 GCD 为 floor(n/2)。**

> **说明:**
> N = 6
> 最大 GCD = 6/2 = 3，出现于对(3，6)

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the approach
#include <bits/stdc++.h>
using namespace std;

// Function to obtain the maximum
// gcd of all pairs from 1 to n
void find(int n)
{
    // Print the answer
    cout << n / 2 << endl;
}

// Driver code
int main()
{
    int n = 5;
    // Function call
    find(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the approach
class GFG{

// Function to obtain the maximum
// gcd of all pairs from 1 to n
static void find(int n)
{
    // Print the answer
    System.out.println(n / 2);
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    // Function call
    find(n);
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program to implement
# the approach

# Function to obtain the maximum
# gcd of all pairs from 1 to n
def find(n):

    # Print the answer
    print(n // 2)

# Driver Code
if __name__ == '__main__':

    # Given n
    n = 5

    # Function call
    find(n)

# This code is contributed by Shivam Singh
```

## C#

```
// C# Program to implement
// the approach
using System;
class GFG{

// Function to obtain the maximum
// gcd of all pairs from 1 to n
static void find(int n)
{
    // Print the answer
    Console.Write(n / 2);
}

// Driver code
public static void Main(string[] args)
{
    int n = 5;
    // Function call
    find(n);
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program to implement
// the approach

// Function to obtain the maximum
// gcd of all pairs from 1 to n
function find(n)
{

    // Print the answer
    document.write(parseInt(n / 2, 10) + "</br>");
}

// Driver code
let n = 5;

// Function call
find(n);

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*