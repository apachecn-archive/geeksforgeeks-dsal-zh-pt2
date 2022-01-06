# 排课所需的最小大厅数

> 原文:[https://www . geeksforgeeks . org/最低大厅-上课时间安排所需/](https://www.geeksforgeeks.org/minimum-halls-required-for-class-scheduling/)

给定 **N** 次讲座的时间，以及它们的开始时间和结束时间(包括开始时间和结束时间)，任务是找到举办所有课程所需的最小大厅数量，以便一个大厅在给定时间只能用于一次讲座。注意，最大结束时间可以是 10 <sup>5</sup> 。
**例:**

> **输入:**讲座[][] = {{0，5}，{1，2}，{1，10}}
> **输出:** 3
> 所有讲座必须在不同的大厅举行，因为
> 在时间实例 1 所有讲座都在进行中。
> **输入:**讲座[][] = {{0，5}，{1，2}，{6，10}}
> **输出:** 2

**进场:**

*   假设时间 T 从 0 开始。任务是找到在特定时间正在进行的讲座的最大数量。这将提供安排所有讲座所需的最少数量的大厅。
*   找出任何时候正在进行的讲座的数量。保留一个 prefix_sum[]，它将存储在时间 t 的任何时刻正在进行的讲座的数量。对于时间在[s，t]之间的任何讲座，请执行 prefix_sum[s]++和 prefix _ sum[t+1]–。
*   之后，这个前缀数组的累积和将给出在任何时刻正在进行的讲座的计数。
*   阵列中任何时刻 t 的最大值是所需的最小大厅数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 100001

// Function to return the minimum
// number of halls required
int minHalls(int lectures[][2], int n)
{

    // Array to store the number of
    // lectures ongoing at time t
    int prefix_sum[MAX] = { 0 };

    // For every lecture increment start
    // point s decrement (end point + 1)
    for (int i = 0; i < n; i++) {
        prefix_sum[lectures[i][0]]++;
        prefix_sum[lectures[i][1] + 1]--;
    }

    int ans = prefix_sum[0];

    // Perform prefix sum and update
    // the ans to maximum
    for (int i = 1; i < MAX; i++) {
        prefix_sum[i] += prefix_sum[i - 1];
        ans = max(ans, prefix_sum[i]);
    }

    return ans;
}

// Driver code
int main()
{
    int lectures[][2] = { { 0, 5 },
                          { 1, 2 },
                          { 1, 10 } };
    int n = sizeof(lectures) / sizeof(lectures[0]);

    cout << minHalls(lectures, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int MAX = 100001;

// Function to return the minimum
// number of halls required
static int minHalls(int lectures[][], int n)
{

    // Array to store the number of
    // lectures ongoing at time t
    int []prefix_sum = new int[MAX];

    // For every lecture increment start
    // point s decrement (end point + 1)
    for (int i = 0; i < n; i++)
    {
        prefix_sum[lectures[i][0]]++;
        prefix_sum[lectures[i][1] + 1]--;
    }

    int ans = prefix_sum[0];

    // Perform prefix sum and update
    // the ans to maximum
    for (int i = 1; i < MAX; i++)
    {
        prefix_sum[i] += prefix_sum[i - 1];
        ans = Math.max(ans, prefix_sum[i]);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int lectures[][] = {{ 0, 5 },
                        { 1, 2 },
                        { 1, 10 }};
    int n = lectures.length;

    System.out.println(minHalls(lectures, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 100001

# Function to return the minimum
# number of halls required
def minHalls(lectures, n) :

    # Array to store the number of
    # lectures ongoing at time t
    prefix_sum = [0] * MAX;

    # For every lecture increment start
    # point s decrement (end point + 1)
    for i in range(n) :
        prefix_sum[lectures[i][0]] += 1;
        prefix_sum[lectures[i][1] + 1] -= 1;

    ans = prefix_sum[0];

    # Perform prefix sum and update
    # the ans to maximum
    for i in range(1, MAX) :
        prefix_sum[i] += prefix_sum[i - 1];
        ans = max(ans, prefix_sum[i]);

    return ans;

# Driver code
if __name__ == "__main__" :

    lectures = [[ 0, 5 ],
                [ 1, 2 ],
                [ 1, 10 ]];

    n = len(lectures);

    print(minHalls(lectures, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MAX = 100001;

// Function to return the minimum
// number of halls required
static int minHalls(int [,]lectures, int n)
{

    // Array to store the number of
    // lectures ongoing at time t
    int []prefix_sum = new int[MAX];

    // For every lecture increment start
    // point s decrement (end point + 1)
    for (int i = 0; i < n; i++)
    {
        prefix_sum[lectures[i,0]]++;
        prefix_sum[lectures[i,1] + 1]--;
    }

    int ans = prefix_sum[0];

    // Perform prefix sum and update
    // the ans to maximum
    for (int i = 1; i < MAX; i++)
    {
        prefix_sum[i] += prefix_sum[i - 1];
        ans = Math.Max(ans, prefix_sum[i]);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int [,]lectures = {{ 0, 5 },
                       { 1, 2 },
                       { 1, 10 }};
    int n = lectures.GetLength(0);

    Console.WriteLine(minHalls(lectures, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

const MAX = 100001;

// Function to return the minimum
// number of halls required
function minHalls(lectures, n)
{

    // Array to store the number of
    // lectures ongoing at time t
    let prefix_sum = new Uint8Array(MAX);

    // For every lecture increment start
    // point s decrement (end point + 1)
    for (let i = 0; i < n; i++) {
        prefix_sum[lectures[i][0]]++;
        prefix_sum[lectures[i][1] + 1]--;
    }

    let ans = prefix_sum[0];

    // Perform prefix sum and update
    // the ans to maximum
    for (let i = 1; i < MAX; i++) {
        prefix_sum[i] += prefix_sum[i - 1];
        ans = Math.max(ans, prefix_sum[i]);
    }

    return ans;
}

// Driver code
    let lectures = [ [ 0, 5 ],
                        [ 1, 2 ],
                        [ 1, 10 ] ];
    let n = lectures.length;

    document.write(minHalls(lectures, n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3
```