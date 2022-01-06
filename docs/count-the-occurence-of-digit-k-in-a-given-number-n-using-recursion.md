# 使用递归计算给定数字 N 中数字 K 的出现次数

> 原文:[https://www . geeksforgeeks . org/count-给定数字中出现数字 k-n-使用递归/](https://www.geeksforgeeks.org/count-the-occurence-of-digit-k-in-a-given-number-n-using-recursion/)

给定一个大于 0 的整数 **N** ，任务是找出给定数字 N 中出现的数字**K**
T5】的出现位置【例:

> **输入:** N = 10000，K = 0
> **输出:** 4
> **说明:**
> 10000 中‘0’位出现次数为 4。
> **输入:** N = 51435，K = 5
> **输出:** 2
> **说明:**
> 51435 中‘5’位的出现次数为 2

**方法:**思路是用[递归](http://www.geeksforgeeks.org/recursion/)提取每一步数字的最低有效位，检查提取的位是否等于给定位 **K** 。最后，通过计算该数除以 10 的整数部分，递归检查该数的下一位数。
以下是上述方法的实现:

## C++

```
// C++ implementation to count
// the occurrence of a digit in
// number using Recursion

#include <bits/stdc++.h>

using namespace std;

// Function to count the digit K
// in the given number N
int countdigits(int n, int k)
{
    if (n == 0)
        return 0;

    // Extracting least
    // significant digit
    int digit = n % 10;
    if (digit == k)
        return 1 + countdigits(n / 10, k);

    return countdigits(n / 10, k);
}

// Driver Code
int main()
{
    int n = 1000;
    int k = 0;

    cout << countdigits(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// the occurrence of a digit in
// number using Recursion

import java.util.*;

class GFG {

    // Function to count the digit K
    // in the given number N
    static double countdigits(int n, int k)
    {
        if (n == 0)
            return 0;

        // Extracting least
        // significant digit
        int digit = n % 10;
        if (digit == k)
            return 1 + countdigits(n / 10, k);

        return countdigits(n / 10, k);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 1000;
        int k = 0;
        System.out.println(countdigits(n, k));
    }
}
```

## 蟒蛇 3

```
# Python implementation to count
# the occurrence of a digit in
# number using Recursion

# Function to count the digit K
# in the given number N
def countdigits(n, k):
    if n == 0:
        return 0

    # Extracting least
    # significant digit
    digit = n % 10

    if digit == k:
        return 1 + countdigits(n / 10, k)

    return countdigits(n / 10, k)

# Driver Code
if __name__ == "__main__":
    n = 1000;
    k = 0;
    print(countdigits(n, k))
```

## C#

```
// C# implementation to count
// the occurrence of a digit in
// number using Recursion

using System;

class GFG {

    // Function to count the digit K
    // in the given number N
    static double countdigits(int n,
                              int k)
    {
        if (n == 0)
            return 0;

        // Extracting least
        // significant digit
        int digit = n % 10;
        if (digit == k)
            return 1 +
             countdigits(n / 10, k);

        return countdigits(n / 10, k);
    }

    // Driver Code
    static public void Main()
    {
        int n = 1000;
        int k = 0;
        Console.WriteLine(countdigits(n, k));
    }
}
```

## java 描述语言

```
<script>

// Javascript implementation to count
// the occurrence of a digit in
// number using Recursion

// Function to count the digit K
// in the given number N
function countdigits(n, k)
{
    if (n == 0)
        return 0;

    // Extracting least
    // significant digit
    var digit = n % 10;
    if (digit == k)
        return 1 + countdigits(n / 10, k);

    return countdigits(n / 10, k);
}

// Driver Code
var n = 1000;
var k = 0;
document.write( countdigits(n, k));

</script>
```

**Output:** 

```
3
```

时间复杂度:O(log <sub>10</sub> n)

辅助空间:0(对数 <sub>10</sub> n)