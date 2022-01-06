# 总和等于其长度的子阵列计数|集合 2

> 原文:[https://www . geeksforgeeks . org/subarrays-sum 等于其长度集-2/](https://www.geeksforgeeks.org/count-of-subarrays-having-sum-equal-to-its-length-set-2/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到子阵列的[数量，其元素之和](https://www.geeksforgeeks.org/number-subarrays-sum-exactly-equal-k/)等于其中的元素数量。

**示例:**

> **输入** : N = 3，arr[] = {1，0，2}
> **输出:** 3
> **说明:**
> 子阵总数为 6，即{1}、{0}、{2}、{1，0}、{0，2}、{1，0}、{1，0，2}。
> 在 6 个子阵列中，以下 3 个子阵列满足给定条件:
> 
> *   {1}:总和= 1，长度= 1
> *   {0，2}:总和= 2，长度= 2
> *   {1，0，2}:总和= 3，长度= 3
> 
> **输入:** N = 3，arr[] = {1，1，0}
> **输出:** 3
> **说明:**
> 子阵总数为 6，即{1}、{1}、{0}、{1，1}、{1，0}、{1，1}、{1，0}、{1，1，0}。
> 在 6 个子阵列中，以下 3 个子阵列满足给定条件:
> 
> *   {1}:总和= 1，长度= 1
> *   {1，1}:总和= 2，长度= 2
> *   {1}:总和= 1，长度= 1
> 
> 输入:N = 6，arr[] = {1，1，1}输出:3 说明:子阵列总数为 6，即{1}，{1}，{1}，{1，1}，{1，1}，{1，1}，{1，1}。在 6 个子阵列中，以下 6 个子阵列满足给定条件:
> 
> *   {1}、{1}、{1}:总和=1，长度=1，子阵列数=3
> *   {1，1}，{1，1}:总和=2，长度=2，子阵列数=2
> *   {1，1，1}:总和=3，长度=3，子阵列数=1
> 
> 总和等于其长度的子阵列总数=6

**幼稚和** [**前缀和**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **为主的方法:**参考[之前的帖子](https://www.geeksforgeeks.org/count-of-subarrays-having-sum-equal-to-its-length/)获得最简单和[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)为主的方法来解决问题。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**对上述方法进行优化，思路是在给定条件下存储子阵的前一次出现，利用[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)进行常量查找。以下是步骤:

*   初始化无序映射 **M** 、**答案**存储子阵个数，**求和**存储数组的[前缀和。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   将当前元素添加到**和**中。
    *   如果**M【sum–I】**存在，那么将该值添加到答案中，因为存在长度为 **i** 的子阵列，其元素的和是当前的**和**。
    *   在地图 **M** 中增加**(sum-I)**的频率。
*   完成上述步骤后，打印**答案**的值作为子阵列的总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function that counts the subarrays
// with sum of its elements as its length
int countOfSubarray(int arr[], int N)
{
    // Store count of elements upto
    // current element with length i
    unordered_map<int, int> mp;

    // Stores the final count of subarray
    int answer = 0;

    // Stores the prefix sum
    int sum = 0;

    // If size of subarray is 1
    mp[1]++;

    // Iterate the array
    for (int i = 0; i < N; i++) {

        // Find the sum
        sum += arr[i];
        answer += mp[sum - i];

        // Update frequency in map
        mp[sum - i]++;
    }

    // Print the total count
    cout << answer;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 0, 2, 1, 2, -2, 2, 4 };

    // Size of array
    int N = sizeof arr / sizeof arr[0];

    // Function Call
    countOfSubarray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that counts the subarrays
// with sum of its elements as its length
static void countOfSubarray(int arr[], int N)
{

    // Store count of elements upto
    // current element with length i
    Map<Integer,
        Integer> mp = new HashMap<Integer,
                                  Integer>(); 

    // Stores the final count of subarray
    int answer = 0;

    // Stores the prefix sum
    int sum = 0;

    // If size of subarray is 1
    if (mp.get(1) != null)
        mp.put(1, mp.get(1) + 1);
    else
        mp.put(1, 1);

    // Iterate the array
    for(int i = 0; i < N; i++)
    {

        // Find the sum
        sum += arr[i];

        if (mp.get(sum - i) != null)
            answer += mp.get(sum - i);

        // Update frequency in map
        if (mp.get(sum - i) != null)
            mp.put(sum - i, mp.get(sum - i) + 1);
        else
            mp.put(sum - i, 1);
    }

    // Print the total count
    System.out.print(answer);
}

// Driver Code
public static void main(String args[])
{

    // Given array arr[]
    int arr[] = { 1, 0, 2, 1, 2, -2, 2, 4 };

    // Size of array
    int N = arr.length;

    // Function Call
    countOfSubarray(arr, N);
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import defaultdict

# Function that counts the subarrays
# with sum of its elements as its length
def countOfSubarray(arr, N):

    # Store count of elements upto
    # current element with length i
    mp = defaultdict(lambda : 0)

    # Stores the final count of subarray
    answer = 0

    # Stores the prefix sum
    sum = 0

    # If size of subarray is 1
    mp[1] += 1

    # Iterate the array
    for i in range(N):

        # Find the sum
        sum += arr[i]
        answer += mp[sum - i]

        # Update frequency in map
        mp[sum - i] += 1

    # Print the total count
    print(answer)

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 0, 2, 1, 2, -2, 2, 4 ]

    # Size of the array
    N = len(arr)

    # Function Call
    countOfSubarray(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function that counts
// the subarrays with sum
// of its elements as its length
static void countOfSubarray(int []arr,
                            int N)
{   
  // Store count of elements upto
  // current element with length i
  Dictionary<int,
             int> mp = new Dictionary<int,
                                      int>(); 

  // Stores the readonly
  // count of subarray
  int answer = 0;

  // Stores the prefix sum
  int sum = 0;

  // If size of subarray is 1
  mp[1] = 1;

  // Iterate the array
  for(int i = 0; i < N; i++)
  {
    // Find the sum
    sum += arr[i];

    if (mp.ContainsKey(sum - i))
      answer += mp[sum - i];

    // Update frequency in map
    if(mp.ContainsKey(sum - 1))
      mp[sum - 1]++;
    else
      mp[sum - 1] = 1;
  }

  // Print the total count
  Console.Write(answer - 2);
}

// Driver Code
public static void Main(String []args)
{
  // Given array []arr
  int []arr = {1, 0, 2, 1,
               2, -2, 2, 4};

  // Size of array
  int N = arr.Length;

  // Function Call
  countOfSubarray(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that counts the subarrays
// with sum of its elements as its length
function countOfSubarray(arr, N)
{
    // Store count of elements upto
    // current element with length i
    var mp = new Map();

    // Stores the final count of subarray
    var answer = 0;

    // Stores the prefix sum
    var sum = 0;

    // If size of subarray is 1
    if(!mp.has(1))
        mp.set(1, 1)
    else
        mp.set(1, mp.get(1)+1)

    // Iterate the array
    for (var i = 0; i < N; i++) {

        // Find the sum
        sum += arr[i];
        answer += mp.has(sum - i)?mp.get(sum - i):0;

        // Update frequency in map
        if(mp.has(sum - i))
            mp.set(sum - i, mp.get(sum - i)+1)
        else
            mp.set(sum - i, 1)
    }

    // Print the total count
    document.write( answer);
}

// Driver Code

// Given array arr[]
var arr = [1, 0, 2, 1, 2, -2, 2, 4];

// Size of array
var N = arr.length;

// Function Call
countOfSubarray(arr, N);

</script>
```

**Output**

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)