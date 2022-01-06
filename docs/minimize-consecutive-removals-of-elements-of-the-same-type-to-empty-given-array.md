# 最小化相同类型元素的连续移除，以清空给定数组

> 原文:[https://www . geeksforgeeks . org/最小化相同类型的元素到空给定数组的连续移除/](https://www.geeksforgeeks.org/minimize-consecutive-removals-of-elements-of-the-same-type-to-empty-given-array/)

给定一个由 **N** **正**整数组成的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **A[ ]** ，使得每个数组元素 **A <sub>i</sub>** 表示 **i <sup>th</sup>** 类型的元素数，任务是最小化相同类型的连续元素的删除次数以清空给定数组。

**示例:**

> **输入:** A[ ] = {3，3，2}
> **输出:** 0
> **说明:**数组分别由 1 <sup>st</sup> 、2 <sup>nd</sup> 和 3 <sup>rd</sup> 类型的 **3、3、2** 元素组成。通过按{2，1，2，3，1，3，1}的顺序移除数组元素，可以获得一个序列，其中没有两个相同类型的连续元素被移除。因此，计数为 0。
> 
> **输入:** A [ ] = {1，4，1}
> **输出:** 1
> **说明:**数组分别由 1 <sup>st</sup> 、2 <sup>nd</sup> 和 3 <sup>rd</sup> 类型的 1、4、1 个元素组成。通过移除顺序为{ 2，3，2，2，1，2}的数组元素，相同类型元素的连续删除减少到 1。因此，计数为 1。

**进场:**问题可以通过 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 解决。按照以下步骤解决问题:

*   [给定数组排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [计算数组元素的和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   找到数组中最大的[元素，也就是 **A <sub>N-1。</sub>** 。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   如果总和与最大元素之差大于最大元素，则打印 0 作为所需答案。
*   否则，打印**2 * max–sum-1**作为所需答案。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum consecutive
// removals of elements of the same type
void minRemovals(int A[], int N)
{

    // Sort the array
    sort(A, A + N);

    // Stores the maximum element
    // present in the array
    int mx = A[N - 1];

    // Stores sum of the array
    int sum = 1;

    // Calculate sum of the array
    for (int i = 0; i < N; i++) {
        sum += A[i];
    }

    if (sum - mx >= mx) {
        cout << 0 << "\n";
    }
    else {
        cout << 2 * mx - sum << "\n";
    }
}

// Driver Code
int main()
{
    int A[] = { 3, 3, 2 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function call
    minRemovals(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

class GFG 
{

    // Function to count minimum consecutive
    // removals of elements of the same type
    static void minRemovals(int []A, int N)
    {

        // Sort the array
        Arrays.sort(A);

        // Stores the maximum element
        // present in the array
        int mx = A[N - 1];

        // Stores sum of the array
        int sum = 1;

        // Calculate sum of the array
        for (int i = 0; i < N; i++)
        {
            sum += A[i];
        }

        if (sum - mx >= mx) {
            System.out.println(0);
        }
        else {
            System.out.println(2 * mx - sum);
        }
    }

    // Driver Code
    public static void main(String[] args) {

        int []A = { 3, 3, 2 };
        int N = A.length;

        // Function call
        minRemovals(A, N);

    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count minimum consecutive 
# removals of elements of the same type 
def minRemovals(A, N):

    # Sort the array
    A.sort()

    # Stores the maximum element 
    # present in the array 
    mx = A[N - 1]

    # stores the sum of array
    sum = 1

    # Calculate sum of array
    for i in range(0, N):
        sum += A[i]

    if ((sum - mx) >= mx):
        print(0, end = "")
    else:
        print(2 * mx - sum, end = "")

# Driver Code  
if __name__ == "__main__" :

    A = [ 3, 3, 2 ]
    N = len(A)

    # Function call 
    minRemovals(A, N) 

# This code is contributed by Virusbuddah
```

## C#

```
// C# implementation of the above approach
using System;

class GFG 
{

    // Function to count minimum consecutive
    // removals of elements of the same type
    static void minRemovals(int []A, int N)
    {

        // Sort the array
        Array.Sort(A);

        // Stores the maximum element
        // present in the array
        int mx = A[N - 1];

        // Stores sum of the array
        int sum = 1;

        // Calculate sum of the array
        for (int i = 0; i < N; i++)
        {
            sum += A[i];
        }

        if (sum - mx >= mx) 
        {
            Console.WriteLine(0);
        }
        else
        {
            Console.WriteLine(2 * mx - sum);
        }
    }

    // Driver Code
    public static void Main(String[] args) 
    {
        int []A = { 3, 3, 2 };
        int N = A.Length;

        // Function call
        minRemovals(A, N);      
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for above approach

    // Function to count minimum consecutive
    // removals of elements of the same type
    function minRemovals(A, N)
    {

        // Sort the array
        A.sort();

        // Stores the maximum element
        // present in the array
        let mx = A[N - 1];

        // Stores sum of the array
        let sum = 1;

        // Calculate sum of the array
        for (let i = 0; i < N; i++)
        {
            sum += A[i];
        }

        if (sum - mx >= mx) {
             document.write(0);
        }
        else {
             document.write(2 * mx - sum);
        }
    }

// Driver Code

     let A = [3, 3, 2 ];
        let N = A.length;

        // Function call
        minRemovals(A, N);

     // This code is contributed by avijitmondal1998.
</script>
```

**Output**

```
0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)