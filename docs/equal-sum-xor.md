# 等和异或

> 原文:[https://www.geeksforgeeks.org/equal-sum-xor/](https://www.geeksforgeeks.org/equal-sum-xor/)

给定正整数 n，求正整数 I 的个数，使得 0 <= i <= n，n+i = n^i

**示例:**

```
Input  : n = 7
Output : 1
Explanation:
7^i = 7+i holds only for only for i = 0
7+0 = 7^0 = 7

Input: n = 12
Output: 4
12^i = 12+i hold only for i = 0, 1, 2, 3
for i=0, 12+0 = 12^0 = 12
for i=1, 12+1 = 12^1 = 13
for i=2, 12+2 = 12^2 = 14
for i=3, 12+3 = 12^3 = 15
```

**方法 1(简单):**
一个简单的解决方案是迭代 i 0 < = i < = n 的所有值，并计算所有令人满意的值。

## C++

```
/* C++ program to print count of values such
   that n+i = n^i */
#include <iostream>
using namespace std;

// function to count number of values less than
// equal to n that satisfy the given condition
int countValues (int n)
{
    int countV = 0;

    // Traverse all numbers from 0 to n and
    // increment result only when given condition
    // is satisfied.
    for (int i=0; i<=n; i++ )
        if ((n+i) == (n^i) )
            countV++;

    return countV;
}

// Driver program
int main()
{
    int n = 12;
    cout << countValues(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to print count of values
 such that n+i = n^i */
import java.util.*;

class GFG {

    // function to count number of values
    // less than equal to n that satisfy
    // the given condition
    public static int countValues (int n)
    {
        int countV = 0;

        // Traverse all numbers from 0 to n
        // and increment result only when
        // given condition is satisfied.
        for (int i = 0; i <= n; i++ )
            if ((n + i) == (n ^ i) )
                countV++;

        return countV;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 12;
        System.out.println(countValues(n));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to print count
# of values such that n+i = n^i

# function to count number
# of values less than
# equal to n that satisfy
# the given condition
def countValues (n):
    countV = 0;

    # Traverse all numbers
    # from 0 to n and
    # increment result only
    # when given condition
    # is satisfied.
    for i in range(n + 1):
        if ((n + i) == (n ^ i)):
            countV += 1;

    return countV;

# Driver Code
n = 12;
print(countValues(n));

# This code is contributed by mits
```

## C#

```
/* C# program to print count of values
such that n+i = n^i */
using System;

class GFG {

    // function to count number of values
    // less than equal to n that satisfy
    // the given condition
    public static int countValues (int n)
    {
        int countV = 0;

        // Traverse all numbers from 0 to n
        // and increment result only when
        // given condition is satisfied.
        for (int i = 0; i <= n; i++ )
            if ((n + i) == (n ^ i) )
                countV++;

        return countV;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int n = 12;
        Console.WriteLine(countValues(n));

    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print count
// of values such that n+i = n^i

// function to count number
// of values less than
// equal to n that satisfy
// the given condition
function countValues ($n)
{
    $countV = 0;

    // Traverse all numbers
    // from 0 to n and
    // increment result only
    // when given condition
    // is satisfied.
    for ($i = 0; $i <= $n; $i++ )
        if (($n + $i) == ($n^$i) )
            $countV++;

    return $countV;
}

    // Driver Code
    $n = 12;
    echo countValues($n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

/* JavaScript program to print count of values such
that n+i = n^i */

// function to count number of values less than
// equal to n that satisfy the given condition
function countValues (n)
{
    let countV = 0;

    // Traverse all numbers from 0 to n and
    // increment result only when given condition
    // is satisfied.
    for (let i=0; i<=n; i++ )
        if ((n+i) == (n^i) )
            countV++;

    return countV;
}

// Driver program

    let n = 12;
    document.write(countValues(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(n)

**空间复杂度:** O(1)

**方法 2(高效):**
一个高效的解决方案如下

我们知道(n+i)=(n^i)+2*(n&i)
所以 n + i = n ^ i 意味着 n & i = 0
因此我们的问题简化为寻找 I 的值，使得 n & i = 0。如何找到这种对的计数？我们可以使用 n 的二进制表示中的未设置位的计数。为了使 n & i 为零，我必须取消设置 n 的所有设置位。如果在 n 中的特定位置设置了第 k 位，I 中的第 k 位必须始终为 0，否则 I 的第 k 位可以为 0 或 1
因此，这样的组合总数是 n 中未设置位的 2^(count 数)
例如，考虑 n = 12(二进制表示:1 1 0 0)。
I 的所有可能值，可以不设置 n 的所有位，都是 0 0/1 0/1，其中 0/1 表示 0 或 1。这样的 I 值的数量是 2^2 = 4。

以下是遵循上述思路的程序。

## C++

```
/* c++ program to print count of values such
  that n+i = n^i */
#include <bits/stdc++.h>
using namespace std;

// function to count number of values less than
// equal to n that satisfy the given condition
int countValues(int n)
{
    // unset_bits keeps track of count of un-set
    // bits in binary representation of n
    int unset_bits=0;
    while (n)
    {
        if ((n & 1) == 0)
            unset_bits++;
        n=n>>1;
    }

    // Return 2 ^ unset_bits
    return 1 << unset_bits;
}

// Driver code
int main()
{
    int n = 12;
    cout << countValues(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to print count of values
  such that n+i = n^i */
import java.util.*;

class GFG {

    // function to count number of values
    // less than equal to n that satisfy
    // the given condition
    public static int countValues(int n)
    {
        // unset_bits keeps track of count
        // of un-set bits in binary
        // representation of n
        int unset_bits=0;
        while (n > 0)
        {
            if ((n & 1) == 0)
                unset_bits++;
            n=n>>1;
        }

        // Return 2 ^ unset_bits
        return 1 << unset_bits;
    }

    /* Driver program to test above
    function */
    public static void main(String[] args)
    {
        int n = 12;
        System.out.println(countValues(n));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## C#

```
/* C# program to print count of values
  such that n+i = n^i */
using System;
public class GFG {

    // function to count number of values
    // less than equal to n that satisfy
    // the given condition
    public static int countValues(int n)
    {

        // unset_bits keeps track of count
        // of un-set bits in binary
        // representation of n
        int unset_bits=0;
        while (n > 0)
        {
            if ((n & 1) == 0)
                unset_bits++;
            n=n>>1;
        }

        // Return 2 ^ unset_bits
        return 1 << unset_bits;
    }

    /* Driver program to test above
    function */
    public static void Main(String[] args)
    {
        int n = 12;
        Console.WriteLine(countValues(n));

    }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python3 program to print count of values such
# that n+i = n^i

# function to count number of values less than
# equal to n that satisfy the given condition
def countValues(n):

    # unset_bits keeps track of count of un-set
    # bits in binary representation of n
    unset_bits = 0

    while(n):
        if n & 1 == 0:
            unset_bits += 1
        n = n >> 1

    # Return 2 ^ unset_bits    
    return 1 << unset_bits

# Driver code
if __name__=='__main__':
    n = 12
    print(countValues(n))

# This code is contributed by rutvik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* PHP program to print count
of values such that n+i = n^i */

// function to count number of
// values less than equal to n
// that satisfy the given
// condition
function countValues( $n)
{

    // unset_bits keeps track
    // of count of un-set bits
    // in binary representation
    // of n
    $unset_bits = 0;
    while ($n)
    {
        if (($n & 1) == 0)
            $unset_bits++;
        $n = $n >> 1;
    }

    // Return 2 ^ unset_bits
    return 1 << $unset_bits;
}

// Driver code

    $n = 12;
    echo countValues($n);

// This code is contributed
// by Anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to print count of values
// such that n+i = n^i

// Function to count number of values
// less than equal to n that satisfy
// the given condition
function countValues(n)
{

    // unset_bits keeps track of count
    // of un-set bits in binary
    // representation of n
    let unset_bits = 0;

    while (n > 0)
    {
        if ((n & 1) == 0)
            unset_bits++;

        n = n >> 1;
    }

    // Return 2 ^ unset_bits
    return 1 << unset_bits;
}

// Driver Code
let n = 12;

document.write(countValues(n));

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(log(n))

**空间复杂度:** O(1)

本文由 **Nikhil Chakravartula** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。