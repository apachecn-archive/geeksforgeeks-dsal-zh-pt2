# 根据给定的规则，最小化 K，让人 A 至少消费 ceil(N/(M + 1))糖果

> 原文:[https://www . geesforgeks . org/minimum-k-to-let-person-a-consume-至少-ceilin-m-1-candes-based-on-given-rules/](https://www.geeksforgeeks.org/minimize-k-to-let-person-a-consume-at-least-ceiln-m-1-candies-based-on-given-rules/)

给定 **N 个**糖果、 **M 个**人以及 **M 个**正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找到 **K 个**的最小值，使得一个**人 A** 能够按照以下规则消耗 **(N/(M + 1))** 糖果的至少 [ceil](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) 的总和:

*   在第一回合中，**人 A** 消耗剩下的**糖果数量**和 **K** 的最少数量。
*   在接下来的 **M** 轮次中，每个 **i <sup>第</sup>人**在随后的范围**【0，M-1】**内消耗**的[楼层](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)剩余糖果的百分比。**
*   重复以上步骤，直到没有糖果剩下。

**示例:**

> **输入:** N = 13，M = 1，arr[] = {50}
> **输出:** 3
> **说明:**
> 对于 K 为 3 的值，好的份额是(13/2) = 7 的上限。以下是发生的转折:
> 
> 1.  **人 A** 服用 min(3，13)=3 颗糖果。因此，剩下的糖果= 13–3 = 10。
> 2.  **人 0** 取剩下的 10 颗糖果中的 arr[0](= 50%)，即 5 颗糖果。因此，剩下的糖果= 10–5 = 5。
> 3.  **人 A** 服用 min(3，5)=3 颗糖果。因此，剩下的糖果= 5–3 = 2。
> 4.  **人 0** 拿走剩下的 2 颗糖果中的 arr[0](= 50%)，即 1 颗糖果。因此，剩下的糖果= 2–1 = 1。
> 5.  **人 A** 吃 1 颗糖。因此，剩下的糖果= 1–1 = 0。
> 
> 经过以上几个回合，人拿的糖果是 3 + 3 + 1 = 7，至少是(N/(M + 1))颗糖果，即 13/2 = 6 颗。
> 
> **输入:** N = 13，M = 2，arr[] = {40，50 }
> T3】输出: 2

**天真的方法:**解决给定问题最简单的方法是检查每个数量的糖果**人 A** 将获得 **K** 的所有可能值。请按照以下步骤解决此问题:

*   找到 **(N/(M + 1))** 的值并存储在变量中，说**好**，因为这是**人 A** 想吃的最小糖果量。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**内 **K** 的所有值，并执行以下步骤:
    *   对于 **K** 的每个值，模拟上述过程，统计**人 A** 将得到的糖果总数。
    *   如果糖果的数量至少是**好**的值，那么[就跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，[继续迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。
*   完成上述步骤后，打印 **K** 的当前值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum value of
// K such that the first person gets
// at least (N/(M+1)) candies
void minimumK(vector<int> &arr, int M,
              int N)
{
    // Find the minimum required value
      // of candies for the first person
    int good = ceil((N * 1.0)
                    / ((M + 1) * 1.0));

    // Iterate K from [1, n]
    for (int i = 1; i <= N; i++) {

          int K = i;

          // Total number of candies
        int candies = N;

          // Candies taken by Person 1
          int taken = 0;

        while (candies > 0) {

            // Candies taken by 1st
            // person is minimum of K
            // and candies left         
            taken += min(K, candies);
            candies -= min(K, candies);

            // Traverse the array arr[]         
            for (int j = 0; j < M; j++) {

                // Amount consumed by the
                  // person j
                int consume = (arr[j]
                               * candies) / 100;

                // Update the number
                  // of candies
                candies -= consume;
            }
        }

        // Good share of candies achieved
        if (taken >= good) {
            cout << i;
            return;
        }
    }
}

// Driver Code
int main()
{
    int N = 13, M = 1;
    vector<int> arr = { 50 }; 
    minimumK(arr, M, N);

      return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find minimum value of
// K such that the first person gets
// at least (N/(M+1)) candies
static void minimumK(ArrayList<Integer> arr, int M,
                                             int N)
{

    // Find the minimum required value
    // of candies for the first person
    int good = (int)((N * 1.0) / ((M + 1) * 1.0)) + 1;

    // Iterate K from [1, n]
    for(int i = 1; i <= N; i++)
    {
        int K = i;

        // Total number of candies
        int candies = N;

        // Candies taken by Person 1
        int taken = 0;

        while (candies > 0)
        {

            // Candies taken by 1st
            // person is minimum of K
            // and candies left
            taken += Math.min(K, candies);
            candies -= Math.min(K, candies);

            // Traverse the array arr[]
            for(int j = 0; j < M; j++)
            {

                // Amount consumed by the
                // person j
                int consume = (arr.get(j) * candies) / 100;

                // Update the number
                // of candies
                candies -= consume;
            }
        }

        // Good share of candies achieved
        if (taken >= good)
        {
            System.out.print(i);
            return;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 13, M = 1;
    ArrayList<Integer> arr = new ArrayList<Integer>();
    arr.add(50);

    minimumK(arr, M, N);
}
}

// This code is contributed by subhammahato348
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import math
# Function to find minimum value of
# K such that the first person gets
# at least (N/(M+1)) candies
def minimumK(arr,  M, N):

    # Find the minimum required value
    # of candies for the first person
    good = math.ceil((N * 1.0) / ((M + 1) * 1.0))

    # Iterate K from [1, n]
    for i in range(1, N + 1):
        K = i

        # Total number of candies
        candies = N

        # Candies taken by Person 1
        taken = 0

        while (candies > 0):

            # Candies taken by 1st
            # person is minimum of K
            # and candies left
            taken += min(K, candies)
            candies -= min(K, candies)

            # Traverse the array arr[]
            for j in range(M):

                # Amount consumed by the
                # person j
                consume = (arr[j]
                           * candies) / 100

                # Update the number
                # of candies
                candies -= consume

        # Good share of candies achieved
        if (taken >= good):
          print(i)
          return

# Driver Code
if __name__ == "__main__":

    N = 13
    M = 1
    arr = [50]
    minimumK(arr, M, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum value of
// K such that the first person gets
// at least (N/(M+1)) candies
static void minimumK(List<int> arr, int M,
              int N)
{
    // Find the minimum required value
      // of candies for the first person
    int good = (int)((N * 1.0) / ((M + 1) * 1.0))+1;

    // Iterate K from [1, n]
    for (int i = 1; i <= N; i++) {

          int K = i;

          // Total number of candies
          int candies = N;

          // Candies taken by Person 1
          int taken = 0;

        while (candies > 0) {

            // Candies taken by 1st
            // person is minimum of K
            // and candies left         
            taken += Math.Min(K, candies);
            candies -= Math.Min(K, candies);

            // Traverse the array arr[]         
            for (int j = 0; j < M; j++) {

                // Amount consumed by the
                  // person j
                int consume = (arr[j]
                               * candies) / 100;

                // Update the number
                  // of candies
                candies -= consume;
            }
        }

        // Good share of candies achieved
        if (taken >= good) {
            Console.Write(i);
            return;
        }
    }
}

// Driver Code
public static void Main()
{
    int N = 13, M = 1;
    List<int> arr = new List<int>();
    arr.Add(50); 
    minimumK(arr, M, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find minimum value of
// K such that the first person gets
// at least (N/(M+1)) candies
function minimumK(arr, M, N)
{
    // Find the minimum required value
   // of candies for the first person
    let good = Math.floor((N * 1.0) / ((M + 1) * 1.0))+1;

    // Iterate K from [1, n]
    for (let i = 1; i <= N; i++) {

          let K = i;

          // Total number of candies
          let candies = N;

          // Candies taken by Person 1
          let taken = 0;

        while (candies > 0) {

            // Candies taken by 1st
            // person is minimum of K
            // and candies left         
            taken += Math.min(K, candies);
            candies -= Math.min(K, candies);

            // Traverse the array arr[]         
            for (let j = 0; j < M; j++) {

                // Amount consumed by the
                  // person j
                let consume = (arr[j]
                               * candies) / 100;

                // Update the number
                  // of candies
                candies -= consume;
            }
        }

        // Good share of candies achieved
        if (taken >= good) {
            document.write(i);
            return;
        }
    }
}

// Driver Code

    let N = 13, M = 1;
    let arr = new Array();
    arr.push(50); 
    minimumK(arr, M, N);

// This code is contributed by _Saurabh_Jaiswal

</script>
```

**输出:**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**上述途径也可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)进行优化。按照以下步骤解决问题:

*   找到 **(N/(M + 1))** 的值并存储在变量中，说**好**，因为这是**人 A** 想吃的最小糖果量。
*   初始化两个变量，分别说**低**和**高**为 **1** 和 **N** 。
*   重复直到**低电平**小于**高电平**，并执行以下步骤:
    *   求**中间**的值为**(低+高)/2** 。
    *   通过模拟上述过程，为 **K** 作为**中间**的值找到**人 A** 所吃糖果的最小数量。
    *   如果**人 A** 拿的糖果数量至少是**好**那么更新**高**的值为**中**。否则，将**低位**的值更新为**(中+ 1)** 。
*   完成上述步骤后，打印**高值**作为 **K** 的合成最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the value of
// mid gives at least (N/(M + 1))
// candies or not
bool check(int K, int n, int m,
           vector<int> arr,
           int good_share)
{
    int candies = n, taken = 0;

    while (candies > 0) {

        // Candies taken by 1st
        // person is minimum of K
        // and candies left
        taken += min(K, candies);
        candies -= min(K, candies);

        // Traverse the given array
        for (int j = 0; j < m; j++) {

            // Amount consumed by
              // person j
            int consume = (arr[j] * candies) / 100;

            // Update the count of
              // candies
            candies -= consume;
        }
    }

    // Check if person 1 gets the
      // good share of candies
    return (taken >= good_share);
}

// Function to find minimum value of
// K such that the first person gets
// at least (N/(M+1)) candies
void minimumK(vector<int> &arr, int N,
              int M)
{
    // Find the minimum required value
      // of candies for the first person
    int good_share = ceil((N * 1.0)
                          / ((M + 1) * 1.0));

    int lo = 1, hi = N;

      // Iterate until low is less
      // than or equal to mid
    while (lo < hi) {

        // Find the value of mid
        int mid = (lo + hi) / 2;

        // Check for mid, whether it
          // can be the possible value
          // of K or not
        if (check(mid, N, M, arr,
                  good_share)) {

            // Update the value of hi
            hi = mid;
        }

          // Otherwise, update the
          // value of lo
        else {
            lo = mid + 1;
        }
    }

    // Print the resultant minimum
      // value of K
    cout << hi;
}

// Driver Code
int main()
{
    int N = 13, M = 1;
    vector<int> arr = { 50 };

    minimumK(arr, N, M);

      return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

// Function to check if the value of
// mid gives at least (N/(M + 1))
// candies or not
static boolean check(int K, int n, int m,
           ArrayList<Integer> arr,
           int good_share)
{
    int candies = n, taken = 0;

    while (candies > 0) {

        // Candies taken by 1st
        // person is minimum of K
        // and candies left
        taken += Math.min(K, candies);
        candies -= Math.min(K, candies);

        // Traverse the given array
        for (int j = 0; j < m; j++) {

            // Amount consumed by
              // person j
            int consume = (arr.get(j) * candies) / 100;

            // Update the count of
              // candies
            candies -= consume;
        }
    }

    // Check if person 1 gets the
      // good share of candies
    return (taken >= good_share);
}

// Function to find minimum value of
// K such that the first person gets
// at least (N/(M+1)) candies
static void minimumK(ArrayList<Integer> arr, int N,
              int M)
{
    // Find the minimum required value
      // of candies for the first person
    int good_share = (int)Math.ceil((N * 1.0)
                          / ((M + 1) * 1.0));

    int lo = 1, hi = N;

      // Iterate until low is less
      // than or equal to mid
    while (lo < hi) {

        // Find the value of mid
        int mid = (lo + hi) / 2;

        // Check for mid, whether it
          // can be the possible value
          // of K or not
        if (check(mid, N, M, arr,
                  good_share)) {

            // Update the value of hi
            hi = mid;
        }

          // Otherwise, update the
          // value of lo
        else {
            lo = mid + 1;
        }
    }

    // Print the resultant minimum
      // value of K
    System.out.print(hi);
}

// Driver Code
public static void main(String[] args)
{
    int N = 13, M = 1;
    ArrayList<Integer> arr = new ArrayList<Integer>();
    arr.add(50);

    minimumK(arr, N, M);
}
}

// This code is contributed by avijitmondal1998.
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*