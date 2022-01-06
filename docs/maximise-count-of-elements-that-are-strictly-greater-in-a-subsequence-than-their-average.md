# 最大化子序列中严格大于其平均值的元素数量

> 原文:[https://www . geeksforgeeks . org/最大化子序列中严格大于平均值的元素数量/](https://www.geeksforgeeks.org/maximise-count-of-elements-that-are-strictly-greater-in-a-subsequence-than-their-average/)

给定一个包含正整数的大小为 **N** 的数组 **arr[]** ，任务是使用任意数量的运算找到可以从数组中删除的元素的最大数量。在一个操作中，从给定的[数组](https://www.geeksforgeeks.org/array-data-structure/)中选择一个子序列，取它们的[平均值](https://www.geeksforgeeks.org/average/)，并从数组中删除严格大于该平均值的数字。

**示例:**

> **输入:** arr[] = {1，1，3，2，4}
> **输出:** 3
> **解释:**
> 操作 1:选择子序列{1，2，4}，求平均值= (1+2+4)/3 = 2。所以 arr[5]=4 被删除。arr[]={1，1，3，2}
> 操作 2:选择子序列{1，3，2}，平均值= (1+3+2)/3 = 2。所以 arr[2]=3 被删除。arr[]={1，1，2}
> 操作 3:选择子序列{1，1}，平均值= (1+1)/2 = 1。所以 arr[3]=2 被删除。arr[]={1，1}
> 不能执行进一步的删除。
> 
> **输入:** arr[] = {5，5，5 }
> T3】输出: 0

**方法:**这个问题的难点在于，除了最小元素之外的所有元素都可以从数组中删除，因为如果只使用最小元素来创建子序列，那么它的平均值基本上是相同的元素，所有其他元素都可以删除。现在要解决这个问题，请按照以下步骤操作:

1.  求最小元素的频率，说 **freq** 。
2.  返回 **N-freq** 作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number of
// elements that can be deleted from the array
int elementsDeleted(vector<int>& arr)
{

    // Size of the array
    int N = arr.size();

    // Minimum element
    auto it = *min_element(arr.begin(), arr.end());

    // Finding frequency of minimum element
    int freq = 0;
    for (auto x : arr) {
        if (x == it)
            freq++;
    }

    return N - freq;
}

// Driver Code
int main()
{
    vector<int> arr = { 3, 1, 1, 2, 4 };
    cout << elementsDeleted(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find the maximum number of
// elements that can be deleted from the array
static int elementsDeleted(int []arr)
{

    // Size of the array
    int N = arr.length;

    // Minimum element
    int it = Arrays.stream(arr).min().getAsInt();

    // Finding frequency of minimum element
    int freq = 0;
    for (int x : arr) {
        if (x == it)
            freq++;
    }

    return N - freq;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 3, 1, 1, 2, 4 };
    System.out.print(elementsDeleted(arr));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the maximum number of
# elements that can be deleted from the array
def elementsDeleted(arr):

    # Size of the array
    N = len(arr)

    # Minimum element
    it = 10**9

    for i in range(len(arr)):
        it = min(it, arr[i])

    # Finding frequency of minimum element
    freq = 0
    for x in arr:
        if (x == it):
            freq += 1
    return N - freq

# Driver Code
arr = [3, 1, 1, 2, 4]
print(elementsDeleted(arr))

# This code is contributed by Saurabh jaiswal
```

## C#

```
// C# code for the above approach
using System;
using System.Linq;
class GFG {

    // Function to find the maximum number of
    // elements that can be deleted from the array
    static int elementsDeleted(int[] arr)
    {

        // Size of the array
        int N = arr.Length;

        // Minimum element
        int it = arr.Min();

        // Finding frequency of minimum element
        int freq = 0;
        foreach(int x in arr)
        {
            if (x == it)
                freq++;
        }

        return N - freq;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 3, 1, 1, 2, 4 };
        Console.WriteLine(elementsDeleted(arr));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find the maximum number of
      // elements that can be deleted from the array
      function elementsDeleted(arr) {

          // Size of the array
          let N = arr.length;

          // Minimum element
          let it = Number.MAX_VALUE;

          for (let i = 0; i < arr.length; i++) {
              it = Math.min(it, arr[i]);
          }

          // Finding frequency of minimum element
          let freq = 0;
          for (let x of arr) {
              if (x == it)
                  freq++;
          }

          return N - freq;
      }

      // Driver Code

      let arr = [3, 1, 1, 2, 4];
      document.write(elementsDeleted(arr));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)