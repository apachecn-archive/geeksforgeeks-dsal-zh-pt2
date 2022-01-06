# 计算将数组拆分为三个非空子数组的方法，这些子数组具有相等的按位异或值

> 原文:[https://www . geeksforgeeks . org/count-way-to-split-array-in-three-non-empty-subarray-with-equal-bitwise-xor-values/](https://www.geeksforgeeks.org/count-ways-to-split-array-into-three-non-empty-subarrays-having-equal-bitwise-xor-values/)

给定一个由非负整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是计算将该数组拆分为三个不同的非空[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的方法数，使得每个子数组的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)相等。

**示例:**

> **输入:** arr[] = {7，0，5，2，7}
> **输出:** 2
> **解释:**所有可能的方式为:
> {{7}、{0，5，2}、{7}}其中每个子阵列的 XOR 值为 7
> {{7，0}、{5，2}、{7}}其中每个子阵列的 XOR 值为 7
> 
> **输入:** arr[] = {3，1，4 }
> T3】输出: 0

**天真方法:**最简单的方法是使用[三环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)将阵列分割成三个非空子阵列，并检查每个子阵列的[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)是否相等。如果给定条件成立，则增加最终计数。打印获得的最终计数。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   让 **xor_arr** 成为数组所有元素的 XOR**arr[]**。
*   如果 **arr[]** 可以分成三个不同的异或值相等的子阵列，那么每个子阵列中所有元素的异或将等于 **xor_arr** 。
*   所以，想法是找到所有前缀和后缀数组，其中**异或**值等于**异或 _arr** 。
*   如果这样的前缀和后缀数组的总长度**小于 N，**，则它们之间存在另一个异或值等于 **xor_arr** 的子数组。

因此，计算满足上述条件的所有前缀和后缀数组的总数。按照以下步骤解决给定的问题:

*   将数组所有元素、 **arr[]** 的[异或存储在变量 **xor_arr** 中。](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)
*   创建一个[数组](https://www.geeksforgeeks.org/array-data-structure/)， **pref_ind[]** 来存储每个异或值等于 **xor_arr** 的前缀数组的结束点。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，在 **pref_ind** 中插入 XOR 值等于 **xor_arr** 的每个前缀数组的结束点。
*   创建另一个大小为 **N** 的数组 **suff_inds[]** ，其中 **suff_inds[i]** 存储异或值等于 **xor_arr** 的后缀数组总数，其起始点大于或等于 **i** 。
*   [按相反顺序遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，填充 **suff_inds[]** 数组。如果当前后缀数组异或值等于 **xor_arr** ，则将 **suff_inds[i]** 增加 **1** 。另外，将 **suff_inds[i+1]** 的值加到 **suff_inds[i]** 上。
*   对于 **pref_ind** 中的每个元素 **idx** 如果 **idx < N-1** 的值，那么将**suffinds【idx+2】**的值加到最终计数中。
*   最后，打印最终计数的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count ways to split array
// into three subarrays with equal Bitwise XOR
int countWays(int arr[], int N)
{
    // Stores the XOR value of arr[]
    int arr_xor = 0;

    // Update the value of arr_xor
    for (int i = 0; i < N; i++)
        arr_xor ^= arr[i];

    // Stores the XOR value of prefix
    // and suffix array respectively
    int pref_xor = 0, suff_xor = 0;

    // Stores the ending points of all
    // the required prefix arrays
    vector<int> pref_ind;

    // Stores the count of suffix arrays
    // whose XOR value is equal to the
    // total XOR value at each index
    int suff_inds[N + 1];
    memset(suff_inds, 0, sizeof suff_inds);

    // Find all prefix arrays with
    // XOR value equal to arr_xor
    for (int i = 0; i < N; i++) {

        // Update pref_xor
        pref_xor ^= arr[i];

        if (pref_xor == arr_xor)
            pref_ind.push_back(i);
    }

    // Fill the values of suff_inds[]
    for (int i = N - 1; i >= 0; i--) {

        // Update suff_xor
        suff_xor ^= arr[i];

        // Update suff_inds[i]
        suff_inds[i] += suff_inds[i + 1];

        if (suff_xor == arr_xor)
            suff_inds[i]++;
    }

    // Stores the total number of ways
    int tot_ways = 0;

    // Count total number of ways
    for (int idx : pref_ind) {
        if (idx < N - 1)
            tot_ways += suff_inds[idx + 2];
    }

    // Return the final count
    return tot_ways;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 7, 0, 5, 2, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countWays(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG
{

  // Function to count ways to split array
  // into three subarrays with equal Bitwise XOR
  static int countWays(int arr[], int N)
  {

    // Stores the XOR value of arr[]
    int arr_xor = 0;

    // Update the value of arr_xor
    for (int i = 0; i < N; i++)
      arr_xor ^= arr[i];

    // Stores the XOR value of prefix
    // and suffix array respectively
    int pref_xor = 0, suff_xor = 0;

    // Stores the ending points of all
    // the required prefix arrays
    ArrayList<Integer> pref_ind=new ArrayList<>();

    // Stores the count of suffix arrays
    // whose XOR value is equal to the
    // total XOR value at each index
    int[] suff_inds= new int[N + 1];

    // Find all prefix arrays with
    // XOR value equal to arr_xor
    for (int i = 0; i < N; i++) {

      // Update pref_xor
      pref_xor ^= arr[i];

      if (pref_xor == arr_xor)
        pref_ind.add(i);
    }

    // Fill the values of suff_inds[]
    for (int i = N - 1; i >= 0; i--) {

      // Update suff_xor
      suff_xor ^= arr[i];

      // Update suff_inds[i]
      suff_inds[i] += suff_inds[i + 1];

      if (suff_xor == arr_xor)
        suff_inds[i]++;
    }

    // Stores the total number of ways
    int tot_ways = 0;

    // Count total number of ways
    for (Integer idx : pref_ind) {
      if (idx < N - 1)
        tot_ways += suff_inds[idx + 2];
    }

    // Return the final count
    return tot_ways;
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given Input
    int arr[] = { 7, 0, 5, 2, 7 };
    int N = arr.length;

    // Function Call
    System.out.println(countWays(arr, N));

  }

}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count ways to split array
# into three subarrays with equal Bitwise XOR
def countWays(arr, N):

    # Stores the XOR value of arr[]
    arr_xor = 0

    # Update the value of arr_xor
    for i in range(N):
        arr_xor ^= arr[i]

    # Stores the XOR value of prefix
    # and suffix array respectively
    pref_xor, suff_xor = 0, 0

    # Stores the ending points of all
    # the required prefix arrays
    pref_ind = []

    # Stores the count of suffix arrays
    # whose XOR value is equal to the
    # total XOR value at each index
    suff_inds = [0] * (N + 1)
    # memset(suff_inds, 0, sizeof suff_inds)

    # Find all prefix arrays with
    # XOR value equal to arr_xor
    for i in range(N):

        # Update pref_xor
        pref_xor ^= arr[i]

        if (pref_xor == arr_xor):
            pref_ind.append(i)

    # Fill the values of suff_inds[]
    for i in range(N - 1, -1, -1):

        # Update suff_xor
        suff_xor ^= arr[i]

        # Update suff_inds[i]
        suff_inds[i] += suff_inds[i + 1]

        if (suff_xor == arr_xor):
            suff_inds[i] += 1

    # Stores the total number of ways
    tot_ways = 0

    # Count total number of ways
    for idx in pref_ind:
        if (idx < N - 1):
            tot_ways += suff_inds[idx + 2]

    # Return the final count
    return tot_ways

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 7, 0, 5, 2, 7 ]
    N = len(arr)

    # Function Call
    print (countWays(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to count ways to split array
    // into three subarrays with equal Bitwise XOR
    static int countWays(int[] arr, int N)
    {

        // Stores the XOR value of arr[]
        int arr_xor = 0;

        // Update the value of arr_xor
        for (int i = 0; i < N; i++)
            arr_xor ^= arr[i];

        // Stores the XOR value of prefix
        // and suffix array respectively
        int pref_xor = 0, suff_xor = 0;

        // Stores the ending points of all
        // the required prefix arrays
        List<int> pref_ind = new List<int>();

        // Stores the count of suffix arrays
        // whose XOR value is equal to the
        // total XOR value at each index
        int[] suff_inds = new int[N + 1];

        // Find all prefix arrays with
        // XOR value equal to arr_xor
        for (int i = 0; i < N; i++) {

            // Update pref_xor
            pref_xor ^= arr[i];

            if (pref_xor == arr_xor)
                pref_ind.Add(i);
        }

        // Fill the values of suff_inds[]
        for (int i = N - 1; i >= 0; i--) {

            // Update suff_xor
            suff_xor ^= arr[i];

            // Update suff_inds[i]
            suff_inds[i] += suff_inds[i + 1];

            if (suff_xor == arr_xor)
                suff_inds[i]++;
        }

        // Stores the total number of ways
        int tot_ways = 0;

        // Count total number of ways
        foreach(int idx in pref_ind)
        {
            if (idx < N - 1)
                tot_ways += suff_inds[idx + 2];
        }

        // Return the final count
        return tot_ways;
    }

    // Driver code
    public static void Main(string[] args)
    {

        // Given Input
        int[] arr = { 7, 0, 5, 2, 7 };
        int N = arr.Length;

        // Function Call
        Console.WriteLine(countWays(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count ways to split array
// into three subarrays with equal Bitwise XOR
function countWays(arr, N)
{
    // Stores the XOR value of arr[]
    let arr_xor = 0;

    // Update the value of arr_xor
    for (let i = 0; i < N; i++)
        arr_xor ^= arr[i];

    // Stores the XOR value of prefix
    // and suffix array respectively
    let pref_xor = 0, suff_xor = 0;

    // Stores the ending points of all
    // the required prefix arrays
    let pref_ind = [];

    // Stores the count of suffix arrays
    // whose XOR value is equal to the
    // total XOR value at each index
    let suff_inds = new Array(N + 1);
    suff_inds.fill(0);

    // Find all prefix arrays with
    // XOR value equal to arr_xor
    for (let i = 0; i < N; i++) {

        // Update pref_xor
        pref_xor ^= arr[i];

        if (pref_xor == arr_xor)
            pref_ind.push(i);
    }

    // Fill the values of suff_inds[]
    for (let i = N - 1; i >= 0; i--) {

        // Update suff_xor
        suff_xor ^= arr[i];

        // Update suff_inds[i]
        suff_inds[i] += suff_inds[i + 1];

        if (suff_xor == arr_xor)
            suff_inds[i]++;
    }

    // Stores the total number of ways
    let tot_ways = 0;

    // Count total number of ways
    for (let idx of pref_ind) {
        if (idx < N - 1)
            tot_ways += suff_inds[idx + 2];
    }

    // Return the final count
    return tot_ways;
}

// Driver Code

    // Given Input
    let arr = [ 7, 0, 5, 2, 7 ];
    let N = arr.length;

    // Function Call
    document.write(countWays(arr, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)