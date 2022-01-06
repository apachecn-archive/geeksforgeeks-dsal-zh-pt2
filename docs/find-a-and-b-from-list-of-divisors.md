# 从除数列表中找出 A 和 B

> 原文:[https://www . geesforgeks . org/find-a-and-b-from-list-of-divisions/](https://www.geeksforgeeks.org/find-a-and-b-from-list-of-divisors/)

给定一个数组 **arr[]** ，它由两个整数 **A** 和 **B** (以及 **A** 、 **B** 和 **1** )的所有除数组成。任务是从给定数组中找到 **A** 和 **B** 。
**注意:**如果一个数是 **A** 和 **B** 的除数，那么它将在数组中出现两次。

**示例:**

> **输入:** arr[] = {1，2，4，8，16，1，2，3，6}
> **输出:** A = 16，B = 6
> 1，2，4，8 和 16 是 16 的除数
> 1，2，3 和 6 是 6 的除数
> 
> **输入:** arr[] = {1，2，4，8，16，1，2，4}
> **输出:** A = 16，B = 4

**方法:**从给定数组开始，由于所有元素都是 **A** 或 **B** 的除数，因此数组中最大的元素必须是 **A** 或 **B** 。为简单起见，将其作为 **A** 。现在，有两种情况适用于元素为 B:

1.  **B** 可以是不是 **A** 除数的最大元素。
2.  **B** 可以是比频率为 **2** 的 **A** 小的最大元素。

为了找到 **A** 和 **B** 的值，对数组进行排序。将**最大元素打印为 A** ，则不是 A 除数或频率为 2 的**最大元素将为 **B** 。
以下是上述方法的实施:**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print A and B all of whose
// divisors are present in the given array
void printNumbers(int arr[], int n)
{

    // Sort the array
    sort(arr, arr + n);

    // A is the largest element from the array
    int A = arr[n - 1], B = -1;

    // Iterate from the second largest element
    for (int i = n - 2; i >= 0; i--) {

        // If current element is not a divisor
        // of A then it must be B
        if (A % arr[i] != 0) {
            B = arr[i];
            break;
        }

        // If current element occurs more than once
        if (i - 1 >= 0 && arr[i] == arr[i - 1]) {
            B = arr[i];
            break;
        }
    }

    // Print A and B
    cout << "A = " << A << ", B = " << B;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 8, 16, 1, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printNumbers(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GfG {

    // Function to print A and B all of whose
    // divisors are present in the given array
    static void printNumbers(int arr[], int n)
    {

        // Sort the array
        Arrays.sort(arr);

        // A is the largest element from the array
        int A = arr[n - 1], B = -1;

        // Iterate from the second largest element
        for (int i = n - 2; i >= 0; i--) {

            // If current element is not a divisor
            // of A then it must be B
            if (A % arr[i] != 0) {
                B = arr[i];
                break;
            }

            // If current element occurs more than once
            if (i - 1 >= 0 && arr[i] == arr[i - 1]) {
                B = arr[i];
                break;
            }
        }

        // Print A and B
        System.out.print("A = " + A + ", B = " + B);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 4, 8, 16, 1, 2, 4 };
        int n = arr.length;
        printNumbers(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print A and B all of whose
# divisors are present in the given array
def printNumbers(arr, n):

    # Sort the array
    arr.sort()

    # A is the largest element from the array
    A, B = arr[n - 1], -1

    # Iterate from the second largest element
    for i in range(n - 2, -1, -1):

        # If current element is not a divisor
        # of A then it must be B
        if A % arr[i] != 0:
            B = arr[i]
            break

        # If current element occurs more than once
        if i - 1 >= 0 and arr[i] == arr[i - 1]:
            B = arr[i]
            break

    # Print A and B
    print("A =", A, ", B =", B)

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 4, 8, 16, 1, 2, 4]
    n = len(arr)
    printNumbers(arr, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System.Collections;
using System;

class GfG
{

    // Function to print A and B all of whose
    // divisors are present in the given array
    static void printNumbers(int []arr, int n)
    {

        // Sort the array
        Array.Sort(arr);

        // A is the largest element from the array
        int A = arr[n - 1], B = -1;

        // Iterate from the second largest element
        for (int i = n - 2; i >= 0; i--)
        {

            // If current element is not a divisor
            // of A then it must be B
            if (A % arr[i] != 0)
            {
                B = arr[i];
                break;
            }

            // If current element occurs more than once
            if (i - 1 >= 0 && arr[i] == arr[i - 1])
            {
                B = arr[i];
                break;
            }
        }

        // Print A and B
        Console.WriteLine("A = " + A + ", B = " + B);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 4, 8, 16, 1, 2, 4 };
        int n = arr.Length;
        printNumbers(arr, n);
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print A and B all of whose
// divisors are present in the given array
function printNumbers($arr, $n)
{

    // Sort the array
    sort($arr);

    // A is the largest element from the array
    $A = $arr[$n - 1]; $B = -1;

    // Iterate from the second largest element
    for ($i = $n - 2; $i >= 0; $i--)
    {

        // If current element is not a divisor
        // of A then it must be B
        if ($A % $arr[$i] != 0)
        {
            $B = $arr[$i];
            break;
        }

        // If current element occurs more than once
        if ($i - 1 >= 0 && $arr[$i] == $arr[$i - 1])
        {
            $B = $arr[$i];
            break;
        }
    }

    // Print A and B
    echo("A = " . $A . ", B = " . $B);
}

// Driver code
$arr = array( 1, 2, 4, 8, 16, 1, 2, 4 );
$n = sizeof($arr);
printNumbers($arr, $n);

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print A and B all of whose
// divisors are present in the given array
function printNumbers(arr, n)
{

    // Sort the array
    arr.sort((a,b)=>{return a-b;});

    // A is the largest element from the array
    var A = arr[n - 1], B = -1;

    // Iterate from the second largest element
    for (var i = n - 2; i >= 0; i--) {

        // If current element is not a divisor
        // of A then it must be B
        if ((A % arr[i]) != 0) {
            B = arr[i];
            break;
        }

        // If current element occurs more than once
        if (i - 1 >= 0 && arr[i] == arr[i - 1]) {
            B = arr[i];
            break;
        }
    }

    // Print A and B
    document.write( "A = " + A + ", B = " + B);
}

// Driver code
var arr = [ 1, 2, 4, 8, 16, 1, 2, 4 ];
var n = arr.length;
printNumbers(arr, n);

</script>
```

**Output:** 

```
A = 16, B = 4
```