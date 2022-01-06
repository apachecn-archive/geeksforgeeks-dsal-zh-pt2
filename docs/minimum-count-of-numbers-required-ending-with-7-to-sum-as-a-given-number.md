# 要求以 7 结尾的数字的最小计数加起来就是一个给定的数字

> 原文:[https://www . geeksforgeeks . org/最小数字计数-要求-以 7 的和作为给定数字结束/](https://www.geeksforgeeks.org/minimum-count-of-numbers-required-ending-with-7-to-sum-as-a-given-number/)

给定一个整数 **N** ，任务是找到以 **7** 结尾的最小个数，这样这些个数的和就是 **N** 。
**示例:**

> **输入:**N = 38
> T3】输出: 4
> 7 + 7 + 7 + 17
> 
> **输入:** N = 46
> **输出:** -1
> 46 不能表示为以 7 结尾的整数之和
> 。
> 
> **输入:**N = 215
> T3】输出: 5
> 7 + 7 + 7 + 7 + 187

**进场:**

*   这里的第一个观察是，每个大于或等于 **70** 的数总是可以写成所有以 **7** 结尾的数的和。例如 **82** 最后一位是 **2** ，所以至少需要 6 个以 7 结尾的数字(即 7 * 6 = 42)。可以创建一个数组 **hasharr[]** ，其中 **hasharr[i]** 表示最后一位数字为 **7** 所需的最小数字数，因此结果总和的最后一位数字为 **i** 。
*   如果数字小于 **70** ，则必须检查 **N** 是否小于以数字七 **7** 结尾的最小数字之和。如果是，则不能打印 **-1** ，否则大于或等于则有可能。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int TEN = 10;

// Function to return the count of
// minimum numbers ending with 7
// required such that the sum
// of these numbers is n
int minCount(int n)
{

    // hasharr[i] will store the minimum
    // numbers ending with 7 so that it
    // sums to number ending with digit i
    int hasharr[TEN] = { 10, 3, 6, 9, 2, 5, 8, 1, 4, 7 };

    // Its always possible to write numbers > 69
    // to write as numbers ending with 7
    if (n > 69)
        return hasharr[n % TEN];
    else {

        // If the number is atleast equal to the
        // sum of minimum numbers ending with 7
        if (n >= hasharr[n % TEN] * 7)
            return (hasharr[n % TEN]);
        else
            return -1;
    }
}

// Driver code
int main()
{
    int n = 38;

    cout << minCount(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

// Function to return the count of
// minimum numbers ending with 7
// required such that the sum
// of these numbers is n
static int minCount(int n)
{

    // hasharr[i] will store the minimum
    // numbers ending with 7 so that it
    // sums to number ending with digit i
    int[] hasharr = { 10, 3, 6, 9, 2,
                       5, 8, 1, 4, 7 };

    // Its always possible to write 
    // numbers > 69 to write as
    // numbers ending with 7
    if (n > 69)
        return hasharr[n % 10];
    else
    {

        // If the number is atleast equal
        // to the sum of minimum numbers
        // ending with 7
        if (n >= hasharr[n % 10] * 7)
            return (hasharr[n % 10]);
        else
            return -1;
    }
}

// Driver code
public static void main (String[] args)
{
    int n = 38;

    System.out.println(minCount(n));
}
}

// This code is contributed by spp____
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the count of
# minimum numbers ending with 7
# required such that the sum
# of these numbers is n
def minCount(n):

    # hasharr[i] will store the minimum
    # numbers ending with 7 so that it
    # sums to number ending with digit i
    hasharr = [ 10, 3, 6, 9, 2,
                 5, 8, 1, 4, 7 ]

    # Its always possible to write 
    # numbers > 69 to write as
    # numbers ending with 7
    if (n > 69):
        return hasharr[n % 10]
    else:

        # If the number is atleast equal
        # to the sum of minimum numbers
        # ending with 7
        if (n >= hasharr[n % 10] * 7):
            return hasharr[n % 10]
        else:
            return -1

# Driver code
n = 38;

print(minCount(n))

# This code is contributed by spp____
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to return the count of
// minimum numbers ending with 7
// required such that the sum
// of these numbers is n
static int minCount(int n)
{

    // hasharr[i] will store the minimum
    // numbers ending with 7 so that it
    // sums to number ending with digit i
    int[] hasharr = { 10, 3, 6, 9, 2,
                       5, 8, 1, 4, 7 };

    // Its always possible to write
    // numbers > 69 to write as
    // numbers ending with 7
    if (n > 69)
        return hasharr[n % 10];
    else
    {

        // If the number is atleast equal 
        // to the sum of minimum numbers
        // ending with 7
        if (n >= hasharr[n % 10] * 7)
            return (hasharr[n % 10]);
        else
            return -1;
    }
}

// Driver code
public static void Main (String[] args)
{
    int n = 38;

    Console.WriteLine(minCount(n));
}
}

// This code is contributed by spp____
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the count of
// minimum numbers ending with 7
// required such that the sum
// of these numbers is n
function minCount(n)
{

    // hasharr[i] will store the minimum
    // numbers ending with 7 so that it
    // sums to number ending with digit i
    let hasharr = [ 10, 3, 6, 9, 2,
                       5, 8, 1, 4, 7 ];

    // Its always possible to write
    // numbers > 69 to write as
    // numbers ending with 7
    if (n > 69)
        return hasharr[n % 10];
    else
    {

        // If the number is atleast equal
        // to the sum of minimum numbers
        // ending with 7
        if (n >= hasharr[n % 10] * 7)
            return (hasharr[n % 10]);
        else
            return -1;
    }
}

// Driver code

      let n = 38;

    document.write(minCount(n));

// This code is contributed by code_hunt.
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(1)

**辅助空间:** O(1)