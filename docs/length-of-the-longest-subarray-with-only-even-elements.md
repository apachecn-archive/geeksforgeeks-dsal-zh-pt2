# 只有偶数元素的最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/只有偶数元素的最长子阵列的长度/](https://www.geeksforgeeks.org/length-of-the-longest-subarray-with-only-even-elements/)

给定数组 arr[]。任务是找到 arr[]的最长子阵列的长度，使其只包含偶数元素。
**例:**

```
Input : arr[] = { 5, 2, 4, 7 }
Output : Length = 2
subArr[] = {2, 4}

Input : arr[] = {9, 8, 5, 4, 4, 4, 2, 4, 1}
Output : Length 5
subArr[] = {4, 4, 4, 2, 4}
```

其思想是观察只有偶数元素的最大子阵列是阵列中连续偶数元素的最大数量。因此，任务现在减少到找到数组中最大数量的连续偶数元素。
为此，使用两个变量遍历数组， **ans** 和 **current_count** 。变量 *ans* 存储最终答案， **current_count** 存储只有偶数的子阵列长度。
现在每当发现偶数元素时，继续递增 *current_count* ，每当发现奇数元素时，取 *ans* 和 *current_count* 的最大值，并将 *current_count* 重置为零。
最后， *ans* 将存储只有偶数元素的最大子阵列的长度。
以下是上述办法的实施:

## C++

```

// C++ Program to find the Length of the
// largest Subarray with only even elements

#include <cmath>
#include <iostream>
using namespace std;

// Function to find the Length of the
// largest Subarray with only even elements
int maxEvenSubarray(int array[], int N)
{
    int ans = 0;
    int count = 0;

    // Iterate the loop
    for (int i = 0; i < N; i++) {

        // Check whether the element is
        // even in continuous fashion
        if (array[i] % 2 == 0) {
            count++;
            ans = max(ans, count);
        }

        else {

            // If element are not even in continuous
            // fashion, Reinitialize the count
            count = 0;
        }
    }

    // Check for the last element in the array
    ans = max(ans, count);
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 9, 8, 5, 4, 4, 4, 2, 4, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxEvenSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the Length of the longest
// Subarray with only Even Elements
public class GFG {

    // Function to find the Length of the longest
    // Subarray with only Even Elements
    static int maxEvenSubarray(int array[], int N)
    {
        int ans = 0;
        int count = 0;

        // Iterate the loop
        for (int i = 0; i < array.length; i++) {

            // Check whether the element is
            // even in continuous fashion
            if (array[i] % 2 == 0) {
                count++;
                ans = Math.max(ans, count);
            }

            else {
                // If element are not even in continuous
                // fashion. Reinitialize the count
                count = 0;
            }
        }

        // Check for the last element in the array
        ans = Math.max(ans, count);
        return ans;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 9, 8, 5, 4, 4, 4, 2, 4, 1 };

        int N = arr.length;

        System.out.println(maxEvenSubarray(arr, N));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to find the Length of the
# largest Subarray with only even elements

# Function to find the Length of the
# largest Subarray with only even elements
def maxEvenSubarray(array,N):
    ans = 0
    count = 0

    # Iterate the loop
    for i in range(0,N):

        # Check whether the element is
        # even in continuous fashion
        if array[i]%2==0:
            count +=1
            ans = max(ans,count)

        else:

            # If element are not even in continuous
            # fashion, Reinitialize the count
            count = 0

    # Check for the last element in the array
    ans = max(ans,count)
    return ans

# Driver code
if __name__=='__main__':
    arr = [9, 8, 5, 4, 4, 4, 2, 4, 1]
    N = len(arr)
    print(maxEvenSubarray(arr,N))

# This article is contributed by Shrikant13
```

## C#

```
// C# Program to find the Length
// of the largest Subarray with
// only even elements
using System;

class GFG
{
// Function to find the Length
// of the largest Subarray with
// only even elements
static int maxEvenSubarray(int []array,
                           int N)
{
    int ans = 0;
    int count = 0;

    // Iterate the loop
    for (int i = 0; i < N; i++)
    {
        // Check whether the element is
        // even in continuous fashion
        if (array[i] % 2 == 0)
        {
            count++;
            ans = Math.Max(ans, count);
        }
        else
        {
            // If element are not even in
            // continuous fashion,
            // Reinitialize the count
            count = 0;
        }
    }

    // Check for the last
    // element in the array
    ans = Math.Max(ans, count);
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { 9, 8, 5, 4,
                  4, 4, 2, 4, 1 };

    int N = arr.Length;

    Console.WriteLine(maxEvenSubarray(arr, N));
}
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the Length
// of the largest Subarray with
// only even elements

// Function to find the Length
// of the largest Subarray with
// only even elements
function maxEvenSubarray($array, $N)
{
    $ans = 0;
    $count = 0;

    // Iterate the loop
    for ($i = 0; $i < $N; $i++)
    {
        // Check whether the element is
        // even in continuous fashion
        if ($array[$i] % 2 == 0)
        {
            $count++;
            $ans = max($ans, $count);
        }
        else
        {
            // If element are not even in
            // continuous fashion,
            // Reinitialize the count
            $count = 0;
        }
    }

    // Check for the last
    // element in the array
    $ans = max($ans, $count);
    return $ans;
}

// Driver Code
$arr = array( 9, 8, 5, 4,
              4, 4, 2, 4, 1 );
$N = sizeof($arr);

echo maxEvenSubarray($arr, $N);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// Javascript Program to find the Length
// of the largest Subarray with
// only even elements

// Function to find the Length
// of the largest Subarray with
// only even elements
function maxEvenSubarray(array, N)
{
    let ans = 0;
    let count = 0;

    // Iterate the loop
    for (let i = 0; i < N; i++)
    {
        // Check whether the element is
        // even in continuous fashion
        if (array[i] % 2 == 0)
        {
            count++;
            ans = Math.max(ans, count);
        }
        else
        {
            // If element are not even in
            // continuous fashion,
            // Reinitialize the count
            count = 0;
        }
    }

    // Check for the last
    // element in the array
    ans = Math.max(ans, count);
    return ans;
}

// Driver Code
let arr = new Array( 9, 8, 5, 4,
            4, 4, 2, 4, 1 );
let N = arr.length;

document.write(maxEvenSubarray(arr, N));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
5
```

**时间复杂度:** ![  ](img/0faf5aa5dcca41fbedb26b2cadf9f952.png "Rendered by QuickLaTeX.com")