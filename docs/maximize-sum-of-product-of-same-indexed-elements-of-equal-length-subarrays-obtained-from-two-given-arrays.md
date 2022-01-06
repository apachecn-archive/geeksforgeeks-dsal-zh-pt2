# 最大化从两个给定阵列获得的等长子阵列的相同索引元素的乘积之和

> 原文:[https://www . geeksforgeeks . org/最大化从两个给定数组获得的等长子数组的相同索引元素的乘积之和/](https://www.geeksforgeeks.org/maximize-sum-of-product-of-same-indexed-elements-of-equal-length-subarrays-obtained-from-two-given-arrays/)

给定两个大小分别为 **N** 和 **M** 整数的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和 **brr[]** ，任务是最大化两个等长子阵列的相同索引元素的乘积之和，从阵列 **brr[]** 中选择的子阵列为[反转](https://www.geeksforgeeks.org/reverse-an-array-in-groups-of-given-size/)。

**示例:**

> **输入:** arr[] = {-1，3，-2，4，5}，brr[] = {4，-5}
> **输出:** 26
> **说明:**
> 从 arr[]和 brr[]数组中选择的子阵为{-2，4}和{4，-5}。
> 因此，同索引元素乘积之和= (-2)*(-5) + 4*4 = 26。
> 
> **输入:** arr[] = {1，1，1}，brr[] = {1，1，1}
> **输出:** 3

**方法:**将两个数组中每个元素的乘积存储在一个**【2D】**[**矩阵**](https://www.geeksforgeeks.org/matrix/) 中，在这个 **2D 矩阵**的每一条右对角线上找到和最大的子数组，就可以解决给定的问题，类似于在数组中找到[最大和子数组。按照以下步骤解决问题:](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)

*   初始化一个大小为 **N*M** 的 2D 矩阵 **mat[][]** ，以存储两个数组中每个元素的乘积。
*   [从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **arr[]** 和 **brr[]** 中生成所有可能的对，并将它们存储在 2D 矩阵 **mat[][]** 中。
*   现在，对于等长的子阵列，想法是从第一行和第一列开始遍历矩阵的对角线。
*   在对角线的每次[遍历后](https://www.geeksforgeeks.org/zigzag-or-diagonal-traversal-of-matrix/)将元素存储在一个数组中，然后[找到存储在数组中的元素的最大和子数组](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。
*   完成上述步骤后，打印在上述步骤中获得的所有最大和中的最大和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to store product of each
// pair of elements from two arrays
void store_in_matrix(int a[], int b[],
                     int n1, int n2,
                     int mat[][10])
{
    // Store product of pairs
    // of elements in a matrix
    for (int i = 0; i < n1; i++) {
        for (int j = 0; j < n2; j++) {

            mat[i][j] = (a[i] * b[j]);
        }
    }
}

// Function to find the maximum subarray
// sum in every right diagonal of the matrix
void maxsum_rt_diag(int n1, int n2,
                    int mat[][10], int& ans)
{
    // Stores maximum continuous sum
    int max_ending_here;

    int i, j;

    // Start with each element
    // from the last column
    for (int t = 0; t < n1; t++) {

        i = t;
        j = n2 - 1;
        max_ending_here = 0;

        // Check for each diagonal
        while (i < n1 && j >= 0) {

            max_ending_here = max_ending_here
                              + mat[i][j];
            i++;
            j--;

            // Update ans if max_ending_here
            // is greater than ans
            if (ans < max_ending_here)
                ans = max_ending_here;

            // If max_ending_here is -ve
            if (max_ending_here < 0)

                // Reset it to 0
                max_ending_here = 0;
        }
    }

    // Start with each element
    // from the first row
    for (int t = 0; t < n2; t++) {
        i = 0;
        j = t;
        max_ending_here = 0;

        // Check for each diagonal
        while (i < n1 && j >= 0) {

            max_ending_here = max_ending_here
                              + mat[i][j];
            i++;
            j--;

            // Update ans if max_ending_here
            // is greater than ans
            if (ans < max_ending_here)
                ans = max_ending_here;

            // If max_ending_here is -ve
            if (max_ending_here < 0)

                // Reset to 0
                max_ending_here = 0;
        }
    }
}

// Function to initialize matrix to 0
void initMatrix(int mat[10][10],
                int n1, int n2)
{
    // Traverse each row
    for (int i = 0; i < n1; i++) {

        // Traverse each column
        for (int j = 0; j < n2; j++) {
            mat[i][j] = 0;
        }
    }
}

// Function to find the maximum sum of
// the two equal subarray selected from
// the given two arrays a[] and b[]
void findMaxProduct(int a[], int n1,
                    int b[], int n2)
{

    // Stores the matrix
    int mat[10][10];

    // Initialize each element in mat[] to 0
    initMatrix(mat, n1, n2);

    // Store product of each element
    // from two arrays in a matrix
    store_in_matrix(a, b, n1, n2, mat);

    // Stores the result
    int ans = 0;

    // Find maximum subarray sum in
    // every right diagonal of matrix
    maxsum_rt_diag(n1, n2, mat, ans);

    // Print the maximum sum
    cout << ans << "\n";
}

// Driver Code
int main()
{
    // Initialize two arrays
    int arr[] = { -1, 3, -2, 4, 5 };
    int brr[] = { 4, -5 };

    // Find size of array
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(brr) / sizeof(brr[0]);

    // Function Call
    findMaxProduct(arr, N, brr, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to store product of each
    // pair of elements from two arrays
    static void store_in_matrix(int a[], int b[], int n1,
                                int n2, int mat[][])
    {
        // Store product of pairs
        // of elements in a matrix
        for (int i = 0; i < n1; i++) {
            for (int j = 0; j < n2; j++) {

                mat[i][j] = (a[i] * b[j]);
            }
        }
    }

    // Function to find the maximum subarray
    // sum in every right diagonal of the matrix
    static int maxsum_rt_diag(int n1, int n2, int mat[][])
    {
        // Stores maximum continuous sum
        int max_ending_here;

        int i, j;

        // Stores the result
        int ans = 0;

        // Start with each element
        // from the last column
        for (int t = 0; t < n1; t++) {

            i = t;
            j = n2 - 1;
            max_ending_here = 0;

            // Check for each diagonal
            while (i < n1 && j >= 0) {

                max_ending_here
                    = max_ending_here + mat[i][j];
                i++;
                j--;

                // Update ans if max_ending_here
                // is greater than ans
                if (ans < max_ending_here)
                    ans = max_ending_here;

                // If max_ending_here is -ve
                if (max_ending_here < 0)

                    // Reset it to 0
                    max_ending_here = 0;
            }
        }

        // Start with each element
        // from the first row
        for (int t = 0; t < n2; t++) {
            i = 0;
            j = t;
            max_ending_here = 0;

            // Check for each diagonal
            while (i < n1 && j >= 0) {

                max_ending_here
                    = max_ending_here + mat[i][j];
                i++;
                j--;

                // Update ans if max_ending_here
                // is greater than ans
                if (ans < max_ending_here)
                    ans = max_ending_here;

                // If max_ending_here is -ve
                if (max_ending_here < 0)

                    // Reset to 0
                    max_ending_here = 0;
            }
        }

        return ans;
    }

    // Function to find the maximum sum of
    // the two equal subarray selected from
    // the given two arrays a[] and b[]
    static void findMaxProduct(int a[], int n1, int b[],
                               int n2)
    {

        // Stores the matrix
        int mat[][] = new int[10][10];

        // Store product of each element
        // from two arrays in a matrix
        store_in_matrix(a, b, n1, n2, mat);

        // Stores the result
        int ans = 0;

        // Find maximum subarray sum in
        // every right diagonal of matrix
        ans = maxsum_rt_diag(n1, n2, mat);

        // Print the maximum sum
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Initialize two arrays
        int arr[] = { -1, 3, -2, 4, 5 };
        int brr[] = { 4, -5 };

        // Find size of array
        int N = arr.length;
        int M = brr.length;

        // Function Call
        findMaxProduct(arr, N, brr, M);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to store product of each
# pair of elements from two arrays
def store_in_matrix(a, b, n1, n2, mat):

    # Store product of pairs
    # of elements in a matrix
    for i in range(n1):
        for j in range(n2):
            mat[i][j] = (a[i] * b[j])

# Function to find the maximum subarray
# sum in every right diagonal of the matrix
def maxsum_rt_diag(n1, n2, mat, ans):
    # Stores maximum continuous sum
    max_ending_here=0

    i, j = 0, 0

    # Start with each element
    # from the last column
    for t in range(n1):

        i = t
        j = n2 - 1
        max_ending_here = 0

        # Check for each diagonal
        while (i < n1 and j >= 0):

            max_ending_here = max_ending_here + mat[i][j]
            i += 1
            j -= 1

            # Update ans if max_ending_here
            # is greater than ans
            if (ans < max_ending_here):
                ans = max_ending_here

            # If max_ending_here is -ve
            if (max_ending_here < 0):

                # Reset it to 0
                max_ending_here = 0

    # Start with each element
    # from the first row
    for t in range(n2):
        i = 0
        j = t
        max_ending_here = 0

        # Check for each diagonal
        while (i < n1 and j >= 0):

            max_ending_here = max_ending_here + mat[i][j]
            i += 1
            j -= 1

            # Update ans if max_ending_here
            # is greater than ans
            if (ans < max_ending_here):
                ans = max_ending_here

            # If max_ending_here is -ve
            if (max_ending_here < 0):

                # Reset to 0
                max_ending_here = 0
    return ans

# Function to initialize matrix to 0
def initMatrix(mat, n1, n2):

    # Traverse each row
    for i in range(n1):

        # Traverse each column
        for j in range(n2):
            mat[i][j] = 0

# Function to find the maximum sum of
# the two equal subarray selected from
# the given two arrays a[] and b[]
def findMaxProduct(a, n1, b, n2):

    # Stores the matrix
    mat = [[ 0 for i in range(10)] for i in range(10)]

    # Initialize each element in mat[] to 0
    initMatrix(mat, n1, n2)

    # Store product of each element
    # from two arrays in a matrix
    store_in_matrix(a, b, n1, n2, mat)

    # Stores the result
    ans = 0

    # Find maximum subarray sum in
    # every right diagonal of matrix
    ans = maxsum_rt_diag(n1, n2, mat, ans)

    # Print the maximum sum
    print (ans)

# Driver Code
if __name__ == '__main__':
    # Initialize two arrays
    arr= [-1, 3, -2, 4, 5]
    brr= [4, -5]

    # Find size of array
    N = len(arr)
    M = len(brr)

    # Function Call
    findMaxProduct(arr, N, brr, M)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Function to store product of each
    // pair of elements from two arrays
    static void store_in_matrix(int[] a, int[] b, int n1,
                                int n2, int[, ] mat)
    {
        // Store product of pairs
        // of elements in a matrix
        for (int i = 0; i < n1; i++) {
            for (int j = 0; j < n2; j++) {

                mat[i, j] = (a[i] * b[j]);
            }
        }
    }

    // Function to find the maximum subarray
    // sum in every right diagonal of the matrix
    static int maxsum_rt_diag(int n1, int n2, int[, ] mat)
    {
        // Stores maximum continuous sum
        int max_ending_here;

        int i, j;

        // Stores the result
        int ans = 0;

        // Start with each element
        // from the last column
        for (int t = 0; t < n1; t++) {

            i = t;
            j = n2 - 1;
            max_ending_here = 0;

            // Check for each diagonal
            while (i < n1 && j >= 0) {

                max_ending_here
                    = max_ending_here + mat[i, j];
                i++;
                j--;

                // Update ans if max_ending_here
                // is greater than ans
                if (ans < max_ending_here)
                    ans = max_ending_here;

                // If max_ending_here is -ve
                if (max_ending_here < 0)

                    // Reset it to 0
                    max_ending_here = 0;
            }
        }

        // Start with each element
        // from the first row
        for (int t = 0; t < n2; t++) {
            i = 0;
            j = t;
            max_ending_here = 0;

            // Check for each diagonal
            while (i < n1 && j >= 0) {

                max_ending_here
                    = max_ending_here + mat[i, j];
                i++;
                j--;

                // Update ans if max_ending_here
                // is greater than ans
                if (ans < max_ending_here)
                    ans = max_ending_here;

                // If max_ending_here is -ve
                if (max_ending_here < 0)

                    // Reset to 0
                    max_ending_here = 0;
            }
        }

        return ans;
    }

    // Function to find the maximum sum of
    // the two equal subarray selected from
    // the given two arrays a[] and b[]
    static void findMaxProduct(int[] a, int n1, int[] b,
                               int n2)
    {

        // Stores the matrix
        int[, ] mat = new int[10, 10];

        // Store product of each element
        // from two arrays in a matrix
        store_in_matrix(a, b, n1, n2, mat);

        // Stores the result
        int ans = 0;

        // Find maximum subarray sum in
        // every right diagonal of matrix
        ans = maxsum_rt_diag(n1, n2, mat);

        // Print the maximum sum
        Console.WriteLine(ans);
    }

    // Driver Code
    public static void Main(string[] args)
    {

        // Initialize two arrays
        int[] arr = { -1, 3, -2, 4, 5 };
        int[] brr = { 4, -5 };

        // Find size of array
        int N = arr.Length;
        int M = brr.Length;

        // Function Call
        findMaxProduct(arr, N, brr, M);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

    // Function to store product of each
    // pair of elements from two arrays
   function store_in_matrix(a, b, n1,
                                n2, mat)
    {
        // Store product of pairs
        // of elements in a matrix
        for (let i = 0; i < n1; i++) {
            for (let j = 0; j < n2; j++) {

                mat[i][j] = (a[i] * b[j]);
            }
        }
    }

    // Function to find the maximum subarray
    // sum in every right diagonal of the matrix
    function maxsum_rt_diag(n1, n2, mat)
    {
        // Stores maximum continuous sum
        let max_ending_here;

        let i, j;

        // Stores the result
        let ans = 0;

        // Start with each element
        // from the last column
        for (let t = 0; t < n1; t++) {

            i = t;
            j = n2 - 1;
            max_ending_here = 0;

            // Check for each diagonal
            while (i < n1 && j >= 0) {

                max_ending_here
                    = max_ending_here + mat[i][j];
                i++;
                j--;

                // Update ans if max_ending_here
                // is greater than ans
                if (ans < max_ending_here)
                    ans = max_ending_here;

                // If max_ending_here is -ve
                if (max_ending_here < 0)

                    // Reset it to 0
                    max_ending_here = 0;
            }
        }

        // Start with each element
        // from the first row
        for (let t = 0; t < n2; t++) {
            i = 0;
            j = t;
            max_ending_here = 0;

            // Check for each diagonal
            while (i < n1 && j >= 0) {

                max_ending_here
                    = max_ending_here + mat[i][j];
                i++;
                j--;

                // Update ans if max_ending_here
                // is greater than ans
                if (ans < max_ending_here)
                    ans = max_ending_here;

                // If max_ending_here is -ve
                if (max_ending_here < 0)

                    // Reset to 0
                    max_ending_here = 0;
            }
        }

        return ans;
    }

    // Function to find the maximum sum of
    // the two equal subarray selected from
    // the given two arrays a[] and b[]
    function findMaxProduct(a, n1, b,
                               n2)
    {

        // Stores the matrix
        let mat = new Array(10);
        for (var i = 0; i < mat.length; i++) {
            mat[i] = new Array(2);
        }

        // Store product of each element
        // from two arrays in a matrix
        store_in_matrix(a, b, n1, n2, mat);

        // Stores the result
        let ans = 0;

        // Find maximum subarray sum in
        // every right diagonal of matrix
        ans = maxsum_rt_diag(n1, n2, mat);

        // Print the maximum sum
        document.write(ans);
    }

// Driver Code

    // Initialize two arrays
        let arr = [ -1, 3, -2, 4, 5 ];
        let brr = [ 4, -5 ];

        // Find size of array
        let N = arr.length;
        let M = brr.length;

        // Function Call
        findMaxProduct(arr, N, brr, M);

 // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
26
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*