# 计算第 N 次幂的奇数和偶数二项式系数

> 原文:[https://www . geeksforgeeks . org/count-n 次方的奇数和偶数二项式系数/](https://www.geeksforgeeks.org/count-odd-and-even-binomial-coefficients-of-n-th-power/)

给定一个整数 **N** ，任务是统计偶数和奇数的[二项式系数](https://en.wikipedia.org/wiki/Binomial_coefficient)直到**N**T6 次方。

**示例:**

> **输入:** N = 4
> **输出:**
> 奇数:2
> 偶数:3
> **说明:**
> 二项式系数如下:
> <sup>4</sup> C <sub>0</sub> = 1、<sup>4</sup>C<sub>1</sub>= 4<sub>T21】、 <sup>4</sup> C <sub>2 【T25
> 因此，可以观察到恰好存在 2 个奇数和 3 个偶数二项式系数。</sub></sub>
> 
> **输入:** N = 5
> **输出:**
> 奇数:4
> 偶数:2
> **说明:**
> 二项式系数如下:
> <sup>5</sup> C <sub>0</sub> = 1、 <sup>5</sup> C <sub>1</sub> = 5、 <sup>5</sup> C <sub>2</sub> = 10、 <sup>因此，有 4 个奇数系数和 2 个偶数系数。</sup>

**解决方法:**解决这个问题的思路是使用[位操纵](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)。找到给定整数 **N** 中的**设定位**。**奇数二项式系数**的计数等于 N 中设定位的 **2 ^计数。类似地，**偶数二项式系数**的计数等于**(n+1–2 个设置位的^计数，单位为 N)** 。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
#include <math.h>
using namespace std;

// Function to count set bits in
// binary representation of number N
int countSetBits(int N)
{
    int count = 0;

    // Count set bits in N
    while (N) {

        N = N & (N - 1);
        count++;
    }

    // Return the final count
    return count;
}

// Driver Code
int main()
{
    int N = 4;

    int bits = countSetBits(N);

    // Print odd Binomial coefficients
    cout << "Odd "
         << ": " << pow(2, bits) << "\n";

    // Print even Binomial coefficients
    cout << "Even "
         << ": " << N + 1 - pow(2, bits)
         << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count set bits in
// binary representation of number N
static int countSetBits(int N)
{
    int count = 0;

    // Count set bits in N
    while (N != 0)
    {

        N = N & (N - 1);
        count++;
    }

    // Return the final count
    return count;
}

// Driver code
public static void main(String[] args)
{
    int N = 4;

    int bits = countSetBits(N);

    // Print odd Binomial coefficients
    System.out.println("Odd " + ": " +
               (int)(Math.pow(2, bits)));

    // Print even Binomial coefficients
    System.out.println("Even " + ": " +
               (N + 1 - (int)(Math.pow(2, bits))));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count set bits in
# binary representation of number N
def countSetBits(N: int) -> int:

    count = 0

    # Count set bits in N
    while (N):
        N = N & (N - 1)
        count += 1

    # Return the final count
    return count

# Driver Code
if __name__ == "__main__":

    N = 4

    bits = countSetBits(N)

    # Print odd Binomial coefficients
    print("Odd : {}".format(pow(2, bits)))

    # Print even Binomial coefficients
    print("Even : {}".format(N + 1 - pow(2, bits)))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count set bits in
// binary representation of number N
static int countSetBits(int N)
{
    int count = 0;

    // Count set bits in N
    while (N != 0)
    {
        N = N & (N - 1);
        count++;
    }

    // Return the final count
    return count;
}

// Driver Code
public static void Main()
{
    int N = 4;
    int bits = countSetBits(N);

    // Print odd Binomial coefficients
    Console.WriteLine("Odd " + ": " +
                     (int)(Math.Pow(2, bits)));

    // Print even Binomial coefficients
    Console.WriteLine("Even " + ": " +
                     (N + 1 - (int)(Math.Pow(2, bits))));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count set bits in
// binary representation of number N
function countSetBits(N)
{
    let count = 0;

    // Count set bits in N
    while (N != 0)
    {
        N = N & (N - 1);
        count++;
    }

    // Return the final count
    return count;
}

// Driver Code
let N = 4;

let bits = countSetBits(N);

// Print odd Binomial coefficients
document.write("Odd " + ": " +
              (Math.pow(2, bits)) + "<br/>");

// Print even Binomial coefficients
document.write("Even " + ": " +
              (N + 1 - (Math.pow(2, bits))));

// This code is contributed by splevel62

</script>
```

**Output:** 

```
Odd : 2
Even : 3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)