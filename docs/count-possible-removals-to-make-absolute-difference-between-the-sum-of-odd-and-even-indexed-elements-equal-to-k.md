# 计算可能的移除，使奇数和偶数索引元素之和与 K 相等

之间产生绝对差异

> 原文:[https://www . geeksforgeeks . org/count-可能的移除次数-使奇数和偶数索引元素之和与 k 相等/](https://www.geeksforgeeks.org/count-possible-removals-to-make-absolute-difference-between-the-sum-of-odd-and-even-indexed-elements-equal-to-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是在从给定数组中一次移除任意一个元素后，找出奇数和偶数索引处元素的[和的绝对差为 **K** 的次数。](https://www.geeksforgeeks.org/python-separate-odd-and-even-index-elements/)

**示例:**

> **输入:** arr[] = {2，4，2}，K = 2
> **输出:** 2
> **说明:**
> 
> *   移除 **arr[0]** 将 arr[]修改为{4，2}。因此，奇数和偶数索引元素的和之差为 2。
> *   移除 **arr[1]** 将 **arr[]** 修改为{2，2}。因此，奇数和偶数索引元素之和的差值为 0。
> *   移除 **arr[2]** 将 arr[]修改为{2，4}。因此，奇数和偶数索引元素的和之差为 2。
> 
> 因此，奇数和偶数索引处元素和之差为 2 的次数为 2。
> 
> **输入:** arr[] = { 1，1，1，1，1 }，K = 0
> T3】输出: 5

**天真方法:**最简单的方法是[逐个移除每个数组元素](https://www.geeksforgeeks.org/delete-an-element-from-array-using-two-traversals-and-one-traversal/)，每次移除后，检查奇数和偶数索引处的[元素之和](https://www.geeksforgeeks.org/python-separate-odd-and-even-index-elements/)的[绝对差是否为 **K** 。如果发现为真，则递增计数。完成数组遍历后，打印**计数**的值。](https://www.geeksforgeeks.org/program-to-find-absolute-value-of-a-given-number/)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[后缀和](https://www.geeksforgeeks.org/python-suffix-list-sum/)数组。按照以下步骤解决问题:

*   将大小为 **(N + 2)** 的两个数组**前缀[]** 和**后缀[]** 初始化为 **0** ，分别存储奇数和偶数索引处元素的前缀和后缀和。
*   从索引 **2** 开始，将数组 **arr[]** 元素的前缀和存储在数组**前缀[]** 的奇数和偶数索引处。
*   从索引 **(N + 1)** 开始，将数组元素的后缀和 **arr[]** 存储在数组的奇数和偶数索引处**后缀和[]** 。
*   将变量**计数**初始化为 **0** 以存储奇数和偶数索引处元素之和的绝对差为 **K** 的次数
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，按照以下条件递增计数:
    *   如果当前元素**arr【I】**被移除，则检查**(前缀[I–1]+后缀[i + 2] )** 和
        **(前缀[I–2]+后缀[i + 1])** 的绝对差是否为 **K** 。
    *   如果发现差值为 **K** ，则将**计数**增加 **1** ，否则检查下一个元素。
*   分别去掉 **0 <sup>第</sup>T3】和**第**元素后，检查条件是否成立，并相应增加计数。**
*   经过上述步骤后，**计数**给出的元素总数被删除。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to check if difference
// between the sum of odd and even
// indexed elements after removing
// the first element is K or not
int findCount0th(vector<int>& arr,
                 int N, int K)
{
    // Stores the sum of elements
    // at odd and even indices
    int oddsum = 0, evensum = 0;

    for (int i = 1; i < N; i += 2) {
        oddsum += arr[i];
    }
    for (int i = 2; i < N; i += 2) {
        evensum += arr[i];
    }

    // Return 1 if difference is K
    if (abs(oddsum - evensum) == K)
        return 1;
    else
        return 0;
}

// Function to check if difference
// between the sum of odd and even
// indexed elements after removing
// the second element is K or not
int findCount1st(vector<int>& arr,
                 int N, int K)
{
    // Stores the sum of elements
    // at odd and even indices
    int evensum = arr[0], oddsum = 0;

    for (int i = 3; i < N; i += 2) {
        evensum += arr[i];
    }
    for (int i = 2; i < N; i += 2) {
        oddsum += arr[i];
    }

    // Return 1 if difference is K
    if (abs(oddsum - evensum) == K)
        return 1;
    else
        return 0;
}

// Function to count number of elements
// to be removed to make sum of
// differences between odd and even
// indexed elements equal to K
int countTimes(vector<int>& arr, int K)
{
    // Size of given array
    int N = (int)arr.size();

    // Base Conditions
    if (N == 1)
        return 1;
    if (N < 3)
        return 0;
    if (N == 3) {
        int cnt = 0;
        cnt += (abs(arr[0] - arr[1])
                        == K
                    ? 1
                    : 0)

               + (abs(arr[2] - arr[1])
                          == K
                      ? 1
                      : 0)

               + (abs(arr[0] - arr[2])
                          == K
                      ? 1
                      : 0);

        return cnt;
    }

    // Stores prefix and suffix sums
    vector<int> prefix(N + 2, 0);
    vector<int> suffix(N + 2, 0);

    // Base assignments
    prefix[0] = arr[0];
    prefix[1] = arr[1];
    suffix[N - 1] = arr[N - 1];
    suffix[N - 2] = arr[N - 2];

    // Store prefix sums of even
    // indexed elements
    for (int i = 2; i < N; i += 2) {
        prefix[i] = arr[i] + prefix[i - 2];
    }

    // Store prefix sums of odd
    // indexed elements
    for (int i = 3; i < N; i += 2) {
        prefix[i] = arr[i] + prefix[i - 2];
    }

    // Similarly, store suffix sums of
    // elements at even and odd indices
    for (int i = N - 3; i >= 0; i -= 2) {
        suffix[i] = arr[i] + suffix[i + 2];
    }
    for (int i = N - 4; i >= 0; i -= 2) {
        suffix[i] = arr[i] + suffix[i + 2];
    }

    // Stores the count of possible removals
    int count = 0;

    // Traverse and remove the ith element
    for (int i = 2; i < N; i++) {

        // If the current element is
        // excluded, then previous index
        // (i - 1) points to (i + 2)
        // and (i - 2) points to (i + 1)
        if (abs(prefix[i - 1] + suffix[i + 2]
                - prefix[i - 2] - suffix[i + 1])
            == K) {
            count++;
        }
    }

    // Find count when 0th element is removed
    count += findCount0th(arr, N, K);

    // Find count when 1st element is removed
    count += findCount1st(arr, N, K);

    // Count gives the required answer
    return count;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 4, 5, 6 };
    int K = 2;

    // Function call
    cout << countTimes(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if difference
// between the sum of odd and even
// indexed elements after removing
// the first element is K or not
static int findCount0th(int[] arr,
                 int N, int K)
{
    // Stores the sum of elements
    // at odd and even indices
    int oddsum = 0, evensum = 0;

    for (int i = 1; i < N; i += 2) {
        oddsum += arr[i];
    }
    for (int i = 2; i < N; i += 2) {
        evensum += arr[i];
    }

    // Return 1 if difference is K
    if (Math.abs(oddsum - evensum) == K)
        return 1;
    else
        return 0;
}

// Function to check if difference
// between the sum of odd and even
// indexed elements after removing
// the second element is K or not
static int findCount1st(int[] arr,
                 int N, int K)
{
    // Stores the sum of elements
    // at odd and even indices
    int evensum = arr[0], oddsum = 0;

    for (int i = 3; i < N; i += 2) {
        evensum += arr[i];
    }
    for (int i = 2; i < N; i += 2) {
        oddsum += arr[i];
    }

    // Return 1 if difference is K
    if (Math.abs(oddsum - evensum) == K)
        return 1;
    else
        return 0;
}

// Function to count number of elements
// to be removed to make sum of
// differences between odd and even
// indexed elements equal to K
static int countTimes(int[] arr, int K)
{
    // Size of given array
    int N = (int)arr.length;

    // Base Conditions
    if (N == 1)
        return 1;
    if (N < 3)
        return 0;
    if (N == 3) {
        int cnt = 0;
        cnt += (Math.abs(arr[0] - arr[1])
                        == K
                    ? 1
                    : 0)

               + (Math.abs(arr[2] - arr[1])
                          == K
                      ? 1
                      : 0)

               + (Math.abs(arr[0] - arr[2])
                          == K
                      ? 1
                      : 0);

        return cnt;
    }

    // Stores prefix and suffix sums
    int[]  prefix = new int[N + 2];
    int[]  suffix = new int[N + 2];
    Arrays.fill(prefix, 0);
    Arrays.fill(suffix, 0);

    // Base assignments
    prefix[0] = arr[0];
    prefix[1] = arr[1];
    suffix[N - 1] = arr[N - 1];
    suffix[N - 2] = arr[N - 2];

    // Store prefix sums of even
    // indexed elements
    for (int i = 2; i < N; i += 2) {
        prefix[i] = arr[i] + prefix[i - 2];
    }

    // Store prefix sums of odd
    // indexed elements
    for (int i = 3; i < N; i += 2) {
        prefix[i] = arr[i] + prefix[i - 2];
    }

    // Similarly, store suffix sums of
    // elements at even and odd indices
    for (int i = N - 3; i >= 0; i -= 2) {
        suffix[i] = arr[i] + suffix[i + 2];
    }
    for (int i = N - 4; i >= 0; i -= 2) {
        suffix[i] = arr[i] + suffix[i + 2];
    }

    // Stores the count of possible removals
    int count = 0;

    // Traverse and remove the ith element
    for (int i = 2; i < N; i++) {

        // If the current element is
        // excluded, then previous index
        // (i - 1) points to (i + 2)
        // and (i - 2) points to (i + 1)
        if (Math.abs(prefix[i - 1] + suffix[i + 2]
                - prefix[i - 2] - suffix[i + 1])
            == K) {
            count++;
        }
    }

    // Find count when 0th element is removed
    count += findCount0th(arr, N, K);

    // Find count when 1st element is removed
    count += findCount1st(arr, N, K);

    // Count gives the required answer
    return count;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 4, 5, 6 };
    int K = 2;

    // Function call
    System.out.println(countTimes(arr, K));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if difference
# between the sum of odd and even
# indexed elements after removing
# the first element is K or not
def findCount0th(arr, N, K):

    # Stores the sum of elements
    # at odd and even indices
    oddsum = 0
    evensum = 0

    for i in range(1, N, 2):
        oddsum += arr[i]

    for i in range(2, N, 2):
        evensum += arr[i]

    # Return 1 if difference is K
    if (abs(oddsum - evensum) == K):
        return 1
    else:
        return 0

# Function to check if difference
# between the sum of odd and even
# indexed elements after removing
# the second element is K or not
def findCount1st(arr, N, K):

    # Stores the sum of elements
    # at odd and even indices
    evensum = arr[0]
    oddsum = 0

    for i in range(3, N, 2):
        evensum += arr[i]

    for i in range(2, N, 2):
        oddsum += arr[i]

    # Return 1 if difference is K
    if (abs(oddsum - evensum) == K):
        return 1
    else:
        return 0

# Function to count number of elements
# to be removed to make sum of
# differences between odd and even
# indexed elements equal to K
def countTimes(arr, K):

    # Size of given array
    N = len(arr)

    # Base Conditions
    if (N == 1):
        return 1

    if (N < 3):
        return 0

    if (N == 3):
        cnt = 0

        if abs(arr[0] - arr[1]) == K:
            cnt += 1

        if abs(arr[2] - arr[1]) == K:
            cnt += 1

        if abs(arr[0] - arr[2]) == K:
            cnt += 1

        return cnt

    # Stores prefix and suffix sums
    prefix = [0] * (N + 2)
    suffix = [0] * (N + 2)

    # Base assignments
    prefix[0] = arr[0]
    prefix[1] = arr[1]
    suffix[N - 1] = arr[N - 1]
    suffix[N - 2] = arr[N - 2]

    # Store prefix sums of even
    # indexed elements
    for i in range(2, N, 2):
        prefix[i] = arr[i] + prefix[i - 2]

    # Store prefix sums of odd
    # indexed elements
    for i in range(3, N, 2):
        prefix[i] = arr[i] + prefix[i - 2]

    # Similarly, store suffix sums of
    # elements at even and odd indices
    for i in range(N - 3, -1, -2):
        suffix[i] = arr[i] + suffix[i + 2]

    for i in range( N - 4, -1, -2):
        suffix[i] = arr[i] + suffix[i + 2]

    # Stores the count of possible removals
    count = 0

    # Traverse and remove the ith element
    for i in range(2, N):

        # If the current element is
        # excluded, then previous index
        # (i - 1) points to (i + 2)
        # and (i - 2) points to (i + 1)
        if (abs(prefix[i - 1] + suffix[i + 2] -
                prefix[i - 2] - suffix[i + 1]) == K):
            count += 1

    # Find count when 0th element is removed
    count += findCount0th(arr, N, K)

    # Find count when 1st element is removed
    count += findCount1st(arr, N, K)

    # Count gives the required answer
    return count

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 4, 5, 6 ]
    K = 2

    # Function call
    print(countTimes(arr, K))

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if difference
// between the sum of odd and even
// indexed elements after removing
// the first element is K or not
static int findCount0th(int[] arr,
                        int N, int K)
{

    // Stores the sum of elements
    // at odd and even indices
    int oddsum = 0, evensum = 0;

    for(int i = 1; i < N; i += 2)
    {
        oddsum += arr[i];
    }
    for(int i = 2; i < N; i += 2)
    {
        evensum += arr[i];
    }

    // Return 1 if difference is K
    if (Math.Abs(oddsum - evensum) == K)
        return 1;
    else
        return 0;
}

// Function to check if difference
// between the sum of odd and even
// indexed elements after removing
// the second element is K or not
static int findCount1st(int[] arr,
                 int N, int K)
{

    // Stores the sum of elements
    // at odd and even indices
    int evensum = arr[0], oddsum = 0;

    for(int i = 3; i < N; i += 2)
    {
        evensum += arr[i];
    }
    for(int i = 2; i < N; i += 2)
    {
        oddsum += arr[i];
    }

    // Return 1 if difference is K
    if (Math.Abs(oddsum - evensum) == K)
        return 1;
    else
        return 0;
}

// Function to count number of elements
// to be removed to make sum of
// differences between odd and even
// indexed elements equal to K
static int countTimes(int[] arr, int K)
{

    // Size of given array
    int N = (int)arr.Length;

    // Base Conditions
    if (N == 1)
        return 1;
    if (N < 3)
        return 0;
    if (N == 3)
    {
        int cnt = 0;
        cnt += (Math.Abs(arr[0] - arr[1]) == K ? 1 : 0) +
               (Math.Abs(arr[2] - arr[1]) == K ? 1 : 0) +
               (Math.Abs(arr[0] - arr[2]) == K ? 1 : 0);

        return cnt;
    }

    // Stores prefix and suffix sums
    int[]  prefix = new int[N + 2];
    int[]  suffix = new int[N + 2];

    for(int i = 0; i < N + 2; i++)
    {
        prefix[i] = 0;
    }
    for(int i = 0; i < N + 2; i++)
    {
        suffix[i] = 0;
    }

    // Base assignments
    prefix[0] = arr[0];
    prefix[1] = arr[1];
    suffix[N - 1] = arr[N - 1];
    suffix[N - 2] = arr[N - 2];

    // Store prefix sums of even
    // indexed elements
    for(int i = 2; i < N; i += 2)
    {
        prefix[i] = arr[i] + prefix[i - 2];
    }

    // Store prefix sums of odd
    // indexed elements
    for(int i = 3; i < N; i += 2)
    {
        prefix[i] = arr[i] + prefix[i - 2];
    }

    // Similarly, store suffix sums of
    // elements at even and odd indices
    for(int i = N - 3; i >= 0; i -= 2)
    {
        suffix[i] = arr[i] + suffix[i + 2];
    }
    for(int i = N - 4; i >= 0; i -= 2)
    {
        suffix[i] = arr[i] + suffix[i + 2];
    }

    // Stores the count of possible removals
    int count = 0;

    // Traverse and remove the ith element
    for(int i = 2; i < N; i++)
    {

        // If the current element is
        // excluded, then previous index
        // (i - 1) points to (i + 2)
        // and (i - 2) points to (i + 1)
        if (Math.Abs(prefix[i - 1] + suffix[i + 2] -
                     prefix[i - 2] - suffix[i + 1]) == K)
        {
            count++;
        }
    }

    // Find count when 0th element is removed
    count += findCount0th(arr, N, K);

    // Find count when 1st element is removed
    count += findCount1st(arr, N, K);

    // Count gives the required answer
    return count;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 4, 5, 6 };
    int K = 2;

    // Function call
    Console.WriteLine(countTimes(arr, K));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to check if difference
    // between the sum of odd and even
    // indexed elements after removing
    // the first element is K or not
    function findCount0th(arr, N, K)
    {

        // Stores the sum of elements
        // at odd and even indices
        let oddsum = 0, evensum = 0;

        for(let i = 1; i < N; i += 2)
        {
            oddsum += arr[i];
        }
        for(let i = 2; i < N; i += 2)
        {
            evensum += arr[i];
        }

        // Return 1 if difference is K
        if (Math.abs(oddsum - evensum) == K)
            return 1;
        else
            return 0;
    }

    // Function to check if difference
    // between the sum of odd and even
    // indexed elements after removing
    // the second element is K or not
    function findCount1st(arr, N, K)
    {

        // Stores the sum of elements
        // at odd and even indices
        let evensum = arr[0], oddsum = 0;

        for(let i = 3; i < N; i += 2)
        {
            evensum += arr[i];
        }
        for(let i = 2; i < N; i += 2)
        {
            oddsum += arr[i];
        }

        // Return 1 if difference is K
        if (Math.abs(oddsum - evensum) == K)
            return 1;
        else
            return 0;
    }

    // Function to count number of elements
    // to be removed to make sum of
    // differences between odd and even
    // indexed elements equal to K
    function countTimes(arr, K)
    {

        // Size of given array
        let N = arr.length;

        // Base Conditions
        if (N == 1)
            return 1;
        if (N < 3)
            return 0;
        if (N == 3)
        {
            let cnt = 0;
            cnt += (Math.abs(arr[0] - arr[1]) == K ? 1 : 0) +
                   (Math.abs(arr[2] - arr[1]) == K ? 1 : 0) +
                   (Math.abs(arr[0] - arr[2]) == K ? 1 : 0);

            return cnt;
        }

        // Stores prefix and suffix sums
        let  prefix = new Array(N + 2);
        let  suffix = new Array(N + 2);

        for(let i = 0; i < N + 2; i++)
        {
            prefix[i] = 0;
        }
        for(let i = 0; i < N + 2; i++)
        {
            suffix[i] = 0;
        }

        // Base assignments
        prefix[0] = arr[0];
        prefix[1] = arr[1];
        suffix[N - 1] = arr[N - 1];
        suffix[N - 2] = arr[N - 2];

        // Store prefix sums of even
        // indexed elements
        for(let i = 2; i < N; i += 2)
        {
            prefix[i] = arr[i] + prefix[i - 2];
        }

        // Store prefix sums of odd
        // indexed elements
        for(let i = 3; i < N; i += 2)
        {
            prefix[i] = arr[i] + prefix[i - 2];
        }

        // Similarly, store suffix sums of
        // elements at even and odd indices
        for(let i = N - 3; i >= 0; i -= 2)
        {
            suffix[i] = arr[i] + suffix[i + 2];
        }
        for(let i = N - 4; i >= 0; i -= 2)
        {
            suffix[i] = arr[i] + suffix[i + 2];
        }

        // Stores the count of possible removals
        let count = 0;

        // Traverse and remove the ith element
        for(let i = 2; i < N; i++)
        {

            // If the current element is
            // excluded, then previous index
            // (i - 1) points to (i + 2)
            // and (i - 2) points to (i + 1)
            if (Math.abs(prefix[i - 1] + suffix[i + 2] -
                         prefix[i - 2] - suffix[i + 1]) == K)
            {
                count++;
            }
        }

        // Find count when 0th element is removed
        count += findCount0th(arr, N, K);

        // Find count when 1st element is removed
        count += findCount1st(arr, N, K);

        // Count gives the required answer
        return count;
    }

    let arr = [ 1, 2, 4, 5, 6 ];
    let K = 2;

    // Function call
    document.write(countTimes(arr, K));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)