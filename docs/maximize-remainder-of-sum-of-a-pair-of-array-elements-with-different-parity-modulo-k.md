# 最大化一对具有不同奇偶模 K 的数组元素之和的余数

> 原文:[https://www . geeksforgeeks . org/最大化具有不同奇偶校验的数组元素对的和的余数-模-k/](https://www.geeksforgeeks.org/maximize-remainder-of-sum-of-a-pair-of-array-elements-with-different-parity-modulo-k/)

给定一个大小为 **N、**的[数组](https://www.geeksforgeeks.org/arrays-in-java/)**arr【】**，每个数组由 **N / 2** 个偶数和奇数以及一个整数 **K** 组成，任务是求一对不同奇偶性的数组元素之和的最大余数[模](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/) **K** 。

**示例:**

> **输入:** arr[] = {3，2，4，11，6，7}，K = 7
> **输出:** 6
> **解释:**
> 一对数组元素之和= 2 + 11
> 之和% K = 13 % 7 = 6。
> 因此，最大可能余数为 6。
> 
> **输入:** arr[] = {8，11，17，16}，K = 13
> T3】输出: 12

**方法:**按照以下步骤解决问题:

*   初始化一个 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) ，比如说**偶**，来存储所有偶数组元素。
*   初始化一个[树集合](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)，说**奇数，**存储所有奇数数组元素。
*   初始化一个变量，比如 **max_rem，**来存储可能的最大余数。
*   [遍历 HashSet](https://www.geeksforgeeks.org/traverse-through-a-hashset-in-java/) ，对于每个元素，找到它的补码，在集合**奇数**中搜索，这个集合小于等于它的补码。
*   用元素之和更新 **max_rem** ，它是补码。
*   打印最大余数，即 **max_rem** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// remainder of sum of a pair
// of array elements modulo K
void maxRemainder(int A[], int N, int K)
{

    // Stores all even numbers
    unordered_set<int> even;

    // Stores all odd numbers
    set<int> odd;

    // Segregate remainders of even
    // and odd numbers in respective sets
    for(int i = 0; i < N; i++)
    {
        int num = A[i];

        if (num % 2 == 0)
            even.insert(num % K);
        else
            odd.insert(num % K);
    }

    // Stores the maximum
    // remainder obtained
    int max_rem = 0;

    // Find the complement of remainder
    // of each even number in odd set
    for(int x : even)
    {

        // Find the complement
        // of remainder x
        int y = K - 1 - x;

        auto it = odd.upper_bound(y);
        if (it != odd.begin())
        {
            it--;
            max_rem = max(max_rem, x + *it);
        }
    }

    // Print the answer
    cout << max_rem;
}

// Driver code
int main()
{

    // Given array
    int arr[] = { 3, 2, 4, 11, 6, 7 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of K
    int K = 7;

    maxRemainder(arr, N, K);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG {

    // Function to find the maximum
    // remainder of sum of a pair
    // of array elements modulo K
    static void maxRemainder(int A[],
                             int N, int K)
    {
        // Stores all even numbers
        HashSet<Integer> even
          = new HashSet<>();

        // Stores all odd numbers
        TreeSet<Integer> odd
          = new TreeSet<>();

        // Segregate remainders of even
        // and odd numbers in respective sets
        for (int num : A) {
            if (num % 2 == 0)
                even.add(num % K);
            else
                odd.add(num % K);
        }

        // Stores the maximum
        // remainder obtained
        int max_rem = 0;

        // Find the complement of remainder
        // of each even number in odd set
        for (int x : even) {

            // Find the complement
            // of remainder x
            int y = K - 1 - x;
            if (odd.floor(y) != null)
                max_rem
                    = Math.max(
              max_rem,
              x + odd.floor(y));
        }

        // Print the answer
        System.out.print(max_rem);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int arr[] = { 3, 2, 4, 11, 6, 7 };

        // Size of the array
        int N = arr.length;

        // Given value of K
        int K = 7;

        maxRemainder(arr, N, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left

# Function to find the maximum
# remainder of sum of a pair
# of array elements modulo K
def maxRemainder(A, N, K):

    # Stores all even numbers
    even = {}

    # Stores all odd numbers
    odd = {}

    # Segregate remainders of even
    # and odd numbers in respective sets
    for i in range(N):
        num = A[i]

        if (num % 2 == 0):
            even[num % K] = 1
        else:
            odd[num % K] = 1

    # Stores the maximum
    # remainder obtained
    max_rem = 0

    # Find the complement of remainder
    # of each even number in odd set
    for x in even:

        # Find the complement
        # of remainder x
        y = K - 1 - x
        od = list(odd.keys())
        it = bisect_left(od, y)

        if (it != 0):
            max_rem = max(max_rem, x + od[it])

    # Print the answer
    print (max_rem)

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [3, 2, 4, 11, 6, 7]

    # Size of the array
    N = len(arr)

    # Given value of K
    K = 7

    maxRemainder(arr, N, K)

# This code is contributed by mohit kumar 29
```

**Output:** 

```
6
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(N)*