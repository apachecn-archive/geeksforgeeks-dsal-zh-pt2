# 用偶数和对两个数组中的对进行计数

> 原文:[https://www . geeksforgeeks . org/从偶数和的两个数组中计数对/](https://www.geeksforgeeks.org/count-pairs-from-two-arrays-with-even-sum/)

分别给定 **N** 和 **M** 整数的两个数组 **A[]** 和 **B[]** 。任务是统计从数组 **A[]** 中选择一个元素，从数组 **B[]** 中选择另一个元素形成的无序对的个数，其和为偶数。
**注意**一个元素只会是单个对的一部分。
**举例:**

> **输入:** A[] = {9，14，6，2，11}，B[] = {8，4，7，20}
> **输出:** 4
> {9，7}、{14，8}、{6，4}和{2，20}为有效对。
> **输入:** A[] = {2，4，6}，B[] = {8，10，12}
> **输出:** 3

**方法:**计算两个数组中奇数和偶数的个数，对个数的答案将是 **min(odd1，odd2) + min(even1，even2)** ，因为**(奇数+奇数)=偶数**和**(偶数+偶数)=偶数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return count of required pairs
int count_pairs(int a[], int b[], int n, int m)
{

    // Count of odd and even numbers
    // from both the arrays
    int odd1 = 0, even1 = 0;
    int odd2 = 0, even2 = 0;

    // Find the count of odd and
    // even elements in a[]
    for (int i = 0; i < n; i++) {
        if (a[i] % 2 == 1)
            odd1++;
        else
            even1++;
    }

    // Find the count of odd and
    // even elements in b[]
    for (int i = 0; i < m; i++) {
        if (b[i] % 2 == 1)
            odd2++;
        else
            even2++;
    }

    // Count the number of pairs
    int pairs = min(odd1, odd2) + min(even1, even2);

    // Return the number of pairs
    return pairs;
}

// Driver code
int main()
{
    int a[] = { 9, 14, 6, 2, 11 };
    int b[] = { 8, 4, 7, 20 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = sizeof(b) / sizeof(b[0]);
    cout << count_pairs(a, b, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return count of required pairs
static int count_pairs(int a[], int b[], int n, int m)
{

    // Count of odd and even numbers
    // from both the arrays
    int odd1 = 0, even1 = 0;
    int odd2 = 0, even2 = 0;

    // Find the count of odd and
    // even elements in a[]
    for (int i = 0; i < n; i++)
    {
        if (a[i] % 2 == 1)
            odd1++;
        else
            even1++;
    }

    // Find the count of odd and
    // even elements in b[]
    for (int i = 0; i < m; i++)
    {
        if (b[i] % 2 == 1)
            odd2++;
        else
            even2++;
    }

    // Count the number of pairs
    int pairs = Math.min(odd1, odd2) + Math.min(even1, even2);

    // Return the number of pairs
    return pairs;
}

// Driver code
public static void main (String[] args)
{

    int a[] = { 9, 14, 6, 2, 11 };
    int b[] = { 8, 4, 7, 20 };
    int n = a.length;
    int m = b.length;
    System.out.println (count_pairs(a, b, n, m));

}
}

// This code is contributes by ajit
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return count of required pairs
def count_pairs(a,b,n,m):

    # Count of odd and even numbers
    # from both the arrays

    odd1 = 0
    even1 = 0
    odd2 = 0
    even2 = 0

    # Find the count of odd and
    # even elements in a[]
    for i in range(n):
        if (a[i] % 2 == 1):
            odd1 += 1
        else:
            even1 += 1

    # Find the count of odd and
    # even elements in b[]

    for i in range(m):
        if (b[i] % 2 == 1):
            odd2 += 1
        else:
            even2 += 1

    # Count the number of pairs
    pairs = min(odd1, odd2) + min(even1, even2)

    # Return the number of pairs
    return pairs

# Driver code
if __name__ == '__main__':
    a = [9, 14, 6, 2, 11]
    b = [8, 4, 7, 20]
    n = len(a)
    m = len(b)
    print(count_pairs(a, b, n, m))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return count of required pairs
static int count_pairs(int []a, int []b, int n, int m)
{

    // Count of odd and even numbers
    // from both the arrays
    int odd1 = 0, even1 = 0;
    int odd2 = 0, even2 = 0;

    // Find the count of odd and
    // even elements in a[]
    for (int i = 0; i < n; i++)
    {
        if (a[i] % 2 == 1)
            odd1++;
        else
            even1++;
    }

    // Find the count of odd and
    // even elements in b[]
    for (int i = 0; i < m; i++)
    {
        if (b[i] % 2 == 1)
            odd2++;
        else
            even2++;
    }

    // Count the number of pairs
    int pairs = Math.Min(odd1, odd2) + Math.Min(even1, even2);

    // Return the number of pairs
    return pairs;
}

// Driver code
public static void Main ()
{

    int []a = { 9, 14, 6, 2, 11 };
    int []b = { 8, 4, 7, 20 };
    int n = a.Length;
    int m = b.Length;
    Console.WriteLine (count_pairs(a, b, n, m));

}
}

// This code is contributes by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return count of required pairs
function count_pairs($a, $b, $n, $m)
{

    // Count of odd and even numbers
    // from both the arrays
    $odd1 = 0; $even1 = 0;
    $odd2 = 0; $even2 = 0;

    // Find the count of odd and
    // even elements in a[]
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] % 2 == 1)
            $odd1++;
        else
            $even1++;
    }

    // Find the count of odd and
    // even elements in b[]
    for ($i = 0; $i < $m; $i++)
    {
        if ($b[$i] % 2 == 1)
            $odd2++;
        else
            $even2++;
    }

    // Count the number of pairs
    $pairs = min($odd1, $odd2) + min($even1, $even2);

    // Return the number of pairs
    return $pairs;
}

// Driver code
$a = array( 9, 14, 6, 2, 11 );
$b = array( 8, 4, 7, 20 );
$n = count($a);
$m = count($b);

echo count_pairs($a, $b, $n, $m);

// This code is contributes by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to return count of required pairs
    function count_pairs(a , b , n , m)
    {

        // Count of odd and even numbers
        // from both the arrays
        var odd1 = 0, even1 = 0;
        var odd2 = 0, even2 = 0;

        // Find the count of odd and
        // even elements in a
        for (i = 0; i < n; i++) {
            if (a[i] % 2 == 1)
                odd1++;
            else
                even1++;
        }

        // Find the count of odd and
        // even elements in b
        for (i = 0; i < m; i++) {
            if (b[i] % 2 == 1)
                odd2++;
            else
                even2++;
        }

        // Count the number of pairs
        var pairs = Math.min(odd1, odd2) +
                    Math.min(even1, even2);

        // Return the number of pairs
        return pairs;
    }

    // Driver code

        var a = [ 9, 14, 6, 2, 11 ];
        var b = [ 8, 4, 7, 20 ];
        var n = a.length;
        var m = b.length;
        document.write(count_pairs(a, b, n, m));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
4
```