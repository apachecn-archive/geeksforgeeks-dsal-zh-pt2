# 对总和等于其异或值的子阵列进行计数

> 原文:[https://www . geeksforgeeks . org/count-sum 等于其 xor 值的子数组/](https://www.geeksforgeeks.org/count-subarrays-with-sum-equal-to-its-xor-value/)

给定一个包含 **N** 元素的数组 **arr[]** ，任务是计算子数组的数量，子数组中所有元素的异或等于子数组中所有元素的和。
**例:**

> **输入:** arr[] = {2，5，4，6}
> **输出:** 5
> **说明:**
> 所有子阵{{2}、{5}、{4}、{6}}满足上述条件，因为子阵的异或等于和。除此之外，子阵列{2，5}还满足条件:
> (2 xor 5) = 7 = (2 + 5)
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 7

**天真方法:**这个问题的天真方法是考虑所有子阵列，对于每个子阵列，检查异或是否等于和。
**时间复杂度:** O(N <sup>2</sup> )
**高效途径:**思路是使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)的概念。首先，我们计算满足上述条件的窗口，然后滑动每个元素，直到 n。可以按照以下步骤计算答案:

*   保持两个指针*左*和*右*最初分配为零。
*   使用右指针计算满足条件 A 异或 B = A + B 的窗口。
*   子阵列的计数将为**右–左**。
*   遍历每个元素并移除前一个元素。

以下是上述方法的实现:

## C++

```
// C++ program to count the number
// of subarrays such that Xor of
// all the elements of that subarray
// is equal to sum of the elements

#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to count the number
// of subarrays such that Xor of
// all the elements of that subarray
// is equal to sum of the elements
ll operation(int arr[], int N)
{
    // Maintain two pointers
    // left and right
    ll right = 0, ans = 0,
       num = 0;

    // Iterating through the array
    for (ll left = 0; left < N; left++) {

        // Calculate the window
        // where the above condition
        // is satisfied
        while (right < N
               && num + arr[right]
                      == (num ^ arr[right])) {
            num += arr[right];
            right++;
        }

        // Count will be (right-left)
        ans += right - left;
        if (left == right)
            right++;

        // Remove the previous element
        // as it is already included
        else
            num -= arr[left];
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << operation(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of subarrays such that Xor of all
// the elements of that subarray is
// equal to sum of the elements
import java.io.*;

class GFG{

// Function to count the number
// of subarrays such that Xor of
// all the elements of that subarray
// is equal to sum of the elements
static long operation(int arr[], int N)
{

    // Maintain two pointers
    // left and right
    int right = 0;
    int    num = 0;
    long ans = 0;

    // Iterating through the array
    for(int left = 0; left < N; left++)
    {

       // Calculate the window
       // where the above condition
       // is satisfied
       while (right < N && num + arr[right] ==
                          (num ^ arr[right]))
       {
           num += arr[right];
           right++;
       }

       // Count will be (right-left)
       ans += right - left;
       if (left == right)
           right++;

       // Remove the previous element
       // as it is already included
       else
           num -= arr[left];
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    System.out.println(operation(arr, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to count the number
# of subarrays such that Xor of
# all the elements of that subarray
# is equal to sum of the elements

# Function to count the number
# of subarrays such that Xor of
# all the elements of that subarray
# is equal to sum of the elements
def operation(arr, N):

    # Maintain two pointers
    # left and right
    right = 0; ans = 0;
    num = 0;

    # Iterating through the array
    for left in range(0, N):

        # Calculate the window
        # where the above condition
        # is satisfied
        while (right < N and
               num + arr[right] ==
              (num ^ arr[right])):
            num += arr[right];
            right += 1;

        # Count will be (right-left)
        ans += right - left;
        if (left == right):
            right += 1;

        # Remove the previous element
        # as it is already included
        else:
            num -= arr[left];

    return ans;

# Driver code
arr = [1, 2, 3, 4, 5];
N = len(arr)
print(operation(arr, N));

# This code is contributed by Nidhi_biet
```

## C#

```
// C# program to count the number
// of subarrays such that Xor of all
// the elements of that subarray is
// equal to sum of the elements
using System;
class GFG{

// Function to count the number
// of subarrays such that Xor of
// all the elements of that subarray
// is equal to sum of the elements
static long operation(int []arr, int N)
{

    // Maintain two pointers
    // left and right
    int right = 0;
    int num = 0;
    long ans = 0;

    // Iterating through the array
    for(int left = 0; left < N; left++)
    {

        // Calculate the window
        // where the above condition
        // is satisfied
        while (right < N &&
               num + arr[right] ==
              (num ^ arr[right]))
        {
            num += arr[right];
            right++;
        }

        // Count will be (right-left)
        ans += right - left;
        if (left == right)
            right++;

        // Remove the previous element
        // as it is already included
        else
            num -= arr[left];
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    Console.WriteLine(operation(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to count the number
// of subarrays such that Xor of
// all the elements of that subarray
// is equal to sum of the elements

// Function to count the number
// of subarrays such that Xor of
// all the elements of that subarray
// is equal to sum of the elements
function operation(arr, N)
{
    // Maintain two pointers
    // left and right
    let right = 0, ans = 0,
       num = 0;

    // Iterating through the array
    for (let left = 0; left < N; left++) {

        // Calculate the window
        // where the above condition
        // is satisfied
        while (right < N
               && num + arr[right]
                      == (num ^ arr[right])) {
            num += arr[right];
            right++;
        }

        // Count will be (right-left)
        ans += right - left;
        if (left == right)
            right++;

        // Remove the previous element
        // as it is already included
        else
            num -= arr[left];
    }

    return ans;
}

// Driver code
    let arr = [ 1, 2, 3, 4, 5 ];
    let N = arr.length;

    document.write(operation(arr, N));

</script>
```

**Output:** 

```
7
```

**时间复杂度:** *O(N)* ，其中 N 为数组长度。