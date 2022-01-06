# 最小化使所有数组元素相等所需的插入和删除的成本

> 原文:[https://www . geesforgeks . org/最小化插入和删除成本-使所有数组元素相等所需的成本/](https://www.geeksforgeeks.org/minimize-cost-of-insertions-and-deletions-required-to-make-all-array-elements-equal/)

给定大小为**N**T6**(1≤N≤10<sup>5</sup>)**的排序后的[数组 **arr[]** ，以及两个整数 **A** 和 B，任务是计算使所有数组元素按增量或减量相等所需的最小成本。每次增减成本分别为 **A** 和 **B** 。](https://www.geeksforgeeks.org/array-data-structure/)

**示例:**

> ***输入:** arr[] = { 2，5，6，9，10，12，15 }，A = 1，B = 2*
> ***输出:** 32*
> ***解释:***
> 增量 arr[0]乘 8，arr[1]乘 5，arr[2]乘 4，arr[3]乘 1，arr[4]乘 0。将 arr[5]减 2，将 arr[6]减 5。
> 因此，arr[]修饰为{ 10，10，10，10，10，10，10 }。
> 因此，所需总成本=(8+5+4+1+0)* 1+(2+5)* 2 = 18+14 = 32
> 
> ***输入:** arr[] = { 2，3，4 }，A = 10，B = 1*
> ***输出:** 3*

**方法:**按照下面的步骤执行:

*   [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   初始化一个新数组来存储累计[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。
*   如果 **A** 和 **B** 都相等，那么中间元素的成本最小。
*   如果 **A** 小于 **B** ，则通过设置**低=中+ 1** ，最小成本要素出现在**中**的右侧。使用[二分搜索法技术](https://www.geeksforgeeks.org/binary-search/)搜索该元素。
*   如果 **A** 大于 **B** ，则最小成本要素出现在**中间**的左侧。通过设置**高=中-1**，使用[二分搜索法技术](https://www.geeksforgeeks.org/binary-search/)搜索该元素。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum cost
// required to make all array elements equal
long long minCost(int arr[], int A,
                  int B, int N)
{

    // Sort the array
    sort(arr, arr + N);

    // Stores the prefix sum and sum
    // of the array respectively
    long long cumarr[N], sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update sum
        sum += arr[i];

        // Update prefix sum
        cumarr[i] = sum;
    }

    // Update middle element
    int mid = (N - 1) / 2;

    // Calculate cost to convert
    // every element to mid element
    long long ans
        = (arr[mid] * (mid + 1)
           - cumarr[mid])
              * A
          + (cumarr[N - 1] - cumarr[mid]
             - (arr[mid] * (N - 1 - mid)))
                * B;

    if (A == B)
        return ans;

    else if (A < B) {
        int low = mid, high = N - 1;

        // Binary search
        while (low <= high) {

            mid = low + (high - low) / 2;

            long long curr
                = (arr[mid] * (mid + 1)
                   - cumarr[mid])
                      * A
                  + (cumarr[N - 1] - cumarr[mid]
                     - (arr[mid] * (N - 1 - mid)))
                        * B;

            if (curr <= ans) {
                ans = curr;
                low = mid + 1;
            }
            else
                high = mid - 1;
        }

        return ans;
    }

    else {
        int low = 0, high = mid;

        // Binary search
        while (low <= high) {
            mid = low + (high - low) / 2;
            long long curr
                = (arr[mid] * (mid + 1)
                   - cumarr[mid])
                      * A
                  + (cumarr[N - 1] - cumarr[mid]
                     - (arr[mid] * (N - 1 - mid)))
                        * B;

            if (curr <= ans) {
                ans = curr;
                high = mid - 1;
            }
            else
                low = mid + 1;
        }

        return ans;
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 5, 6, 9, 10, 12, 15 };
    int A = 1, B = 2;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minCost(arr, A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find minimum cost required
// to make all array elements equal
static int minCost(int[] arr, int A,
                   int B, int N)
{

    // Sort the array
    Arrays.sort(arr);

    // Stores the prefix sum and sum
    // of the array respectively
    int[] cumarr = new int[N];
    int sum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update sum
        sum += arr[i];

        // Update prefix sum
        cumarr[i] = sum;
    }

    // Update middle element
    int mid = (N - 1) / 2;

    // Calculate cost to convert
    // every element to mid element
    int ans = (arr[mid] * (mid + 1) - cumarr[mid]) *
                      A + (cumarr[N - 1] -
            cumarr[mid] - (arr[mid] * (N -
                      1 - mid))) * B;

    if (A == B)
        return ans;

    else if (A < B)
    {
        int low = mid, high = N - 1;

        // Binary search
        while (low <= high)
        {
            mid = low + (high - low) / 2;

            int curr = (arr[mid] * (mid + 1) -
                    cumarr[mid]) * A + (cumarr[N - 1] -
                     cumarr[mid] - (arr[mid] *
                              (N - 1 - mid))) * B;

            if (curr <= ans)
            {
                ans = curr;
                low = mid + 1;
            }
            else
                high = mid - 1;
        }
        return ans;
    }

    else
    {
        int low = 0, high = mid;

        // Binary search
        while (low <= high)
        {
            mid = low + (high - low) / 2;
            int curr = (arr[mid] * (mid + 1) -
                    cumarr[mid]) * A + (cumarr[N - 1] -
                     cumarr[mid] - (arr[mid] * (N - 1 -
                          mid))) * B;

            if (curr <= ans)
            {
                ans = curr;
                high = mid - 1;
            }
            else
                low = mid + 1;
        }
        return ans;
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 5, 6, 9, 10, 12, 15 };
    int A = 1, B = 2;
    int N = (int)(arr.length);

    System.out.println(minCost(arr, A, B, N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find minimum cost required
# to make all array elements equal
def minCost(arr, A, B, N):

    # Sort the array
    arr.sort();

    # Stores the prefix sum and sum
    # of the array respectively
    cumarr = [0]*N;
    sum = 0;

    # Traverse the array
    for i in range(N):

        # Update sum
        sum += arr[i];

        # Update prefix sum
        cumarr[i] = sum;

    # Update middle element
    mid = (N - 1) // 2;

    # Calculate cost to convert
    # every element to mid element
    ans = (arr[mid] * (mid + 1) - cumarr[mid]) * A\
    + (cumarr[N - 1] - cumarr[mid] - (arr[mid] * (N - 1 - mid))) * B;
    if (A == B):
        return ans;
    elif (A < B):
        low = mid; high = N - 1;

        # Binary search
        while (low <= high):
            mid = low + (high - low) // 2;
            curr = (arr[mid] * (mid + 1) - cumarr[mid]) * A\
            + (cumarr[N - 1] - cumarr[mid] - (arr[mid] * (N - 1 - mid))) * B;
            if (curr <= ans):
                ans = curr;
                low = mid + 1;
            else:
                high = mid - 1;
        return ans;
    else:
        low = 0;
        high = mid;

        # Binary search
        while (low <= high):
            mid = low + (high - low) // 2;
            curr = (arr[mid] * (mid + 1) - cumarr[mid]) * A\
            + (cumarr[N - 1] - cumarr[mid] - (arr[mid] * (N - 1 - mid))) * B;
            if (curr <= ans):
                ans = curr;
                high = mid - 1;
            else:
                low = mid + 1;
        return ans;

# Driver Code
if __name__ == '__main__':
    arr = [2, 5, 6, 9, 10, 12, 15];
    A = 1; B = 2;
    N = (int)(len(arr));

    print(minCost(arr, A, B, N));

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to find minimum cost
    // required to make all array elements equal
    static ulong minCost(ulong[] arr, ulong A, ulong B,
                         ulong N)
    {

        // Sort the array
        Array.Sort(arr);

        // Stores the prefix sum and sum
        // of the array respectively
        ulong[] cumarr = new ulong[N];
        ulong sum = 0;

        // Traverse the array
        for (ulong i = 0; i < N; i++)
        {

            // Update sum
            sum += arr[i];

            // Update prefix sum
            cumarr[i] = sum;
        }

        // Update middle element
        ulong mid = (N - 1) / 2;

        // Calculate cost to convert
        // every element to mid element
        ulong ans = (arr[mid] * (mid + 1) - cumarr[mid]) * A
                    + (cumarr[N - 1] - cumarr[mid]
                       - (arr[mid] * (N - 1 - mid)))
                          * B;
        if (A == B)
            return ans;
        else if (A < B) {
            ulong low = mid, high = N - 1;

            // Binary search
            while (low <= high) {

                mid = low + (high - low) / 2;

                ulong curr
                    = (arr[mid] * (mid + 1) - cumarr[mid])
                          * A
                      + (cumarr[N - 1] - cumarr[mid]
                         - (arr[mid] * (N - 1 - mid)))
                            * B;

                if (curr <= ans) {
                    ans = curr;
                    low = mid + 1;
                }
                else
                    high = mid - 1;
            }

            return ans;
        }

        else {
            ulong low = 0, high = mid;

            // Binary search
            while (low <= high) {
                mid = low + (high - low) / 2;
                ulong curr
                    = (arr[mid] * (mid + 1) - cumarr[mid])
                          * A
                      + (cumarr[N - 1] - cumarr[mid]
                         - (arr[mid] * (N - 1 - mid)))
                            * B;

                if (curr <= ans) {
                    ans = curr;
                    high = mid - 1;
                }
                else
                    low = mid + 1;
            }
            return ans;
        }
    }

    // Driver Code
    public static void Main()
    {
        ulong[] arr = { 2, 5, 6, 9, 10, 12, 15 };
        ulong A = 1, B = 2;
        ulong N = (ulong)(arr.Length);
        Console.Write(minCost(arr, A, B, N));
    }
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach   

// Creating the bblSort function
 function bblSort(arr){

 for(var i = 0; i < arr.length; i++){

   // Last i elements are already in place 
   for(var j = 0; j < ( arr.length - i -1 ); j++){

     // Checking if the item at present iteration
     // is greater than the next iteration
     if(arr[j] > arr[j+1]){

       // If the condition is true then swap them
       var temp = arr[j]
       arr[j] = arr[j + 1]
       arr[j+1] = temp
     }
   }
 }
return arr;
}
// Function to find minimum cost required
    // to make all array elements equal
    function minCost(arr , A , B , N) {

        // Sort the array
        arr = bblSort(arr);

        // Stores the prefix sum and sum
        // of the array respectively
        var cumarr = Array(N).fill(0);
        var sum = 0;

        // Traverse the array
        for (i = 0; i < N; i++) {

            // Update sum
            sum += arr[i];

            // Update prefix sum
            cumarr[i] = sum;
        }

        // Update middle element
        var mid = ((N - 1) / 2);

        // Calculate cost to convert
        // every element to mid element
        var ans = (arr[mid] * (mid + 1) - cumarr[mid]) * A
                + (cumarr[N - 1] - cumarr[mid] - (arr[mid] *
                (N - 1 - mid))) * B-2;

        if (A == B)
            return ans;

        else if (A < B) {
            var low = mid, high = N - 1;

            // Binary search
            while (low <= high) {
                mid = low + (high - low) / 2;

                var curr = (arr[mid] * (mid + 1) - cumarr[mid]) * A
                        + (cumarr[N - 2] - cumarr[mid] - (arr[mid] *
                        (N - 1 - mid))) * B;

                if (curr <= ans) {
                    ans = curr;
                    low = mid + 1;
                } else
                    high = mid - 1;
            }
            return ans;
        }

        else {
            var low = 0, high = mid;

            // Binary search
            while (low <= high) {
                mid = low + ((high - low) / 2);
                var curr = (arr[mid] * (mid + 1) - cumarr[mid]) * A
                        + (cumarr[N - 1] - cumarr[mid] - (arr[mid] *
                        (N - 1 - mid))) * B;

                if (curr <= ans) {
                    ans = curr;
                    high = mid - 1;
                } else
                    low = mid + 1;
            }
            return ans;
        }
    }

    // Driver Code

        var arr = [ 2, 5, 6, 9, 10, 12, 15 ];
        var A = 1, B = 2;
        var N = parseInt(arr.length);

        document.write(minCost(arr, A, B, N));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
32
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)