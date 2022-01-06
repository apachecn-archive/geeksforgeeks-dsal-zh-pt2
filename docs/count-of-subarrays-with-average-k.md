# 平均 K 的子阵列计数

> 原文:[https://www . geeksforgeeks . org/子阵列计数平均值-k/](https://www.geeksforgeeks.org/count-of-subarrays-with-average-k/)

给定一个大小为 **N、**的[阵列](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是计算[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，其[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)正好等于 **k** 。

**示例:**

> **输入:** arr[ ] = {1，4，2，6，10}，N = 6，K = 4
> **输出:** 3
> **说明:**平均值等于 4 的子阵为{4}、{2，6}、{4，2，6}。
> 
> **输入:** arr[ ] = {12，5，3，10，4，8，10，12，-6，-1}，N = 10，K = 6
> **输出:** 4

**天真方法:**解决问题最简单的方法是遍历所有[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)并计算它们的[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)。如果他们的[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)为 **K，**则增加答案。

下面是天真方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count subarray having average
// exactly equal to K
int countKAverageSubarrays(int arr[], int n, int k)
{

    // To Store the final answer
    int res = 0;

    // Calculate all subarrays
    for (int L = 0; L < n; L++) {
        int sum = 0;
        for (int R = L; R < n; R++) {
            // Calculate required average
            sum += arr[R];
            int len = (R - L + 1);

            // Check if average
            // is equal to k
            if (sum % len == 0) {
                int avg = sum / len;

                // Required average found
                if (avg == k)

                    // Increment res
                    res++;
            }
        }
    }
    return res;
}

// Driver code
int main()
{
    // Given Input
    int K = 6;
    int arr[] = { 12, 5, 3, 10, 4, 8, 10, 12, -6, -1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countKAverageSubarrays(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG{

// Function to count subarray having average
// exactly equal to K
static int countKAverageSubarrays(int arr[], int n,
                                  int k)
{

    // To Store the final answer
    int res = 0;

    // Calculate all subarrays
    for(int L = 0; L < n; L++)
    {
        int sum = 0;
        for(int R = L; R < n; R++)
        {

            // Calculate required average
            sum += arr[R];
            int len = (R - L + 1);

            // Check if average
            // is equal to k
            if (sum % len == 0)
            {
                int avg = sum / len;

                // Required average found
                if (avg == k)

                    // Increment res
                    res++;
            }
        }
    }
    return res;
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int K = 6;
    int arr[] = { 12, 5, 3, 10, 4,
                   8, 10, 12, -6, -1 };
    int N = arr.length;

    // Function Call
    System.out.print(countKAverageSubarrays(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to count subarray having average
# exactly equal to K
def countKAverageSubarrays(arr, n, k):
    # To Store the final answer
    res = 0

    # Calculate all subarrays
    for L in range(n):
        sum = 0
        for R in range(L,n,1):
            # Calculate required average
            sum += arr[R]
            len1 = (R - L + 1)

            # Check if average
            # is equal to k
            if (sum % len1 == 0):
                avg = sum // len1

                # Required average found
                if (avg == k):

                    # Increment res
                    res += 1

    return res

# Driver code
if __name__ == '__main__':
    # Given Input
    K = 6
    arr = [12, 5, 3, 10, 4, 8, 10, 12, -6, -1]
    N = len(arr)

    # Function Call
    print(countKAverageSubarrays(arr, N, K))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count subarray having average
// exactly equal to K
static int countKAverageSubarrays(int []arr, int n, int k)
{

    // To Store the final answer
    int res = 0;

    // Calculate all subarrays
    for (int L = 0; L < n; L++)
    {
        int sum = 0;
        for (int R = L; R < n; R++)
        {

            // Calculate required average
            sum += arr[R];
            int len = (R - L + 1);

            // Check if average
            // is equal to k
            if (sum % len == 0) {
                int avg = sum / len;

                // Required average found
                if (avg == k)

                    // Increment res
                    res++;
            }
        }
    }
    return res;
}

// Driver code
public static void Main()
{
    // Given Input
    int K = 6;
    int []arr = { 12, 5, 3, 10, 4, 8, 10, 12, -6, -1 };
    int N = arr.Length;

    // Function Call
    Console.Write(countKAverageSubarrays(arr, N, K));
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to count subarray having average
// exactly equal to K
function countKAverageSubarrays(arr, n, k)
{

  // To Store the final answer
  let res = 0;

  // Calculate all subarrays
  for (let L = 0; L < n; L++)
  {
    let sum = 0;
    for (let R = L; R < n; R++)
    {

      // Calculate required average
      sum += arr[R];
      let len = R - L + 1;

      // Check if average
      // is equal to k
      if (sum % len == 0)
      {
        let avg = sum / len;

        // Required average found
        if (avg == k)
          // Increment res
          res++;
      }
    }
  }
  return res;
}

// Driver code

// Given Input
let K = 6;
let arr = [12, 5, 3, 10, 4, 8, 10, 12, -6, -1];
let N = arr.length;

// Function Call
document.write(countKAverageSubarrays(arr, N, K));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
4
```

***时间复杂度:** O(N^2)*
***辅助空间:** O(1)*

**有效方法:**有效的解决方案基于以下观察:

> 假设有一个[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)【L，R】的[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)等于 K，那么
> *= > K =平均值【L，R】= sum[0，R]–sum[0，L-1]/(R–L+1)*
> *=>(R–L+1)* K = sum[0，R]–sum[0，L–1]*
> *=> L–1]*
> *=>sum[0，R]–R * K = sum[0，L–1]–(L–1)* K*
> 
> 如果每个元素减少 **K** ，那么[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)也会减少 **K** 。所以[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)可以降为零，那么问题就变成了求[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)有[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)的个数等于**零**。
> [平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)只有在以下情况下才可能为零:
> *总和[0，R]–总和[0，L-1]/(R–L+1)= 0*
> *=>总和[0，R] =总和[0，L-1]*

按照以下步骤解决此问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说 **mp** 来存储数组 **arr[]的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的频率。**
*   初始化一个变量，比如说**curSum****结果**为 **0。**
*   [使用变量 **i:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代
    *   从当前元素中减去 **K** ，然后加到 **curSum。**
    *   如果 **curSum** 为 **0** ，[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的[平均值](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)等于 **0** ，那么将**结果**增加 **1** 。
    *   如果**光标**在使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)之前已经出现过。如果之前发生过，则将之前发生的次数加到**结果中，**然后**使用[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)增加**的频率。
*   完成以上步骤后，打印**结果**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count subarray having average
// exactly equal to K
int countKAverageSubarrays(int arr[], int n, int k)
{
    int result = 0, curSum = 0;

    // Store the frequency of prefix
    // sum of the array arr[]
    unordered_map<int, int> mp;

    for (int i = 0; i < n; i++) {
        // Subtract k from each element,
        // then add it to curSum
        curSum += (arr[i] - k);

        // If curSum is 0 that means
        // sum[0...i] is 0 so increment
        // res
        if (curSum == 0)
            result++;

        // Check if curSum has occurred
        // before and if it has occurred
        // before, add it's frequency to
        // res
        if (mp.find(curSum) != mp.end())
            result += mp[curSum];

        // Increment the frequency
        // of curSum
        mp[curSum]++;
    }

    // Return result
    return result;
}

// Driver code
int main()
{
    // Given Input
    int K = 6;
    int arr[] = { 12, 5, 3, 10, 4, 8, 10, 12, -6, -1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countKAverageSubarrays(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count subarray having average
// exactly equal to K
static int countKAverageSubarrays(int[] arr, int n,
                                  int k)
{
    int result = 1, curSum = 0;

    // Store the frequency of prefix
    // sum of the array arr[]
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    for(int i = 0; i < n; i++)
    {

        // Subtract k from each element,
        // then add it to curSum
        curSum += (arr[i] - k);

        // If curSum is 0 that means
        // sum[0...i] is 0 so increment
        // res
        if (curSum == 0)
            result++;

        // Check if curSum has occurred
        // before and if it has occurred
        // before, add it's frequency to
        // res
        if (mp.containsKey(curSum))
            result += mp.get(curSum);

        // Increment the frequency
        // of curSum
        mp.put(curSum, 1);
    }

    // Return result
    return result;
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int K = 6;
    int[] arr = { 12, 5, 3, 10, 4,
                  8, 10, 12, -6, -1 };
    int N = arr.length;

    // Function Call
    System.out.print(countKAverageSubarrays(arr, N, K));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to count subarray having average
# exactly equal to K
def countKAverageSubarrays(arr, n, k):

    result = 0
    curSum = 0

    # Store the frequency of prefix
    # sum of the array arr[]
    mp = dict()

    for i in range(0, n):

        # Subtract k from each element,
        # then add it to curSum
        curSum += (arr[i] - k)

        # If curSum is 0 that means
        # sum[0...i] is 0 so increment
        # res
        if (curSum == 0):
            result += 1

        # Check if curSum has occurred
        # before and if it has occurred
        # before, add it's frequency to
        # res
        if curSum in mp:
            result += mp[curSum]

        # Increment the frequency
        # of curSum
        if curSum in mp:
            mp[curSum] += 1
        else:
            mp[curSum] = 1

    # Return result
    return result

# Driver code
if __name__ == '__main__':

    # Given Input
    K = 6
    arr = [12, 5, 3, 10, 4, 8, 10, 12, -6, -1]
    N = len(arr)

    # Function Call
    print(countKAverageSubarrays(arr, N, K))

# This code is contributed by MuskanKalra1
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Function to count subarray having average
// exactly equal to K
static int countKAverageSubarrays(int[] arr, int n,
                                  int k)
{
    int result = 1, curSum = 0;

    // Store the frequency of prefix
    // sum of the array []arr
    Dictionary<int,
            int> mp = new Dictionary<int,
                                      int>();

    for(int i = 0; i < n; i++)
    {

        // Subtract k from each element,
        // then add it to curSum
        curSum += (arr[i] - k);

        // If curSum is 0 that means
        // sum[0...i] is 0 so increment
        // res
        if (curSum == 0)
            result++;

        // Check if curSum has occurred
        // before and if it has occurred
        // before, add it's frequency to
        // res
        if (mp.ContainsKey(curSum))
            result += mp[curSum];
        else
        // Increment the frequency
        // of curSum
        mp.Add(curSum, 1);
    }

    // Return result
    return result;
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int K = 6;
    int[] arr = { 12, 5, 3, 10, 4,
                  8, 10, 12, -6, -1 };
    int N = arr.Length;

    // Function Call
    Console.Write(countKAverageSubarrays(arr, N, K));
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

        // JavaScript Program for the above approach

        // Function to count subarray having average
        // exactly equal to K
        function countKAverageSubarrays(arr, n, k) {
            let result = 0, curSum = 0;

            // Store the frequency of prefix
            // sum of the array arr[]
            let mp = new Map();

            for (let i = 0; i < n; i++) {
                // Subtract k from each element,
                // then add it to curSum
                curSum += (arr[i] - k);

                // If curSum is 0 that means
                // sum[0...i] is 0 so increment
                // res
                if (curSum == 0) {
                    result++;
                }
                // Check if curSum has occurred
                // before and if it has occurred
                // before, add it's frequency to
                // res
                if (mp.has(curSum)) {
                    result += mp.get(curSum);
                }

                // Increment the frequency
                // of curSum
                if (mp.has(curSum)) {
                    mp.set(curSum, mp.get(curSum) + 1);
                }
                else {
                    mp.set(curSum, 1);
                }

            }

            // Return result
            return result;
        }

        // Driver code

        // Given Input
        let K = 6;
        let arr = [12, 5, 3, 10, 4, 8, 10, 12, -6, -1];
        let N = arr.length;

        // Function Call
        document.write(countKAverageSubarrays(arr, N, K));

    // This code is contributed by Potta Lokesh

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)