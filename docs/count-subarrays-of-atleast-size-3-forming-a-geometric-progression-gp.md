# 计算至少大小为 3 的子阵列，形成几何级数

> 原文:[https://www . geesforgeks . org/count-至少大小为 3 的子阵列-形成几何级数-gp/](https://www.geeksforgeeks.org/count-subarrays-of-atleast-size-3-forming-a-geometric-progression-gp/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是从给定的至少大小为 **3** 的数组中找出所有子数组的计数，形成一个[几何级数](https://www.geeksforgeeks.org/geometric-progression/)。

**示例:**

> **输入:** arr[] = {1，2，4，8}
> **输出:** 3
> **说明:**形成几何级数所需的子阵有:
> 
> 1.  {1, 2, 4}
> 2.  {2, 4, 8}
> 3.  {1, 2, 4, 8}
> 
> **输入:** arr[] = {1，2，4，8，16，24}
> **输出:** 6
> **说明:**形成几何级数所需的子阵有:
> 
> 1.  {1, 2, 4}
> 2.  {2, 4, 8}
> 3.  {4, 8, 16}
> 4.  {1, 2, 4, 8}
> 5.  {2, 4, 8, 16}
> 6.  {1, 2, 4, 8, 16}

**天真方法:**最简单的方法是[生成所有大小至少为 3 的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并对所有这些子阵列进行计数，形成一个[几何级数](https://www.geeksforgeeks.org/geometric-progression/)。检查所有子阵列后打印计数。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**有效方法:**思路是利用[几何级数](https://www.geeksforgeeks.org/geometric-progression/)的一个性质，即 **{a，b，c}** 为 [GP](https://www.geeksforgeeks.org/geometric-progression/) 当且仅当 **a*c = b** 。按照以下步骤解决问题:

*   初始化一个变量， **res** ，**用 **0** 计数**，以存储形成当前子阵列几何级数和长度的总子阵列。
*   [在范围**【2，N–1】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果当前元素形成几何级数，即**arr[I]* arr[I–2]= arr[I–1]* arr[I–1]**，则增加**计数的值**否则，将**计数**设置为零。
*   对于上述步骤中的每次迭代，将**计数**加到 **res** 上。
*   完成上述步骤后，打印 **res** 的值作为结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count all the subarrays
// of size at least 3 forming GP
int numberOfGP(int L[], int N)
{
    // If array size is less than 3
    if (N <= 2)
        return 0;

    // Stores the count of subarray
    int count = 0;

    // Stores the count of subarray
    // for each iteration
    int res = 0;

    // Traverse the array
    for (int i = 2; i < N; ++i) {

        // Check if L[i] forms GP
        if (L[i - 1] * L[i - 1]
            == L[i] * L[i - 2]) {
            ++count;
        }

        // Otherwise, update count to 0
        else {
            count = 0;
        }

        // Update the final count
        res += count;
    }

    // Return the final count
    return res;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 4, 8, 16, 24 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << numberOfGP(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to count all
// the subarrays of size
// at least 3 forming GP
static int numberOfGP(int L[],
                      int N)
{
  // If array size
  // is less than 3
  if (N <= 2)
    return 0;

  // Stores the count
  // of subarray
  int count = 0;

  // Stores the count
  // of subarray for
  // each iteration
  int res = 0;

  // Traverse the array
  for (int i = 2; i < N; ++i)
  {
    // Check if L[i] forms GP
    if (L[i - 1] * L[i - 1] ==
        L[i] * L[i - 2])
    {
      ++count;
    }

    // Otherwise, update
    // count to 0
    else
    {
      count = 0;
    }

    // Update the
    // final count
    res += count;
  }

  // Return the final count
  return res;
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {1, 2, 4,
               8, 16, 24};

  int N = arr.length;

  // Function Call
  System.out.print(numberOfGP(arr, N));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count all the subarrays
# of size at least 3 forming GP
def numberOfGP(L, N):

    # If array size is less than 3
    if (N <= 2):
        return 0

    # Stores the count of subarray
    count = 0

    # Stores the count of subarray
    # for each iteration
    res = 0

    # Traverse the array
    for i in range(2, N):

        # Check if L[i] forms GP
        if (L[i - 1] * L[i - 1] ==
                L[i] * L[i - 2]):
            count += 1

        # Otherwise, update count to 0
        else:
            count = 0

        # Update the final count
        res += count

    # Return the final count
    return res

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 4, 8, 16, 24 ]

    N = len(arr)

    # Function Call
    print(numberOfGP(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
class GFG {

// Function to count all
// the subarrays of size
// at least 3 forming GP
static int numberOfGP(int[] L,
                      int N)
{
  // If array size
  // is less than 3
  if (N <= 2)
    return 0;

  // Stores the count
  // of subarray
  int count = 0;

  // Stores the count
  // of subarray for
  // each iteration
  int res = 0;

  // Traverse the array
  for (int i = 2; i < N; ++i)
  {
    // Check if L[i] forms GP
    if (L[i - 1] * L[i - 1] ==
        L[i] * L[i - 2])
    {
      ++count;
    }

    // Otherwise, update
    // count to 0
    else
    {
      count = 0;
    }

    // Update the
    // final count
    res += count;
  }

  // Return the final
  // count
  return res;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array arr[]
  int[] arr = {1, 2, 4, 8, 16, 24};

  int N = arr.Length;

  // Function Call
  Console.Write(numberOfGP(arr, N));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count all the subarrays
// of size at least 3 forming GP
function numberOfGP(L, N)
{
    // If array size is less than 3
    if (N <= 2)
        return 0;

    // Stores the count of subarray
    let count = 0;

    // Stores the count of subarray
    // for each iteration
    let res = 0;

    // Traverse the array
    for (let i = 2; i < N; ++i) {

        // Check if L[i] forms GP
        if (L[i - 1] * L[i - 1]
            == L[i] * L[i - 2]) {
            ++count;
        }

        // Otherwise, update count to 0
        else {
            count = 0;
        }

        // Update the final count
        res += count;
    }

    // Return the final count
    return res;
}

// Driver Code

    // Given array arr[]
    let arr = [ 1, 2, 4, 8, 16, 24];

    let N = arr.length;

    // Function Call
    document.write(numberOfGP(arr, N));

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)