# 最大化给定数组可拆分成的子集的数量，使其满足给定条件

> 原文:[https://www . geeksforgeeks . org/给定数组可拆分到的子集数量最大化，以满足给定条件/](https://www.geeksforgeeks.org/maximize-count-of-subsets-into-which-the-given-array-can-be-split-such-that-it-satisfies-the-given-condition/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个正整数 **X** ，任务是将数组划分为最大数量的子集，使得每个子集的最小元素与子集内元素的计数的乘积大于或等于 **K** 。打印此类子集的最大数量。

**示例:**

> **输入:** arr[] = {1，3，3，7}，X = 3
> **输出:** 3
> **解释:**将数组划分为 3 个子集{ {1，3}、{3}、{7} }。因此，所需的输出为 3。
> 
> **输入:** arr[] = {2，4，2，5，1}，X = 2
> T3】输出: 4

**方法:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   [按降序排列数组元素](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并跟踪当前子集的大小
*   由于数组是按降序排序的，子集最右边的元素将是当前划分的最小元素。
*   因此，如果**(当前子集的大小*当前元素)**大于或等于 **X** ，则增加计数并将当前分区的大小重置为 **0** 。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count maximum subsets into
// which the given array can be split such
// that it satisfies the given condition
void maxDivisions(int arr[], int N, int X)
{

    // Sort the array in decreasing order
    sort(arr, arr + N, greater<int>());

    // Stores count of subsets possible
    int maxSub = 0;

    // Stores count of elements
    // in current subset
    int size = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Update size
        size++;

        // If product of the smallest element
        // present in the current subset and
        // size of current subset is >= K
        if (arr[i] * size >= X) {

            // Update maxSub
            maxSub++;

            // Update size
            size = 0;
        }
    }

    cout << maxSub << endl;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 3, 3, 7 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of X
    int X = 3;

    maxDivisions(arr, N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to count maximum subsets into
// which the given array can be split such
// that it satisfies the given condition
static void maxDivisions(Integer arr[], int N, int X)
{

    // Sort the array in decreasing order
    Arrays.sort(arr,Collections.reverseOrder());

    // Stores count of subsets possible
    int maxSub = 0;

    // Stores count of elements
    // in current subset
    int size = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Update size
        size++;

        // If product of the smallest element
        // present in the current subset and
        // size of current subset is >= K
        if (arr[i] * size >= X)
        {

            // Update maxSub
            maxSub++;

            // Update size
            size = 0;
        }
    }
    System.out.print(maxSub +"\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    Integer arr[] = { 1, 3, 3, 7 };

    // Size of the array
    int N = arr.length;

    // Given value of X
    int X = 3;
    maxDivisions(arr, N, X);

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count maximum subsets into
# which the given array can be split such
# that it satisfies the given condition
def maxDivisions(arr, N, X) :

    # Sort the array in decreasing order
    arr.sort(reverse = True)

    # Stores count of subsets possible
    maxSub = 0;

    # Stores count of elements
    # in current subset
    size = 0;

    # Traverse the array arr[]
    for i in range(N) :

        # Update size
        size += 1;

        # If product of the smallest element
        # present in the current subset and
        # size of current subset is >= K
        if (arr[i] * size >= X) :

            # Update maxSub
            maxSub += 1;

            # Update size
            size = 0;
    print(maxSub);

# Driver Code
if __name__ == "__main__" :

    # Given array
    arr = [ 1, 3, 3, 7 ];

    # Size of the array
    N = len(arr);

    # Given value of X
    X = 3;

    maxDivisions(arr, N, X);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to count maximum subsets into
  // which the given array can be split such
  // that it satisfies the given condition
  static void maxDivisions(int[] arr, int N, int X)
  {

    // Sort the array in decreasing order
    Array.Sort(arr);
    Array.Reverse(arr);

    // Stores count of subsets possible
    int maxSub = 0;

    // Stores count of elements
    // in current subset
    int size = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

      // Update size
      size++;

      // If product of the smallest element
      // present in the current subset and
      // size of current subset is >= K
      if (arr[i] * size >= X)
      {

        // Update maxSub
        maxSub++;

        // Update size
        size = 0;
      }
    }

    Console.WriteLine(maxSub);
  }

  // Driver Code
  public static void Main()
  {

    // Given array
    int[] arr = { 1, 3, 3, 7 };

    // Size of the array
    int N = arr.Length;

    // Given value of X
    int X = 3;
    maxDivisions(arr, N, X);
  }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function to count maximum subsets into
// which the given array can be split such
// that it satisfies the given condition
function maxDivisions(arr, N, X)
{

    // Sort the array in decreasing order
    arr.sort();

    // Stores count of subsets possible
    let maxSub = 0;

    // Stores count of elements
    // in current subset
    let size = 0;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++)
    {

        // Update size
        size++;

        // If product of the smallest element
        // present in the current subset and
        // size of current subset is >= K
        if (arr[i] * size >= X)
        {

            // Update maxSub
            maxSub++;

            // Update size
            size = 0;
        }
    }
    document.write(maxSub + "<br/>");
}

    // Driver Code

    // Given array
    let arr = [ 1, 3, 3, 7 ];

    // Size of the array
    let N = arr.length;

    // Given value of X
    let X = 3;
    maxDivisions(arr, N, X);

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*