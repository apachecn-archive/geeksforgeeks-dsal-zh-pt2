# 将所有数组元素相等所需的除法数减少 2

> 原文:[https://www . geeksforgeeks . org/最小化所有数组元素相等所需的 2 分频数/](https://www.geeksforgeeks.org/minimize-count-of-divisions-by-2-required-to-make-all-array-elements-equal/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过 **2** 找到数组元素的最小除法数(**整数除法**，使所有[个数组元素相同](https://www.geeksforgeeks.org/all-elements-in-an-array-are-same-or-not/)。

**示例:**

> **输入:** arr[] = {3，1，1，3}
> **输出:** 2
> **解释:**
> **运算 1:** 将 arr[0] ( = 3)除以 2。数组 arr[]修改为{1，1，1，3}。
> **运算 2:** 将 arr[3] ( = 3)除以 2。数组 arr[]修改为{1，1，1，1}。
> 因此，所需除法运算的计数为 2。
> 
> **输入:** arr[] = {2，2，2 }
> T3】输出: 0

**方法:**解决给定问题的思路是找到数组中所有元素可以减少到的最大个数。按照以下步骤解决问题:

*   初始化一个变量，比如**和**，以存储所需除法运算的最小计数。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) ，比如说 **M** ，来存储数组元素的频率。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，直到发现任意数组元素 **arr[i]** 大于 **0** 。继续将**arr【I】**除以 **2** ，同时更新在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 中获得的元素的频率。
*   [遍历 HashMap](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) 找到频率最大的元素 **N** 。储存在**最大数量**中。
*   再次，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，通过将 **arr[i]** 除以 **2** 找到将 **arr[i]** 减少到 **maxNumber** 所需的操作数，并将操作数加到变量 **ans** 中。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number of
// division by 2 operations required to
// make all array elements equal
void makeArrayEqual(int A[], int n)
{
    // Stores the frequencies of elements
    map<int, int> mp;

    // Stores the maximum number to
    // which every array element
    // can be reduced to
    int max_number = 0;

    // Stores the minimum number
    // of operations required
    int ans = 0;

    // Traverse the array and store
    // the frequencies in the map
    for (int i = 0; i < n; i++) {

        int b = A[i];

        // Iterate while b > 0
        while (b) {
            mp[b]++;

            // Keep dividing b by 2
            b /= 2;
        }
    }

    // Iterate over the map to find
    // the required maximum number
    for (auto x : mp) {

        // Check if the frequency
        // is equal to n
        if (x.second == n) {

            // If true, store it in
            // max_number
            max_number = x.first;
        }
    }

    // Iterate over the array, A[]
    for (int i = 0; i < n; i++) {
        int b = A[i];

        // Find the number of operations
        // required to reduce A[i] to
        // max_number
        while (b != max_number) {

            // Increment the number of
            // operations by 1
            ans++;
            b /= 2;
        }
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 1, 1, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    makeArrayEqual(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.Map;
import java.util.HashMap;

class GFG
{

  // Function to count minimum number of
  // division by 2 operations required to
  // make all array elements equal
  public static void makeArrayEqual(int A[], int n)
  {

    // Stores the frequencies of elements
    HashMap<Integer, Integer> map = new HashMap<>();

    // Stores the maximum number to
    // which every array element
    // can be reduced to
    int max_number = 0;

    // Stores the minimum number
    // of operations required
    int ans = 0;

    // Traverse the array and store
    // the frequencies in the map
    for (int i = 0; i < n; i++) {

      int b = A[i];

      // Iterate while b > 0
      while (b>0) {
        Integer k = map.get(b);
        map.put(b, (k == null) ? 1 : k + 1);

        // Keep dividing b by 2
        b /= 2;
      }
    }

    // Iterate over the map to find
    // the required maximum number
    for (Map.Entry<Integer, Integer> e :
         map.entrySet()) {

      // Check if the frequency
      // is equal to n
      if (e.getValue() == n) {

        // If true, store it in
        // max_number
        max_number = e.getKey();
      }
    }

    // Iterate over the array, A[]
    for (int i = 0; i < n; i++) {
      int b = A[i];

      // Find the number of operations
      // required to reduce A[i] to
      // max_number
      while (b != max_number) {

        // Increment the number of
        // operations by 1
        ans++;
        b /= 2;
      }
    }

    // Print the answer
    System.out.println(ans + " ");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 3, 1, 1, 3 };
    int N = arr.length;
    makeArrayEqual(arr, N);
  }
}

// This code is contributed by aditya7409.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to count minimum number of
# division by 2 operations required to
# make all array elements equal
def makeArrayEqual(A, n):

  # Stores the frequencies of elements
  mp = dict()

  # Stores the maximum number to
  # which every array element
  # can be reduced to
  max_number = 0

  # Stores the minimum number
  # of operations required
  ans = 0

  # Traverse the array and store
  # the frequencies in the map
  for i in range(n):
    b = A[i]

      # Iterate while b > 0
    while (b>0):
      if (b in mp):
        mp[b] += 1
      else:
        mp[b] = mp.get(b,0)+1

      # Keep dividing b by 2
      b //= 2

  # Iterate over the map to find
  # the required maximum number
  for key,value in mp.items():

    # Check if the frequency
    # is equal to n
    if (value == n):

      # If true, store it in
      # max_number
      max_number = key

  # Iterate over the array, A[]
  for i in range(n):
    b = A[i]

      # Find the number of operations
      # required to reduce A[i] to
      # max_number
    while (b != max_number):

      # Increment the number of
      # operations by 1
      ans += 1
      b //= 2

  # Print the answer
  print(ans)

# Driver Code
if __name__ == '__main__':
  arr = [3, 1, 1, 3]
  N = len(arr)
  makeArrayEqual(arr, N)

  # This code is contributed by bgangwar59.
```

## C#

```
using System;
using System.Collections.Generic;

class GFG
{

  // Function to count minimum number of
  // division by 2 operations required to
  // make all array elements equal
  public static void makeArrayEqual(int[] A, int n)
  {

    // Stores the frequencies of elements
    Dictionary<int, int> map = new Dictionary<int, int>();

    // Stores the maximum number to
    // which every array element
    // can be reduced to
    int max_number = 0;

    // Stores the minimum number
    // of operations required
    int ans = 0;

    // Traverse the array and store
    // the frequencies in the map
    for (int i = 0; i < n; i++) {

      int b = A[i];

      // Iterate while b > 0
      while (b > 0)
      {
        if (map.ContainsKey(b))
            map[b] ++;
        else
            map[b]=  1;

        // Keep dividing b by 2
        b /= 2;
      }
    }

    // Iterate over the map to find
    // the required maximum number
    foreach(KeyValuePair<int, int> e in map)
    {

      // Check if the frequency
      // is equal to n
      if (e.Value == n) {

        // If true, store it in
        // max_number
        max_number = e.Key;
      }
    }

    // Iterate over the array, A[]
    for (int i = 0; i < n; i++) {
      int b = A[i];

      // Find the number of operations
      // required to reduce A[i] to
      // max_number
      while (b != max_number) {

        // Increment the number of
        // operations by 1
        ans++;
        b /= 2;
      }
    }

    // Print the answer
    Console.Write(ans + " ");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 3, 1, 1, 3 };
    int N = arr.Length;
    makeArrayEqual(arr, N);
  }
}

// This code is contributed by shubhamsingh10.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count minimum number of
// division by 2 operations required to
// make all array elements equal
function makeArrayEqual(A, n)
{

    // Stores the frequencies of elements
    let mp = new Map();

    // Stores the maximum number to
    // which every array element
    // can be reduced to
    let max_number = 0;

    // Stores the minimum number
    // of operations required
    let ans = 0;

    // Traverse the array and store
    // the frequencies in the map
    for(let i = 0; i < n; i++)
    {
        let b = A[i];

        // Iterate while b > 0
        while (b)
        {
            if (mp.has(b))
            {
                mp.set(b, mp.get(b) + 1)
            }
            else
            {
                mp.set(b, 1)
            }

            // Keep dividing b by 2
            b = Math.floor(b / 2);
        }
    }

    // Iterate over the map to find
    // the required maximum number
    for(let x of mp)
    {

        // Check if the frequency
        // is equal to n
        if (x[1] == n)
        {

            // If true, store it in
            // max_number
            max_number = x[0];
        }
    }

    // Iterate over the array, A[]
    for(let i = 0; i < n; i++)
    {
        let b = A[i];

        // Find the number of operations
        // required to reduce A[i] to
        // max_number
        while (b != max_number)
        {

            // Increment the number of
            // operations by 1
            ans++;
            b = Math.floor(b / 2);
        }
    }

    // Print the answer
    document.write(ans);
}

// Driver Code
let arr = [ 3, 1, 1, 3 ];
let N = arr.length

makeArrayEqual(arr, N);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*