# 通过重复递增子序列

使所有数组元素等于 K

> 原文:[https://www . geesforgeks . org/make-all-array-elements-equal-k-by-repeating-subseries/](https://www.geeksforgeeks.org/make-all-array-elements-equal-to-k-by-repeatedly-incrementing-subsequences/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过将子序列的所有元素重复递增 **1** 来使所有数组元素等于 **K** 。
***注:**的值 **K** 至少是数组* 的 [*最大元素。*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**示例:**

> **输入:** arr[] = {2，3，3，4}，K = 5
> **输出:** 4
> **解释:**
> **操作 1:** 选择子序列{2，3，4}。递增每个元素后，子序列会修改为{3，4，5}。数组修改为{3，3，4，5}。
> **操作 2:** 选择子序列{3，4}。递增每个元素后，子序列修改为{4，5}。数组修改为{3，4，5，5}。
> **操作 3:** 选择子序列{3，4}。递增每个元素后，子序列修改为{4，5}。数组修改为{4，5，5，5}。
> **操作 4:** 选择子序列{4}。递增每个元素后，子序列修改为{5}。数组修改为{5，5，5，5}。
> 
> **输入:** arr[] = {1，1，1，1}，K = 3
> T3】输出: 5

**方法:**想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来跟踪子序列中的元素。当子序列中的元素增加 **1** 时，其频率减少 **1** ，其修改值的频率增加 **1** 。
按照以下步骤解决问题:

*   初始化一个变量，比如**和**，它存储所需的最小操作数。
*   初始化一个 [Hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，说 **mp** ，[存储数组元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)。
*   当 **K** 的频率小于 **N** 即**MP【K】<N**时，执行以下操作:
    *   使用变量 **i** 迭代一个范围**【1，K–1】**
        *   如果**MP【I】**大于 **0** ，则通过 **1** 降低当前值的频率，增加下一组 **(i + 1)** 元素的频率。
        *   如果 **(i + 1)** 不是任何先前值的一部分，跳过它并[继续遍历循环](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   将**和**的值增加 1。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations required to make all
// elements equal to k
void minOperations(int arr[], int n, int k)
{
    // Initialize a hashmap
    map<int, int> mp;

    // Store frequency of array elements
    for (int i = 0; i < n; i++) {
        mp[arr[i]]++;
    }

    // Store the minimum number of
    // operations required
    int ans = 0;

    // Iterate until all array elements
    // becomes equal to K
    while (mp[k] < n) {

        // Iterate through range [1, k - 1]
        // since only one element can be
        // increased from each group
        for (int i = 1; i <= k - 1; i++) {

            // Check if the current number
            // has frequency > 0, i.e.,
            // it is a part of a group
            if (mp[i]) {

                // If true, decrease the
                // frequency of current
                // group of element by 1
                mp[i]--;

                // Increase the frequency
                // of the next group of
                // elements by 1
                mp[i + 1]++;

                // If the next element is
                // not the part of any
                // group, then skip it
                if (mp[i + 1] == 1) {
                    i++;
                }
            }
        }

        // Increment count of operations
        ans++;
    }

    // Print the count of operations
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 3, 4 };
    int K = 5;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minOperations(arr, N, K);

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

  // Function to find the minimum number
  // of operations required to make all
  // elements equal to k
  static void minOperations(int arr[], int n, int k)
  {

    // Initialize a hashmap
    Map<Integer, Integer> mp = new HashMap<>();

    // Store frequency of array elements
    for (int i = 0; i < n; i++)
    {
      if (mp.containsKey(arr[i]))
      {
        mp.put(arr[i], mp.get(arr[i]) + 1);
      }
      else
      {
        mp.put(arr[i], 1);
      }
    }

    // Store the minimum number of
    // operations required
    int ans = 0;

    // Iterate until all array elements
    // becomes equal to K
    while (mp.containsKey(k) == false
           || mp.get(k) < n) {

      // Iterate through range [1, k - 1]
      // since only one element can be
      // increased from each group
      for (int i = 1; i <= k - 1; i++) {

        // Check if the current number
        // has frequency > 0, i.e.,
        // it is a part of a group
        if (mp.containsKey(i) && mp.get(i) > 0) {

          // If true, decrease the
          // frequency of current
          // group of element by 1
          mp.put(i, mp.get(i) - 1);

          // Increase the frequency
          // of the next group of
          // elements by 1
          if (mp.containsKey(i + 1))
            mp.put(i + 1, mp.get(i + 1) + 1);
          else
            mp.put(i + 1, 1);

          // If the next element is
          // not the part of any
          // group, then skip it
          if (mp.containsKey(i + 1)
              && mp.get(i + 1) == 1) {
            i++;
          }
        }
      }

      // Increment count of operations
      ans++;
    }

    // Print the count of operations
    System.out.print(ans);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 2, 3, 3, 4 };
    int K = 5;
    int N = arr.length;

    // Function Call
    minOperations(arr, N, K);
  }
}

// This code is contributed by Dharanendra L V.
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

public class GFG
{

  // Function to find the minimum number
  // of operations required to make all
  // elements equal to k
  static void minOperations(int []arr, int n, int k)
  {

    // Initialize a hashmap
    Dictionary<int, int> mp = new Dictionary<int, int>();

    // Store frequency of array elements
    for (int i = 0; i < n; i++)
    {
      if (mp.ContainsKey(arr[i]))
      {
        mp[arr[i]] =  mp[arr[i]] + 1;
      }
      else
      {
        mp.Add(arr[i], 1);
      }
    }

    // Store the minimum number of
    // operations required
    int ans = 0;

    // Iterate until all array elements
    // becomes equal to K
    while (mp.ContainsKey(k) == false
           || mp[k] < n) {

      // Iterate through range [1, k - 1]
      // since only one element can be
      // increased from each group
      for (int i = 1; i <= k - 1; i++) {

        // Check if the current number
        // has frequency > 0, i.e.,
        // it is a part of a group
        if (mp.ContainsKey(i) && mp[i] > 0) {

          // If true, decrease the
          // frequency of current
          // group of element by 1
          mp[i] = mp[i] - 1;

          // Increase the frequency
          // of the next group of
          // elements by 1
          if (mp.ContainsKey(i + 1))
            mp[i + 1] = mp[i + 1] + 1;
          else
            mp.Add(i + 1, 1);

          // If the next element is
          // not the part of any
          // group, then skip it
          if (mp.ContainsKey(i + 1)
              && mp[i + 1] == 1) {
            i++;
          }
        }
      }

      // Increment count of operations
      ans++;
    }

    // Print the count of operations
    Console.Write(ans);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 2, 3, 3, 4 };
    int K = 5;
    int N = arr.Length;

    // Function Call
    minOperations(arr, N, K);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

  // Function to find the minimum number
  // of operations required to make all
  // elements equal to k
  function minOperations(arr, n, k)
  {

    // Initialize a hashmap
    let mp = new Map();

    // Store frequency of array elements
    for (let i = 0; i < n; i++)
    {
      if (mp.has(arr[i]))
      {
        mp.set(arr[i], mp.get(arr[i]) + 1);
      }
      else
      {
        mp.set(arr[i], 1);
      }
    }

    // Store the minimum number of
    // operations required
    let ans = 0;

    // Iterate until all array elements
    // becomes equal to K
    while (mp.has(k) == false
           || mp.get(k) < n) {

      // Iterate through range [1, k - 1]
      // since only one element can be
      // increased from each group
      for (let i = 1; i <= k - 1; i++) {

        // Check if the current number
        // has frequency > 0, i.e.,
        // it is a part of a group
        if (mp.has(i) && mp.get(i) > 0) {

          // If true, decrease the
          // frequency of current
          // group of element by 1
          mp.set(i, mp.get(i) - 1);

          // Increase the frequency
          // of the next group of
          // elements by 1
          if (mp.has(i + 1))
            mp.set(i + 1, mp.get(i + 1) + 1);
          else
            mp.set(i + 1, 1);

          // If the next element is
          // not the part of any
          // group, then skip it
          if (mp.has(i + 1)
              && mp.get(i + 1) == 1) {
            i++;
          }
        }
      }

      // Increment count of operations
      ans++;
    }

    // Print the count of operations
    document.write(ans);
  }

// Driver Code

     let arr = [ 2, 3, 3, 4 ];
    let K = 5;
    let N = arr.length;

    // Function Call
    minOperations(arr, N, K);

</script>  
```

**Output:** 

```
4
```

***时间复杂度:** O(N*K)*
***辅助空间:** O(N)*