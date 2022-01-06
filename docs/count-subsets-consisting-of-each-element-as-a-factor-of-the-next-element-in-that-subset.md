# 将每个元素组成的子集计数为该子集中下一个元素的因子

> 原文:[https://www . geesforgeks . org/count-subset-由每个元素作为该子集中下一个元素的因子组成/](https://www.geeksforgeeks.org/count-subsets-consisting-of-each-element-as-a-factor-of-the-next-element-in-that-subset/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出数组中存在的非空子集的数量，使得子集中除最后一个之外的每个元素都是该子集中下一个相邻元素的因子。**子集中的元素可以重新排列**，因此，如果子集的任何重新排列满足条件，那么该子集将被计算在内。但是，这个子集应该只计算一次。

**示例:**

> **输入:** arr[] = {2，3，6，8}
> **输出:** 7
> **解释:**
> 所需子集为:{2}、{3}、{6}、{8}、{2，6}、{8，2}、{3，6}。
> 由于子集{2}、{3}、{6}、{8}包含一个数字，因此它们包含在答案中。
> 在子集{2，6}中，2 是 6 的因子。
> 在子集{3，6}中，3 是 6 的因子。
> {8，2}重新排列成{2，8}时，满足要求的条件。
> 
> **输入:** arr[] = {16，18，6，7，2，19，20，9}
> **输出:** 15

**天真方法:**最简单的想法是[生成数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)并打印那些子集的计数，这些子集的相邻元素 **(arr[i]，arr[i + 1])** ， **arr[i]** 是 **arr[i + 1]** 的因子。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Function to calculate each subset
// for the array using bit masking
set<int> getSubset(int n, int* arr,
                   int mask)
{
    // Stores the unique elements
    // of the array arr[]
    set<int> subset;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Get the ith bit of the mask
        int b = (mask & (1 << i));

        // ith bit of mask is set then
        // include the corresponding
        // element in subset
        if (b != 0) {
            subset.insert(arr[i]);
        }
    }
    return subset;
}

// Function to count the subsets
// that satisfy the given condition
int countSets(int n, set<int>* power_set)
{
    // Store the count of subsets
    int count = 0;

    // Iterate through all the sets
    // in the power set
    for (int i = 1; i < (1 << n); i++) {

        // Initially, set flag as true
        bool flag = true;

        int N = power_set[i].size();

        // Convert the current subset
        // into an array
        int* temp = new int[N];

        auto it = power_set[i].begin();

        for (int j = 0;
             it != power_set[i].end();
             j++, it++) {
            temp[j] = *it;
        }

        // Check for any index, i,
        // a[i] is a factor of a[i+1]
        for (int k1 = 1, k0 = 0; k1 < N;) {

            if (temp[k1] % temp[k0] != 0) {
                flag = false;
                break;
            }
            if (k0 > 0)
                k0--;
            else {
                k1++;
                k0 = k1 - 1;
            }
        }

        // If flag is stil set, then
        // update the count
        if (flag)
            count = 1LL * (count + 1) % mod;

        delete[] temp;
    }

    // Return the final count
    return count;
}

// Function to generate power set of
// the given array arr[]
void generatePowerSet(int arr[], int n)
{

    // Declare power set of size 2^n
    set<int>* power_set
        = new set<int>[1 << n];

    // Represent each subset using
    // some mask
    int mask = 0;
    for (int i = 0; i < (1 << n); i++) {
        power_set[i] = getSubset(n, arr, mask);
        mask++;
    }

    // Find the required number of
    // subsets
    cout << countSets(n, power_set) % mod;

    delete[] power_set;
}

