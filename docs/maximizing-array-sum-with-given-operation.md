# 给定操作下最大化数组和

> 原文:[https://www . geeksforgeeks . org/最大化给定运算的数组和/](https://www.geeksforgeeks.org/maximizing-array-sum-with-given-operation/)

有一个由(2 * n–1)个整数组成的数组。我们可以改变数组中 n 个元素的符号。换句话说，我们可以精确地选择 n 个数组元素，并将其乘以-1。求数组的最大和。
**例:**

```
Input : arr[] = 50 50 50
Output : 150
There is no need to change anything.
The sum of elements equals 150 
which is maximum.

Input :  arr[] = -1 -100 -1
Output : 100
Change the sign of the first two 
elements. Sum of the elements 
equal to 100.
```

**逼近:**
**步骤 1:-** 循环迭代 2*n-1 次，重复步骤 2、3、4。
**第二步:-** 计算负数(负数)的个数。
**第三步:-** 取数字的绝对值计算数组的和(sum)。
**步骤 4:-** 通过取数值的绝对值(min)来求数组的最小个数。
**步骤 5:-** 检查负数的个数是否为奇数，n(给定)的值是否为偶数，然后从和中减去 m 的两倍，这将是数组的 max_sum，否则 sum 的值将是数组的 max_sum。
以下是上述方法的实施:

## C++

```
// CPP program to get the maximum
// sum of the array.
#include <bits/stdc++.h>
using namespace std;

// function to find maximum sum
int maxSum(int arr[], int n)
{
    int neg = 0, sum = 0,
     m = INT_MAX, max_sum;

    // step 1
    for (int i = 0; i < 2 * n - 1; i++) {

        // step 2
        neg += (arr[i] < 0);

        // step 3
        sum += abs(arr[i]);

        // step 4
        m = min(m, abs(arr[i]));
    }

    // step 5
    if (neg % 2 && n % 2 == 0) {
        max_sum = sum -= 2 * m;
        return (max_sum);
    }

    max_sum = sum;
    return (max_sum);
}

// Driver Function
int main()
{
    int arr[] = { -1, -100, -1 };
    int n = 2;
    cout << maxSum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get the maximum
// sum of the array.
import java.io.*;
import java.math.*;

class GFG {

// function to find maximum sum
static int maxSum(int arr[], int n) {
    int neg = 0, sum = 0, m = 100000000, max_sum;

    // step 1
    for (int i = 0; i < 2 * n - 1; i++) {

    // step 2
    if (arr[i] < 0)
        neg += 1;

    // step 3
    sum += Math.abs(arr[i]);

    // step 4
    m = Math.min(m, Math.abs(arr[i]));
    }

    // step 5
    if (neg % 2 == 1 && n % 2 == 0) {
    max_sum = sum -= 2 * m;
    return (max_sum);
    }

    max_sum = sum;
    return (max_sum);
}

// Driver Function
public static void main(String args[]) {
    int arr[] = {-1, -100, -1};
    int n = 2;
    System.out.println(maxSum(arr, n));
}
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 code to get the maximum
# sum of the array.
import sys

# function to find maximum sum
def maxSum (arr, n):
    neg = 0
    sum = 0
    m = sys.maxsize

    # step 1
    for i in range(2 * n - 1):

        # step 2
        neg += (arr[i] < 0)

        # step 3
        sum += abs(arr[i])

        # step 4
        m = min(m, abs(arr[i]))

    # step 5
    if neg % 2 and n % 2 == 0:
        max_sum = sum - 2 * m
        return (max_sum)

    max_sum = sum
    return max_sum

# Driver Code
arr = [ -1, -100, -1 ]
n = 2
print( maxSum(arr, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to get the maximum
// sum of the array.
using System;

class GFG
{

// function to find maximum sum
static int maxSum(int []arr, int n)
{
    int neg = 0, sum = 0;
    int m = 100000000, max_sum;

    // step 1
    for (int i = 0; i < 2 * n - 1; i++)
    {

        // step 2
        if (arr[i] < 0)
        neg += 1;

        // step 3
        sum += Math.Abs(arr[i]);

        // step 4
        m = Math.Min(m, Math.Abs(arr[i]));
    }

    // step 5
    if (neg % 2 == 1 && n % 2 == 0)
    {
        max_sum = sum -= 2 * m;
        return (max_sum);
    }

    max_sum = sum;
    return (max_sum);
}

// Driver Code
public static void Main()
{
    int []arr = {-1, -100, -1};
    int n = 2;
    Console.WriteLine(maxSum(arr, n));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get the
// maximum sum of the array.

// function to find maximum sum
function maxSum($arr, $n)
{
    $neg = 0; $sum = 0;
    $m = PHP_INT_MAX; $max_sum;

    // step 1
    for ($i = 0; $i < 2 * $n - 1; $i++)
    {
        // step 2
        $neg += ($arr[$i] < 0);

        // step 3
        $sum += abs($arr[$i]);

        // step 4
        $m = min($m, abs($arr[$i]));
    }

    // step 5
    if ($neg % 2 && $n % 2 == 0)
    {
        $max_sum = $sum -= 2 * $m;
        return ($max_sum);
    }

    $max_sum = $sum;
    return ($max_sum);
}

// Driver Code
$arr = array(-1, -100, -1);
$n = 2;
echo maxSum($arr, $n) ;

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>
    // Javascript program to get the maximum
    // sum of the array.

    // function to find maximum sum
    function maxSum(arr, n)
    {
        let neg = 0, sum = 0, m = Number.MAX_VALUE, max_sum;

        // step 1
        for (let i = 0; i < 2 * n - 1; i++) {

            // step 2
            neg += (arr[i] < 0);

            // step 3
            sum += Math.abs(arr[i]);

            // step 4
            m = Math.min(m, Math.abs(arr[i]));
        }

        // step 5
        if (neg % 2 && n % 2 == 0) {
            max_sum = sum -= 2 * m;
            return (max_sum);
        }

        max_sum = sum;
        return (max_sum);
    }

    let arr = [ -1, -100, -1 ];
    let n = 2;
    document.write(maxSum(arr, n));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
100
```