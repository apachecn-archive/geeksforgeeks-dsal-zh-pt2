# 范围[L，R]

中两个数的最大可能位或

> 原文:[https://www . geeksforgeeks . org/最大可能位或范围内的两个数-l-r/](https://www.geeksforgeeks.org/maximum-possible-bitwise-or-of-the-two-numbers-from-the-range-l-r/)

给定一个范围**【L，R】**，任务是从给定的范围中找出某对 **(a，b)** 的最大位或。
**例:**

> **输入:** L = 10，R = 20
> **输出:** 31
> **输入:** L = 56，R = 77
> **输出:** 127

**方法:**首先，将给定的整数 **L** 和 **R** 转换为它们的二进制表示。现在，如果 **L** 的位数比 **R** 少，那么将零推到 **L** 的 MSB 侧，使 **L** 和 **R** 的位数相等。
现在从 MSB 侧比较 **L** 和 **R** 的各个位。由于 **R** 大于 **L** ，我们会发现 **i <sup>第</sup>位**位 **R** 为**1****I<sup>第</sup>位**位 **L** 为 **0** 的情况。所以在**之后我<sup>第</sup>位**位，使 **L** 的所有位成为 **1** 。这保证了在 **L** 位所做的修改不会超过 **R** ，所以只会在 **L** 和 **R** 之间。这样做还可以确保最大位“或”。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum bitwise
// OR of any pair from the given range
long long int max_bitwise_or(long long int L, long long int R)
{
    vector<long long int> v1, v2, v3;
    long long int z = 0, i, ans = 0, cnt = 1;

    // Converting L to its binary representation
    while (L > 0) {
        v1.push_back(L % 2);
        L = L / 2;
    }

    // Converting R to its binary representation
    while (R > 0) {
        v2.push_back(R % 2);
        R = R / 2;
    }

    // In order to make the number
    // of bits of L and R same
    while (v1.size() != v2.size()) {

        // Push 0 to the MSB
        v1.push_back(0);
    }

    for (i = v2.size() - 1; i >= 0; i--) {

        // When ith bit of R is 1
        // and ith bit of L is 0
        if (v2[i] == 1 && v1[i] == 0 && z == 0) {

            z = 1;
            continue;
        }

        // From MSB side set all bits of L to be 1
        if (z == 1) {

            // From (i+1)th bit, all bits
            // of L changed to be 1
            v1[i] = 1;
        }
    }

    for (i = 0; i < v2.size(); i++) {
        v3.push_back(v2[i] | v1[i]);
    }

    for (i = 0; i < v2.size(); i++) {
        if (v3[i] == 1) {
            ans += cnt;
        }
        cnt *= 2;
    }
    return ans;
}

// Driver code
int main()
{
    long long int L = 10, R = 20;

    cout << max_bitwise_or(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function to return the maximum bitwise
// OR of any pair from the given range
static int max_bitwise_or(int L, int R)
{
    Vector<Integer> v1 = new Vector<Integer>(),
                    v2 = new Vector<Integer>(),
                    v3 = new Vector<Integer>();

    int z = 0, i, ans = 0, cnt = 1;

    // Converting L to its binary representation
    while (L > 0)
    {
        v1.add(L % 2);
        L = L / 2;
    }

    // Converting R to its binary representation
    while (R > 0)
    {
        v2.add(R % 2);
        R = R / 2;
    }

    // In order to make the number
    // of bits of L and R same
    while (v1.size() != v2.size())
    {

        // Push 0 to the MSB
        v1.add(0);
    }

    for (i = v2.size() - 1; i >= 0; i--)
    {

        // When ith bit of R is 1
        // and ith bit of L is 0
        if (v2.get(i) == 1 && v1.get(i) == 0 && z == 0)
        {
            z = 1;
            continue;
        }

        // From MSB side set all bits of L to be 1
        if (z == 1)
        {

            // From (i+1)th bit, all bits
            // of L changed to be 1
            v1.remove(i);
            v1.add(i,1);
        }
    }

    for (i = 0; i < v2.size(); i++)
    {
        v3.add(v2.get(i) | v1.get(i));
    }

    for (i = 0; i < v2.size(); i++)
    {
        if (v3.get(i) == 1)
        {
            ans += cnt;
        }
        cnt *= 2;
    }
    return ans;
}

// Driver code
public static void main(String []args)
{
    int L = 10, R = 20;

    System.out.println(max_bitwise_or(L, R));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum bitwise
# OR of any pair from the given range
def max_bitwise_or(L, R):
    v1 = []
    v2 = []
    v3 = []
    z = 0
    i = 0
    ans = 0
    cnt = 1

    # Converting L to its binary representation
    while (L > 0):
        v1.append(L % 2)
        L = L // 2

    # Converting R to its binary representation
    while (R > 0):
        v2.append(R % 2)
        R = R // 2

    # In order to make the number
    # of bits of L and R same
    while (len(v1) != len(v2)):

        # Push 0 to the MSB
        v1.append(0)

    for i in range(len(v2) - 1, -1, -1):

        # When ith bit of R is 1
        # and ith bit of L is 0
        if (v2[i] == 1 and
            v1[i] == 0 and z == 0):
            z = 1
            continue

        # From MSB side set all bits of L to be 1
        if (z == 1):

            # From (i+1)th bit, all bits
            # of L changed to be 1
            v1[i] = 1

    for i in range(len(v2)):
        v3.append(v2[i] | v1[i])

    for i in range(len(v2)):
        if (v3[i] == 1):
            ans += cnt
        cnt *= 2

    return ans

# Driver code
L = 10
R = 20

print(max_bitwise_or(L, R))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the maximum bitwise
// OR of any pair from the given range
static int max_bitwise_or(int L, int R)
{
    List<int> v1 = new List<int>(),
              v2 = new List<int>(),
              v3 = new List<int>();

    int z = 0, i, ans = 0, cnt = 1;

    // Converting L to its binary representation
    while (L > 0)
    {
        v1.Add(L % 2);
        L = L / 2;
    }

    // Converting R to its binary representation
    while (R > 0)
    {
        v2.Add(R % 2);
        R = R / 2;
    }

    // In order to make the number
    // of bits of L and R same
    while (v1.Count != v2.Count)
    {

        // Push 0 to the MSB
        v1.Add(0);
    }

    for (i = v2.Count - 1; i >= 0; i--)
    {

        // When ith bit of R is 1
        // and ith bit of L is 0
        if (v2[i] == 1 && v1[i] == 0 && z == 0)
        {
            z = 1;
            continue;
        }

        // From MSB side set all bits of L to be 1
        if (z == 1)
        {

            // From (i+1)th bit, all bits
            // of L changed to be 1
            v1.RemoveAt(i);
            v1.Insert(i, 1);
        }
    }

    for (i = 0; i < v2.Count; i++)
    {
        v3.Add(v2[i] | v1[i]);
    }

    for (i = 0; i < v2.Count; i++)
    {
        if (v3[i] == 1)
        {
            ans += cnt;
        }
        cnt *= 2;
    }
    return ans;
}

// Driver code
public static void Main(String []args)
{
    int L = 10, R = 20;

    Console.WriteLine(max_bitwise_or(L, R));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum bitwise
// OR of any pair from the given range
function max_bitwise_or(L, R)
{
    let v1 = [], v2 = [], v3 = [];
    let z = 0, i, ans = 0, cnt = 1;

    // Converting L to its binary representation
    while (L > 0) {
        v1.push(L % 2);
        L = parseInt(L / 2);
    }

    // Converting R to its binary representation
    while (R > 0) {
        v2.push(R % 2);
        R = parseInt(R / 2);
    }

    // In order to make the number
    // of bits of L and R same
    while (v1.length != v2.length) {

        // Push 0 to the MSB
        v1.push(0);
    }

    for (i = v2.length - 1; i >= 0; i--) {

        // When ith bit of R is 1
        // and ith bit of L is 0
        if (v2[i] == 1 && v1[i] == 0 && z == 0) {

            z = 1;
            continue;
        }

        // From MSB side set all bits of L to be 1
        if (z == 1) {

            // From (i+1)th bit, all bits
            // of L changed to be 1
            v1[i] = 1;
        }
    }

    for (i = 0; i < v2.length; i++) {
        v3.push(v2[i] | v1[i]);
    }

    for (i = 0; i < v2.length; i++) {
        if (v3[i] == 1) {
            ans += cnt;
        }
        cnt *= 2;
    }
    return ans;
}

// Driver code
    let L = 10, R = 20;

    document.write(max_bitwise_or(L, R));

</script>
```

**Output:** 

```
31
```

**时间复杂度:**O(logR+logL)
T3】辅助空间: O(logR + logL)