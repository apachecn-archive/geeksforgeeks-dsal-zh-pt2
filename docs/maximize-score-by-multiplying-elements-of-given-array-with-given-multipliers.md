# 通过给定数组的元素与给定乘数相乘来最大化得分

> 原文:[https://www . geeksforgeeks . org/给定数组的元素乘以给定乘数最大化分数/](https://www.geeksforgeeks.org/maximize-score-by-multiplying-elements-of-given-array-with-given-multipliers/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/) **数组[]** 和**乘法器[]** ，大小为 **N** 和 **M** ，其中 **N** 总是大于等于**M。**有 **M** 个操作要执行。在每个操作中，从数组中选择**乘数[i]** 和一个元素 **arr[]** 开始或结束假设 **K** 然后将**乘数[i]*K** 加到总分中假设 **ans** 并从数组 **arr[]中移除 **K** 。**任务是找到最终得分 **ans 的最大值。**

**示例:**

> **输入**:数组[] = {1，2，3}，乘数[] = {3，2，1}，N=3，M=3
> **输出** : 14
> **解释**:一个最优解如下:
> –从末尾开始选择，【1，2，3】，分数加 3 * 3 = 9。
> –从最后开始选择，[1，2]，分数加 2 * 2 = 4。
> –从最后开始选择，[1]，分数加 1 * 1 = 1。
> 总分 9 + 4 + 1 = 14。
> 
> **输入:**数组[] = {2，1}，乘数[] = {0}，N=2，M=1
> **输出:** 0
> **说明:**无论选择 2 还是 1，答案都是 0，因为乘数[0]等于 0。

**天真的做法:**蛮力的解决方法是递归地检查每一对，找到最优解。

下面是上述方法的实现

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum score
// using dynamic programming and
// memoization
int getMaxScore(vector<int>& array,
                vector<int>& multipliers)
{

  // M is the number of elements needed to pick
  int M = multipliers.size(), N = array.size();

  int remain = N - M;
  vector<int> dp(M + 1, 0);

  for (int i = 0; i < M; ++i) {
    int mm = multipliers[M - i - 1];

    for (int j = 0; j < M - i; ++j) {

      dp[j] = max(mm * array[j] + dp[j + 1],
                  mm * array[j + remain] + dp[j]);
    }
    remain += 1;
  }
  return dp[0];
}

// Driver Code
int main()
{

  vector<int> array = { 1, 2, 3 };
  vector<int> multipliers = { 3, 2, 1 };

  cout << getMaxScore(array, multipliers);

  return 0;
}

// This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

  // Function to find the maximum score
  // using dynamic programming and
  // memoization
  static int getMaxScore(int []array,int []multipliers)
  {

    // M is the number of elements needed to pick
    int M = multipliers.length;
    int N = array.length;

    int remain = N - M;
    int dp[] = new int[M + 1];

    for (int i = 0; i < M; ++i) {
      int mm = multipliers[M - i - 1];

      for (int j = 0; j < M - i; ++j) {

        dp[j] = Math.max(mm * array[j] + dp[j + 1],
                         mm * array[j + remain] + dp[j]);
      }
      remain += 1;
    }
    return dp[0];
  }

  // Driver Code
  public static void main (String[] args)
  {

    int []array = { 1, 2, 3 };
    int []multipliers = { 3, 2, 1 };

    System.out.println(getMaxScore(array, multipliers));

  }

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum score
# recursively

def getMaxScore(array, multipliers):

    # Depth first search
    def dfs(start, end, index):
        if index == len(multipliers):
            return 0

        # Pick left
        left = multipliers[index] * array[start] + \
            dfs(start + 1, end, index + 1)

        # Pick right
        right = multipliers[index] * array[end] + \
            dfs(start, end - 1, index + 1)

        return max(right, left)

    return dfs(0, len(array) - 1, 0)

# Driver Code
if __name__ == "__main__":

    array = [1, 2, 3]
    multipliers = [3, 2, 1]

    print(getMaxScore(array, multipliers))
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Function to find the maximum score
    // using dynamic programming and
    // memoization
    static int getMaxScore(int[] array, int[] multipliers)
    {

        // M is the number of elements needed to pick
        int M = multipliers.Length;
        int N = array.Length;

        int remain = N - M;
        int[] dp = new int[M + 1];

        for (int i = 0; i < M; ++i)
        {
            int mm = multipliers[M - i - 1];

            for (int j = 0; j < M - i; ++j)
            {

                dp[j] = Math.Max(mm * array[j] + dp[j + 1],
                                 mm * array[j + remain] + dp[j]);
            }
            remain += 1;
        }
        return dp[0];
    }

    // Driver Code
    public static void Main(String[] args)
    {

        int[] array = { 1, 2, 3 };
        int[] multipliers = { 3, 2, 1 };

        Console.Write(getMaxScore(array, multipliers));

    }
}

// This code is contributed by gfgking.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum score
// using dynamic programming and
// memoization
function getMaxScore(array, multipliers) {

  // M is the number of elements needed to pick
  let M = multipliers.length, N = array.length;

  let remain = N - M;
  let dp = new Array(M + 1).fill(0);

  for (let i = 0; i < M; ++i) {
    let mm = multipliers[M - i - 1];

    for (let j = 0; j < M - i; ++j) {

      dp[j] = Math.max(mm * array[j] + dp[j + 1],
        mm * array[j + remain] + dp[j]);
    }
    remain += 1;
  }
  return dp[0];
}

// Driver Code

let array = [1, 2, 3];
let multipliers = [3, 2, 1];

document.write(getMaxScore(array, multipliers));

