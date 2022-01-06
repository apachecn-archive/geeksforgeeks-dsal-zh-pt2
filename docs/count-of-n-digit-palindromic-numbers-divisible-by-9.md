# 可被 9 整除的 N 位回文数计数

> 原文:[https://www . geeksforgeeks . org/n 位回文数字计数-可被 9 整除/](https://www.geeksforgeeks.org/count-of-n-digit-palindromic-numbers-divisible-by-9/)

给定一个整数 **N** ，任务是统计 N 位回文数字的个数，这些数字包含从 1 到 9 的数字，并且可以被 9 整除。
**例:**

> **输入:** N = 1
> **输出:** 1
> **说明:**
> 只有 9 是 1 位数，是回文，可被 9 整除。
> **输入:** N = 3
> **输出:** 9
> **解释:**
> 回文可被 9 整除的三位数为–
> { 171，252，333，414，585，666，747，828，999}

**方法:**问题中的关键观察是如果数能被 9 整除，那么数的位数之和也能被 9 整除。因此，这个问题可以根据它的等价性来解决。

*   **如果 N 是奇数:**我们可以把 1 到 9 之间的任意一个数放在 1 到(N-1)/2 的位置，类似的，其他的数字按相反的顺序选择，形成回文数，中间的元素选择上，形成可被 9 整除的数字之和。因此，数字(N-1)/2 位的每个位置有 9 个选择，因此该数字的计数为:

```
Count of N-digit Palindromic numbers =
                 9(N-1)/2
```

*   **如果 N 为偶数:**我们可以在 1 到(N-2)/2 的位置放上 1 到 9 之间的任意一个数，同样的，其他的数字按照相反的顺序选择，形成回文数，中间的元素选择上，形成可被 9 整除的数字之和。因此，数字(N-2)/2 位的每个位置有 9 个选择，因此该数字的计数为:

```
Count of N-digit Palindromic numbers =
                 9(N-2)/2
```

## C++

```
// C++ implementation to count the
// number of N digit palindromic
// numbers divisible by 9

#include <bits/stdc++.h>

using namespace std;

// Function to find the count of
// N digits palindromic numbers
// which are divisible by 9
int countPalindromic(int n)
{
    int count;

    // if N is odd
    if (n % 2 == 1) {
        count = pow(9, (n - 1) / 2);
    }
    // if N is even
    else
    {
        count = pow(9, (n - 2) / 2);
    }
    return count;
}

// Driver Code
int main()
{
    int n = 3;
    cout << countPalindromic(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of N digit palindromic
// numbers divisible by 9
import java.util.*;

class GFG{

// Function to find the count of
// N digits palindromic numbers
// which are divisible by 9
static int countPalindromic(int n)
{
    int count;

    // If N is odd
    if (n % 2 == 1)
    {
        count = (int) Math.pow(9, (n - 1) / 2);
    }

    // If N is even
    else
    {
        count = (int) Math.pow(9, (n - 2) / 2);
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3;
    System.out.println(countPalindromic(n));
}
}

// This code is contributed by ANKITKUMAR34
```

## 蟒蛇 3

```
# Python3 implementation to count the
# number of N digit palindromic
# numbers divisible by 9

# Function to find the count of
# N digits palindromic numbers
# which are divisible by 9
def countPalindromic(n):

    count = 0

    # If N is odd
    if (n % 2 == 1):
        count = pow(9, (n - 1) // 2)

    # If N is even
    else:
        count = pow(9, (n - 2) // 2)

    return count

# Driver Code
n = 3
print(countPalindromic(n))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# implementation to count the
// number of N digit palindromic
// numbers divisible by 9
using System;
class GFG{

// Function to find the count of
// N digits palindromic numbers
// which are divisible by 9
static int countPalindromic(int n)
{
    int count;

    // If N is odd
    if (n % 2 == 1)
    {
        count = (int) Math.Pow(9, (n - 1) / 2);
    }

    // If N is even
    else
    {
        count = (int) Math.Pow(9, (n - 2) / 2);
    }
    return count;
}

// Driver Code
public static void Main()
{
    int n = 3;
    Console.Write(countPalindromic(n));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// Javascript implementation to count the
// number of N digit palindromic
// numbers divisible by 9

// Function to find the count of
// N digits palindromic numbers
// which are divisible by 9
function countPalindromic(n)
{
    var count;

    // if N is odd
    if (n % 2 == 1) {
        count = Math.pow(9, (n - 1) / 2);
    }
    // if N is even
    else
    {
        count = Math.pow(9, (n - 2) / 2);
    }
    return count;
}

// Driver Code
var n = 3;
document.write( countPalindromic(n));

</script>
```

**Output:** 

```
9
```