# 计数具有偶数位异或的子阵列

> 原文:[https://www . geesforgeks . org/count-subarrays-having-bitwise-xor/](https://www.geeksforgeeks.org/count-subarrays-having-even-bitwise-xor/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算给定阵列中[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为偶数的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 4
> **解释:** *具有偶数位异或的子阵列为{* {2}、{4}、{1，2，3}、{1，2，3，4}}。
> 
> **输入:** arr[] = {2，4，6}
> **输出:** 6
> **解释:** *具有偶数按位异或的子阵列为{* {2}、{4}、{6}、{2，4}、{4，6}、{2，4，6}}。

**天真方法:**解决这个问题最简单的方法是[生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/) s，[检查每个子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，其所有元素的**按位异或**是否为偶数。如果发现是偶数，则增加计数。最后，打印计数作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// subarrays having even Bitwise XOR
void evenXorSubarray(int arr[], int n)
{
    // Store the required result
    int ans = 0;

    // Generate subarrays with
    // arr[i] as the first element
    for (int i = 0; i < n; i++) {

        // Store XOR of current subarray
        int XOR = 0;

        // Generate subarrays with
        // arr[j] as the last element
        for (int j = i; j < n; j++) {

            // Calculate Bitwise XOR
            // of the current subarray
            XOR = XOR ^ arr[j];

            // If XOR is even,
            // increase ans by 1
            if ((XOR & 1) == 0)
                ans++;
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Stores the size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    evenXorSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to count the number of
  // subarrays having even Bitwise XOR
  static void evenXorSubarray(int arr[], int n)
  {

    // Store the required result
    int ans = 0;

    // Generate subarrays with
    // arr[i] as the first element
    for (int i = 0; i < n; i++) {

      // Store XOR of current subarray
      int XOR = 0;

      // Generate subarrays with
      // arr[j] as the last element
      for (int j = i; j < n; j++) {

        // Calculate Bitwise XOR
        // of the current subarray
        XOR = XOR ^ arr[j];

        // If XOR is even,
        // increase ans by 1
        if ((XOR & 1) == 0)
          ans++;
      }
    }

    // Print the result
    System.out.println(ans);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Stores the size of the array
    int N = arr.length;
    evenXorSubarray(arr, N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# subarrays having even Bitwise XOR
def evenXorSubarray(arr, n):

    # Store the required result
    ans = 0

    # Generate subarrays with
    # arr[i] as the first element
    for i in range(n):

        # Store XOR of current subarray
        XOR = 0

        # Generate subarrays with
        # arr[j] as the last element
        for j in range(i, n):

            # Calculate Bitwise XOR
            # of the current subarray
            XOR = XOR ^ arr[j]

            # If XOR is even,
            # increase ans by 1
            if ((XOR & 1) == 0):
                ans += 1

    # Prthe result
    print (ans)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, 2, 3, 4]

    # Stores the size of the array
    N = len(arr)

    # Function Call
    evenXorSubarray(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
  // Function to count the number of
  // subarrays having even Bitwise XOR
  static void evenXorSubarray(int[] arr, int n)
  {

    // Store the required result
    int ans = 0;

    // Generate subarrays with
    // arr[i] as the first element
    for (int i = 0; i < n; i++) {

      // Store XOR of current subarray
      int XOR = 0;

      // Generate subarrays with
      // arr[j] as the last element
      for (int j = i; j < n; j++) {

        // Calculate Bitwise XOR
        // of the current subarray
        XOR = XOR ^ arr[j];

        // If XOR is even,
        // increase ans by 1
        if ((XOR & 1) == 0)
          ans++;
      }
    }

    // Print the result
    Console.WriteLine(ans);
  }

  // Driver Code
  public static void Main()
  {
    // Given array
    int[] arr = { 1, 2, 3, 4 };

    // Stores the size of the array
    int N = arr.Length;
    evenXorSubarray(arr, N);
  }
}

// This code is contributed by souravghosh0416.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of
// subarrays having even Bitwise XOR
function evenXorSubarray(arr, n)
{
    // Store the required result
    let ans = 0;

    // Generate subarrays with
    // arr[i] as the first element
    for (let i = 0; i < n; i++) {

        // Store XOR of current subarray
        let XOR = 0;

        // Generate subarrays with
        // arr[j] as the last element
        for (let j = i; j < n; j++) {

            // Calculate Bitwise XOR
            // of the current subarray
            XOR = XOR ^ arr[j];

            // If XOR is even,
            // increase ans by 1
            if ((XOR & 1) == 0)
                ans++;
        }
    }

    // Print the result
    document.write(ans);
}

// Driver Code
// Given array
let arr = [ 1, 2, 3, 4 ];

// Stores the size of the array
let N = arr.length;

// Function Call
evenXorSubarray(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 索引范围内所有元素的按位异或**【I+1，j】**为 **A.**
> 索引范围内所有元素的按位异或**【0，I】**为 **B.**
> 索引范围内所有元素的按位异或**【0，j】**为 **C** 。
> 通过执行 **B ^ C** ，来自两个范围的公共元素抵消，导致来自范围**【I+1，j】**的所有元素异或。

因此，想法是从索引 **0 开始更新子阵列的数量，在[遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)的同时**具有偶数和奇数异或值，并相应地更新计数。按照以下步骤解决问题:

*   初始化两个变量，说 **ans** 和 **XOR，**分别存储所需的子阵列个数和存储子阵列的 XOR 值。
*   初始化一个数组，比如说大小为 2 的 **freq[]** ，其中 **freq[0]** 表示具有偶数异或值的子数组的数量， **freq[1]** 表示具有奇数异或值的子数组的数量，从索引 0 开始。
*   [使用变量遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，比如 **i** ，对于每个数组元素:
    *   将 **XOR** 的值更新为**xor ^ arr【I】**。
    *   [如果**异或**为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将 **ans** 的值增加**1+freq【0】**。
    *   将 **freq[0]** 增加 **1，**，因为当子阵列{arr[0]，i]与具有偶数异或值的其他子阵列异或时，将产生偶数异或值。此外，添加 1 以考虑整个子阵列[0，i]。
    *   类似地，[如果**异或**为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将 **ans** 增加**freq【1】**并将**freq【1】**增加 1。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count subarrays
// having even Bitwise XOR
void evenXorSubarray(int arr[], int n)
{
    // Store the required result
    int ans = 0;

    // Stores count of subarrays
    // with even and odd XOR values
    int freq[] = { 0, 0 };

    // Stores Bitwise XOR of
    // current subarray
    int XOR = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Update current Xor
        XOR = XOR ^ arr[i];

        // If XOR is even
        if (XOR % 2 == 0) {

            // Update ans
            ans += freq[0] + 1;

            // Increment count of
            // subarrays with even XOR
            freq[0]++;
        }
        else {

            // Otherwise, increment count
            // of subarrays with odd XOR
            ans += freq[1];
            freq[1]++;
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 3, 4 };

    // Stores the size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    evenXorSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to count subarrays
    // having even Bitwise XOR
    static void evenXorSubarray(int arr[], int n)
    {
        // Store the required result
        int ans = 0;

        // Stores count of subarrays
        // with even and odd XOR values
        int freq[] = { 0, 0 };

        // Stores Bitwise XOR of
        // current subarray
        int XOR = 0;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // Update current Xor
            XOR = XOR ^ arr[i];

            // If XOR is even
            if (XOR % 2 == 0) {

                // Update ans
                ans += freq[0] + 1;

                // Increment count of
                // subarrays with even XOR
                freq[0]++;
            }
            else {

                // Otherwise, increment count
                // of subarrays with odd XOR
                ans += freq[1];
                freq[1]++;
            }
        }

        // Print the result
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array
        int arr[] = { 1, 2, 3, 4 };

        // Stores the size of the array
        int N = arr.length;

        evenXorSubarray(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count subarrays
# having even Bitwise XOR
def evenXorSubarray(arr, n):

    # Store the required result
    ans = 0

    # Stores count of subarrays
    # with even and odd XOR values
    freq = [0] * n

    # Stores Bitwise XOR of
    # current subarray
    XOR = 0

    # Traverse the array
    for i in range(n):

        # Update current Xor
        XOR = XOR ^ arr[i]

        # If XOR is even
        if (XOR % 2 == 0):

            # Update ans
            ans += freq[0] + 1

            # Increment count of
            # subarrays with even XOR
            freq[0] += 1

        else:

            # Otherwise, increment count
            # of subarrays with odd XOR
            ans += freq[1]
            freq[1] += 1

    # Print the result
    print(ans)

# Driver Code

# Given array
arr = [ 1, 2, 3, 4 ]

# Stores the size of the array
N = len(arr)

evenXorSubarray(arr, N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
  // Function to count subarrays
  // having even Bitwise XOR
  static void evenXorSubarray(int[] arr, int n)
  {

    // Store the required result
    int ans = 0;

    // Stores count of subarrays
    // with even and odd XOR values
    int[] freq = { 0, 0 };

    // Stores Bitwise XOR of
    // current subarray
    int XOR = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

      // Update current Xor
      XOR = XOR ^ arr[i];

      // If XOR is even
      if (XOR % 2 == 0) {

        // Update ans
        ans += freq[0] + 1;

        // Increment count of
        // subarrays with even XOR
        freq[0]++;
      }
      else {

        // Otherwise, increment count
        // of subarrays with odd XOR
        ans += freq[1];
        freq[1]++;
      }
    }

    // Print the result
    Console.WriteLine(ans);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    // Given array
    int[] arr = { 1, 2, 3, 4 };

    // Stores the size of the array
    int N = arr.Length;

    evenXorSubarray(arr, N);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count subarrays
// having even Bitwise XOR
function evenXorSubarray(arr, n)
{
    // Store the required result
    let ans = 0;

    // Stores count of subarrays
    // with even and odd XOR values
    let freq = [ 0, 0 ];

    // Stores Bitwise XOR of
    // current subarray
    let XOR = 0;

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // Update current Xor
        XOR = XOR ^ arr[i];

        // If XOR is even
        if (XOR % 2 == 0) {

            // Update ans
            ans += freq[0] + 1;

            // Increment count of
            // subarrays with even XOR
            freq[0]++;
        }
        else {

            // Otherwise, increment count
            // of subarrays with odd XOR
            ans += freq[1];
            freq[1]++;
        }
    }

    // Print the result
    document.write(ans);
}

// Driver Code
    // Given array
    let arr = [ 1, 2, 3, 4 ];

    // Stores the size of the array
    let N = arr.length;

    evenXorSubarray(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)