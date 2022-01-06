# 使数组按递增顺序排列的最小增量操作

> 原文:[https://www . geeksforgeeks . org/最小增量操作以递增顺序制造阵列/](https://www.geeksforgeeks.org/minimum-increment-operations-to-make-the-array-in-increasing-order/)

给定一个大小为 N 和 x 的数组。找到使数组按递增顺序排列所需的最小移动量。在每次移动中，可以向数组中的任何元素添加 X。

**示例**:

```
Input : a = { 1, 3, 3, 2 }, X = 2
Output : 3
Explanation : Modified array is { 1, 3, 5, 6 }

Input : a = { 3, 5, 6 }, X = 5
Output : 0
```

**观察**:

> 让我们取两个数字 a 和 b。a > = b，并将其转换为 a < b by adding some number X. 
> 所以，a<b+k * X
> (a–b)/X<k
> 所以，k 的最小可能值是(a–b)/X+1。

**接近**:

```
Iterate over the given array and take two numbers when a[i] >= a[i-1] 
and apply above observation.
```

下面是上述方法的实现:

## C++

```
// C++ program to find minimum moves required
// to make the array in increasing order
#include <bits/stdc++.h>
using namespace std;

// function to find minimum moves required
// to make the array in increasing order
int MinimumMoves(int a[], int n, int x)
{
    // to store answer
    int ans = 0;

    // iterate over an array
    for (int i = 1; i < n; i++) {

        // non- increasing order
        if (a[i] <= a[i - 1]) {
            int p = (a[i - 1] - a[i]) / x + 1;

            // add moves to answer
            ans += p;

            // increase the element
            a[i] += p * x;
        }
    }

    // return required answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 3, 2 };
    int x = 2;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << MinimumMoves(arr, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum moves required
// to make the array in increasing order
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{
// function to find minimum moves required
// to make the array in increasing order
static int MinimumMoves(int a[], int n, int x)
{
    // to store answer
    int ans = 0;

    // iterate over an array
    for (int i = 1; i < n; i++) {

        // non- increasing order
        if (a[i] <= a[i - 1]) {
            int p = (a[i - 1] - a[i]) / x + 1;

            // add moves to answer
            ans += p;

            // increase the element
            a[i] += p * x;
        }
    }

    // return required answer
    return ans;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 3, 3, 2 };
    int x = 2;
    int n = arr.length;

    System.out.println(MinimumMoves(arr, n, x));

}
}
```

## 蟒蛇 3

```
# Python3 program to find minimum
# moves required to make the array
# in increasing order

# function to find minimum moves required
# to make the array in increasing order
def MinimumMoves(a, n, x) :

    # to store answer
    ans = 0

    # iterate over an array
    for i in range(1, n) :

        # non- increasing order
        if a[i] <= a[i - 1] :

            p = (a[i - 1] - a[i]) // x + 1

            # add moves to answer
            ans += p

            # increase the element
            a[i] += p * x

    # return required answer
    return ans

# Driver code    
if __name__ == "__main__" :

    arr = [1, 3, 3, 2]
    x = 2
    n = len(arr)

    print(MinimumMoves(arr, n, x))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find minimum moves required
// to make the array in increasing order
using System;

class GFG {

// function to find minimum moves required
// to make the array in increasing order
static int MinimumMoves(int[] a, int n, int x)
{

    // to store answer
    int ans = 0;

    // iterate over an array
    for (int i = 1; i < n; i++) {

        // non- increasing order
        if (a[i] <= a[i - 1]) {

            int p = (a[i - 1] - a[i]) / x + 1;

            // add moves to answer
            ans += p;

            // increase the element
            a[i] += p * x;
        }
    }

    // return required answer
    return ans;
}

// Driver code
public static void Main()
{

    int[] arr = {1, 3, 3, 2};
    int x = 2;
    int n = arr.Length;

    Console.Write(MinimumMoves(arr, n, x));

}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// moves required to make the
// array in increasing order

// function to find minimum
// moves required to make the
// array in increasing order
function MinimumMoves(&$a, $n, $x)
{
    // to store answer
    $ans = 0;

    // iterate over an array
    for ($i = 1; $i < $n; $i++)
    {

        // non- increasing order
        if ($a[$i] <= $a[$i - 1])
        {
            $p = ($a[$i - 1] - $a[$i]) / $x + 1;

            // add moves to answer
            $ans += $p;

            // increase the element
            $a[$i] += $p * $x;
        }
    }

    // return required answer
    return $ans;
}

// Driver code
$arr = array(1, 3, 3, 2 );
$x = 2;
$n = sizeof($arr);

echo ((int)MinimumMoves($arr, $n, $x));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum
// moves required to make the array in
// increasing order   

// Function to find minimum moves required
// to make the array in increasing order
function MinimumMoves(a, n, x)
{

    // To store answer
    var ans = 0;

    // Tterate over an array
    for(i = 1; i < n; i++)
    {

        // Non- increasing order
        if (a[i] <= a[i - 1])
        {
            var p = parseInt((a[i - 1] -
                              a[i]) / x + 1);

            // Add moves to answer
            ans += p;

            // Increase the element
            a[i] += p * x;
        }
    }

    // Return required answer
    return ans;
}

// Driver code
var arr = [ 1, 3, 3, 2 ];
var x = 2;
var n = arr.length;

document.write(MinimumMoves(arr, n, x));

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
3
```