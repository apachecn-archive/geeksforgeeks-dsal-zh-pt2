# 最小化移除时将阵列分成 3 个子阵列的对的和

> 原文:[https://www . geeksforgeeks . org/最小化移除时将阵列分成 3 个子阵列的对总和/](https://www.geeksforgeeks.org/minimize-the-sum-of-pair-which-upon-removing-divides-the-array-into-3-subarrays/)

给定一个大小为 **N** 的数组 **arr** ，任务是找到具有最小和的元素对，在移除时将该数组分解为原始数组的 3 个非空子数组。打印该对元素的总和。

> **输入:** arr[]: {4，2，1，2，4}
> **输出:** 4
> **解释:**
> 最小和对是值(2，1)和(1，2)，但是选择具有相邻索引的对不会将数组分成 3 部分。下一个最小值对是(2，2)，它将数组分为{4}、{1}、{4}。因此答案是 2 + 2 = 4。
> 
> **输入:** arr[] = {5，2，4，6，3，7}
> **输出:** 5
> **解释:**
> 在所有将数组分成 3 个子部分的对中，值为(2，3)的对给出最小和。

**天真的做法:**将阵列分成三个子阵列。需要移除的两个元素应符合以下条件:

*   任何端点(索引 ***0*** 和 ***N-1*** )都不能被选择。
*   无法选择相邻的索引。

因此，找到所有可能的组合对，并选择一个符合上述条件，并有最低的总和。

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)

**高效方法**:按照以下步骤高效解决此问题:

1.  创建一个数组前缀，其中**with**元素表示数组 arr 中从第 0 到第 1 个索引的最小元素。
2.  创建一个变量 ans，存储最终答案并用 INT_MAX 初始化它。
3.  现在，对 i=3 到 i=N-1 运行一个循环(从 3 开始，因为第 0 个不能被选择，并且这个循环是选择对中的第二个元素，这意味着它甚至不能从 2 开始，因为那么第一个元素的唯一剩余选项是 1 和 2，这两个选项都不遵循给定的条件)，并且在每次迭代中将 ans 更改为 ans 和 arr[i]+prefixMin[i-2]中的最小值。
4.  执行上述步骤后，打印 ans。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum possible sum
// of pair which breaks the array into 3
// non-empty subarrays
int minSumPair(int arr[], int N)
{

    if (N < 5) {
        return -1;
    }

    int prefixMin[N];
    prefixMin[0] = arr[0];

    // prefixMin[i] contains minimum element till i
    for (int i = 1; i < N - 1; i++) {
        prefixMin[i] = min(arr[i], prefixMin[i - 1]);
    }

    int ans = INT_MAX;

    for (int i = 3; i < N - 1; i++) {
        ans = min(ans, arr[i] + prefixMin[i - 2]);
    }

    return ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 5, 2, 4, 6, 3, 7 };
    int N = sizeof(arr) / sizeof(int);

    cout << minSumPair(arr, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find minimum possible sum
// of pair which breaks the array into 3
// non-empty subarrays
static int minSumPair(int arr[], int N)
{

    if (N < 5) {
        return -1;
    }

    int []prefixMin = new int[N];
    prefixMin[0] = arr[0];

    // prefixMin[i] contains minimum element till i
    for (int i = 1; i < N - 1; i++) {
        prefixMin[i] = Math.min(arr[i], prefixMin[i - 1]);
    }

    int ans = Integer.MAX_VALUE;

    for (int i = 3; i < N - 1; i++) {
        ans = Math.min(ans, arr[i] + prefixMin[i - 2]);
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // Given array
    int arr[] = { 5, 2, 4, 6, 3, 7 };
    int N = arr.length;

    System.out.print(minSumPair(arr, N) +"\n");

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach
import sys

# Function to find minimum possible sum
# of pair which breaks the array into 3
# non-empty subarrays
def minSumPair(arr, N):
    if(N < 5):
        return -1

    prefixMin = [0 for i in range(N)]
    prefixMin[0] = arr[0]

    # prefixMin[i] contains minimum element till i
    for i in range(1,N - 1,1):
        prefixMin[i] = min(arr[i], prefixMin[i - 1])

    ans = sys.maxsize

    for i in range(3,N - 1,1):
        ans = min(ans, arr[i] + prefixMin[i - 2])

    return ans

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [5, 2, 4, 6, 3, 7]
    N = len(arr)
    print(minSumPair(arr, N))

    # This code is contributed by ipg201107.
```

## C#

```
// C# implementation of the above approach
using System;

public class GFG{

// Function to find minimum possible sum
// of pair which breaks the array into 3
// non-empty subarrays
static int minSumPair(int []arr, int N)
{

    if (N < 5) {
        return -1;
    }

    int []prefixMin = new int[N];
    prefixMin[0] = arr[0];

    // prefixMin[i] contains minimum element till i
    for (int i = 1; i < N - 1; i++) {
        prefixMin[i] = Math.Min(arr[i], prefixMin[i - 1]);
    }

    int ans = int.MaxValue;

    for (int i = 3; i < N - 1; i++) {
        ans = Math.Min(ans, arr[i] + prefixMin[i - 2]);
    }

    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 5, 2, 4, 6, 3, 7 };
    int N = arr.Length;

    Console.Write(minSumPair(arr, N) +"\n");

}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find minimum possible sum
        // of pair which breaks the array into 3
        // non-empty subarrays
        function minSumPair(arr, N) {

            if (N < 5) {
                return -1;
            }

            let prefixMin = new Array(N).fill(0);
            prefixMin[0] = arr[0];

            // prefixMin[i] contains minimum element till i
            for (let i = 1; i < N - 1; i++) {
                prefixMin[i] = Math.min(arr[i], prefixMin[i - 1]);
            }

            let ans = Number.MAX_VALUE;

            for (let i = 3; i < N - 1; i++) {
                ans = Math.min(ans, arr[i] + prefixMin[i - 2]);
            }

            return ans;
        }

        // Driver Code

        // Given array
        let arr = [5, 2, 4, 6, 3, 7];
        let N = arr.length;

        document.write(minSumPair(arr, N));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
5
```

**时间复杂度** : *O(n)*

**空间复杂度** : *O(n)*