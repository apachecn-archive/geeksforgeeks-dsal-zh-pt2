# 计算与 x 的异或大于 x 的较小值

> 原文:[https://www . geesforgeks . org/count-small-values-what-xor-x-greater-x/](https://www.geeksforgeeks.org/count-smaller-values-whose-xor-x-greater-x/)

给定一个整数“x”，求满足以下条件的“a”的值的个数:

1.  异或 x > x
2.  0 < a < x

**示例:**

```
Input : x = 10 
Output : 5
Explanation: For x = 10, following 5 values
             of 'a' satisfy the conditions:
             1 XOR 10 = 11
             4 XOR 10 = 14
             5 XOR 10 = 15
             6 XOR 10 = 12
             7 XOR 10 = 13 

Input : x = 2
Output : 1
Explanation: For x=2, we have just one value
             1 XOR 2 = 3.
```

**天真方法**
一个简单的方法是检查 0 和“x”之间的“A”的所有值，并计算它与 x 的异或，检查条件 1 是否满足。

## C++

```
// C++ program to find count of values
// whose XOR with x is greater than x
// and values are smaller than x
#include<bits/stdc++.h>
using namespace std;

int countValues(int x)
{
    int count = 0;
    for (int i=1; i < x; i++)
        if ((i ^ x) > x)
            count++;
    return count;
}

// Driver code
int main()
{
    int x = 10;
    cout << countValues(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of values
// whose XOR with x is greater than x
// and values are smaller than x

public class XOR
{
    static int countValues(int x)
    {
        int count = 0;
        for (int i=1; i < x; i++)
            if ((i ^ x) > x)
                count++;
        return count;
    }

    public static void main (String[] args)
    {
        int x = 10;
        System.out.println(countValues(x));
    }
}

// This code is contributed by Saket Kumar
```

## 蟒蛇 3

```
# Python3 program to find
# count of values whose
# XOR with x is greater
# than x and values are
# smaller than x

def countValues(x):

    count = 0
    for i in range(1 ,x):
        if ((i ^ x) > x):
            count += 1
    return count

# Driver code
x = 10
print(countValues(x))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find count of values
// whose XOR with x is greater than x
// and values are smaller than x
using System;

class GFG
{
    static int countValues(int x)
    {
        int count = 0;
        for (int i = 1; i < x; i++)
            if ((i ^ x) > x)
                count++;
        return count;
    }

    public static void Main ()
    {
        int x = 10;
        Console.Write(countValues(x));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count of values
// whose XOR with x is greater than x
// and values are smaller than x

function countValues($x)
{
    $count = 0;
    for ($i = 1; $i < $x; $i++)
        if (($i ^ $x) > $x)
            $count++;
    return $count;
}

    // Driver code
    $x = 10;
    echo countValues($x);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find count of values
// whose XOR with x is greater than x
// and values are smaller than x

function countValues(x)
{
    let count = 0;
    for (let i=1; i < x; i++)
        if ((i ^ x) > x)
            count++;
    return count;
}

// Driver code
    let x = 10;
    document.write(countValues(x));

</script>
```

**输出:**

```
5
```

上述方法的时间复杂度为 O(x)。

**高效方法**
高效的解决方案在于数字的二进制表示。我们考虑二进制表示中的所有 0。对于第 I 个位置上的每一个 0，我们可以有 2 个小于或等于 x 的 <sup>i</sup> 数，并且具有更大的异或。

## C++

```
// C++ program to find count of values
// whose XOR with x is greater than x
// and values are smaller than x
#include<bits/stdc++.h>
using namespace std;

int countValues(int x)
{
    // Initialize result
    int count = 0, n = 1;

    // Traversing through all bits of x
    while (x != 0)
    {
        // If current last bit of x is set
        // then increment count by n. Here
        // n is a power of 2 corresponding
        // to position of bit
        if (x%2 == 0)
            count += n;

        // Simultaneously calculate the 2^n
        n *= 2;

        // Replace x with x/2;
        x /= 2;
    }

    return count;
}

// Driver code
int main()
{
    int x = 10;
    cout << countValues(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of values
// whose XOR with x is greater than x
// and values are smaller than x

class GFG
{
    static int countValues(int x)
    {
        // Initialize result
        int count = 0, n = 1;

        // Traversing through all bits of x
        while (x != 0)
        {
            // If current last bit of x is set
            // then increment count by n. Here
            // n is a power of 2 corresponding
            // to position of bit
            if (x % 2 == 0)
                count += n;

            // Simultaneously calculate the 2^n
            n *= 2;

            // Replace x with x/2;
            x /= 2;
        }
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int x = 10;
        System.out.println(countValues(x));
    }

}

// This code is contributed by Saket Kumar
```

## 蟒蛇 3

```
# Python3 program to find count
# of values whose XOR with
# x is greater than x and
# values are smaller than x

def countValues(x):

    # Initialize result
    count = 0;
    n = 1;

    # Traversing through
    # all bits of x
    while (x > 0):

        # If current last bit
        # of x is set then
        # increment count by
        # n. Here n is a power
        # of 2 corresponding
        # to position of bit
        if (x % 2 == 0):
            count += n;

        # Simultaneously
        # calculate the 2^n
        n *= 2;

        # Replace x with x/2;
        x /= 2;
        x = int(x);

    return count;

# Driver code
x = 10;
print(countValues(x));

# This code is contributed
# by mits
```

## C#

```
// C# program to find count of values
// whose XOR with x is greater than x
// and values are smaller than x
using System;

class GFG
{
    static int countValues(int x)
    {
        // Initialize result
        int count = 0, n = 1;

        // Traversing through all bits of x
        while (x != 0)
        {
            // If current last bit of x is set
            // then increment count by n. Here
            // n is a power of 2 corresponding
            // to position of bit
            if (x % 2 == 0)
                count += n;

            // Simultaneously calculate the 2^n
            n *= 2;

            // Replace x with x/2;
            x /= 2;
        }
        return count;
    }

    // Driver code
    public static void Main ()
    {
        int x = 10;
        Console.Write(countValues(x));
    }

}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count
// of values whose XOR with
// x is greater than x and
// values are smaller than x

function countValues($x)
{

    // Initialize result
    $count = 0;
    $n = 1;

    // Traversing through
    // all bits of x
    while ($x != 0)
    {
        // If current last bit
        // of x is set then
        // increment count by
        // n. Here n is a power
        // of 2 corresponding
        // to position of bit
        if ($x % 2 == 0)
            $count += $n;

        // Simultaneously
        // calculate the 2^n
        $n *= 2;

        // Replace x with x/2;
        $x /= 2;
        $x = (int)$x;
    }

    return $count;
}

// Driver code
$x = 10;
echo countValues($x);

// This code is contributed
// by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript program to find count of
// values whose XOR with x is greater
// than x and values are smaller than x  
function countValues(x)
{

    // Initialize result
    var count = 0, n = 1;

    // Traversing through all bits of x
    while (x != 0)
    {

        // If current last bit of x is set
        // then increment count by n. Here
        // n is a power of 2 corresponding
        // to position of bit
        if (x % 2 == 0)
            count += n;

        // Simultaneously calculate the 2^n
        n *= 2;

        // Replace x with x/2;
        x = parseInt(x / 2);
    }
    return count;
}

// Driver code
var x = 10;
document.write(countValues(x));

// This code is contributed by Princi Singh

</script>
```

**输出:**

```
5
```

该解决方案的时间复杂度为 0(对数 x)

本文由 [**丹麦 KALEEM**](https://www.linkedin.com/in/mohdanishh/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。