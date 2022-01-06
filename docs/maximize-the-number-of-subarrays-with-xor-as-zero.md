# 以异或为 0 最大化子阵数量

> 原文:[https://www . geeksforgeeks . org/最大化子数组的数量，异或等于零/](https://www.geeksforgeeks.org/maximize-the-number-of-subarrays-with-xor-as-zero/)

给定一组 N 个数字。任务是通过多次交换任何给定子阵列的阵列元素的位来最大化异或值为零的子阵列的数量。
**注:**1<= A【I】<= 10<sup>18</sup>
**例:**

> **输入:** a[] = {6，7，14}
> **输出:** 2
> 2 个子阵列是{7，14}和{6，7 和 14}，通过在子阵列中单独交换它们的位来实现。
> 斯巴莱{7，14}有效，因为 7 更改为 11(111 到 1011)，14 更改为 11，因此斯巴莱现在是{11，11}。Subarray {6，7，14}有效，因为 6 更改为 3，7 更改为 13，14 不变，因此 3^13^14 = 0。
> **输入:** a[] = {1，1}
> **输出:**

**方法:**第一个观察是，在任何给定的索引处，只有偶数个设置位可以导致异或值 0。由于数组元素的最大大小可以是 10 <sup>18</sup> 的数量级，我们可以假设 60 位用于交换。解决上述问题可以遵循以下步骤:

*   因为只需要设置位数，所以计算每个第 I 个元素中的设置位数。
*   为了通过交换位使任何子阵列的异或为零，需要同时满足两个条件。条件如下:
    1.  如果在任何 L-R 范围内有偶数个设置位，那么我们可以尝试对子阵列 0 进行异或运算。
    2.  如果比特的总和小于或等于任何给定范围内最大设置比特数的两倍，则可以使其异或为零。

上面已经解释了每个子阵列在 L-R 范围内需要做的数学工作。
一个**天真的解决方案**将是对每个子阵列进行迭代，明确地检查两个条件，并计算这些子阵列的数量。但是这样做的时间复杂度将是 O(N^2).
一个有效的解决方案将遵循以下步骤:

*   使用**前缀[]** 和数组计算只服从第一个条件的子阵个数。
*   第**步-1** 给出了子阵列的数量，它是比特的总和，甚至在 **O(N)** 复杂度中也是如此。
*   利用[包含-排除原理](https://www.geeksforgeeks.org/inclusion-exclusion-principle-and-programming-applications/)，我们可以明确的减去子阵中**2 *最大数**的设定位超过子阵中设定位之和的子阵数。
*   使用数学，我们可以减少步骤 3 中检查子阵列的数量，因为设置位的数量可以最小为 1，所以我们可以只检查长度为 60 的每个子阵列，因为超过该长度，第二个条件永远不能被篡改。
*   一旦完成，我们可以从在**步骤-1** 中获得的子阵列数量中减去该数量，以获得我们的答案。

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to count subarrays not satisfying condition 2
int exclude(int a[], int n)
{
    int count = 0;
    // iterate in the array
    for (int i = 0; i < n; i++) {

        // store the sum of set bits
        // in the subarray
        int s = 0;
        int maximum = 0;

        // iterate for range of 60 subarrays
        for (int j = i; j < min(n, i + 60); j++) {
            s += a[j];
            maximum = max(a[j], maximum);

            // check if falsifies the condition-2
            if (s % 2 == 0 && 2 * maximum > s)
                count++;
        }
    }

    return count;
}

// Function to count subarrays
int countSubarrays(int a[], int n)
{

    // replace the array element by number
    // of set bits in them
    for (int i = 0; i < n; i++)
        a[i] = __builtin_popcountll(a[i]);

    // calculate prefix array
    int pre[n];
    for (int i = 0; i < n; i++) {
        pre[i] = a[i];
        if (i != 0)

            pre[i] += pre[i - 1];
    }

    // Count the number of subarrays
    // satisfying step-1
    int odd = 0, even = 0;

    // count number of odd and even
    for (int i = 0; i < n; i++) {
        if (pre[i] & 1)
            odd++;
    }
    even = n - odd;

    // Increase even by 1 for 1, so that the
    // subarrays starting from the index-0
    // are also taken to count
    even++;

    // total subarrays satisfying condition-1 only
    int answer = (odd * (odd - 1) / 2) + (even * (even - 1) / 2);

    cout << answer << endl;

    // exclude total subarrays not satisfying condition2
    answer = answer - exclude(a, n);

    return answer;
}

// Driver Code
int main()
{

    int a[] = { 6, 7, 14 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << countSubarrays(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum element to
// be added such that the array can be partitioned
// into two contiguous subarrays with equal sums
import java.util.*;

class GFG
{

// Function to count subarrays not satisfying condition 2
static int exclude(int a[], int n)
{
    int count = 0;
    // iterate in the array
    for (int i = 0; i < n; i++)
    {

        // store the sum of set bits
        // in the subarray
        int s = 0;
        int maximum = 0;

        // iterate for range of 60 subarrays
        for (int j = i; j < Math.min(n, i + 60); j++)
        {
            s += a[j];
            maximum = Math.max(a[j], maximum);

            // check if falsifies the condition-2
            if (s % 2 == 0 && 2 * maximum > s)
                count++;
        }
    }

    return count;
}

// Function to count subarrays
static int countSubarrays(int a[], int n)
{

    // replace the array element by number
    // of set bits in them
    for (int i = 0; i < n; i++)
        a[i] = Integer.bitCount(a[i]);

    // calculate prefix array
    int []pre = new int[n];
    for (int i = 0; i < n; i++)
    {
        pre[i] = a[i];
        if (i != 0)

            pre[i] += pre[i - 1];
    }

    // Count the number of subarrays
    // satisfying step-1
    int odd = 0, even = 0;

    // count number of odd and even
    for (int i = 0; i < n; i++)
    {
        if (pre[i]%2== 1)
            odd++;
    }
    even = n - odd;

    // Increase even by 1 for 1, so that the
    // subarrays starting from the index-0
    // are also taken to count
    even++;

    // total subarrays satisfying condition-1 only
    int answer = (odd * (odd - 1) / 2) + (even * (even - 1) / 2);

    System.out.println(answer);

    // exclude total subarrays not satisfying condition2
    answer = answer - exclude(a, n);

    return answer;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 6, 7, 14 };
    int n = a.length;

    System.out.println(countSubarrays(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code for the given approach.

# Function to count subarrays not
# satisfying condition 2
def exclude(a, n):

    count = 0

    # iterate in the array
    for i in range(0, n):

        # store the sum of set bits
        # in the subarray
        s = 0
        maximum = 0

        # iterate for range of 60 subarrays
        for j in range(i, min(n, i + 60)):
            s += a[j]
            maximum = max(a[j], maximum)

            # check if falsifies the condition-2
            if s % 2 == 0 and 2 * maximum > s:
                count += 1

    return count

# Function to count subarrays
def countSubarrays(a, n):

    # replace the array element by
    # number of set bits in them
    for i in range(0, n):
        a[i] = bin(a[i]).count('1')

    # calculate prefix array
    pre = [None] * n
    for i in range(0, n):
        pre[i] = a[i]

        if i != 0:
            pre[i] += pre[i - 1]

    # Count the number of subarrays
    # satisfying step-1
    odd, even = 0, 0

    # count number of odd and even
    for i in range(0, n):
        if pre[i] & 1:
            odd += 1

    even = n - odd

    # Increase even by 1 for 1, so that the
    # subarrays starting from the index-0
    # are also taken to count
    even += 1

    # total subarrays satisfying condition-1 only
    answer = ((odd * (odd - 1) // 2) +
             (even * (even - 1) // 2))

    print(answer)

    # exclude total subarrays not
    # satisfying condition2
    answer = answer - exclude(a, n)

    return answer

# Driver Code
if __name__ == "__main__":

    a = [6, 7, 14]
    n = len(a)

    print(countSubarrays(a, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# Program to find the minimum element to
// be added such that the array can be partitioned
// into two contiguous subarrays with equal sums
using System;

class GFG
{

// Function to count subarrays not satisfying condition 2
static int exclude(int []a, int n)
{
    int count = 0;
    // iterate in the array
    for (int i = 0; i < n; i++)
    {

        // store the sum of set bits
        // in the subarray
        int s = 0;
        int maximum = 0;

        // iterate for range of 60 subarrays
        for (int j = i; j < Math.Min(n, i + 60); j++)
        {
            s += a[j];
            maximum = Math.Max(a[j], maximum);

            // check if falsifies the condition-2
            if (s % 2 == 0 && 2 * maximum > s)
                count++;
        }
    }

    return count;
}

// Function to count subarrays
static int countSubarrays(int []a, int n)
{

    // replace the array element by number
    // of set bits in them
    for (int i = 0; i < n; i++)
        a[i] = bitCount(a[i]);

    // calculate prefix array
    int []pre = new int[n];
    for (int i = 0; i < n; i++)
    {
        pre[i] = a[i];
        if (i != 0)

            pre[i] += pre[i - 1];
    }

    // Count the number of subarrays
    // satisfying step-1
    int odd = 0, even = 0;

    // count number of odd and even
    for (int i = 0; i < n; i++)
    {
        if (pre[i]%2== 1)
            odd++;
    }
    even = n - odd;

    // Increase even by 1 for 1, so that the
    // subarrays starting from the index-0
    // are also taken to count
    even++;

    // total subarrays satisfying condition-1 only
    int answer = (odd * (odd - 1) / 2) + (even * (even - 1) / 2);

    Console.WriteLine(answer);

    // exclude total subarrays not satisfying condition2
    answer = answer - exclude(a, n);

    return answer;
}

static int bitCount(long x)
{
    int setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 6, 7, 14 };
    int n = a.Length;

    Console.WriteLine(countSubarrays(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Function to count subarrays not
// satisfying condition 2
function exclude(a, n)
{
    let count = 0;
    // iterate in the array
    for (let i = 0; i < n; i++)
    {

        // store the sum of set bits
        // in the subarray
        let s = 0;
        let maximum = 0;

        // iterate for range of 60 subarrays
        for (let j = i; j < Math.min(n, i + 60); j++)
        {
            s += a[j];
            maximum = Math.max(a[j], maximum);

            // check if falsifies the condition-2
            if (s % 2 == 0 && 2 * maximum > s)
                count++;
        }
    }

    return count;
}

// Function to count subarrays
function countSubarrays(a, n)
{

    // replace the array element by number
    // of set bits in them
    for (let i = 0; i < n; i++)
        a[i] = bitCount(a[i]);

    // calculate prefix array
    let pre = new Array(n);
    for (let i = 0; i < n; i++) {
        pre[i] = a[i];
        if (i != 0)

            pre[i] += pre[i - 1];
    }

    // Count the number of subarrays
    // satisfying step-1
    let odd = 0, even = 0;

    // count number of odd and even
    for (let i = 0; i < n; i++) {
        if (pre[i] & 1)
            odd++;
    }
    even = n - odd;

    // Increase even by 1 for 1, so that the
    // subarrays starting from the index-0
    // are also taken to count
    even++;

    // total subarrays satisfying condition-1 only
    let answer = parseInt((odd * (odd - 1) / 2) +
                 (even * (even - 1) / 2));

    document.write(answer + "<br>");

    // exclude total subarrays not
    // satisfying condition2
    answer = answer - exclude(a, n);

    return answer;
}

function bitCount(x)
{
    let setBits = 0;
    while (x != 0) {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code

    let a = [ 6, 7, 14 ];
    let n = a.length;

    document.write(countSubarrays(a, n));

</script>
```

**Output:** 

```
3
2
```

**时间复杂度:** O(N*60)