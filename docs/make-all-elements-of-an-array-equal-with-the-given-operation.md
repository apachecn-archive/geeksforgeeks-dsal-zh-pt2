# 用给定的运算使数组的所有元素相等

> 原文:[https://www . geesforgeks . org/make-all-elements-of-of-a-array-equal-of-the-给定操作/](https://www.geeksforgeeks.org/make-all-elements-of-an-array-equal-with-the-given-operation/)

给定一个由 **n** 个整数和一个整数 **k** 组成的数组 **arr[]** 。任务是使**arr【】**的所有元素与给定的操作相等。单次运算中，任意非负数 **x ≤ k** (可以是浮点值)都可以加到数组的任意元素中， **k** 将更新为**k = k–x**。打印**是**可以，否则打印**否**。
**例:**

> **输入:** k = 8，arr[] = {1，2，3，4}
> **输出:**是
> 1+3.5 = 4.5
> 2+2.5 = 4.5
> 3+1.5 = 4.5
> 4+0.5 = 4.5
> 3.5+2.5+1.5+0.5 = 8 = k
> **输入:** k = 2，arr[]

**方法:**因为任务是使数组的所有元素相等，并且加法的总数必须正好是 **k** 。只有一个值可以使所有这些元素相等，即 **(sum(arr) + k) / n** 。如果数组中有一个元素已经大于该值，则答案不存在，否则打印**是**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if all the elements
// of the array can be made equal
// with the given operation
bool isPossible(int n, int k, int arr[])
{

    // To store the sum of the array elements
    // and the maximum element from the array
    int sum = arr[0], maxVal = arr[0];

    for (int i = 1; i < n; i++) {
        sum += arr[i];
        maxVal = max(maxVal, arr[i]);
    }

    if ((float)maxVal > (float)(sum + k) / n)
        return false;

    return true;
}

// Driver code
int main()
{
    int k = 8;
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (isPossible(n, k, arr))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach
import java.io.*;

class GFG
{

// Function that returns true if all
// the elements of the array can be
// made equal with the given operation
static boolean isPossible(int n, int k, int arr[])
{

    // To store the sum of the array elements
    // and the maximum element from the array
    int sum = arr[0];
    int maxVal = arr[0];

    for (int i = 1; i < n; i++)
    {
        sum += arr[i];
        maxVal = Math.max(maxVal, arr[i]);
    }

    if ((float)maxVal > (float)(sum + k) / n)
        return false;

    return true;
}

    // Driver code
    public static void main (String[] args)
    {

        int k = 8;
        int arr[] = { 1, 2, 3, 4 };
        int n = arr.length;

        if (isPossible(n, k, arr))
            System.out.println ("Yes");
        else
            System.out.println( "No");
    }
}

// This code is contributed by @Tushil.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if all
# the elements of the array can be
# made equal with the given operation
def isPossible(n, k, arr):

    # To store the sum of the array elements
    # and the maximum element from the array
    sum = arr[0]
    maxVal = arr[0];

    for i in range(1, n):
        sum += arr[i]
        maxVal = max(maxVal, arr[i])

    if (int(maxVal)> int((sum + k) / n)):
        return False

    return True

# Driver code
if __name__ == '__main__':
    k = 8
    arr = [1, 2, 3, 4]
    n = len(arr)

    if (isPossible(n, k, arr)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if all
    // the elements of the array can be
    // made equal with the given operation
    static bool isPossible(int n,
                        int k, int []arr)
    {

        // To store the sum of the array elements
        // and the maximum element from the array
        int sum = arr[0];
        int maxVal = arr[0];

        for (int i = 1; i < n; i++)
        {
            sum += arr[i];
            maxVal = Math.Max(maxVal, arr[i]);
        }

        if ((float)maxVal > (float)(sum + k) / n)
            return false;

        return true;
    }

    // Driver code
    public static void Main()
    {

        int k = 8;
        int []arr = { 1, 2, 3, 4 };
        int n = arr.Length;

        if (isPossible(n, k, arr))
            Console.WriteLine("Yes");
        else
            Console.WriteLine( "No");
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function that returns true if
// all the elements of the array
// can be made equal with the given operation

function isPossible($n, $k, $arr)
{

    // To store the sum of the array elements
    // and the maximum element from the array
    $sum = $arr[0];
    $maxVal = $arr[0];

    for ($i = 1; $i < $n; $i++)
    {
        $sum += $arr[$i];
        $maxVal = max($maxVal, $arr[$i]);
    }

    if ((float)$maxVal > (float)($sum + $k) / $n)
        return false;

    return true;
}

    // Driver code
    $k = 8;
    $arr = array( 1, 2, 3, 4 );
    $n = sizeof($arr) / sizeof($arr[0]);

    if (isPossible($n, $k, $arr))
        echo "Yes";
    else
        echo "No";

# This code is contributed by akt_miit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function that returns true if all
// the elements of the array can be
// made equal with the given operation
function isPossible(n, k, arr)
{

    // To store the sum of the array elements
    // and the maximum element from the array
    let sum = arr[0];
    let maxVal = arr[0];

    for (let i = 1; i < n; i++)
    {
        sum += arr[i];
        maxVal = Math.max(maxVal, arr[i]);
    }

    if (maxVal > (sum + k) / n)
        return false;

    return true;
}

// driver program

        let k = 8;
        let arr = [ 1, 2, 3, 4 ];
        let n = arr.length;

        if (isPossible(n, k, arr))
            document.write ("Yes");
        else
            document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(n)