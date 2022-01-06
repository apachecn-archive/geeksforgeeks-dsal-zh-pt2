# 最小化由唯一元素组成的 K 个等长子集的不相容性之和

> 原文:[https://www . geeksforgeeks . org/最小化 k 等长子集的不兼容性总和-由唯一元素组成/](https://www.geeksforgeeks.org/minimize-sum-of-incompatibilities-of-k-equal-length-subsets-made-up-of-unique-elements/)

给定一个由 **N** 个整数和一个整数 **K、**组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找出具有唯一元素的相等大小的 **K** 个子集的不兼容性的最小和。

> 集合中最大元素和最小元素之间的差异被称为集合的**不兼容性。**

**示例:**

> **输入:** arr[] = {1，2，1，4}，K = 2
> **输出:** 4
> **解释:**
> 将数组分配到 K(即 2)个子集的一种可能方式是{1，2}和{1，4}。
> 第一个子集的不相容性=(2–1)= 1。
> 第二子集的不相容性=(4–1)= 3。
> 因此，两个子集不相容的总和= 1 + 3 = 4，这是所有可能性中的最小值。
> 
> **输入:** arr[] = {6，3，8，1，3，1，2，2}，K = 4
> **输出:** 6
> **解释:**
> 将数组分配到 K 个子集的一种可能方式是:{1，2}、{2，3}、{6，8}、{1，3}。
> 第一子集的不相容性= (2-1) = 1。
> 第二子集的不相容性= (3-2) = 1。
> 第三子集的不相容性= (8-6) = 2。
> 第四子集的不相容性= (3-1) = 2。
> 因此，K 子集的不相容性总和= 1 + 1 + 2 + 2 = 6。这也是所有可能性中的最小值

**朴素方法:**最简单的方法是[递归遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，在每次递归中[使用位掩码](https://www.geeksforgeeks.org/iterating-over-all-possible-combinations-in-an-array-using-bits/)遍历选择数组 N/K 元素的所有可能方式，计算该子集的不兼容性，然后返回所有方式中的最小值。

***时间复杂度:**O(N * 2<sup>3 * N</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法可以使用[动态规划进行优化。](https://www.geeksforgeeks.org/dynamic-programming/)给定的问题可以基于以下观察来解决:

*   可以观察到，它需要具有位屏蔽的 2 状态[动态编程](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)说 **DP(屏蔽，i)** 来解决其中 **i** 表示阵列的当前位置并且**屏蔽的每个二进制位**表示元素是否已经被选择的问题。
*   过渡状态将包括通过选择尺寸 **N/K** 的子集来计算不兼容性。
    *   假设 **X** 和 **Y** 是当前设置的最小值和最大值，**新掩码**是另一个变量，其值最初作为**掩码**
    *   现在，标记所有已经选中的 ***N/*** **K** 元素在**新蒙版**中只出现一次，然后 **DP(蒙版，i)** 由**(Y–X+min(DP(新蒙版，i + 1)，DP(蒙版，I))**计算。

按照以下步骤解决问题:

*   初始化一个 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)，说 **dp[][]** 。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如说 **dfs (mask，i)** ，来计算结果:
    *   **基本情况:**如果 **i > K** ，则返回 **0** 。
    *   检查 **dp 是否【屏蔽】【I】！= -1** ，然后返回 **dp【掩码】【I】**，因为当前状态已经计算好了。
    *   使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)从数组中选择 **N/K** 元素，如果有可能选择子集的 **i** 元素，该元素只出现一次，并且还不是其他子集的一部分，则更新当前的 **dp** 状态为:

> **dp[mask][i] = min(dp[mask][i]，y–x+DFS(new mask，I)]**

*   返回 **dp【掩码】【I】**的值作为当前递归调用的结果。
*   调用递归函数 **dfs(2 <sup>N</sup> -1，0)** 并打印其返回的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
int k;
int n;
int goal;
vector<vector<int>> dp;
vector<int> bits;

// Recursive function to find
// the minimum required value
int dfs(vector<int> A, int state,int index)
{

    // Base Case
    if (index >= k)
    {
        return 0;
    }

    // Stores the minimum value
    // of the current state
    int res = 1000;

    // If dp[state][index] is
    // already calculated
    if (dp[state][index] != -1) {

        // return dp[state][index]
        return dp[state][index];
    }

    // Traverse over all the bits
    for (int bit : bits) {

        // If count of set bit is N/K
        if (__builtin_popcount(bit)
            == goal) {

            // Store the new state after
            // choosing N/K elements
            int newstate = state;

            // Stores the minimum and
            // maximum of current subset
            int mn = 100, mx = -1;

            // Stores if the elements
            // have been already
            // selected or not
            vector<bool> visit(n+1,false);

            // Stores if it is possible
            // to select N/K elements
            bool good = true;

            // Traverse over the array
            for (int j = 0; j < n; j++) {

                // If not chosen already
                // for another subset
                if ((bit & (1 << j)) != 0) {

                    // If already chosen
                    // for another subset
                    // or current subset
                    if (visit[A[j]] == true
                        || (state & (1 << j)) == 0) {

                        // Mark the good false
                        good = false;
                        break;
                    }

                    // Mark the current
                    // number visited
                    visit[A[j]] = true;

                    // Mark the current
                    // position in mask
                    // newstate
                    newstate = newstate
                               ^ (1 << j);

                    // Update the maximum
                    // and minimum
                    mx = max(mx,
                                  A[j]);
                    mn = min(mn,
                                  A[j]);
                }
            }

            // If good is true then
            // Update the res
            if (good) {
                res = min(
                    res, mx - mn
                             + dfs(A, newstate,
                                   index + 1));
            }
        }
    }

    // Update the current sp state
    dp[state][index] = res;

    // Return the res
    return res;
}

// Function to find the minimum
// incompatibility sum
int minimumIncompatibility(vector<int> A, int K)
{
    n = A.size();
    k = K;
    goal = n / k;

    // Stores the count of element
    map<int, int> mp;

    // Traverse the array
    for (int i : A) {

        // If number i not occurs
        // in Map
        if (mp.find(i)!=mp.end()){
            // Put the element
            // in the Map
            mp[i] = 0;
          }

        // Increment the count of
        // i in the Hash Map
        mp[i]++;

        // If count of i in Map is
        // greater than K then
        // return -1
        if (mp[i] > k)
            return -1;
    }

    // Stores all total state
    int state = (1 << n) - 1;

    // Traverse over all the state
    for (int i = 0; i <= state; i++) {

        // If number of set bit
        // is equal to N/K
        if (__builtin_popcount(i) == goal)
            bits.push_back(i);
    }

    // Stores the minimum value
    // at a state
    dp.resize(1<<n,vector<int>(k,-1));

    // Initialize the dp state
    // with -1
    // for (int i = 0;
    //      i < dp.ize(); i++) {
    //     Arrays.fill(dp[i], -1);
    // }

    // Call the recursive function
    return dfs(A, state, 0);
}

// Driver code
int main()
{

    vector<int> arr = { 1, 2, 1, 4 };
    int K = 2;

    // Function Call
    cout<<(minimumIncompatibility(arr, K));
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class Solution {
    int k;
    int n;
    int goal;
    int dp[][];
    List<Integer> bits = new ArrayList<>();

    // Function to find the minimum
    // incompatibility sum
    public int minimumIncompatibility(
        int[] A, int k)
    {
        this.n = A.length;
        this.k = k;
        goal = n / k;

        // Stores the count of element
        Map<Integer, Integer> map
            = new HashMap<>();

        // Traverse the array
        for (int i : A) {

            // If number i not occurs
            // in Map
            if (!map.containsKey(i))

                // Put the element
                // in the Map
                map.put(i, 0);

            // Increment the count of
            // i in the Hash Map
            map.put(i, map.get(i) + 1);

            // If count of i in Map is
            // greater than K then
            // return -1
            if (map.get(i) > k)
                return -1;
        }

        // Stores all total state
        int state = (1 << n) - 1;

        // Traverse over all the state
        for (int i = 0; i <= state; i++) {

            // If number of set bit
            // is equal to N/K
            if (Integer.bitCount(i) == goal)
                bits.add(i);
        }

        // Stores the minimum value
        // at a state
        dp = new int[1 << n][k];

        // Initialize the dp state
        // with -1
        for (int i = 0;
             i < dp.length; i++) {
            Arrays.fill(dp[i], -1);
        }

        // Call the recursive function
        return dfs(A, state, 0);
    }

    // Recursive function to find
    // the minimum required value
    public int dfs(int A[], int state,
                   int index)
    {
        // Base Case
        if (index >= k) {
            return 0;
        }

        // Stores the minimum value
        // of the current state
        int res = 1000;

        // If dp[state][index] is
        // already calculated
        if (dp[state][index] != -1) {

            // return dp[state][index]
            return dp[state][index];
        }

        // Traverse over all the bits
        for (int bit : bits) {

            // If count of set bit is N/K
            if (Integer.bitCount(bit)
                == goal) {

                // Store the new state after
                // choosing N/K elements
                int newstate = state;

                // Stores the minimum and
                // maximum of current subset
                int mn = 100, mx = -1;

                // Stores if the elements
                // have been already
                // selected or not
                boolean visit[]
                    = new boolean[n + 1];

                // Stores if it is possible
                // to select N/K elements
                boolean good = true;

                // Traverse over the array
                for (int j = 0; j < n; j++) {

                    // If not chosen already
                    // for another subset
                    if ((bit & (1 << j)) != 0) {

                        // If already chosen
                        // for another subset
                        // or current subset
                        if (visit[A[j]] == true
                            || (state & (1 << j)) == 0) {

                            // Mark the good false
                            good = false;
                            break;
                        }

                        // Mark the current
                        // number visited
                        visit[A[j]] = true;

                        // Mark the current
                        // position in mask
                        // newstate
                        newstate = newstate
                                   ^ (1 << j);

                        // Update the maximum
                        // and minimum
                        mx = Math.max(mx,
                                      A[j]);
                        mn = Math.min(mn,
                                      A[j]);
                    }
                }

                // If good is true then
                // Update the res
                if (good) {
                    res = Math.min(
                        res, mx - mn
                                 + dfs(A, newstate,
                                       index + 1));
                }
            }
        }

        // Update the current sp state
        dp[state][index] = res;

        // Return the res
        return res;
    }
}

// Driver Code
class GFG {

    public static void main(String[] args)
    {
        Solution st = new Solution();
        int[] arr = { 1, 2, 1, 4 };
        int K = 2;

        // Function Call
        System.out.print(
            st.minimumIncompatibility(arr, K));
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;

class Solution {
  int k;
  int n;
  int goal;
  int [,]dp;
  List<int> bits = new List<int>();

  // Function to find the minimum
  // incompatibility sum
  public int minimumIncompatibility(
    int[] A, int k)
  {
    this.n = A.Length;
    this.k = k;
    goal = n / k;

    // Stores the count of element
    Dictionary<int,int> map
      = new Dictionary<int,int>();

    // Traverse the array
    foreach(int i in A) {

      // If number i not occurs
      // in Map
      if (!map.ContainsKey(i))

        // Put the element
        // in the Map
        map[i]= 0;

      // Increment the count of
      // i in the Hash Map
      map[i]++;

      // If count of i in Map is
      // greater than K then
      // return -1
      if (map[i] > k)
        return -1;
    }

    // Stores all total state
    int state = (1 << n) - 1;

    // Traverse over all the state
    for (int i = 0; i <= state; i++) {

      // If number of set bit
      // is equal to N/K
      if (Convert.ToString(i, 2).Count(c => c == '1') == goal)
        bits.Add(i);
    }

    // Stores the minimum value
    // at a state
    dp = new int[1 << n,k];

    // Initialize the dp state
    // with -1
    for (int i = 0;i < dp.GetLength(0); i++) {

      for (int j = 0;j < dp.GetLength(1); j++) {
        dp[i,j]=-1;
      }

    }

    // Call the recursive function
    return dfs(A, state, 0);
  }

  // Recursive function to find
  // the minimum required value
  public int dfs(int []A, int state,
                 int index)
  {
    // Base Case
    if (index >= k) {
      return 0;
    }

    // Stores the minimum value
    // of the current state
    int res = 1000;

    // If dp[state][index] is
    // already calculated
    if (dp[state,index] != -1) {

      // return dp[state][index]
      return dp[state,index];
    }

    // Traverse over all the bits
    foreach(int bit in bits) {

      // If count of set bit is N/K
      if(Convert.ToString(bit, 2).Count(c => c == '1')== goal) {

        // Store the new state after
        // choosing N/K elements
        int newstate = state;

        // Stores the minimum and
        // maximum of current subset
        int mn = 100, mx = -1;

        // Stores if the elements
        // have been already
        // selected or not
        bool []visit
          = new bool[n + 1];

        // Stores if it is possible
        // to select N/K elements
        bool good = true;

        // Traverse over the array
        for (int j = 0; j < n; j++) {

          // If not chosen already
          // for another subset
          if ((bit & (1 << j)) != 0) {

            // If already chosen
            // for another subset
            // or current subset
            if (visit[A[j]] == true
                || (state & (1 << j)) == 0) {

              // Mark the good false
              good = false;
              break;
            }

            // Mark the current
            // number visited
            visit[A[j]] = true;

            // Mark the current
            // position in mask
            // newstate
            newstate = newstate
              ^ (1 << j);

            // Update the maximum
            // and minimum
            mx = Math.Max(mx,
                          A[j]);
            mn = Math.Min(mn,
                          A[j]);
          }
        }

        // If good is true then
        // Update the res
        if (good) {
          res = Math.Min(
            res, mx - mn
            + dfs(A, newstate,
                  index + 1));
        }
      }
    }

    // Update the current sp state
    dp[state,index] = res;

    // Return the res
    return res;
  }
}

// Driver Code
class GFG {

  public static void Main()
  {
    Solution st = new Solution();
    int[] arr = { 1, 2, 1, 4 };
    int K = 2;

    // Function Call
    Console.Write(
      st.minimumIncompatibility(arr, K));
  }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let k,n,goal;
let dp;
let bits = [];

// Function to find the minimum
// incompatibility sum
function minimumIncompatibility(A,K)
{
    n = A.length;
    k = K;
    goal = Math.floor(n / k);

    // Stores the count of element
        let map = new Map();

        // Traverse the array
        for (let i=0;i< A.length;i++) {

            // If number i not occurs
            // in Map
            if (!map.has(A[i]))

                // Put the element
                // in the Map
                map.set(A[i], 0);

            // Increment the count of
            // i in the Hash Map
            map.set(A[i], map.get(A[i]) + 1);

            // If count of i in Map is
            // greater than K then
            // return -1
            if (map.get(A[i]) > k)
                return -1;
        }

        // Stores all total state
        let state = (1 << n) - 1;

        // Traverse over all the state
        for (let i = 0; i <= state; i++) {

            // If number of set bit
            // is equal to N/K
            if (i.toString(2).split('0').join('').length == goal)
                bits.push(i);
        }

        // Stores the minimum value
        // at a state
        dp = new Array(1 << n);

        // Initialize the dp state
        // with -1
        for (let i = 0;
            i < dp.length; i++) {
            dp[i]=new Array(k);
            for(let j=0;j<k;j++)
                dp[i][j]=-1;
        }

        // Call the recursive function
        return dfs(A, state, 0);
}

// Recursive function to find
// the minimum required value
function dfs(A,state,index)
{
    // Base Case
        if (index >= k) {
            return 0;
        }

        // Stores the minimum value
        // of the current state
        let res = 1000;

        // If dp[state][index] is
        // already calculated
        if (dp[state][index] != -1) {

            // return dp[state][index]
            return dp[state][index];
        }

        // Traverse over all the bits
        for (let bit=0;bit< bits.length;bit++) {

            // If count of set bit is N/K
            if (bits[bit].toString(2).split('0').join('').length
                == goal) {

                // Store the new state after
                // choosing N/K elements
                let newstate = state;

                // Stores the minimum and
                // maximum of current subset
                let mn = 100, mx = -1;

                // Stores if the elements
                // have been already
                // selected or not
                let visit
                    = new Array(n + 1);
                    for(let i=0;i<=n;i++)
                    {
                        visit[i]=false;
                    }

                // Stores if it is possible
                // to select N/K elements
                let good = true;

                // Traverse over the array
                for (let j = 0; j < n; j++) {

                    // If not chosen already
                    // for another subset
                    if ((bits[bit] & (1 << j)) != 0) {

                        // If already chosen
                        // for another subset
                        // or current subset
                        if (visit[A[j]] == true
                            || (state & (1 << j)) == 0) {

                            // Mark the good false
                            good = false;
                            break;
                        }

                        // Mark the current
                        // number visited
                        visit[A[j]] = true;

                        // Mark the current
                        // position in mask
                        // newstate
                        newstate = newstate
                                   ^ (1 << j);

                        // Update the maximum
                        // and minimum
                        mx = Math.max(mx,
                                      A[j]);
                        mn = Math.min(mn,
                                      A[j]);
                    }
                }

                // If good is true then
                // Update the res
                if (good) {
                    res = Math.min(
                        res, mx - mn
                                 + dfs(A, newstate,
                                       index + 1));
                }
            }
        }

        // Update the current sp state
        dp[state][index] = res;

        // Return the res
        return res;
}

// Driver Code
let arr=[1, 2, 1, 4];
let K = 2;
document.write(minimumIncompatibility(arr, K))

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>* 2<sup>2 * N</sup>)*
***辅助空间:** O(N)*