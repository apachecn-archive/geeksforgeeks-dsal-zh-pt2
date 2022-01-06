# 通过从一个或两个

中递减一个值来最小化操作，使两个数组相等

> 原文:[https://www . geeksforgeeks . org/最小化-操作-使两个数组相等-从两个或其中之一减去一个值/](https://www.geeksforgeeks.org/minimize-operations-to-make-both-arrays-equal-by-decrementing-a-value-from-either-or-both/)

假设两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**具有 **N** 个整数，任务是找到使两个数组的所有元素在每次操作时相等所需的**个最小**个操作，可以完成以下操作:

*   将**A【I】**的值减 **1** ，其中 **i** 位于范围**【0，N)** 内。
*   将 **B[i]** 的值递减 **1** ，其中 **i** 位于范围**【0，N)** 内。
*   将 **A[i]** 和 **B[i]** 的值递减 **1** ，其中 **i** 位于**【0，N)** 范围内。

**注:**阵中元素 **A[]** 和 **B[]** 不必相等。

**示例:**

> **输入:** arr1[] = {1，2，3}，arr2[] = {5，4，3}
> **输出:** 5
> **说明:**操作可以通过以下方式进行:
> 
> 1.  将索引 2 处的元素减 1。因此，A[] = {1，2，2}。
> 2.  将索引 2 处的元素减 1。因此，A[] = {1，2，1}。
> 3.  将 B[]的索引 0 处的元素减 1。因此，B[] = {4，4，3}。
> 4.  将 B[]的索引 0 处的元素减 1。因此，B[] = {3，4，3}。
> 5.  将 A[]和 B[]的索引 1 处的元素减 1。因此 A[] = {1，1，1}和 B[] = {3，3，3}
> 
> 因此，阵列 A[]和 B[]的所有元素可以在 5 次运算中相等，这是最小可能的。
> 
> **输入:** A[] = {7，2，8，5，3}，B[] = {3，4，5，9，1}，N = 5
> T3】输出: 23

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。由于所有可能的操作只减少数组值，所有元素必须等于给定数组中的[最小元素。假设 **min_A** 和 **min_B** 分别是数组 **A[]** 和 **B[]** 中的最小整数。因此，要求的答案将是 **i** 在**【0，N】**范围内的所有可能值的**最大值(A[I]–min _ A，B[I]–min _ B)**之和。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum operations
// required to make elements of each array
// equal of the given two arrays
int minOperations(int a[], int b[], int N)
{
    // Stores the minimum element in array a[]
    int min_a = *min_element(a, a + N);

    // Stores the minimum element in array b[]
    int min_b = *min_element(b, b + N);

    // Variable to store the required ans
    int ans = 0;

    // Iterate over the elements
    for (int i = 0; i < N; i++) {
        // Store the difference between current
        // element and minimum of respective array
        int x = a[i] - min_a;
        int y = b[i] - min_b;

        // Add maximum of x and y to ans
        ans += max(x, y);
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int a[] = { 7, 2, 8, 5, 3 };
    int b[] = { 3, 4, 5, 9, 1 };

    int N = sizeof(a) / sizeof(b[0]);

    cout << minOperations(a, b, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG
{
// Function to find the minimum operations
// required to make elements of each array
// equal of the given two arrays
static int minOperations(int []a, int []b, int N)
{
    // Stores the minimum element in array a[]
    int min_a = Arrays.stream(a).min().getAsInt();

    // Stores the minimum element in array b[]
    int min_b = Arrays.stream(b).min().getAsInt();

    // Variable to store the required ans
    int ans = 0;

    // Iterate over the elements
    for (int i = 0; i < N; i++) {
        // Store the difference between current
        // element and minimum of respective array
        int x = a[i] - min_a;
        int y = b[i] - min_b;

        // Add maximum of x and y to ans
        ans += Math.max(x, y);
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int []a = { 7, 2, 8, 5, 3 };
    int []b = { 3, 4, 5, 9, 1 };
    int N = a.length;

    System.out.println(minOperations(a, b, N));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum operations
# required to make elements of each array
# equal of the given two arrays
def minOperations(a, b, N):

    # Stores the minimum element in array a[]
    min_a = min(a)

    # Stores the minimum element in array b[]
    min_b = min(b)

    # Variable to store the required ans
    ans = 0

    # Iterate over the elements
    for i in range(N):

       # Store the difference between current
       # element and minimum of respective array
        x = a[i] - min_a
        y = b[i] - min_b

       # Add maximum of x and y to ans
        ans += max(x, y)

    # Return Answer
    return ans

# Driver Code
if __name__ == "__main__":
    a = [7, 2, 8, 5, 3]
    b = [3, 4, 5, 9, 1]
    N = len(a)
    print(minOperations(a, b, N))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

public class GFG
{
// Function to find the minimum operations
// required to make elements of each array
// equal of the given two arrays
static int minOperations(int []a, int []b, int N)
{
    // Stores the minimum element in array a[]
    int min_a = a.Min();

    // Stores the minimum element in array b[]
    int min_b = b.Min();

    // Variable to store the required ans
    int ans = 0;

    // Iterate over the elements
    for (int i = 0; i < N; i++) {
        // Store the difference between current
        // element and minimum of respective array
        int x = a[i] - min_a;
        int y = b[i] - min_b;

        // Add maximum of x and y to ans
        ans += Math.Max(x, y);
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void Main()
{
    int []a = { 7, 2, 8, 5, 3 };
    int []b = { 3, 4, 5, 9, 1 };
    int N = a.Length;

    Console.Write(minOperations(a, b, N));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum operations
// required to make elements of each array
// equal of the given two arrays
function minOperations(a, b, N)
{
    // Stores the minimum element in array a[]
    let min_a = Math.min.apply(Math,a);

    // Stores the minimum element in array b[]
    let min_b = Math.min.apply(Math,b);

    // Variable to store the required ans
    let ans = 0;

    // Iterate over the elements
    for (let i = 0; i < N; i++) {
        // Store the difference between current
        // element and minimum of respective array
        let x = a[i] - min_a;
        let y = b[i] - min_b;

        // Add maximum of x and y to ans
        ans += Math.max(x, y);
    }

    // Return Answer
    return ans;
}

// Driver Code
let a = [ 7, 2, 8, 5, 3 ];
let b = [ 3, 4, 5, 9, 1 ];
let N = a.length;

document.write(minOperations(a, b, N));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
23
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)