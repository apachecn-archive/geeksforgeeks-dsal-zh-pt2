# 通过用任何索引最多 K 次的和替换两个元素来最小化减少数组的成本

> 原文:[https://www . geeksforgeeks . org/通过将两个元素替换为最多 k 次的任意索引来最小化减少数组的成本/](https://www.geeksforgeeks.org/minimize-cost-for-reducing-array-by-replacing-two-elements-with-sum-at-most-k-times-for-any-index/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-class-c/) **arr[]** 和一个整数 **K** 。任务是找到收集数组总和所需的最小成本。通过选取任何元素并将其添加到数组中任何索引的元素中来收集数组的总和。同一指标的元素添加最多允许 **K** 次。

**示例:**

> **输入:** arr[] = {3，6，4，1，1}，N = 5，K = 2
> **输出:** 11
> **说明:**数组的和可以收集如下:
> 
> *   在索引 4 处选择元素，并将其添加到索引 2 处的元素，即(1 ⇢ 4) = 1+4 = 5，成本= 1，arr[] = {3，6，5，1，0}。
> *   在索引 3 处选择元素，并将其添加到索引 2 处的元素，即(1 ⇢ 5) = 1+5 = 6，成本= 1+1 = 2，arr[] = {3，6，6，0，0}。
> *   在索引 0 处选取元素，并将其添加到索引 1 处的元素，即(3 ⇢ 6) = 3+6 = 9，成本= 2+3 = 5，arr[] = {0，9，6，0，0}。
> *   在索引 2 处选择元素，并将其添加到索引 1 处的元素，即(6 ⇢ 9) = 6+9 = 15，成本= 5+6 = 11，arr[] = {0，15，0，0，0}。
> 
> **输入:** arr[] = {5，3，2，1，4，6}，N = 6，K = 3
> **输出:** 18
> **说明:**求和可按如下方式进行
> 
> *   在索引 3 处选择元素，并将其添加到索引 4 处的元素，即(1 ⇢ 4) = 1+4 = 5，成本= 1，arr[] = {5，3，2，0，5，6}。
> *   在索引 2 处选取元素，并将其添加到索引 0 处的元素，即(2 ⇢ 5) = 2+5 = 7，成本= 1+2 = 3，arr[] = {7，3，0，0，5，6}。
> *   在索引 1 处选择元素，并将其添加到索引 5 处的元素，即(3 ⇢ 6) = 3+6 = 9，成本= 3+3 = 6，arr[] = {7，0，0，0，5，9}。
> *   在索引 4 处选择元素，并将其添加到索引 5 处的元素，即(5 ⇢ 9) = 5+9 = 14，成本= 6+5 = 11，arr[] = {7，0，0，0，0，14}。
> *   在索引 0 处选取元素，并将其添加到索引 5 处的元素，即(7 ⇢ 14) = 7+14 = 21，成本= 11+7 = 18，arr[] = {0，0，0，0，0，21}。

**方法:**给定的问题可以使用[贪婪的](http://www.geeksforgeeks.org/greedy-algorithms/)方法来解决。想法是[整理阵列](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。以下对问题的解释:给定的元素是图的顶点。⇢操作将一个元素添加到其他⇢操作中，以将一个顶点的子树暂停到另一个顶点。

任务是得到这样的树结构，每个顶点有不超过 K 个子树悬挂在上面，写在顶点上的数字和顶点深度(其中根的深度为 0)的乘积之和**最小。**为了最小化总和:

*   具有较大数量**的顶点不得比具有较小数量**的顶点具有更大的**深度(否则有可能改变它们并获得更少的总和)。**
*   每个内部顶点，除此之外，也许，一个，有**正好 k 个后继者。**(实际实现中，不需要建树，我们只需要知道这是一棵树。)

现在计算这个配置的总和。为了做到这一点，请遵循以下步骤:

*   将从**第 1 到第 kth** 的元素之和相加(在 0 索引数组中，按非递增顺序排序)，**乘以 1**；然后将下 k 个桩的尺寸之和乘以 2；以此类推，直到数组结束。
*   排序数组后，使用 [**前缀和**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 即可得到线段和的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the difference
// of the elements in a range
int sum(int s[], int l, int r, int N)
{

    r = min(r, (N - 1));

    return s[r] - s[l - 1];
}

// Function to find the minimum cost required
// to collect the sum of the array
int minCost(int arr[], int K, int N)
{

    int s[N];

    // Sort the array in descending order
    sort(arr, arr + N, greater<int>());

    s[0] = arr[0];

    // Traverse and store the sums
    // in prefix array s[]
    for (int i = 1; i < N; i++)
        s[i] = s[i - 1] + arr[i];

    int res_1 = 0;

    // Iterate the array and add the
    // value of the element
    // multiplied by its index
    for (int i = 1; i < N; i++)
        res_1 += arr[i] * i;

    // If K = 1 return res_1
    if (K == 1)
        return res_1;

    // Variable to store the answer
    int res = 0, sz = 1;

    // Traverse and find the
    // answer accordingly
    for (int j = 1, t = 1; j < N; j += sz, t++) {

        sz *= K;
        res += sum(s, j, j + sz - 1, N) * t;
    }

    // Return res
    return res;
}

// Driver Code
int main()
{

    // Initialize the array
    int arr[] = { 3, 6, 4, 1, 1 };

    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Call the function and
    // print the answer
    cout << minCost(arr, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.Arrays;
import java.util.Collections;
class GFG {

    // Function to return the difference
    // of the elements in a range
    static int sum(int s[], int l, int r, int N)
    {

        r = Math.min(r, (N - 1));

        return s[r] - s[l - 1];
    }

    // Function to find the minimum cost required
    // to collect the sum of the array
    static int minCost(int arr[], int K, int N)
    {

        int[] s = new int[N];

        // Sort the array in descending order
        // Sorting the array in ascending order
        Arrays.sort(arr);

        // Reversing the array
        reverse(arr);

        s[0] = arr[0];

        // Traverse and store the sums
        // in prefix array s[]
        for (int i = 1; i < N; i++)
            s[i] = s[i - 1] + arr[i];

        int res_1 = 0;

        // Iterate the array and add the
        // value of the element
        // multiplied by its index
        for (int i = 1; i < N; i++)
            res_1 += arr[i] * i;

        // If K = 1 return res_1
        if (K == 1)
            return res_1;

        // Variable to store the answer
        int res = 0, sz = 1;

        // Traverse and find the
        // answer accordingly
        for (int j = 1, t = 1; j < N; j += sz, t++) {

            sz *= K;
            res += sum(s, j, j + sz - 1, N) * t;
        }

        // Return res
        return res;
    }
    public static void reverse(int[] array)
    {

        // Length of the array
        int n = array.length;

        // Swaping the first half elements with last half
        // elements
        for (int i = 0; i < n / 2; i++) {

            // Storing the first half elements temporarily
            int temp = array[i];

            // Assigning the first half to the last half
            array[i] = array[n - i - 1];

            // Assigning the last half to the first half
            array[n - i - 1] = temp;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Initialize the array
        int arr[] = { 3, 6, 4, 1, 1 };

        int K = 2;
        int N = arr.length;

        // Call the function and
        // print the answer

        System.out.println(minCost(arr, K, N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to return the difference
# of the elements in a range
def sum (s, l, r, N):
    r = min(r, (N - 1))
    return s[r] - s[l - 1]

# Function to find the minimum cost required
# to collect the sum of the array
def minCost (arr, K, N):

    s = [0] * N

    # Sort the array in descending order
    arr = sorted(arr, reverse=True)

    s[0] = arr[0]

    # Traverse and store the sums
    # in prefix array s[]
    for i in range(1, N):
        s[i] = s[i - 1] + arr[i]

    res_1 = 0

    # Iterate the array and add the
    # value of the element
    # multiplied by its index
    for i in range(1, N):
        res_1 += arr[i] * i

    # If K = 1 return res_1
    if (K == 1):
        return res_1

    # Variable to store the answer
    res = 0
    sz = 1

    # Traverse and find the
    # answer accordingly
    j=1
    t=1

    while(j < N ):
        sz *= K
        res += sum(s, j, j + sz - 1, N) * t
        j += sz
        t += 1

    # Return res
    return res

# Driver Code

# Initialize the array
arr = [3, 6, 4, 1, 1]

K = 2
N = len(arr)

# Call the function and
# print the answer
print(minCost(arr, K, N))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code for the above approach
using System;

public class GFG {

    // Function to return the difference
    // of the elements in a range
    static int sum(int []s, int l, int r, int N)
    {

        r = Math.Min(r, (N - 1));

        return s[r] - s[l - 1];
    }

    // Function to find the minimum cost required
    // to collect the sum of the array
    static int minCost(int []arr, int K, int N)
    {

        int[] s = new int[N];

        // Sort the array in descending order
        // Sorting the array in ascending order
        Array.Sort(arr);

        // Reversing the array
        reverse(arr);

        s[0] = arr[0];

        // Traverse and store the sums
        // in prefix array s[]
        for (int i = 1; i < N; i++)
            s[i] = s[i - 1] + arr[i];

        int res_1 = 0;

        // Iterate the array and add the
        // value of the element
        // multiplied by its index
        for (int i = 1; i < N; i++)
            res_1 += arr[i] * i;

        // If K = 1 return res_1
        if (K == 1)
            return res_1;

        // Variable to store the answer
        int res = 0, sz = 1;

        // Traverse and find the
        // answer accordingly
        for (int j = 1, t = 1; j < N; j += sz, t++) {

            sz *= K;
            res += sum(s, j, j + sz - 1, N) * t;
        }

        // Return res
        return res;
    }
    public static void reverse(int[] array)
    {

        // Length of the array
        int n = array.Length;

        // Swaping the first half elements with last half
        // elements
        for (int i = 0; i < n / 2; i++) {

            // Storing the first half elements temporarily
            int temp = array[i];

            // Assigning the first half to the last half
            array[i] = array[n - i - 1];

            // Assigning the last half to the first half
            array[n - i - 1] = temp;
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Initialize the array
        int []arr = { 3, 6, 4, 1, 1 };

        int K = 2;
        int N = arr.Length;

        // Call the function and
        // print the answer

        Console.WriteLine(minCost(arr, K, N));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // JavaScript implementation for the above approach

    // Function to return the difference
    // of the elements in a range
    const sum = (s, l, r, N) => {

        r = Math.min(r, (N - 1));

        return s[r] - s[l - 1];
    }

    // Function to find the minimum cost required
    // to collect the sum of the array
    const minCost = (arr, K, N) => {

        let s = new Array(N).fill(0);

        // Sort the array in descending order
        arr.sort((a, b) => b - a);

        s[0] = arr[0];

        // Traverse and store the sums
        // in prefix array s[]
        for (let i = 1; i < N; i++)
            s[i] = s[i - 1] + arr[i];

        let res_1 = 0;

        // Iterate the array and add the
        // value of the element
        // multiplied by its index
        for (let i = 1; i < N; i++)
            res_1 += arr[i] * i;

        // If K = 1 return res_1
        if (K == 1)
            return res_1;

        // Variable to store the answer
        let res = 0, sz = 1;

        // Traverse and find the
        // answer accordingly
        for (let j = 1, t = 1; j < N; j += sz, t++) {

            sz *= K;
            res += sum(s, j, j + sz - 1, N) * t;
        }

        // Return res
        return res;
    }

    // Driver Code

    // Initialize the array
    let arr = [3, 6, 4, 1, 1];

    let K = 2;
    let N = arr.length

    // Call the function and
    // print the answer
    document.write(minCost(arr, K, N));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
11
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(N)