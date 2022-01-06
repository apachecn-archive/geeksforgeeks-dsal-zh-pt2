# 对所有可能的数组进行计数，使得每个数组元素都可以在[1，arr[i]]

的范围内

> 原文:[https://www . geesforgeks . org/所有可能数组的计数-这样每个数组元素都可以超出范围-1-arri/](https://www.geeksforgeeks.org/count-of-all-possible-arrays-such-that-each-array-element-can-be-over-the-range-1-arri/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出所有可能数组的数量，使得每个数组元素可以在**【1，arr[I]】**的范围内，新构造的[数组中的所有元素必须成对不同](https://www.geeksforgeeks.org/shortest-subarray-to-be-removed-to-make-all-array-elements-unique/)。

**示例:**

> **输入:** arr[] = {5}
> **输出:** 5
> **解释:**
> 使用给定标准可以形成的所有可能数组为{1}、{2}、{3}、{4}、{5}。因此，这种阵列的计数是 5。
> 
> **输入:** arr[] = {4，4，4，4 }
> T3】输出: 24

**方法:**给定的问题可以基于这样的观察来解决，即数组元素的顺序 **arr[]** 与使用新标准生成数组的顺序无关。下图也是同样的情况:

插图:

> 考虑数组 arr[] = {1，2}，满足给定条件的每个可能的数组都是{1，2}。
> 
> 现在，如果 arr[]元素的顺序改变，比如说{2，1}，那么满足给定条件的所有可能的数组都是{2，1}。

按照以下步骤解决给定的问题:

*   [按照非递减顺序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)对数组 **arr[]** 进行排序。
*   初始化一个变量，比如说 **res** 为 **1** ，它存储所有可能形成的数组的计数。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素 **arr[i]** 执行以下步骤:
    *   在索引 **i** 处插入新数组元素的所有可能选择的计数是**arr【I】**，但是为了使数组成对不同，所有先前选择的数字不能再次被选择。因此，可用选项的总数为**(arr[I]–I)**。
    *   现在，索引 **i** 之前可能的组合总数由**RES *(arr[I]–I)**给出。因此，将 **res** 的值更新为**RES *(arr[I]–I)**。
*   完成上述步骤后，打印 **res** 的值，作为形成的数组的最终可能计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total number of
// arrays of pairwise distinct element
// and each element lies in [1, arr[i]]
int findArraysInRange(int arr[], int N)
{
    // Stores all possible arrays formed
    int res = 1;

    // Sort the array arr[] in the
    // non-decreasing order
    sort(arr, arr + N);

    for (int i = 0; i < N; i++) {

        // Total combinations for the
        // current index i
        int combinations = (arr[i] - i);

        // Update the value of res
        res *= combinations;
    }

    // Return the possible count
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 4, 4, 4, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findArraysInRange(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the total number of
    // arrays of pairwise distinct element
    // and each element lies in [1, arr[i]]
    static int findArraysInRange(int[] arr, int N)
    {

        // Stores all possible arrays formed
        int res = 1;

        // Sort the array arr[] in the
        // non-decreasing order
        Arrays.sort(arr);

        for (int i = 0; i < N; i++) {

            // Total combinations for the
            // current index i
            int combinations = (arr[i] - i);

            // Update the value of res
            res *= combinations;
        }

        // Return the possible count
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 4, 4, 4, 4 };
        int N = arr.length;
        System.out.print(findArraysInRange(arr, N));
    }
}

// This code is contributed by subhammahato348.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the total number of
# arrays of pairwise distinct element
# and each element lies in [1, arr[i]]
def findArraysInRange(arr, n):

    # Sort the array
    arr.sort()

    # res Stores all possible arrays formed
    res = 1
    i = 0

    # Sort the array arr[] in the
    # non-decreasing order
    arr.sort()

    for i in range(0, n):

        # Total combinations for the
        # current index i
        combinations = (arr[i] - i)

        # Update the value of res
        res = res*combinations

    # Return the possible count
    return res

# Driver Code
arr = [4, 4, 4, 4]
N = len(arr)
print(findArraysInRange(arr, N))

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to find the total number of
    // arrays of pairwise distinct element
    // and each element lies in [1, arr[i]]
    static int findArraysInRange(int[] arr, int N)
    {

        // Stores all possible arrays formed
        int res = 1;

        // Sort the array arr[] in the
        // non-decreasing order
        Array.Sort(arr);

        for (int i = 0; i < N; i++) {

            // Total combinations for the
            // current index i
            int combinations = (arr[i] - i);

            // Update the value of res
            res *= combinations;
        }

        // Return the possible count
        return res;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 4, 4, 4, 4 };
        int N = arr.Length;
        Console.Write(findArraysInRange(arr, N));
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the total number of
// arrays of pairwise distinct element
// and each element lies in [1, arr[i]]
function findArraysInRange(arr, n, k) {
// Sort the array
arr.sort((a, b) => a - b);

// res Stores all possible arrays formed
let res= 1,i=0,combinations;

// Sort the array arr[] in the
    // non-decreasing order
   arr.sort((a, b) => a - b);

    for (i = 0; i < N; i++) {

        // Total combinations for the
        // current index i
         combinations = (arr[i] - i);

        // Update the value of res
        res = res*combinations;
    }

    // Return the possible count

return res;
}

// Driver Code

let arr = [4,4,4,4];
let N = arr.length;
document.write(findArraysInRange(arr, N));

// This code is contributed by dwivediyash
</script>
```

**Output:** 

```
24
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*