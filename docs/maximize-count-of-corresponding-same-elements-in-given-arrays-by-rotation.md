# 通过旋转

最大化给定数组中相应相同元素的数量

> 原文:[https://www . geeksforgeeks . org/最大化旋转给定数组中对应的相同元素的数量/](https://www.geeksforgeeks.org/maximize-count-of-corresponding-same-elements-in-given-arrays-by-rotation/)

给定两个数组 **arr1[]** 和**arr 2[]****N**整数，数组 **arr1[]** 具有不同的元素。任务是通过对数组 **arr1[]** 执行[循环左移或右移，找到给定数组中对应相同元素的最大个数。
**示例:**](https://www.geeksforgeeks.org/array-rotation/) 

> **输入:** arr1[] = { 6，7，3，9，5 }，arr2[] = { 7，3，9，5，6 }
> **输出:** 5
> **解释:**
> 通过对 arr1[]执行循环左移 1。
> 更新数组 arr1[] = {7，3，9，5，6}。
> 此旋转包含数组 arr1[]和 arr2[]之间最大数量的相等元素。
> **输入:** arr1[] = {1，3，2，4}，arr2[] = {4，2，3，1}
> **输出:** 2
> **解释:**
> 通过对数组 arr1[]执行循环左移 1。
> 更新数组 arr1[] = {3，2，4，1}
> 此循环包含数组 arr1[]和 arr2[]之间最大数量的相等元素。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  存储数组中所有元素的位置 **arr2[]** (比如**存储[]** )。
2.  对于数组 **arr1[]** 中的每个元素，执行以下操作:
    *   找出当前元素在**arr 2【】**中的位置与在**arr 1【】**中的位置之间的差异(比如 **diff** )。
    *   如果**差值**小于 0，那么将差值更新为**(N–差值)**。
    *   将电流差**的频率差**存储在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
3.  经过以上步骤，map 中存储的最大频率为**arr 1【】**上旋转后的最大等元数。

以下是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that prints maximum
// equal elements
void maximumEqual(int a[], int b[],
                  int n)
{

    // Vector to store the index
    // of elements of array b
    vector<int> store(1e5);

    // Storing the positions of
    // array B
    for (int i = 0; i < n; i++) {
        store[b[i]] = i + 1;
    }

    // frequency array to keep count
    // of elements with similar
    // difference in distances
    vector<int> ans(1e5);

    // Iterate through all element in arr1[]
    for (int i = 0; i < n; i++) {

        // Calculate number of
        // shift required to
        // make current element
        // equal
        int d = abs(store[a[i]]
                    - (i + 1));

        // If d is less than 0
        if (store[a[i]] < i + 1) {
            d = n - d;
        }

        // Store the frequency
        // of current diff
        ans[d]++;
    }

    int finalans = 0;

    // Compute the maximum frequency
    // stored
    for (int i = 0; i < 1e5; i++)
        finalans = max(finalans,
                       ans[i]);

    // Printing the maximum number
    // of equal elements
    cout << finalans << "\n";
}

// Driver Code
int main()
{
    // Given two arrays
    int A[] = { 6, 7, 3, 9, 5 };
    int B[] = { 7, 3, 9, 5, 6 };

    int size = sizeof(A) / sizeof(A[0]);

    // Function Call
    maximumEqual(A, B, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;
class GFG{

// Function that prints maximum
// equal elements
static void maximumEqual(int a[],
                         int b[], int n)
{

    // Vector to store the index
    // of elements of array b
    int store[] = new int[(int) 1e5];

    // Storing the positions of
    // array B
    for (int i = 0; i < n; i++)
    {
        store[b[i]] = i + 1;
    }

    // frequency array to keep count
    // of elements with similar
    // difference in distances
    int ans[] = new int[(int) 1e5];

    // Iterate through all element in arr1[]
    for (int i = 0; i < n; i++)
    {

        // Calculate number of
        // shift required to
        // make current element
        // equal
        int d = Math.abs(store[a[i]] - (i + 1));

        // If d is less than 0
        if (store[a[i]] < i + 1)
        {
            d = n - d;
        }

        // Store the frequency
        // of current diff
        ans[d]++;
    }

    int finalans = 0;

    // Compute the maximum frequency
    // stored
    for (int i = 0; i < 1e5; i++)
        finalans = Math.max(finalans,
                            ans[i]);

    // Printing the maximum number
    // of equal elements
    System.out.print(finalans + "\n");
}

// Driver Code
public static void main(String[] args)
{
    // Given two arrays
    int A[] = { 6, 7, 3, 9, 5 };
    int B[] = { 7, 3, 9, 5, 6 };

    int size = A.length;

    // Function Call
    maximumEqual(A, B, size);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that prints maximum
# equal elements
def maximumEqual(a, b, n):

    # List to store the index
    # of elements of array b
    store = [0] * 10 ** 5

    # Storing the positions of
    # array B
    for i in range(n):
        store[b[i]] = i + 1

    # Frequency array to keep count
    # of elements with similar
    # difference in distances
    ans = [0] * 10 ** 5

    # Iterate through all element
    # in arr1[]
    for i in range(n):

        # Calculate number of shift
        # required to make current
        # element equal
        d = abs(store[a[i]] - (i + 1))

        # If d is less than 0
        if (store[a[i]] < i + 1):
            d = n - d

        # Store the frequency
        # of current diff
        ans[d] += 1

    finalans = 0

    # Compute the maximum frequency
    # stored
    for i in range(10 ** 5):
        finalans = max(finalans, ans[i])

    # Printing the maximum number
    # of equal elements
    print(finalans)

# Driver Code
if __name__ == '__main__':

    # Given two arrays
    A = [ 6, 7, 3, 9, 5 ]
    B = [ 7, 3, 9, 5, 6 ]

    size = len(A)

    # Function Call
    maximumEqual(A, B, size)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program of the above approach
using System;
class GFG{

// Function that prints maximum
// equal elements
static void maximumEqual(int[] a,
                         int[] b, int n)
{

    // Vector to store the index
    // of elements of array b
    int[] store = new int[(int) 1e5];

    // Storing the positions of
    // array B
    for(int i = 0; i < n; i++)
    {
       store[b[i]] = i + 1;
    }

    // Frequency array to keep count
    // of elements with similar
    // difference in distances
    int[] ans = new int[(int) 1e5];

    // Iterate through all element in arr1[]
    for(int i = 0; i < n; i++)
    {

       // Calculate number of
       // shift required to
       // make current element
       // equal
       int d = Math.Abs(store[a[i]] - (i + 1));

       // If d is less than 0
       if (store[a[i]] < i + 1)
       {
           d = n - d;
       }

       // Store the frequency
       // of current diff
       ans[d]++;
    }

    int finalans = 0;

    // Compute the maximum frequency
    // stored
    for(int i = 0; i < 1e5; i++)
       finalans = Math.Max(finalans, ans[i]);

    // Printing the maximum number
    // of equal elements
    Console.Write(finalans + "\n");
}

// Driver Code
public static void Main()
{

    // Given two arrays
    int[]A = { 6, 7, 3, 9, 5 };
    int[]B = { 7, 3, 9, 5, 6 };

    int size = A.Length;

    // Function Call
    maximumEqual(A, B, size);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// JavaScript program of the above approach

// Function that prlets maximum
// equal elements
function maximumEqual(a, b, n)
{

    // Vector to store the index
    // of elements of array b
    let store = Array.from({length: 1e5}, (_, i) => 0); 

    // Storing the positions of
    // array B
    for (let i = 0; i < n; i++)
    {
        store[b[i]] = i + 1;
    }

    // frequency array to keep count
    // of elements with similar
    // difference in distances
    let ans = Array.from({length: 1e5}, (_, i) => 0); 

    // Iterate through all element in arr1[]
    for (let i = 0; i < n; i++)
    {

        // Calculate number of
        // shift required to
        // make current element
        // equal
        let d = Math.abs(store[a[i]] - (i + 1));

        // If d is less than 0
        if (store[a[i]] < i + 1)
        {
            d = n - d;
        }

        // Store the frequency
        // of current diff
        ans[d]++;
    }

    let finalans = 0;

    // Compute the maximum frequency
    // stored
    for (let i = 0; i < 1e5; i++)
        finalans = Math.max(finalans,
                            ans[i]);

    // Printing the maximum number
    // of equal elements
    document.write(finalans + "\n");
}

// Driver Code

    // Given two arrays
    let A = [ 6, 7, 3, 9, 5 ];
    let B = [ 7, 3, 9, 5, 6 ];

    let size = A.length;

    // Function Call
    maximumEqual(A, B, size);

</script>
```

**Output:** 

```
5
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*