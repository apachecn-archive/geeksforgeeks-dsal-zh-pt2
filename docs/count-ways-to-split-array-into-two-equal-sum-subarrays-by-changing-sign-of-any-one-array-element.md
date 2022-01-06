# 通过改变任意一个数组元素的符号来计数将数组拆分为两个相等和的子数组的方法

> 原文:[https://www . geeksforgeeks . org/count-way-通过改变任意一个数组元素的符号将数组拆分为两个等和子数组/](https://www.geeksforgeeks.org/count-ways-to-split-array-into-two-equal-sum-subarrays-by-changing-sign-of-any-one-array-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过改变任意一个数组元素的符号来计算将数组拆分成两个相等和的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的方法。

**示例:**

> **输入:** arr[] = {2，2，-3，3}
> **输出:** 2
> **解释:**
> 将 arr[0] = 2 改为 arr[0] = -2，数组变成{-2，2，-3，3}。只有一个可能的拆分是{-2，2}和{-3，3}。
> 将 arr[1] = 2 改为 arr[1] = -2，数组变成{2，-2，-3，3}。只有一个可能的拆分是{-2，2}和{-3，3}。
> 将 arr[2] = -3 改为 arr[2] = 3，数组变成{2，2，3，3}。无法分割数组。
> 将 arr[3] = 3 改为 arr[2] = -3，数组变成{2，2，-3，-3}。无法分割数组。
> 因此，拆分方式总数= 1 + 1 + 0 + 0 = 2。
> 
> **输入:** arr[] = {2，2，1，-3，3 }
> T3】输出: 0

**天真法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)逐个改变每个数组元素的符号，统计每次改变将数组拆分成两个等和子数组的方式数。最后，打印所有可能方式的总和。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，其思想是为每个阵列索引存储[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[后缀和](https://www.geeksforgeeks.org/python-suffix-list-sum/)，以找到 ***O(1)*** 计算复杂度中的分裂子阵列的和。按照以下步骤解决问题:

*   初始化一个变量，比如**计数**，来存储拆分数组的方式数。
*   初始化两个变量，比如**前缀**和**后缀**，用 **0** 来存储两个数组的前缀和后缀和。
*   初始化两个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **前缀计数**和**后缀计数**来存储前缀和后缀数组中的元素计数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并更新**后缀**中各元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   遍历数组 **arr[]** 并执行以下步骤:
    *   [将**arr【I】**插入**前缀**地图](https://www.geeksforgeeks.org/map-insert-in-c-stl/)[并将其从**后缀**](https://www.geeksforgeeks.org/map-erase-function-in-c-stl/) 中移除。
    *   将**arr【I】**添加到**前缀**并将**后缀**设置为数组和**前缀**的[总和的差。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
    *   将子阵列之和，即**前缀-后缀**的差值存储在一个变量中，比如**差值**。
    *   在 **i <sup>第</sup>指数**处的分割方式的计数通过以下方式计算:
        *   如果 **diff** 为奇数，则数组不能拆分。
        *   如果 **diff** 为偶数，则将值**(前缀+后缀 Count[ -diff / 2])** 加到 **count** 上。
*   完成上述步骤后，**计数**的值给出可能拆分的总计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count ways of splitting
// the array in two subarrays of equal
// sum by changing sign of any 1 element
int countSubArraySignChange(int arr[], int N)
{
    // Stores the count of elements
    // in prefix and suffix of array
    unordered_map<int, int> prefixCount;
    unordered_map<int, int> suffixCount;

    // Stores the total sum of array
    int total = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--) {

        total += arr[i];

        // Increase the frequency of
        // current element in suffix
        suffixCount[arr[i]]++;
    }

    // Stores prefix sum upto
    // an index
    int prefixSum = 0;

    // Stores sum of suffix
    // from an index
    int suffixSum = 0;

    // Stores the count of ways to
    // split the array in 2 subarrays
    // having equal sum
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // Modify prefix sum
        prefixSum += arr[i];

        // Add arr[i] to prefix Map
        prefixCount[arr[i]]++;

        // Calculate suffix sum by
        // subtracting prefix sum
        // from total sum of elements
        suffixSum = total - prefixSum;

        // Remove arr[i] from suffix Map
        suffixCount[arr[i]]--;

        // Store the difference
        // between the subarrays
        int diff = prefixSum - suffixSum;

        // Check if diff is even or not
        if (diff % 2 == 0) {

            // Count number of ways to
            // split array at index i such
            // that subarray sums are same
            int x = prefixCount
                    + suffixCount[-diff / 2];

            // Update the count
            count = count + x;
        }
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 2, -3, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countSubArraySignChange(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to count ways of splitting
// the array in two subarrays of equal
// sum by changing sign of any 1 element
static int countSubArraySignChange(int arr[], int N)
{

    // Stores the count of elements
    // in prefix and suffix of array
    HashMap<Integer,Integer> prefixCount = new HashMap<Integer,Integer>();
    HashMap<Integer,Integer> suffixCount = new HashMap<Integer,Integer>();

    // Stores the total sum of array
    int total = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--)
    {

        total += arr[i];

        // Increase the frequency of
        // current element in suffix
        if(suffixCount.containsKey(arr[i])){
            suffixCount.put(arr[i], suffixCount.get(arr[i]) + 1);
        }
        else{
            suffixCount.put(arr[i], 1);
        }
    }

    // Stores prefix sum upto
    // an index
    int prefixSum = 0;

    // Stores sum of suffix
    // from an index
    int suffixSum = 0;

    // Stores the count of ways to
    // split the array in 2 subarrays
    // having equal sum
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++)
    {

        // Modify prefix sum
        prefixSum += arr[i];

        // Add arr[i] to prefix Map
        if(prefixCount.containsKey(arr[i]))
        {
            prefixCount.put(arr[i], prefixCount.get(arr[i])+1);
        }
        else
        {
            prefixCount.put(arr[i], 1);
        }

        // Calculate suffix sum by
        // subtracting prefix sum
        // from total sum of elements
        suffixSum = total - prefixSum;

        // Remove arr[i] from suffix Map
        if(suffixCount.containsKey(arr[i]))
        {
            suffixCount.put(arr[i], suffixCount.get(arr[i]) - 1);
        }

        // Store the difference
        // between the subarrays
        int diff = prefixSum - suffixSum;

        // Check if diff is even or not
        if (diff % 2 == 0)
        {

            // Count number of ways to
            // split array at index i such
            // that subarray sums are same
            int x = (prefixCount.containsKey(diff / 2)?prefixCount.get(diff / 2):0)
                    + (suffixCount.containsKey(-diff / 2)?suffixCount.get(-diff / 2):0);

            // Update the count
            count = count + x;
        }
    }

    // Return the count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 2, -3, 3 };
    int N = arr.length;

    // Function Call
    System.out.print(countSubArraySignChange(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count ways of spliting
# the array in two subarrays of equal
# sum by changing sign of any 1 element
def countSubArraySignChange(arr, N):

    # Stores the count of elements
    # in prefix and suffix of array
    prefixCount = {}
    suffixCount = {}

    # Stores the total sum of array
    total = 0

    # Traverse the array
    for i in range(N - 1, -1, -1):

        total += arr[i]

        # Increase the frequency of
        # current element in suffix
        suffixCount[arr[i]] = suffixCount.get(arr[i], 0) + 1

    # Stores prefix sum upto
    # an index
    prefixSum = 0

    # Stores sum of suffix
    # from an index
    suffixSum = 0

    # Stores the count of ways to
    # split the array in 2 subarrays
    # having equal sum
    count = 0

    # Traverse the array
    for i in range(N - 1):

        # Modify prefix sum
        prefixSum += arr[i]

        # Add arr[i] to prefix Map
        prefixCount[arr[i]] = prefixCount.get(arr[i], 0) + 1

        # Calculate suffix sum by
        # subtracting prefix sum
        # from total sum of elements
        suffixSum = total - prefixSum

        # Remove arr[i] from suffix Map
        suffixCount[arr[i]] -= 1

        # Store the difference
        # between the subarrays
        diff = prefixSum - suffixSum

        # Check if diff is even or not
        if (diff % 2 == 0):

            # Count number of ways to
            # split array at index i such
            # that subarray sums are same
            y, z = 0, 0
            if -diff//2 in suffixCount:
                y = suffixCount[-dff//2]
            if diff//2 in prefixCount:
                z = prefixCount
            x = z+ y

            # Update the count
            count = count + x

    # Return the count
    return count

# Driver Code
if __name__ == '__main__':
    arr=[2, 2, -3, 3]
    N = len(arr)

    # Function Call
    print(countSubArraySignChange(arr, N))

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to count ways of splitting
  // the array in two subarrays of equal
  // sum by changing sign of any 1 element
  static int countSubArraySignChange(int []arr, int N)
  {

    // Stores the count of elements
    // in prefix and suffix of array
    Dictionary<int,int> prefixCount = new Dictionary<int,int>();
    Dictionary<int,int> suffixCount = new Dictionary<int,int>();

    // Stores the total sum of array
    int total = 0;

    // Traverse the array
    for (int i = N - 1; i >= 0; i--)
    {

      total += arr[i];

      // Increase the frequency of
      // current element in suffix
      if(suffixCount.ContainsKey(arr[i])){
        suffixCount[arr[i]] = suffixCount[arr[i]] + 1;
      }
      else{
        suffixCount.Add(arr[i], 1);
      }
    }

    // Stores prefix sum upto
    // an index
    int prefixSum = 0;

    // Stores sum of suffix
    // from an index
    int suffixSum = 0;

    // Stores the count of ways to
    // split the array in 2 subarrays
    // having equal sum
    int count = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++)
    {

      // Modify prefix sum
      prefixSum += arr[i];

      // Add arr[i] to prefix Map
      if(prefixCount.ContainsKey(arr[i]))
      {
        prefixCount[arr[i]] = prefixCount[arr[i]] + 1;
      }
      else
      {
        prefixCount.Add(arr[i], 1);
      }

      // Calculate suffix sum by
      // subtracting prefix sum
      // from total sum of elements
      suffixSum = total - prefixSum;

      // Remove arr[i] from suffix Map
      if(suffixCount.ContainsKey(arr[i]))
      {
        suffixCount[arr[i]] = suffixCount[arr[i]] - 1;
      }

      // Store the difference
      // between the subarrays
      int diff = prefixSum - suffixSum;

      // Check if diff is even or not
      if (diff % 2 == 0)
      {

        // Count number of ways to
        // split array at index i such
        // that subarray sums are same
        int x = (prefixCount.ContainsKey(diff / 2)?prefixCount:0)
          + (suffixCount.ContainsKey(-diff / 2)?suffixCount[-diff / 2]:0);

        // Update the count
        count = count + x;
      }
    }

    // Return the count
    return count;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 2, 2, -3, 3 };
    int N = arr.Length;

    // Function Call
    Console.Write(countSubArraySignChange(arr, N));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count ways of splitting
// the array in two subarrays of equal
// sum by changing sign of any 1 element
function countSubArraySignChange(arr,N)
{
    // Stores the count of elements
    // in prefix and suffix of array
    let prefixCount = new Map();
    let suffixCount = new Map();

    // Stores the total sum of array
    let total = 0;

    // Traverse the array
    for (let i = N - 1; i >= 0; i--)
    {

        total += arr[i];

        // Increase the frequency of
        // current element in suffix
        if(suffixCount.has(arr[i])){
            suffixCount.set(arr[i], suffixCount.get(arr[i]) + 1);
        }
        else{
            suffixCount.set(arr[i], 1);
        }
    }

    // Stores prefix sum upto
    // an index
    let prefixSum = 0;

    // Stores sum of suffix
    // from an index
    let suffixSum = 0;

    // Stores the count of ways to
    // split the array in 2 subarrays
    // having equal sum
    let count = 0;

    // Traverse the array
    for (let i = 0; i < N - 1; i++)
    {

        // Modify prefix sum
        prefixSum += arr[i];

        // Add arr[i] to prefix Map
        if(prefixCount.has(arr[i]))
        {
            prefixCount.set(arr[i], prefixCount.get(arr[i])+1);
        }
        else
        {
            prefixCount.set(arr[i], 1);
        }

        // Calculate suffix sum by
        // subtracting prefix sum
        // from total sum of elements
        suffixSum = total - prefixSum;

        // Remove arr[i] from suffix Map
        if(suffixCount.has(arr[i]))
        {
            suffixCount.set(arr[i], suffixCount.get(arr[i]) - 1);
        }

        // Store the difference
        // between the subarrays
        let diff = prefixSum - suffixSum;

        // Check if diff is even or not
        if (diff % 2 == 0)
        {

            // Count number of ways to
            // split array at index i such
            // that subarray sums are same
            let x = (prefixCount.has(diff / 2)?
                     prefixCount.get(diff / 2):0)
                    + (suffixCount.has(-diff / 2)?
                       suffixCount.get(-diff / 2):0);

            // Update the count
            count = count + x;
        }
    }

    // Return the count
    return count;
}

// Driver Code
let arr=[2, 2, -3, 3];
let N = arr.length;
// Function Call
document.write(countSubArraySignChange(arr, N));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)