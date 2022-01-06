# 通过在末端顺序插入数组元素的字典式最大排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-最大-按顺序-插入-数组-元素-在末端/](https://www.geeksforgeeks.org/lexicographically-largest-permutation-by-sequentially-inserting-array-elements-at-ends/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过将数组元素依次插入到另一个数组的前面或后面来找到字典上最大的排列。

**示例:**

> **输入:** arr[] = {3，1，2，4}
> **输出:** 4 3 1 2
> **解释:**
> 通过将数组元素依次插入容器的前面或后面可以创建的排列是{3，1，2，4}、{1，3，2，4}、{2，3，1，4}、{2，1，4}、{ 2，1，3，4}、{4，1，3，2}、{4 其中{4，3，1，2}是最大的排列。
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 5 4 3 2 1

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)使用[得求](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)来解决，这是基于这样的观察，即如果当前数组元素至少是新数组的第一个元素，则最理想的选择总是将该元素插入容器的前面，以便在字典上最大化排列。否则，将元素插入数组的末尾。按照以下步骤解决给定的问题:

*   初始化一个 [deque](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/) ，比如说 **DQ** ，它存储容器的当前状态。
*   初始化一个变量，比如 **mx** ，它存储最大值，直到每个索引都代表了德格 **DQ** 的**1<sup>ST</sup>T5】元素。**
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果当前元素**arr[I]****>=****MX**，则将 **arr[i]** 插入到德格 **DQ** 的前面，更新 **mx** 的值。否则，将**arr【I】**插入德格 **DQ** 后面。
*   完成上述步骤后，将存储在德格 **DQ** 中的元素打印为结果最大排列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// largest permutation by sequentially
// inserting the array elements
void largestPermutation(int arr[], int N)
{

    // Stores the current state of
    // the new array
    deque<int> p;

    // Stores ythe current maximum
    // element of array arr[]
    int mx = arr[0];
    p.push_back(arr[0]);

    // Iterate the array elements
    for (int i = 1; i < N; i++) {

        // If the current element is
        // smaller than the current
        // maximum, then insert
        if (arr[i] < mx)
            p.push_back(arr[i]);

        // If the current element is
        // at least the current maximum
        else {
            p.push_front(arr[i]);

            // Update the value of
            // the current maximum
            mx = arr[i];
        }
    }

    // Print resultant permutation
    for (auto i : p)
        cout << i << " ";
}

// Driver Code
int main()
{
    int arr[] = { 3, 1, 2, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    largestPermutation(arr, N);

    return 0;
}
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the lexicographically
# largest permutation by sequentially
# inserting the array elements
from typing import Deque

def largestPermutation(arr, N):

    # Stores the current state of
    # the new array
    p = Deque()

    # Stores ythe current maximum
    # element of array arr[]
    mx = arr[0]
    p.append(arr[0])

    # Iterate the array elements
    for i in range(1, N):

        # If the current element is
        # smaller than the current
        # maximum, then insert
        if (arr[i] < mx):
            p.append(arr[i])

        # If the current element is
        # at least the current maximum
        else:
            p.appendleft(arr[i])

            # Update the value of
            # the current maximum
            mx = arr[i]

    # Print resultant permutation
    for i in p:
        print(i, end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [3, 1, 2, 4]
    N = len(arr)

    largestPermutation(arr, N)

# This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the lexicographically
// largest permutation by sequentially
// inserting the array elements
function largestPermutation(arr, N)
{

  // Stores the current state of
  // the new array
  let p = [];

  // Stores ythe current maximum
  // element of array arr[]
  let mx = arr[0];
  p.push(arr[0]);

  // Iterate the array elements
  for (let i = 1; i < N; i++)
  {

    // If the current element is
    // smaller than the current
    // maximum, then insert
    if (arr[i] < mx) p.push(arr[i]);

    // If the current element is
    // at least the current maximum
    else {
      p.unshift(arr[i]);

      // Update the value of
      // the current maximum
      mx = arr[i];
    }
  }

  // Prlet resultant permutation
  for (i of p) document.write(i + " ");
}

// Driver Code

let arr = [3, 1, 2, 4];
let N = arr.length;

largestPermutation(arr, N);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
4 3 1 2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)