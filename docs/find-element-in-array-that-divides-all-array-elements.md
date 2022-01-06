# 在数组中找到分割所有数组元素的元素

> 原文:[https://www . geeksforgeeks . org/find-array-in-element-the-division-all-array-elements/](https://www.geeksforgeeks.org/find-element-in-array-that-divides-all-array-elements/)

给定一个非负整数的数组。在数组中找到这样的元素，所有的数组元素都可以被它整除。
**例:**

```
Input : arr[] = {2, 2, 4}
Output : 2

Input : arr[] = {2, 1, 3, 1, 6}
Output : 1

Input: arr[] = {2, 3, 5}
Output : -1
```

方法是计算整个数组的 GCD，然后检查是否存在与数组的 GCD 相等的元素。为了计算整个数组的 gcd，我们将使用 [**欧几里德算法**](https://www.geeksforgeeks.org/gcd-two-array-numbers/) 。

## C++

```
// CPP program to find such number in the array
// that all array elements are divisible by it
#include <bits/stdc++.h>
using namespace std;

// Returns gcd of two numbers.
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to return the
// desired number if exists
int findNumber(int arr[], int n)
{
    // Find GCD of array
    int ans = arr[0];
    for (int i = 0; i < n; i++)
        ans = gcd(ans, arr[i]);

    // Check if GCD is present in array
    for (int i = 0; i < n; i++)
        if (arr[i] == ans)
            return ans;

    return -1;
}

// Driver Function
int main()
{
    int arr[] = { 2, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findNumber(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find such number in
// the array that all array elements
// are divisible by it
import java.io.*;

class GFG {

    // Returns GCD of two numbers
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to return the desired
    // number if exists
    static int findNumber(int arr[], int n)
    {
        // Find GCD of array
        int ans = arr[0];
        for (int i = 0; i < n; i++)
            ans = gcd(ans, arr[i]);

        // Check if GCD is present in array
        for (int i = 0; i < n; i++)
            if (arr[i] == ans)
                return ans;

        return -1;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 2, 2, 4 };
        int n = arr.length;
        System.out.println(findNumber(arr, n));
    }
}

// This code is contributed by Nikita Tiwari
```

## 蟒蛇 3

```
# Python3 program to find such number
# in the array that all array
# elements are divisible by it

# Returns GCD of two numbers
def gcd (a, b) :
    if (a == 0) :
        return b

    return gcd (b % a, a)

# Function to return the desired
# number if exists
def findNumber (arr, n) :

    # Find GCD of array
    ans = arr[0]
    for i in range(0, n) :
        ans = gcd (ans, arr[i])

    # Check if GCD is present in array
    for i in range(0, n) :
        if (arr[i] == ans) :
            return ans

    return -1

# Driver Code
arr = [2, 2, 4];
n = len(arr)
print(findNumber(arr, n))

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# program to find such number in
// the array that all array elements
// are divisible by it
using System;

class GFG {

    // Returns GCD of two numbers
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to return the desired
    // number if exists
    static int findNumber(int[] arr, int n)
    {
        // Find GCD of array
        int ans = arr[0];
        for (int i = 0; i < n; i++)
            ans = gcd(ans, arr[i]);

        // Check if GCD is present in array
        for (int i = 0; i < n; i++)
            if (arr[i] == ans)
                return ans;

        return -1;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 2, 4 };
        int n = arr.Length;
        Console.WriteLine(findNumber(arr, n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find such
// number in the array that
// all array elements are
// divisible by it

// Returns gcd of two numbers
function gcd ($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd ($b % $a, $a);
}

// Function to return the
// desired number if exists
function findNumber ($arr, $n)
{
    // Find GCD of array
    $ans = $arr[0];
    for ($i = 0; $i < $n; $i++)
        $ans = gcd ($ans, $arr[$i]);

    // Check if GCD is
    // present in array
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] == $ans)        
            return $ans;    

    return -1;
}

// Driver Code
$arr =array (2, 2, 4);
$n = sizeof($arr);
echo findNumber($arr, $n), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find such number in the array
    // that all array elements are divisible by it

    // Returns gcd of two numbers.
    function gcd(a, b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to return the
    // desired number if exists
    function findNumber(arr, n)
    {
        // Find GCD of array
        let ans = arr[0];
        for (let i = 0; i < n; i++)
            ans = gcd(ans, arr[i]);

        // Check if GCD is present in array
        for (let i = 0; i < n; i++)
            if (arr[i] == ans)
                return ans;

        return -1;
    }

    let arr = [ 2, 2, 4 ];
    let n = arr.length;
    document.write(findNumber(arr, n));

</script>
```

**输出:**

```
2
```