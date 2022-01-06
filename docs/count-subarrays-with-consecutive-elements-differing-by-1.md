# 计数连续元素相差 1 的子阵列

> 原文:[https://www . geeksforgeeks . org/count-子数组-具有连续元素-相差 1/](https://www.geeksforgeeks.org/count-subarrays-with-consecutive-elements-differing-by-1/)

给定一个由 N 个整数组成的数组 arr[]。任务是计算给定阵列的子阵列总数，使得子阵列中连续元素之间的差为 1。也就是说，对于子阵列中的任何索引![i  ](img/da3a035c66100e6c313a80f2aa178eb3.png "Rendered by QuickLaTeX.com")，**arr[I+1]–arr[I]= 1**。
**注**:不考虑单元素的子阵。
**举例:**

```
Input : arr[] = {1, 2, 3}
Output : 3
The subarrays are {1, 2}. {2, 3} and {1, 2, 3}

Input : arr[] = {1, 2, 3, 5, 6, 7}
Output : 6
```

**天真方法**:一个简单的方法是运行两个嵌套循环，检查每个子阵列，并计算连续元素相差 1 的子阵列的数量。
**有效方法**:一个有效的方法是观察在一个长度为 **K** 的数组中，大小大于 1 的子数组的总数= (K)*(K-1)/2。
所以，想法是通过使用两个指针来遍历数组，以计算在最大长度的窗口中具有连续元素的子阵列，然后使用上述公式计算该窗口中的所有子阵列。
下面是分步算法:

*   取两个指针表示*快*和*慢*，保持一个连续元素的窗口。
*   开始遍历数组。
*   如果元素相差 1，则仅递增快速指针。
*   否则，计算当前窗口在索引*快*和*慢*之间的长度。

下面是给定方法的实现:

## C++

```
// C++ program to count Subarrays with
// Consecutive elements differing by 1

#include <iostream>
using namespace std;

// Function to count Subarrays with
// Consecutive elements differing by 1
int subarrayCount(int arr[], int n)
{
    // Variable to store count of subarrays
    // whose consecutive elements differ by 1
    int result = 0;

    // Take two pointers for maintaining a
    // window of consecutive elements
    int fast = 0, slow = 0;

    // Traverse the array
    for (int i = 1; i < n; i++) {

        // If elements differ by 1
        // increment only the fast pointer
        if (arr[i] - arr[i - 1] == 1) {
            fast++;
        }
        else {

            // Calculate length of subarray
            int len = fast - slow + 1;

            // Calculate total subarrays except
            // Subarrays with single element
            result += len * (len - 1) / 2;

            // Update fast and slow
            fast = i;
            slow = i;
        }
    }

    // For last iteration. That is if array is
    // traversed and fast > slow
    if (fast != slow) {
        int len = fast - slow + 1;
        result += len * (len - 1) / 2;
    }

    return result;
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << subarrayCount(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count Subarrays with
// Consecutive elements differing by 1
class cfg
{

// Function to count Subarrays with
// Consecutive elements differing by 1
static int subarrayCount(int arr[], int n)
{
    // Variable to store count of subarrays
    // whose consecutive elements differ by 1
    int result = 0;

    // Take two pointers for maintaining a
    // window of consecutive elements
    int fast = 0, slow = 0;

    // Traverse the array
    for (int i = 1; i < n; i++) {

        // If elements differ by 1
        // increment only the fast pointer
        if (arr[i] - arr[i - 1] == 1) {
            fast++;
        }
        else {

            // Calculate length of subarray
            int len = fast - slow + 1;

            // Calculate total subarrays except
            // Subarrays with single element
            result += len * (len - 1) / 2;

            // Update fast and slow
            fast = i;
            slow = i;
        }
    }

    // For last iteration. That is if array is
    // traversed and fast > slow
    if (fast != slow) {
        int len = fast - slow + 1;
        result += len * (len - 1) / 2;
    }

    return result;
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 1, 2, 3, 5, 6, 7 };
    int n = arr.length;

    System.out.println(subarrayCount(arr, n));

}
}
//This code is contributed by Mukul Singh
```

## 蟒蛇 3

```
# Python3 program to count Subarrays with
# Consecutive elements differing by 1

# Function to count Subarrays with
# Consecutive elements differing by 1
def subarrayCount(arr, n) :

    # Variable to store count of subarrays
    # whose consecutive elements differ by 1
    result = 0

    # Take two pointers for maintaining a
    # window of consecutive elements
    fast, slow = 0, 0

    # Traverse the array
    for i in range(1, n) :

        # If elements differ by 1
        # increment only the fast pointer
        if (arr[i] - arr[i - 1] == 1) :
            fast += 1

        else :

            # Calculate length of subarray
            length = fast - slow + 1

            # Calculate total subarrays except
            # Subarrays with single element
            result += length * (length - 1) // 2;

            # Update fast and slow
            fast = i
            slow = i

    # For last iteration. That is if array is
    # traversed and fast > slow
    if (fast != slow) :
        length = fast - slow + 1
        result += length * (length - 1) // 2;

    return result

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 5, 6, 7 ]
    n = len(arr)

    print(subarrayCount(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# program to count Subarrays with
// Consecutive elements differing by 1
using System;
class cfg
{

// Function to count Subarrays with
// Consecutive elements differing by 1
static int subarrayCount(int []arr, int n)
{
    // Variable to store count of subarrays
    // whose consecutive elements differ by 1
    int result = 0;

    // Take two pointers for maintaining a
    // window of consecutive elements
    int fast = 0, slow = 0;

    // Traverse the array
    for (int i = 1; i < n; i++) {

        // If elements differ by 1
        // increment only the fast pointer
        if (arr[i] - arr[i - 1] == 1) {
            fast++;
        }
        else {

            // Calculate length of subarray
            int len = fast - slow + 1;

            // Calculate total subarrays except
            // Subarrays with single element
            result += len * (len - 1) / 2;

            // Update fast and slow
            fast = i;
            slow = i;
        }
    }

    // For last iteration. That is if array is
    // traversed and fast > slow
    if (fast != slow) {
        int len = fast - slow + 1;
        result += len * (len - 1) / 2;
    }

    return result;
}

// Driver Code
public static void Main()
{

    int []arr = { 1, 2, 3, 5, 6, 7 };
    int n = arr.Length;

    Console.WriteLine(subarrayCount(arr, n));

}
}
//This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count Subarrays with
// Consecutive elements differing by 1

// Function to count Subarrays with
// Consecutive elements differing by 1
function subarrayCount($arr, $n)
{
    // Variable to store count of subarrays
    // whose consecutive elements differ by 1
    $result = 0;

    // Take two pointers for maintaining a
    // window of consecutive elements
    $fast = 0; $slow = 0;

    // Traverse the array
    for ($i = 1; $i < $n; $i++)
    {

        // If elements differ by 1
        // increment only the fast pointer
        if ($arr[$i] - $arr[$i - 1] == 1)
        {
            $fast++;
        }
        else
        {

            // Calculate length of subarray
            $len = $fast - $slow + 1;

            // Calculate total subarrays except
            // Subarrays with single element
            $result += $len * ($len - 1) / 2;

            // Update fast and slow
            $fast = $i;
            $slow = $i;
        }
    }

    // For last iteration. That is if array
    // is traversed and fast > slow
    if ($fast != $slow)
    {
        $len = $fast - $slow + 1;
        $result += $len * ($len - 1) / 2;
    }

    return $result;
}

// Driver Code
$arr = array(1, 2, 3, 5, 6, 7);
$n = sizeof($arr);

echo subarrayCount($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to count Subarrays with
// Consecutive elements differing by 1

    // Function to count Subarrays with
    // Consecutive elements differing by 1
    function subarrayCount(arr , n) {
        // Variable to store count of subarrays
        // whose consecutive elements differ by 1
        var result = 0;

        // Take two pointers for maintaining a
        // window of consecutive elements
        var fast = 0, slow = 0;

        // Traverse the array
        for (i = 1; i < n; i++) {

            // If elements differ by 1
            // increment only the fast pointer
            if (arr[i] - arr[i - 1] == 1) {
                fast++;
            } else {

                // Calculate length of subarray
                var len = fast - slow + 1;

                // Calculate total subarrays except
                // Subarrays with single element
                result += len * (len - 1) / 2;

                // Update fast and slow
                fast = i;
                slow = i;
            }
        }

        // For last iteration. That is if array is
        // traversed and fast > slow
        if (fast != slow) {
            var len = fast - slow + 1;
            result += len * (len - 1) / 2;
        }

        return result;
    }

    // Driver Code

        var arr = [ 1, 2, 3, 5, 6, 7 ];
        var n = arr.length;

        document.write(subarrayCount(arr, n));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
6
```

**时间复杂度** : O(N)
**辅助空间** : (1)