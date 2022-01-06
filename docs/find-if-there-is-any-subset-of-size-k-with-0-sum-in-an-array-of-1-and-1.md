# 查找在-1 和+1 的数组中是否有大小为 0 和的 K 的子集

> 原文:[https://www . geeksforgeeks . org/find-如果有大小为 0 的 k 的任何子集，请在 1 和 1 的数组中求和/](https://www.geeksforgeeks.org/find-if-there-is-any-subset-of-size-k-with-0-sum-in-an-array-of-1-and-1/)

给定一个整数 **K** 和一个只包含 **1** 和 **-1** 的数组 **arr** ，任务是找出是否有大小为 **K** 的子集，其元素之和为 **0** 。
**示例:**

> **输入:** arr[] = {1，-1，1}，K = 2
> **输出:**是
> {1，-1}是有效子集
> **输入:** arr[] = {1，1，-1，-1，1}，K = 5
> **输出:**否

**进场:**

*   为了使总和为 **0** ，子集中必须有相等数量的 **1** 和 **-1** 。
*   如果 **K** 为奇数，则没有子集满足给定条件。
*   否则，如果 **K** 是偶数，那么我们需要精确地选择 **(K / 2)** 1 和 **(K / 2)** -1，以便形成子集，使其所有元素的和为 **0**
*   所以，如果 **K** 为偶数且**1 的数量≥ K / 2** 和**的数量-1 的数量≥ K / 2** 则打印**是**否则打印**否**。

以下是上述方法的实现:

## C++

```
// C++ program to find if there is a subset of size
// k with sum 0 in an array of -1 and +1
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of 1's in the array
int countOnes(int n, int a[])
{
    int i, count = 0;
    for (i = 0; i < n; i++)
        if (a[i] == 1)
            count++;
    return count;
}

bool isSubset(int arr[], int n, int k)
{
    int countPos1 = countOnes(n, arr);
    int countNeg1 = n - countPos1;

    // If K is even and there are
    // at least K/2 1's and -1's
    return (k % 2 == 0 && countPos1 >= k / 2 &&
                          countNeg1 >= k / 2);
}

// Driver Program to test above function
int main()
{
    int a[] = { 1, 1, -1, -1, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 5;
    if (isSubset(a, n, k))
      cout << "Yes";
    else
      cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if there is a subset of size
// k with sum 0 in an array of -1 and +1

import java.io.*;

class GFG {

// Function to return the number of 1's in the array
static int countOnes(int n, int a[])
{
    int i, count = 0;
    for (i = 0; i < n; i++)
        if (a[i] == 1)
            count++;
    return count;
}

static boolean isSubset(int arr[], int n, int k)
{
    int countPos1 = countOnes(n, arr);
    int countNeg1 = n - countPos1;

    // If K is even and there are
    // at least K/2 1's and -1's
    return (k % 2 == 0 && countPos1 >= k / 2 &&
                        countNeg1 >= k / 2);
}

// Driver Program to test above function
public static void main (String[] args) {
        int []a = { 1, 1, -1, -1, 1 };
    int n = a.length;
    int k = 5;
    if (isSubset(a, n, k))
     System.out.println( "Yes");
    else
    System.out.println( "No");
    }
}
// This code is contributed by shs
```

## 蟒蛇 3

```
# Python3 program to find if there is
# a subset of size k with sum 0 in an
# array of -1 and +1

# Function to return the number of
# 1's in the array
def countOnes(n, a):

    count = 0
    for i in range(0, n):
        if a[i] == 1:
            count += 1
    return count

def isSubset(arr, n, k):

    countPos1 = countOnes(n, arr)
    countNeg1 = n - countPos1

    # If K is even and there are
    # at least K/2 1's and -1's
    return (k % 2 == 0 and countPos1 >= k // 2 and
                           countNeg1 >= k // 2)

# Driver Code
if __name__ == "__main__":

    a = [1, 1, -1, -1, 1]
    n = len(a)
    k = 5

    if isSubset(a, n, k) == True:
        print("Yes")
    else:
        print("No")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find if there is
// a subset of size k with sum 0
// in an array of -1 and +1
using System;

class GFG
{

// Function to return the number
// of 1's in the array
static int countOnes(int n, int []a)
{
    int i, count = 0;
    for (i = 0; i < n; i++)
        if (a[i] == 1)
            count++;
    return count;
}

static bool isSubset(int []arr,
                     int n, int k)
{
    int countPos1 = countOnes(n, arr);
    int countNeg1 = n - countPos1;

    // If K is even and there are
    // at least K/2 1's and -1's
    return (k % 2 == 0 && countPos1 >= k / 2 &&
                          countNeg1 >= k / 2);
}

// Driver Code
public static void Main ()
{
    int []a = { 1, 1, -1, -1, 1 };
    int n = a.Length;
    int k = 5;
    if (isSubset(a, n, k))
        Console.WriteLine( "Yes");
    else
        Console.WriteLine( "No");
}
}

// This code is contributed by shs
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if there
// is a subset of size k with
// sum 0 in an array of -1 and +1

// Function to return the number
// of 1's in the array
function countOnes($n, $a)
{
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        if ($a[$i] == 1)
            $count++;
    return $count;
}

function isSubset($arr, $n, $k)
{
    $countPos1 = countOnes($n, $arr);
    $countNeg1 = $n - $countPos1;

    // If K is even and there are
    // at least K/2 1's and -1's
    return ($k % 2 == 0 && $countPos1 >= $k / 2 &&
                           $countNeg1 >= $k / 2);
}

// Driver Code
$a = array(1, 1, -1, -1, 1);
$n = sizeof($a);
$k = 5;

if (isSubset($a, $n, $k))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find if there is a subset of size
// k with sum 0 in an array of -1 and +1

// Function to return the number of 1's in the array
function countOnes(n, a)
{
    var i, count = 0;
    for (i = 0; i < n; i++)
        if (a[i] == 1)
            count++;
    return count;
}

function isSubset(arr, n, k)
{
    var countPos1 = countOnes(n, arr);
    var countNeg1 = n - countPos1;

    // If K is even and there are
    // at least K/2 1's and -1's
    return (k % 2 == 0 && countPos1 >= k / 2 &&
                          countNeg1 >= k / 2);
}

// Driver Program to test above function
var a = [1, 1, -1, -1, 1];
var n = a.length;
var k = 5;
if (isSubset(a, n, k))
  document.write( "Yes");
else
  document.write( "No");

// This code is contributed by famously.
</script>
```

**Output:** 

```
No
```

**时间复杂度:** O(n)