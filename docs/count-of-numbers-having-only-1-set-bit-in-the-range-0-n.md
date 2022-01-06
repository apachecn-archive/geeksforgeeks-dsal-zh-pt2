# 在[0，n]

范围内只有 1 个设置位的数字计数

> 原文:[https://www . geesforgeks . org/numbers-count-with-1-set-bit-in-range-0-n/](https://www.geeksforgeeks.org/count-of-numbers-having-only-1-set-bit-in-the-range-0-n/)

给定一个整数 **n** ，任务是对范围**【0，n】**中只有 1 个设定位的数字进行计数。
**例:**

> **输入:** n = 7
> **输出:** 3
> 000、001、010、011、100、101、110 和 111 是直到 7 的所有数字的二进制表示。
> 只有 3 个数字(001、010 和 100)只有 1 个设置位。
> **输入:** n = 3
> **输出:** 2

**方法:**如果需要 **k** 位来表示 **n** ，则可能有 **k** 个数字，因为 **1 每次可以位于 k 个不同的位置**。
以下是上述方法的实施

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required count
int count(int n)
{

    // To store the count of numbers
    int cnt = 0;
    int p = 1;
    while (p <= n) {
        cnt++;

        // Every power of 2 contains
        // only 1 set bit
        p *= 2;
    }
    return cnt;
}

// Driver code
int main()
{
    int n = 7;
    cout << count(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the required count
    static int count(int n)
    {

        // To store the count of numbers
        int cnt = 0;
        int p = 1;
        while (p <= n) {
            cnt++;

            // Every power of 2 contains
            // only 1 set bit
            p *= 2;
        }
        return cnt;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 7;
        System.out.print(count(n));
    }
}
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the required count
    static int count(int n)
    {

        // To store the count of numbers
        int cnt = 0;
        int p = 1;
        while (p <= n) {
            cnt++;

            // Every power of 2 contains
            // only 1 set bit
            p *= 2;
        }
        return cnt;
    }

    // Driver code
    public static void Main()
    {
        int n = 7;
        Console.Write(count(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required count
def count(n):

    # To store the count of numbers
    cnt = 0
    p = 1
    while (p <= n):
        cnt = cnt + 1

        # Every power of 2 contains
        # only 1 set bit
        p *= 2
    return cnt

# Driver code
n = 7
print(count(n));
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required count
function count_t($n)
{

    // To store the count of numbers
    $cnt = 0;
    $p = 1;
    while ($p <= $n)
    {
        $cnt++;

        // Every power of 2 contains
        // only 1 set bit
        $p *= 2;
    }
    return $cnt;
}

// Driver code
$n = 7;
echo count_t($n);

// This Code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the required count
function count(n)
{

    // To store the count of numbers
    var cnt = 0;
    var p = 1;
    while (p <= n) {
        cnt++;

        // Every power of 2 contains
        // only 1 set bit
        p *= 2;
    }
    return cnt;
}

// Driver code
var n = 7;
document.write(count(n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(log n)