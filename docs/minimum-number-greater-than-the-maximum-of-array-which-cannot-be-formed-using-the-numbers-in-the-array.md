# 小于数组最大值的最小数，不能用数组中的数字构成

> 原文:[https://www . geeksforgeeks . org/最小数量大于最大数量的数组-不能使用数组中的数字形成/](https://www.geeksforgeeks.org/minimum-number-greater-than-the-maximum-of-array-which-cannot-be-formed-using-the-numbers-in-the-array/)

给定一个整数数组 **arr[]** ，任务是从数组中找到大于最大元素的最小数量，该元素不能使用数组中的数字来形成(将元素相加以形成其他数字)。如果不存在这样的元素，则打印 **-1** 。

**示例:**

> **输入:** arr[] = {2，6，9}
> **输出:** -1
> 没有大于 9 的数字
> 不能用 2，6，9 构成。
> 
> **输入:** arr[] = {6，7，15}
> **输出:** 16
> 16 是大于 15 的最小数，使用 6，7 和 15 无法形成
> 。

**处理方式:**问题类似于[最小硬币兑换](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)问题，略有修改。首先按升序对数组进行排序，找到最大元素**最大值**，它将是数组最后一个索引处的数字。检查范围**(最大值，2 *最大值)**中的数字以获得答案。如果这个范围内的一个数不能用数组的元素构成，那么这个数就是答案，但是如果所有的数都能在这个范围内构成，那么就不存在不能用数组的元素构成的数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the minimum
// number greater than maximum of the
// array that cannot be formed using the
// elements of the array
int findNumber(int arr[], int n)
{

    // Sort the given array
    sort(arr, arr + n);

    // Maximum number in the array
    int max = arr[n - 1];

    // table[i] will store the minimum number of
    // elements from the array to form i
    int table[(2 * max) + 1];

    table[0] = 0;

    for (int i = 1; i < (2 * max) + 1; i++)
        table[i] = INT_MAX;

    int ans = -1;

    // Calculate the minimum number of elements
    // from the array required to form
    // the numbers from 1 to (2 * max)
    for (int i = 1; i < (2 * max) + 1; i++) {
        for (int j = 0; j < n; j++) {
            if (arr[j] <= i) {
                int res = table[i - arr[j]];
                if (res != INT_MAX && res + 1 < table[i])
                    table[i] = res + 1;
            }
        }

        // If there exists a number greater than
        // the maximum element of the array that can be
        // formed using the numbers of array
        if (i > arr[n - 1] && table[i] == INT_MAX) {
            ans = i;
            break;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 6, 7, 15 };
    int n = (sizeof(arr) / sizeof(int));

    cout << findNumber(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

// Function that returns the minimum
// number greater than maximum of the
// array that cannot be formed using the
// elements of the array
static int findNumber(int arr[], int n)
{

    // Sort the given array
    Arrays.sort(arr);

    // Maximum number in the array
    int max = arr[n - 1];

    // table[i] will store the minimum number of
    // elements from the array to form i
    int table[] = new int[(2 * max) + 1];

    table[0] = 0;

    for (int i = 1; i < (2 * max) + 1; i++)
        table[i] = Integer.MAX_VALUE;

    int ans = -1;

    // Calculate the minimum number of elements
    // from the array required to form
    // the numbers from 1 to (2 * max)
    for (int i = 1; i < (2 * max) + 1; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (arr[j] <= i)
            {
                int res = table[i - arr[j]];
                if (res != Integer.MAX_VALUE && res + 1 < table[i])
                    table[i] = res + 1;
            }
        }

        // If there exists a number greater than
        // the maximum element of the array that can be
        // formed using the numbers of array
        if (i > arr[n - 1] && table[i] == Integer.MAX_VALUE)
        {
            ans = i;
            break;
        }
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 6, 7, 15 };
    int n = arr.length;

    System.out.println(findNumber(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns the minimum
# number greater than Maximum of the
# array that cannot be formed using the
# elements of the array
def findNumber(arr, n):

    # Sort the given array
    arr = sorted(arr)

    # Maximum number in the array
    Max = arr[n - 1]

    # table[i] will store the minimum number of
    # elements from the array to form i
    table = [10**9 for i in range((2 * Max) + 1)]

    table[0] = 0

    ans = -1

    # Calculate the minimum number of elements
    # from the array required to form
    # the numbers from 1 to (2 * Max)
    for i in range(1, 2 * Max + 1):
        for j in range(n):
            if (arr[j] <= i):
                res = table[i - arr[j]]
                if (res != 10**9 and res + 1 < table[i]):
                    table[i] = res + 1

        # If there exists a number greater than
        # the Maximum element of the array that can be
        # formed using the numbers of array
        if (i > arr[n - 1] and table[i] == 10**9):
            ans = i
            break

    return ans

# Driver code
arr = [6, 7, 15]
n = len(arr)

print(findNumber(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns the minimum
// number greater than maximum of the
// array that cannot be formed using the
// elements of the array
static int findNumber(int[] arr, int n)
{

    // Sort the given array
    Array.Sort(arr);

    // Maximum number in the array
    int max = arr[n - 1];

    // table[i] will store the minimum number of
    // elements from the array to form i
    int[] table = new int[(2 * max) + 1];

    table[0] = 0;

    for (int i = 1; i < (2 * max) + 1; i++)
        table[i] = int.MaxValue;

    int ans = -1;

    // Calculate the minimum number of elements
    // from the array required to form
    // the numbers from 1 to (2 * max)
    for (int i = 1; i < (2 * max) + 1; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (arr[j] <= i)
            {
                int res = table[i - arr[j]];
                if (res != int.MaxValue && res + 1 < table[i])
                    table[i] = res + 1;
            }
        }

        // If there exists a number greater than
        // the maximum element of the array that can be
        // formed using the numbers of array
        if (i > arr[n - 1] && table[i] == int.MaxValue)
        {
            ans = i;
            break;
        }
    }

    return ans;
}

// Driver code
public static void Main()
{
    int[] arr = { 6, 7, 15 };
    int n = arr.Length;

    Console.WriteLine(findNumber(arr, n));
}
}

/* This code contributed by Code_Mech */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP
// PHP implementation of the approach
// Function that returns the minimum
// number greater than maximum of the
// array that cannot be formed using the
// elements of the array
function findNumber($arr, $n)
{

    // Sort the given array
    sort($arr);

    // Maximum number in the array
    $max = $arr[$n - 1];

    // table[i] will store the minimum number of
    // elements from the array to form i
    $table = array((2 * $max) + 1);

    $table[0] = 0;

    for ($i = 1; $i < (2 * $max) + 1; $i++)
        $table[$i] = PHP_INT_MAX;

    $ans = -1;

    // Calculate the minimum number of elements
    // from the array required to form
    // the numbers from 1 to (2 * max)
    for ($i = 1; $i < (2 * $max) + 1; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            if ($arr[$j] <= $i)
            {
                $res = $table[$i - $arr[$j]];
                if ($res != PHP_INT_MAX && $res + 1 < $table[$i])
                    $table[$i] = $res + 1;
            }
        }

        // If there exists a number greater than
        // the maximum element of the array that can be
        // formed using the numbers of array
        if ($i > $arr[$n - 1] && $table[$i] == PHP_INT_MAX)
        {
            $ans = $i;
            break;
        }
    }

    return $ans;
}

// Driver code
{
    $arr = array(6, 7, 15 );
    $n = sizeof($arr);

    echo(findNumber($arr, $n));
}

/* This code contributed by Code_Mech*/
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns the minimum
// number greater than maximum of the
// array that cannot be formed using the
// elements of the array
function findNumber(arr, n)
{

    // Sort the given array
    arr.sort((a, b) => a - b);

    // Maximum number in the array
    var max = arr[n - 1];

    // table[i] will store the minimum number of
    // elements from the array to form i
    var table = Array((2 * max) + 1).fill(0);

    table[0] = 0;

    for(i = 1; i < (2 * max) + 1; i++)
        table[i] = Number.MAX_VALUE;

    var ans = -1;

    // Calculate the minimum number of elements
    // from the array required to form
    // the numbers from 1 to (2 * max)
    for(i = 1; i < (2 * max) + 1; i++)
    {
        for(j = 0; j < n; j++)
        {
            if (arr[j] <= i)
            {
                var res = table[i - arr[j]];
                if (res != Number.MAX_VALUE &&
                    res + 1 < table[i])
                    table[i] = res + 1;
            }
        }

        // If there exists a number greater than
        // the maximum element of the array that can be
        // formed using the numbers of array
        if (i > arr[n - 1] &&
            table[i] == Number.MAX_VALUE)
        {
            ans = i;
            break;
        }
    }
    return ans;
}

// Driver code
var arr = [ 6, 7, 15 ];
var n = arr.length;

document.write(findNumber(arr, n));

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
16
```

**时间复杂度:**O(MAX * N)
T3】辅助空间: O(MAX)