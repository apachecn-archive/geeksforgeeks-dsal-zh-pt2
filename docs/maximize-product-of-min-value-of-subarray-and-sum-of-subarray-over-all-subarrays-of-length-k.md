# 最大化子阵列的最小值和所有长度为 K 的子阵列的子阵列之和的乘积

> 原文:[https://www . geeksforgeeks . org/最大化子阵列最小值乘积和子阵列长度 k 的总和/](https://www.geeksforgeeks.org/maximize-product-of-min-value-of-subarray-and-sum-of-subarray-over-all-subarrays-of-length-k/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在所有可能的具有 **K 个**元素的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中找到( **min * sum** 的最大可能值，其中 **min** 表示子阵列的最小整数， **sum** 表示子阵列的所有元素之和。

**例**:

> **输入** : arr[] = {1，2，3，2}，K = 3
> **输出** : 14
> **解释**:对于子阵{2，3，2}，给出的分数为 min(2，3，2) * sum(2，3，2) = 2 * 7 = 14，这是最大可能。
> 
> **输入** : arr[] = {3，1，5，6，4，2}，K = 2
> 输出 : 55

**逼近**:上述问题可以借助[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)解决，方法是在数组遍历过程中维护一个 **K** 元素的窗口，并分别跟踪变量**最小值**和**总和**中当前窗口中的最小元素和所有元素的总和。所有 **K** 大小的子阵列的最小值可以使用类似于这里[讨论的算法](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)的[多集数据结构](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)来计算，总和可以使用这里[讨论的算法](https://www.geeksforgeeks.org/find-maximum-minimum-sum-subarray-size-k/)来计算。所有 **K** 大小的窗户的**最小值*总和**的最大值是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to the maximum value of min * sum
// over all possible subarrays of K elements
int maxMinSum(vector<int> arr, int K)
{
    // Store the array size
    int N = arr.size();

    // Multiset data structure to calculate the
    // minimum over all K sized subarrays
    multiset<int> s;

    // Stores the sum of the surrent window
    int sum = 0;

    // Loop to calculate the sum and min of the
    // 1st window of size K
    for (int i = 0; i < K; i++) {
        s.insert(arr[i]);
        sum += arr[i];
    }

    // Stores the required answer
    int ans = sum * (*s.begin());

    // Loop to iterate over the remaining windows
    for (int i = K; i < N; i++) {

        // Add the current value and remove the
        // (i-K)th value from the sum
        sum += (arr[i] - arr[i - K]);

        // Update the set
        s.erase(s.find(arr[i - K]));
        s.insert(arr[i]);

        // Update answer
        ans = max(ans, sum * (*s.begin()));
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 3, 1, 5, 6, 4, 2 };
    int K = 2;

    cout << maxMinSum(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.HashSet;

class GFG {

    // Function to the maximum value of min * sum
    // over all possible subarrays of K elements
    public static int maxMinSum(int[] arr, int K)
    {

        // Store the array size
        int N = arr.length;

        // Multiset data structure to calculate the
        // minimum over all K sized subarrays
        HashSet<Integer> s = new HashSet<Integer>();

        // Stores the sum of the surrent window
        int sum = 0;

        // Loop to calculate the sum and min of the
        // 1st window of size K
        for (int i = 0; i < K; i++) {
            s.add(arr[i]);
            sum += arr[i];
        }

        // Stores the required answer
        int ans = sum * (s.iterator().next());

        // Loop to iterate over the remaining windows
        for (int i = K; i < N; i++) {

            // Add the current value and remove the
            // (i-K)th value from the sum
            sum += (arr[i] - arr[i - K]);

            // Update the set
            if (s.contains(arr[i - K]))
                s.remove(arr[i - K]);
            s.add(arr[i]);

            // Update answer
            ans = Math.max(ans, sum * (s.iterator().next()));
        }

        // Return Answer
        return ans;
    }

    // Driver Code
    public static void main(String args[]) {
        int[] arr = { 3, 1, 5, 6, 4, 2 };
        int K = 2;

        System.out.println(maxMinSum(arr, K));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python implementation for the above approach

# Function to the maximum value of min * sum
# over all possible subarrays of K elements
def maxMinSum(arr, K):

    # Store the array size
    N = len(arr)

    # Multiset data structure to calculate the
    # minimum over all K sized subarrays
    s = set()

    # Stores the sum of the surrent window
    sum = 0

    # Loop to calculate the sum and min of the
    # 1st window of size K
    for i in range(0, K):
        s.add(arr[i])
        sum += arr[i]

    # Stores the required answer
    ans = sum * (list(s)[0])

    # Loop to iterate over the remaining windows
    for i in range(K, N):

       # Add the current value and remove the
       # (i-K)th value from the sum
        sum += (arr[i] - arr[i - K])

        # Update the set
        if arr[i-K] in s:
            s.remove(arr[i-K])

        s.add(arr[i])

        # Update answer
        ans = max(ans, sum * (list(s)[0]))

        # Return Answer
    return ans

# Driver Code
if __name__ == "__main__":

    arr = [3, 1, 5, 6, 4, 2]
    K = 2

    print(maxMinSum(arr, K))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG {

    // Function to the maximum value of min * sum
    // over all possible subarrays of K elements
    public static int maxMinSum(int[] arr, int K)
    {

        // Store the array size
        int N = arr.Length;

        // Multiset data structure to calculate the
        // minimum over all K sized subarrays
        HashSet<int> s = new HashSet<int>();

        // Stores the sum of the surrent window
        int sum = 0;

        // Loop to calculate the sum and min of the
        // 1st window of size K
        for (int i = 0; i < K; i++) {
            s.Add(arr[i]);
            sum += arr[i];
        }

        // Stores the required answer
        int ans = sum * (s.ToList<int>()[0]);

        // Loop to iterate over the remaining windows
        for (int i = K; i < N; i++) {

            // Add the current value and remove the
            // (i-K)th value from the sum
            sum += (arr[i] - arr[i - K]);

            // Update the set
            if (s.Contains(arr[i - K]))
                s.Remove(arr[i - K]);
            s.Add(arr[i]);

            // Update answer
            ans = Math.Max(ans, sum * (s.ToList<int>()[0]));
        }

        // Return Answer
        return ans;
    }

    // Driver Code
    public static void Main() {
        int[] arr = { 3, 1, 5, 6, 4, 2 };
        int K = 2;

        Console.Write(maxMinSum(arr, K));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach
       function MultiSet() {
           let tm = {}; // treemap: works for key >= 0
           return { add, erase, first }
           function add(x) {
               tm[x] ? tm[x]++ : tm[x] = 1;
           }

           function erase(x) {
               delete tm[x];
           }

           function first() {
               let a = Object.keys(tm);
               return a[0] - '0';
           }

       }

       // Function to the maximum value of min * sum
       // over all possible subarrays of K elements
       function maxMinSum(arr, K) {
           // Store the array size
           let N = arr.length;

           // Multiset data structure to calculate the
           // minimum over all K sized subarrays
           let s = new MultiSet();

           // Stores the sum of the surrent window
           let sum = 0;

           // Loop to calculate the sum and min of the
           // 1st window of size K
           for (let i = 0; i < K; i++) {
               s.add(arr[i]);
               sum += arr[i];
           }

           // Stores the required answer
           let ans = sum * (s.first());

           // Loop to iterate over the remaining windows
           for (let i = K; i < N; i++) {

               // Add the current value and remove the
               // (i-K)th value from the sum
               sum += (arr[i] - arr[i - K]);

               // Update the set
               s.erase(arr[i - K]);
               s.add(arr[i]);

               // Update answer
               ans = Math.max(ans, sum * (s.first()));
           }

           // Return Answer
           return ans;
       }

       // Driver Code

       let arr = [3, 1, 5, 6, 4, 2];
       let K = 2;

       document.write(maxMinSum(arr, K));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
55
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*