# 从两个差值超过 K 的数组中计数对

> 原文:[https://www . geesforgeks . org/count-pairs-from-two-array-different-exclusive-k/](https://www.geeksforgeeks.org/count-pairs-from-two-arrays-with-difference-exceeding-k/)

给定两个整数[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和**brr【】**分别由大小为 **N** 和 **M** 的不同元素和一个整数 **K** 组成，任务是找到对的计数 **(arr[i]，brr[j])** ，使得**(brr[j]–arr[I])>K**。

**示例:**

> **输入:** arr[] = {5，9，1，8}，brr[] {10，12，7，4，2，3}，K = 3
> **输出:** 6
> **说明:**
> 满足给定条件的可能对有:{ (5，10)，(5，12)，(1，10)，(1，12)，(1，7)，(8，12) }。
> 因此，要求输出为 6。
> 
> **输入:** arr[] = {2，10}，brr[] = {5，7}，K = 2
> **输出:** 2
> **解释:**
> 满足给定条件的可能对为:{ (2，5)，(2，7) }。
> 因此，要求的输出为 2。

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，对于每一对，检查**(brr[j]–arr[I])>K**是否存在。如果发现为真，则递增计数器。最后，打印计数器的值。

***时间复杂度:** O(N × M)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是首先[对数组](https://www.geeksforgeeks.org/sort-c-stl/)进行排序，然后使用[两个指针技术](https://www.geeksforgeeks.org/tag/two-pointer-algorithm/)。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntPairs** 来存储满足给定条件的对的计数。
*   [给定数组排序](https://www.geeksforgeeks.org/sort-c-stl/)。
*   初始化两个变量，比如说 **i = 0** 和 **j = 0** 分别存储左右指针的索引。
*   [遍历两个数组](https://www.geeksforgeeks.org/array-data-structure/)并检查**(brr[j]–arr[I])>K**是否存在。如果发现为真，则更新**cntPairs+=(M–j)**的值，并增加 **i** 指针变量的值。
*   否则，增加 **j** 指针变量的值。
*   最后，打印**的值，打印**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs that satisfy
// the given conditions
int count_pairs(int arr[], int brr[],
                int N, int M, int K)
{
    // Stores index of
    // the left pointer.
    int i = 0;

    // Stores index of
    // the right pointer
    int j = 0;

    // Stores count of total pairs
    // that satisfy the conditions
    int cntPairs = 0;

    // Sort arr[] array
    sort(arr, arr + N);

    // Sort brr[] array
    sort(brr, brr + M);

    // Traverse both the array
    // and count then pairs
    while (i < N && j < M) {

        // If the value of
        // (brr[j] - arr[i]) exceeds K
        if (brr[j] - arr[i] > K) {

            // Update cntPairs
            cntPairs += (M - j);

            // Update
            i++;
        }
        else {

            // Update j
            j++;
        }
    }

    return cntPairs;
}

// Driver Code
int main()
{
    int arr[] = { 5, 9, 1, 8 };
    int brr[] = { 10, 12, 7, 4, 2, 3 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(brr) / sizeof(brr[0]);
    cout << count_pairs(arr, brr, N, M, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count pairs that satisfy
// the given conditions
static int count_pairs(int arr[], int brr[],
                       int N, int M, int K)
{

    // Stores index of
    // the left pointer.
    int i = 0;

    // Stores index of
    // the right pointer
    int j = 0;

    // Stores count of total pairs
    // that satisfy the conditions
    int cntPairs = 0;

    // Sort arr[] array
    Arrays.sort(arr);

    // Sort brr[] array
    Arrays.sort(brr);

    // Traverse both the array
    // and count then pairs
    while (i < N && j < M)
    {

        // If the value of
        // (brr[j] - arr[i]) exceeds K
        if (brr[j] - arr[i] > K)
        {

            // Update cntPairs
            cntPairs += (M - j);

            // Update
            i++;
        }
        else
        {

            // Update j
            j++;
        }
    }
    return cntPairs;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 5, 9, 1, 8 };
    int brr[] = { 10, 12, 7, 4, 2, 3 };
    int K = 3;

    int N = arr.length;
    int M = brr.length;

    System.out.println(count_pairs(arr, brr, N, M, K));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count pairs that satisfy
# the given conditions
def count_pairs(arr, brr, N, M, K):

    # Stores index of
    # the left pointer.
    i = 0

    # Stores index of
    # the right pointer
    j = 0

    # Stores count of total pairs
    # that satisfy the conditions
    cntPairs = 0

    # Sort arr[] array
    arr = sorted(arr)

    # Sort brr[] array
    brr = sorted(brr)

    # Traverse both the array
    # and count then pairs
    while (i < N and j < M):

        # If the value of
        # (brr[j] - arr[i]) exceeds K
        if (brr[j] - arr[i] > K):

            # Update cntPairs
            cntPairs += (M - j)

            # Update
            i += 1
        else:

            # Update j
            j += 1

    return cntPairs

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 9, 1, 8 ]
    brr = [ 10, 12, 7, 4, 2, 3 ]
    K = 3

    N = len(arr)
    M = len(brr)

    print(count_pairs(arr, brr, N, M, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to count pairs
// that satisfy the given
// conditions
static int count_pairs(int[] arr, int[] brr,
                       int N, int M, int K)
{
  // Stores index of
  // the left pointer.
  int i = 0;

  // Stores index of
  // the right pointer
  int j = 0;

  // Stores count of total pairs
  // that satisfy the conditions
  int cntPairs = 0;

  // Sort arr[] array
  Array.Sort(arr);

  // Sort brr[] array
  Array.Sort(brr);

  // Traverse both the array
  // and count then pairs
  while (i < N && j < M)
  {
    // If the value of
    // (brr[j] - arr[i])
    // exceeds K
    if (brr[j] - arr[i] > K)
    {
      // Update cntPairs
      cntPairs += (M - j);

      // Update
      i++;
    }
    else
    {
      // Update j
      j++;
    }
  }
  return cntPairs;
}

// Driver code 
static void Main()
{
  int[] arr = {5, 9, 1, 8};
  int[] brr = {10, 12,
               7, 4, 2, 3};
  int K = 3;
  int N = arr.Length;
  int M = brr.Length;
  Console.WriteLine(
  count_pairs(arr, brr,
              N, M, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to count pairs that satisfy
// the given conditions
function count_pairs(arr, brr, N, M, K)
{

    // Stores index of
    // the left pointer.
    let i = 0;

    // Stores index of
    // the right pointer
    let j = 0;

    // Stores count of total pairs
    // that satisfy the conditions
    let cntPairs = 0;

    // Sort arr[] array
    (arr).sort(function(a,b){return a-b;});

    // Sort brr[] array
    (brr).sort(function(a,b){return a-b;});

    // Traverse both the array
    // and count then pairs
    while (i < N && j < M)
    {

        // If the value of
        // (brr[j] - arr[i]) exceeds K
        if (brr[j] - arr[i] > K)
        {

            // Update cntPairs
            cntPairs += (M - j);

            // Update
            i++;
        }
        else
        {

            // Update j
            j++;
        }
    }
    return cntPairs;
}

// Driver Code
let arr = [5, 9, 1, 8];
let brr = [ 10, 12, 7, 4, 2, 3];
let K = 3;
let N = arr.length;
let M = brr.length;
document.write(count_pairs(arr, brr, N, M, K));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N * log(N)+M * log(M))*
***辅助空间:** O(1)*