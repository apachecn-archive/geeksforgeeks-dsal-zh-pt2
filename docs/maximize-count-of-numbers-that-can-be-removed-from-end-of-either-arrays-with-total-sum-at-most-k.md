# 最大化可从任一数组末尾移除的数的计数，总和最多为 K

> 原文:[https://www . geeksforgeeks . org/最大化最多可从任意一个数组末尾移除的数量总和-k/](https://www.geeksforgeeks.org/maximize-count-of-numbers-that-can-be-removed-from-end-of-either-arrays-with-total-sum-at-most-k/)

给定两个包含 **N** 和 **M** 整数的数组 **S1** 和 **S2** ，以及一个整数 **K** ，任务是找出可以从任一给定数组末尾移除的整数的最大数量，使得移除的元素之和小于或等于 **K** 。

**示例:**

> ***输入:*** S1[] = {1，2，3}，S2[] = {1，2，4}，K = 10
> ***输出:*** 5
> ***解释:***S1 的所有元素，即{1，2，3}和 S2 的两个元素，即{1，2}可以从给定数组中移除，因为它们的总和是 9，小于 10。因此，可以移除的整数数量是 5，这是最大可能值。
> 
> ***输入:*** S1[] = {12，21，102}，S2[] = {167，244，377，56，235，269，23}，K = 1000
> ***输出:*** 7

**进场:**以上进场可以借助[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。其思想是**将给定的数组视为堆栈**(因为任何数组中只能移除最末端的元素)。使用[双指针方法](https://www.geeksforgeeks.org/two-pointers-technique/)检查所有可能的有效操作顺序。以下是要遵循的步骤:

*   首先，考虑到 **S2** 不存在，检查一下 **S1** 可以获得多少个数字。
*   现在，在步骤 1 中获得的当前答案被存储为最终答案。
*   现在开始遍历 **S2** ，并继续在移除的整数集中插入元素。如果被删除元素的总和在任一点超过 **K** ，则删除从最后一个到总和小于或等于 **K** 的 **S1** 的整数。
*   根据每个步骤中的当前答案更新最终答案，这实际上给出了所有可能的有效操作序列。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return max profit
// from both stacks given as input
int Max_profit_maximisation(int Stack1[], int Stack2[],
                            int n, int m, int K)
{
    // Stores the final answer
    int maximum_result = 0;

    // Stores the pointer to the
    // current window in stack 1
    int index_for_Stack1 = 0;

    // Stores the pointer to the
    // current window in stack 2
    int index_for_Stack2;

    // Stores sum of current window
    int curr_sum = 0;

    // Case where snly stack 1
    // is considered
    while (index_for_Stack1 < n
           && curr_sum + Stack1[index_for_Stack1]
                  < K) {
        curr_sum += Stack1[index_for_Stack1];
        index_for_Stack1++;
    }

    // Update answer
    maximum_result = index_for_Stack1;

    // Traverse Stack 2 and insert
    // elements into the current
    // window one at a time
    while (index_for_Stack2 < m) {
        curr_sum += Stack2[index_for_Stack2];
        index_for_Stack2++;

        // curr_sum after removing
        // last elements from Stack1
        while (curr_sum > K
               && index_for_Stack1 > 0) {
            index_for_Stack1--;
            curr_sum -= Stack1[index_for_Stack1];
        }

        // Updating the answer
        maximum_result
            = max(maximum_result,
                  index_for_Stack1
                      + index_for_Stack2);
    }

    // Return Answer
    return maximum_result;
}

// Driver code
int main()
{
    int S1[] = { 12, 21, 102 };
    int S2[] = { 167, 244, 377, 56,
                 235, 269, 23 };
    int N = 3;
    int M = 7;
    int K = 1000;

    cout << Max_profit_maximisation(S1, S2, N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function to return max profit
// from both stacks given as input
static int Max_profit_maximisation(int Stack1[], int Stack2[],
                            int n, int m, int K)
{
    // Stores the final answer
    int maximum_result = 0;

    // Stores the pointer to the
    // current window in stack 1
    int index_for_Stack1 =0;

    // Stores the pointer to the
    // current window in stack 2
    int index_for_Stack2=Integer.MAX_VALUE;

    // Stores sum of current window
    int curr_sum = 0;

    // Case where snly stack 1
    // is considered
    while (index_for_Stack1 < n
           && curr_sum + Stack1[index_for_Stack1]
                  < K) {
        curr_sum += Stack1[index_for_Stack1];
        index_for_Stack1++;
    }

    // Update answer
    maximum_result = index_for_Stack1;

    // Traverse Stack 2 and insert
    // elements into the current
    // window one at a time
    while (index_for_Stack2 < m) {
        curr_sum += Stack2[index_for_Stack2];
        index_for_Stack2++;

        // curr_sum after removing
        // last elements from Stack1
        while (curr_sum > K
               && index_for_Stack1 > 0) {
            index_for_Stack1--;
            curr_sum -= Stack1[index_for_Stack1];
        }

        // Updating the answer
        maximum_result
            = Math.max(maximum_result,
                  index_for_Stack1
                      + index_for_Stack2);
    }

    // Return Answer
    return maximum_result;
}

// Driver code
public static void main(String[] args)
{
    int S1[] = { 12, 21, 102 };
    int S2[] = { 167, 244, 377, 56,
                 235, 269, 23 };
    int N = 3;
    int M = 7;
    int K = 1000;

    System.out.print(Max_profit_maximisation(S1, S2, N, M, K));
}
}

// This code is contributed by shikhasingrajput
```

## 计算机编程语言

```
# Python program of the above approach

# Function to return max profit
# from both stacks given as input
def Max_profit_maximisation(Stack1, Stack2, n, m, K):

    # Stores the final answer
    maximum_result = 0

    # Stores the pointer to the
    # current window in stack 1
    index_for_Stack1 = 0

    # Stores the pointer to the
    # current window in stack 2
    index_for_Stack2 = 100**100

    # Stores sum of current window
    curr_sum = 0

    # Case where snly stack 1
    # is considered
    while (index_for_Stack1 < n
           and curr_sum + Stack1[index_for_Stack1]
                  < K):
        curr_sum += Stack1[index_for_Stack1]
        index_for_Stack1 += 1

    # Update answer
    maximum_result = index_for_Stack1

    # Traverse Stack 2 and insert
    # elements into the current
    # window one at a time
    while (index_for_Stack2 < m) :
        curr_sum += Stack2[index_for_Stack2]
        index_for_Stack2 += 1

        # curr_sum after removing
        # last elements from Stack1
        while (curr_sum > K
               and index_for_Stack1 > 0):
            index_for_Stack1 -= 1
            curr_sum -= Stack1[index_for_Stack1]

        # Updating the answer
        maximum_result = max(maximum_result,
                            index_for_Stack1
                            + index_for_Stack2)

    # Return Answer
    return maximum_result

# Driver Code
if __name__ == '__main__':

    S1 = [ 12, 21, 102 ];
    S2 = [ 167, 244, 377, 56,
                 235, 269, 23 ];
    N = 3;
    M = 7;
    K = 1000;

    print(Max_profit_maximisation(S1, S2, N, M, K))

    # This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program of the above approach
using System;

class GFG{

// Function to return max profit
// from both stacks given as input
static int Max_profit_maximisation(int []Stack1, int []Stack2,
                                   int n, int m, int K)
{

    // Stores the readonly answer
    int maximum_result = 0;

    // Stores the pointer to the
    // current window in stack 1
    int index_for_Stack1 =0;

    // Stores the pointer to the
    // current window in stack 2
    int index_for_Stack2=int.MaxValue;

    // Stores sum of current window
    int curr_sum = 0;

    // Case where snly stack 1
    // is considered
    while (index_for_Stack1 < n && 
           curr_sum + Stack1[index_for_Stack1] < K) 
    {
        curr_sum += Stack1[index_for_Stack1];
        index_for_Stack1++;
    }

    // Update answer
    maximum_result = index_for_Stack1;

    // Traverse Stack 2 and insert
    // elements into the current
    // window one at a time
    while (index_for_Stack2 < m)
    {
        curr_sum += Stack2[index_for_Stack2];
        index_for_Stack2++;

        // curr_sum after removing
        // last elements from Stack1
        while (curr_sum > K && index_for_Stack1 > 0)
        {
            index_for_Stack1--;
            curr_sum -= Stack1[index_for_Stack1];
        }

        // Updating the answer
        maximum_result = Math.Max(maximum_result,
                                  index_for_Stack1 + 
                                  index_for_Stack2);
    }

    // Return Answer
    return maximum_result;
}

// Driver code
public static void Main(String[] args)
{
    int []S1 = { 12, 21, 102 };
    int []S2 = { 167, 244, 377, 56,
                 235, 269, 23 };
    int N = 3;
    int M = 7;
    int K = 1000;

    Console.Write(Max_profit_maximisation(S1, S2, N, M, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to return max profit
       // from both stacks given as input
       function Max_profit_maximisation(Stack1, Stack2,
           n, m, K) {
           // Stores the final answer
           let maximum_result = 0;

           // Stores the pointer to the
           // current window in stack 1
           let index_for_Stack1 = 0;

           // Stores the pointer to the
           // current window in stack 2
           let index_for_Stack2;

           // Stores sum of current window
           let curr_sum = 0;

           // Case where snly stack 1
           // is considered
           while (index_for_Stack1 < n
               && curr_sum + Stack1[index_for_Stack1]
               < K) {
               curr_sum += Stack1[index_for_Stack1];
               index_for_Stack1++;
           }

           // Update answer
           maximum_result = index_for_Stack1;

           // Traverse Stack 2 and insert
           // elements into the current
           // window one at a time
           while (index_for_Stack2 < m) {
               curr_sum += Stack2[index_for_Stack2];
               index_for_Stack2++;

               // curr_sum after removing
               // last elements from Stack1
               while (curr_sum > K
                   && index_for_Stack1 > 0) {
                   index_for_Stack1--;
                   curr_sum -= Stack1[index_for_Stack1];
               }

               // Updating the answer
               maximum_result
                   = Math.max(maximum_result,
                       index_for_Stack1
                       + index_for_Stack2);
           }

           // Return Answer
           return maximum_result;
       }

       // Driver code
       let S1 = [12, 21, 102];
       let S2 = [167, 244, 377, 56,
           235, 269, 23];
       let N = 3;
       let M = 7;
       let K = 1000;

       document.write(Max_profit_maximisation(S1, S2, N, M, K));

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
3
```

***时间复杂度** : O(N+M)*
***辅助空间:** O(1)*