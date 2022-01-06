# 尽量减少给定数组 A[]中的插入和删除，使其与数组 B[]相同

> 原文:[https://www . geesforgeks . org/最小化给定数组 a 中的插入和删除，使其与数组 b 相同/](https://www.geeksforgeeks.org/minimize-insertions-and-deletions-in-given-array-a-to-make-it-identical-to-array-b/)

给定两个长度分别为 **N** 和 **M** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是找到使两个阵列相同所需的阵列 **A[]** 上的插入和删除的最小数量。
**注意:**数组 **B[]** 是排序的，它的所有元素都是不同的，可以在任何索引处进行操作，不一定要在末尾。

**示例:**

> **输入:** A[] = {1，2，5，3，1}，B[] = {1，3，5}
> **输出:** 4
> **说明:**在第一次操作中，从数组 A[]中删除 A[1]，在第二次操作中，在该位置插入 3。在第 3 和第 4 次操作中，删除 A[3]和 A[4]。因此，在 4 个操作中，A[] = {1，3，5} = B[]，这是最小的可能。
> 
> **输入:** A[] = {1，4}，B[] = {1，4 }
> T3】输出: 0

**方法:**通过观察[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**中不能删除的元素的最优选择是**A【】**和**B【】**中常见元素中[最长递增子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)的元素，可以解决给定的问题。因此，上述问题可以通过将数组 **A[]** 和 **B[]** 的公共元素存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，并使用[这个](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)算法找到 LIS 来解决。之后，除 LIS 之外的所有元素都可以从 **A[]** 中删除，剩下的在 **B[]** 中但不在 **A[]** 中的元素可以插入。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum operations
// to convert array A to B using
// insertions and deletion opertations
int minInsAndDel(int A[], int B[], int n, int m)
{

    // Stores the common elements in A and B
    vector<int> common;
    unordered_set<int> s;

    // Loop to iterate over B
    for (int i = 0; i < m; i++) {
        s.insert(B[i]);
    }

    // Loop to iterate over A
    for (int i = 0; i < n; i++) {

        // If current element is also present
        // in array B
        if (s.find(A[i]) != s.end()) {
            common.push_back(A[i]);
        }
    }

    // Stores the Longest Increasing Subsequence
    // among the common elements in A and B
    vector<int> lis;

    // Loop to find the LIS among the common
    // elements in A and B
    for (auto e : common) {
        auto it = lower_bound(
            lis.begin(), lis.end(), e);

        if (it != lis.end())
            *it = e;
        else
            lis.push_back(e);
    }

    // Stores the final answer
    int ans;

    // Count of elements to be inserted in A[]
    ans = m - lis.size();

    // Count of elements to be deleted from A[]
    ans += n - lis.size();

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int N = 5, M = 3;
    int A[] = { 1, 2, 5, 3, 1 };
    int B[] = { 1, 3, 5 };

    cout << minInsAndDel(A, B, N, M) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.util.*;

class GFG
{

  // Function to implement lower_bound
static int lower_bound(int arr[], int X)
{
    int mid;
    int N = arr.length;

    // Initialise starting index and
    // ending index
    int low = 0;
    int high = N;

    // Till low is less than high
    while (low < high) {
        mid = low + (high - low) / 2;

        // If X is less than or equal
        // to arr[mid], then find in
        // left subarray
        if (X <= arr[mid]) {
            high = mid;
        }

        // If X is greater arr[mid]
        // then find in right subarray
        else {
            low = mid + 1;
        }
    }

    // if X is greater than arr[n-1]
    if(low < N && arr[low] < X) {
       low++;
    }

    // Return the lower_bound index
    return low;
}

    // Function to find minimum operations
    // to convert array A to B using
    // insertions and deletion opertations
    static int minInsAndDel(int A[], int B[], int n, int m)
    {

        // Stores the common elements in A and B
        int[] common = new int[n];
        int k = 0;
        HashSet<Integer> s= new HashSet<Integer>();

        // Loop to iterate over B
        for (int i = 0; i < m; i++) {
            s.add(B[i]);
        }

        // Loop to iterate over A
        for (int i = 0; i < n; i++) {

            // If current element is also present
            // in array B
            if (s.contains(A[i]) == false) {
                common[k++] = A[i];
            }
        }

        // Stores the Longest Increasing Subsequence
        // among the common elements in A and B
        int[] lis = new int[n];
        k = 0;
      ArrayList<Integer> LIS = new ArrayList<Integer>();

        // Loop to find the LIS among the common
        // elements in A and B
        for (int e : common) {
            int it = lower_bound(lis, e);

            if (it <lis.length)
                it = e;
            else{
                lis[k++] = e;
                LIS.add(e);
            }
        }

        // Stores the final answer
        int ans;

        // Count of elements to be inserted in A[]
        ans = m - LIS.size()-1;

        // Count of elements to be deleted from A[]
        ans = ans+ n - LIS.size()-1;

        // Return Answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5, M = 3;
        int A[] = { 1, 2, 5, 3, 1 };
        int B[] = { 1, 3, 5 };

        System.out.println(minInsAndDel(A, B, N, M));
    }
}

// This code is contributed by lokeshpotta20.
```

## 蟒蛇 3

```
# python program of the above approach
from bisect import bisect_left

# Function to find minimum operations
# to convert array A to B using
# insertions and deletion opertations
def minInsAndDel(A, B, n, m):

    # Stores the common elements in A and B
    common = []
    s = set()

    # Loop to iterate over B
    for i in range(0, m):
        s.add(B[i])

    # Loop to iterate over A
    for i in range(0, n):

        # If current element is also present
        # in array B
        if (A[i] in s):
            common.append(A[i])

    # Stores the Longest Increasing Subsequence
    # among the common elements in A and B
    lis = []

    # Loop to find the LIS among the common
    # elements in A and B
    for e in common:
        it = bisect_left(lis, e, 0, len(lis))

        if (it != len(lis)):
            lis[it] = e
        else:
            lis.append(e)

    # Stores the final answer
    ans = 0

    # Count of elements to be inserted in A[]
    ans = m - len(lis)

    # Count of elements to be deleted from A[]
    ans += n - len(lis)

    # Return Answer
    return ans

# Driver Code
if __name__ == "__main__":

    N = 5
    M = 3
    A = [1, 2, 5, 3, 1]
    B = [1, 3, 5]

    print(minInsAndDel(A, B, N, M))

    # This code is contributed by rakeshsahni
```

## C#

```
/*package whatever //do not write package name here */
using System;
using System.Collections.Generic;

class GFG {

    // Function to implement lower_bound
    static int lower_bound(int[] arr, int X)
    {
        int mid;
        int N = arr.Length;

        // Initialise starting index and
        // ending index
        int low = 0;
        int high = N;

        // Till low is less than high
        while (low < high) {
            mid = low + (high - low) / 2;

            // If X is less than or equal
            // to arr[mid], then find in
            // left subarray
            if (X <= arr[mid]) {
                high = mid;
            }

            // If X is greater arr[mid]
            // then find in right subarray
            else {
                low = mid + 1;
            }
        }

        // if X is greater than arr[n-1]
        if (low < N && arr[low] < X) {
            low++;
        }

        // Return the lower_bound index
        return low;
    }

    // Function to find minimum operations
    // to convert array A to B using
    // insertions and deletion opertations
    static int minInsAndDel(int[] A, int[] B, int n, int m)
    {

        // Stores the common elements in A and B
        int[] common = new int[n];
        int k = 0;
        HashSet<int> s = new HashSet<int>();

        // Loop to iterate over B
        for (int i = 0; i < m; i++) {
            s.Add(B[i]);
        }

        // Loop to iterate over A
        for (int i = 0; i < n; i++) {

            // If current element is also present
            // in array B
            if (s.Contains(A[i]) == false) {
                common[k++] = A[i];
            }
        }

        // Stores the Longest Increasing Subsequence
        // among the common elements in A and B
        int[] lis = new int[n];
        k = 0;
        List<int> LIS = new List<int>();

        // Loop to find the LIS among the common
        // elements in A and B
        foreach(int e in common)
        {
            int it = lower_bound(lis, e);

            if (it < lis.Length)
                it = e;
            else {
                lis[k++] = e;
                LIS.Add(e);
            }
        }

        // Stores the final answer
        int ans;

        // Count of elements to be inserted in A[]
        ans = m - LIS.Count - 1;

        // Count of elements to be deleted from A[]
        ans = ans + n - LIS.Count - 1;

        // Return Answer
        return ans;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 5, M = 3;
        int[] A = { 1, 2, 5, 3, 1 };
        int[] B = { 1, 3, 5 };

        Console.WriteLine(minInsAndDel(A, B, N, M));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program of the above approach

// Function to find minimum operations
// to convert array A to B using
// insertions and deletion opertations
function minInsAndDel(A, B, n, m) {

  // Stores the common elements in A and B
  let common = [];
  let s = new Set();

  // Loop to iterate over B
  for (let i = 0; i < m; i++) {
    s.add(B[i]);
  }

  // Loop to iterate over A
  for (let i = 0; i < n; i++) {

    // If current element is also present
    // in array B
    if (s.has(A[i])) {
      common.push(A[i]);
    }
  }

  // Stores the Longest Increasing Subsequence
  // among the common elements in A and B
  let lis = [];

  // Loop to find the LIS among the common
  // elements in A and B
  for (e of common) {
    let it = lower_bound(lis, lis.length, e);

    if (lis.includes(it))
      it = e;
    else
      lis.push(e);
  }

  // Stores the final answer
  let ans;

  // Count of elements to be inserted in A[]
  ans = m - lis.length;

  // Count of elements to be deleted from A[]
  ans += n - lis.length;

  // Return Answer
  return ans;
}

function lower_bound(arr, N, X)
{
    let mid;

    // Initialise starting index and
    // ending index
    let low = 0;
    let high = N;

  // Till low is less than high
  while (low < high) {
    mid = Math.floor(low + (high - low) / 2);

    // If X is less than or equal
    // to arr[mid], then find in
    // left subarray
    if (X <= arr[mid]) {
      high = mid;
    }

    // If X is greater arr[mid]
    // then find in right subarray
    else {
      low = mid + 1;
    }
  }

  // if X is greater than arr[n-1]
  if (low < N && arr[low] < X) {
    low++;
  }

  // Return the lower_bound index
  return low;
}

// Driver Code
let N = 5, M = 3;
let A = [1, 2, 5, 3, 1];
let B = [1, 3, 5];

document.write(minInsAndDel(A, B, N, M));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
4
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*