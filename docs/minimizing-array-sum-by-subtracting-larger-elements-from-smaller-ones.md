# 通过从较小的元素中减去较大的元素来最小化数组和

> 原文:[https://www . geeksforgeeks . org/将较小元素减去较大元素的最小化数组总和/](https://www.geeksforgeeks.org/minimizing-array-sum-by-subtracting-larger-elements-from-smaller-ones/)

给定 n 个元素执行的数组，我们需要最小化数组和。我们可以多次执行以下操作。

*   从数组中选择任意两个元素，比如 A 和 B，其中 A > B，然后从 A 中减去 B

**例:**

```

Input : 1
        arr[] = 1
Output : 1
There is no need to apply the above operation
because there is only a single number that is 1.
Hence, the minimum sum of the array is 1.

Input : 3
        arr[] = 2 4 6
Output : 6
Perform the following operations:-
subtract 2 from 4 then the array becomes 2 2 6
subtract 2 (at 2nd position) from 6 the array 
becomes 2 2 4
subtract 2 (at 2nd position) from 4 the array
becomes 2 2 2
Now the sum of the array will be 6.
```

**方法:**应用所有运算后，给定数组中的所有值将相等，否则我们仍然可以选择两个数字 A 和 B，这样 A >和 B 可以进一步减少总和。应用所有操作后，每个元素的值将等于数组的 gcd，即 ans。
因此，最小可能和等于 n * ans。
以下是上述办法的实施:

## C++

```
// CPP program to find the minimum
// sum of the array.
#include <bits/stdc++.h>
using namespace std;

// returns gcd of two numbers
int gcd(int a, int b)
{
    if (b == 0)
        return a;   
    return gcd(b, a % b);
}

// returns the gcd of the array.
int gcdofArray(int arr[], int n)
{
    int ans = arr[0];
    for (int i = 1; i < n; i++)
        ans = gcd(ans, arr[i]);   
    return ans;
}

// Driver Function
int main()
{
    int arr[] = { 2, 4, 6 }, n;
    n = sizeof(arr) / sizeof(arr[0]);
    cout << n * gcdofArray(arr, n)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find the minimum
// sum of the array.
import java.io.*;

class GFG {

    // returns gcd of two numbers
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // returns the gcd of the array.
    static int gcdofArray(int arr[], int n)
    {
        int ans = arr[0];
        for (int i = 1; i < n; i++)
            ans = gcd(ans, arr[i]);
        return ans;
    }

    // Driver Function
    public static void main (String[] args)
    {
        int arr[] = { 2, 4, 6 }, n;
        n = arr.length;
        System.out.println( n * gcdofArray(arr, n)) ;

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 code to find the minimum
# sum of the array.

# returns gcd of two numbers
def gcd(a, b):
    if b == 0:
        return a
    return gcd(b, a % b)

# returns the gcd of the array.
def gcdofArray(arr, n):
    ans = arr[0]
    for i in range(n):
        ans = gcd(ans, arr[i])
    return ans

# Driver Code
arr = [ 2, 4, 6 ]
n = len(arr)
print(n * gcdofArray(arr, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to find the minimum
// sum of the array.
using System;

class GFG
{

    // returns gcd of two numbers
    static int gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // returns the gcd of the array.
    static int gcdofArray(int []arr, int n)
    {
        int ans = arr[0];
        for (int i = 1; i < n; i++)
            ans = gcd(ans, arr[i]);
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {2, 4, 6};
        int n;
        n = arr.Length;
        Console.WriteLine(n * gcdofArray(arr, n)) ;

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum
// sum of the array.

// returns gcd of two numbers
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return gcd($b, $a % $b);
}

// returns the gcd of the array.
function gcdofArray($arr, $n)
{
    $ans = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $ans = gcd($ans, $arr[$i]);
    return $ans;
}

// Driver Code
$arr = array( 2, 4, 6 );
$n = count($arr);
echo $n * gcdofArray($arr, $n), "\n";

// This code is contributed by Sach
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the minimum
    // sum of the array.

    // returns gcd of two numbers
    function gcd(a, b)
    {
        if (b == 0)
            return a;   
        return gcd(b, a % b);
    }

    // returns the gcd of the array.
    function gcdofArray(arr, n)
    {
        let ans = arr[0];
        for (let i = 1; i < n; i++)
            ans = gcd(ans, arr[i]);   
        return ans;
    }

    let arr = [ 2, 4, 6 ], n;
    n = arr.length;
    document.write(n * gcdofArray(arr, n));

</script>
```

**输出:**

```
6
```