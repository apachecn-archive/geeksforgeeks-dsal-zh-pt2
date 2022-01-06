# 可以分成 N 个相等部分的杆的最小长度，这些相等部分可以进一步分成给定数量的相等部分

> 原文:[https://www . geeksforgeeks . org/可拆分成 n 个相等部分的最小长度杆可进一步拆分成给定数量的相等部分/](https://www.geeksforgeeks.org/minimum-length-of-a-rod-that-can-be-split-into-n-equal-parts-that-can-further-be-split-into-given-number-of-equal-parts/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到一根杆的最小可能长度，该杆可以被切割成 **N** 相等的部分，这样每一个**I**T10】第部分都可以被切割成**arr【I】**相等的部分。

**示例:**

> **输入:** arr[] = {1，2}
> **输出:** 4
> **说明:**
> 将杆的长度考虑为 4。然后它可以被分成 2 个相等的部分，每个部分都有长度 2。
> 现在，部分 1 可以分成长度为 2 的相等部分 arr[0](= 1)。
> 第 2 部分可以分成长度为 1 的相等部分。
> 因此，杆的最小长度必须为 4。
> 
> **输入:** arr[] = {1，1}
> **输出:** 2

**天真方法:**给定的问题可以基于以下观察来解决:

*   考虑杆的最小长度为 **X** ，然后将此杆切成 **N 等分**，每个部分的长度为 **X/N** 。
*   现在每个 **N 个零件**将再次被切割如下:
    *   **第 1 部分**将被切割成**等份【0】**，每个部分都有一个长度，比如说 <sub>1</sub> 。
    *   **第二部分**将被切成**等份【1】**，每个部分都有一个长度，比如说 <sub>2</sub> 。
    *   **第 3 部分**将被切成**等份【2】**，每个部分都有一个长度，比如说 <sub>3</sub> 。
    *   。
    *   。
    *   。
    *   等等。
*   现在，上述关系也可以写成:

> x/N = arr[0]* a<sub>1</sub>= arr[1]* a<sub>2</sub>=…= arr[N–1]* a<sub>N</sub>。

*   因此，杆的最小长度由下式给出:

> n * LCM(arr[0]* a<sub>1</sub>、arr[1]* a<sub>2</sub>、arr[n-1]* a<sub>n</sub>)

根据以上观察，打印给定数组 **arr[]** 的 **N** 和 [LCM 的乘积值，作为杆的合成最小长度。](https://www.geeksforgeeks.org/lcm-of-given-array-elements/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find GCD
// of two numbers a and b
int gcd(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Find GCD recursively
    return gcd(b, a % b);
}

// Function to find the LCM
// of the resultant array
int findlcm(int arr[], int n)
{
    // Initialize a variable ans
    // as the first element
    int ans = arr[0];

    // Traverse the array
    for (int i = 1; i < n; i++) {

        // Update LCM
        ans = (((arr[i] * ans))
               / (gcd(arr[i], ans)));
    }

    // Return the minimum
    // length of the rod
    return ans;
}

// Function to find the minimum length
// of the rod that can be divided into
// N equals parts and each part can be
// further divided into arr[i] equal parts
void minimumRod(int A[], int N)
{
    // Print the result
    cout << N * findlcm(A, N);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    minimumRod(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to find GCD
    // of two numbers a and b
    static int gcd(int a, int b)
    {
        // Base Case
        if (b == 0)
            return a;

        // Find GCD recursively
        return gcd(b, a % b);
    }

    // Function to find the LCM
    // of the resultant array
    static int findlcm(int arr[], int n)
    {
        // Initialize a variable ans
        // as the first element
        int ans = arr[0];

        // Traverse the array
        for (int i = 1; i < n; i++) {

            // Update LCM
            ans = (((arr[i] * ans)) / (gcd(arr[i], ans)));
        }

        // Return the minimum
        // length of the rod
        return ans;
    }

    // Function to find the minimum length
    // of the rod that can be divided into
    // N equals parts and each part can be
    // further divided into arr[i] equal parts
    static void minimumRod(int A[], int N)
    {
        // Print the result
        System.out.println(N * findlcm(A, N));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2 };
        int N = arr.length;
        minimumRod(arr, N);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find GCD
# of two numbers a and b
def gcd(a, b):

    # Base Case
    if (b == 0):
        return a

    # Find GCD recursively
    return gcd(b, a % b)

# Function to find the LCM
# of the resultant array
def findlcm(arr, n):

    # Initialize a variable ans
    # as the first element
    ans = arr[0]

    # Traverse the array
    for i in range(n):

        # Update LCM
        ans = (((arr[i] * ans)) /
            (gcd(arr[i], ans)))

    # Return the minimum
    # length of the rod
    return ans

# Function to find the minimum length
# of the rod that can be divided into
# N equals parts and each part can be
# further divided into arr[i] equal parts
def minimumRod(A, N):

    # Print the result
    print(int(N * findlcm(A, N)))

# Driver Code
arr = [ 1, 2 ]
N = len(arr)

minimumRod(arr, N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find GCD
    // of two numbers a and b
    static int gcd(int a, int b)
    {

        // Base Case
        if (b == 0)
            return a;

        // Find GCD recursively
        return gcd(b, a % b);
    }

    // Function to find the LCM
    // of the resultant array
    static int findlcm(int[] arr, int n)
    {

        // Initialize a variable ans
        // as the first element
        int ans = arr[0];

        // Traverse the array
        for (int i = 1; i < n; i++) {

            // Update LCM
            ans = (((arr[i] * ans)) / (gcd(arr[i], ans)));
        }

        // Return the minimum
        // length of the rod
        return ans;
    }

    // Function to find the minimum length
    // of the rod that can be divided into
    // N equals parts and each part can be
    // further divided into arr[i] equal parts
    static void minimumRod(int[] A, int N)
    {

        // Print the result
        Console.WriteLine(N * findlcm(A, N));
    }

  // Driver code
    static void Main()
    {
        int[] arr = { 1, 2 };
        int N = arr.Length;
        minimumRod(arr, N);
    }
}

// This code is contributed by sk944795.
```

## java 描述语言

```
<script>

// javascript program for the above approach

    // Function to find GCD
    // of two numbers a and b
    function gcd(a, b)
    {
        // Base Case
        if (b == 0)
            return a;

        // Find GCD recursively
        return gcd(b, a % b);
    }

    // Function to find the LCM
    // of the resultant array
    function findlcm(arr, n)
    {
        // Initialize a variable ans
        // as the first element
        let ans = arr[0];

        // Traverse the array
        for (let i = 1; i < n; i++) {

            // Update LCM
            ans = (((arr[i] * ans)) / (gcd(arr[i], ans)));
        }

        // Return the minimum
        // length of the rod
        return ans;
    }

    // Function to find the minimum length
    // of the rod that can be divided into
    // N equals parts and each part can be
    // further divided into arr[i] equal parts
    function minimumRod(A, N)
    {
        // Print the result
        document.write(N * findlcm(A, N));
    }

// Driver Code

    let arr = [ 1, 2 ];
    let N = arr.length;
    minimumRod(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log M)其中 M 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(N)*