// This code is contributed by gfgking
</script>
```

**Output**

```
14
```

***时间复杂度:**O(2<sup>M</sup>)*
***辅助空间:** O(1)*

**有效方法:**解决方案基于[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)，因为它包含属性–[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)和[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。假设 **dp[i][j]** 是当前从一个子阵列可以得到的最大结果，其中 **i** 是开始索引， **j** 是结束。在任何阶段，都有两种选择:

> 选择第一个:dp[i + 1][j] + curr_weight *数组[i]
> 
> 选择最后一个:DP[I][j–1]+curr _ weight *数组[j]

结果将是两者的最大值。按照以下步骤使用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)和[记忆](https://www.geeksforgeeks.org/tabulation-vs-memoization/)解决问题:

*   初始化一个变量**保持**为 **N-M** 。
*   [初始化大小为 **M+1** 的数组](https://www.geeksforgeeks.org/python-arrays/) **dp[]** ，值为 **0。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/loops-in-python/)**【0，M)** ，并执行以下步骤:
    *   将变量 **mm** 初始化为**乘数[-i-1]** 。
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/loops-in-python/)**【0，M-i)** ，并执行以下步骤:
        *   将 **dp[j]** 的值设置为**mm *数组[j] + dp[j+1]** 或**mm *数组[j+剩余] + dp[j]的最大值。**
        *   将**剩余**的值增加 **1。**
*   执行上述步骤后，打印**DP【0】**的值作为答案。

下面是上述方法的实现:

## C++

```
// Java program for the above approach
#include <bits/stdc++.h>
using namespace std;

  // Function to find the maximum score
  // using dynamic programming and
  // memoization
int getMaxScore(vector<int>& array,
                vector<int>& multipliers)
{

    // M is the number of elements needed to pick
    int M = multipliers.size(), N = array.size();

    int remain = N - M;
    vector<int> dp(M + 1, 0);

    for (int i = 0; i < M; ++i) {
      int mm = multipliers[M - i - 1];

      for (int j = 0; j < M - i; ++j) {

        dp[j] = max(mm * array[j] + dp[j + 1],
                         mm * array[j + remain] + dp[j]);
      }
      remain += 1;
    }
    return dp[0];
  }

  // Driver Code
  int main ()
  {

    vector<int> array = { 1, 2, 3 };
    vector<int> multipliers = { 3, 2, 1 };

    cout << getMaxScore(array, multipliers);

  }

// This code is contributed by shikhasingrajput
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG {

  // Function to find the maximum score
  // using dynamic programming and
  // memoization
  static int getMaxScore(int []array,int []multipliers)
  {

    // M is the number of elements needed to pick
    int M = multipliers.length;
    int N = array.length;

    int remain = N - M;
    int dp[] = new int[M + 1];

    for (int i = 0; i < M; ++i) {
      int mm = multipliers[M - i - 1];

      for (int j = 0; j < M - i; ++j) {

        dp[j] = Math.max(mm * array[j] + dp[j + 1],
                         mm * array[j + remain] + dp[j]);
      }
      remain += 1;
    }
    return dp[0];
  }

  // Driver Code
  public static void main (String[] args)
  {

    int []array = { 1, 2, 3 };
    int []multipliers = { 3, 2, 1 };

    System.out.println(getMaxScore(array, multipliers));

  }

}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum score
# using dynamic programming and
# memoization
def getMaxScore(array, multipliers):

    # M is the number of elements needed to pick
    M, N = len(multipliers), len(array)
    remain = N - M
    dp = [0] * (M + 1)

    for i in range(M):
        mm = multipliers[-i - 1]
        for j in range(M - i):
            dp[j] = max(mm * array[j] + dp[j + 1],
                        mm * array[j + remain] + dp[j])
        remain += 1
    return dp[0]

# Driver Code
if __name__ == "__main__":

    array = [1, 2, 3]
    multipliers = [3, 2, 1]

    print(getMaxScore(array, multipliers))
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Function to find the maximum score
    // using dynamic programming and
    // memoization
    static int getMaxScore(int[] array, int[] multipliers)
    {

        // M is the number of elements needed to pick
        int M = multipliers.Length;
        int N = array.Length;

        int remain = N - M;
        int[] dp = new int[M + 1];

        for (int i = 0; i < M; ++i) {
            int mm = multipliers[M - i - 1];

            for (int j = 0; j < M - i; ++j) {

                dp[j] = Math.Max(mm * array[j] + dp[j + 1],
                                 mm * array[j + remain]
                                     + dp[j]);
            }
            remain += 1;
        }
        return dp[0];
    }

    // Driver Code
    public static void Main(string[] args)
    {

        int[] array = { 1, 2, 3 };
        int[] multipliers = { 3, 2, 1 };

        Console.WriteLine(getMaxScore(array, multipliers));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       //Function to find the maximum score
       //using dynamic programming and
       //memoization

       function getMaxScore(array, multipliers) {
           //M is the number of elements needed to pick
           M = multipliers.length
           N = array.length
           remain = N - M
           dp = new Array(M + 1).fill(0)

           for (let i = 0; i < M; i++) {
               mm = multipliers[M - i - 1]
               for (j = 0; j < M - i; j++)
                   dp[j] = Math.max(mm * array[j] + dp[j + 1],
                       mm * array[j + remain] + dp[j])
               remain += 1
           }
           return dp[0]
       }

       array = [1, 2, 3]
       multipliers = [3, 2, 1]

       document.write(getMaxScore(array, multipliers))

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
14
```

***时间复杂度:** O(M*M)*
***辅助空间:** O(M)*