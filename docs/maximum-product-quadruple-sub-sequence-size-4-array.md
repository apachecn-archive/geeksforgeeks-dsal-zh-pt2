# 数组中最大乘积四倍(大小为 4 的子序列)

> 原文:[https://www . geesforgeks . org/maximum-product-四联-子序列-size-4-array/](https://www.geeksforgeeks.org/maximum-product-quadruple-sub-sequence-size-4-array/)

给定一个整数数组，求数组中四的最大乘积。
**例:**

```
Input:  [10, 3, 5, 6, 20]
Output: 6000
Multiplication of 10, 5, 6 and 20

Input:  [-10, -3, -5, -6, -20]
Output: 6000

Input:  [1, -4, 3, -6, 7, 0]
Output: 504
```

**接近 1(天真，O(** ![     ](img/50eb6463f75f46b39e856a75b3902c32.png "Rendered by QuickLaTeX.com") **)时间，O(1)空间)**
一个简单的解决方案是使用四个嵌套循环检查每四个。下面是它的实现-

## C++

```
// A C++ program to find a maximum product of a
// quadruple in array of integers
#include <bits/stdc++.h>
using namespace std;

/* Function to find a maximum product of a
   quadruple in array of integers of size n */
int maxProduct(int arr[], int n)
{
    // if size is less than 4, no quadruple exists
    if (n < 4)
        return -1;

    // will contain max product
    int max_product = INT_MIN;

    for (int i = 0; i < n - 3; i++)
        for (int j = i + 1; j < n - 2; j++)
            for (int k = j + 1; k < n - 1; k++)
                for (int l = k + 1; l < n; l++)
                    max_product = max(max_product,
                   arr[i] * arr[j] * arr[k] * arr[l]);

    return max_product;
}

// Driver program to test above functions
int main()
{
    int arr[] = { 10, 3, 5, 6, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int max = maxProduct(arr, n);
    if (max == -1)
        cout << "No Quadruple Exists";
    else
        cout << "Maximum product is " << max;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find
// a maximum product of a
// quadruple in array of
// integers
import java.io.*;

class GFG
{

/* Function to find a
maximum product of a
quadruple in array of
integers of size n */
static int maxProduct(int arr[],
                      int n)
{
    // if size is less than 4,
    // no quadruple exists
    if (n < 4)
        return -1;

    // will contain
    // max product
    int max_product = Integer.MIN_VALUE;

    for (int i = 0;
             i < n - 3; i++)
        for (int j = i + 1;
                 j < n - 2; j++)
            for (int k = j + 1;
                     k < n - 1; k++)
                for (int l = k + 1;
                         l < n; l++)
                    max_product = Math.max(max_product,
                                            arr[i] * arr[j] *
                                            arr[k] * arr[l]);

    return max_product;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 10, 3, 5, 6, 20 };
    int n = arr.length;
    int max = maxProduct(arr, n);
    if (max == -1)
        System.out.println("No Quadruple Exists");
    else
        System.out.println("Maximum product is " + max);
}
}

// This code is contributed
// by anuj_67
```

## 蟒蛇 3

```
# Python3 program to find a
# maximum product of a
# quadruple in array of
# integers
import sys

# Function to find a maximum
# product of a quadruple in
# array of integers of size n
def maxProduct(arr, n):

    # if size is less than
    # 4, no quadruple exists
    if (n < 4):
        return -1;

    # will contain max product
    max_product = -sys.maxsize;

    for i in range(n - 3):
        for j in range(i + 1, n - 2):
            for k in range(j + 1, n - 1):
                for l in range(k + 1, n):
                    max_product = max(max_product,
                                      arr[i] * arr[j] *
                                      arr[k] * arr[l]);

    return max_product;

# Driver Code
arr = [10, 3, 5, 6, 20];
n = len(arr);
max = maxProduct(arr, n);

if (max == -1):
    print("No Quadruple Exists");
else:
    print("Maximum product is", max);

# This code is contributed
# by rahul
```

## C#

```
// A C# program to find
// a maximum product of a
// quadruple in array of
// integers
using System;

class GFG
{

/* Function to find a
maximum product of a
quadruple in array of
integers of size n */
static int maxProduct(int []arr,
                      int n)
{
    // if size is less than 4,
    // no quadruple exists
    if (n < 4)
        return -1;

    // will contain
    // max product
    int max_product = int.MinValue;

    for (int i = 0;
             i < n - 3; i++)
        for (int j = i + 1;
                 j < n - 2; j++)
            for (int k = j + 1;
                     k < n - 1; k++)
                for (int l = k + 1;
                         l < n; l++)
                    max_product = Math.Max(max_product,
                                           arr[i] * arr[j] *
                                           arr[k] * arr[l]);

    return max_product;
}

// Driver Code
public static void Main ()
{
    int []arr = {10, 3, 5, 6, 20};
    int n = arr.Length;
    int max = maxProduct(arr, n);
    if (max == -1)
        Console.WriteLine("No Quadruple Exists");
    else
        Console.WriteLine("Maximum product is " + max);
}
}

// This code is contributed
// by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a
// maximum product of a
// quadruple in array of
// integers

// Function to find a maximum
// product of a quadruple in
// array of integers of size n
function maxProduct($arr, $n)
{
    // if size is less than
    // 4, no quadruple exists
    if ($n < 4)
        return -1;

    // will contain max product
    $max_product = PHP_INT_MIN;

    for ($i = 0; $i < $n - 3; $i++)
        for ($j = $i + 1; $j < $n - 2; $j++)
            for ($k = $j + 1; $k < $n - 1; $k++)
                for ($l = $k + 1; $l < $n; $l++)
                    $max_product = max($max_product,
                                       $arr[$i] * $arr[$j] *
                                       $arr[$k] * $arr[$l]);

    return $max_product;
}

// Driver Code
$arr = array(10, 3, 5, 6, 20);
$n = count($arr);
$max = maxProduct($arr, $n);
if ($max == -1)
    echo "No Quadruple Exists";
else
    echo "Maximum product is " , $max;

// This code is contributed
// by anuj_67
?>
```

## java 描述语言

```
<script>
// A Javascript program to find
// a maximum product of a
// quadruple in array of
// integers

    /* Function to find a
maximum product of a
quadruple in array of
integers of size n */
    function maxProduct(arr,n)
    {
        // if size is less than 4,
    // no quadruple exists
    if (n < 4)
        return -1;

    // will contain
    // max product
    let max_product = Number.MIN_VALUE;

    for (let i = 0;
             i < n - 3; i++)
        for (let j = i + 1;
                 j < n - 2; j++)
            for (let k = j + 1;
                     k < n - 1; k++)
                for (let l = k + 1;
                         l < n; l++)
                    max_product = Math.max(max_product,
                                            arr[i] * arr[j] *
                                            arr[k] * arr[l]);

    return max_product;
    }

    // Driver Code
    let arr=[10, 3, 5, 6, 20 ];
    let n = arr.length;
    let max = maxProduct(arr, n);
    if (max == -1)
        document.write("No Quadruple Exists");
    else
        document.write("Maximum product is " + max);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Maximum product is 6000
```

**进场 2: O(nlogn)时间，O(1)空间**

1.  使用一些高效的就地排序算法按升序对数组进行排序。

2.  设 x 是最后四个元素的乘积。

3.  设 y 是前四个元素的乘积。

4.  设 z 是前两个元素和后两个元素的乘积。

5.  返回 x，y，z 的最大值

下面是它的实现–

## C++

```
// A C++ program to find a maximum product of a
// quadruple in array of integers
#include <bits/stdc++.h>
using namespace std;

/* Function to find a maximum product of a quadruple
   in array of integers of size n */
int maxProduct(int arr[], int n)
{
    // if size is less than 4, no quadruple exists
    if (n < 4)
        return -1;

    // Sort the array in ascending order
    sort(arr, arr + n);

    int x = arr[n - 1] * arr[n - 2] * arr[n - 3] * arr[n - 4];
    int y = arr[0] * arr[1] * arr[2] * arr[3];
    int z = arr[0] * arr[1] * arr[n - 1] * arr[n - 2];

    // Return the maximum of x, y and z
    return max(x, max(y, z));
}

// Driver program to test above functions
int main()
{
    int arr[] = { -10, -3, 5, 6, -20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int max = maxProduct(arr, n);
    if (max == -1)
        cout << "No Quadruple Exists";
    else
        cout << "Maximum product is " << max;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find a
// maximum product of a
// quadruple in array of integers
import java.io.*;
import java.util.Arrays;

class GFG
{

/* Function to find a
maximum product of a quadruple
in array of integers of size n */
static int maxProduct(int arr[],
                      int n)
{
    // if size is less than 4,
    // no quadruple exists
    if (n < 4)
        return -1;

    // Sort the array
    // in ascending order
    Arrays.sort(arr);

    int x = arr[n - 1] * arr[n - 2] *
            arr[n - 3] * arr[n - 4];
    int y = arr[0] * arr[1] *
            arr[2] * arr[3];
    int z = arr[0] * arr[1] *
            arr[n - 1] * arr[n - 2];

    // Return the maximum
    // of x, y and z
    return Math.max(x, Math.max(y, z));
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {-10, -3, 5, 6, -20};
    int n = arr.length;
    int max = maxProduct(arr, n);
    if (max == -1)
        System.out.println("No Quadruple Exists");
    else
        System.out.println("Maximum product is " +
                                             max);
}
}

// This code is contributed
// by anuj_67
```

## 蟒蛇 3

```
# A Python 3 program to find a maximum
# product of a quadruple in array of integers

# Function to find a maximum product of a
# quadruple in array of integers of size n
def maxProduct(arr, n):

    # if size is less than 4, no
    # quadruple exists
    if (n < 4):
        return -1

    # Sort the array in ascending order
    arr.sort()

    x = (arr[n - 1] * arr[n - 2] *
         arr[n - 3] * arr[n - 4])
    y = arr[0] * arr[1] * arr[2] * arr[3]
    z = (arr[0] * arr[1] *
         arr[n - 1] * arr[n - 2])

    # Return the maximum of x, y and z
    return max(x, max(y, z))

# Driver Code
if __name__ == "__main__":

    arr = [ -10, -3, 5, 6, -20 ]
    n = len(arr)
    max = maxProduct(arr, n)
    if (max == -1):
        print("No Quadruple Exists")
    else:
        print("Maximum product is", max)

# This code is contributed by ita_c
```

## C#

```
// A C# program to find a
// maximum product of a
// quadruple in array of
// integers
using System;

class GFG
{

/* Function to find a
maximum product of a
quadruple in array of
integers of size n */
static int maxProduct(int []arr,
                      int n)
{
    // if size is less than 4,
    // no quadruple exists
    if (n < 4)
        return -1;

    // Sort the array
    // in ascending order
    Array.Sort(arr);

    int x = arr[n - 1] * arr[n - 2] *
            arr[n - 3] * arr[n - 4];
    int y = arr[0] * arr[1] *
            arr[2] * arr[3];
    int z = arr[0] * arr[1] *
            arr[n - 1] * arr[n - 2];

    // Return the maximum
    // of x, y and z
    return Math.Max(x, Math.Max(y, z));
}

// Driver Code
public static void Main ()
{
    int []arr = {-10, -3, 5, 6, -20};
    int n = arr.Length;
    int max = maxProduct(arr, n);
    if (max == -1)
        Console.WriteLine("No Quadruple Exists");
    else
        Console.WriteLine("Maximum product is " +
                                            max);

}
}

// This code is contributed
// by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find a
// maximum product of a
// quadruple in array of
// integers

/* Function to find a maximum
   product of a quadruple
   in array of integers of size n */
function maxProduct($arr, $n)
{
    // if size is less than 4,
    // no quadruple exists
    if ($n < 4)
        return -1;

    // Sort the array
    // in ascending order
    sort($arr);

    $x = $arr[$n - 1] * $arr[$n - 2] *
         $arr[$n - 3] * $arr[$n - 4];
    $y = $arr[0] * $arr[1] *
         $arr[2] * $arr[3];
    $z = $arr[0] * $arr[1] *
         $arr[$n - 1] * $arr[$n - 2];

    // Return the maximum
    // of x, y and z
    return max($x, max($y, $z));
}

// Driver Code
$arr = array(-10, -3, 5, 6, -20);
$n = sizeof($arr);

$max = maxProduct($arr, $n);
    if ($max == -1)
        echo "No Quadruple Exists";
    else
        echo "Maximum product is " . $max;

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// A Javascript program to find a
// maximum product of a
// quadruple in array of integers

    /* Function to find a
maximum product of a quadruple
in array of integers of size n */
    function maxProduct(arr,n)
    {
        // if size is less than 4,
    // no quadruple exists
    if (n < 4)
        return -1;

    // Sort the array
    // in ascending order
    arr.sort(function(a,b){return a-b;});

    let x = arr[n - 1] * arr[n - 2] *
            arr[n - 3] * arr[n - 4];
    let y = arr[0] * arr[1] *
            arr[2] * arr[3];
    let z = arr[0] * arr[1] *
            arr[n - 1] * arr[n - 2];

    // Return the maximum
    // of x, y and z
    return Math.max(x, Math.max(y, z));
    }

    // Driver Code
    let arr=[-10, -3, 5, 6, -20];
    let n = arr.length;
    let max = maxProduct(arr, n);
    if (max == -1)
        document.write("No Quadruple Exists");
    else
        document.write("Maximum product is " +
                                             max);

// This code is contributed by rag2127

</script>
```

**输出:**

```
Maximum product is 6000
```

**进场 3: O(n)时间，O(1)空间**

1.  扫描数组并计算数组中存在的最大值、第二个最大值、第三个最大值和第四个最大值元素。

2.  扫描阵列并计算阵列中存在的最小、第二最小、第三最小和第四最小元素。

3.  返回(最大值、第二个最大值、第三个最大值和第四个最大值的乘积)、(最小值、第二个最小值、第三个最小值和第四个最小值的乘积)和(最大值、第二个最大值、最小值、第二个最小值的乘积)的最大值。

注意–步骤 1 和步骤 2 可以在数组的单次遍历中完成。
下面是它的实现–

## C++

```
// A O(n) C++ program to find maximum quadruple in
// an array.
#include <bits/stdc++.h>
using namespace std;

/* Function to find a maximum product of a quadruple
   in array of integers of size n */
int maxProduct(int arr[], int n)
{
    // if size is less than 4, no quadruple exists
    if (n < 4)
        return -1;

    // Initialize Maximum, second maximum, third
    // maximum and fourth maximum element
    int maxA = INT_MIN, maxB = INT_MIN,
        maxC = INT_MIN, maxD = INT_MIN;

    // Initialize Minimum, second minimum, third
    // minimum and fourth minimum element
    int minA = INT_MAX, minB = INT_MAX,
        minC = INT_MAX, minD = INT_MAX;

    for (int i = 0; i < n; i++) {

        // Update Maximum, second maximum, third
        // maximum and fourth maximum element
        if (arr[i] > maxA) {
            maxD = maxC;
            maxC = maxB;
            maxB = maxA;
            maxA = arr[i];
        }

        // Update second maximum, third maximum
        // and fourth maximum element
        else if (arr[i] > maxB) {
            maxD = maxC;
            maxC = maxB;
            maxB = arr[i];
        }

        // Update third maximum and
        // fourth maximum element
        else if (arr[i] > maxC) {
            maxD = maxC;
            maxC = arr[i];
        }

        // Update fourth maximum element
        else if (arr[i] > maxD)
            maxD = arr[i];

        // Update Minimum, second minimum
        // third minimum and fourth minimum element
        if (arr[i] < minA) {
            minD = minC;
            minC = minB;
            minB = minA;
            minA = arr[i];
        }

        // Update second minimum, third
        // minimum and fourth minimum element
        else if (arr[i] < minB) {
            minD = minC;
            minC = minB;
            minB = arr[i];
        }

        // Update third minimum and
        // fourth minimum element
        else if (arr[i] < minC) {
            minD = minC;
            minC = arr[i];
        }

        // Update fourth minimum element
        else if (arr[i] < minD)
            minD = arr[i];
    }

    int x = maxA * maxB * maxC * maxD;
    int y = minA * minB * minC * minD;
    int z = minA * minB * maxA * maxB;
    // Return the maximum of x, y and z
    return max(x, max(y, z));
}

// Driver program to test above function
int main()
{
    int arr[] = { 1, -4, 3, -6, 7, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int max = maxProduct(arr, n);
    if (max == -1)
        cout << "No Quadruple Exists";
    else
        cout << "Maximum product is " << max;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(n) Java program to find maximum
// quadruple in an array.
class GFG
{

    /* Function to find a maximum product of a
    quadruple in array of integers of size n */
    static int maxProduct(int arr[], int n)
    {
        // if size is less than 4, no quadruple exists
        if (n < 4) {
            return -1;
        }

        // Initialize Maximum, second maximum, third
        // maximum and fourth maximum element
        int maxA = Integer.MIN_VALUE,
            maxB = Integer.MIN_VALUE,
            maxC = Integer.MIN_VALUE,
            maxD = Integer.MIN_VALUE;

        // Initialize Minimum, second minimum, third
        // minimum and fourth minimum element
        int minA = Integer.MAX_VALUE,
            minB = Integer.MAX_VALUE,
            minC = Integer.MAX_VALUE,
            minD = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++)
        {

            // Update Maximum, second maximum, third
            // maximum and fourth maximum element
            if (arr[i] > maxA) {
                maxD = maxC;
                maxC = maxB;
                maxB = maxA;
                maxA = arr[i];
            }

            // Update second maximum, third maximum
            // and fourth maximum element
            else if (arr[i] > maxB) {
                maxD = maxC;
                maxC = maxB;
                maxB = arr[i];
            }

            // Update third maximum and
            // fourth maximum element
            else if (arr[i] > maxC) {
                maxD = maxC;
                maxC = arr[i];
            }

            // Update fourth maximum element
            else if (arr[i] > maxD) {
                maxD = arr[i];
            }

            // Update Minimum, second minimum
            // third minimum and fourth minimum element
            if (arr[i] < minA) {
                minD = minC;
                minC = minB;
                minB = minA;
                minA = arr[i];
            }

            // Update second minimum, third
            // minimum and fourth minimum element
            else if (arr[i] < minB) {
                minD = minC;
                minC = minB;
                minB = arr[i];
            }

            // Update third minimum and
            // fourth minimum element
            else if (arr[i] < minC) {
                minD = minC;
                minC = arr[i];
            }

            // Update fourth minimum element
            else if (arr[i] < minD) {
                minD = arr[i];
            }
        }

        int x = maxA * maxB * maxC * maxD;
        int y = minA * minB * minC * minD;
        int z = minA * minB * maxA * maxB;

        // Return the maximum of x, y and z
        return Math.max(x, Math.max(y, z));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, -4, 3, -6, 7, 0 };
        int n = arr.length;
        int max = maxProduct(arr, n);
        if (max == -1)
            System.out.println("No Quadruple Exists");
        else
            System.out.println("Maximum product is " + max);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# A O(n) Python 3 program to find maximum quadruple in# an array.
import sys

# Function to find a maximum product of a quadruple
# in array of integers of size n
def maxProduct(arr, n):
    # if size is less than 4, no quadruple exists
    if (n < 4):
        return -1

    # Initialize Maximum, second maximum, third
    # maximum and fourth maximum element
    maxA = -sys.maxsize - 1
    maxB = -sys.maxsize - 1
    maxC = -sys.maxsize - 1
    maxD = -sys.maxsize - 1

    # Initialize Minimum, second minimum, third
    # minimum and fourth minimum element
    minA = sys.maxsize
    minB = sys.maxsize
    minC = sys.maxsize
    minD = sys.maxsize

    for i in range(n):
        # Update Maximum, second maximum, third
        # maximum and fourth maximum element
        if (arr[i] > maxA):
            maxD = maxC
            maxC = maxB
            maxB = maxA
            maxA = arr[i]

        # Update second maximum, third maximum
        # and fourth maximum element
        elif (arr[i] > maxB):
            maxD = maxC
            maxC = maxB
            maxB = arr[i]

        # Update third maximum and
        # fourth maximum element
        elif (arr[i] > maxC):
            maxD = maxC
            maxC = arr[i]

        # Update fourth maximum element
        elif (arr[i] > maxD):
            maxD = arr[i]

        # Update Minimum, second minimum
        # third minimum and fourth minimum element
        if (arr[i] < minA):
            minD = minC
            minC = minB
            minB = minA
            minA = arr[i]

        # Update second minimum, third
        # minimum and fourth minimum element
        elif (arr[i] < minB):
            minD = minC
            minC = minB
            minB = arr[i]

        # Update third minimum and
        # fourth minimum element
        elif (arr[i] < minC):
            minD = minC
            minC = arr[i]

        # Update fourth minimum element
        elif (arr[i] < minD):
            minD = arr[i]

    x = maxA * maxB * maxC * maxD
    y = minA * minB * minC * minD
    z = minA * minB * maxA * maxB
    # Return the maximum of x, y and z
    return max(x, max(y, z))

# Driver program to test above function
if __name__ == '__main__':
    arr = [1, -4, 3, -6, 7, 0]
    n = len(arr)
    max1 = maxProduct(arr, n)
    if (max1 == -1):
        print("No Quadruple Exists")
    else:
        print("Maximum product is", max1)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// A O(n) C# program to find maximum
// quadruple in an array.
using System;

class GFG
{

    /* Function to find a maximum product of a
    quadruple in array of integers of size n */
    static int maxProduct(int []arr, int n)
    {
        // if size is less than 4, no quadruple exists
        if (n < 4)
        {
            return -1;
        }

        // Initialize Maximum, second maximum, third
        // maximum and fourth maximum element
        int maxA = int.MinValue,
            maxB = int.MinValue,
            maxC = int.MinValue,
            maxD = int.MinValue;

        // Initialize Minimum, second minimum, third
        // minimum and fourth minimum element
        int minA = int.MaxValue,
            minB = int.MaxValue,
            minC = int.MaxValue,
            minD = int.MaxValue;

        for (int i = 0; i < n; i++)
        {

            // Update Maximum, second maximum, third
            // maximum and fourth maximum element
            if (arr[i] > maxA)
            {
                maxD = maxC;
                maxC = maxB;
                maxB = maxA;
                maxA = arr[i];
            }

            // Update second maximum, third maximum
            // and fourth maximum element
            else if (arr[i] > maxB)
            {
                maxD = maxC;
                maxC = maxB;
                maxB = arr[i];
            }

            // Update third maximum and
            // fourth maximum element
            else if (arr[i] > maxC)
            {
                maxD = maxC;
                maxC = arr[i];
            }

            // Update fourth maximum element
            else if (arr[i] > maxD)
            {
                maxD = arr[i];
            }

            // Update Minimum, second minimum
            // third minimum and fourth minimum element
            if (arr[i] < minA)
            {
                minD = minC;
                minC = minB;
                minB = minA;
                minA = arr[i];
            }

            // Update second minimum, third
            // minimum and fourth minimum element
            else if (arr[i] < minB)
            {
                minD = minC;
                minC = minB;
                minB = arr[i];
            }

            // Update third minimum and
            // fourth minimum element
            else if (arr[i] < minC)
            {
                minD = minC;
                minC = arr[i];
            }

            // Update fourth minimum element
            else if (arr[i] < minD)
            {
                minD = arr[i];
            }
        }

        int x = maxA * maxB * maxC * maxD;
        int y = minA * minB * minC * minD;
        int z = minA * minB * maxA * maxB;

        // Return the maximum of x, y and z
        return Math.Max(x, Math.Max(y, z));
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 1, -4, 3, -6, 7, 0 };
        int n = arr.Length;
        int max = maxProduct(arr, n);
        if (max == -1)
            Console.Write("No Quadruple Exists");
        else
            Console.Write("Maximum product is " + max);
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(n) PHP program to find maximum
// quadruple in an array.

/* Function to find a maximum product of
a quadruple in array of integers of size n */
function maxProduct($arr, $n)
{
    // if size is less than 4,
    // no quadruple exists
    if ($n < 4)
        return -1;

    // Initialize Maximum, second maximum, third
    // maximum and fourth maximum element
    $maxA = -2147483648; $maxB = -2147483648;
    $maxC = -2147483648; $maxD = -2147483648;

    // Initialize Minimum, second minimum, third
    // minimum and fourth minimum element
    $minA = 2147483647; $minB = 2147483647;
    $minC = 2147483647; $minD = 2147483647;

    for ($i = 0; $i < $n; $i++)
    {

        // Update Maximum, second maximum, third
        // maximum and fourth maximum element
        if ($arr[$i] > $maxA)
        {
            $maxD = $maxC;
            $maxC = $maxB;
            $maxB = $maxA;
            $maxA = $arr[$i];
        }

        // Update second maximum, third maximum
        // and fourth maximum element
        elseif ($arr[$i] > $maxB)
        {
            $maxD = $maxC;
            $maxC = $maxB;
            $maxB = $arr[$i];
        }

        // Update third maximum and fourth
        // maximum element
        elseif ($arr[$i] > $maxC)
        {
            $maxD = $maxC;
            $maxC = $arr[$i];
        }

        // Update fourth maximum element
        elseif ($arr[$i] > $maxD)
            $maxD = $arr[$i];

        // Update Minimum, second minimum,
        // third minimum and fourth minimum element
        if ($arr[$i] < $minA)
        {
            $minD = $minC;
            $minC = $minB;
            $minB = $minA;
            $minA = $arr[$i];
        }

        // Update second minimum, third
        // minimum and fourth minimum element
        elseif ($arr[$i] < $minB)
        {
            $minD = $minC;
            $minC = $minB;
            $minB = $arr[$i];
        }

        // Update third minimum and
        // fourth minimum element
        elseif ($arr[$i] < $minC)
        {
            $minD = $minC;
            $minC = $arr[$i];
        }

        // Update fourth minimum element
        elseif ($arr[$i] < $minD)
            $minD = $arr[$i];
    }

    $x = $maxA * $maxB * $maxC * $maxD;
    $y = $minA * $minB * $minC * $minD;
    $z = $minA * $minB * $maxA * $maxB;

    // Return the maximum of x, y and z
    return max($x, max($y, $z));
}

// Driver Code
$arr = array( 1, -4, 3, -6, 7, 0 );
$n = count($arr);
$max = maxProduct($arr, $n);
if ($max == -1)
    echo "No Quadruple Exists";
else
    echo "Maximum product is " . $max;

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>
    // A O(n) Javascript program to find maximum
    // quadruple in an array.

    /* Function to find a maximum product of a
    quadruple in array of integers of size n */
    function maxProduct(arr, n)
    {
        // if size is less than 4, no quadruple exists
        if (n < 4)
        {
            return -1;
        }

        // Initialize Maximum, second maximum, third
        // maximum and fourth maximum element
        let maxA = Number.MIN_VALUE,
            maxB = Number.MIN_VALUE,
            maxC = Number.MIN_VALUE,
            maxD = Number.MIN_VALUE;

        // Initialize Minimum, second minimum, third
        // minimum and fourth minimum element
        let minA = Number.MAX_VALUE,
            minB = Number.MAX_VALUE,
            minC = Number.MAX_VALUE,
            minD = Number.MAX_VALUE;

        for (let i = 0; i < n; i++)
        {

            // Update Maximum, second maximum, third
            // maximum and fourth maximum element
            if (arr[i] > maxA)
            {
                maxD = maxC;
                maxC = maxB;
                maxB = maxA;
                maxA = arr[i];
            }

            // Update second maximum, third maximum
            // and fourth maximum element
            else if (arr[i] > maxB)
            {
                maxD = maxC;
                maxC = maxB;
                maxB = arr[i];
            }

            // Update third maximum and
            // fourth maximum element
            else if (arr[i] > maxC)
            {
                maxD = maxC;
                maxC = arr[i];
            }

            // Update fourth maximum element
            else if (arr[i] > maxD)
            {
                maxD = arr[i];
            }

            // Update Minimum, second minimum
            // third minimum and fourth minimum element
            if (arr[i] < minA)
            {
                minD = minC;
                minC = minB;
                minB = minA;
                minA = arr[i];
            }

            // Update second minimum, third
            // minimum and fourth minimum element
            else if (arr[i] < minB)
            {
                minD = minC;
                minC = minB;
                minB = arr[i];
            }

            // Update third minimum and
            // fourth minimum element
            else if (arr[i] < minC)
            {
                minD = minC;
                minC = arr[i];
            }

            // Update fourth minimum element
            else if (arr[i] < minD)
            {
                minD = arr[i];
            }
        }

        let x = maxA * maxB * maxC * maxD;
        let y = minA * minB * minC * minD;
        let z = minA * minB * maxA * maxB;

        // Return the maximum of x, y and z
        return Math.max(x, Math.max(y, z));
    }

    let arr = [ 1, -4, 3, -6, 7, 0 ];
    let n = arr.length;
    let max = maxProduct(arr, n);
    if (max == -1)
      document.write("No Quadruple Exists");
    else
      document.write("Maximum product is " + max);

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
Maximum product is 504
```