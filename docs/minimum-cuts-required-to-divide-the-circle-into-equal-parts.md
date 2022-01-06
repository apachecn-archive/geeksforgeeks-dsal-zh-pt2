# 将圆分成相等部分所需的最小切口

> 原文:[https://www . geesforgeks . org/将圆分成相等部分所需的最小切割数/](https://www.geeksforgeeks.org/minimum-cuts-required-to-divide-the-circle-into-equal-parts/)

给定一个数组 *arr* ，该数组表示一个圆被切割的不同角度，任务是确定需要更多切割的最小次数，以便将圆分成相等的部分。
**注:**数组已经按升序排序。
**例:**

> **输入:** arr[] = {0，90，180，270}
> **输出:** 0
> 由于圆已经被分成四个相等的部分，因此不再需要切割。
> **输入:** arr[] = {90，210}
> **输出:** 1
> 需要 330 度单次切割，将圆分成三等分。

**方法:**思路是计算数组中两个元素连续差得到的所有值的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)，以便找到圆可以划分的部分的最大(减少所需的切割次数)可能尺寸。

*   首先将数组前两个值的绝对差值存储在名为*因子= arr[1]–arr[0]*的变量中。

*   现在遍历数组从索引 *2* 到 *N-1* ，对于每个元素更新*因子*为*因子= gcd(因子，arr[I]–arr[I-1])*。

*   然后对于最后一个元素更新*因子= gcd(因子，360–arr[N-1]+arr[0])*。

*   最后，所需的总切割量为 *(360 /因子)–N*。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of cuts
// required to divide a circle into equal parts
int Parts(int Arr[], int N)
{
    int factor = Arr[1] - Arr[0];
    for (int i = 2; i < N; i++) {
        factor = __gcd(factor, Arr[i] - Arr[i - 1]);
    }

    // Since last part is connected with the first
    factor = __gcd(factor, 360 - Arr[N - 1] + Arr[0]);

    int cuts = (360 / factor) - N;

    return cuts;
}

// Driver code
int main()
{
    int Arr[] = { 0, 1 };
    int N = sizeof(Arr) / sizeof(Arr[0]);

    cout << Parts(Arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.io.*;

class GFG {
    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0 
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

// Function to return the number of cuts
// required to divide a circle into equal parts
static int Parts(int Arr[], int N)
{
    int factor = Arr[1] - Arr[0];
    for (int i = 2; i < N; i++) {
        factor = __gcd(factor, Arr[i] - Arr[i - 1]);
    }

    // Since last part is connected with the first
    factor = __gcd(factor, 360 - Arr[N - 1] + Arr[0]);

    int cuts = (360 / factor) - N;

    return cuts;
}

// Driver code

    public static void main (String[] args) {
    int Arr[] = { 0, 1 };
    int N = Arr.length;

    System.out.println( Parts(Arr, N));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach
import math

# Function to return the number
# of cuts required to divide a
# circle into equal parts
def Parts(Arr, N):

    factor = Arr[1] - Arr[0]
    for i in range(2, N) :
        factor = math.gcd(factor, Arr[i] -
                                  Arr[i - 1])

    # Since last part is connected
    # with the first
    factor = math.gcd(factor, 360 -
                      Arr[N - 1] + Arr[0])

    cuts = (360 // factor) - N

    return cuts

# Driver code
if __name__ == "__main__":
    Arr = [ 0, 1 ]
    N = len(Arr)

    print( Parts(Arr, N))

# This code is contributed
# by ChitraNayal
```

## C#

```
//  C# implementation of above approach

using System;

class GFG
{
   // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0 
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

    // Function to return the number of cuts
    // required to divide a circle into equal parts
    static int Parts(int []Arr, int N)
    {
        int factor = Arr[1] - Arr[0];
        for (int i = 2; i < N; i++) {
            factor = __gcd(factor, Arr[i] - Arr[i - 1]);
        }

        // Since last part is connected with the first
        factor = __gcd(factor, 360 - Arr[N - 1] + Arr[0]);

        int cuts = (360 / factor) - N;

        return cuts;
    }

    // Driver code
    static void Main()
    {
            int []Arr = { 0, 1 };
            int N = Arr.Length;
            Console.WriteLine(Parts(Arr, N));
    }
}
// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Recursive function to return
// gcd of a and b
function __gcd( $a, $b)
{
    // Everything divides 0
    if ($a == 0)
        return $b;
    if ($b == 0)
        return $a;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);
    return __gcd($a, $b - $a);
}

// Function to return the number of cuts
function Parts($Arr, $N)
{
    $factor = $Arr[1] - $Arr[0];
    for ($i = 2; $i < $N; $i++)
    {
        $factor = __gcd($factor, $Arr[$i] -
                                 $Arr[$i - 1]);
    }

    // Since last part is connected
    // with the first
    $factor = __gcd($factor, 360 -
                    $Arr[$N - 1] + $Arr[0]);

    $cuts = (360 / $factor) - $N;

    return $cuts;
}

// Driver code
$Arr = array( 0, 1 );
$N = sizeof($Arr);
echo (Parts($Arr, $N));

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Recursive function to return gcd of a and b
function __gcd(a, b)
    {
        // Everything divides 0 
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

// Function to return the number of cuts
// required to divide a circle into equal parts
function Parts(Arr, N)
{
    var factor = Arr[1] - Arr[0];
    for (var i = 2; i < N; i++) {
        factor = __gcd(factor, Arr[i] - Arr[i - 1]);
    }

    // Since last part is connected with the first
    factor = __gcd(factor, 360 - Arr[N - 1] + Arr[0]);

    var cuts = (360 / factor) - N;

    return cuts;
}

// Driver code
var Arr = [ 0, 1 ];
var N = Arr.length;
document.write( Parts(Arr, N));

</script>
```

**Output:** 

```
358
```