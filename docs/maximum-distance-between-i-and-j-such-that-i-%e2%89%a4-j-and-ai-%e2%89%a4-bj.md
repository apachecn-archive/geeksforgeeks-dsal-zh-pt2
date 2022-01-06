# I 和 j 之间的最大距离，使得 i ≤ j 和 A[i] ≤ B[j]

> 原文:[https://www . geesforgeks . org/I-和-j-之间的最大距离-这样-I-% E2 % 89% a4-j-和-ai-%e2%89%a4-bj/](https://www.geeksforgeeks.org/maximum-distance-between-i-and-j-such-that-i-%e2%89%a4-j-and-ai-%e2%89%a4-bj/)

给定两个大小为 **N** 的非递增[阵列](https://www.geeksforgeeks.org/arrays-in-java/) **A[]** 和 **B[]** ，任务是找出 **i** 和 **j** 之间的最大距离，使得 **i ≤ j** 和**A【I】≤B【j】**。

**示例:**

> ***输入:** A[]* = {2，2，2}，B[] = {10，10，1}
> ***输出:** 1*
> **说明:**
> 满足条件的有效对为(0，0)、(0，1)和(1，1)。
> 因此，A[]的指数 0 和 B[]的指数 1 之间的最大距离为 1。
> 
> ***输入:** A[]* = {55，30，5，4，2}，B[] = {100，20，10，10，5}
> ***输出:** 2*
> ***说明:***
> 满足条件的有效对为(0，0)、(2，2)、(2，3)、(2，4)、(3，3)、(3，4)和(4，4)。
> 因此，A[]的指数 2 和 B[]的指数 4 之间的最大距离为 2。

**天真法:**解决问题最简单的方法是遍历数组 A 【】,对于 A【】的每个元素，遍历数组 B【】，找到点与点之间的最大距离，使得 j > =i，B【j】>= A【I】。

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)

**高效方法:**上述方法可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)算法进一步优化。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**为 **0** 来存储两个非递增数组中两个元素之间的最大距离。
*   [使用变量 **i、**在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   初始化两个变量，说**低**为 **i，高**为 **N-1。**
    *   [迭代](https://www.geeksforgeeks.org/java-while-loop-with-examples/)直到**低**小于或等于**高**，并执行以下 **:**
        *   初始化一个变量，说**中间**为**低+(高-低)/2** 。
        *   如果**A【I】**小于等于 **B【中】，**则更新 **ans** 为[最大](https://www.geeksforgeeks.org/stdmax_element-in-cpp/)**T11**ans**和**中 i** 和**低**至**中+1。****
        *   否则，将**高**更新为**中 1。**
*   最后，完成以上步骤后，打印**和**的值作为答案

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum distance
// between two elements satisfying the
// conditions
int maxDistance(int A[], int B[], int N)
{
    // Stores the result
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        int low = i, high = N - 1;

        // Iterate until low is less than
        // or equal to high
        while (low <= high) {

            int mid = low + (high - low) / 2;

            // If A[i] less than equal to B[mid]
            if (A[i] <= B[mid]) {

                // Update answer and low
                ans = max(ans, mid - i);
                low = mid + 1;
            }
            // Otherwise
            else {
                // Update high
                high = mid - 1;
            }
        }
    }

    // Finally, print the ans
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int A[] = { 2, 2, 2 };
    int B[] = { 10, 10, 1 };
    int N = 3;

    // Function Call
    cout << maxDistance(A, B, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to find the maximum distance
    // between two elements satisfying the
    // conditions
    static int maxDistance(int A[], int B[], int N)
    {

        // Stores the result
        int ans = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            int low = i, high = N - 1;

            // Iterate until low is less than
            // or equal to high
            while (low <= high) {

                int mid = low + (high - low) / 2;

                // If A[i] less than equal to B[mid]
                if (A[i] <= B[mid]) {

                    // Update answer and low
                    ans = Math.max(ans, mid - i);
                    low = mid + 1;
                }
                // Otherwise
                else {
                    // Update high
                    high = mid - 1;
                }
            }
        }

        // Finally, print the ans
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Input
        int A[] = { 2, 2, 2 };
        int B[] = { 10, 10, 1 };
        int N = 3;

        // Function Call
        System.out.println(maxDistance(A, B, N));
    }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum distance
# between two elements satisfying the
# conditions
def maxDistance(A, B, N):

    # Stores the result
    ans = 0

    # Traverse the array
    for i in range(N):
        low = i
        high = N - 1

        # Iterate until low is less than
        # or equal to high
        while (low <= high):
            mid = low + (high - low) // 2

            # If A[i] less than equal to B[mid]
            if (A[i] <= B[mid]):

                # Update answer and low
                ans = max(ans, mid - i)
                low = mid + 1

            # Otherwise
            else:

                # Update high
                high = mid - 1

    # Finally, print the ans
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = [ 2, 2, 2 ]
    B = [ 10, 10, 1 ]
    N = 3

    # Function Call
    print(maxDistance(A, B, N))

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{
    // Function to find the maximum distance
    // between two elements satisfying the
    // conditions
    static int maxDistance(int[] A, int[] B, int N)
    {

        // Stores the result
        int ans = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            int low = i, high = N - 1;

            // Iterate until low is less than
            // or equal to high
            while (low <= high) {

                int mid = low + (high - low) / 2;

                // If A[i] less than equal to B[mid]
                if (A[i] <= B[mid]) {

                    // Update answer and low
                    ans = Math.Max(ans, mid - i);
                    low = mid + 1;
                }
                // Otherwise
                else {
                    // Update high
                    high = mid - 1;
                }
            }
        }

        // Finally, print the ans
        return ans;
    }

    // Driver code
    public static void Main()
    {
        // Given Input
        int[] A = { 2, 2, 2 };
        int[] B = { 10, 10, 1 };
        int N = 3;

        // Function Call
        Console.Write(maxDistance(A, B, N));
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function to find the maximum distance
       // between two elements satisfying the
       // conditions
       function maxDistance(A, B, N) {
           // Stores the result
           let ans = 0;

           // Traverse the array
           for (let i = 0; i < N; i++) {

               let low = i, high = N - 1;

               // Iterate until low is less than
               // or equal to high
               while (low <= high) {

                   let mid = low + (high - low) / 2;

                   // If A[i] less than equal to B[mid]
                   if (A[i] <= B[mid]) {

                       // Update answer and low
                       ans = Math.max(ans, mid - i);
                       low = mid + 1;
                   }
                   // Otherwise
                   else {
                       // Update high
                       high = mid - 1;
                   }
               }
           }

           // Finally, prlet the ans
           return ans;
       }

       // Driver Code

       // Given Input
       let A = [2, 2, 2];
       let B = [10, 10, 1];
       let N = 3;

       // Function Call
       document.write(maxDistance(A, B, N));

   // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
1
```

***时间复杂度:** O(N×log(N))*
***辅助空间:** O(1)*

**高效方法:**使用[二指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)可以进一步优化上述方法。按照以下步骤解决问题:

*   初始化两个**变量，**表示， **i，**和 **j** 执行一个双指针。
*   [迭代直到](https://www.geeksforgeeks.org/java-while-loop-with-examples/) **i** 和 **j** 小于 **N** ，执行以下步骤 **:**
    *   如果 **A[i]** 大于 **B[j]，**，那么将 **i** 增加 **1，**，因为数组是以非递增方式排序的。
    *   否则，将 **ans** 和 **j-i、**的 **ans** 更新为[max](https://www.geeksforgeeks.org/stdmax_element-in-cpp/) ，并将 **j** 增加 **1。**
*   最后，完成以上步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum distance
// between two elements in two non increasing
// arrays

int maxDistance(int A[], int B[], int N)
{

    int i = 0, j = 0;
    // Stores the result
    int ans = 0;

    // Iterate while i and j are less than N
    while (i < N && j < N) {

        // If A[i] is greater than B[j]
        if (A[i] > B[j]) {
            ++i;
        }
        // Otherwise,
        else {

            // Update the answer
            ans = max(ans, j - i);

            // Increment j
            j++;
        }
    }

    // Finally, print the ans
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int A[] = { 2, 2, 2 };
    int B[] = { 10, 10, 1 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    cout << maxDistance(A, B, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to find the maximum distance
    // between two elements in two non increasing
    // arrays   
    static int maxDistance(int A[], int B[], int N)
    {

        int i = 0, j = 0;

        // Stores the result
        int ans = 0;

        // Iterate while i and j are less than N
        while (i < N && j < N) {

            // If A[i] is greater than B[j]
            if (A[i] > B[j]) {
                ++i;
            }
            // Otherwise,
            else {

                // Update the answer
                ans = Math.max(ans, j - i);

                // Increment j
                j++;
            }
        }

        // Finally, print the ans
        return ans;
    }

    // Driver Code
    public static void main (String[] args)
    {

        // Given Input
        int A[] = { 2, 2, 2 };
        int B[] = { 10, 10, 1 };
        int N = A.length;

        // Function Call
        System.out.println(maxDistance(A, B, N));
    }
}

// This code is contributed by Shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum distance
# between two elements in two non increasing
# arrays
def maxDistance(A, B, N):

    i = 0
    j = 0

    # Stores the result
    ans = 0

    # Iterate while i and j are less than N
    while (i < N and j < N):

        # If A[i] is greater than B[j]
        if (A[i] > B[j]):
            i += 1

        # Otherwise,
        else:

            # Update the answer
            ans = max(ans, j - i)

            # Increment j
            j += 1

    # Finally, prthe ans
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = [ 2, 2, 2 ]
    B = [ 10, 10, 1 ]
    N = len(A)

    # Function Call
    print(maxDistance(A, B, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the maximum distance
    // between two elements in two non increasing
    // arrays   
    static int maxDistance(int []A, int []B, int N)
    {

        int i = 0, j = 0;

        // Stores the result
        int ans = 0;

        // Iterate while i and j are less than N
        while (i < N && j < N) {

            // If A[i] is greater than B[j]
            if (A[i] > B[j]) {
                ++i;
            }
            // Otherwise,
            else {

                // Update the answer
                ans = Math.Max(ans, j - i);

                // Increment j
                j++;
            }
        }

        // Finally, print the ans
        return ans;
    }

    // Driver Code
    public static void Main (String[] args)
    {

        // Given Input
        int []A = { 2, 2, 2 };
        int []B = { 10, 10, 1 };
        int N = A.Length;

        // Function Call
        Console.Write(maxDistance(A, B, N));
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program for the above approach
// Function to find the maximum distance
// between two elements in two non increasing
// arrays   
function maxDistance( A, B, N)
    {

        var i = 0, j = 0;

        // Stores the result
        var ans = 0;

        // Iterate while i and j are less than N
        while (i < N && j < N) {

            // If A[i] is greater than B[j]
            if (A[i] > B[j]) {
                ++i;
            }

            // Otherwise,
            else {

                // Update the answer
                ans = Math.max(ans, j - i);

                // Increment j
                j++;
            }
        }

        // Finally, print the ans
        return ans;
    }

    // Driver Code
    // Given Input
    var A = [ 2, 2, 2 ];
    var B = [ 10, 10, 1 ];
    var N = A.length;

    // Function Call
    document.write(maxDistance(A, B, N));

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)