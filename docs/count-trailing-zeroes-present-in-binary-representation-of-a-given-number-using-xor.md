# 使用异或运算对给定数字的二进制表示中出现的尾随零进行计数

> 原文:[https://www . geeksforgeeks . org/count-training-zero-present-in-binary-present-presented-of-to-number-use-xor/](https://www.geeksforgeeks.org/count-trailing-zeroes-present-in-binary-representation-of-a-given-number-using-xor/)

给定一个整数 **N** ，任务是在给定数字的二进制表示中找到尾随零的[数。](https://www.geeksforgeeks.org/count-number-of-trailing-zeros-in-binary-representation-of-a-number-using-bitset/)

**示例:**

> **输入:** N = 12
> **输出:** 2
> **解释:**
> 数字 13 的二进制表示为“1100”。
> 因此，12 中有两个尾随零。
> 
> **输入:** N = -56
> **输出:** 3
> **解释:**
> 数字-56 的二进制表示为“001000”。
> 因此，在-56 中有 3 个尾随零。

**方法:**按照步骤解决问题

*   其思想是利用这样的观察:在将 **N** 的 [XOR](https://www.geeksforgeeks.org/xor-of-two-binary-strings/) 与**n–1**进行计算后， **N** 的所有设置位都向左移动到最右边的设置位，即 LSB 设置位消失， **N** 的最右边的设置位成为**n ^(n–1)**的最左边的设置位。
*   打印数字**(n ^(n–1))**的[位数减 **1** 。](https://www.geeksforgeeks.org/count-total-bits-number/)

下面是上述方法的实现:

## C++

```
// C++ implementation
// of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print count of
// trailing zeroes present in
// binary representation of N
int countTrailingZeroes(int N)
{
    // Count set bits in (N ^ (N - 1))
    int res = log2(N ^ (N - 1));

    // If res < 0, return 0
    return res >= 0 ? res : 0;
}

// Driver Code
int main()
{
    int N = 12;

    // Function call to print the count
    // of trailing zeroes in the binary
    // representation of N
    cout << countTrailingZeroes(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of the above approach
import java.io.*;

class GFG {

    // Function to print count of
    // trailing zeroes present in
    // binary representation of N
    public static int countTrailingZeroes(int N)
    {
        // Stores XOR of N and (N-1)
        int res = N ^ (N - 1);

        // Return count of set bits in res
        return (int)(Math.log(temp)
                     / Math.log(2));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 12;

        // Function call to print the count
        // of trailing zeroes in the binary
        // representation of N
        System.out.println(
            countTrailingZeroes(N));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation
# of the above approach
from math import log2

# Function to print count of
# trailing zeroes present in
# binary representation of N
def countTrailingZeroes(N):

    # Count set bits in (N ^ (N - 1))
    res = int(log2(N ^ (N - 1)))

    # If res < 0, return 0
    return res if res >= 0 else 0

# Driver Code
if __name__ == '__main__':
    N = 12

    # Function call to print the count
    # of trailing zeroes in the binary
    # representation of N
    print (countTrailingZeroes(N))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# implementation
// of the above approach
using System;
public class GFG{

  // Function to print count of
  // trailing zeroes present in
  // binary representation of N
  public static int countTrailingZeroes(int N)
  {
    // Stores XOR of N and (N-1)
    int res = (int)Math.Log(N ^ (N - 1), 2.0);

    // Return count of set bits in res
    if(res >= 0)
      return res;
    else
      return 0;
  }

  // Driver Code
  static public void Main ()
  {

    int N = 12;

    // Function call to print the count
    // of trailing zeroes in the binary
    // representation of N
    Console.WriteLine(
      countTrailingZeroes(N));
  }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Javascript implementation
// of the above approach

// Function to print count of
// trailing zeroes present in
// binary representation of N
function countTrailingZeroes(N)
{

    // Count set bits in (N ^ (N - 1))
    let res = parseInt(Math.log(N ^ (N - 1)) /
                       Math.log(2));

    // If res < 0, return 0
    return res >= 0 ? res : 0;
}

// Driver Code
let N = 12;

// Function call to print the count
// of trailing zeroes in the binary
// representation of N
document.write(countTrailingZeroes(N));

// This code is contributed by souravmahato348 

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*