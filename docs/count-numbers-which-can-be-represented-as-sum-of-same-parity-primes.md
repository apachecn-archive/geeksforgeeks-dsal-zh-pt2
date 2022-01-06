# 计数可以表示为相同奇偶素数之和的数

> 原文:[https://www . geesforgeks . org/count-numbers-可以表示为相同奇偶素数之和/](https://www.geeksforgeeks.org/count-numbers-which-can-be-represented-as-sum-of-same-parity-primes/)

给定一组正整数，你必须计算有多少个数可以表示为相同奇偶素数的和(可以相同)

**示例:**

```
Input : arr[] = {1, 3, 4, 6}
Output : 2
4 = 2+2, 6 = 3+3

Input : arr[] = {4, 98, 0, 36, 51}
Output : 3
```

1.如果两个相同奇偶性的数相加，那么它们总是偶数，所以数组中的所有奇数永远不会有助于答案。
2。谈 0 和 2 都不能用同一个奇偶素数的和来表示。
3。其余的数字将有助于答案(参考[https://www . geeksforgeeks . org/program-for-goldbachs-猜想-两个素数的给定和/](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/) )

因此，我们只需迭代整个数组，找出不等于 0 和 2 的偶数元素的数量。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to calculate count
int calculate(int* array, int size)
{
    int count = 0;

    for (int i = 0; i < size; i++)
        if (array[i] % 2 == 0 &&
            array[i] != 0 &&
            array[i] != 2)
            count++;

    return count;
}

// Driver Code
int main()
{
    int a[] = { 1, 3, 4, 6 };
    int size = sizeof(a) / sizeof(a[0]);
    cout << calculate(a, size);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count numbers
// which can be represented as
// sum of same parity primes
import java.util.*;

class GFG
{
// Function to calculate count
public static int calculate(int ar[],
                            int size)
{
    int count = 0;

    for (int i = 0; i < size; i++)
        if (ar[i] % 2 == 0 &&
            ar[i] != 0 &&
            ar[i] != 2)
            count++;

    return count;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 3, 4, 6 };
    int size = a.length;
    System.out.print(calculate(a, size));
}
}

// This code is contributed
// by ankita_saini
```

## 蟒蛇 3

```
# Function to calculate count
def calculate(array, size):

    count = 0

    for i in range(size):
        if (array[i] % 2 == 0 and
            array[i] != 0 and
            array[i] != 2 ):
            count += 1

    return count

# Driver Code
if __name__ == "__main__":
    a = [ 1, 3, 4, 6 ]
    size = len(a)
    print(calculate(a, size))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to Count numbers
// which can be represented as
// sum of same parity primes
using System;

class GFG
{
// Function to calculate count
public static int calculate(int []ar,
                            int size)
{
    int count = 0;

    for (int i = 0; i < size; i++)
        if (ar[i] % 2 == 0 &&
            ar[i] != 0 &&
            ar[i] != 2)
            count++;

    return count;
}

// Driver code
static public void Main (String []args)
{
    int []a = { 1, 3, 4, 6 };
    int size = a.Length;
    Console.WriteLine(calculate(a, size));
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to calculate count
function calculate(&$array, $size)
{
    $count = 0;

    for ($i = 0; $i < $size; $i++)
        if ($array[$i] % 2 == 0 &&
            $array[$i] != 0 &&
            $array[$i] != 2)
            $count++;

    return $count;
}

// Driver Code
$a = array(1, 3, 4, 6 );
$size = sizeof($a);
echo calculate($a, $size);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to Count numbers
// which can be represented as
// sum of same parity primes

// Function to calculate count
function calculate(ar, size)
{
    var count = 0;

    for(i = 0; i < size; i++)
        if (ar[i] % 2 == 0 &&
            ar[i] != 0 && ar[i] != 2)
            count++;

    return count;
}

// Driver code
var a = [ 1, 3, 4, 6 ];
var size = a.length;

document.write(calculate(a, size));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
2
```