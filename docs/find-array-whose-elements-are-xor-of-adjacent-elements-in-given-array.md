# 查找给定数组中相邻元素异或的数组

> 原文:[https://www . geeksforgeeks . org/find-array-其元素是给定数组中相邻元素的异或/](https://www.geeksforgeeks.org/find-array-whose-elements-are-xor-of-adjacent-elements-in-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是重新构造一个数组 **arr[]** ，使得 **arr[]** 中的值通过对数组中的相邻元素进行异或运算而获得。打印数组元素。

**示例:**

> **输入:** arr[ ] = {10，11，1，2，3}
> **输出:** 1 10 3 1 3
> **解释:**
> 在索引 0 处，arr[0]异或 arr[1] = 1
> 在索引 1 处，arr[1]异或 arr[2] = 10
> 在索引 2 处，arr[2]异或 arr[3] = 3
> …
> 在索引 4 处，没有元素留下，所以
> 新阵列将是{1，10，3，1，3}
> 
> **输入:** arr[ ] = {5，9，7，6}
> **输出:** 12 14 1 6
> **解释:**
> 在索引 0 处，arr[0] xor arr[1] = 12
> 在索引 1 处，arr[1] xor arr[2] = 14
> 在索引 2 处，arr[2] xor arr[3] = 1
> 在索引 3 处，没有元素留下，因此它将保持原样。
> 新阵列将是{12，14，1，6}

**方法:**解决给定问题的主要思路是执行以下步骤:

1.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 从第 0 个<sup>索引到第(N–2)个索引。</sup>
2.  对于位置 I 处每个元素 arr[i],计算 **arr[i] ^ arr[i+1]** ,并将其存储在位置 I 处

下面是上述方法的实现:

## C++

```
// C++ implementation
// of the above approach
#include <iostream>
using namespace std;

// Function to reconstruct the array
// arr[] with xor of adjacent elements
int* game_with_number(int arr[], int n)
{
    // Iterate through each element
    for (int i = 0; i < n - 1; i++) {
        // Store the xor of current
        // and next element in arr[i]
        arr[i] = arr[i] ^ arr[i + 1];
    }

    return arr;
}

// Function to print the array
void print(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    // Inputs
    int arr[] = { 10, 11, 1, 2, 3 };

    // Length of the array given
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to reconstruct the arr[]
    int* new_arr = game_with_number(arr, n);

    // Function call to print arr[]
    print(new_arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of the above approach
import java.io.*;

class GFG{

// Function to reconstruct the array
// arr[] with xor of adjacent elements
static int[] game_with_number(int arr[], int n)
{

    // Iterate through each element
    for(int i = 0; i < n - 1; i++)
    {

        // Store the xor of current
        // and next element in arr[i]
        arr[i] = arr[i] ^ arr[i + 1];
    }
    return arr;
}

// Function to print the array
static void print(int arr[], int n)
{
    for(int i = 0; i < n; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Inputs
    int arr[] = { 10, 11, 1, 2, 3 };

    // Length of the array given
    int n = arr.length;

    // Function call to reconstruct the arr[]
    int[] new_arr = game_with_number(arr, n);

    // Function call to print arr[]
    print(new_arr, n);
}
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python3 implementation
# of the above approach

# Function to reconstruct the array
# arr[] with xor of adjacent elements
def game_with_number(arr, n):
    # Iterate through each element
    for i in range(n-1):

        # Store the xor of current
        #and next element in arr[i]
        arr[i] = arr[i] ^ arr[i + 1]

    return arr

# Function to print array
def printt(arr, n):
    print(*arr)

# Driver Code
if __name__ == '__main__':
    # Inputs
    arr= [10, 11, 1, 2, 3]

    # Length of the array given
    n = len(arr)

    # Function call to reconstruct the arr[]
    new_arr = game_with_number(arr, n);

    # Function call to prarr[]
    printt(new_arr, n)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to reconstruct the array
// arr[] with xor of adjacent elements
static int[] game_with_number(int[] arr, int n)
{

    // Iterate through each element
    for(int i = 0; i < n - 1; i++)
    {

        // Store the xor of current
        // and next element in arr[i]
        arr[i] = arr[i] ^ arr[i + 1];
    }
    return arr;
}

// Function to print the array
static void print(int[] arr, int n)
{
    for(int i = 0; i < n; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver Code
public static void Main()
{
    // Inputs
    int[] arr = { 10, 11, 1, 2, 3 };

    // Length of the array given
    int n = arr.Length;

    // Function call to reconstruct the arr[]
    int[] new_arr = game_with_number(arr, n);

    // Function call to print arr[]
    print(new_arr, n);
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
    <script>
    // Javascript program for the above approach

// Function to reconstruct the array
// arr[] with xor of adjacent elements
function game_with_number(arr,n)
{
    // Iterate through each element
    for (let i = 0; i < n - 1; i++)
    {

        // Store the xor of current
        // and next element in arr[i]
        arr[i] = arr[i] ^ arr[i + 1];
    }

    return arr;
}

// Function to print the array
function print(arr,n)
{
    for (let i = 0; i < n; i++) {
        document.write(arr[i]+" ");
    }
}

// Driver Code

    //Inputs
    let arr = [10, 11, 1, 2, 3 ];

    // Length of the array given
    let n = arr.length;

    // Function call to reconstruct the arr[]
    let new_arr = game_with_number(arr, n);

    // Function call to print arr[]
    print(new_arr, n);

// This code is contributed by
// Potta Lokesh

    </script>
```

**Output**

```
1 10 3 1 3 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)