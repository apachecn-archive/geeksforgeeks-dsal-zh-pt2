# 长度为 N 的非递减数组的计数，其值在范围 L 至 R 内

> 原文:[https://www . geeksforgeeks . org/count-of-non-reduced-length-n-formed-with-range-l-to-r/](https://www.geeksforgeeks.org/count-of-non-decreasing-arrays-of-length-n-formed-with-values-in-range-l-to-r/)

给定整数 **N** 、 **L** 和 **R** ，任务是计算长度为 N 的非递减数组的数量，数组的值在允许重复的范围【L，R】内。
**举例:**

> **输入:** N = 4，L = 4，R = 6
> **输出:** 5
> 所有可能的数组为{4，4，4，6}，{4，4，5，6}，{4，5，5，6}，{4，5，6，6，6}和{4，6，6，6，6}。
> **输入:** N = 2，L = 5，R = 2
> **输出:** 0
> 不存在 L>R
> 这样的组合

**进场:**

*   既然知道阵列中最小数量为 **L** ，最大数量为 **R** 。
*   如果剩余的**(N–2)**指数用 **L** 填充，则得到**最小可能和**，如果剩余的 **(N-2)** 指数用 **R** 填充，则得到**最大可能和**。
*   可以得出这样的结论:存在一个数的组合，其结果是最小可能和最大可能和之间的和。
*   因此，不同总数的总和可以通过下式计算:
    **[(N–2)* R –( N–2)* L]+1 =(N–2)*(R–L)+1**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of different arrays
int countSum(int N, int L, int R)
{

    // No such combination exists
    if (L > R) {
        return 0;
    }

    // Arrays formed with single elements
    if (N == 1) {
        return R - L + 1;
    }

    if (N > 1) {
        return (N - 2) * (R - L) + 1;
    }
}

// Driver code
int main()
{
    int N = 4, L = 4, R = 6;

    cout << countSum(N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of different arrays
static int countSum(int N, int L, int R)
{

    // No such combination exists
    if (L > R)
    {
        return 0;
    }

    // Arrays formed with single elements
    if (N == 1)
    {
        return R - L + 1;
    }

    if (N > 1)
    {
        return (N - 2) * (R - L) + 1;
    }
    return 0;
}

// Driver code
public static void main(String[] args)
{
    int N = 4, L = 4, R = 6;

    System.out.print(countSum(N, L, R));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of different arrays
def countSum(N, L, R):

    # No such combination exists
    if (L > R):
        return 0;

    # Arrays formed with single elements
    if (N == 1):
        return R - L + 1;
    if (N > 1):
        return (N - 2) * (R - L) + 1;

    return 0;

# Driver code
if __name__ == '__main__':
    N, L, R = 4, 4, 6;

    print(countSum(N, L, R));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of different arrays
static int countSum(int N, int L, int R)
{

    // No such combination exists
    if (L > R)
    {
        return 0;
    }

    // Arrays formed with single elements
    if (N == 1)
    {
        return R - L + 1;
    }

    if (N > 1)
    {
        return (N - 2) * (R - L) + 1;
    }
    return 0;
}

// Driver code
public static void Main(String[] args)
{
    int N = 4, L = 4, R = 6;

    Console.Write(countSum(N, L, R));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of different arrays
function countSum(N, L, R)
{

    // No such combination exists
    if (L > R) {
        return 0;
    }

    // Arrays formed with single elements
    if (N == 1) {
        return R - L + 1;
    }

    if (N > 1) {
        return (N - 2) * (R - L) + 1;
    }
}

// Driver code
var N = 4, L = 4, R = 6;
document.write( countSum(N, L, R));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(1)