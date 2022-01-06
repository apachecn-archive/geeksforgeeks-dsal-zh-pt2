# 对给定数组中的对(I，j)进行计数，使得 i K * arr[j]

> 原文:[https://www . geesforgeks . org/count-pairs-I-j-from-给定数组-so-I-j-and-arri-k-arrj/](https://www.geeksforgeeks.org/count-pairs-i-j-from-given-array-such-that-i-j-and-arri-k-arrj/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是计算对 **(i，j)** 的数量，使得 **i < j** 和**arr【I】>K * arr【j】**。

**示例:**

> **输入:** arr[] = {5，6，2，5}，K = 2
> **输出:** 2
> **说明:**数组由两个这样的对组成:
> (5，2):索引 5 和 2 分别为 0，2。因此，满足要求的条件(0 < 2 和 5 > 2 * 2)。
> (6，2):6 和 2 的指数分别为 1，2。因此，满足要求的条件(0 < 2 和 6 > 2 * 2)。
> 
> **输入:** arr[] = {4，6，5，1}，K = 2
> T3】输出: 3

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个索引，找到索引大于它的数字，这样当乘以 **K** 时，其中的元素小于当前索引处的元素。

按照以下步骤解决问题:

1.  初始化一个变量，比如说 **cnt** ，用 **0** 来计算所需对的总数。
2.  [从左到右遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
3.  对于每个可能的索引，假设 **i** ，遍历索引 **i + 1** 到**N–1**，并将 **cnt** 的值增加 **1** 如果发现任何元素，假设 arr[j]，使得 **arr[j] * K** 小于 **arr[i]** 。
4.  完成数组遍历后，打印 **cnt** 作为所需的对数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count required pairs
int getPairs(int arr[], int N, int K)
{
    // Stores count of pairs
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        for (int j = i + 1; j < N; j++) {

            // Check if the condition
            // is satisfied or not
            if (arr[i] > K * arr[i + 1])
                count++;
        }
    }
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 5, 6, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    // Function Call
    getPairs(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to find the count required pairs
static void getPairs(int arr[], int N, int K)
{
    // Stores count of pairs
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {

            // Check if the condition
            // is satisfied or not
            if (arr[i] > K * arr[i + 1])
                count++;
        }
    }
    System.out.print(count);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 6, 2, 1 };
    int N = arr.length;
    int K = 2;

    // Function Call
    getPairs(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the count required pairs
def getPairs(arr, N, K):

    # Stores count of pairs
    count = 0

    # Traverse the array
    for i in range(N):
        for j in range(i + 1, N):

            # Check if the condition
            # is satisfied or not
            if (arr[i] > K * arr[i + 1]):
                count += 1

    print(count)

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 6, 2, 1 ]
    N   = len(arr)
    K = 2

    # Function Call
    getPairs(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to find the count required pairs
static void getPairs(int []arr, int N, int K)
{
    // Stores count of pairs
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {

            // Check if the condition
            // is satisfied or not
            if (arr[i] > K * arr[i + 1])
                count++;
        }
    }
    Console.Write(count);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 5, 6, 2, 1 };
    int N = arr.Length;
    int K = 2;

    // Function Call
    getPairs(arr, N, K);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the count required pairs
function getPairs(arr, N, K)
{

    // Stores count of pairs
    let count = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {
        for(let j = i + 1; j < N; j++)
        {

            // Check if the condition
            // is satisfied or not
            if (arr[i] > K * arr[i + 1])
                count++;
        }
    }
    document.write(count);
}

// Driver Code
let arr = [ 5, 6, 2, 1 ];
let N = arr.length;
let K = 2;

// Function Call
getPairs(arr, N, K);

// This code is contributed by splevel62

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效途径:**思路是利用[的概念合并排序](https://www.geeksforgeeks.org/merge-sort/)，然后根据给定的条件进行配对计数。按照以下步骤解决问题:

*   初始化一个变量，说**回答**，计算满足给定条件的对的数量。
*   重复地将数组分成两等份或几乎等份，直到每个分区中剩下一个元素。
*   调用递归函数，计算合并两个分区后满足条件 **arr[i] > K * arr[j]** 和 **i < j** 的次数。
*   通过初始化两个变量来执行，分别为前半部分和后半部分的指数设置 **i** 和 **j** 。
*   增加 **j** 直到**arr【I】>K * arr【j】**和 **j <尺寸**的后半部分。在**答案**中添加**(j –( mid+1))**，并增加 **i** 。
*   完成上述步骤后，打印**答案**的值作为所需的对数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to merge two sorted arrays
int merge(int arr[], int temp[],
          int l, int m, int r, int K)
{
    // i: index to left subarray
    int i = l;

    // j: index to right subarray
    int j = m + 1;

    // Stores count of pairs that
    // satisfy the given condition
    int cnt = 0;

    for (int l = 0; i <= m; i++) {
        bool found = false;

        // Traverse to check for the
        // valid conditions
        while (j <= r) {

            // If condition satisfies
            if (arr[i] >= K * arr[j]) {
                found = true;
            }
            else
                break;
            j++;
        }

        // While a[i] > K*a[j] satisfies
        // increase j

        // All elements in the right
        // side of the left subarray
        // also satisfies
        if (found) {
            cnt += j - (m + 1);
            j--;
        }
    }

    // Sort the two given arrays and
    // store in the resultant array
    int k = l;
    i = l;
    j = m + 1;

    while (i <= m && j <= r) {

        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
            temp[k++] = arr[j++];
    }

    // Elements which are left
    // in the left subarray
    while (i <= m)
        temp[k++] = arr[i++];

    // Elements which are left
    // in the right subarray
    while (j <= r)
        temp[k++] = arr[j++];

    for (int i = l; i <= r; i++)
        arr[i] = temp[i];

    // Return the count obtained
    return cnt;
}

// Function to partition array into two halves
int mergeSortUtil(int arr[], int temp[],
                  int l, int r, int K)
{
    int cnt = 0;
    if (l < r) {

        // Same as (l + r) / 2, but avoids
        // overflow for large l and h
        int m = (l + r) / 2;

        // Sort first and second halves
        cnt += mergeSortUtil(arr, temp,
                             l, m, K);
        cnt += mergeSortUtil(arr, temp,
                             m + 1, r, K);

        // Call the merging function
        cnt += merge(arr, temp, l,
                     m, r, K);
    }

    return cnt;
}

// Function to print the count of
// required pairs using Merge Sort
int mergeSort(int arr[], int N, int K)
{
    int temp[N];

    cout << mergeSortUtil(arr, temp, 0,
                          N - 1, K);
}

// Driver code
int main()
{
    int arr[] = { 5, 6, 2, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    // Function Call
    mergeSort(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to merge two sorted arrays
    static int merge(int arr[], int temp[],
              int l, int m, int r, int K)
    {

        // i: index to left subarray
        int i = l;

        // j: index to right subarray
        int j = m + 1;

        // Stores count of pairs that
        // satisfy the given condition
        int cnt = 0;

        for (i = l; i <= m; i++)
        {
            boolean found = false;

            // Traverse to check for the
            // valid conditions
            while (j <= r)
            {

                // If condition satisfies
                if (arr[i] >= K * arr[j])
                {
                    found = true;
                }
                else
                    break;
                j++;
            }

            // While a[i] > K*a[j] satisfies
            // increase j

            // All elements in the right
            // side of the left subarray
            // also satisfies
            if (found == true)
            {
                cnt += j - (m + 1);
                j--;
            }
        }

        // Sort the two given arrays and
        // store in the resultant array
        int k = l;
        i = l;
        j = m + 1;

        while (i <= m && j <= r)
        {

            if (arr[i] <= arr[j])
                temp[k++] = arr[i++];
            else
                temp[k++] = arr[j++];
        }

        // Elements which are left
        // in the left subarray
        while (i <= m)
            temp[k++] = arr[i++];

        // Elements which are left
        // in the right subarray
        while (j <= r)
            temp[k++] = arr[j++];

        for (i = l; i <= r; i++)
            arr[i] = temp[i];

        // Return the count obtained
        return cnt;
    }

    // Function to partition array into two halves
    static int mergeSortUtil(int arr[], int temp[],
                      int l, int r, int K)
    {
        int cnt = 0;
        if (l < r)
        {

            // Same as (l + r) / 2, but avoids
            // overflow for large l and h
            int m = (l + r) / 2;

            // Sort first and second halves
            cnt += mergeSortUtil(arr, temp,
                                 l, m, K);
            cnt += mergeSortUtil(arr, temp,
                                 m + 1, r, K);

            // Call the merging function
            cnt += merge(arr, temp, l,
                         m, r, K);
        }   
        return cnt;
    }

    // Function to print the count of
    // required pairs using Merge Sort
    static void mergeSort(int arr[], int N, int K)
    {
        int temp[] = new int[N];
        System.out.print(mergeSortUtil(arr, temp, 0, N - 1, K));
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 5, 6, 2, 5 };
        int N = arr.length;
        int K = 2;

        // Function Call
        mergeSort(arr, N, K);   
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to merge two sorted arrays
def merge(arr, temp, l, m, r, K) :

    # i: index to left subarray
    i = l

    # j: index to right subarray
    j = m + 1

    # Stores count of pairs that
    # satisfy the given condition
    cnt = 0
    for l in range(m + 1) :
        found = False

        # Traverse to check for the
        # valid conditions
        while (j <= r) :

            # If condition satisfies
            if (arr[i] >= K * arr[j]) :
                found = True        
            else :
                break
            j += 1

        # While a[i] > K*a[j] satisfies
        # increase j

        # All elements in the right
        # side of the left subarray
        # also satisfies
        if (found) :
            cnt += j - (m + 1)
            j -= 1

    # Sort the two given arrays and
    # store in the resultant array
    k = l
    i = l
    j = m + 1

    while (i <= m and j <= r) :
        if (arr[i] <= arr[j]) :
            temp[k] = arr[i]
            k += 1
            i += 1
        else :
            temp[k] = arr[j]
            k += 1
            j += 1

    # Elements which are left
    # in the left subarray
    while (i <= m) :
        temp[k] = arr[i]
        k += 1
        i += 1

    # Elements which are left
    # in the right subarray
    while (j <= r) :
        temp[k] = arr[j]
        k += 1
        j += 1
    for i in range(l, r + 1) :
        arr[i] = temp[i]

    # Return the count obtained
    return cnt

# Function to partition array into two halves
def mergeSortUtil(arr, temp, l, r, K) :
    cnt = 0
    if (l < r) :

        # Same as (l + r) / 2, but avoids
        # overflow for large l and h
        m = (l + r) // 2

        # Sort first and second halves
        cnt += mergeSortUtil(arr, temp, l, m, K)
        cnt += mergeSortUtil(arr, temp, m + 1, r, K)

        # Call the merging function
        cnt += merge(arr, temp, l, m, r, K)
    return cnt

# Function to print the count of
# required pairs using Merge Sort
def mergeSort(arr, N, K) :
    temp = [0]*N
    print(mergeSortUtil(arr, temp, 0, N - 1, K))

  # Driver code
arr = [ 5, 6, 2, 5 ]
N = len(arr)
K = 2

# Function Call
mergeSort(arr, N, K)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

  // Function to merge two sorted arrays
  static int merge(int[] arr, int[] temp, int l, int m,
                   int r, int K)
  {

    // i: index to left subarray
    int i = l;

    // j: index to right subarray
    int j = m + 1;

    // Stores count of pairs that
    // satisfy the given condition
    int cnt = 0;

    for (i = l; i <= m; i++) {
      bool found = false;

      // Traverse to check for the
      // valid conditions
      while (j <= r) {

        // If condition satisfies
        if (arr[i] >= K * arr[j]) {
          found = true;
        }
        else
          break;
        j++;
      }

      // While a[i] > K*a[j] satisfies
      // increase j

      // All elements in the right
      // side of the left subarray
      // also satisfies
      if (found == true) {
        cnt += j - (m + 1);
        j--;
      }
    }

    // Sort the two given arrays and
    // store in the resultant array
    int k = l;
    i = l;
    j = m + 1;

    while (i <= m && j <= r)
    {
      if (arr[i] <= arr[j])
        temp[k++] = arr[i++];
      else
        temp[k++] = arr[j++];
    }

    // Elements which are left
    // in the left subarray
    while (i <= m)
      temp[k++] = arr[i++];

    // Elements which are left
    // in the right subarray
    while (j <= r)
      temp[k++] = arr[j++];

    for (i = l; i <= r; i++)
      arr[i] = temp[i];

    // Return the count obtained
    return cnt;
  }

  // Function to partition array into two halves
  static int mergeSortUtil(int[] arr, int[] temp, int l,
                           int r, int K)
  {
    int cnt = 0;
    if (l < r) {

      // Same as (l + r) / 2, but avoids
      // overflow for large l and h
      int m = (l + r) / 2;

      // Sort first and second halves
      cnt += mergeSortUtil(arr, temp, l, m, K);
      cnt += mergeSortUtil(arr, temp, m + 1, r, K);

      // Call the merging function
      cnt += merge(arr, temp, l, m, r, K);
    }
    return cnt;
  }

  // Function to print the count of
  // required pairs using Merge Sort
  static void mergeSort(int[] arr, int N, int K)
  {
    int[] temp = new int[N];
    Console.WriteLine(
      mergeSortUtil(arr, temp, 0, N - 1, K));
  }

  // Driver code
  static public void Main()
  {

    int[] arr = new int[] { 5, 6, 2, 5 };
    int N = arr.Length;
    int K = 2;

    // Function Call
    mergeSort(arr, N, K); 
  }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to merge two sorted arrays
function merge(arr, temp, l, m, r, K)
{

    // i: index to left subarray
    let i = l;

    // j: index to right subarray
    let j = m + 1;

    // Stores count of pairs that
    // satisfy the given condition
    let cnt = 0;

    for(i = l; i <= m; i++)
    {
        let found = false;

        // Traverse to check for the
        // valid conditions
        while (j <= r)
        {

            // If condition satisfies
            if (arr[i] >= K * arr[j])
            {
                found = true;
            }
            else
                break;
                j++;
        }

        // While a[i] > K*a[j] satisfies
        // increase j

        // All elements in the right
        // side of the left subarray
        // also satisfies
        if (found == true)
        {
            cnt += j - (m + 1);
            j--;
        }
    }

    // Sort the two given arrays and
    // store in the resultant array
    let k = l;
    i = l;
    j = m + 1;

    while (i <= m && j <= r)
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
            temp[k++] = arr[j++];
    }

    // Elements which are left
    // in the left subarray
    while (i <= m)
        temp[k++] = arr[i++];

    // Elements which are left
    // in the right subarray
    while (j <= r)
        temp[k++] = arr[j++];

    for(i = l; i <= r; i++)
        arr[i] = temp[i];

    // Return the count obtained
    return cnt;
}

// Function to partition array into two halves
function mergeSortUtil(arr, temp, l, r, K)
{
    let cnt = 0;
    if (l < r)
    {

        // Same as (l + r) / 2, but avoids
        // overflow for large l and h
        let m = parseInt((l + r) / 2, 10);

        // Sort first and second halves
        cnt += mergeSortUtil(arr, temp,
                             l, m, K);
        cnt += mergeSortUtil(arr, temp,
                             m + 1, r, K);

        // Call the merging function
        cnt += merge(arr, temp, l, m, r, K);
    }
    return cnt;
}

// Function to print the count of
// required pairs using Merge Sort
function mergeSort(arr, N, K)
{
    let temp = new Array(N);
    document.write(mergeSortUtil(
        arr, temp, 0, N - 1, K));
}

// Driver code
let arr = [ 5, 6, 2, 5 ];
let N = arr.length;
let K = 2;

// Function Call
mergeSort(arr, N, K);

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*