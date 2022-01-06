# 找到权重相同的最接近的整数

> 原文:[https://www . geesforgeks . org/find-最接近的同权整数/](https://www.geeksforgeeks.org/find-closest-integer-with-the-same-weight/)

给定一个正整数 **X** 任务是找到一个整数 **Y** 这样:

1.  设定位的计数为 **Y** 等于 **X** 中设定位的计数。
2.  **X！= Y** 。
3.  **| X–Y |**为最小值。

**例:**

> **输入:** X = 92
> **输出:** 90
> 90 是与 92 最接近的数字，具有
> 相等的设定位数。
> **输入:** X = 17
> **输出:** 18

**方法:**一点数学就可以引导我们走向求解方法。由于两个数字中的位数必须相同，如果一个设置的位被翻转，那么一个未设置的位也必须被翻转。
现在问题简化为选择两位进行翻转。假设索引 **i** 处的一个位被翻转，而索引 **j** (j < i)处的另一个位来自 LSB(最低有效位)。那么原整数与新整数之差的绝对值就是**2<sup>I</sup>–2<sup>j</sup>**。为了尽量减少这种情况， **i** 必须尽可能小， **j** 必须尽可能靠近 **i** 。
由于设置位的数量必须相等，因此索引 **i** 处的位必须不同于索引 **j** 处的位。这意味着最小的位可以是与 LSB 不同的最右边的位，而 **j** 必须是下一个位。总之，正确的方法是交换两个不同的最右边的连续位。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int NumUnsignBits = 64;

// Function to return the number
// closest to x which has equal
// number of set bits as x
unsigned long findNum(unsigned long x)
{
    // Loop for each bit in x and
    // compare with the next bit
    for (int i = 0; i < NumUnsignBits - 1; i++) {
        if (((x >> i) & 1) != ((x >> (i + 1)) & 1)) {
            x ^= (1 << i) | (1 << (i + 1));
            return x;
        }
    }
}

// Driver code
int main()
{
    int n = 92;

    cout << findNum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int NumUnsignBits = 64;

// Function to return the number
// closest to x which has equal
// number of set bits as x
static long findNum(long x)
{
    // Loop for each bit in x and
    // compare with the next bit
    for (int i = 0; i < NumUnsignBits - 1; i++)
    {
        if (((x >> i) & 1) != ((x >> (i + 1)) & 1))
        {
            x ^= (1 << i) | (1 << (i + 1));
            return x;
        }
    }
    return Long.MIN_VALUE;
}

// Driver code
public static void main(String[] args)
{
    int n = 92;

    System.out.println(findNum(n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
NumUnsignBits = 64;

# Function to return the number
# closest to x which has equal
# number of set bits as x
def findNum(x) :

    # Loop for each bit in x and
    # compare with the next bit
    for i in range(NumUnsignBits - 1) :
        if (((x >> i) & 1) != ((x >> (i + 1)) & 1)) :
            x ^= (1 << i) | (1 << (i + 1));
            return x;

# Driver code
if __name__ == "__main__" :
    n = 92;
    print(findNum(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int NumUnsignBits = 64;

// Function to return the number
// closest to x which has equal
// number of set bits as x
static long findNum(long x)
{
    // Loop for each bit in x and
    // compare with the next bit
    for (int i = 0; i < NumUnsignBits - 1; i++)
    {
        if (((x >> i) & 1) != ((x >> (i + 1)) & 1))
        {
            x ^= (1 << i) | (1 << (i + 1));
            return x;
        }
    }
    return long.MinValue;
}

// Driver code
public static void Main(String[] args)
{
    int n = 92;

    Console.WriteLine(findNum(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let NumUnsignBits = 64;

    // Function to return the number
    // closest to x which has equal
    // number of set bits as x
    function findNum(x)
    {
        // Loop for each bit in x and
        // compare with the next bit
        for (let i = 0; i < NumUnsignBits - 1; i++)
        {
            if (((x >> i) & 1) != ((x >> (i + 1)) & 1))
            {
                x ^= (1 << i) | (1 << (i + 1));
                return x;
            }
        }
        return Number.MIN_VALUE;
    }

    let n = 92;

    document.write(findNum(n));

</script>
```

**Output:** 

```
90
```

**时间复杂度:** O(logn)

**辅助空间:** O(1)