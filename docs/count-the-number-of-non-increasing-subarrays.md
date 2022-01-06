# 统计非递增子阵数量

> 原文:[https://www . geeksforgeeks . org/count-非递增子阵列的数量/](https://www.geeksforgeeks.org/count-the-number-of-non-increasing-subarrays/)

给定一个 N 个整数的数组。任务是计算不增加的子阵列(大小至少为 1)的数量。

**示例:**

```
Input : arr[] = {1, 4, 3}
Output : 4
The possible subarrays are {1}, {4}, {3}, {4, 3}.

Input :{4, 3, 2, 1}
Output : 10
The possible subarrays are:
{4}, {3}, {2}, {1}, {4, 3}, {3, 2}, {2, 1}, 
{4, 3, 2}, {3, 2, 1}, {4, 3, 2, 1}.
```

**简单的解决方案**:简单的解决方案是生成所有可能的子阵列，对于每个子阵列检查子阵列是否不增加。该解决方案的时间复杂度为 0(N<sup>3</sup>)。

**高效解决方案**:更好的解决方案是利用这样一个事实:如果子阵列 arr[i:j]不是不递增的，那么子阵列 arr[i:j+1]，arr[i:j+2]，..arr[i:n-1]不能是非递增的。因此，开始遍历数组，对于当前子数组，不断增加它的长度，直到它不增加，并更新计数。一旦子阵列开始增加，重置长度。

下面是上述想法的实现:

## C++

```
// C++ program to count number of non
// increasing subarrays
#include <bits/stdc++.h>
using namespace std;

int countNonIncreasing(int arr[], int n)
{
    // Initialize result
    int cnt = 0;

    // Initialize length of current non
    // increasing subarray
    int len = 1;

    // Traverse through the array
    for (int i = 0; i < n - 1; ++i) {

        // If arr[i+1] is less than or equal to arr[i],
        // then increment length
        if (arr[i + 1] <= arr[i])
            len++;

        // Else Update count and reset length
        else {
            cnt += (((len + 1) * len) / 2);
            len = 1;
        }
    }

    // If last length is more than 1
    if (len > 1)
        cnt += (((len + 1) * len) / 2);

    return cnt;
}

// Driver code
int main()
{
    int arr[] = { 5, 2, 3, 7, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countNonIncreasing(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of non
// increasing subarrays
class GFG
{

static int countNonIncreasing(int arr[], int n)
{
    // Initialize result
    int cnt = 0;

    // Initialize length of current non
    // increasing subarray
    int len = 1;

    // Traverse through the array
    for (int i = 0; i < n - 1; ++i)
    {

        // If arr[i+1] is less than or equal to arr[i],
        // then increment length
        if (arr[i + 1] <= arr[i])
            len++;

        // Else Update count and reset length
        else
        {
            cnt += (((len + 1) * len) / 2);
            len = 1;
        }
    }

    // If last length is more than 1
    if (len > 1)
        cnt += (((len + 1) * len) / 2);

    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 2, 3, 7, 1, 1 };
    int n =arr.length;

    System.out.println(countNonIncreasing(arr, n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 program to count number of non
# increasing subarrays
def countNonIncreasing(arr, n):

    # Initialize result
    cnt = 0;

    # Initialize length of current
    # non-increasing subarray
    len = 1;

    # Traverse through the array
    for i in range(0, n - 1):

        # If arr[i+1] is less than
        # or equal to arr[i],
        # then increment length
        if (arr[i + 1] <= arr[i]):
            len += 1;

        # Else Update count and reset length
        else:
            cnt += (((len + 1) * len) / 2);
            len = 1;

    # If last length is more than 1
    if (len > 1):
        cnt += (((len + 1) * len) / 2);

    return int(cnt);

# Driver code
if __name__ == '__main__':
    arr = [5, 2, 3, 7, 1, 1];
    n = len(arr);

    print(countNonIncreasing(arr, n));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to count number of non
// increasing subarrays
using System;

class GFG
{

static int countNonIncreasing(int []arr, int n)
{
    // Initialize result
    int cnt = 0;

    // Initialize length of current non
    // increasing subarray
    int len = 1;

    // Traverse through the array
    for (int i = 0; i < n - 1; ++i)
    {

        // If arr[i+1] is less than or equal to arr[i],
        // then increment length
        if (arr[i + 1] <= arr[i])
            len++;

        // Else Update count and reset length
        else
        {
            cnt += (((len + 1) * len) / 2);
            len = 1;
        }
    }

    // If last length is more than 1
    if (len > 1)
        cnt += (((len + 1) * len) / 2);

    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 5, 2, 3, 7, 1, 1 };
    int n = arr.Length;

    Console.Write(countNonIncreasing(arr, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of non
// increasing subarrays
function countNonIncreasing($arr, $n)
{
    // Initialize result
    $cnt = 0;

    // Initialize length of current non
    // increasing subarray
    $len = 1;

    // Traverse through the array
    for ($i = 0; $i < $n - 1; ++$i)
    {

        // If arr[i+1] is less than
        // or equal to arr[i],
        // then increment length
        if ($arr[$i + 1] <= $arr[$i])
            $len++;

        // Else Update count and reset length
        else
        {
            $cnt += (($len + 1) * $len) / 2;
            $len = 1;
        }
    }

    // If last length is more than 1
    if ($len > 1)
        $cnt += (($len + 1) * $len) / 2;

    return $cnt;
}

// Driver code
$arr = array( 5, 2, 3, 7, 1, 1 );
$n = sizeof($arr);

echo countNonIncreasing($arr, $n);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to count number of non
// increasing subarrays
function countNonIncreasing(arr, n)
{

    // Initialize result
    var cnt = 0;

    // Initialize length of current non
    // increasing subarray
    var len = 1;

    // Traverse through the array
    for(var i = 0; i < n - 1; ++i)
    {

        // If arr[i+1] is less than or equal
        // to arr[i], then increment length
        if (arr[i + 1] <= arr[i])
            len++;

        // Else Update count and reset length
        else
        {
            cnt += parseInt(((len + 1) * len) / 2);
            len = 1;
        }
    }

    // If last length is more than 1
    if (len > 1)
        cnt += parseInt(((len + 1) * len) / 2);

    return cnt;
}

// Driver code
var arr = [ 5, 2, 3, 7, 1, 1 ];
var n = arr.length;

document.write(countNonIncreasing(arr, n));

// This code is contributed by rutvik_56

</script>
```

**Output**

```
10
```

**时间复杂度:**O(N)
T3】辅助空间 : O(1)