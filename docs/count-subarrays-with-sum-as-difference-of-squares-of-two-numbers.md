# 以和为两个数平方差的子阵计数

> 原文:[https://www . geeksforgeeks . org/count-两个数平方和差子阵/](https://www.geeksforgeeks.org/count-subarrays-with-sum-as-difference-of-squares-of-two-numbers/)

给定一个数组 **arr[]** ，任务是对所有子数组进行计数，这些子数组的和可以表示为任意两个数的平方差。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 4
> **解释:**
> 所需子阵列为{1}、{3}、{1，2}和{2，3 }
> As 1<sup>2</sup>–0<sup>2</sup>= 1，2<sup>2</sup>–1<sup>2</sup>= 3，2+3 = 5 =
> 
> **输入:** arr[] = {2，1，3，7}
> **输出:** 7
> 所需子阵列为–
> {1}、{3}、{7}、{2，1 }、{2，1，3，7}、{1，3}和{ 1，3，7}

**方法:**思路是利用奇数或可被 4 整除的数只能表示为 2 个数的平方差。下面是步骤的图示:

*   运行嵌套循环，检查每个子数组的总和是否可以写成两个数的平方差。
*   如果任何子阵列的和可以表示为两个数的平方之差，那么将这些子阵列的计数增加 1

下面是上述方法的实现:

## C++

```
// C++ implementation  to count the
// subarray which can be represented
// as the difference of two square
// of two numbers

#include <bits/stdc++.h>

using namespace std;
#define ll long long

// Function to count sub-arrays whose
// sum can be represented as difference
// of squares of 2 numbers
int countSubarray(int* arr, int n)
{
    int count = 0;
    for (int i = 0; i < n; i++) {

        // Count the elements that
        // are odd and divisible by 4
        if (arr[i] % 2 != 0 || arr[i] % 4 == 0)
            count++;

        // Declare a variable to store sum
        ll sum = arr[i];
        for (int j = i + 1; j < n; j++) {

            // Calculate sum of
            // current subarray
            sum += arr[j];
            if (sum % 2 != 0 || sum % 4 == 0)
                count++;
        }
    }
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 3, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countSubarray(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation  to count the
// subarray which can be represented
// as the difference of two square
// of two numbers

import java.util.*;

class GFG {

    // Function to count sub-arrays whose
    // sum can be represented as difference
    // of squares of 2 numbers
    static int countSubarray(int[] arr, int n)
    {
        int count = 0;
        for (int i = 0; i < n; i++) {

            // Count the elements that
            // are odd and divisible by 4
            if (arr[i] % 2 != 0 || arr[i] % 4 == 0)
                count++;

            // Declare a variable to store sum
            long sum = arr[i];
            for (int j = i + 1; j < n; j++) {

                // Calculate sum of
                // current subarray
                sum += arr[j];
                if (sum % 2 != 0 || sum % 4 == 0)
                    count++;
            }
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 1, 3, 7 };
        int n = arr.length;
        System.out.println(countSubarray(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python implementation to
# count the sub-arrays whose
# sum can be represented as
# difference of square of two
# numbers

# Function to count sub-arrays whose
# sum can be represented as
# difference of squares of 2 numbers
def countSubarray(arr, n):
    count = 0
    for i in range(n):

        # Count the elements that
        # are odd or divisible by 4
        if arr[i]% 2 != 0 or arr[i]% 4 == 0:
            count+= 1

        # Declare a variable to store sum
        tot = arr[i]
        for j in range(i + 1, n):

            # Calculate sum of
            # current subarray
            tot+= arr[j]
            if tot % 2 != 0 or tot % 4 == 0:
                count+= 1
    return count

# Driver Code
if __name__ == "__main__":
    arr = [ 2, 1, 3, 7 ]
    n = len(arr)
    print(countSubarray(arr, n))
```

## C#

```
// C# implementation  to count the
// subarray which can be represented
// as the difference of two square
// of two numbers
using System;

class GFG {

    // Function to count sub-arrays whose
    // sum can be represented as difference
    // of squares of 2 numbers
    static int countSubarray(int[] arr, int n)
    {
        int count = 0;
        for (int i = 0; i < n; i++) {

            // Count the elements that
            // are odd and divisible by 4
            if (arr[i] % 2 != 0 || arr[i] % 4 == 0)
                count++;

            // Declare a variable to store sum
            long sum = arr[i];
            for (int j = i + 1; j < n; j++) {

                // Calculate sum of
                // current subarray
                sum += arr[j];
                if (sum % 2 != 0 || sum % 4 == 0)
                    count++;
            }
        }
        return count;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 1, 3, 7 };
        int n = arr.Length;
        Console.WriteLine(countSubarray(arr, n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation  to count the
// subarray which can be represented
// as the difference of two square
// of two numbers

// Function to count sub-arrays whose
// sum is divisible by K
function countSubarray($arr, $n)
{
    $count=0;
    for($i=0;$i<$n;$i++)
    {

        // Count the elements that
        // are odd and divisible by 4
        if($arr[$i]%2!=0 || $arr[$i]%4==0)
        $count++;

        // Declare a variable to store sum
        $sum=$arr[$i];
        for($j=$i+1;$j<$n;$j++)
        {

            // Calculate sum of
            // current subarray
            $sum+=$arr[$j];
            if($sum%2!=0 || $sum%4==0)
            $count++;
        }
    }
    return $count;
}

// Driver code
$arr = array( 2, 1, 3, 7 );
$n = count($arr);
echo countSubarray($arr, $n);

?>
```

## java 描述语言

```
<script>

// Javascript implementation to count the
// subarray which can be represented
// as the difference of two square
// of two numbers

// Function to count sub-arrays whose
// sum can be represented as difference
// of squares of 2 numbers
function countSubarray(arr, n)
{
    var count = 0;
    for(var i = 0; i < n; i++)
    {

        // Count the elements that
        // are odd and divisible by 4
        if (arr[i] % 2 != 0 || arr[i] % 4 == 0)
            count++;

        // Declare a variable to store sum
        var sum = arr[i];
        for(var j = i + 1; j < n; j++)
        {

            // Calculate sum of
            // current subarray
            sum += arr[j];
            if (sum % 2 != 0 || sum % 4 == 0)
                count++;
        }
    }
    return count;
}

// Driver code
var arr = [ 2, 1, 3, 7 ];
var n = arr.length;

document.write(countSubarray(arr, n));

// This code is contributed by shivanisinghss2110 

</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N <sup>2</sup> )