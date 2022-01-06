# 交换可能产生的字典上最大的置换，小于给定的数组

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大可能置换比给定数组小/](https://www.geeksforgeeks.org/lexicographically-largest-permutation-possible-by-a-swap-that-is-smaller-than-a-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过恰好一次交换找到给定数组的字典式[最大置换，该置换小于给定数组。如果有可能获得这样的排列，那么打印该排列。否则，打印**-1”**。](https://www.geeksforgeeks.org/largest-permutation-k-swaps/)

**示例:**

> **输入:** arr[] = {5，4，3，2，1}
> **输出:** 5 4 3 1 2
> **解释:**
> *从字典上讲，*比给定数组小的最大排列可以通过交换 2 和 1 来形成。
> 因此，结果排列是{5，4，3，1，2}
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** -1

**方法:**给定的问题可以通过找到大于其下一个元素的最后一个元素，并将其与数组中的[下一个较小的元素交换来解决。按照以下步骤解决问题:](https://www.geeksforgeeks.org/next-smaller-element/)

*   如果给定的[数组是按照升序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)排序的，那么打印**-1”**，因为不可能在字典中找到给定数组中比给定数组小的[最大排列。](https://www.geeksforgeeks.org/largest-permutation-k-swaps/)
*   [从最后](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)遍历给定的数组，找到那个索引，比如说 **idx** ，它严格大于下一个元素。
*   现在，再次[从末尾遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，找到第一个元素的索引(比如说 **j** ，它更小，元素**arr【idx】**。
*   减小 **j** 的值直到**arr【j–1】**与**arr【j】**相同。
*   [交换数组**arr【】**中索引 **idx** 和 **j** 处的元素](https://www.geeksforgeeks.org/python-program-to-swap-two-elements-in-a-list/)以获得结果排列。
*   完成上述步骤后，打印数组作为结果排列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to lexicographic largest
// permutation possible by a swap
// that is smaller than given array
void findPermutation(vector<int>& arr)
{
    int N = arr.size();
    int i = N - 2;

    // Find the index of first element
    // such that arr[i] > arr[i + 1]
    while (i >= 0 && arr[i] <= arr[i + 1])
        i--;

    // If the array is sorted
    // in increasing order
    if (i == -1) {
        cout << "-1";
        return;
    }

    int j = N - 1;

    // Find the index of first element
    // which is smaller than arr[i]
    while (j > i && arr[j] >= arr[i])
        j--;

    // If arr[j] == arr[j-1]
    while (j > i && arr[j] == arr[j - 1]) {

        // Decrement j
        j--;
    }

    // Swap the element
    swap(arr[i], arr[j]);

    // Print the array arr[]
    for (auto& it : arr) {
        cout << it << ' ';
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 5, 3, 4, 6 };
    findPermutation(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.util.*;
class GFG{

// Function to lexicographic largest
// permutation possible by a swap
// that is smaller than given array
static void findPermutation(int[] arr)
{
    int N = arr.length;
    int i = N - 2;

    // Find the index of first element
    // such that arr[i] > arr[i + 1]
    while (i >= 0 && arr[i] <= arr[i + 1])
        i--;

    // If the array is sorted
    // in increasing order
    if (i == -1)
    {
         System.out.print("-1");
        return;
    }

    int j = N - 1;

    // Find the index of first element
    // which is smaller than arr[i]
    while (j > i && arr[j] >= arr[i])
        j--;

    // If arr[j] == arr[j-1]
    while (j > i && arr[j] == arr[j - 1])
    {

        // Decrement j
        j--;
    }

    // Swap the element
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;

    // Print the array arr[]
    for(int it : arr)
    {
        System.out.print(it + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 5, 3, 4, 6 };
    findPermutation(arr);
}
}

// This code is contributed by splevel62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to lexicographic largest
// permutation possible by a swap
// that is smaller than given array
static void findPermutation(int[] arr)
{
    int N = arr.Length;
    int i = N - 2;

    // Find the index of first element
    // such that arr[i] > arr[i + 1]
    while (i >= 0 && arr[i] <= arr[i + 1])
        i--;

    // If the array is sorted
    // in increasing order
    if (i == -1)
    {
        Console.Write("-1");
        return;
    }

    int j = N - 1;

    // Find the index of first element
    // which is smaller than arr[i]
    while (j > i && arr[j] >= arr[i])
        j--;

    // If arr[j] == arr[j-1]
    while (j > i && arr[j] == arr[j - 1])
    {

        // Decrement j
        j--;
    }

    // Swap the element
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;

    // Print the array arr[]
    foreach(int it in arr)
    {
        Console.Write(it + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 5, 3, 4, 6 };
    findPermutation(arr);
}
}

// This code is contributed by ukasp
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to lexicographic largest
# permutation possible by a swap
# that is smaller than given array
def findPermutation(arr):

    N = len(arr)
    i = N - 2

    # Find the index of first element
    # such that arr[i] > arr[i + 1]
    while (i >= 0 and arr[i] <= arr[i + 1]):
        i -= 1

    # If the array is sorted
    # in increasing order
    if (i == -1) :
        print("-1")
        return

    j = N - 1

    # Find the index of first element
    # which is smaller than arr[i]
    while (j > i and arr[j] >= arr[i]):
        j -= 1

    # If arr[j] == arr[j-1]
    while (j > i and arr[j] == arr[j - 1]) :

        # Decrement j
        j -= 1

    # Swap the element
    temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;

    # Pr the array arr[]
    for it in arr :
        print(it, end = " ")

# Driver Code
arr =  [ 1, 2, 5, 3, 4, 6 ]
findPermutation(arr)

# This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to lexicographic largest
// permutation possible by a swap
// that is smaller than given array
function findPermutation(arr)
{
    let N = arr.length;
    let i = N - 2;

    // Find the index of first element
    // such that arr[i] > arr[i + 1]
    while (i >= 0 && arr[i] <= arr[i + 1])
        i--;

    // If the array is sorted
    // in increasing order
    if (i == -1)
    {
        document.write("-1");
        return;
    }

    let j = N - 1;

    // Find the index of first element
    // which is smaller than arr[i]
    while (j > i && arr[j] >= arr[i])
        j--;

    // If arr[j] == arr[j-1]
    while (j > i && arr[j] == arr[j - 1])
    {
        // Decrement j
        j--;
    }

    // Swap the element
    let temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;

    // Print the array arr[]
    for(let it in arr)
    {
        document.write(arr[it] + " ");
    }
}

// Driver Code

    let arr = [ 1, 2, 5, 3, 4, 6 ];
    findPermutation(arr);

</script>
```

**Output:** 

```
1 2 4 3 5 6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)