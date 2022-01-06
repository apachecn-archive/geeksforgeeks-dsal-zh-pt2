# 切割 N 根绳索产生的所有可能的 K 根等长绳索的最大长度

> 原文:[https://www . geeksforgeeks . org/最大可能长度-k-等长-绳索-通过切割生成-n-绳索/](https://www.geeksforgeeks.org/maximum-length-of-all-possible-k-equal-length-ropes-generated-by-cutting-n-ropes/)

给定一个由代表 **N** 绳索长度的 **N** 正整数和一个正整数 **K** 组成的[数组**arr【】【**，任务是通过将任何绳索切割成任意数量的段来找到频率至少为**K**的绳索的最大长度。](https://www.geeksforgeeks.org/introduction-to-arrays/)

**示例:**

> **输入:** arr[] = {5，2，7，4，9}，K = 5
> **输出:** 4
> **解释:**
> 以下是绳索可能的切割:
> 
> 1.  arr[0](= 5)被切割成{4，1}。
> 2.  arr[2](= 7)被切割成{4，3}。
> 3.  arr[4](= 9)被切割成{4，4，1}。
> 
> 经过上述切割组合后，最大长度为 4，至少是频率(K = 5)。
> 
> **输入:** arr[] = {1，2，3，4，9}，K = 6
> T3】输出: 2

**方法:**给定的问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。按照以下步骤解决问题:

*   初始化 3 个变量，说**低**为 **1** ，**高**为[数组 arr【】](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的最大值， **ans** 为 **-1** ，存储[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的左边界右边界，存储 **K** 绳索的最大可能长度。
*   重复直到**低电平**小于或等于**高电平**，并执行以下步骤:
    *   找到范围的中间值**【低，高】**，并将其存储在一个变量中，比如**中间**。
    *   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**找到长度为**中间**的绳子的数量，可以通过切割绳子获得，并将其存储在一个变量中，比如 **count** 。
    *   如果**计数**的值至少为 **K** ，则将**中**的值更新为**和**，将**低**的值更新为**(中+ 1)** 。
    *   否则，将**高值**更新为**(中-1)**。
*   完成步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum size
// of ropes having frequency at least
// K by cutting the given ropes
int maximumSize(int a[], int k, int n)
{
    // Stores the left and
    // the right boundaries
    int low = 1;
    int high = *max_element(a, a + n);

    // Stores the maximum length
    // of rope possible
    int ans = -1;

    // Iterate while low is less
    // than or equal to high
    while (low <= high) {

        // Stores the mid value of
        // the range [low, high]
        int mid = low + (high - low) / 2;

        // Stores the count of ropes
        // of length mid
        int count = 0;

        // Traverse the array arr[]
        for (int c = 0; c < n; c++) {
            count += a / mid;
        }

        // If count is at least K
        if (count >= k) {

            // Assign mid to ans
            ans = mid;

            // Update the value
            // of low
            low = mid + 1;
        }

        // Otherwise, update the
        // value of high
        else {
            high = mid - 1;
        }
    }

    // Return the value of ans
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 9 };
    int K = 6;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << (maximumSize(arr, K, n));
}

// This code is contributed by ukasp
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the maximum size
    // of ropes having frequency at least
    // K by cutting the given ropes
    static int maximumSize(Integer[] a,
                           int k)
    {
        // Stores the left and
        // the right boundaries
        int low = 1;
        int high = Collections.max(
            Arrays.asList(a));

        // Stores the maximum length
        // of rope possible
        int ans = -1;

        // Iterate while low is less
        // than or equal to high
        while (low <= high) {

            // Stores the mid value of
            // the range [low, high]
            int mid = low + (high - low) / 2;

            // Stores the count of ropes
            // of length mid
            int count = 0;

            // Traverse the array arr[]
            for (int c = 0;
                 c < a.length; c++) {
                count += a / mid;
            }

            // If count is at least K
            if (count >= k) {

                // Assign mid to ans
                ans = mid;

                // Update the value
                // of low
                low = mid + 1;
            }

            // Otherwise, update the
            // value of high
            else {
                high = mid - 1;
            }
        }

        // Return the value of ans
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        Integer[] arr = { 1, 2, 3, 4, 9 };
        int K = 6;
        System.out.println(
            maximumSize(arr, K));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum size
# of ropes having frequency at least
# K by cutting the given ropes
def maximumSize(a, k):

    # Stores the left and
    # the right boundaries
    low = 1
    high = max(a)

    # Stores the maximum length
    # of rope possible
    ans = -1

    # Iterate while low is less
    # than or equal to high
    while (low <= high):

        # Stores the mid value of
        # the range [low, high]
        mid = low + (high - low) // 2

        # Stores the count of ropes
        # of length mid
        count = 0

        # Traverse the array arr[]
        for c in range(len(a)):
            count += a // mid

        # If count is at least K
        if (count >= k):

            # Assign mid to ans
            ans = mid

            # Update the value
            # of low
            low = mid + 1

        # Otherwise, update the
        # value of high
        else:
            high = mid - 1

    # Return the value of ans
    return ans

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 9]
    K = 6
    print(maximumSize(arr, K))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

class GFG{

// Function to find the maximum size
// of ropes having frequency at least
// K by cutting the given ropes
static int maximumSize(int[] a, int k)
{

    // Stores the left and
    // the right boundaries
    int low = 1;
    int high = a.Max();

    // Stores the maximum length
    // of rope possible
    int ans = -1;

    // Iterate while low is less
    // than or equal to high
    while (low <= high)
    {

        // Stores the mid value of
        // the range [low, high]
        int mid = low + (high - low) / 2;

        // Stores the count of ropes
        // of length mid
        int count = 0;

        // Traverse the array []arr
        for(int c = 0;
                c < a.Length; c++)
        {
            count += a / mid;
        }

        // If count is at least K
        if (count >= k)
        {

            // Assign mid to ans
            ans = mid;

            // Update the value
            // of low
            low = mid + 1;
        }

        // Otherwise, update the
        // value of high
        else
        {
            high = mid - 1;
        }
    }

    // Return the value of ans
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 2, 3, 4, 9 };
    int K = 6;

    Console.WriteLine(
        maximumSize(arr, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
        // Javascript program for the above approach

            // Function to find the maximum size
            // of ropes having frequency at least
            // K by cutting the given ropes
            function maximumSize( a, k) {
            // Stores the left and
            // the right boundaries
            let low = 1;
            let high = Math.max.apply(Math, a);

            // Stores the maximum length
            // of rope possible
            let ans = -1;

            // Iterate while low is less
            // than or equal to high
            while (low <= high) {

                // Stores the mid value of
                // the range [low, high]
                let mid = Math.floor(low + (high - low) / 2);

                // Stores the count of ropes
                // of length mid
                let count = 0;

                // Traverse the array arr[]
                for (let c = 0;
                    c < a.length; c++) {
                    count += Math.floor(a / mid);
                }

                // If count is at least K
                if (count >= k) {

                    // Assign mid to ans
                    ans = mid;

                    // Update the value
                    // of low
                    low = mid + 1;
                }

                // Otherwise, update the
                // value of high
                else {
                    high = mid - 1;
                }
            }

            // Return the value of ans
            return ans;
        }

        // Driver Code

        let arr = [ 1, 2, 3, 4, 9 ];
        let K = 6;
        document.write(maximumSize(arr, K))

        // This code is contributed by Hritik
    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*