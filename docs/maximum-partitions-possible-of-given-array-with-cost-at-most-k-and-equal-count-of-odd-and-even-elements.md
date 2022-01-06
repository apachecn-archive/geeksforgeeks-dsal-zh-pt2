# 给定数组的最大可能分区，成本最多为 K，奇数和偶数元素数量相等

> 原文:[https://www . geeksforgeeks . org/给定数组的最大可能分区与奇数和偶数元素的最大 k 和相等计数/](https://www.geeksforgeeks.org/maximum-partitions-possible-of-given-array-with-cost-at-most-k-and-equal-count-of-odd-and-even-elements/)

给定两个整数 **N，K** 和一个大小为 **N，**的[数组](https://www.geeksforgeeks.org/array-data-structure/)，**arr【】**包含相等数量的偶数和奇数元素，并且还给定通过在索引 **i** 和 **i+1** 之间进行切割来划分数组的成本等于 **abs(arr[i]-arr[i+1])** ，任务是找到数组的最大分区，

**示例:**

> **输入:** N = 6，K = 4，arr[] = {1，2，5，10，15，20}
> **输出:** 1
> **解释:**
> 唯一可能的分割方法是在索引 1 和索引 2 之间进行切割。
> 分区成本= |arr[1]( =2)- arr[2](= 5)| = 3，小于等于 K
> 分区后的数组:{1，2}和{5，10，15，20}。
> 
> **输入:** N = 4，K = 10，arr[] = {1，3，2，4 }
> T3】输出: 0

**方法:**如果 **i** 前缀中的偶数和奇数元素的[计数相等，则可以通过在索引 **i** 和 **i+i、**之间进行切割来进行有效划分，基于这一观察来解决给定的问题。按照步骤解决问题。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **V** 来存储数组中所有可能的削减成本。
*   另外，初始化变量，将**奇数**表示为 **0** ，将**偶数**表示为 **0** ，存储偶数和奇数元素的计数。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]，**，并执行以下步骤:
    *   如果当前元素为奇数，则将**奇数**增加 **1。**否则，将**连**增加 **1。**
    *   如果**奇数**的值等于**偶数**的值，则将|**arr【I】**–**arr【I+1】**的值|追加到 **V.**
*   [按升序排列向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) **V** 。
*   初始化一个整型变量**和**为 **1，**来存储数组的分区数。
*   [使用变量 **i** 遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **V、**，并执行以下步骤:
    *   如果 **V[i]** 的值小于或等于 **K** ，则将值 **K** 更新为**K**–**V[I]**，并将 **ans** 增加 **1。**
    *   否则，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   最后，完成上述步骤后，打印**和**的值作为得到的答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// partitions of the array with
// equal even and odd elements
// with cost less than k
int maximumcut(int arr[], int N, int K)
{
    // Stores count of odd elements
    int odd = 0;
    // Stores count of even elements
    int even = 0;

    // Stores the cost of partitions
    vector<int> V;

    for (int i = 0; i < N - 1; i++) {
        // Odd element
        if (arr[i] % 2 == 1) {
            odd++;
        }
        // Even element
        else {
            even++;
        }

        // Partition is possible
        if (odd == even) {
            int cost = abs(arr[i] - arr[i + 1]);

            // Append the cost of partition
            V.push_back(cost);
        }
    }
    // Stores the maximum number of
    // partitions
    int ans = 0;

    // Sort the costs in ascending order
    sort(V.begin(), V.end());

    // Traverse the vector V
    for (int i = 0; i < V.size(); i++) {
        // Check if cost is less than K
        if (V[i] <= K) {
            // Update the value of K
            K = K - V[i];

            // Update the value of ans
            ans++;
        }
        else {
            break;
        }
    }
    // Return ans
    return ans;
}

// Driver code
int main()
{
    // Given Input
    int arr[] = {1, 2, 5, 10, 15, 20};
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 4;
    // Function call
    cout << maximumcut(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.ArrayList;
import java.util.Arrays;

class GFG
{

// Function to find the maximum
// partitions of the array with
// equal even and odd elements
// with cost less than k
public static int maximumcut(int arr[], int N, int K)
{

    // Stores count of odd elements
    int odd = 0;

    // Stores count of even elements
    int even = 0;

    // Stores the cost of partitions
    ArrayList<Integer> V = new ArrayList<Integer>();

    for (int i = 0; i < N - 1; i++) {
        // Odd element
        if (arr[i] % 2 == 1) {
            odd++;
        }
        // Even element
        else {
            even++;
        }

        // Partition is possible
        if (odd == even) {
            int cost = Math.abs(arr[i] - arr[i + 1]);

            // Append the cost of partition
            V.add(cost);
        }
    }
    // Stores the maximum number of
    // partitions
    int ans = 0;

    // Sort the costs in ascending order
    V.sort(null);

    // Traverse the vector V
    for (int i = 0; i < V.size(); i++)
    {

        // Check if cost is less than K
        if (V.get(i) <= K)
        {

            // Update the value of K
            K = K - V.get(i);

            // Update the value of ans
            ans++;
        }
        else {
            break;
        }
    }
    // Return ans
    return ans;
}

// Driver code
public static void  main(String args[])
{
    // Given Input
    int arr[] = {1, 2, 5, 10, 15, 20};
    int N = arr.length;
    int K = 4;
    // Function call
    System.out.println(maximumcut(arr, N, K));
}

}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to find the maximum
# partitions of the array with
# equal even and odd elements
# with cost less than k
def maximumcut(arr, N, K):

    # Stores count of odd elements
    odd = 0

    # Stores count of even elements
    even = 0

    # Stores the cost of partitions
    V = []

    for i in range(0, N - 1, 1):

        # Odd element
        if (arr[i] % 2 == 1):
            odd += 1

        # Even element
        else:
            even += 1

        # Partition is possible
        if (odd == even):
            cost = abs(arr[i] - arr[i + 1])

            # Append the cost of partition
            V.append(cost)

    # Stores the maximum number of
    # partitions
    ans = 0

    # Sort the costs in ascending order
    V.sort()

    # Traverse the vector V
    for i in range(len(V)):

        # Check if cost is less than K
        if (V[i] <= K):

            # Update the value of K
            K = K - V[i]

            # Update the value of ans
            ans += 1

        else:
            break

    # Return ans
    return ans

# Driver code
if __name__ == '__main__':

    # Given Input
    arr = [ 1, 2, 5, 10, 15, 20 ]
    N = len(arr)
    K = 4

    # Function call
    print(maximumcut(arr, N, K))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# code for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum
// partitions of the array with
// equal even and odd elements
// with cost less than k
static int maximumcut(int []arr, int N, int K)
{

    // Stores count of odd elements
    int odd = 0;

    // Stores count of even elements
    int even = 0;

    // Stores the cost of partitions
    List<int> V = new List<int>();

    for(int i = 0; i < N - 1; i++)
    {

        // Odd element
        if (arr[i] % 2 == 1)
        {
            odd++;
        }

        // Even element
        else
        {
            even++;
        }

        // Partition is possible
        if (odd == even)
        {
            int cost = Math.Abs(arr[i] - arr[i + 1]);

            // Append the cost of partition
            V.Add(cost);
        }
    }

    // Stores the maximum number of
    // partitions
    int ans = 0;

    // Sort the costs in ascending order
    V.Sort();

    // Traverse the vector V
    for(int i = 0; i < V.Count; i++)
    {

        // Check if cost is less than K
        if (V[i] <= K)
        {

            // Update the value of K
            K = K - V[i];

            // Update the value of ans
            ans++;
        }
        else
        {
            break;
        }
    }

    // Return ans
    return ans;
}

// Driver code
public static void Main()
{

    // Given Input
    int []arr = { 1, 2, 5, 10, 15, 20 };
    int N = arr.Length;
    int K = 4;

    // Function call
    Console.Write(maximumcut(arr, N, K));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

        // JavaScript code for the above approach

        // Function to find the maximum
        // partitions of the array with
        // equal even and odd elements
        // with cost less than k
        function maximumcut(arr, N, K) {
            // Stores count of odd elements
            let odd = 0;
            // Stores count of even elements
            let even = 0;

            // Stores the cost of partitions
            var V = [];

            for (let i = 0; i < N - 1; i++) {
                // Odd element
                if (arr[i] % 2 == 1) {
                    odd++;
                }
                // Even element
                else {
                    even++;
                }

                // Partition is possible
                if (odd == even) {
                    let cost = Math.abs(arr[i] - arr[i + 1]);

                    // Append the cost of partition
                    V.push(cost);
                }
            }
            // Stores the maximum number of
            // partitions
            let ans = 0;

            // Sort the costs in ascending order
            V.sort();

            // Traverse the vector V
            for (let i = 0; i < V.length; i++) {
                // Check if cost is less than K
                if (V[i] <= K) {
                    // Update the value of K
                    K = K - V[i];

                    // Update the value of ans
                    ans++;
                }
                else {
                    break;
                }
            }
            // Return ans
            return ans;
        }

        // Driver code

        // Given Input
        let arr = [1, 2, 5, 10, 15, 20];
        let N = arr.length;
        let K = 4;
        // Function call
        document.write(maximumcut(arr, N, K));

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*