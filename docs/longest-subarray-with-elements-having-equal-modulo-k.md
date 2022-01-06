# 元素模 K 相等的最长子阵列

> 原文:[https://www . geeksforgeeks . org/elements-having-equal-modal-k/](https://www.geeksforgeeks.org/longest-subarray-with-elements-having-equal-modulo-k/)

给定整数 *K* 和整数元素的数组 *arr* ，任务是打印最长子数组的长度，使得该子数组的每个元素在被 *K* 除后产生相同的余数。
**举例:**

> **输入:** arr[] = {2，1，5，8，1}，K = 3
> **输出:** 2
> {2，1，5，8，1}给出余数{2，1，2，2，1}除以 3
> 因此，最长的子阵列长度为 2。
> **输入:** arr[] = {1，100，2，9，4，32，6，3}，K = 2
> **输出:** 3

**简单方法:**

*   从左到右遍历数组，在第二个数组中用 *K* 存储每个元素的模。
*   现在任务简化为寻找具有相同元素的最长子阵列。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
int LongestSubarray(int arr[], int n, int k)
{
    // second array contains modulo
    // results of each element with K
    int arr2[n];
    for (int i = 0; i < n; i++)
        arr2[i] = arr[i] % k;

    int current_length, max_length = 0;
    int j;

    // loop for finding longest sub-array
    // with equal elements
    for (int i = 0; i < n;) {
        current_length = 1;
        for (j = i + 1; j < n; j++) {
            if (arr2[j] == arr2[i])
                current_length++;
            else
                break;
        }
        max_length = max(max_length, current_length);
        i = j;
    }
    return max_length;
}

// Driver code
int main()
{
    int arr[] = { 4, 9, 7, 18, 29, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 11;
    cout << LongestSubarray(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  Java implementation of above approach
import java .io.*;

class GFG
{
// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
static int LongestSubarray(int[] arr,
                        int n, int k)
{
    // second array contains modulo
    // results of each element with K
    int[] arr2 = new int[n];
    for (int i = 0; i < n; i++)
        arr2[i] = arr[i] % k;

    int current_length, max_length = 0;
    int j;

    // loop for finding longest
    // sub-array with equal elements
    for (int i = 0; i < n;)
    {
        current_length = 1;
        for (j = i + 1; j < n; j++)
        {
            if (arr2[j] == arr2[i])
                current_length++;
            else
                break;
        }
        max_length = Math.max(max_length,
                            current_length);
        i = j;
    }
    return max_length;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 4, 9, 7, 18, 29, 11 };
    int n = arr.length;
    int k = 11;
    System.out.println(LongestSubarray(arr, n, k));
}
}

// This code is contributed
// by shs
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# function to find longest sub-array
# whose elements gives same remainder
# when divided with K
def LongestSubarray(arr, n, k):

    # second array contains modulo
    # results of each element with K
    arr2 = [0] * n
    for i in range( n):
        arr2[i] = arr[i] % k

    max_length = 0

    # loop for finding longest sub-array
    # with equal elements
    i = 0
    while i < n :
        current_length = 1
        for j in range(i + 1, n):
            if (arr2[j] == arr2[i]):
                current_length += 1
            else:
                break

        max_length = max(max_length,
                         current_length)
        i = j
        i += 1

    return max_length

# Driver code
if __name__ == "__main__":
    arr = [ 4, 9, 7, 18, 29, 11 ]
    n = len(arr)
    k = 11
    print(LongestSubarray(arr, n, k))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
static int LongestSubarray(int[] arr,
                           int n, int k)
{
    // second array contains modulo
    // results of each element with K
    int[] arr2 = new int[n];
    for (int i = 0; i < n; i++)
        arr2[i] = arr[i] % k;

    int current_length, max_length = 0;
    int j;

    // loop for finding longest
    // sub-array with equal elements
    for (int i = 0; i < n;)
    {
        current_length = 1;
        for (j = i + 1; j < n; j++)
        {
            if (arr2[j] == arr2[i])
                current_length++;
            else
                break;
        }
        max_length = Math.Max(max_length,  
                              current_length);
        i = j;
    }
    return max_length;
}

// Driver code
public static void Main()
{
    int[] arr = { 4, 9, 7, 18, 29, 11 };
    int n = arr.Length;
    int k = 11;
    Console.Write(LongestSubarray(arr, n, k));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
function LongestSubarray($arr, $n, $k)
{
    // second array contains modulo
    // results of each element with K
    $arr2[$n] = array();
    for ($i = 0; $i < $n; $i++)
        $arr2[$i] = $arr[$i] % $k;

    $current_length;
    $max_length = 0;
    $j;

    // loop for finding longest sub-array
    // with equal elements
    for ($i = 0; $i < $n😉
    {
        $current_length = 1;
        for ($j = $i + 1; $j < $n; $j++)
        {
            if ($arr2[$j] == $arr2[$i])
                $current_length++;
            else
                break;
        }
        $max_length = max($max_length,
                          $current_length);
        $i = $j;
    }
    return $max_length;
}

// Driver code
$arr = array( 4, 9, 7, 18, 29, 11 );
$n = sizeof($arr);
$k = 11;
echo LongestSubarray($arr, $n, $k);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
function LongestSubarray(arr, n, k)
{
    // second array contains modulo
    // results of each element with K
    var arr2 = Array(n);
    for (var i = 0; i < n; i++)
        arr2[i] = arr[i] % k;

    var current_length, max_length = 0;
    var j;

    // loop for finding longest sub-array
    // with equal elements
    for (var i = 0; i < n;) {
        current_length = 1;
        for (j = i + 1; j < n; j++) {
            if (arr2[j] == arr2[i])
                current_length++;
            else
                break;
        }
        max_length = Math.max(max_length, current_length);
        i = j;
    }
    return max_length;
}

// Driver code
var arr = [4, 9, 7, 18, 29, 11 ];
var n = arr.length;
var k = 11;
document.write( LongestSubarray(arr, n, k));

</script>
```

**Output**

```
3
```

**时间复杂度:**O(n * n)
T3】辅助空间: O(n)
一种**高效的方法**是在单次遍历中跟踪当前计数。每当我们找到一个模不相同的元素，我们就把计数重置为 0。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
int LongestSubarray(int arr[], int n, int k)
{
    int count = 1;
    int max_length = 1;
    int prev_mod = arr[0] % k;

    // Iterate in the array
    for (int i = 1; i < n; i++) {

        int curr_mod = arr[i] % k;

        // check if array element
        // greater then X or not
        if (curr_mod == prev_mod) {
            count++;
        }
        else {

            max_length = max(max_length, count);  
            count = 1;
            prev_mod = curr_mod;
        }
    }

    return max(max_length, count);
}

// Driver code
int main()
{
    int arr[] = { 4, 9, 7, 18, 29, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 11;
    cout << LongestSubarray(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG {

// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
    static public int LongestSubarray(int arr[], int n, int k) {
        int count = 1;
        int max_length = 1;
        int prev_mod = arr[0] % k;

        // Iterate in the array
        for (int i = 1; i < n; i++) {

            int curr_mod = arr[i] % k;

            // check if array element
            // greater then X or not
            if (curr_mod == prev_mod) {
                count++;
            } else {

                max_length = Math.max(max_length, count);
                count = 1;
                prev_mod = curr_mod;
            }
        }

        return Math.max(max_length, count);
    }

// Driver code
    public static void main(String[] args) {
        int arr[] = {4, 9, 7, 18, 29, 11};
        int n = arr.length;
        int k = 11;
        System.out.print(LongestSubarray(arr, n, k));
    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# function to find longest sub-array
# whose elements gives same remainder
#  when divided with K

def LongestSubarray(arr,n,k):
    count = 1
    max_lenght = 1
    prev_mod = arr[0]%k

    # Iterate in the array
    for i in range(1,n):
        curr_mod = arr[i]%k

       #  check if array element
       # greater then X or not
        if curr_mod==prev_mod:
            count+=1
        else:
            max_lenght = max(max_lenght,count)
            count=1
            prev_mod = curr_mod

    return max(max_lenght,count)

# Driver code
arr = [4, 9, 7, 18, 29, 11]
n = len(arr)
k =11
print(LongestSubarray(arr,n,k))

# This code is contributed by Shrikant13
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
static int LongestSubarray(int []arr, int n, int k)
{
    int count = 1;
    int max_length = 1;
    int prev_mod = arr[0] % k;

    // Iterate in the array
    for (int i = 1; i < n; i++)
    {

        int curr_mod = arr[i] % k;

        // check if array element
        // greater then X or not
        if (curr_mod == prev_mod)
        {
            count++;
        }
        else
        {
            max_length = Math.Max(max_length, count);
            count = 1;
            prev_mod = curr_mod;
        }
    }
    return Math.Max(max_length, count);
}

// Driver code
public static void Main()
{
    int[] arr = { 4, 9, 7, 18, 29, 11 };
    int n = arr.Length;
    int k = 11;
    Console.Write(LongestSubarray(arr, n, k));
}
}

// This code is contributed by Shivi_Aggarwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// function to find longest sub-array
// whose elements gives same remainder
// when divided with K
function LongestSubarray($arr, $n, $k)
{
    $cnt = 1;
    $max_length = 1;
    $prev_mod = $arr[0] % $k;

    // Iterate in the array
    for ($i = 1; $i < $n; $i++)
    {

        $curr_mod = $arr[$i] % $k;

        // check if array element
        // greater then X or not
        if ($curr_mod == $prev_mod)
        {
            $cnt++;
        }
        else
        {
            $max_length = max($max_length, $cnt);
            $cnt = 1;
            $prev_mod = $curr_mod;
        }
    }

    return max($max_length, $cnt);
}

// Driver code
$arr = array( 4, 9, 7, 18, 29, 11 );
$n = count($arr) ;
$k = 11;
echo LongestSubarray($arr, $n, $k);

// This code is contributed by 29AjayKumar
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

    // function to find longest sub-array
// whose elements gives same remainder
// when divided with K
    function LongestSubarray(arr,n,k)
    {
        let count = 1;
        let max_length = 1;
        let prev_mod = arr[0] % k;

        // Iterate in the array
        for (let i = 1; i < n; i++) {

            let curr_mod = arr[i] % k;

            // check if array element
            // greater then X or not
            if (curr_mod == prev_mod) {
                count++;
            } else {

                max_length = Math.max(max_length, count);
                count = 1;
                prev_mod = curr_mod;
            }
        }

        return Math.max(max_length, count);
    }

    // Driver code
    let arr = [4, 9, 7, 18, 29, 11];
    let n = arr.length;
    let k = 11;
    document.write(LongestSubarray(arr, n, k));

// This code is contributed by rag2127
</script>
```

**Output**

```
3
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)