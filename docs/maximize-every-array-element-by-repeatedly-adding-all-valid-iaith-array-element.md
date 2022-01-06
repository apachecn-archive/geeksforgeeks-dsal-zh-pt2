# 通过重复添加所有有效的第 I+a[I]个数组元素

来最大化每个数组元素

> 原文:[https://www . geeksforgeeks . org/通过重复添加所有有效的数组元素来最大化每个数组元素/](https://www.geeksforgeeks.org/maximize-every-array-element-by-repeatedly-adding-all-valid-iaith-array-element/)

给定一个整数[数组](https://www.geeksforgeeks.org/array-data-structure/)，大小为 **N** 的**arr【】**，任务是在每个有效索引处打印所有可能的和，这可以通过添加**I+a【I】th**(*1 基索引*)后续元素直到 **i ≤ N** 来获得。

**示例:**

> ***输入:** arr[]* = {4，1，4}
> ***输出:** 4 5 4*
> **解释:**
> 对于 i = 1，arr[1] = 4。
> 对于 i = 2，arr[2]= arr[2]+arr[2+arr[2]]= arr[2]+arr[2+1]= arr[2]+arr[3]= 1+4 = 5。
> 对于 i = 3，arr[3] = 4。
> 
> ***输入：** 疤痕[]* = {1， 2， 7， 1， 8}
> ***输出：*** 12 11 7 9 8
> ***说明：***
> 】 【T14 for i = 1， arr[1] = scar[1] + scar[1 + 1] + scar[1 + 1] + arr[1 + 1 + 2 + 1] = arr[1] + scar[2] + scar[4] + scar[5] = 1 + 2 + 1 + 8 = 12.
> 对于 i = 2，疤痕[2] = 疤痕[2] + 疤痕[2 + 2] + 疤痕[2 + 2 + 1] = 2 + 1 + 8 = 11。
> 对于 i = 3，疤痕[3] = 7。
> 对于 i = 4，疤痕[4] = 疤痕[4] + 疤痕[4 + 1] = 1 + 8 = 9。
> 当 i = 5 时，总和将出现疤痕[5] = 8。

**天真方法:** 最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并且对于每个 i <sup>第</sup>个索引，不断更新**arr【I】**到**arr【I+arr【I】】**同时 **i ≤ N** 并打印该索引处的和。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法**:上述方法可以通过[反向遍历数组](https://www.geeksforgeeks.org/java-program-to-traverse-through-arraylist-in-reverse-direction/)并将每个访问索引的总和存储到当前索引来优化。最后，打印数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to maximize value
// at every array index by
// performing given operations
int maxSum(int arr[], int N)
{
    int ans = 0;

    // Traverse the array in reverse
    for (int i = N - 1; i >= 0; i--) {

        int t = i;

        // If the current index
        // is a valid index
        if (t + arr[i] < N) {
            arr[i] += arr[t + arr[i]];
        }
    }

    // Print the array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << ' ';
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 7, 1, 8 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    maxSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to maximize value
// at every array index by
// performing given operations
static void maxSum(int[] arr, int N)
{
    int ans = 0;

    // Traverse the array in reverse
    for(int i = N - 1; i >= 0; i--)
    {
        int t = i;

        // If the current index
        // is a valid index
        if (t + arr[i] < N)
        {
            arr[i] += arr[t + arr[i]];
        }
    }

    // Print the array
    for(int i = 0; i < N; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int[] arr = { 1, 2, 7, 1, 8 };

    // Size of the array
    int N = arr.length;

    maxSum(arr, N);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to maximize value
# at every array index by
# performing given operations
def maxSum(arr, N):
    ans = 0;

    # Traverse the array in reverse
    for i in range(N - 1, -1, -1):
        t = i;

        # If the current index
        # is a valid index
        if (t + arr[i] < N):
            arr[i] += arr[t + arr[i]];

    # Prthe array
    for i in range(N):
        print(arr[i], end = " ");

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, 2, 7, 1, 8];

    # Size of the array
    N = len(arr);
    maxSum(arr, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to maximize value
// at every array index by
// performing given operations
static void maxSum(int[] arr, int N)
{

    // Traverse the array in reverse
    for(int i = N - 1; i >= 0; i--)
    {
        int t = i;

        // If the current index
        // is a valid index
        if (t + arr[i] < N)
        {
            arr[i] += arr[t + arr[i]];
        }
    }

    // Print the array
    for(int i = 0; i < N; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver Code
static public void Main()
{

    // Given array
    int[] arr = { 1, 2, 7, 1, 8 };

    // Size of the array
    int N = arr.Length;

    maxSum(arr, N);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to maximize value
// at every array index by
// performing given operations
function maxSum(arr, N)
{
    let ans = 0;

    // Traverse the array in reverse
    for (let i = N - 1; i >= 0; i--) {

        let t = i;

        // If the current index
        // is a valid index
        if (t + arr[i] < N) {
            arr[i] += arr[t + arr[i]];
        }
    }

    // Print the array
    for (let i = 0; i < N; i++) {
         document.write(arr[i] + ' ');
    }
}

// Driver Code

    // Given array
    let arr = [ 1, 2, 7, 1, 8 ];

    // Size of the array
    let N = arr.length;

    maxSum(arr, N);

</script>
```

**Output:** 

```
12 11 7 9 8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)