// Driver Code
int main()
{
    int arr[] = { 16, 18, 6, 7, 2, 19, 20, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    generatePowerSet(arr, N);

    return 0;
}
```

**Output:** 

```
15
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

[**HashMap**](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) **基于方法:**为了优化上述方法，想法是使用一个 [hashmap](https://www.geeksforgeeks.org/hashing-data-structure/) 和一个数组**DP【】**以排序的方式存储数组元素，并保持子集的计数。对于索引 **i，dp[arr[i]]** 将存储满足以索引 **i** 结束的给定条件的所有子集的数量。按照以下步骤解决问题:

*   将 **cnt** 初始化为 **0** 以存储所需子集的数量。
*   为范围**【0，N–1】**内的每一个 **i** 初始化一个哈希表， **dp** 并用 **1** 标记**DP【arr[I]】**。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**DP【】**并从 **i** 开始嵌套遍历开始使用迭代器 **j** ，如果 **i** 不等于 **j** ，且 **j** 处的元素是 **i** 处元素的因子，则更新 **dp[i] += dp[j]** 。
*   再次，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并将 **cnt** 更新为 **cnt += dp[i]** 。
*   完成上述步骤后，打印 **cnt** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Function that counts subsets whose
// every element is divisible by the
// previous adjacent element
void countSets(int* arr, int n)
{
    // Declare a map
    map<int, int> dp;

    // Initialise dp[arr[i]] with 1
    for (int i = 0; i < n; i++)
        dp[arr[i]] = 1;

    // Traverse the map till end
    map<int, int>::iterator i = dp.begin();

    for (; i != dp.end(); i++) {

        // Traverse the map from i to
        // begin using iterator j
        map<int, int>::iterator j = i;

        for (; j != dp.begin(); j--) {

            if (i == j)
                continue;

            // Check if condition is true
            if (i->first % j->first == 0) {

                // If factor found, append
                // i at to all subsets
                i->second
                    = (i->second % mod
                       + j->second % mod)
                      % mod;
            }
        }

        // Check for the first element
        // of the map
        if (i != j
            && i->first % j->first == 0) {
            i->second
                = (i->second % mod
                   + j->second % mod)
                  % mod;
        }
    }

    // Store count of required subsets
    int cnt = 0;

    // Traverse the map
    for (i = dp.begin(); i != dp.end(); i++)

        // Update the cnt variable
        cnt = (cnt % mod
               + i->second % mod)
              % mod;

    // Print the result
    cout << cnt % mod;
}

// Driver Code
int main()
{
    int arr[] = { 16, 18, 6, 7, 2, 19, 20, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countSets(arr, N);

    return 0;
}
```

**Output:** 

```
15
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效途径:**对上述途径进行优化，思路是使用类似于厄拉多塞的[筛的概念。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   创建一个数组**筛选掉数组中最大元素[大小的[]](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)** (比如说 **maxE** )， **arr[]** ，并用 **0s** 初始化。
*   设置**筛[i] = 1** ，其中 **i** 是数组的元素。
*   [使用变量 I 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **筛【】**到范围**【1，MaxE】**，如果**筛【I】**的值为正，那么如果筛【j】为正，则将**筛【I】**加到 I(比如 j)的所有倍数上。
*   完成上述步骤后，打印数组 **筛【】**元素的[和作为结果。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

// Function to find number of subsets
// satisfying the given condition
void countSets(int* arr, int n)
{
    // Stores number of required sets
    int cnt = 0;

    // Stores maximum element of arr[]
    // that defines the size of sieve
    int maxE = -1;

    // Iterate through the arr[]
    for (int i = 0; i < n; i++) {

        // If current element > maxE,
        // then update maxE
        if (maxE < arr[i])
            maxE = arr[i];
    }

    // Declare an array sieve of size N + 1
    int* sieve = new int[maxE + 1];

    // Initialize with all 0s
    for (int i = 0; i <= maxE; i++)
        sieve[i] = 0;

    // Mark all elements corresponding in
    // the array, by one as there will
    // always exists a singleton set
    for (int i = 0; i < n; i++)
        sieve[arr[i]] = 1;

    // Iterate from range [1, N]
    for (int i = 1; i <= maxE; i++) {

        // If element is present in array
        if (sieve[i] != 0) {

            // Traverse through all its
            // multiples <= n
            for (int j = i * 2; j <= maxE; j += i) {

                // Update them if they
                // are present in array
                if (sieve[j] != 0)
                    sieve[j] = (sieve[j] + sieve[i])
                               % mod;
            }
        }
    }

    // Iterate from the range [1, N]
    for (int i = 0; i <= maxE; i++)

        // Update the value of cnt
        cnt = (cnt % mod + sieve[i] % mod) % mod;

    delete[] sieve;

    // Print the result
    cout << cnt % mod;
}

// Driver Code
int main()
{
    int arr[] = { 16, 18, 6, 7, 2, 19, 20, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countSets(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

  static int mod = 1000000007;

  // Function to find number of subsets
  // satisfying the given condition
  static void countSets(int arr[], int n)
  {
    // Stores number of required sets
    int cnt = 0;

    // Stores maximum element of arr[]
    // that defines the size of sieve
    int maxE = -1;

    // Iterate through the arr[]
    for (int i = 0; i < n; i++) {

      // If current element > maxE,
      // then update maxE
      if (maxE < arr[i])
        maxE = arr[i];
    }

    // Declare an array sieve of size N + 1
    int sieve[] = new int[maxE + 1];

    // Mark all elements corresponding in
    // the array, by one as there will
    // always exists a singleton set
    for (int i = 0; i < n; i++)
      sieve[arr[i]] = 1;

    // Iterate from range [1, N]
    for (int i = 1; i <= maxE; i++) {

      // If element is present in array
      if (sieve[i] != 0) {

        // Traverse through all its
        // multiples <= n
        for (int j = i * 2; j <= maxE; j += i) {

          // Update them if they
          // are present in array
          if (sieve[j] != 0)
            sieve[j]
            = (sieve[j] + sieve[i]) % mod;
        }
      }
    }

    // Iterate from the range [1, N]
    for (int i = 0; i <= maxE; i++)

      // Update the value of cnt
      cnt = (cnt % mod + sieve[i] % mod) % mod;

    // Print the result
    System.out.println(cnt % mod);
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 16, 18, 6, 7, 2, 19, 20, 9 };
    int N = arr.length;

    // Function Call
    countSets(arr, N);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
#mod 1000000007

# Function to find number of subsets
# satisfying the given condition
def countSets(arr, n):

    # Stores number of required sets
    cnt = 0

    # Stores maximum element of arr[]
    # that defines the size of sieve
    maxE = -1

    # Iterate through the arr[]
    for i in range(n):

        # If current element > maxE,
        # then update maxE
        if (maxE < arr[i]):
            maxE = arr[i]

    # Declare an array sieve of size N + 1
    sieve = [0]*(maxE + 1)

    # Mark all elements corresponding in
    # the array, by one as there will
    # always exists a singleton set
    for i in range(n):
        sieve[arr[i]] = 1

    # Iterate from range [1, N]
    for i in range(1, maxE + 1):

        # If element is present in array
        if (sieve[i] != 0):

            # Traverse through all its
            # multiples <= n
            for j in range(i * 2, maxE + 1, i):

                # Update them if they
                # are present in array
                if (sieve[j] != 0):
                    sieve[j] = (sieve[j] + sieve[i])% 1000000007

    # Iterate from the range [1, N]
    for i in range(maxE + 1):

        # Update the value of cnt
        cnt = (cnt % 1000000007 + sieve[i] % 1000000007) % 1000000007

    #delete[] sieve

    # Prthe result
    print (cnt % 1000000007)

# Driver Code
if __name__ == '__main__':
    arr =[16, 18, 6, 7, 2, 19, 20, 9]
    N = len(arr)

    # Function Call
    countSets(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# Program to implement
// the above approach
using System;

class GFG {

  static int mod = 1000000007;

  // Function to find number of subsets
  // satisfying the given condition
  static void countSets(int[] arr, int n)
  {
    // Stores number of required sets
    int cnt = 0;

    // Stores maximum element of arr[]
    // that defines the size of sieve
    int maxE = -1;

    // Iterate through the arr[]
    for (int i = 0; i < n; i++) {

      // If current element > maxE,
      // then update maxE
      if (maxE < arr[i])
        maxE = arr[i];
    }

    // Declare an array sieve of size N + 1
    int[] sieve = new int[maxE + 1];

    // Mark all elements corresponding in
    // the array, by one as there will
    // always exists a singleton set
    for (int i = 0; i < n; i++)
      sieve[arr[i]] = 1;

    // Iterate from range [1, N]
    for (int i = 1; i <= maxE; i++) {

      // If element is present in array
      if (sieve[i] != 0) {

        // Traverse through all its
        // multiples <= n
        for (int j = i * 2; j <= maxE; j += i) {

          // Update them if they
          // are present in array
          if (sieve[j] != 0)
            sieve[j]
            = (sieve[j] + sieve[i]) % mod;
        }
      }
    }

    // Iterate from the range [1, N]
    for (int i = 0; i <= maxE; i++)

      // Update the value of cnt
      cnt = (cnt % mod + sieve[i] % mod) % mod;

    // Print the result
    Console.WriteLine(cnt % mod);
  }

  // Driver Code
  public static void Main(string[] args)
  {

    int[] arr = { 16, 18, 6, 7, 2, 19, 20, 9 };
    int N = arr.Length;

    // Function Call
    countSets(arr, N);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

let mod = 1000000007;

// Function to find number of subsets
  // satisfying the given condition
function countSets(arr,n)
{
    // Stores number of required sets
    let cnt = 0;

    // Stores maximum element of arr[]
    // that defines the size of sieve
    let maxE = -1;

    // Iterate through the arr[]
    for (let i = 0; i < n; i++) {

      // If current element > maxE,
      // then update maxE
      if (maxE < arr[i])
        maxE = arr[i];
    }

    // Declare an array sieve of size N + 1
    let sieve = new Array(maxE + 1);
     for(let i=0;i<maxE + 1;i++)
    {
        sieve[i]=0;
    }

    // Mark all elements corresponding in
    // the array, by one as there will
    // always exists a singleton set
    for (let i = 0; i < n; i++)
      sieve[arr[i]] = 1;

    // Iterate from range [1, N]
    for (let i = 1; i <= maxE; i++) {

      // If element is present in array
      if (sieve[i] != 0) {

        // Traverse through all its
        // multiples <= n
        for (let j = i * 2; j <= maxE; j += i) {

          // Update them if they
          // are present in array
          if (sieve[j] != 0)
            sieve[j]
            = (sieve[j] + sieve[i]) % mod;
        }
      }
    }

    // Iterate from the range [1, N]
    for (let i = 0; i <= maxE; i++)

      // Update the value of cnt
      cnt = (cnt % mod + sieve[i] % mod) % mod;

    // Print the result
    document.write(cnt % mod+"<br>");
}

// Driver Code
let arr=[16, 18, 6, 7, 2, 19, 20, 9 ];
let N = arr.length;

// Function Call
countSets(arr, N);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
15
```

***时间复杂度:**O(maxE * log(log(maxE)))*
***辅助空间:** O(maxE)*