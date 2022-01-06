# 对数组中的对进行计数，使其乘积除以 2 的最高幂为 1

> 原文:[https://www . geeksforgeeks . org/数组中的对数，即 2 的最高次方除以其乘积为 1/](https://www.geeksforgeeks.org/count-of-pairs-in-an-array-such-that-the-highest-power-of-2-that-divides-their-product-is-1/)

给定一个正整数数组**arr[]****N**。任务是找到配对的计数 **(arr[i]，arr[j])** ，这样 **2** 除 **arr[i] * arr[j]** 的最大功率为 **1** 。
**示例:**

> **输入:** arr[] = {3，5，2，8}
> **输出:** 3
> (3，2)、(5，2)和(3，5)是唯一有效的对。
> 因为 2 除以 3 * 2 = 6 的幂是 1，
> 5 * 2 = 10 是 1，3 * 5 = 15 是 0。
> **输入:** arr[] = {4，2，7，11，14，15，18}
> **输出:** 12

**趋近:**由于 **2** 除**arr【I】* arr【j】**的最大功率在最大 **1** 处，这意味着如果 **P** 是乘积，那么它必须要么是**奇数**要么是 **2** 是 **P** 的唯一偶数因子。
表示**arr【I】**和**arr【j】**都必须是**奇数**或者恰好其中一个是**偶数****2**是这个数唯一的偶数因子。
如果**奇数**是奇数的计数而**偶数**是偶数的计数，使得 **2** 是该数的唯一偶数因子，那么答案将是**奇数*偶数+奇数*(奇数–1)/2**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of valid pairs
int cntPairs(int a[], int n)
{

    // To store the count of odd numbers and
    // the count of even numbers such that 2
    // is the only even factor of that number
    int odd = 0, even = 0;

    for (int i = 0; i < n; i++) {

        // If current number is odd
        if (a[i] % 2 == 1)
            odd++;

        // If current number is even and 2
        // is the only even factor of it
        else if ((a[i] / 2) % 2 == 1)
            even++;
    }

    // Calculate total number of valid pairs
    int ans = odd * even + (odd * (odd - 1)) / 2;

    return ans;
}

// Driver code
int main()
{

    int a[] = { 4, 2, 7, 11, 14, 15, 18 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << cntPairs(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of valid pairs
static int cntPairs(int a[], int n)
{

    // To store the count of odd numbers and
    // the count of even numbers such that 2
    // is the only even factor of that number
    int odd = 0, even = 0;

    for (int i = 0; i < n; i++)
    {

        // If current number is odd
        if (a[i] % 2 == 1)
            odd++;

        // If current number is even and 2
        // is the only even factor of it
        else if ((a[i] / 2) % 2 == 1)
            even++;
    }

    // Calculate total number of valid pairs
    int ans = odd * even + (odd * (odd - 1)) / 2;

    return ans;
}

// Driver code
public static void main(String []args)
{
    int a[] = { 4, 2, 7, 11, 14, 15, 18 };
    int n = a.length;

    System.out.println(cntPairs(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of valid pairs
def cntPairs(a, n) :

    # To store the count of odd numbers and
    # the count of even numbers such that 2
    # is the only even factor of that number
    odd = 0; even = 0;

    for i in range(n) :

        # If current number is odd
        if (a[i] % 2 == 1) :
            odd += 1;

        # If current number is even and 2
        # is the only even factor of it
        elif ((a[i] / 2) % 2 == 1) :
            even += 1;

    # Calculate total number of valid pairs
    ans = odd * even + (odd * (odd - 1)) // 2;

    return ans;

# Driver code
if __name__ == "__main__" :

    a = [ 4, 2, 7, 11, 14, 15, 18 ];
    n = len(a);

    print(cntPairs(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of valid pairs
static int cntPairs(int []a, int n)
{

    // To store the count of odd numbers and
    // the count of even numbers such that 2
    // is the only even factor of that number
    int odd = 0, even = 0;

    for (int i = 0; i < n; i++)
    {

        // If current number is odd
        if (a[i] % 2 == 1)
            odd++;

        // If current number is even and 2
        // is the only even factor of it
        else if ((a[i] / 2) % 2 == 1)
            even++;
    }

    // Calculate total number of valid pairs
    int ans = odd * even + (odd * (odd - 1)) / 2;

    return ans;
}

// Driver code
public static void Main(String []args)
{
    int []a = { 4, 2, 7, 11, 14, 15, 18 };
    int n = a.Length;

    Console.WriteLine(cntPairs(a, n));
}
}

// This code is contributed by Ajay KUmar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of valid pairs
function cntPairs(a, n)
{

    // To store the count of odd numbers and
    // the count of even numbers such that 2
    // is the only even factor of that number
    var odd = 0, even = 0;

    for (var i = 0; i < n; i++) {

        // If current number is odd
        if (a[i] % 2 == 1)
            odd++;

        // If current number is even and 2
        // is the only even factor of it
        else if ((a[i] / 2) % 2 == 1)
            even++;
    }

    // Calculate total number of valid pairs
    var ans = odd * even + (odd * (odd - 1)) / 2;

    return ans;
}

// Driver code
var a = [4, 2, 7, 11, 14, 15, 18];
var n = a.length;
document.write( cntPairs(a, n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(N)