# 计数与 N 之差等于与 N 异或的数

> 原文:[https://www . geesforgeks . org/count-numbers-其与 n 的差等于与 n 的异或/](https://www.geeksforgeeks.org/count-numbers-whose-difference-with-n-is-equal-to-xor-with-n/)

给定一个数字 N，任务是计算 x 的所有可能值，使得 n ![\oplus  ](img/290920f59367bd65a77d4691be9d6c08.png "Rendered by QuickLaTeX.com") x 等于(N-x)，其中![\oplus  ](img/290920f59367bd65a77d4691be9d6c08.png "Rendered by QuickLaTeX.com")表示按位异或运算。
**例:**

```
Input: N = 3
Output: 4
The all possible values of x are respectively 0, 1, 2, 3.

Input: N = 6
Output: 4
The all possible values of x are respectively 0, 2, 4, 6.
```

**方法:**如果两位符号相反，则两位的异或值为 1，如果两位相同，则为 0。所以基于异或的性质，我们可以说 n ![\oplus  ](img/290920f59367bd65a77d4691be9d6c08.png "Rendered by QuickLaTeX.com") x 总是大于或等于 n-x，其值与 n-x 相等的唯一条件是 x 的比特构成 n 的比特子集，因为如果在第 I 个位置 **x** 和 **n** 都设置了比特，那么在异或之后，该值将减小，减小的值将是![2^{i}  ](img/208ddf4ce006cd0aacbdeda1dcbccc19.png "Rendered by QuickLaTeX.com")，其中 **i** 是基于 0 的位置。
那么答案是 n 个数的比特子集的总计数为![2^{k}  ](img/fefb8300088438e1196c54808f5d6759.png "Rendered by QuickLaTeX.com")，其中 k 为 n 中设置比特的计数
下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// function to Count all values of x
void count_values(int n)
{
    // Count set bits in n
    // by using stl function
    int set_bits = __builtin_popcount(n);

    // count all subset of set bits
    cout << pow(2, set_bits) << "\n";
}

// Driver code
int main()
{

    int n = 27;
    count_values(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class Solution
{
//count number of set bits
static int __builtin_popcount(int n)
{
    //count variable
    int count=0;

    while(n>0)
    {
        //if the bit is 1
        if(n%2==1)
        count++;

        n=n/2;
    }
    return count;
}

// function to Count all values of x
static void count_values(int n)
{
    // Count set bits in n
    // by using stl function
    int set_bits = __builtin_popcount(n);

    // count all subset of set bits
    System.out.println((int)Math.pow(2, set_bits));
}

// Driver code
public static void main(String args[])
{

    int n = 27;
    count_values(n);

}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to implement
# above approach

# from math import pow method
from math import pow

# count number of set bits
def __builtin_popcount(n) :

    # count variable
    count = 0

    while n > 0 :

        # if the bit is 1
        if n % 2 == 1 :
            count += 1

        n = n//2

    return count

# function to Count all values of x
def count_values(n) :

    set_bits = __builtin_popcount(n)

    # count all subset of set bits
    print(int(pow(2, set_bits)))

# Driver code
if __name__ == "__main__" :

    n = 27
    count_values(n)

# This code is contributed by
# ANKITRAI1
```

## C#

```
using System;
class GFG
{
// count number of set bits
static int __builtin_popcount(int n)
{
    // count variable
    int count = 0;

    while(n > 0)
    {
        //if the bit is 1
        if(n % 2 == 1)
        count++;

        n = n / 2;
    }
    return count;
}

// function to Count all values of x
static void count_values(int n)
{
    // Count set bits in n
    // by using stl function
    int set_bits = __builtin_popcount(n);

    // count all subset of set bits
    Console.Write((int)Math.Pow(2, set_bits));
}

// Driver code
public static void Main()
{
    int n = 27;
    count_values(n);
}
}

// This code is contributed by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// count number of set bits
function __builtin_popcount($n)
{
    // count variable
    $count = 0;

    while($n > 0)
    {
        //if the bit is 1
        if($n % 2 == 1)
            $count++;

        $n = $n / 2;
    }
    return $count;
}

// function to Count all values of x
function count_values($n)
{
    // Count set bits in n
    // by using stl function
    $set_bits = __builtin_popcount($n);

    // count all subset of set bits
    echo (int)pow(2, $set_bits);
}

// Driver code
$n = 27;
count_values($n);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// count number of set bits
function __builtin_popcount(n)
{
    // count variable
    let count = 0;

    while(n > 0)
    {
        //if the bit is 1
        if(n % 2 == 1)
        count++;

        n = parseInt(n / 2);
    }
    return count;
}

// function to Count all values of x
function count_values(n)
{
    // Count set bits in n
    // by using stl function
    let set_bits = __builtin_popcount(n);

    // count all subset of set bits
    document.write(Math.pow(2, set_bits) + "<br>");
}

// Driver code

    let n = 27;
    count_values(n);

</script>
```

**Output:** 

```
16
```

**时间复杂度:** O(k)，其中 k 为 n 中的设定位数