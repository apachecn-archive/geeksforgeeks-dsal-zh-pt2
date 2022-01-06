# 尽量减少将第一个和最后一个元素分别作为数组中最大和最小元素所需的交换

> 原文:[https://www . geeksforgeeks . org/minimum-swaps-需要制作第一个和最后一个元素-分别是数组中最大和最小的元素/](https://www.geeksforgeeks.org/minimize-swaps-required-to-make-the-first-and-last-elements-the-largest-and-smallest-elements-in-the-array-respectively/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到使数组中的第一个和最后一个元素分别成为数组中最大的和最小的[个元素所需的相邻交换的最小数量。](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

**示例:**

> **输入:** arr[] = {1，3，2}
> **输出:** 2
> **解释:**
> 最初数组为{1，3，2}。
> 操作 1:在索引 0 和 1 处交换元素。数组修改为{3，1，2}。
> 操作 2:在索引 1 和索引 2 处交换元素。数组修改为{3，2，1}。
> 因此，所需的最小操作次数为 2 次。
> 
> **输入:** arr[] = {100，95，100，100，88}
> **输出:** 0

**方法:**按照以下步骤解决给定问题:

*   初始化一个变量，比如说**计数**，以存储所需的交换总数。
*   找到数组的最小值和[最大值元素并存储在变量中，分别说 **minElement** 和 **maxElement** 。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   如果发现最小和最大元素相同，则数组由单个不同的元素组成。因此，打印 **0** ，因为两个元素分别处于正确的位置。
*   否则[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)找到 **maxElement** 的第一次出现和 **minElement** 的最后一次出现的索引并存储在变量中，分别说 **minIndex** 和 **maxIndex** 。
*   更新**的值，将**计为**最大索引**和**(N–1–minidex)**之和，作为将最大和最小元素分别作为数组的第一个和最后一个元素所需的交换操作数。
*   如果**最小索引**小于**最大索引**，那么将**计数**减少 **1** ，因为一个交换操作将重叠。
*   完成上述步骤后，打印**计数**的值，作为所需的最小交换次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of swaps required to make the first
// and the last elements the largest
// and smallest element in the array
int minimum_swaps(int arr[], int n)
{
    // Stores the count of swaps
    int count = 0;

    // Stores the maximum element
    int max_el = *max_element(arr,
                              arr + n);

    // Stores the minimum element
    int min_el = *min_element(arr,
                              arr + n);

    // If the array contains
    // a single distinct element
    if (min_el == max_el)
        return 0;

    // Stores the indices of the
    // maximum and minimum elements
    int index_max = -1;
    int index_min = -1;

    for (int i = 0; i < n; i++) {

        // If the first index of the
        // maximum element is found
        if (arr[i] == max_el
            && index_max == -1) {
            index_max = i;
        }

        // If current index has
        // the minimum element
        if (arr[i] == min_el) {
            index_min = i;
        }
    }

    // Update the count of operations to
    // place largest element at the first
    count += index_max;

    // Update the count of operations to
    // place largest element at the last
    count += (n - 1 - index_min);

    // If smallest element is present
    // before the largest element initially
    if (index_min < index_max)
        count -= 1;

    return count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 1, 6, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minimum_swaps(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
import java.util.Collections;

class GFG{

// Function to find the minimum number
// of swaps required to make the first
// and the last elements the largest
// and smallest element in the array
static int minimum_swaps(Integer arr[], int n)
{

    // Stores the count of swaps
    int count = 0;

    // Stores the maximum element
    int max_el = Collections.max(Arrays.asList(arr));

    // Stores the minimum element
    int min_el = Collections.min(Arrays.asList(arr));

    // If the array contains
    // a single distinct element
    if (min_el == max_el)
        return 0;

    // Stores the indices of the
    // maximum and minimum elements
    int index_max = -1;
    int index_min = -1;

    for(int i = 0; i < n; i++)
    {

        // If the first index of the
        // maximum element is found
        if (arr[i] == max_el &&
            index_max == -1)
        {
            index_max = i;
        }

        // If current index has
        // the minimum element
        if (arr[i] == min_el)
        {
            index_min = i;
        }
    }

    // Update the count of operations to
    // place largest element at the first
    count += index_max;

    // Update the count of operations to
    // place largest element at the last
    count += (n - 1 - index_min);

    // If smallest element is present
    // before the largest element initially
    if (index_min < index_max)
        count -= 1;

    return count;
}

// Driver Code
public static void main (String[] args)
{
    Integer arr[] = { 2, 4, 1, 6, 5 };
    int N = arr.length;

    System.out.println(minimum_swaps(arr, N));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of swaps required to make the first
# and the last elements the largest
# and smallest element in the array
def minimum_swaps(arr, n):

    # Stores the count of swaps
    count = 0

    # Stores the maximum element
    max_el = max(arr)

    # Stores the minimum element
    min_el = min(arr)

    # If the array contains
    # a single distinct element
    if (min_el == max_el):
        return 0

    # Stores the indices of the
    # maximum and minimum elements
    index_max = -1
    index_min = -1

    for i in range(n):

        # If the first index of the
        # maximum element is found
        if (arr[i] == max_el and
            index_max == -1):
            index_max = i

        # If current index has
        # the minimum element
        if (arr[i] == min_el):
            index_min = i

    # Update the count of operations to
    # place largest element at the first
    count += index_max

    # Update the count of operations to
    # place largest element at the last
    count += (n - 1 - index_min)

    # If smallest element is present
    # before the largest element initially
    if (index_min < index_max):
        count -= 1

    return count

# Driver Code
if __name__ == '__main__':

    arr = [2, 4, 1, 6, 5]
    N = len(arr)

    print(minimum_swaps(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

class GFG{

// Function to find the minimum number
// of swaps required to make the first
// and the last elements the largest
// and smallest element in the array
static int minimum_swaps(int[] arr, int n)
{

    // Stores the count of swaps
    int count = 0;

    // Stores the maximum element
    int max_el = arr.Max();

    // Stores the minimum element
    int min_el = arr.Min();

    // If the array contains
    // a single distinct element
    if (min_el == max_el)
        return 0;

    // Stores the indices of the
    // maximum and minimum elements
    int index_max = -1;
    int index_min = -1;

    for(int i = 0; i < n; i++)
    {

        // If the first index of the
        // maximum element is found
        if (arr[i] == max_el &&
            index_max == -1)
        {
            index_max = i;
        }

        // If current index has
        // the minimum element
        if (arr[i] == min_el)
        {
            index_min = i;
        }
    }

    // Update the count of operations to
    // place largest element at the first
    count += index_max;

    // Update the count of operations to
    // place largest element at the last
    count += (n - 1 - index_min);

    // If smallest element is present
    // before the largest element initially
    if (index_min < index_max)
        count -= 1;

    return count;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 2, 4, 1, 6, 5 };
    int N = arr.Length;

    Console.WriteLine(minimum_swaps(arr, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find the minimum number
      // of swaps required to make the first
      // and the last elements the largest
      // and smallest element in the array
      function minimum_swaps(arr, n) {
        // Stores the count of swaps
        var count = 0;

        // Stores the maximum element
        var max_el = Math.max(...arr);

        // Stores the minimum element
        var min_el = Math.min(...arr);

        // If the array contains
        // a single distinct element
        if (min_el === max_el) return 0;

        // Stores the indices of the
        // maximum and minimum elements
        var index_max = -1;
        var index_min = -1;

        for (var i = 0; i < n; i++) {
          // If the first index of the
          // maximum element is found
          if (arr[i] === max_el && index_max === -1) {
            index_max = i;
          }

          // If current index has
          // the minimum element
          if (arr[i] === min_el) {
            index_min = i;
          }
        }

        // Update the count of operations to
        // place largest element at the first
        count += index_max;

        // Update the count of operations to
        // place largest element at the last
        count += n - 1 - index_min;

        // If smallest element is present
        // before the largest element initially
        if (index_min < index_max) count -= 1;

        return count;
      }

      // Driver Code
      var arr = [2, 4, 1, 6, 5];
      var N = arr.length;

      document.write(minimum_swaps(arr, N));
    </script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)