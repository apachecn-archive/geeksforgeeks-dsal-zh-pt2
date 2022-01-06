# 将二进制字符串转换为全 0 或全 1 所需的最小运算量

> 原文:[https://www . geesforgeks . org/minimum-operations-required-convert-a-binary-string-all-0 或-all-1s/](https://www.geeksforgeeks.org/minimum-operations-required-to-convert-a-binary-string-to-all-0s-or-all-1s/)

给定一个二进制字符串 **str** ，任务是找到使该字符串的所有字符相同所需的最小操作数，即结果字符串包含全 0 或全 1。在一次操作中，任何连续 0 的数据块都可以转换为相同长度的连续 1 的数据块，反之亦然。
**例:**

> **输入:** str = "000111"
> **输出:** 1
> 在一次操作中，要么将全 0 改为 1
> 要么将全 1 改为 0。
> **输入:** str = "0011101010"
> **输出:** 3
> 所有的 1 可以通过 3 次运算转换为 0。

**处理方法:**问题是把所有的字符转换成一个单独的字符。既然转换一整组连续的字符算一步。您可以计算不同组的数量，因为它们之间存在其他字符。现在，步数将是这两个数字的最小值。因此，答案将是 0 的连续块计数或 1 的连续块计数的最小值。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// minimum operations required
int minOperations(string str, int n)
{
    int count = 0;
    for (int i = 0; i < n - 1; i++) {

        // Increment count when consecutive
        // characters are different
        if (str[i] != str[i + 1])
            count++;
    }

    // Answer is rounding off the
    // (count / 2) to lower
    return (count + 1) / 2;
}

// Driver code
int main()
{
    string str = "000111";
    int n = str.length();

    cout << minOperations(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of
// minimum operations required
static int minOperations(String str, int n)
{
    int count = 0;
    for (int i = 0; i < n - 1; i++)
    {

        // Increment count when consecutive
        // characters are different
        if (str.charAt(i) != str.charAt(i + 1))
            count++;
    }

    // Answer is rounding off the
    // (count / 2) to lower
    return (count + 1) / 2;
}

// Driver code
public static void main(String[] args)
{
    String str = "000111";
    int n = str.length();

    System.out.println(minOperations(str, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# minimum operations required
def minOperations(str, n):
    count = 0
    for i in range(n - 1):

        # Increment count when consecutive
        # characters are different
        if (str[i] != str[i + 1]):
            count += 1

    # Answer is rounding off the
    # (count / 2) to lower
    return (count + 1) // 2

# Driver code
str = "000111"
n = len(str)

print(minOperations(str, n))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// minimum operations required
static int minOperations(string str, int n)
{
    int count = 0;
    for (int i = 0; i < n - 1; i++)
    {

        // Increment count when consecutive
        // characters are different
        if (str[(i)] != str[(i + 1)])
            count++;
    }

    // Answer is rounding off the
    // (count / 2) to lower
    return (count + 1) / 2;
}

// Driver code
public static void Main()
{
    string str = "000111";
    int n = str.Length;

    Console.WriteLine(minOperations(str, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
 //Javascript implementation of the approach

// Function to return the count of
// minimum operations required
function minOperations(str, n)
{
    var count = 0;
    for (var i = 0; i < n - 1; i++) {

        // Increment count when consecutive
        // characters are different
        if (str[i] != str[i + 1])
            count++;
    }

    // Answer is rounding off the
    // (count / 2) to lower
    return (count + 1) / 2;
}

 var str = "000111";
 var n = str.length;
document.write(minOperations(str, n));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
1
```