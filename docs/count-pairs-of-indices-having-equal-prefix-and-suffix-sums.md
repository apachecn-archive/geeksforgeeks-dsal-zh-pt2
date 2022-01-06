# 计数前缀和后缀和相等的索引对

> 原文:[https://www . geesforgeks . org/count-对索引-具有相等的前缀和后缀-sums/](https://www.geeksforgeeks.org/count-pairs-of-indices-having-equal-prefix-and-suffix-sums/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到索引对(I，j) ( *基于 0 的索引*)的计数，使得子数组 **{arr[0]，… arr[i]}** 的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)等于子数组**{ arr[N–1]，…arr[j]}的[后缀和](https://www.geeksforgeeks.org/tag/suffix-sum/)**

**示例:**

> **输入:** arr[] = {1，2，1，1}
> **输出:** 3
> **解释:**
> 3 对可能的指数如下:
> 
> 1.  对{0，3}:子数组{arr[0]}的前缀和= 1。子数组{arr[3]}的后缀和= 1。
> 2.  对{2，1}:子数组{arr[0]的前缀和，..arr[2]} = 4。后缀子数组的和{arr[3]，…，arr[1]} = 4。
> 3.  对{3，0}:子数组{arr[0]的前缀和，..arr[3]} = 5。后缀子数组的和{arr[3]，…，arr[0]} = 5。
> 
> **输入:** arr[] = {1，0，-1 }
> T3】输出: 1

**方法:**思路是用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)来解决这个问题。按照以下步骤解决问题:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并计算所有数组索引的**前缀和**，并将它们的频率存储在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中。
2.  [反向遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，一直计算到每个数组索引的**后缀和**。
3.  对于获得的每个后缀和，[检查它是否存在于地图中](https://www.geeksforgeeks.org/check-key-present-cpp-map-unordered_map/)。如果发现是真的，将**计数**增加 **1** 。
4.  打印获得的**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// index pairs having equal
// prefix and suffix sums
void countPairs(int* arr, int n)
{
    // Maps indices with prefix sums
    unordered_map<int, int> mp1;
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Update prefix sum
        sum += arr[i];

        // Update frequency in Map
        mp1[sum] += 1;
    }

    sum = 0;
    int ans = 0;

    // Traverse the array in reverse
    for (int i = n - 1; i >= 0; i--) {

        // Update suffix sum
        sum += arr[i];

        // Check if any prefix sum of
        // equal value exists or not
        if (mp1.find(sum) != mp1.end()) {
            ans += mp1[sum];
        }
    }

    // Print the obtained count
    cout << ans;
}

// Driver code
int main()
{

    // Given array
    int arr[] = { 1, 2, 1, 1 };

    // Given size
    int n = sizeof(arr)
            / sizeof(arr[0]);

    // Function Call
    countPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to find the count of
  // index pairs having equal
  // prefix and suffix sums
  static void countPairs(int []arr, int n)
  {

    // Maps indices with prefix sums
    HashMap<Integer,Integer> mp1 = new HashMap<Integer,Integer>();
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // Update prefix sum
      sum += arr[i];

      // Update frequency in Map
      if(mp1.containsKey(sum)){
        mp1.put(sum, mp1.get(sum)+1);
      }
      else{
        mp1.put(sum, 1);
      }
    }

    sum = 0;
    int ans = 0;

    // Traverse the array in reverse
    for (int i = n - 1; i >= 0; i--)
    {

      // Update suffix sum
      sum += arr[i];

      // Check if any prefix sum of
      // equal value exists or not
      if (mp1.containsKey(sum))
      {
        ans += mp1.get(sum);
      }
    }

    // Print the obtained count
    System.out.print(ans);
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 1, 2, 1, 1 };

    // Given size
    int n = arr.length;

    // Function Call
    countPairs(arr, n);
  }
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the count of
# index pairs having equal
# prefix and suffix sums
def countPairs(arr, n):

    # Maps indices with prefix sums
    mp1 = {}
    sum = 0

    # Traverse the array
    for i in range(n):

        # Update prefix sum
        sum += arr[i]

        # Update frequency in Map
        mp1[sum] = mp1.get(sum, 0) + 1

    sum = 0
    ans = 0

    # Traverse the array in reverse
    for i in range(n - 1, -1, -1):

        # Update suffix sum
        sum += arr[i]

        # Check if any prefix sum of
        # equal value exists or not
        if (sum in mp1):
            ans += mp1[sum]

    # Print the obtained count
    print (ans)

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 2, 1, 1 ]

    # Given size
    n = len(arr)

    # Function Call
    countPairs(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# code for above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to find the count of
  // index pairs having equal
  // prefix and suffix sums
  static void countPairs(int[] arr, int n)
  {

    // Maps indices with prefix sums
    Dictionary<int, int> mp1 = new Dictionary<int, int>();
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // Update prefix sum
      sum += arr[i];

      // Update frequency in Map
      if(mp1.ContainsKey(sum))
      {
        mp1.Add(sum, mp1[sum] + 1);
      }
      else{
        mp1.Add(sum, 1);
      }
    }

    sum = 0;
    int ans = 0;

    // Traverse the array in reverse
    for (int i = n - 1; i >= 0; i--)
    {

      // Update suffix sum
      sum += arr[i];

      // Check if any prefix sum of
      // equal value exists or not
      if (mp1.ContainsKey(sum))
      {
        ans += mp1[sum];
      }
    }

    // Print the obtained count
    Console.Write(ans);
  }

  // Driver code
  static public void Main ()
  {

    // Given array
    int[] arr = { 1, 2, 1, 1 };

    // Given size
    int n = arr.Length;

    // Function Call
    countPairs(arr, n);
  }
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the count of
// index pairs having equal
// prefix and suffix sums
function countPairs(arr, n)
{

    // Maps indices with prefix sums
    let mp1 = new Map();
    let sum = 0;

    // Traverse the array
    for(let i = 0; i < n; i++)
    {

        // Update prefix sum
        sum += arr[i];

        // Update frequency in Map
        if (mp1.has(sum))
        {
            mp1.set(sum, mp1.get(sum) + 1);
        }
        else
        {
            mp1.set(sum, 1)
        }
    }

    sum = 0;
    let ans = 0;

    // Traverse the array in reverse
    for(let i = n - 1; i >= 0; i--)
    {

        // Update suffix sum
        sum += arr[i];

        // Check if any prefix sum of
        // equal value exists or not
        if (mp1.has(sum))
        {
            ans += mp1.get(sum);
        }
    }

    // Print the obtained count
    document.write(ans);
}

// Driver code

// Given array
let arr = [ 1, 2, 1, 1 ];

// Given size
let n = arr.length

// Function Call
countPairs(arr, n);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)