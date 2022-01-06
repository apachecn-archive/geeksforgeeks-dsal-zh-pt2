# 所需的最小插入次数，使得前 K 个自然数可以作为数组子序列的和获得

> 原文:[https://www . geeksforgeeks . org/最小插入次数-必需-这样-第一个-k 个-自然数-可以作为数组子序列的总和获得/](https://www.geeksforgeeks.org/minimum-number-of-insertions-required-such-that-first-k-natural-numbers-can-be-obtained-as-sum-of-a-subsequence-of-the-array/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，任务是找到需要插入的元素的最小数量，使得范围**【1，K】**中的所有数字都可以作为数组的任何子序列的和获得。

**示例:**

> **输入:** arr[] = {1，3，5}，K = 10
> **输出:** 1
> **解释:**
> 将元素{1}附加到数组会将数组修改为{1，3，5，1}。现在，范围[1，K]内的所有和可以得到如下:
> 
> 1.  **总和 1:** 元素为{1}。
> 2.  **和 2:** 元素为{1，1}。
> 3.  **总和 3:** 元素为{3}。
> 4.  **Sum 4:** 元素为{1。3}.
> 5.  **和 5:** 元素为{1，3，1}。
> 6.  **和 6:** 元素为{1，5}。
> 7.  **和 7:** 元素为{1，5，1}。
> 8.  **和 8:** 元素为{3，5}。
> 9.  **求和 9:** 元素为{1，3，5}。
> 10.  **和 10:** 元素为{1，3，5，1}。
> 
> **输入:** arr[] = {2，6，8，12，19}，K = 20
> T3】输出: 2

**方法:**给定的问题可以通过[对数组进行递增排序](https://www.geeksforgeeks.org/quick-sort/)来解决，然后利用如果数组元素 **X** 的[和，则可以形成范围**【1，X】**内的所有值，从而试图使和值超过范围**【1，K】**。否则需要插入值 **(sum + 1)** 作为数组元素。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   [按递增顺序排列数组**arr[]**](https://www.geeksforgeeks.org/quick-sort/)。
*   初始化变量，将**索引**设为 **0** 以保持数组元素的索引，**将**设为 **0** 以存储所添加的总元素。
*   如果**arr【0】**的值大于 **1** ，则需要追加 **1** ，因此将**计数**的值增加 **1** 。否则，将**索引**的值增加 **1** 。
*   初始化变量，将**预期**设为 **2** 以保持从 **1** 到 **K** 范围内的下一个预期值，该值将由[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**形成。
*   [迭代一个循环](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到**期望**的值最多为**K**并执行以下步骤:
    *   如果**指数**大于等于 **N** 或者 **arr【指数】**大于**期望**的值，那么将**的值增加**计数 **1** 并将**期望**的值乘以 **2。**
    *   否则，将**期望**的值增加 **arr【指数】**并将**指数**的值增加 **1** 。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现。

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of elements that must be added to
// make the sum of array element over
// the range [1, K]
void findMinimumNumberOfElements(
    int n, int k, int arr[])
{
    // Sort the given array
    sort(arr, arr + n);

    // Stores the index for the
    // array
    int index = 0;
    int count = 0;

    if (arr[0] > 1) {

        // If 1 is not present, then
        // append it
        ++count;
    }

    // Move on to next index
    else {
        ++index;
    }

    // The expected value in the array
    long long expect = 2;
    while (expect <= k) {

        // Need to append this number
        if (index >= n || arr[index] > expect) {
            ++count;
            expect += expect;
        }

        // Otherwise, expand the range
        // by current number
        else {
            expect += arr[index];
            ++index;
        }
    }

    // Print the answer
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 6, 8, 12, 19 };
    int K = 20;
    int N = sizeof(arr) / sizeof(arr[0]);
    findMinimumNumberOfElements(N, K, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG {

    // Function to find the minimum number
    // of elements that must be added to
    // make the sum of array element over
    // the range [1, K]
    static void findMinimumNumberOfElements(int n, int k,
                                            int[] arr)
    {
        // Sort the given array
        Arrays.sort(arr);

        // Stores the index for the
        // array
        int index = 0;
        int count = 0;

        if (arr[0] > 1) {

            // If 1 is not present, then
            // append it
            ++count;
        }

        // Move on to next index
        else {
            ++index;
        }

        // The expected value in the array
        long expect = 2;
        while (expect <= k) {

            // Need to append this number
            if (index >= n || arr[index] > expect) {
                ++count;
                expect += expect;
            }

            // Otherwise, expand the range
            // by current number
            else {
                expect += arr[index];
                ++index;
            }
        }

        // Print the answer
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 2, 6, 8, 12, 19 };
        int K = 20;
        int N = arr.length;
        findMinimumNumberOfElements(N, K, arr);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum number
# of elements that must be added to
# make the sum of array element over
# the range [1, K]
def findMinimumNumberOfElements(n, k, arr):
    # Sort the given array
    arr.sort()

    # Stores the index for the
    # array
    index = 0
    count = 0

    if (arr[0] > 1):
        # If 1 is not present, then
        # append it
        count += 1

    # Move on to next index
    else:
        index += 1

    # The expected value in the array
    expect = 2
    while (expect <= k):

        # Need to append this number
        if (index >= n or arr[index] > expect):
            count += 1
            expect += expect

        # Otherwise, expand the range
        # by current number
        else:
            expect += arr[index]
            index += 1

    # Print the answer
    print(count)

# Driver Code
if __name__ == '__main__':
    arr = [2, 6, 8, 12, 19]
    K = 20
    N = len(arr)
    findMinimumNumberOfElements(N, K, arr)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

 // Function to find the minimum number
    // of elements that must be added to
    // make the sum of array element over
    // the range [1, K]
    static void findMinimumNumberOfElements(int n, int k,
                                            int[] arr)
    {
        // Sort the given array
        Array.Sort(arr);

        // Stores the index for the
        // array
        int index = 0;
        int count = 0;

        if (arr[0] > 1) {

            // If 1 is not present, then
            // append it
            ++count;
        }

        // Move on to next index
        else {
            ++index;
        }

        // The expected value in the array
        long expect = 2;
        while (expect <= k) {

            // Need to append this number
            if (index >= n || arr[index] > expect) {
                ++count;
                expect += expect;
            }

            // Otherwise, expand the range
            // by current number
            else {
                expect += arr[index];
                ++index;
            }
        }

        // Print the answer
        Console.WriteLine(count);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 6, 8, 12, 19 };
        int K = 20;
        int N = arr.Length;
        findMinimumNumberOfElements(N, K, arr);
    }
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum number
// of elements that must be added to
// make the sum of array element over
// the range [1, K]
function findMinimumNumberOfElements(n, k, arr) {
    // Sort the given array
    arr.sort((a, b) => a - b);

    // Stores the index for the
    // array
    let index = 0;
    let count = 0;

    if (arr[0] > 1) {

        // If 1 is not present, then
        // append it
        ++count;
    }

    // Move on to next index
    else {
        ++index;
    }

    // The expected value in the array
    let expect = 2;
    while (expect <= k) {

        // Need to append this number
        if (index >= n || arr[index] > expect) {
            ++count;
            expect += expect;
        }

        // Otherwise, expand the range
        // by current number
        else {
            expect += arr[index];
            ++index;
        }
    }

    // Print the answer
    document.write(count);
}

// Driver Code

let arr = [2, 6, 8, 12, 19];
let K = 20;
let N = arr.length;
findMinimumNumberOfElements(N, K, arr);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(max(K，N*log N))*
***辅助空间:** O(1)*