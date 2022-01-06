# 每组中相邻元素之和可被 K 整除的最小组数

> 原文:[https://www . geeksforgeeks . org/最小组数-这样相邻元素的和可被每组中的 k 整除/](https://www.geeksforgeeks.org/minimum-count-of-groups-such-that-sum-of-adjacent-elements-is-divisible-by-k-in-each-group/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是打印取数组元素形成的组的最小计数，使得每个组中相邻元素的和可被 **K** 整除。

**示例:**

> **输入:** arr[] = {2，6，5，8，2，9}，K = 2
> **输出:** 2
> 数组可以分为两组{2，6，2，8}和{5，9}。
> 每个组的相邻元素之和可被 k 整除。
> 因此，可以形成的组的最小数量是 2。
> 
> **输入:** arr[] = {1，1，4，4，8，6，7}，K = 8
> **输出:** 4
> **解释:**
> 数组可以分为 4 组:{1，7，1}、{4，4}、{8}和{6}。
> 每个组的相邻元素之和可被 k 整除。
> 因此，可以形成的最小组数是 4。
> 
> **输入:** arr[] = {144}，K = 5
> T3】输出: 1

**方法:**给定的问题可以基于以下观察来解决:

*   可以观察到，一个组应该形成为:
    1.  组应该只包含一个不能被 **K.** 整除的元素
    2.  组的所有元素都应该可以被 **K** 单独整除。
    3.  该组的每个相邻元素都应该得到满足； **X % K + Y % K = K** ，其中 **X** 和 **Y** 是该组的两个相邻元素。

按照以下步骤解决问题:

*   初始化一个[图< int，int>T1，说 **mp，**来存储**arr【I】% k 的计数**](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)
*   初始化一个变量，说 **ans** 为 **0，**存储组数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并增加 **mp** 中 **arr[i] % K** 的计数，如果 **arr[i] % K** 为 **0** ，则将 **1** 分配给 **ans** 。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，K/2】**并执行以下操作:
    *   将 **mp[i]** 和**MP[K–I]**的最小值存储在一个变量中，比如说 **C1。**
    *   将 **mp[i]** 和**MP[K–I]**的最大值存储在一个变量中，比如说 **C2。**
    *   如果 **C1** 为 **0** ，则通过 **C2** 递增 **ans** 。
    *   否则，如果 **C1** 等于 **C1** 或 **C1 + 1，**则以 **1** 递增 **ans** 。
    *   否则，将**和**增加**C2-C1-1。**
*   最后，完成上述步骤后，打印在**和**中获得的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of groups
int findMinGroups(int arr[], int N, int K)
{
    // Stores the count of elements
    unordered_map<int, int> mp;

    // Stores the count of groups
    int ans = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Update arr[i]
        arr[i] = arr[i] % K;

        // If arr[i] is 0
        if (arr[i] == 0) {

            // Update ans
            ans = 1;
        }
        else {

            // Increment mp[arr[i]] by 1
            mp[arr[i]]++;
        }
    }

    // Iterarte over the range [1, K / 2]
    for (int i = 1; i <= K / 2; i++) {

        // Stores the minimum of count of i
        // and K - i
        int c1 = min(mp[K - i], mp[i]);

        // Stores the maximum of count of i
        // and K - i
        int c2 = max(mp[K - i], mp[i]);

        // If c1 is 0
        if (c1 == 0) {

            // Increment ans by c2
            ans += c2;
        }

        // Otherwise if c2 is equal to c1 + 1
        // or c1
        else if (c2 == c1 + 1 || c1 == c2) {

            // Increment ans by 1
            ans++;
        }
        // Otherwise
        else {

            // Increment ans by c2 - c1 - 1
            ans += (c2 - c1 - 1);
        }
    }

    // Return the ans
    return ans;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 1, 4, 4, 8, 6, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 8;

    // Function Call
    cout << findMinGroups(arr, N, K);

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

    // Function to count the minimum number
    // of groups
    public static int findMinGroups(int arr[], int N, int K)
    {
        // Stores the count of elements
        HashMap<Integer, Integer> mp = new HashMap<>();

        // Stores the count of groups
        int ans = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // Update arr[i]
            arr[i] = arr[i] % K;

            // If arr[i] is 0
            if (arr[i] == 0) {

                // Update ans
                ans = 1;
            }
            else {

                // Increment mp[arr[i]] by 1
                if (!mp.containsKey(arr[i])) {
                    mp.put(arr[i], 1);
                }
                else {
                    Integer ct = mp.get(arr[i]);
                    if(ct!=null)
                    {
                        ct++;
                        mp.put(arr[i], ct);
                    }
                }
            }
        }

        // Iterarte over the range [1, K / 2]
        for (int i = 1; i <= K / 2; i++) {

            // Stores the minimum of count of i
            // and K - i
            int a=0,b=0;
            if(mp.containsKey(K-i)){
                a=mp.get(K-i);
            }
            if(mp.containsKey(i)){
                b=mp.get(i);
            }
            int c1 = Math.min(a, b);

            // Stores the maximum of count of i
            // and K - i
            int c2 = Math.max(a, b);

            // If c1 is 0
            if (c1 == 0) {

                // Increment ans by c2
                ans += c2;
            }

            // Otherwise if c2 is equal to c1 + 1
            // or c1
            else if (c2 == c1 + 1 || c1 == c2) {

                // Increment ans by 1
                ans++;
            }
            // Otherwise
            else {

                // Increment ans by c2 - c1 - 1
                ans += (c2 - c1 - 1);
            }
        }

        // Return the ans
        return ans;
    }
    public static void main (String[] args) {
        // Input
        int arr[] = { 1, 1, 4, 4, 8, 6, 7 };
        int N = 7;
        int K = 8;

        // Function Call
        System.out.println(findMinGroups(arr, N, K));
    }
}

// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum number
# of groups
def findMinGroups(arr, N, K):

    # Stores the count of elements
    mp = {}

    # Stores the count of groups
    ans = 0

    # Traverse the array arr[]
    for i in range(N):

        # Update arr[i]
        arr[i] = arr[i] % K

        # If arr[i] is 0
        if (arr[i] == 0):

            # Update ans
            ans = 1
        else:
            mp[arr[i]] = mp.get(arr[i], 0) + 1

    # Iterarte over the range [1, K / 2]
    for i in range(1, K // 2):

        # Stores the minimum of count of i
        # and K - i
        x, y = (0 if (K - i) not in mp else mp[K - i],
                      0 if i not in mp else mp[K - i])
        c1 = min(x, y)

        # The maximum of count of i
        # K - i
        c2 = max(x, y)

        # If c1 is 0
        if (c1 == 0):

            # Increment ans by c2
            ans += c2

        # Otherwise if c2 is equal to c1 + 1
        # or c1
        elif (c2 == c1 + 1 or c1 == c2):

            # Increment ans by 1
            ans += 1

        # Otherwise   
        else:

            # Increment ans by c2 - c1 - 1
            ans += (c2 - c1 - 1)

    # Return the ans
    return ans + 1

# Driver code
if __name__ == '__main__':

    # Input
    arr = [ 1, 1, 4, 4, 8, 6, 7 ]
    N = len(arr)
    K = 8

    # Function Call
    print(findMinGroups(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

    // Function to count the minimum number
    // of groups
     static int findMinGroups(int[] arr, int N, int K)
    {
        // Stores the count of elements
        Dictionary<int, int> mp = new Dictionary<int, int>();

        // Stores the count of groups
        int ans = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // Update arr[i]
            arr[i] = arr[i] % K;

            // If arr[i] is 0
            if (arr[i] == 0) {

                // Update ans
                ans = 1;
            }
            else {

                // Increment mp[arr[i]] by 1
                if (!mp.ContainsKey(arr[i])) {
                    mp.Add(arr[i], 1);
                }
                else {
                    int ct = mp[arr[i]];
                    if(ct!=0)
                    {
                        ct++;
                        mp[arr[i]]= ct;
                    }
                }
            }
        }

        // Iterarte over the range [1, K / 2]
        for (int i = 1; i <= K / 2; i++) {

            // Stores the minimum of count of i
            // and K - i
            int a=0,b=0;
            if(mp.ContainsKey(K-i)){
                a=mp[K-i];
            }
            if(mp.ContainsKey(i)){
                b=mp[i];
            }
            int c1 = Math.Min(a, b);

            // Stores the maximum of count of i
            // and K - i
            int c2 = Math.Max(a, b);

            // If c1 is 0
            if (c1 == 0) {

                // Increment ans by c2
                ans += c2;
            }

            // Otherwise if c2 is equal to c1 + 1
            // or c1
            else if (c2 == c1 + 1 || c1 == c2) {

                // Increment ans by 1
                ans++;
            }
            // Otherwise
            else {

                // Increment ans by c2 - c1 - 1
                ans += (c2 - c1 - 1);
            }
        }

        // Return the ans
        return ans;
    }
    static public void Main ()
    {
        // InAdd
        int[] arr = { 1, 1, 4, 4, 8, 6, 7 };
        int N = 7;
        int K = 8;

        // Function Call
        Console.Write(findMinGroups(arr, N, K));
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function to count the minimum number
       // of groups
       function findMinGroups(arr, N, K)
       {

           // Stores the count of elements
           let mp = new Map();

           // Stores the count of groups
           let ans = 0;

           // Traverse the array arr[]
           for (let i = 0; i < N; i++) {

               // Update arr[i]
               arr[i] = arr[i] % K;

               // If arr[i] is 0
               if (arr[i] == 0) {

                   // Update ans
                   ans = 1;
               }
               else {

                   // Increment mp[arr[i]] by 1
                   if (!mp.has(arr[i])) {
                       mp.set(arr[i], 1);
                   }
                   else {
                       let ct = mp.get(arr[i]);
                       if (ct != null) {
                           ct++;
                           mp.set(arr[i], ct);
                       }
                   }
               }
           }

           // Iterarte over the range [1, K / 2]
           for (let i = 1; i <= K / 2; i++) {

               // Stores the minimum of count of i
               // and K - i
               let a = 0, b = 0;
               if (mp.has(K - i)) {
                   a = mp.get(K - i);
               }
               if (mp.has(i)) {
                   b = mp.get(i);
               }
               let c1 = Math.min(a, b);

               // Stores the maximum of count of i
               // and K - i
               let c2 = Math.max(a, b);

               // If c1 is 0
               if (c1 == 0) {

                   // Increment ans by c2
                   ans += c2;
               }

               // Otherwise if c2 is equal to c1 + 1
               // or c1
               else if (c2 == c1 + 1 || c1 == c2) {

                   // Increment ans by 1
                   ans++;
               }
               // Otherwise
               else {

                   // Increment ans by c2 - c1 - 1
                   ans += (c2 - c1 - 1);
               }
           }

           // Return the ans
           return ans;
       }

       // Input
       let arr = [1, 1, 4, 4, 8, 6, 7];
       let N = 7;
       let K = 8;

       // Function Call
       document.write(findMinGroups(arr, N, K));

   // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(K)