# 元素可以重新排列形成回文的子阵列的数量

> 原文:[https://www . geesforgeks . org/子数组计数-其元素可以重新排列以形成回文/](https://www.geeksforgeeks.org/count-of-sub-arrays-whose-elements-can-be-re-arranged-to-form-palindromes/)

给定一个大小为 **n** 的数组 **arr[]** 。任务是计算可能的子数组的数量，以便它们的元素可以重新排列形成回文。
**例:**

> **输入:** arr[] = {1，2，1，2}
> **输出:** 7
> {1}、{2}、{1}、{2}、{1，2，1}、{2，1，2}和{1，2，1，2}是有效的子数组。
> **输入:** arr[] = {1，2，3，1，2，3，4}
> **输出:** 11

**进场:**有几点观察:

*   为了创建一个偶数长度的回文，所有不同的数字需要有偶数个出现。
*   要创建奇数长度回文，必须只有一个奇数出现次数。

现在，棘手的部分是确定数组的某个特定部分是否能以 O(1)的复杂度变成回文。我们可以用异或来实现这个:

*   对于每个数字 m，我们可以在 xor 计算中将其用作 2^n，以便它包含单个设置位。
*   如果一个部分的所有元素的异或是 **0** ，那么这意味着这个部分的所有不同数字的出现都是偶数。
*   如果一个部分的所有元素的异或大于 **0** ，则意味着:
    *   要么有一个以上不同的奇数出现，在这种情况下，该部分不能重新排列形成回文
    *   或者正好是一个出现次数为奇数的数字(该数字的二进制表示将只有 1 个设置位)。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
typedef signed long long ll;

// Function that returns true if n is a
// power of 2 i.e. n has only 1 set bit
bool is_power_of_two(ll n)
{
    return !(n & (n - 1LL));
}

// Function to return the count
// of all valid sub-arrays
int countSubArrays(int arr[], int n)
{

    // To store the count of valid sub-arrays
    int cnt = 0;

    for (int j = 0; j < n; j++) {
        ll xorval = 0LL;
        for (int k = j; k < n; k++) {

            // num = 2 ^ arr[k]
            ll num = 1LL << arr[k];
            xorval ^= num;

            // If frequency of all the elements of the
            // sub-array is even or there is only a
            // single element with odd frequency
            if (xorval == 0LL || is_power_of_two(xorval))
                cnt++;
        }
    }

    // Return the required count
    return cnt;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countSubArrays(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

static long ll;

// Function that returns true if n is a
// power of 2 i.e. n has only 1 set bit
static boolean is_power_of_two(long n)
{
    //return !(n & (n - 1));
    return false;
}

// Function to return the count
// of all valid sub-arrays
static int countSubArrays(int arr[], int n)
{

    // To store the count of valid sub-arrays
    int cnt = 0;

    for (int j = 0; j < n; j++)
    {
        long xorval = 0;
        for (int k = j; k < n; k++)
        {

            // num = 2 ^ arr[k]
            long num = 1 << arr[k];
            xorval ^= num;

            // If frequency of all the elements of the
            // sub-array is even or there is only a
            // single element with odd frequency
            if (xorval == 0 || is_power_of_two(xorval))
                cnt++;
        }
    }

    // Return the required count
    return cnt;
}

// Driver code
public static void main(String[] args)
{

    int arr[] = { 1, 2, 3, 1, 2, 3, 4 };
    int n = arr.length;
    System.out.println(countSubArrays(arr, n) + "1");
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if n is a
# power of 2 i.e. n has only 1 set bit
def is_power_of_two(n):

    return 0 if(n & (n - 1)) else 1;

# Function to return the count
# of all valid sub-arrays
def countSubArrays(arr, n):

    # To store the count of valid sub-arrays
    cnt = 0;

    for j in range(n):
        xorval = 0;
        for k in range(j, n):

            # num = 2 ^ arr[k]
            num = 1 << arr[k];
            xorval ^= num;

            # If frequency of all the elements of the
            # sub-array is even or there is only a
            # single element with odd frequency
            if (xorval == 0 or is_power_of_two(xorval)):
                cnt += 1;

    # Return the required count
    return cnt;

# Driver code
arr = [ 1, 2, 3, 1, 2, 3, 4 ];
n = len(arr);
print(countSubArrays(arr, n));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

static long ll;

// Function that returns true if n is a
// power of 2 i.e. n has only 1 set bit
static bool is_power_of_two(long n)
{
    //return !(n & (n - 1));
    return false;
}

// Function to return the count
// of all valid sub-arrays
static int countSubArrays(int []arr, int n)
{

    // To store the count of valid sub-arrays
    int cnt = 0;

    for (int j = 0; j < n; j++)
    {
        long xorval = 0;
        for (int k = j; k < n; k++)
        {

            // num = 2 ^ arr[k]
            long num = 1 << arr[k];
            xorval ^= num;

            // If frequency of all the elements of the
            // sub-array is even or there is only a
            // single element with odd frequency
            if (xorval == 0 || is_power_of_two(xorval))
                cnt++;
        }
    }

    // Return the required count
    return cnt;
}

// Driver code
public static void Main(String[] args)
{

    int []arr = { 1, 2, 3, 1, 2, 3, 4 };
    int n = arr.Length;
    Console.WriteLine(countSubArrays(arr, n) + "1");
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if n is a
// power of 2 i.e. n has only 1 set bit
function is_power_of_two($n)
{
    return !($n & ($n - 1));
}

// Function to return the count
// of all valid sub-arrays
function countSubArrays($arr, $n)
{

    // To store the count of valid sub-arrays
    $cnt = 0;

    for ($j = 0; $j < $n; $j++) {
        $xorval = 0;
        for ($k = $j; $k < $n; $k++) {

            // num = 2 ^ arr[k]
            $num = 1 << $arr[$k];
            $xorval ^= $num;

            // If frequency of all the elements of the
            // sub-array is even or there is only a
            // single element with odd frequency
            if ($xorval == 0 || is_power_of_two($xorval))
                $cnt++;
        }
    }

    // Return the required count
    return $cnt;
}

// Driver code

    $arr = array( 1, 2, 3, 1, 2, 3, 4 );
    $n = count($arr);
    echo countSubArrays($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if n is a
// power of 2 i.e. n has only 1 set bit
function is_power_of_two(n)
{
    return !(n & (n - 1));
}

// Function to return the count
// of all valid sub-arrays
function countSubArrays(arr, n)
{

    // To store the count of valid sub-arrays
    let cnt = 0;

    for (let j = 0; j < n; j++) {
        let xorval = 0;
        for (let k = j; k < n; k++) {

            // num = 2 ^ arr[k]
            let num = 1 << arr[k];
            xorval ^= num;

            // If frequency of all the elements of the
            // sub-array is even or there is only a
            // single element with odd frequency
            if (xorval == 0 || is_power_of_two(xorval))
                cnt++;
        }
    }

    // Return the required count
    return cnt;
}

// Driver code

    let arr = [ 1, 2, 3, 1, 2, 3, 4 ];
    let n = arr.length;
    document.write(countSubArrays(arr, n));

</script>
```

**Output:** 

```
11
```