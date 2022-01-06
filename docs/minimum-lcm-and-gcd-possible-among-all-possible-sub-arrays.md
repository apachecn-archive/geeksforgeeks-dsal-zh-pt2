# 所有可能的子阵列中可能的最小 LCM 和 GCD

> 原文:[https://www . geesforgeks . org/minimum-LCM-and-gcd-所有可能的子阵列中的可能/](https://www.geeksforgeeks.org/minimum-lcm-and-gcd-possible-among-all-possible-sub-arrays/)

给定一个正整数数组**arr[]****N**，任务是找到所有可能的子数组元素之间的最小值 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 和 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。
**举例:**

> **输入:** arr[] = {4，4，8}
> **输出:** LCM = 4，GCD = 4
> 所有可能的子阵列为:
> {4} - > LCM = 4，GCD = 4
> {8} - > LCM = 8，GCD = 8
> {4，8} - > LCM = 8，GCD = 4
> **输入:**arr[=]

**进场:**我们要贪婪地进场这个问题。很明显，当我们减少元素数量时，LCM 会变小，当我们增加元素数量时，GCD 会变小。因此，我们将取数组中最小的元素，它是一个元素，并且是所需的 LCM。现在对于 GCD，最小 GCD 将是数组所有元素的 GCD。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum GCD
// among all subarrays
int minGCD(int arr[], int n)
{

    int minGCD = 0;

    // Minimum GCD among all sub-arrays will be
    // the GCD of all the elements of the array
    for (int i = 0; i < n; i++)
        minGCD = __gcd(minGCD, arr[i]);

    return minGCD;
}

// Function to return minimum LCM
// among all subarrays
int minLCM(int arr[], int n)
{

    int minLCM = arr[0];

    // Minimum LCM among all sub-arrays will be
    // the minimum element from the array
    for (int i = 1; i < n; i++)
        minLCM = min(minLCM, arr[i]);

    return minLCM;
}

// Driver code
int main()
{

    int arr[] = { 2, 66, 14, 521 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "LCM = " << minLCM(arr, n)
         << ", GCD = " << minGCD(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
// Function to return minimum GCD
// among all subarrays
static int __gcd(int a, int b)
{
    if (a == 0)
        return b;
    return __gcd(b % a, a);
}
static int minGCD(int arr[], int n)
{

    int minGCD = 0;

    // Minimum GCD among all sub-arrays will be
    // the GCD of all the elements of the array
    for (int i = 0; i < n; i++)
        minGCD = __gcd(minGCD, arr[i]);

    return minGCD;
}

// Function to return minimum LCM
// among all subarrays
static int minLCM(int arr[], int n)
{

    int minLCM = arr[0];

    // Minimum LCM among all sub-arrays will be
    // the minimum element from the array
    for (int i = 1; i < n; i++)
        minLCM = Math.min(minLCM, arr[i]);

    return minLCM;
}

// Driver code
public static void main(String[] args)
{

    int arr[] = { 2, 66, 14, 521 };
    int n = arr.length;

    System.out.println("LCM = " + minLCM(arr, n)
        + " GCD = "+minGCD(arr, n));

}
}
// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return minimum GCD
# among all subarrays
def minGCD(arr, n) :

    minGCD = 0;

    # Minimum GCD among all sub-arrays
    # will be the GCD of all the elements
    # of the array
    for i in range(n) :
        minGCD = gcd(minGCD, arr[i]);

    return minGCD;

# Function to return minimum LCM
# among all subarrays
def minLCM(arr, n) :

    minLCM = arr[0];

    # Minimum LCM among all sub-arrays 
    # will be the minimum element from
    # the array
    for i in range(1, n) :
        minLCM = min(minLCM, arr[i]);

    return minLCM;

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 66, 14, 521 ];
    n = len(arr);

    print("LCM = ", minLCM(arr, n),
          ", GCD =", minGCD(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return minimum GCD
    // among all subarrays
    static int __gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return __gcd(b % a, a);
    }
    static int minGCD(int [] arr, int n)
    {
        int minGCD = 0;

        // Minimum GCD among all sub-arrays
        // will be the GCD of all the
        // elements of the array
        for (int i = 0; i < n; i++)
            minGCD = __gcd(minGCD, arr[i]);

        return minGCD;
    }

    // Function to return minimum LCM
    // among all subarrays
    static int minLCM(int [] arr, int n)
    {

        int minLCM = arr[0];

        // Minimum LCM among all sub-arrays
        // will be the minimum element from
        // the array
        for (int i = 1; i < n; i++)
            minLCM = Math.Min(minLCM, arr[i]);

        return minLCM;
    }

    // Driver code
    public static void Main()
    {

        int [] arr = { 2, 66, 14, 521 };
        int n = arr.Length;

        Console.WriteLine("LCM = " + minLCM(arr, n) +      
                          ", GCD = " + minGCD(arr, n));
    }
}

// This code is contributed by ihritik.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return minimum GCD
// among all subarrays
function __gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return __gcd($b % $a, $a);
}
function minGCD($arr, $n)
{
    $minGCD = 0;

    // Minimum GCD among all sub-arrays
    // will be the GCD of all the
    // elements of the array
    for ($i = 0; $i < $n; $i++)
        $minGCD = __gcd($minGCD,
                        $arr[$i]);

    return $minGCD;
}

// Function to return minimum LCM
// among all subarrays
function minLCM($arr, $n)
{
    $minLCM = $arr[0];

    // Minimum LCM among all sub-arrays
    // will be the minimum element from
    // the array
    for ($i = 1; $i < $n; $i++)
        $minLCM = min($minLCM,
                      $arr[$i]);

    return $minLCM;
}

// Driver code
$arr = array(2, 66, 14, 521 );
$n = sizeof($arr);

echo "LCM = " . minLCM($arr, $n) . ", ";
echo "GCD = " . minGCD($arr, $n);

// This code is contributed by ihritik.
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to return minimum GCD
    // among all subarrays
    function __gcd(a , b) {
        if (a == 0)
            return b;
        return __gcd(b % a, a);
    }

    function minGCD(arr , n) {

        var minGCD = 0;

        // Minimum GCD among all sub-arrays will be
        // the GCD of all the elements of the array
        for (i = 0; i < n; i++)
            minGCD = __gcd(minGCD, arr[i]);

        return minGCD;
    }

    // Function to return minimum LCM
    // among all subarrays
    function minLCM(arr , n) {

        var minLCM = arr[0];

        // Minimum LCM among all sub-arrays will be
        // the minimum element from the array
        for (i = 1; i < n; i++)
            minLCM = Math.min(minLCM, arr[i]);

        return minLCM;
    }

    // Driver code
        var arr = [ 2, 66, 14, 521 ];
        var n = arr.length;
        document.write("LCM = " + minLCM(arr, n) + " GCD = " + minGCD(arr, n));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
LCM = 2, GCD = 1
```

**时间复杂度:** O(N)