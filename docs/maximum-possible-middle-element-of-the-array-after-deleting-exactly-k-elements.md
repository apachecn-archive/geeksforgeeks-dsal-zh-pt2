# 恰好删除 k 个元素后最大可能的数组中间元素

> 原文:[https://www . geeksforgeeks . org/最大可能-删除-精确-k-元素后的数组中间元素/](https://www.geeksforgeeks.org/maximum-possible-middle-element-of-the-array-after-deleting-exactly-k-elements/)

给定一个大小为 n 的整数数组和一个数字 k。如果索引是基于 1 的，那么数组的中间元素是索引(n + 1) / 2 处的元素，如果 n 是奇数，则为 n / 2。任务是从数组中精确地删除 k 个元素，使得简化数组的中间元素尽可能最大。精确删除 k 个元素后，找到数组中最大可能的中间元素。
**例:**

```
Input :
n = 5, k = 2
arr[] = {9, 5, 3, 7, 10};
Output : 7

Input :
n = 9, k = 3
arr[] = {2, 4, 3, 9, 5, 8, 7, 6, 10};
Output : 9

In the first input, if we delete 5 and 3 then the array becomes {9, 7, 10} and
the middle element will be 7.
In the second input, if we delete one element before 9 and two elements after 9 
(for example 2, 5, 8) then the array becomes {4, 3, 9, 7, 6, 10} and middle 
element will be 9 and it will be the optimum solution.
```

**天真方法:**
天真方法是检查所有可能的解决方案。可能有 C(n，k)种可能的解决方案。如果我们检查所有可能的解决方案来找到一个最佳解决方案，这将消耗大量时间。
**最优方法:**
删除 k 个元素后，数组将缩小到 n–k 的大小，因为我们可以从数组中删除任意 k 个数字来找到最大可能的中间元素。如果我们注意到，删除 k 个元素后中间元素的索引将位于(n+1–k)/2 和(n+1–k)/2+k 的范围内，所以为了找到最优解，只需将数组从索引(n+1–k)/2 迭代到索引(n+1–k)/2+k，并选择该范围内的最大元素。
是下面给出的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum possible middle
// value of the array after deleting exactly k
// elements
int maximum_middle_value(int n, int k, int arr[])
{
    // Initialize answer as -1
    int ans = -1;

    // Calculate range of elements that can give
    // maximum possible middle value of the array
    // since index of maximum possible middle
    // value after deleting exactly k elements from
    // array will lie in between low and high
    int low = (n + 1 - k) / 2;

    int high = (n + 1 - k) / 2 + k;

    // Find maximum element of the array in
    // range low and high
    for (int i = low; i <= high; i++) {

        // since indexing is 1 based so
        // check element at index i - 1
        ans = max(ans, arr[i - 1]);
    }

    // Return the maximum possible middle value
    //  of the array after deleting exactly k
    // elements from the array
    return ans;
}

// Driver Code
int main()
{
    int n = 5, k = 2;
    int arr[] = { 9, 5, 3, 7, 10 };
    cout << maximum_middle_value(n, k, arr) << endl;

    n = 9;
    k = 3;
    int arr1[] = { 2, 4, 3, 9, 5, 8, 7, 6, 10 };
    cout << maximum_middle_value(n, k, arr1) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to calculate maximum possible middle
// value of the array after deleting exactly k
// elements
static int maximum_middle_value(int n, int k, int arr[])
{
    // Initialize answer as -1
    int ans = -1;

    // Calculate range of elements that can give
    // maximum possible middle value of the array
    // since index of maximum possible middle
    // value after deleting exactly k elements from
    // array will lie in between low and high
    int low = (n + 1 - k) / 2;

    int high = (n + 1 - k) / 2 + k;

    // Find maximum element of the array in
    // range low and high
    for (int i = low; i <= high; i++)
    {

        // since indexing is 1 based so
        // check element at index i - 1
        ans = Math.max(ans, arr[i - 1]);
    }

    // Return the maximum possible middle value
    // of the array after deleting exactly k
    // elements from the array
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int n = 5, k = 2;
    int arr[] = { 9, 5, 3, 7, 10 };
    System.out.println( maximum_middle_value(n, k, arr));

    n = 9;
    k = 3;
    int arr1[] = { 2, 4, 3, 9, 5, 8, 7, 6, 10 };
    System.out.println( maximum_middle_value(n, k, arr1));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to calculate maximum possible
# middle value of the array after
# deleting exactly k elements
def maximum_middle_value(n, k, arr):

    # Initialize answer as -1
    ans = -1

    # Calculate range of elements that can give
    # maximum possible middle value of the array
    # since index of maximum possible middle
    # value after deleting exactly k elements
    # from array will lie in between low and high
    low = (n + 1 - k) // 2

    high = (n + 1 - k) // 2 + k

    # Find maximum element of the
    # array in range low and high
    for i in range(low, high+1): 

        # since indexing is 1 based so
        # check element at index i - 1
        ans = max(ans, arr[i - 1])

    # Return the maximum possible middle
    # value of the array after deleting
    # exactly k elements from the array
    return ans

# Driver Code
if __name__ == "__main__":

    n, k = 5, 2
    arr = [9, 5, 3, 7, 10]
    print(maximum_middle_value(n, k, arr))

    n, k = 9, 3
    arr1 = [2, 4, 3, 9, 5, 8, 7, 6, 10] 
    print(maximum_middle_value(n, k, arr1))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to calculate maximum possible middle
// value of the array after deleting exactly k
// elements
static int maximum_middle_value(int n, int k, int []arr)
{
    // Initialize answer as -1
    int ans = -1;

    // Calculate range of elements that can give
    // maximum possible middle value of the array
    // since index of maximum possible middle
    // value after deleting exactly k elements from
    // array will lie in between low and high
    int low = (n + 1 - k) / 2;

    int high = (n + 1 - k) / 2 + k;

    // Find maximum element of the array in
    // range low and high
    for (int i = low; i <= high; i++)
    {

        // since indexing is 1 based so
        // check element at index i - 1
        ans = Math.Max(ans, arr[i - 1]);
    }

    // Return the maximum possible middle value
    // of the array after deleting exactly k
    // elements from the array
    return ans;
}

// Driver Code
static public void Main ()
{

    int n = 5, k = 2;
    int []arr = { 9, 5, 3, 7, 10 };
    Console.WriteLine( maximum_middle_value(n, k, arr));

    n = 9;
    k = 3;
    int []arr1 = { 2, 4, 3, 9, 5, 8, 7, 6, 10 };
    Console.WriteLine( maximum_middle_value(n, k, arr1));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Function to calculate maximum possible middle
// value of the array after deleting exactly k
// elements
function maximum_middle_value(n, k, arr)
{
    // Initialize answer as -1
    let ans = -1;

    // Calculate range of elements that can give
    // maximum possible middle value of the array
    // since index of maximum possible middle
    // value after deleting exactly k elements from
    // array will lie in between low and high
    let low = Math.floor((n + 1 - k) / 2);

    let high = Math.floor(((n + 1 - k) / 2) + k);

    // Find maximum element of the array in
    // range low and high
    for (let i = low; i <= high; i++) {

        // since indexing is 1 based so
        // check element at index i - 1
        ans = Math.max(ans, arr[i - 1]);
    }

    // Return the maximum possible middle value
    // of the array after deleting exactly k
    // elements from the array
    return ans;
}

// Driver Code

    let n = 5, k = 2;
    let arr = [ 9, 5, 3, 7, 10 ];
    document.write(maximum_middle_value(n, k, arr) + "<br>");

    n = 9;
    k = 3;
    let arr1 = [ 2, 4, 3, 9, 5, 8, 7, 6, 10 ];
    document.write(maximum_middle_value(n, k, arr1) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
7
9
```