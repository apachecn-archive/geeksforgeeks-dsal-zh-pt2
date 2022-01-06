# 用和重复替换偶和对后的最小数组大小

> 原文:[https://www . geeksforgeeks . org/重复替换偶数和对后的最小数组大小/sum/](https://www.geeksforgeeks.org/minimum-array-size-after-repeated-replacement-of-even-sum-pair-with-sum/)

给定一个大小为 n 的数组。从序列中选择一对随机元素，使它们的和为偶数，从序列中删除这两个元素，并将它们的和插入序列中，以最小化数组的长度。最后，打印阵列的最小可能大小。
**例:**

```
Input : 88 98 1 7 3
Output : 2
By following above rules --[88, 98, 1, 10]
[98, 88, 1]---[186, 1]--we cannot move further since
186 + 1 = 187, which is not even. So, size = 2.

Input : 7 4 3 2 6
Output : 1
delete 7 and 3, insert 10---[10, 4, 2, 6]
repeating the process of deleting and inserting---[14, 8]--[22]
size of array becomes 1.
```

**方法:**
如果一对数都是偶数或者都是奇数，那么这两个数的和就是偶数。所以，我们只需要计算给定数组中出现的奇数。答案可以是 2，也可以是 1(除此之外什么都没有)，这取决于条件。如果数组中的总赔率是奇数，则打印 2，否则打印 1。

## C++

```
// CPP Program to find minimum size of array
// after repeatedly replacing even sum pair
// with the sum
#include <bits/stdc++.h>
using namespace std;

// function to count and check
// total number of odds
bool check(int a[], int n)
{
    int i, c = 0;

    // loop to count total no. of
    // odd numbers in the array
    if (n == 1)
        return false;

    for (i = 0; i < n; i++)
        if (a[i] & 1)
            c++;   

    if (c & 1)
        return true;

    return false;
}

// Driver program to test
// above function
int main()
{
    int n, a[] = { 7, 4, 3, 2, 6 };
    n = sizeof(a) / sizeof(a[0]);

    // if in total there are
    // odd number of odds
    if (check(a, n))
        cout << 2;
    else
        cout << 1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find minimum size of array
// after repeatedly replacing even sum pair
// with the sum
import java.io.*;
import java.math.*;

class GFG {

    // function to count and check
    // total number of odds
    static boolean check(int a[], int n)
    {
        int i, c = 0;

        // loop to count total no. of
        // odd numbers in the array
        if (n == 1)
            return false;

        for (i = 0; i < n; i++)
            if ((a[i] & 1)==1)
                c++;

        if ((c & 1) == 1)
            return true;

        return false;
    }

    // Driver program to test
    // above function
    public static void main(String args[])
    {
        int n, a[] = { 7, 4, 3, 2, 6 };
        n = a.length;

        // if in total there are
        // odd number of odds
        if (check(a, n))
            System.out.println("2");
        else
            System.out.println("1");
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 Program to illustrate
# the above approach

# function to count and check
# total number of odds
def check(a):
    c = 0
# if length is 1, then we return
# false in order to get output 1
    if len(a) == 1:
        return False
# loop to count number of odds
    for i in a:
        if i & 1:
            c += 1
# if c is odd
    if c & 1:
        return True

    return False

# Driver program to test above function
a = [7, 4, 3, 2, 6]

# if in total there are odd
# number of odd numbers
if(check(a)):
    print(2)
else:
    print(1)
```

## C#

```
// C# Program to find minimum size of array
// after repeatedly replacing even sum pair
// with the sum
using System;

class GFG {

    // function to count and check
    // total number of odds
    static bool check(int []a, int n)
    {
        int i, c = 0;

        // loop to count total no. of
        // odd numbers in the array
        if (n == 1)
            return false;

        for (i = 0; i < n; i++)
            if ((a[i] & 1)==1)
                c++;

        if ((c & 1) == 1)
            return true;

        return false;
    }

    // Driver program
    public static void Main()
    {
        int n;
        int []a = { 7, 4, 3, 2, 6 };
        n = a.Length;

        // if in total there are
        // odd number of odds
        if (check(a, n))
            Console.WriteLine("2");
        else
            Console.WriteLine("1");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find
// minimum size of array
// after repeatedly replacing
// even sum pair with the sum

// function to count and check
// total number of odds
function check( $a, $n)
{
    $i; $c = 0;

    // loop to count total
    // no. of odd numbers
    // in the array
    if ($n == 1)
        return false;

    for ($i = 0; $i < $n; $i++)
        if ($a[$i] & 1)
            $c++;

    if ($c & 1)
        return true;

    return false;
}

// Driver Code
$n; $a = array( 7, 4, 3, 2, 6 );
$n = count($a);

// if in total there are
// odd number of odds
if (check($a, $n))
    echo 2;
else
    echo 1;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find minimum size of array
    // after repeatedly replacing even sum pair
    // with the sum

    // function to count and check
    // total number of odds
    function check(a, n)
    {
        let i, c = 0;

        // loop to count total no. of
        // odd numbers in the array
        if (n == 1)
            return false;

        for (i = 0; i < n; i++)
            if ((a[i] & 1)==1)
                c++;

        if ((c & 1) == 1)
            return true;

        return false;
    }

    let n;
    let a = [7, 4, 3, 2, 6];
    n = a.length;

    // if in total there are
    // odd number of odds
    if (check(a, n))
      document.write("2" + "</br>");
    else
      document.write("1");

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
1
```

时间复杂度 **O(n)**
空间复杂度 **O(1)。**