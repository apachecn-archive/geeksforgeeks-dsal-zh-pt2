# 获得三角形非负面积所需的边的最小增量

> 原文:[https://www . geesforgeks . org/最小边增量-需要获得非负三角形面积/](https://www.geeksforgeeks.org/minimum-increment-in-the-sides-required-to-get-non-negative-area-of-a-triangle/)

给定三角形的三条边，求三角形边长的最小增量，使三角形的面积非负。
**例:**

> **输入** : a = 3，b = 4，c = 10
> **输出** : 3
> 给定边，面积为负。
> 如果 a 增加到 5，b 增加到 5，那么面积变成 0，不是负数。
> **输入** : a = 6，b = 6，c = 10
> **输出** : 2

Ap **proach:** 由于任何三角形的面积都是非负的，如果最小的两条边的和总是大于或等于第三条边，因此应遵循以下步骤来解决上述问题:

*   按照递增的顺序排列三面。
*   检查前两边之和是否大于等于第三边，如果是，则答案为 0。
*   如果不是，那么答案就是(第三面–(第一面+第二面))。

下面是给定方法的实现。

## C++

```
// C++ program to find Minimum
// increase in sides to get
// non-negative area of a triangle
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum increase in side
// lengths of the triangle
int minimumIncrease(int a, int b, int c)
{
    // push the three sides to a array
    int arr[] = { a, b, c };

    // sort the array
    sort(arr, arr + 3);

    // check if sum is greater than third side
    if (arr[0] + arr[1] >= arr[2])
        return 0;
    else
        return arr[2] - (arr[0] + arr[1]);
}

// Driver Code
int main()
{
    int a = 3, b = 5, c = 10;

    cout << minimumIncrease(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Minimum
// increment in the sides required
// to get non-negative area of
// a triangle
import java.util.*;
class GFG
{
static int minimumIncrease(int a, int b,
                           int c)
{
    // push the three sides
    // to a array
    int arr[] = { a, b, c };

    // sort the array
    Arrays.sort(arr);

    // check if sum is greater
    // than third side
    if (arr[0] + arr[1] >= arr[2])
        return 0;
    else
        return arr[2] - (arr[0] + arr[1]);
}

// Driver Code
public static void main (String[] args)
{
    int a = 3, b = 5, c = 10;

    System.out.println(minimumIncrease(a, b, c));
}
}

// This code is contributed
// by Shashank
```

## 蟒蛇 3

```
# Python program to find Minimum
# increase in sides to get
# non-negative area of a triangle

# Function to return the
# minimum increase in side
# lengths of the triangle
def minimumIncrease(a, b, c) :

    # push the three sides
    # to a array
    arr = [ a, b, c ]

    # sort the array
    arr.sort()

    # check if sum is greater
    # than third side
    if arr[0] + arr[1] >= arr[2] :
        return 0

    else :
        return arr[2] - (arr[0] + arr[1])

# Driver code    
if __name__ == "__main__" :

    a, b, c = 3, 5, 10
    print(minimumIncrease(a, b, c))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# Program to find Minimum
// increment in the sides required
// to get non-negative area of
// a triangle
using System;

class GFG
{
static int minimumIncrease(int a, int b,
                           int c)
{
    // push the three sides
    // to a array
    int[] arr = { a, b, c };

    // sort the array
    Array.Sort(arr);

    // check if sum is greater
    // than third side
    if (arr[0] + arr[1] >= arr[2])
        return 0;
    else
        return arr[2] - (arr[0] + arr[1]);
}

// Driver Code
public static void Main ()
{
    int a = 3, b = 5, c = 10;

    Console.Write(minimumIncrease(a, b, c));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Minimum
// increase in sides to get
// non-negative area of a triangle

// Function to return the
// minimum increase in side
// lengths of the triangle
function minimumIncrease($a, $b, $c)
{
    // push the three sides to a array
    $arr = array($a, $b, $c );

    // sort the array
    sort($arr);

    // check if sum is greater
    // than third side
    if ($arr[0] + $arr[1] >= $arr[2])
        return 0;
    else
        return $arr[2] - ($arr[0] + $arr[1]);
}

// Driver Code
$a = 3;
$b = 5;
$c = 10;

echo minimumIncrease($a, $b, $c);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript Program to find Minimum
// increment in the sides required
// to get non-negative area of
// a triangle

    function minimumIncrease(a , b , c)
    {
        // push the three sides
        // to a array
        var arr = [ a, b, c ];

        // sort the array
        arr.sort((a,b)=>a-b);

        // check if sum is greater
        // than third side
        if (arr[0] + arr[1] >= arr[2])
            return 0;
        else
            return arr[2] - (arr[0] + arr[1]);
    }

    // Driver Code

        var a = 3, b = 5, c = 10;

        document.write(minimumIncrease(a, b, c));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
2
```