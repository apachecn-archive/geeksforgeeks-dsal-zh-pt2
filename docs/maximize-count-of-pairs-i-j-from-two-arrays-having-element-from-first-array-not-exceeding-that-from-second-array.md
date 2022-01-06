# 最大化来自两个阵列的对(I，j)的计数，其中来自第一阵列的元素不超过来自第二阵列的元素

> 原文:[https://www . geeksforgeeks . org/最大化两个数组中的 i-j 对的计数-从第一个数组中有元素-不超过从第二个数组中有元素/](https://www.geeksforgeeks.org/maximize-count-of-pairs-i-j-from-two-arrays-having-element-from-first-array-not-exceeding-that-from-second-array/)

给定两个长度分别为 **N** 和 **M** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr1[]** 和 **arr2[]** ，任务是找到最大对数 **(i，j)** ，使得**2 * arr 1[I]≤arr 2[j]**(**1≤I≤N**和 **1 ≤ j ≤ M** )。

**注意:**任何数组元素都可以是单个对的一部分。

**示例:**

> **输入:** N = 3，arr1[] = {3，2，1}，M = 4，arr2[] = {3，4，2，1}
> **输出:** 2
> **说明:**
> 只能选择两对:
> 
> *   **(1，3):** 选择元素 arr1[3]和 arr2[1]。
>     因此，pair = (arr1[3]，arr2[1]) = (1，3)。另外，2 * arr1[3] ≤ arr2[1]。
>     现在分别位于 arr1[]和 arr2[]的位置 3 和 1 的元素不能被选择。
> *   **(2，2):** 选择元素 arr1[2]和 arr2[2]。
>     因此，pair = (arr1[2]，arr2[2]) = (2，4)。另外，2*arr1[2] < = arr2[2]。
>     现在无法选择 arr1[]和 arr2[]位置 2 的元素。
> 
> **输入:** N = 1，arr1[] = {40}，M = 4，arr2[] = {10，20，30，40}
> **输出:** 0
> **解释:**
> 不存在满足条件的可能对。

**天真方法:**最简单的方法是首先[对数组](https://www.geeksforgeeks.org/sorting-algorithms/)和每个元素 **arr1[i]** 、[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)找到给定数组 **arr2[]** 中刚好大于或等于值 **2 * arr1[i]** 的元素，然后通过将所需的总对数增加 **1** 从 **arr2[]** 中移除该元素遍历整个数组 **arr1[]** 后，打印对的数量。

***时间复杂度:** O(N * M)，其中 N 和 M 是给定数组的长度。*
***辅助空间:** O(N+M)*

**有效方法:**思路是使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)通过在**arr 2【】**中找到一个刚好大于或等于值**2 * arr 1【I】**的元素，其中 **0 < =i < =N-1** 。按照以下步骤解决问题:

1.  [排序数组](https://www.geeksforgeeks.org/sorting-algorithms/) **arr1[]** 并初始化一个变量 **ans** 来存储最大的对数。
2.  将[最大堆](https://www.geeksforgeeks.org/binary-heap/)中 **arr2[]** 的所有元素相加。
3.  [从**I =(N–1)**到 **0** 按非递增顺序遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr1[]** 。
4.  对于每个元素 **arr1[i]** ，从[最大堆](https://www.geeksforgeeks.org/binary-heap/)中移除 peek 元素，直到 **2*arr1[i]** 变得小于或等于 peek 元素，如果找到此类元素，则将**和**增加 **1** 。
5.  遍历整个数组后，打印**和**作为最大对数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// number of required pairs
int numberOfPairs(int arr1[], int n,
                  int arr2[], int m)
{

    // Max Heap to add values of arar2[]
    priority_queue<int> pq;
    int i, j;

    // Sort the array arr1[]
    sort(arr1, arr1 + n);

    // Push all arr2[] into Max Heap
    for (j = 0; j < m; j++) {
        pq.push(arr2[j]);
    }

    // Initialize the ans
    int ans = 0;

    // Traverse the arr1[] in
    // decreasing order
    for (i = n - 1; i >= 0; i--) {

        // Remove element until a
        // required pair is found
        if (pq.top() >= 2 * arr1[i]) {
            ans++;

            pq.pop();
        }
    }

    // Return maximum number of pairs
    return ans;
}

// Driver Code
int main()
{
    // Given arrays
    int arr1[] = { 3, 1, 2 };
    int arr2[] = { 3, 4, 2, 1 };

    int N = sizeof(arr1) / sizeof(arr1[0]);
    int M = sizeof(arr2) / sizeof(arr2[0]);

    // Function Call
    cout << numberOfPairs(arr1, N,
                          arr2, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to return the maximum
// number of required pairs
static int numberOfPairs(int[] arr1, int n,
                         int[] arr2, int m)
{

    // Max Heap to add values of arr2[]
    PriorityQueue<Integer> pQueue =
    new PriorityQueue<Integer>(
        new Comparator<Integer>()
    {
        public int compare(Integer lhs,
                           Integer rhs)
        {
            if (lhs < rhs)
            {
                return + 1;
            }
            if (lhs.equals(rhs))
            {
                return 0;
            }
            return -1;
        }
    });

    int i, j;

    // Sort the array arr1[]
    Arrays.sort(arr1);

    // Push all arr2[] into Max Heap
    for(j = 0; j < m; j++)
    {
        pQueue.add(arr2[j]);
    }

    // Initialize the ans
    int ans = 0;

    // Traverse the arr1[] in
    // decreasing order
    for(i = n - 1; i >= 0; i--)
    {

        // Remove element until a
        // required pair is found
        if (pQueue.peek() >= 2 * arr1[i])
        {
            ans++;
            pQueue.poll();
        }
    }

    // Return maximum number of pairs
    return ans;
}

// Driver Code
public static void main (String[] args)
{

    // Given arrays
    int[] arr1 = { 3, 1, 2 };
    int[] arr2 = { 3, 4, 2, 1 };

    int N = 3;
    int M = 4;

    // Function call
    System.out.println(numberOfPairs(arr1, N,
                                     arr2, M));
}
}

// This code is contributed by sallagondaavinashreddy7
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the maximum
# number of required pairs
def numberOfPairs(arr1, n, arr2, m):

    # Max Heap to add values of arr2[]
    pq = []

    # Sort the array arr1[]
    arr1.sort(reverse = False)

    # Push all arr2[] into Max Heap
    for j in range(m):
        pq.append(arr2[j])

    # Initialize the ans
    ans = 2

    # Traverse the arr1[] in
    # decreasing order
    i = n - 1
    while (i >= 0):

        # Remove element until a
        # required pair is found
        pq.sort(reverse = False)

        if (pq[0] >= 2 * arr1[i]):
            ans += 1
            print(pq[0])
            pq.remove(pq[0])

        i -= 1

    # Return maximum number of pairs
    return ans

# Driver Code
if __name__ == '__main__':

    # Given arrays
    arr1 = [ 3, 2, 1 ]
    arr2 = [ 3, 4, 2, 1 ]

    N = len(arr1)
    M = len(arr2)

    # Function Call
    print(numberOfPairs(arr1, N, arr2, M))

# This code is contributed by ipg2016107
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N + M*log M)，其中 N 和 M 是给定数组的长度。*
***辅助空间:** O(N+M)*