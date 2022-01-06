# 最长子序列的长度，使得相邻元素的异或等于 K

> 原文:[https://www . geeksforgeeks . org/最长子序列的长度使得相邻元素的异或等于-k/](https://www.geeksforgeeks.org/length-of-the-longest-subsequence-such-that-xor-of-adjacent-elements-is-equal-to-k/)

给定一个非负整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】****N**和一个整数 **K** ，其思想是找出相邻元素的[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **K** 的最长子序列的长度。

**示例:**

> **输入:** N = 5，arr[] = {3，2，4，3，5}，K = 1
> **输出:** 3
> **解释:**
> 所有相邻元素异或等于 K 的子序列为{3，2}、{2，3}、{4，5}、{3，2，3}。
> 因此，相邻元素异或为 1 的最长子序列的长度为 3。
> 
> **输入:** N = 8，arr[] = {4，5，4，7，3，5，4，6}，K = 2
> **输出:** 3
> **解释:**
> 所有相邻元素的 Xor 等于 K 的子序列为{4，6}、{5，7}、{7，5}、{5，7，5}。
> 因此，相邻元素异或为 1 的最长子序列的长度为 3

**天真方法:**想法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。给定的问题可以基于以下观察来解决:

> *   Let **DP (I)** represent the maximum length of [subsequence](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) ending with index **I** .
> *   Then, the transition from one state to another is as follows:
>     *   Find the index **j** so that **j < I** and **a [j] a [I] = k** .
>     *   阿胜， **Dp(i) =最大(Dp(j)+1，DP(I)]**

按照以下步骤解决问题:

*   初始化一个整数，比如说**和**，来存储最长子序列的长度，初始化一个数组，比如说 **dp[]** ，来存储 dp 状态。
*   将基本情况定义为 **dp[0] = 1。**
*   迭代范围 **[1，N-1]:**
    *   迭代范围**【0，I-1】**并将 **dp[i]** 更新为 **max(dp[i]，dp[j] + 1)** 如果 **a[i] ^ a[j] = K.**
    *   更新**年** as **最大值(年，dp[i])** 。
*   最后，打印最长子序列**和**的最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum length
// of subsequence having XOR of
// adjacent elements equal to K
int xorSubsequence(int a[], int n, int k)
{

  // Store maximum length of subsequence
  int ans = 0;

  // Stores the dp-states
  int dp[n] = {0};

  // Base case
  dp[0] = 1;

  // Iterate over the range [1, N-1]
  for (int i = 1; i < n; i++) {

    // Iterate over the range [0, i - 1]
    for (int j = i - 1; j >= 0; j--) {

      // If arr[i]^arr[j] == K
      if ((a[i] ^ a[j]) == k)

        // Update the dp[i]
        dp[i] = max(dp[i], dp[j] + 1);
    }

    // Update the maximum subsequence length
    ans = max(ans, dp[i]);
    dp[i] = max(1, dp[i]);
  }

  // If length of longest subsequence
  // is less than 2 then return 0
  return ans >= 2 ? ans : 0;
}

// Driver Code
int main()
{

  // Input
  int arr[] = { 3, 2, 4, 3, 5 };
  int K = 1;
  int N = sizeof(arr) / sizeof(arr[0]);

  // Print the length of longest subsequence
  cout << xorSubsequence(arr, N, K);
  return 0;
}

// This code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Function to find maximum length
    // of subsequence having XOR of
    // adjacent elements equal to K
    public static int xorSubsequence(int a[],
                                     int n, int k)
    {

        // Store maximum length of subsequence
        int ans = 0;

        // Stores the dp-states
        int dp[] = new int[n];

        // Base case
        dp[0] = 1;

        // Iterate over the range [1, N-1]
        for (int i = 1; i < n; i++) {

            // Iterate over the range [0, i - 1]
            for (int j = i - 1; j >= 0; j--) {

                // If arr[i]^arr[j] == K
                if ((a[i] ^ a[j]) == k)

                    // Update the dp[i]
                    dp[i] = Math.max(dp[i], dp[j] + 1);
            }
            // Update the maximum subsequence length
            ans = Math.max(ans, dp[i]);

            dp[i] = Math.max(1, dp[i]);
        }
        // If length of longest subsequence
        // is less than 2 then return 0
        return ans >= 2 ? ans : 0;
    }
    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int arr[] = { 3, 2, 4, 3, 5 };
        int K = 1;
        int N = arr.length;
        // Print the length of longest subsequence
        System.out.println(xorSubsequence(arr, N, K));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find maximum length
# of subsequence having XOR of
# adjacent elements equal to K
def xorSubsequence(a, n, k):

    # Store maximum length of subsequence
    ans = 0;

    # Stores the dp-states
    dp = [0] * n;

    # Base case
    dp[0] = 1;

    # Iterate over the range [1, N-1]
    for i in range(1, n):

        # Iterate over the range [0, i - 1]
        for j in range(i - 1, -1, -1):

            # If arr[i]^arr[j] == K
            if ((a[i] ^ a[j]) == k):

                # Update the dp[i]
                dp[i] = max(dp[i], dp[j] + 1);

        # Update the maximum subsequence length
        ans = max(ans, dp[i]);
        dp[i] = max(1, dp[i]);

    # If length of longest subsequence
    # is less than 2 then return 0
    return ans if ans >= 2 else 0;

# Driver Code
if __name__ == '__main__':

    # Input
    arr = [3, 2, 4, 3, 5];
    K = 1;
    N = len(arr);

    # Print the length of longest subsequence
    print(xorSubsequence(arr, N, K));

    # This code contributed by shikhasingrajput
```

## C#

```
// C# program of the above approach
using System;

class GFG{

// Function to find maximum length
// of subsequence having XOR of
// adjacent elements equal to K
static int xorSubsequence(int[] a, int n,
                          int k)
{

    // Store maximum length of subsequence
    int ans = 0;

    // Stores the dp-states
    int[] dp = new int[n];

    // Base case
    dp[0] = 1;

    // Iterate over the range [1, N-1]
    for(int i = 1; i < n; i++)
    {

        // Iterate over the range [0, i - 1]
        for(int j = i - 1; j >= 0; j--)
        {

            // If arr[i]^arr[j] == K
            if ((a[i] ^ a[j]) == k)

                // Update the dp[i]
                dp[i] = Math.Max(dp[i], dp[j] + 1);
        }

        // Update the maximum subsequence length
        ans = Math.Max(ans, dp[i]);

        dp[i] = Math.Max(1, dp[i]);
    }

    // If length of longest subsequence
    // is less than 2 then return 0
    return ans >= 2 ? ans : 0;
} 

// Driver code   
static void Main()
{

    // Input
    int[] arr = { 3, 2, 4, 3, 5 };
    int K = 1;
    int N = arr.Length;

    // Print the length of longest subsequence
    Console.WriteLine(xorSubsequence(arr, N, K)); 
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript program of the above approach

    // Function to find maximum length
    // of subsequence having XOR of
    // adjacent elements equal to K
    function xorSubsequence(a, n, k)
    {

        // Store maximum length of subsequence
        let ans = 0;

        // Stores the dp-states
        let dp = new Array(n);
        dp.fill(0);

        // Base case
        dp[0] = 1;

        // Iterate over the range [1, N-1]
        for(let i = 1; i < n; i++)
        {

            // Iterate over the range [0, i - 1]
            for(let j = i - 1; j >= 0; j--)
            {

                // If arr[i]^arr[j] == K
                if ((a[i] ^ a[j]) == k)

                    // Update the dp[i]
                    dp[i] = Math.max(dp[i], dp[j] + 1);
            }

            // Update the maximum subsequence length
            ans = Math.max(ans, dp[i]);

            dp[i] = Math.max(1, dp[i]);
        }

        // If length of longest subsequence
        // is less than 2 then return 0
        return ans >= 2 ? ans : 0;
    }

    let arr = [ 3, 2, 4, 3, 5 ];
    let K = 1;
    let N = arr.length;

    // Print the length of longest subsequence
    document.write(xorSubsequence(arr, N, K));

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过使用 Xor 和 [Hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 的[属性结合](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/)[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来存储以整数结尾的子序列的最大长度，从而在 [DP 中产生恒定的状态时间转换。](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)

*   初始化一个整数表示 **ans =0** 来存储最长子序列的长度，初始化一个数组表示**DP【】**来存储 [DP 的状态。](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 比如 **mp** 来存储以一个元素结束的最长长度的子序列。
*   将基本情况定义为 **dp[0] = 1** 并将配对 **{arr[0]，1}** 推入 **mp。**
*   迭代范围 **[1，N-1]:**
    *   从 HashMap **mp 中找出最长子序列的长度，比如说 **dpj** 在元素**arr【I】^k**处结束。**
    *   将 **dp[i]** 更新为 **max(dp[i]，dpj+1)** ，并更新 HashMap **mp 中以元素 **arr[i]** 结束的子序列的最长长度。**
    *   更新**年=最大(年，dp[i])。**
*   最后，打印最长子序列 **ans 的最大长度。**

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum length of subsequence
int xorSubsequence(int a[], int n, int k)
{

    // Stores maximum length of subsequence
    int ans = 0;

    // Dictionary to store the longest length of
    // subsequence ending at an integer, say X
    map<int, int> map;

    // Stores the maximum length of
    // subsequence ending at index i
    int dp[n] = {0};

    // Base case
    map[a[0]] = 1;
    dp[0] = 1;

    // Iterate over the range [1, N-1]
    for (int i = 1; i < n; i++)
    {

        int dpj;

        // Retrieve the longest length of
        // subsequence ending at integer []a^K
        if(map.find(a[i] ^ k) != map.end())
        {
            dpj = map[a[i] ^ k];
        }
        else{
            dpj = -1;
        }

        // If dpj is not NULL
        if (dpj != 0)

            // Update dp[i]
            dp[i] = max(dp[i], dpj + 1);

        // Update ans
        ans = max(ans, dp[i]);

        // Update the maximum length of subsequence
        // ending at element is a[i] in Dictionary
        if(map.find(a[i]) != map.end())
        {
            map[a[i]] = max(map[a[i]]+1, dp[i]);
        }
        else
        {
            map[a[i]] = max(1, dp[i]);
        }
    }

    // Return the ans if ans>=2.
    // Otherwise, return 0
    return ans >= 2 ? ans : 0;
}

int main()
{
    // Input
    int arr[] = { 3, 2, 4, 3, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 1;

    // Print the length of the longest subsequence
    cout << (xorSubsequence(arr, N, K));

    return 0;
}

// This code is contributed by divyesh072019.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to find maximum length of subsequence
  public static int xorSubsequence(int a[], int n, int k)
  {
    // Stores maximum length of subsequence
    int ans = 0;

    // HashMap to store the longest length of
    // subsequence ending at an integer, say X
    HashMap<Integer, Integer> map = new HashMap<>();

    // Stores the maximum length of
    // subsequence ending at index i
    int dp[] = new int[n];

    // Base case
    map.put(a[0], 1);
    dp[0] = 1;

    // Iterate over the range [1, N-1]
    for (int i = 1; i < n; i++) {

      // Retrieve the longest length of
      // subsequence ending at integer a[]^K
      Integer dpj = map.get(a[i] ^ k);

      // If dpj is not NULL
      if (dpj != null)

        // Update dp[i]
        dp[i] = Math.max(dp[i], dpj + 1);

      // Update ans
      ans = Math.max(ans, dp[i]);

      // Update the maximum length of subsequence
      // ending at element is a[i] in HashMap
      map.put(
        a[i],
        Math.max(map.getOrDefault(a[i], 1), dp[i]));
    }

    // Return the ans if ans>=2.
    // Otherwise, return 0
    return ans >= 2 ? ans : 0;
  }

  // Driver Code
  public static void main(String[] args)
  {
    // Input
    int arr[] = { 3, 2, 4, 3, 5 };
    int N = arr.length;
    int K = 1;

    // Print the length of the longest subsequence
    System.out.println(xorSubsequence(arr, N, K));
  }
}
```

## 蟒蛇 3

```
# Python 3 program for above approach

# Function to find maximum length of subsequence
def xorSubsequence( a, n, k):

    # Stores maximum length of subsequence
    ans = 0

    # HashMap to store the longest length of
    # subsequence ending at an integer, say X
    map = {}

    # Stores the maximum length of
    # subsequence ending at index i
    dp = [0]* n

    # Base case
    map[a[0]] =  1
    dp[0] = 1

    # Iterate over the range[1, N-1]
    for i in range(1, n):

        # Retrieve the longest length of
        # subsequence ending at integer a[] ^ K

        # If dpj is not NULL
        if (a[i] ^ k  in map):

            # Update dp[i]
               dp[i] = max(dp[i], map[a[i] ^ k] + 1)

        # Update ans
        ans = max(ans, dp[i])

        # Update the maximum length of subsequence
        # ending at element is a[i] in HashMap
        if a[i] in map:
              map[a[i]] = max(map[a[i]],dp[i])
        else:
            map[a[i]] = max(1, dp[i])

    # Return the ans if ans >= 2.
    # Otherwise, return 0
    if ans >= 2 :
      return ans
    return 0

# Driver Code
if __name__ == "__main__":

    # Input
    arr = [3, 2, 4, 3, 5]
    N = len(arr)
    K = 1

    # Print the length of the longest subsequence
    print(xorSubsequence(arr, N, K))

    # This code is contributed by chitranayal.
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

public class GFG
{

    // Function to find maximum length of subsequence
    public static int xorSubsequence(int []a, int n, int k)
    {

        // Stores maximum length of subsequence
        int ans = 0;

        // Dictionary to store the longest length of
        // subsequence ending at an integer, say X
        Dictionary<int, int> map = new Dictionary<int, int>();

        // Stores the maximum length of
        // subsequence ending at index i
        int []dp = new int[n];

        // Base case
        map.Add(a[0], 1);
        dp[0] = 1;

        // Iterate over the range [1, N-1]
        for (int i = 1; i < n; i++)
        {

            // Retrieve the longest length of
            // subsequence ending at integer []a^K
            int dpj = map.ContainsKey(a[i] ^ k)?map[a[i] ^ k]:-1;

            // If dpj is not NULL
            if (dpj != 0)

                // Update dp[i]
                dp[i] = Math.Max(dp[i], dpj + 1);

            // Update ans
            ans = Math.Max(ans, dp[i]);

            // Update the maximum length of subsequence
            // ending at element is a[i] in Dictionary
            if(map.ContainsKey(a[i]))
            {
                map[a[i]] = Math.Max(map[a[i]]+1, dp[i]); ;
            }
            else
            {
                map.Add(a[i], Math.Max(1, dp[i]));
            }
        }

        // Return the ans if ans>=2.
        // Otherwise, return 0
        return ans >= 2 ? ans : 0;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Input
        int []arr = { 3, 2, 4, 3, 5 };
        int N = arr.Length;
        int K = 1;

        // Print the length of the longest subsequence
        Console.WriteLine(xorSubsequence(arr, N, K));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to find maximum length of subsequence
function xorSubsequence(a, n, k)
{

    // Stores maximum length of subsequence
    var ans = 0;

    // Dictionary to store the longest length of
    // subsequence ending at an integer, say X
    var map = new Map();

    // Stores the maximum length of
    // subsequence ending at index i
    var dp = Array(n).fill(0);

    // Base case
    map.set(a[0], 1)
    dp[0] = 1;

    // Iterate over the range [1, N-1]
    for (var i = 1; i < n; i++)
    {

        var dpj;

        // Retrieve the longest length of
        // subsequence ending at integer []a^K
        if(map.has(a[i] ^ k))
        {
            dpj = map.get(a[i] ^ k);
        }
        else{
            dpj = -1;
        }

        // If dpj is not NULL
        if (dpj != 0)

            // Update dp[i]
            dp[i] = Math.max(dp[i], dpj + 1);

        // Update ans
        ans = Math.max(ans, dp[i]);

        // Update the maximum length of subsequence
        // ending at element is a[i] in Dictionary
        if(map.has(a[i]))
        {
            map.set(a[i] , Math.max(map.get(a[i])+1, dp[i]));
        }
        else
        {
            map.set(a[i], Math.max(1, dp[i]));
        }
    }

    // Return the ans if ans>=2.
    // Otherwise, return 0
    return ans >= 2 ? ans : 0;
}

// Input
var arr = [3, 2, 4, 3, 5];
var N = arr.length;
var K = 1;

// Print the length of the longest subsequence
document.write(xorSubsequence(arr, N, K));

// This code is contributed by famously.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N )