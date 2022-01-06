# 仅用 1 构成的可被 K 整除的最小数的长度

> 原文:[https://www . geeksforgeeks . org/最小数字长度可被 k 整除且仅使用-1s 形成/](https://www.geeksforgeeks.org/length-of-the-smallest-number-which-is-divisible-by-k-and-formed-by-using-1s-only/)

给定一个整数 **K** ，任务是找到最小的编号 **N** 的长度，该编号可被 **K** 整除，并且仅用 1 作为其位数。如果没有这样的号码，则打印 **-1**
**示例:**

> **输入:** K = 3
> **输出:** 3
> 111 是仅用 1 构成的最小数
> 可被 3 整除。
> **输入:** K = 7
> **输出:** 6
> 111111 为必输号码。
> **输入:** K = 12
> **输出:** -1

**天真的做法:**

1.  首先我们要检查 **K** 是不是 **2** 或者 **5** 的倍数，那么答案将是 **-1** ，因为没有只使用 **1 的**作为其数字组成的数字，它可以被 **2** 或者 **5** 整除。
2.  现在循环使用 **1 的**最多 **K** 次形成的每个可能的编号，并用 **K** 检查其可分性。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return length
// of the resultant number
int numLen(int K)
{

    // If K is a multiple of 2 or 5
    if (K % 2 == 0 || K % 5 == 0)
        return -1;

    int number = 0;

    int len = 1;

    for (len = 1; len <= K; len++) {

        // Generate all possible numbers
        // 1, 11, 111, 111, ..., K 1's
        number = number * 10 + 1;

        // If number is divisible by k
        // then return the length
        if ((number % K == 0))
            return len;
    }

    return -1;
}

// Driver code
int main()
{

    int K = 7;
    cout << numLen(K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return length
    // of the resultant number
    static int numLen(int K)
    {

        // If K is a multiple of 2 or 5
        if (K % 2 == 0 || K % 5 == 0)
        {
            return -1;
        }

        int number = 0;

        int len = 1;

        for (len = 1; len <= K; len++)
        {

            // Generate all possible numbers
            // 1, 11, 111, 111, ..., K 1's
            number = number * 10 + 1;

            // If number is divisible by k
            // then return the length
            if ((number % K == 0))
            {
                return len;
            }
        }

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int K = 7;
        System.out.println(numLen(K));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return length
# of the resultant number
def numLen(K):

    # If K is a multiple of 2 or 5
    if (K % 2 == 0 or K % 5 == 0):
        return -1;

    number = 0;

    len = 1;

    for len in range(1,K+1):

        # Generate all possible numbers
        # 1, 11, 111, 111, ..., K 1's
        number = number * 10 + 1;

        # If number is divisible by k
        # then return the length
        if ((number % K == 0)):
            return len;

    return -1;

# Driver code
K = 7;
print(numLen(K));

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return length
// of the resultant number
static int numLen(int K)
{

    // If K is a multiple of 2 or 5
    if (K % 2 == 0 || K % 5 == 0)
        return -1;

    int number = 0;

    int len = 1;

    for (len = 1; len <= K; len++)
    {

        // Generate all possible numbers
        // 1, 11, 111, 111, ..., K 1's
        number = number * 10 + 1;

        // If number is divisible by k
        // then return the length
        if ((number % K == 0))
            return len;
    }

    return -1;
}

// Driver code
static void Main()
{
    int K = 7;
    Console.WriteLine(numLen(K));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return length
// of the resultant number
function numLen($K)
{

    // If K is a multiple of 2 or 5
    if ($K % 2 == 0 || $K % 5 == 0)
        return -1;

    $number = 0;

    $len = 1;

    for ($len = 1; $len <= $K; $len++)
    {

        // Generate all possible numbers
        // 1, 11, 111, 111, ..., K 1's
        $number = $number * 10 + 1;

        // If number is divisible by k
        // then return the length
        if (($number % $K == 0))
            return $len;
    }

    return -1;
}

// Driver code
$K = 7;
echo numLen($K);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   

// Function to return length
    // of the resultant number
    function numLen(K) {

        // If K is a multiple of 2 or 5
        if (K % 2 == 0 || K % 5 == 0) {
            return -1;
        }

        var number = 0;
        var len = 1;
        for (len = 1; len <= K; len++)
        {

            // Generate all possible numbers
            // 1, 11, 111, 111, ..., K 1's
            number = number * 10 + 1;

            // If number is divisible by k
            // then return the length
            if ((number % K == 0)) {
                return len;
            }
        }
        return -1;
    }

    // Driver code   
    var K = 7;
    document.write(numLen(K));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
6
```

**有效方法:**正如我们在上面的方法中看到的，我们生成所有可能的数字，如 **1，11，1111，11111，…，K 次**，但是如果 **K** 的值非常大，那么编号将超出数据类型的范围，因此我们可以利用模块化属性。
不做 **number = number * 10 + 1** ，我们可以做得更好作为**number =(number * 10+1)% K**
**说明:**我们从 **number = 1** 开始，反复做 **number = number * 10 + 1** ，然后在每次迭代中我们会得到上述序列的一个新项。

> 1 * 10+1 = 11
> 11 * 10+1 = 111
> 111 * 10+1 = 1111
> 1111 * 10+1 = 11111
> 11111 * 10+1 = 11111

因为我们在每一步都在重复取这个数的余数，所以在每一步我们都有， **newNum = oldNum * 10 + 1** 。根据模运算规则 **(a * b + c) % m** 与 **((a * b) % m + c % m) % m** 相同。所以不管 **oldNum** 是余数还是原数，答案都是正确的。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return length
// of the resultant number
int numLen(int K)
{

    // If K is a multiple of 2 or 5
    if (K % 2 == 0 || K % 5 == 0)
        return -1;

    int number = 0;

    int len = 1;

    for (len = 1; len <= K; len++) {

        // Instead of generating all possible numbers
        // 1, 11, 111, 111, ..., K 1's
        // Take remainder with K
        number = (number * 10 + 1) % K;

        // If number is divisible by k
        // then remainder will be 0
        if (number == 0)
            return len;
    }

    return -1;
}

// Driver code
int main()
{

    int K = 7;
    cout << numLen(K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return length
    // of the resultant number
    public static int numLen(int K)
    {

        // If K is a multiple of 2 or 5
        if (K % 2 == 0 || K % 5 == 0)
            return -1;

        int number = 0;

        int len = 1;

        for (len = 1; len <= K; len++) {

            // Instead of generating all possible numbers
            // 1, 11, 111, 111, ..., K 1's
            // Take remainder with K
            number = (number * 10 + 1) % K;

            // If number is divisible by k
            // then remainder will be 0
            if (number == 0)
                return len;
        }

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int K = 7;
        System.out.print(numLen(K));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return length
# of the resultant number
def numLen(K):

    # If K is a multiple of 2 or 5
    if(K % 2 == 0 or K % 5 == 0):
        return -1

    number = 0

    len = 1

    for len in range (1, K + 1):

        # Instead of generating all possible numbers
        # 1, 11, 111, 111, ..., K 1's
        # Take remainder with K
        number = ( number * 10 + 1 ) % K

        # If number is divisible by k
        # then remainder will be 0
        if number == 0:
            return len

    return -1

# Driver code
K = 7
print(numLen(K))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return length
// of the resultant number
public static int numLen(int K)
{

    // If K is a multiple of 2 or 5
    if (K % 2 == 0 || K % 5 == 0)
        return -1;

    int number = 0;

    int len = 1;

    for (len = 1; len <= K; len++)
    {

        // Instead of generating all possible numbers
        // 1, 11, 111, 111, ..., K 1's
        // Take remainder with K
        number = (number * 10 + 1) % K;

        // If number is divisible by k
        // then remainder will be 0
        if (number == 0)
            return len;
    }

    return -1;
}

// Driver code
public static void Main()
{
    int K = 7;
    Console.WriteLine(numLen(K));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return length
// of the resultant number
function numLen($K)
{

    // If K is a multiple of 2 or 5
    if ($K % 2 == 0 || $K % 5 == 0)
        return -1;

    $number = 0;

    $len = 1;

    for ($len = 1; $len <= $K; $len++)
    {

        // Instead of generating all possible numbers
        // 1, 11, 111, 111, ..., K 1's
        // Take remainder with K
        $number = ($number * 10 + 1) % $K;

        // If number is divisible by k
        // then remainder will be 0
        if ($number == 0)
            return $len;
    }

    return -1;
}

// Driver code
$K = 7;
echo numLen($K);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach 
// Function to return length
// of the resultant number
function numLen(K)
{

    // If K is a multiple of 2 or 5
    if (K % 2 == 0 || K % 5 == 0)
        return -1;

    var number = 0;

    var len = 1;

    for (len = 1; len <= K; len++) {

        // Instead of generating all possible numbers
        // 1, 11, 111, 111, ..., K 1's
        // Take remainder with K
        number = (number * 10 + 1) % K;

        // If number is divisible by k
        // then remainder will be 0
        if (number == 0)
            return len;
    }

    return -1;
}

// Driver code
var K = 7;
document.write(numLen(K));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
6
```

**时间复杂度:**O(K)
T3】辅助空间: O(1)