# 三个连续元素中第二小的元素计数

> 原文:[https://www . geeksforgeeks . org/三个连续元素中第二小的元素数/](https://www.geeksforgeeks.org/count-of-elements-which-are-second-smallest-among-three-consecutive-elements/)

给定第一个 **N** 自然数的排列 **P** 。任务是找到元素数量 **P <sub>i</sub>** ，使得 **P <sub>i</sub>** 在**P<sub>I–1</sub>、P <sub>i</sub> 和 P <sub>i + 1</sub>** 中排名第二。
**例:**

> **输入:** P[] = {2，5，1，3，4}
> **输出:** 1
> 3 是唯一这样的元素。
> **输入:** P[] = {1，2，3，4}
> **输出:** 2

**方法:**遍历从 **1** 到**N–2**的排列(从零开始索引)，检查以下两个条件。如果这些条件中的任何一个满足，则增加所需的答案。

*   如果**P[I–1]<P[I]<P[I+1]**。
*   如果**P[I–1]>P[I]>P[I+1]**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of elements
// P[i] such that P[i] is the second smallest
// among P[i – 1], P[i] and P[i + 1]
int countElements(int p[], int n)
{
    // To store the required answer
    int ans = 0;

    // Traverse from the second element
    // to the second last element
    for (int i = 1; i < n - 1; i++) {
        if (p[i - 1] > p[i] and p[i] > p[i + 1])
            ans++;
        else if (p[i - 1] < p[i] and p[i] < p[i + 1])
            ans++;
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int p[] = { 2, 5, 1, 3, 4 };
    int n = sizeof(p) / sizeof(p[0]);

    cout << countElements(p, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of elements
// P[i] such that P[i] is the second smallest
// among P[i-1], P[i] and P[i + 1]
static int countElements(int p[], int n)
{
    // To store the required answer
    int ans = 0;

    // Traverse from the second element
    // to the second last element
    for (int i = 1; i < n - 1; i++)
    {
        if (p[i - 1] > p[i] && p[i] > p[i + 1])
            ans++;
        else if (p[i - 1] < p[i] && p[i] < p[i + 1])
            ans++;
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String []args)
{
    int p[] = { 2, 5, 1, 3, 4 };
    int n = p.length;

    System.out.println(countElements(p, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of elements
# P[i] such that P[i] is the second smallest
# among P[i – 1], P[i] and P[i + 1]
def countElements(p, n) :

    # To store the required answer
    ans = 0;

    # Traverse from the second element
    # to the second last element
    for i in range(1, n - 1) :

        if (p[i - 1] > p[i] and p[i] > p[i + 1]) :
            ans += 1;
        elif (p[i - 1] < p[i] and p[i] < p[i + 1]) :
            ans += 1;

    # Return the required answer
    return ans;

# Driver code
if __name__ == "__main__" :

    p = [ 2, 5, 1, 3, 4 ];
    n = len(p);

    print(countElements(p, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of elements
// P[i] such that P[i] is the second smallest
// among P[i-1], P[i] and P[i + 1]
static int countElements(int []p, int n)
{
    // To store the required answer
    int ans = 0;

    // Traverse from the second element
    // to the second last element
    for (int i = 1; i < n - 1; i++)
    {
        if (p[i - 1] > p[i] && p[i] > p[i + 1])
            ans++;
        else if (p[i - 1] < p[i] && p[i] < p[i + 1])
            ans++;
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void Main(String []args)
{
    int []p = { 2, 5, 1, 3, 4 };
    int n = p.Length;

    Console.WriteLine(countElements(p, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of elements
// P[i] such that P[i] is the second smallest
// among P[i-1], P[i] and P[i + 1]
    function countElements(p , n)
    {
        // To store the required answer
        var ans = 0;

        // Traverse from the second element
        // to the second last element
        for (i = 1; i < n - 1; i++) {
            if (p[i - 1] > p[i] && p[i] > p[i + 1])
                ans++;
            else if (p[i - 1] < p[i] && p[i] < p[i + 1])
                ans++;
        }

        // Return the required answer
        return ans;
    }

    // Driver code

        var p = [ 2, 5, 1, 3, 4 ];
        var n = p.length;

        document.write(countElements(p, n));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
1
```