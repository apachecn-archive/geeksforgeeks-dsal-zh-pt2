# 长度为 N 且值小于 K 的整数的计数，使得它们只包含给定集合中的数字

> 原文:[https://www . geesforgeks . org/长度为 n 且值小于 k 的整数计数，以便它们仅包含给定集合中的数字/](https://www.geeksforgeeks.org/count-of-integers-of-length-n-and-value-less-than-k-such-that-they-contain-digits-only-from-the-given-set/)

给定一组按排序顺序排列的数字 **A[]** 和两个整数 **N** 和 **K** ，任务是找出长度为 **N** 的可能数字中有多少个值小于 **K** ，并且这些数字仅来自给定的集合。**注意**可以多次使用同一个数字。

**示例:**

> **输入:** A[] = {0，1，5}，N = 1，K = 2
> **输出:** 2
> 只有有效数字是 0 和 1。
> 
> **输入:** A[] = {0，1，2，5}，N = 2，K = 21
> **输出:** 5
> 10，11，12，15，20 为有效数字。

**进场:**让 **d** 有**A【】**那么大。我们可以把这个问题分成三种更简单的情况。

1.  当 **N** 大于 **K** 的长度时，很明显，如果 N 的长度大于 K 的长度，或者如果 d 等于 0，则不可能有这样的数字。
2.  当 **N** 小于 **K** 的长度时，则长度为 **N** 的数字的所有可能组合都有效。还有，我们要记住 **0** 不能放在第一位。所以，如果 **A[]** 包含 **0** ，第一位可以用**(d–1)**方式填写。由于允许重复，且 **0** 可以占据其他位置，休息**N–1**位置可以用**d * d *……* d(N–1)**次填充，即以**d<sup>N–1</sup>**方式填充。所以答案是**(d–1)*(d<sup>N–1</sup>)**如果 **A[]** 包含 **0** 否则**d<sup>N</sup>T35】。**
3.  当 **N** 等于 **K** 的长度时，这是最棘手的部分。这部分需要用到[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。构造一个 **K** 的数字数组。姑且称之为**数字[]** 。设**第一个(i)** 为取其第一个 **i** 位形成的数字。让**低[i]** 表示 **A[]** 中小于 **i** 的元素个数。
    例如，423 的第一个(2)是 42。如果 A[] = {0，2}，则低[0] = 0，低[1] = 1，低[2] = 1，低[3] = 2。
    通过动态编程生成 **N** 位数。让 **dp[i]** 表示长度 **i** 的总数小于 **K** 的第一个 **i** 位数。
    元素在 **dp[i]** 中可以通过两种情况生成:
    *   对于所有 **K** 的**First(I–1)**小于**First(I–1)**的数字，我们可以在 **i <sup>th</sup>** 索引处放置任意一位数字。因此，**DP[I]= DP[I]+(DP[I–1]* d)**
    *   对于所有 **K** 的**第一位(I–1)**与**第一位(I–1)**相同的数字，我们只能放那些小于**数字【I】**的数字。因此， **dp[i] = dp[i] +低[数字[i]]** 。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 10

// Function to convert a number into vector
vector<int> numToVec(int N)
{
    vector<int> digit;

    // Push all the digits of N from the end
    // one by one to the vector
    while (N != 0) {
        digit.push_back(N % 10);
        N = N / 10;
    }

    // If the original number was 0
    if (digit.size() == 0)
        digit.push_back(0);

    // Reverse the vector elements
    reverse(digit.begin(), digit.end());

    // Return the required vector
    return digit;
}

// Function to return the count of B length integers
// which are less than C and they
// contain digits from set A[] only
int solve(vector<int>& A, int B, int C)
{
    vector<int> digit;
    int d, d2;

    // Convert number to digit array
    digit = numToVec(C);
    d = A.size();

    // Case 1: No such number possible as the
    // generated numbers will always
    // be greater than C
    if (B > digit.size() || d == 0)
        return 0;

    // Case 2: All integers of length B are valid
    // as they all are less than C
    else if (B < digit.size()) {
        // contain 0
        if (A[0] == 0 && B != 1)
            return (d - 1) * pow(d, B - 1);
        else
            return pow(d, B);
    }

    // Case 3
    else {
        int dp[B + 1] = { 0 };
        int lower[MAX + 1] = { 0 };

        // Update the lower[] array such that
        // lower[i] stores the count of elements
        // in A[] which are less than i
        for (int i = 0; i < d; i++)
            lower[A[i] + 1] = 1;
        for (int i = 1; i <= MAX; i++)
            lower[i] = lower[i - 1] + lower[i];

        bool flag = true;
        dp[0] = 0;
        for (int i = 1; i <= B; i++) {
            d2 = lower[digit[i - 1]];
            dp[i] = dp[i - 1] * d;

            // For first index we can't use 0
            if (i == 1 && A[0] == 0 && B != 1)
                d2 = d2 - 1;

            // Whether (i-1) digit of generated number
            // can be equal to (i - 1) digit of C
            if (flag)
                dp[i] += d2;

            // Is digit[i - 1] present in A ?
            flag = (flag & (lower[digit[i - 1] + 1]
                            == lower[digit[i - 1]] + 1));
        }
        return dp[B];
    }
}

// Driver code
int main()
{

    // Digits array
    vector<int> A = { 0, 1, 2, 5 };
    int N = 2;
    int k = 21;

    cout << solve(A, N, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 10;

// Function to convert a number into vector
static Vector<Integer> numToVec(int N)
{
    Vector<Integer> digit = new Vector<Integer>();

    // Push all the digits of N from the end
    // one by one to the vector
    while (N != 0)
    {
        digit.add(N % 10);
        N = N / 10;
    }

    // If the original number was 0
    if (digit.size() == 0)
        digit.add(0);

    // Reverse the vector elements
    Collections.reverse(digit);

    // Return the required vector
    return digit;
}

// Function to return the count
// of B length integers which are
// less than C and they contain
// digits from set A[] only
static int solve(Vector<Integer> A, int B, int C)
{
    Vector<Integer> digit = new Vector<Integer>();
    int d, d2;

    // Convert number to digit array
    digit = numToVec(C);
    d = A.size();

    // Case 1: No such number possible as the
    // generated numbers will always
    // be greater than C
    if (B > digit.size() || d == 0)
        return 0;

    // Case 2: All integers of length B are valid
    // as they all are less than C
    else if (B < digit.size())
    {
        // contain 0
        if (A.get(0) == 0 && B != 1)
            return (int) ((d - 1) * Math.pow(d, B - 1));
        else
            return (int) Math.pow(d, B);
    }

    // Case 3
    else
    {
        int []dp = new int[B + 1];
        int []lower = new int[MAX + 1];

        // Update the lower[] array such that
        // lower[i] stores the count of elements
        // in A[] which are less than i
        for (int i = 0; i < d; i++)
            lower[A.get(i) + 1] = 1;
        for (int i = 1; i <= MAX; i++)
            lower[i] = lower[i - 1] + lower[i];

        boolean flag = true;
        dp[0] = 0;
        for (int i = 1; i <= B; i++)
        {
            d2 = lower[digit.get(i - 1)];
            dp[i] = dp[i - 1] * d;

            // For first index we can't use 0
            if (i == 1 && A.get(0) == 0 && B != 1)
                d2 = d2 - 1;

            // Whether (i-1) digit of generated number
            // can be equal to (i - 1) digit of C
            if (flag)
                dp[i] += d2;

            // Is digit[i - 1] present in A ?
            flag = (flag & (lower[digit.get(i - 1) + 1] ==
                            lower[digit.get(i - 1)] + 1));
        }
        return dp[B];
    }
}

// Driver code
public static void main(String[] args)
{
    Integer arr[] = { 0, 1, 2, 5 };
    // Digits array
    Vector<Integer> A = new Vector<>(Arrays.asList(arr));
    int N = 2;
    int k = 21;

    System.out.println(solve(A, N, k));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX=10

# Function to convert a number into vector
def numToVec(N):

    digit = []

    # Push all the digits of N from the end
    # one by one to the vector
    while (N != 0):
        digit.append(N % 10)
        N = N // 10

    # If the original number was 0
    if (len(digit) == 0):
        digit.append(0)

    # Reverse the vector elements
    digit = digit[::-1]

    # Return the required vector
    return digit

# Function to return the count of B length integers
# which are less than C and they
# contain digits from set A[] only
def solve(A, B, C):
    d, d2 = 0,0

    # Convert number to digit array
    digit = numToVec(C)
    d = len(A)

    # Case 1: No such number possible as the
    # generated numbers will always
    # be greater than C
    if (B > len(digit) or d == 0):
        return 0

    # Case 2: All integers of length B are valid
    # as they all are less than C
    elif (B < len(digit)):
        # contain 0
        if (A[0] == 0 and B != 1):
            return (d - 1) * pow(d, B - 1)
        else:
            return pow(d, B)

    # Case 3
    else :
        dp=[0 for i in range(B + 1)]
        lower=[0 for i in range(MAX + 1)]

        # Update the lower[] array such that
        # lower[i] stores the count of elements
        # in A[] which are less than i
        for i in range(d):
            lower[A[i] + 1] = 1
        for i in range(1, MAX+1):
            lower[i] = lower[i - 1] + lower[i]

        flag = True
        dp[0] = 0
        for i in range(1, B+1):
            d2 = lower[digit[i - 1]]
            dp[i] = dp[i - 1] * d

            # For first index we can't use 0
            if (i == 1 and A[0] == 0 and B != 1):
                d2 = d2 - 1

            # Whether (i-1) digit of generated number
            # can be equal to (i - 1) digit of C
            if (flag):
                dp[i] += d2

            # Is digit[i - 1] present in A ?
            flag = (flag & (lower[digit[i - 1] + 1] == lower[digit[i - 1]] + 1))

        return dp[B]

# Driver code

# Digits array
A =[0, 1, 2, 5]
N = 2
k = 21

print(solve(A, N, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static int MAX = 10;

// Function to convert a number into vector
static List<int> numToVec(int N)
{
    List<int> digit = new List<int>();

    // Push all the digits of N from the end
    // one by one to the vector
    while (N != 0)
    {
        digit.Add(N % 10);
        N = N / 10;
    }

    // If the original number was 0
    if (digit.Count == 0)
        digit.Add(0);

    // Reverse the vector elements
    digit.Reverse();

    // Return the required vector
    return digit;
}

// Function to return the count
// of B length integers which are
// less than C and they contain
// digits from set A[] only
static int solve(List<int> A, int B, int C)
{
    List<int> digit = new List<int>();
    int d, d2;

    // Convert number to digit array
    digit = numToVec(C);
    d = A.Count;

    // Case 1: No such number possible as the
    // generated numbers will always
    // be greater than C
    if (B > digit.Count || d == 0)
        return 0;

    // Case 2: All integers of length B are valid
    // as they all are less than C
    else if (B < digit.Count)
    {
        // contain 0
        if (A[0] == 0 && B != 1)
            return (int) ((d - 1) * Math.Pow(d, B - 1));
        else
            return (int) Math.Pow(d, B);
    }

    // Case 3
    else
    {
        int []dp = new int[B + 1];
        int []lower = new int[MAX + 1];

        // Update the lower[] array such that
        // lower[i] stores the count of elements
        // in A[] which are less than i
        for (int i = 0; i < d; i++)
            lower[A[i] + 1] = 1;
        for (int i = 1; i <= MAX; i++)
            lower[i] = lower[i - 1] + lower[i];

        Boolean flag = true;
        dp[0] = 0;
        for (int i = 1; i <= B; i++)
        {
            d2 = lower[digit[i-1]];
            dp[i] = dp[i - 1] * d;

            // For first index we can't use 0
            if (i == 1 && A[0] == 0 && B != 1)
                d2 = d2 - 1;

            // Whether (i-1) digit of generated number
            // can be equal to (i - 1) digit of C
            if (flag)
                dp[i] += d2;

            // Is digit[i - 1] present in A ?
            flag = (flag & (lower[digit[i-1] + 1] ==
                            lower[digit[i-1]] + 1));
        }
        return dp[B];
    }
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 0, 1, 2, 5 };

    // Digits array
    List<int> A = new List<int>(arr);
    int N = 2;
    int k = 21;

    Console.WriteLine(solve(A, N, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
let MAX = 10;

// Function to convert a number into vector
function numToVec(N)
{
    let digit = [];

    // Push all the digits of N from the end
    // one by one to the vector
    while (N != 0)
    {
        digit.push(N % 10);
        N = Math.floor(N / 10);
    }

    // If the original number was 0
    if (digit.length == 0)
        digit.push(0);

    // Reverse the vector elements
    digit.reverse();

    // Return the required vector
    return digit;
}

// Function to return the count
// of B length integers which are
// less than C and they contain
// digits from set A[] only
function solve(A, B, C)
{
    let digit = [];
    let d, d2;

    // Convert number to digit array
    digit = numToVec(C);
    d = A.length;

    // Case 1: No such number possible as the
    // generated numbers will always
    // be greater than C
    if (B > digit.length || d == 0)
        return 0;

    // Case 2: All integers of length B are valid
    // as they all are less than C
    else if (B < digit.length)
    {

        // contain 0
        if (A[0] == 0 && B != 1)
            return  Math.floor((d - 1) *
                    Math.pow(d, B - 1));
        else
            return Math.floor(Math.pow(d, B));
    }

    // Case 3
    else
    {
        let dp = new Array(B + 1);
        let lower = new Array(MAX + 1);

          for(let i = 0; i < dp.length; i++)
        {
            dp[i] = 0;
        }
        for(let i = 0; i < lower.length; i++)
        {
            lower[i] = 0;
        }

        // Update the lower[] array such that
        // lower[i] stores the count of elements
        // in A[] which are less than i
        for(let i = 0; i < d; i++)
            lower[A[i] + 1] = 1;
        for(let i = 1; i <= MAX; i++)
            lower[i] = lower[i - 1] + lower[i];

        let flag = true;
        dp[0] = 0;
        for(let i = 1; i <= B; i++)
        {
            d2 = lower[digit[i - 1]];
            dp[i] = dp[i - 1] * d;

            // For first index we can't use 0
            if (i == 1 && A[0] == 0 && B != 1)
                d2 = d2 - 1;

            // Whether (i-1) digit of generated number
            // can be equal to (i - 1) digit of C
            if (flag)
                dp[i] += d2;

            // Is digit[i - 1] present in A ?
            flag = (flag & (lower[digit[i - 1] + 1] ==
                            lower[digit[i - 1]] + 1));
        }
        return dp[B];
    }
}

// Driver code
let arr = [ 0, 1, 2, 5 ];
let N = 2;
let k = 21;

document.write(solve(arr, N, k));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)