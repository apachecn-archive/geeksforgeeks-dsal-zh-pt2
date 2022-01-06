# 相邻元素间差异之和最大的字典最小排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-最小排列-相邻元素之间的差异之和最大/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-having-maximum-sum-of-differences-between-adjacent-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定数组的字典上最小的[排列，使得相邻元素之间的差之和最大。](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 5 2 3 4 1
> **解释:**
> 相邻元素之差之和=(5–2)+(2–3)+(3–4)+(4–1)= 4。
> {5，2，3，4，1}是字典上最小的数组，4 是可能的最大和。
> 
> **输入:** arr[] = {3，4，1}
> **输出:** 4 3 1
> **解释:**
> 相邻元素之差之和=(4–3)+(3–1)= 3
> { 4，3，1}是可能的数组元素的字典最小排列。相邻元素的最大可能和为 3。

**天真方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)的所有排列，并在跟踪获得的最大和的同时，找到每个排列的和。最后，用最大和打印字典上最小的排列。

***时间复杂度:** O(N * N！)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 让数组所需的排列为{p <sub>1</sub> ，p <sub>2</sub> ，p <sub>3</sub> ，…，p<sub>N–2</sub>，p<sub>N–1，</sub> p <sub>N</sub> }。
> 相邻元素之差之和，S =(p<sub>1</sub>-p<sub>2</sub>)+(p<sub>2</sub>-p<sub>3</sub>)+…。+(p<sub>N–2</sub>–p<sub>N–1</sub>)+(p<sub>N–1</sub>–p<sub>N</sub>)
> = p<sub>1</sub>–p<sub>N</sub>

为了最大化 **S** ，**p<sub>1</sub>T5】应该是给定数组中最大的元素， **p <sub>N</sub>** 应该是最小的元素 **arr[]** 。要构建字典上最小的排列，请按升序排列其余元素。按照以下步骤解决问题:**

*   [按升序排列数组 **arr[]** 。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   [交换](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)第一个数组元素，即**a【0】**和最后一个数组元素，即**arr【N–1】**。
*   完成以上步骤后，打印修改后的数组 **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest permutation of an array such
// that the sum of the difference between
// adjacent elements is maximum
void maximumSumPermutation(vector<int>& arr)
{

    // Stores the size of the array
    int N = arr.size();

    // Sort the given array in
    // increasing order
    sort(arr.begin(), arr.end());

    // Swap the first and last array elements
    swap(arr[0], arr[N - 1]);

    // Print the required permutation
    for (int i : arr) {

        cout << i << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 3, 4, 5 };
    maximumSumPermutation(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to find the lexicographically
    // smallest permutation of an array such
    // that the sum of the difference between
    // adjacent elements is maximum
    static void maximumSumPermutation(int[] arr)
    {

        // Stores the size of the array
        int N = arr.length;

        // Sort the given array in
        // increasing order
        Arrays.sort(arr);

        // Swap the first and last array elements
          int temp = arr[0];
          arr[0] = arr[N - 1];
        arr[N - 1] = temp;

        // Print the required permutation
        for (int i : arr) {

            System.out.print(i + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        maximumSumPermutation(arr);
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the lexicographically
# smallest permutation of an array such
# that the sum of the difference between
# adjacent elements is maximum
def maximumSumPermutation(arr):

    # Stores the size of the array
    N = len(arr);

    # Sort the given array in
    # increasing order
    arr.sort();

    # Swap the first and last array elements
    temp = arr[0];
    arr[0] = arr[N - 1];
    arr[N - 1] = temp;

    # Print the required permutation
    for i in arr:
        print(i, end = " ");

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5];
    maximumSumPermutation(arr);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

  // Function to find the lexicographically
  // smallest permutation of an array such
  // that the sum of the difference between
  // adjacent elements is maximum
  static void maximumSumPermutation(int[] arr)
  {

    // Stores the size of the array
    int N = arr.Length;

    // Sort the given array in
    // increasing order
    Array.Sort(arr);

    // Swap the first and last array elements
    int temp = arr[0];
    arr[0] = arr[N - 1];
    arr[N - 1] = temp;

    // Print the required permutation
    foreach (int i in arr)
    {
      Console.Write(i + " ");
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 1, 2, 3, 4, 5 };
    maximumSumPermutation(arr);
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to find the lexicographically
// smallest permutation of an array such
// that the sum of the difference between
// adjacent elements is maximum
function maximumSumPermutation(arr)
{

    // Stores the size of the array
    var N = arr.length;
    // Sort the given array in
    // increasing order
    arr.sort((a,b)=>a-b);
    // Swap the first and last array elements
      var temp = arr[0];
      arr[0] = arr[N - 1];
      arr[N - 1] = temp;

    // Prvar the required permutation
    document.write(arr);
}

// Driver Code
var arr = [ 1, 2, 3, 4, 5 ];
maximumSumPermutation(arr);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
5 2 3 4 1
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*