# 长度为 K 的所有子阵列的最小 MEX

> 原文:[https://www . geesforgeks . org/minimum-MEX-from-all-subarles-of-length-k/](https://www.geeksforgeeks.org/minimum-mex-from-all-subarrays-of-length-k/)

给定一个由 **N** 个不同正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是从所有[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中找到长度为 **K** 的最小值 **MEX** 。

> *MEX 是数组* *中不存在的最小正整数* [*<u>。</u>*](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)

**示例:**

> **输入:** arr[] = {1，2，3}，K = 2
> **输出:** 1
> **解释:**
> 长度为 2 的所有子阵列都是{1，2}、{2，3}。
> 在子阵列{1，2}中，不存在的最小正整数为 3。
> 在子阵列{2，3}中，不存在的最小正整数为 1。
> 因此，长度为 K (= 2)的所有子阵列的所有 MEX 的最小值为 1。
> 
> **输入:** arr[] = {1，2，3，4，5，6}，K = 3
> T3】输出: 1

**天真方法:**解决问题最简单的方法是[生成所有长度的子阵列**K**T5】并为每个](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)找到 **MEX** 。找到所有的**墨西哥**后，打印得到的最小的一个。
***时间复杂度:**O(K * N<sup>2</sup>)*
*T21】辅助空间: O(1)*

**高效方法:**上述方法也可以通过使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)和[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)进行优化。按照以下步骤解决问题:

*   初始化一个变量，比如 **mex** ，以存储大小为 **K** 的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的所有 **MEX** 中的最小值。
*   初始化一组 **S** 来存储当前子阵列中不存在的值。最初插入范围**【1，N+1】**中的所有数字，因为最初，窗口的大小是 **0** 。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K–1】**和[从集合](https://www.geeksforgeeks.org/seterase-c-stl/)中删除元素**arr【I】**。
*   现在，该组的第一个元素是超范围子阵列的**MEX****【0，K】**并将该值存储在 **mex** 中。
*   现在，重复范围**【K，N–1】**，并执行以下步骤:
    *   [将元素**arr【I】**插入到集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)中。
    *   [从设置](https://www.geeksforgeeks.org/seterase-c-stl/)中删除元素**arr【I–K】**。
    *   现在，集合的第一个元素是当前子阵列的 **MEX** 。因此，将 **mex** 的值更新为最小的 **mex** 和集合的第一个**元素。**
*   完成上述步骤后，在所有尺寸为 **K** 的子阵列中，将 **mex** 的值打印为最小值 **MEX** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return minimum
// MEX from all K-length subarrays
void minimumMEX(int arr[], int N, int K)
{
    // Stores element from [1, N + 1]
    // which are not present in subarray
    set<int> s;

    // Store number 1 to N + 1 in set s
    for (int i = 1; i <= N + 1; i++)
        s.insert(i);

    // Find the MEX of K-length
    // subarray starting from index 0
    for (int i = 0; i < K; i++)
        s.erase(arr[i]);

    int mex = *(s.begin());

    // Find the MEX of all subarrays
    // of length K by erasing arr[i]
    // and inserting arr[i - K]
    for (int i = K; i < N; i++) {

        s.erase(arr[i]);

        s.insert(arr[i - K]);

        // Store first element of set
        int firstElem = *(s.begin());

        // Updating the mex
        mex = min(mex, firstElem);
    }

    // Print minimum MEX of
    // all K length subarray
    cout << mex << ' ';
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);

    minimumMEX(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashSet;

class GFG{

// Function to return minimum
// MEX from all K-length subarrays
static void minimumMEX(int arr[], int N, int K)
{

    // Stores element from [1, N + 1]
    // which are not present in subarray
    HashSet<Integer> s = new HashSet<Integer>();

    // Store number 1 to N + 1 in set s
    for(int i = 1; i <= N + 1; i++)
        s.add(i);

    // Find the MEX of K-length
    // subarray starting from index 0
    for(int i = 0; i < K; i++)
        s.remove(arr[i]);

    int mex = s.iterator().next();

    // Find the MEX of all subarrays
    // of length K by erasing arr[i]
    // and inserting arr[i - K]
    for(int i = K; i < N; i++)
    {
        s.remove(arr[i]);
        s.add(arr[i - K]);

        // Store first element of set
        int firstElem = s.iterator().next();

        // Updating the mex
        mex = Math.min(mex, firstElem);
    }

    // Print minimum MEX of
    // all K length subarray
    System.out.print(mex + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int K = 3;
    int N = arr.length;

    minimumMEX(arr, N, K);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to return minimum
# MEX from all K-length subarrays
def minimumMEX(arr, N, K):

    # Stores element from [1, N + 1]
    # which are not present in subarray
    s = set()

    # Store number 1 to N + 1 in set s
    for i in range(1, N + 2, 1):
        s.add(i)

    # Find the MEX of K-length
    # subarray starting from index 0
    for i in range(K):
        s.remove(arr[i])

    mex = list(s)[0]

    # Find the MEX of all subarrays
    # of length K by erasing arr[i]
    # and inserting arr[i - K]
    for i in range(K,N,1):
        s.remove(arr[i])

        s.add(arr[i - K])

        # Store first element of set
        firstElem = list(s)[0]

        # Updating the mex
        mex = min(mex, firstElem)

    # Print minimum MEX of
    # all K length subarray
    print(mex)

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6]
    K = 3
    N = len(arr)
    minimumMEX(arr, N, K)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

// Function to return minimum
// MEX from all K-length subarrays
static void minimumMEX(int[] arr, int N, int K)
{

    // Stores element from [1, N + 1]
    // which are not present in subarray
    HashSet<int> s = new HashSet<int>();

    // Store number 1 to N + 1 in set s
    for(int i = 1; i <= N + 1; i++)
        s.Add(i);

    // Find the MEX of K-length
    // subarray starting from index 0
    for(int i = 0; i < K; i++)
        s.Remove(arr[i]);
    int mex = s.First();

    // Find the MEX of all subarrays
    // of length K by erasing arr[i]
    // and inserting arr[i - K]
    for(int i = K; i < N; i++)
    {
        s.Remove(arr[i]);
        s.Add(arr[i - K]);

        // Store first element of set
        int firstElem = s.First();

        // Updating the mex
        mex = Math.Min(mex, firstElem);
    }

    // Print minimum MEX of
    // all K length subarray
    Console.Write(mex + " ");
}

// Driver code
static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int K = 3;
    int N = arr.Length;

    minimumMEX(arr, N, K);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to return minimum
    // MEX from all K-length subarrays
    function minimumMEX(arr, N, K)
    {

        // Stores element from [1, N + 1]
        // which are not present in subarray
        let s = new Set();

        // Store number 1 to N + 1 in set s
        for(let i = 1; i <= N + 1; i++)
            s.add(i);

        // Find the MEX of K-length
        // subarray starting from index 0
        for(let i = 0; i < K; i++)
            s.delete(arr[i]);
        let entry = s.entries();
        let mex = 1;

        // Find the MEX of all subarrays
        // of length K by erasing arr[i]
        // and inserting arr[i - K]
        for(let i = K; i < N; i++)
        {
            s.delete(arr[i]);
            s.add(arr[i - K]);

            // Store first element of set
            let firstElem = entry.next().value

            // Updating the mex
            mex = Math.min(mex, 1);
        }

        // Print minimum MEX of
        // all K length subarray
        document.write(mex + " ");
    }

    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let K = 3;
    let N = arr.length;

    minimumMEX(arr, N, K);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)