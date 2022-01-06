# 在数组中找到一个划分点，使其异或和最大化

> 原文:[https://www . geesforgeks . org/find-a-partition-in-point-array-to-maximum-its-xor-sum/](https://www.geeksforgeeks.org/find-a-partition-point-in-array-to-maximize-its-xor-sum/)

给定一个大小为 **N** 的数组**。任务是找到一个索引‘I’(1<= I<= n)，使得(a[1]^…^ a[I])+(a[I+1]^…^ a[n])(x^y 代表 x 和 y 的 [xor](https://www.geeksforgeeks.org/tag/xor/) 值)最大可能。
**举例:**** 

```
**Input :** arr[] = {1, 4, 6, 3, 8, 13, 34, 2, 21, 10}
**Output :** 2
**Explanation :** The maximum value is 68 at index 2

**Input :** arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9}
**Output :** 4
```

****天真的方法**:天真的方法是使用嵌套循环。遍历数组，找到数组的 xor，直到第 I 个索引，找到从索引 i+1 到的元素的 xor，并计算可能的最大和。
以下是上述办法的实施情况:** 

## **C++**

```
// CPP program to find partition point in
// array to maximize xor sum
#include <bits/stdc++.h>
using namespace std;

// Function to find partition point in
// array to maximize xor sum
int Xor_Sum(int arr[], int n)
{
    int sum = 0, index, left_xor = 0, right_xor = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++)
    {
        // Calculate xor of elements left of index i
        // including ith element
        left_xor = left_xor ^ arr[i];
        right_xor = 0;

        for (int j = i + 1; j < n; j++)
        {
            // Calculate xor of the elements right of
            // index i
            right_xor = right_xor ^ arr[j];
        }

        // Keep the maximum possible xor sum
        if (left_xor + right_xor > sum)
        {
            sum = left_xor + right_xor;
            index = i;
        }
    }

    // Return the 1 based index of the array
    return index+1;
}

// Driver code
int main()
{
    int arr[] = { 1, 4, 6, 3, 8, 13, 34, 2, 21, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << Xor_Sum(arr, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find partition point in
// array to maximize xor sum
class GFG
{

    // Function to find partition point in
    // array to maximize xor sum
    public static int Xor_Sum(int[] arr, int n)
    {
        int sum = 0, index = -1;
        int left_xor = 0, right_xor = 0;

        // Traverse through the array
        for (int i = 0; i < n; i++)
        {

            // Calculate xor of elements left of index i
            // including ith element
            left_xor = left_xor ^ arr[i];
            right_xor = 0;

            for (int j = i + 1; j < n; j++)
            {

                // Calculate xor of the elements right of
                // index i
                right_xor = right_xor ^ arr[j];
            }

            // Keep the maximum possible xor sum
            if (left_xor + right_xor > sum)
            {
                sum = left_xor + right_xor;
                index = i;
            }
        }

        // Return the 1 based index of the array
        return index + 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 1, 4, 6, 3, 8,
                      13, 34, 2, 21, 10 };
        int n = arr.length;

        // Function call
        System.out.println(Xor_Sum(arr, n));

    }
}

// This code is contributed by sanjeev2552
```

## **蟒蛇 3**

```
# Python3 program to find partition point in
# array to maximize xor sum

# Function to find partition point in
# array to maximize xor sum
def Xor_Sum(arr, n):

    sum = 0
    index, left_xor = 0, 0
    right_xor = 0

    # Traverse through the array
    for i in range(n):

        # Calculate xor of elements left of index i
        # including ith element
        left_xor = left_xor ^ arr[i]
        right_xor = 0

        for j in range(i + 1, n):

            # Calculate xor of the elements
            # right of index i
            right_xor = right_xor ^ arr[j]

        # Keep the maximum possible xor sum
        if (left_xor + right_xor > sum):
            sum = left_xor + right_xor
            index = i

    # Return the 1 based index of the array
    return index + 1

# Driver code
arr = [ 1, 4, 6, 3, 8,
        13, 34, 2, 21, 10]
n = len(arr)

# Function call
print(Xor_Sum(arr, n))

# This code is contributed by Mohit Kumar
```

## **C#**

```
// C# program to find partition point in
// array to maximize xor sum
using System;

class GFG
{

    // Function to find partition point in
    // array to maximize xor sum
    public static int Xor_Sum(int[] arr,
                              int n)
    {
        int sum = 0, index = -1;
        int left_xor = 0, right_xor = 0;

        // Traverse through the array
        for (int i = 0; i < n; i++)
        {

            // Calculate xor of elements left of index i
            // including ith element
            left_xor = left_xor ^ arr[i];
            right_xor = 0;

            for (int j = i + 1; j < n; j++)
            {

                // Calculate xor of the elements
                // right of index i
                right_xor = right_xor ^ arr[j];
            }

            // Keep the maximum possible xor sum
            if (left_xor + right_xor > sum)
            {
                sum = left_xor + right_xor;
                index = i;
            }
        }

        // Return the 1 based index of the array
        return index + 1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 1, 4, 6, 3, 8,
                      13, 34, 2, 21, 10 };
        int n = arr.Length;

        // Function call
        Console.WriteLine (Xor_Sum(arr, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>

// Javascript program to
// find partition point in
// array to maximize xor sum

// Function to find partition point in
// array to maximize xor sum
function Xor_Sum(arr, n)
{
    let sum = 0, index, left_xor = 0,
        right_xor = 0;

    // Traverse through the array
    for (let i = 0; i < n; i++)
    {
        // Calculate xor of elements
        // left of index i
        // including ith element
        left_xor = left_xor ^ arr[i];
        right_xor = 0;

        for (let j = i + 1; j < n; j++)
        {
            // Calculate xor of the
            // elements right of
            // index i
            right_xor = right_xor ^ arr[j];
        }

        // Keep the maximum possible xor sum
        if (left_xor + right_xor > sum)
        {
            sum = left_xor + right_xor;
            index = i;
        }
    }

    // Return the 1 based index of the array
    return index+1;
}

// Driver code
    let arr = [ 1, 4, 6, 3, 8, 13, 34, 2, 21, 10 ];
    let n = arr.length;

    // Function call
    document.write(Xor_Sum(arr, n));

</script>
```

****输出:****

```
 2 
```

****时间复杂度:** O( N^2)。
**高效方法**:一种高效的方法是使用前缀异或数组。在任何索引中,“I”前缀表示“我”给了我们“t5”arr[1]^ arr[1]^….^逮捕[i] 并让**逮捕[i+1] ^逮捕[i+2] ^。。^ arr[n-1]** ，找到**前缀【I】^前缀【n】**。
以下是上述方法的实施:** 

## **C++**

```
// CPP program to find partition point in
// array to maximize xor sum
#include <bits/stdc++.h>
using namespace std;

// Function to calculate Prefix Xor array
void ComputePrefixXor(int arr[], int PrefixXor[], int n)
{
    PrefixXor[0] = arr[0];

    // Calculating prefix xor
    for (int i = 1; i < n; i++)
        PrefixXor[i] = PrefixXor[i - 1] ^ arr[i];
}

// Function to find partition point in
// array to maximize xor sum
int Xor_Sum(int arr[], int n)
{
    // To store prefix xor
    int PrefixXor[n];

    // Compute the prefix xor
    ComputePrefixXor(arr, PrefixXor, n);

    // To store sum and index
    int sum = 0, index;

    // Calculate the maximum sum that can be obtained
    // splitting the array at some index i
    for (int i = 0; i < n; i++)
    {
        // PrefixXor[i] = Xor of all arr
        // elements till i'th index PrefixXor[n-1]
        //  ^ PrefixXor[i] = Xor of all elements
        // from i+1' th index to n-1'th index
        if (PrefixXor[i] + (PrefixXor[n - 1] ^
                PrefixXor[i]) > sum)
        {
            sum = PrefixXor[i] +
                 (PrefixXor[n - 1] ^ PrefixXor[i]);
            index = i;
        }
    }

    // Return the index
    return index+1;
}

// Driver code
int main()
{
    int arr[] = { 1, 4, 6, 3, 8, 13, 34, 2, 21, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << Xor_Sum(arr, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find partition point in
// array to maximize xor sum
import java.util.*;

class GFG
{

// Function to calculate Prefix Xor array
static void ComputePrefixXor(int arr[],
                             int PrefixXor[],
                             int n)
{
    PrefixXor[0] = arr[0];

    // Calculating prefix xor
    for (int i = 1; i < n; i++)
        PrefixXor[i] = PrefixXor[i - 1] ^ arr[i];
}

// Function to find partition point in
// array to maximize xor sum
static int Xor_Sum(int arr[], int n)
{
    // To store prefix xor
    int []PrefixXor = new int[n];

    // Compute the prefix xor
    ComputePrefixXor(arr, PrefixXor, n);

    // To store sum and index
    int sum = 0, index = 0;

    // Calculate the maximum sum that can be obtained
    // splitting the array at some index i
    for (int i = 0; i < n; i++)
    {
        // PrefixXor[i] = Xor of all arr
        // elements till i'th index PrefixXor[n-1]
        // ^ PrefixXor[i] = Xor of all elements
        // from i+1' th index to n-1'th index
        if (PrefixXor[i] + (PrefixXor[n - 1] ^
                PrefixXor[i]) > sum)
        {
            sum = PrefixXor[i] +
                (PrefixXor[n - 1] ^ PrefixXor[i]);
            index = i;
        }
    }

    // Return the index
    return index+1;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 4, 6, 3, 8,
                 13, 34, 2, 21, 10 };
    int n = arr.length;

    // Function call
    System.out.println(Xor_Sum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program to find partition point in
# array to maximize xor sum

# Function to calculate Prefix Xor array
def ComputePrefixXor(arr, PrefixXor, n):
    PrefixXor[0] = arr[0];

    # Calculating prefix xor
    for i in range(1, n):
        PrefixXor[i] = PrefixXor[i - 1] ^ arr[i];

# Function to find partition point in
# array to maximize xor sum
def Xor_Sum(arr, n):
    # To store prefix xor
    PrefixXor = [0] * n;

    # Compute the prefix xor
    ComputePrefixXor(arr, PrefixXor, n);

    # To store sum and index
    sum, index = 0, 0;

    # Calculate the maximum sum that can be obtained
    # splitting the array at some index i
    for i in range(n):

        # PrefixXor[i] = Xor of all arr
        # elements till i'th index PrefixXor[n-1]
        # ^ PrefixXor[i] = Xor of all elements
        # from i+1' th index to n-1'th index
        if (PrefixXor[i] + (PrefixXor[n - 1] ^
                            PrefixXor[i]) > sum):
            sum = PrefixXor[i] +\
                 (PrefixXor[n - 1] ^ PrefixXor[i]);
            index = i;

    # Return the index
    return index + 1;

# Driver code
arr = [ 1, 4, 6, 3, 8, 13, 34, 2, 21, 10 ];
n = len(arr);

# Function call
print(Xor_Sum(arr, n));

# This code is contributed by Rajput-Ji
```

## **C#**

```
// C# program to find partition point in
// array to maximize xor sum
using System;

class GFG
{

// Function to calculate Prefix Xor array
static void ComputePrefixXor(int[] arr,
                             int[] PrefixXor,
                              int n)
{
    PrefixXor[0] = arr[0];

    // Calculating prefix xor
    for (int i = 1; i < n; i++)
        PrefixXor[i] = PrefixXor[i - 1] ^ arr[i];
}

// Function to find partition point in
// array to maximize xor sum
static int Xor_Sum(int[] arr, int n)
{
    // To store prefix xor
    int []PrefixXor = new int[n];

    // Compute the prefix xor
    ComputePrefixXor(arr, PrefixXor, n);

    // To store sum and index
    int sum = 0, index = 0;

    // Calculate the maximum sum that can be obtained
    // splitting the array at some index i
    for (int i = 0; i < n; i++)
    {
        // PrefixXor[i] = Xor of all arr
        // elements till i'th index PrefixXor[n-1]
        // ^ PrefixXor[i] = Xor of all elements
        // from i+1' th index to n-1'th index
        if (PrefixXor[i] + (PrefixXor[n - 1] ^
                            PrefixXor[i]) > sum)
        {
            sum = PrefixXor[i] + (PrefixXor[n - 1] ^
                                  PrefixXor[i]);
            index = i;
        }
    }

    // Return the index
    return index + 1;
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 4, 6, 3, 8,
                13, 34, 2, 21, 10 };
    int n = arr.Length;

    // Function call
    Console.WriteLine(Xor_Sum(arr, n));
}
}

// This code is contributed by Code_Mech
```

## **java 描述语言**

```
<script>
// Javascript program to find partition point in
// array to maximize xor sum

// Function to calculate Prefix Xor array
function ComputePrefixXor(arr, PrefixXor, n)
{
    PrefixXor[0] = arr[0];

    // Calculating prefix xor
    for (let i = 1; i < n; i++)
        PrefixXor[i] = PrefixXor[i - 1] ^ arr[i];
}

// Function to find partition point in
// array to maximize xor sum
function Xor_Sum(arr, n)
{
    // To store prefix xor
    let PrefixXor = new Array(n);

    // Compute the prefix xor
    ComputePrefixXor(arr, PrefixXor, n);

    // To store sum and index
    let sum = 0, index;

    // Calculate the maximum sum that can be obtained
    // splitting the array at some index i
    for (let i = 0; i < n; i++)
    {
        // PrefixXor[i] = Xor of all arr
        // elements till i'th index PrefixXor[n-1]
        //  ^ PrefixXor[i] = Xor of all elements
        // from i+1' th index to n-1'th index
        if (PrefixXor[i] + (PrefixXor[n - 1] ^
                PrefixXor[i]) > sum)
        {
            sum = PrefixXor[i] +
                 (PrefixXor[n - 1] ^ PrefixXor[i]);
            index = i;
        }
    }

    // Return the index
    return index+1;
}

// Driver code
    let arr = [ 1, 4, 6, 3, 8, 13, 34, 2, 21, 10 ];
    let n = arr.length;

    // Function call
    document.write(Xor_Sum(arr, n));

</script>
```

****输出:****

```
 2 
```