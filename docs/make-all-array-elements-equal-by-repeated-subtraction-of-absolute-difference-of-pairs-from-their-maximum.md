# 通过从最大值开始重复减去对的绝对差，使所有数组元素相等

> 原文:[https://www . geesforgeks . org/make-all-array-elements-通过重复从它们的最大值减去对的绝对差来实现相等/](https://www.geeksforgeeks.org/make-all-array-elements-equal-by-repeated-subtraction-of-absolute-difference-of-pairs-from-their-maximum/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr 【】,任务是通过从数组中选择任意一对整数并用它们的绝对差替换该对整数中的较大整数任意多次来使所有数组元素相等。打印所有数组元素的最终值。**

**示例:**

> **输入:** arr[] ={2，3，4}
> **输出:** 1
> **解释:**
> 步骤 1:对配对(2，3)执行修改 arr[] ={2，1，4}
> 步骤 2:对配对(2，4)执行修改 arr[] = {2，1，2}
> 步骤 3:对配对(2，1)执行修改{1，1，2}
> 步骤 4:对
> 
> **输入:** arr[] = {24，60 }
> T3】输出: 12

**逼近:**从上面的问题表述可以观察到，对于任意一对 **(a，b)** ，从最大元素中减去绝对差。那么这个操作类似于找到配对的 [GCD。因此，从这个观察，很明显，所有的数组元素都需要减少到数组的](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。按照以下步骤解决问题:

*   将变量 **gcd** 初始化为 **1** 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并在遍历时更新 **gcd** 如下:

> **gcd = gcd(arr[i]，gcd)** ，其中 **0 ≤ i < N**

*   在上述步骤之后， **gcd** 的值是给定操作应用于每对不同的元素之后所需的数组元素。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return
// gcd of a and b
int gcd(int a, int b)
{
  // Base Case
  if (a == 0)
    return b;

  // Recursive Call
  return gcd(b % a, a);
}

// Function to find gcd of array
int findGCD(int arr[], int N)
{
  // Initialise the result
  int result = 0;

  // Traverse the array arr[]
  for (int i = 0; i < N; i++)
  {
    // Update result as gcd of
    // the result and arr[i]
    result = gcd(result, arr[i]);

    if (result == 1)
    {
      return 1;
    }
  }

  // Return the resultant GCD
    return result;
}

// Driver Code
int main()
{
  // Given array arr[]
  int arr[] = {2, 3, 4};

  int N = sizeof(arr) /
          sizeof(arr[0]);

  // Function Call
  cout << findGCD(arr, N);
  return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GCD {

    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        // Base Case
        if (a == 0)
            return b;

        // Recursive Call
        return gcd(b % a, a);
    }

    // Function to find gcd of array
    static int findGCD(int arr[], int N)
    {
        // Initialise the result
        int result = 0;

        // Traverse the array arr[]
        for (int element : arr) {

            // Update result as gcd of
            // the result and arr[i]
            result = gcd(result, element);

            if (result == 1) {
                return 1;
            }
        }

        // Return the resultant GCD
        return result;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int arr[] = { 2, 3, 4 };

        int N = arr.length;

        // Function Call
        System.out.println(findGCD(arr, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return gcd of a and b
def gcd(a, b):

    # Base Case
    if (a == 0):
        return b

    # Recursive call
    return gcd(b % a, a)

# Function to find gcd of array
def findGCD(arr, N):

    # Initialise the result
    result = 0

    # Traverse the array arr[]
    for element in arr:

        # Update result as gcd of
        # the result and arr[i]
        result = gcd(result, element)

        if (result == 1):
            return 1

    # Return the resultant GCD
    return result

# Driver Code

# Given array arr[]
arr = [ 2, 3, 4 ]

N = len(arr)

# Function call
print(findGCD(arr, N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return gcd of a and b
static int gcd(int a, int b)
{

    // Base Case
    if (a == 0)
        return b;

    // Recursive call
    return gcd(b % a, a);
}

// Function to find gcd of array
static int findGCD(int[] arr, int N)
{

    // Initialise the result
    int result = 0;

    // Traverse the array arr[]
    foreach(int element in arr)
    {

        // Update result as gcd of
        // the result and arr[i]
        result = gcd(result, element);

        if (result == 1)
        {
            return 1;
        }
    }

    // Return the resultant GCD
    return result;
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 2, 3, 4 };

    int N = arr.Length;

    // Function call
    Console.WriteLine(findGCD(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

    // Function to return gcd of a and b
    function gcd(a, b)
    {
        // Base Case
        if (a == 0)
            return b;

        // Recursive Call
        return gcd(b % a, a);
    }

    // Function to find gcd of array
    function findGCD(arr, N)
    {
        // Initialise the result
        let result = 0;

        // Traverse the array arr[]
        for (let element in arr) {

            // Update result as gcd of
            // the result and arr[i]
            result = gcd(result, element);

            if (result == 1) {
                return 1;
            }
        }

        // Return the resultant GCD
        return result;
    }

// Driver code

          // Given array arr[]
        let arr = [ 2, 3, 4 ];

        let N = arr.length;

        // Function Call
        document.write(findGCD(arr, N));

</script>
```

**Output**

```
1
```

***时间复杂度:** O(N*logN)，其中 N 是给定数组的大小。*
***辅助空间:** O(N)*