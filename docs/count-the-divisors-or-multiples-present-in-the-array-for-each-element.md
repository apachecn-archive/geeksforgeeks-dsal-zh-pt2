# 计算数组中每个元素的除数或倍数

> 原文:[https://www . geeksforgeeks . org/count-the-dividers-or-倍数-数组中每个元素的存在数/](https://www.geeksforgeeks.org/count-the-divisors-or-multiples-present-in-the-array-for-each-element/)

给定一个带有 **N** 整数的数组 **A[]** ，对于数组中的每个整数 **A[i]** ，任务是找出整数的个数 **A[j]** (j！= i)以使 **A[i] % A[j] = 0** 或 **A[j] % A[i] = 0** 。

**示例:**

> **输入:** A = {2，3，4，5，6 }
> **Outpu*****t*****:**2 1 0 2
> **说明:**
> 对于 i=0，有效指数为 2 和 4，为 4%2 = 0 和 6%2 = 0。
> 对于 i=1，唯一有效的索引是 4 作为 6%3 = 0。
> 对于 i=2，唯一有效的索引是 0，因为 4%2 = 0。
> 对于 i=3，没有有效的索引。
> 对于 i=0，有效指数为 0 和 1，即 6%2 = 0 和 6%3 = 0。
> 
> **输入:** A = {6，6，6，6，6 }
> T3】OutpuT5**t**T8**:**4 4 4 4 4 4

**方法:**利用满足给定条件的整数个数可以分为两种情况的观察，可以解决给定的问题。假设当前整数为**P****Q**为满足给定条件的整数。

*   **情况 1** 其中 **Q** 是 **P** 的倍数。因此，给定数组中可被 P 整除的整数个数是必需的答案。这种情况可以使用厄拉多塞的[筛的简单修改来处理，这里](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[讨论](https://www.geeksforgeeks.org/queries-counts-multiples-array/)。
*   **情况 2** 其中 **P** 是 **Q** 的倍数。因此，给定数组中 Q 除 P 的整数个数就是需要的答案。这种情况可以使用与第一种情况类似的筛子进行处理。

因此，任何整数所需的答案都是**情况 1** 和**情况 2** 的结果整数之和。在 **P = Q** 的情况下，**情况 1** 和**情况 2** 代表相同的值，应该只考虑一次。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of integers
// such that A[i]%A[j] = 0 or A[j]%A[i] = 0
// for each index of the array A[]
void countIndex(int A[], int N)
{

    // Stores the maximum integer in A[]
    int MAX = *max_element(A, A + N);

    // Stores the frequency of each
    // element in the array A[]
    vector<int> freq(MAX + 1, 0);

    for (int i = 0; i < N; i++)
        freq[A[i]]++;

    // Stores the valid integers in A[]
    // for all integers from 1 to MAX
    vector<int> res(MAX + 1, 0);

    for (int i = 1; i <= MAX; ++i) {
        for (int j = i; j <= MAX; j += i) {

            // Case where P = Q
            if (i == j) {

                // Subtract 1 because P & Q
                // cannot have same index
                res[i] += (freq[j] - 1);
            }
            else {
                // Case 1
                res[i] += freq[j];

                // Case 2
                res[j] += freq[i];
            }
        }
    }

    // Loop to print answer for
    // each index of array A[]
    for (int i = 0; i < N; i++) {
        cout << res[A[i]] << " ";
    }
}

// Driver Code
int main()
{
    int A[] = { 2, 3, 4, 5, 6 };
    int N = sizeof(A) / sizeof(int);

    // Function Call
    countIndex(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;

class GFG{

// Function to find the count of integers
// such that A[i]%A[j] = 0 or A[j]%A[i] = 0
// for each index of the array []A
static void countIndex(int []A, int N)
{

    // Stores the maximum integer in []A
    int MAX = Arrays.stream(A).max().getAsInt();

    // Stores the frequency of each
    // element in the array []A

    int []freq = new int[MAX + 1];

    for (int i = 0; i < N; i++)
        freq[A[i]]++;

    // Stores the valid integers in []A
    // for all integers from 1 to MAX
    int []res = new int[MAX + 1];

    for (int i = 1; i <= MAX; ++i) {
        for (int j = i; j <= MAX; j += i) {

            // Case where P = Q
            if (i == j) {

                // Subtract 1 because P & Q
                // cannot have same index
                res[i] += (freq[j] - 1);
            }
            else {
                // Case 1
                res[i] += freq[j];

                // Case 2
                res[j] += freq[i];
            }
        }
    }

    // Loop to print answer for
    // each index of array []A
    for (int i = 0; i < N; i++) {
        System.out.print(res[A[i]]+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int []A = { 2, 3, 4, 5, 6 };
    int N = A.length;

    // Function Call
    countIndex(A, N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 Program for the above approach

# Function to find the count of integers
# such that A[i]%A[j] = 0 or A[j]%A[i] = 0
# for each index of the array A[]
def countIndex(A, N):

    # Stores the maximum integer in A[]
    MAX = max(A)

    # Stores the frequency of each
    # element in the array A[]
    freq = [0 for i in range(MAX+1)]

    for i in range(N):
        if A[i] in freq:
            freq[A[i]] += 1
        else:
            freq[A[i]] = 1

    # Stores the valid integers in A[]
    # for all integers from 1 to MAX
    res = [0 for i in range(MAX+1)]

    for i in range(1, MAX + 1, 1):
        for j in range(i, MAX + 1, i):

            # Case where P = Q
            if (i == j):

                # Subtract 1 because P & Q
                # cannot have same index
                res[i] += (freq[j] - 1)
            else:
                # Case 1
                res[i] += freq[j]

                # Case 2
                res[j] += freq[i]

    # Loop to print answer for
    # each index of array A[]
    for i in range(N):
        print(res[A[i]],end = " ")

# Driver Code
if __name__ == '__main__':
    A = [2, 3, 4, 5, 6]
    N = len(A)

    # Function Call
    countIndex(A, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program of above approach
using System;

public class GFG {
    static void countIndex(int[] A, int N)
    {

        // Stores the maximum integer in []A
        int MAX = A[0];
        for (int i = 1; i < N; i++) {
            if (A[i] > MAX) {
                MAX = A[i];
            }
        }

        // Stores the frequency of each
        // element in the array []A
        int[] freq = new int[MAX + 1];

        for (int i = 0; i < N; i++)
            freq[A[i]]++;

        // Stores the valid integers in []A
        // for all integers from 1 to MAX
        int[] res = new int[MAX + 1];

        for (int i = 1; i <= MAX; ++i) {
            for (int j = i; j <= MAX; j += i) {

                // Case where P = Q
                if (i == j) {

                    // Subtract 1 because P & Q
                    // cannot have same index
                    res[i] += (freq[j] - 1);
                }
                else {
                    // Case 1
                    res[i] += freq[j];

                    // Case 2
                    res[j] += freq[i];
                }
            }
        }

        // Loop to print answer for
        // each index of array []A
        for (int i = 0; i < N; i++) {
            Console.Write(res[A[i]] + " ");
        }
    }

    // Driver Code
    static public void Main()
    {
        int[] A = { 2, 3, 4, 5, 6 };
        int N = A.Length;

        // Function Call
        countIndex(A, N);
    }
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to find the count of integers
        // such that A[i]%A[j] = 0 or A[j]%A[i] = 0
        // for each index of the array A[]
        function max_element(A, N) {
            let MAX = Number.MIN_VALUE;
            for (let i = 0; i < A.length; i++) {
                if (A[i] > MAX) {
                    MAX = A[i];
                }
            }
            return MAX;
        }
        function countIndex(A, N) {

            // Stores the maximum integer in A[]
            let MAX = max_element(A, A + N);

            // Stores the frequency of each
            // element in the array A[]
            let freq = new Array(MAX + 1).fill(0);

            for (let i = 0; i < N; i++)
                freq[A[i]]++;

            // Stores the valid integers in A[]
            // for all integers from 1 to MAX
            let res = new Array(MAX + 1).fill(0);

            for (let i = 1; i <= MAX; ++i) {
                for (let j = i; j <= MAX; j += i) {

                    // Case where P = Q
                    if (i == j) {

                        // Subtract 1 because P & Q
                        // cannot have same index
                        res[i] += (freq[j] - 1);
                    }
                    else {
                        // Case 1
                        res[i] += freq[j];

                        // Case 2
                        res[j] += freq[i];
                    }
                }
            }

            // Loop to print answer for
            // each index of array A[]
            for (let i = 0; i < N; i++) {
                document.write(res[A[i]] + " ");
            }
        }

        // Driver Code
        let A = [2, 3, 4, 5, 6];
        let N = A.length;

        // Function Call
        countIndex(A, N);

   // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2 1 1 0 2 
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(MAX)，其中 MAX 代表给定数组中的最大整数。*