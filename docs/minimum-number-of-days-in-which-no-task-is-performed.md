# 不执行任务的最小天数

> 原文:[https://www . geesforgeks . org/无任务执行的最小天数/](https://www.geeksforgeeks.org/minimum-number-of-days-in-which-no-task-is-performed/)

给定一个由长度为 N 的值(0，1，2，3)组成的数组**arr【】**，代表任意一天可以完成的工作类型，这样任务要么是**A 型，要么是 B 型**。数组中的每个值定义为:
**0**–无任务可用。
**1**–B 型任务可用。
**2**–A 类任务可用。
**3**–任务 A 和任务 B 均可用。

如果同一类型的任务不能连续两天完成，则任务是最大限度地减少不执行任务的天数。

**示例:**

> **输入** : N = 4，arr = {0，1，3，2}
> **输出** : 2
> **说明**:以下是每天完成的任务类型。
> 第一天没有任务，所以他什么都不做，计数变成 1。
> 第二天执行 B 类任务
> 第三天两个任务都有，但是因为他前一天做了 B 类任务，所以他执行任务 A
> 最后一天有任务 A，但是他前一天做了同样的任务，所以他什么都不做，计数变成 2。
> 所以，2 是最终答案。
> 
> **输入:** N = 8，arr[] = {0，1，3，2，0，2，3，3}
> **输出:** 3

**天真的做法**:这个问题可以用**递归**解决。按照以下步骤解决给定的问题。

*   声明一个变量，比如 count = 0，来存储答案。
*   如果 arr[i]=0，则没有任务，因此不做任何事情并增加计数。
*   如果 arr[i]=1，则只有任务 B 可用，如果最后一天的任务是 B，则不做任何事情，并增加计数，否则执行任务 B
*   如果 arr[i]=2，则只有任务 A 可用，如果最后一天的任务是 A，则不做任何事情，并增加计数，否则执行任务 A
*   如果 arr[i]=3，并且最后一天的任务是 A，则执行任务 B，如果最后一天的任务是 B，则执行任务 A，否则执行任务，这将使不执行任务的天数最少。
*   使用变量 last 跟踪前一天的任务，该变量可以采用以下值:
    *   0–未执行任何任务。
    *   1–已执行的 A 类任务
    *   2–执行的 B 类任务

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;

int solve(int a[], int last, int n)
{
    // Base case
    if (n == 0)
        return 0;

    // Condition 1 (no task) so does nothing
    if (a[n - 1] == 0) {
        // Increase count
        return 1 + solve(a, 0, n - 1);
    }

    // Condition 2 (only task B)
    else if (a[n - 1] == 1) {
        // Last task is of type B
        // so can't perform it again
        if (last == 2)

            // Increase count
            return 1 + solve(a, 0, n - 1);
        else

            // Perform task B
            return solve(a, 2, n - 1);
    }

    // Condition 3 (only task A )
    else if (a[n - 1] == 2) {
        // Last task is of type A
        // so can't perform it again
        if (last == 1)

            // Increase count
            return 1 + solve(a, 0, n - 1);
        else

            // Perform task A
            return solve(a, 1, n - 1);
    }

    // Condition 4 (both task A and B)
    else {
        // Last task is of type A
        if (last == 1)

            // Perform task B
            return solve(a, 2, n - 1);

        // Last task is of type B
        else if (last == 2)

            // Perform task A
            return solve(a, 1, n - 1);
        else

            // Perform the minimum among both
            return min(solve(a, 2, n - 1),
                       solve(a, 1, n - 1));
    }
}

int main()
{
    // Number of days
    int N = 4;
    int arr[] = { 0, 1, 3, 2 };

    cout << solve(arr, 0, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

public class GFG
{

static int solve(int []a, int last, int n)
{
    // Base case
    if (n == 0)
        return 0;

    // Condition 1 (no task) so does nothing
    if (a[n - 1] == 0) {
        // Increase count
        return 1 + solve(a, 0, n - 1);
    }

    // Condition 2 (only task B)
    else if (a[n - 1] == 1) {
        // Last task is of type B
        // so can't perform it again
        if (last == 2)

            // Increase count
            return 1 + solve(a, 0, n - 1);
        else

            // Perform task B
            return solve(a, 2, n - 1);
    }

    // Condition 3 (only task A )
    else if (a[n - 1] == 2) {
        // Last task is of type A
        // so can't perform it again
        if (last == 1)

            // Increase count
            return 1 + solve(a, 0, n - 1);
        else

            // Perform task A
            return solve(a, 1, n - 1);
    }

    // Condition 4 (both task A and B)
    else {
        // Last task is of type A
        if (last == 1)

            // Perform task B
            return solve(a, 2, n - 1);

        // Last task is of type B
        else if (last == 2)

            // Perform task A
            return solve(a, 1, n - 1);
        else

            // Perform the minimum among both
            return Math.min(solve(a, 2, n - 1),
                       solve(a, 1, n - 1));
    }
}

public static void main(String args[])
{
    // Number of days
    int N = 4;
    int []arr = { 0, 1, 3, 2 };

    System.out.println(solve(arr, 0, N));

}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
def solve(a, last, n):

    # Base case
    if (n == 0):
        return 0

    # Condition 1 (no task) so does nothing
    if (a[n - 1] == 0):

        # Increase count
        return 1 + solve(a, 0, n - 1)

    # Condition 2 (only task B)
    elif (a[n - 1] == 1):

        # Last task is of type B
        # so can't perform it again
        if (last == 2):

            # Increase count
            return 1 + solve(a, 0, n - 1)
        else:
            # Perform task B
            return solve(a, 2, n - 1)

    # Condition 3 (only task A )
    elif (a[n - 1] == 2):

        # Last task is of type A
        # so can't perform it again
        if (last == 1):

            # Increase count
            return 1 + solve(a, 0, n - 1)
        else:
            # Perform task A
            return solve(a, 1, n - 1)

    # Condition 4 (both task A and B)
    else:
        # Last task is of type A
        if (last == 1):

            # Perform task B
            return solve(a, 2, n - 1)

        # Last task is of type B
        elif (last == 2):

            # Perform task A
            return solve(a, 1, n - 1)
        else:

            # Perform the minimum among both
            return min(solve(a, 2, n - 1),
                        solve(a, 1, n - 1))

# Number of days
N = 4
arr = [0, 1, 3, 2]

print(solve(arr, 0, N))

# This code is contributed by gfgking.
```

## C#

```
using System;

class GFG
{

static int solve(int []a, int last, int n)
{
    // Base case
    if (n == 0)
        return 0;

    // Condition 1 (no task) so does nothing
    if (a[n - 1] == 0) {
        // Increase count
        return 1 + solve(a, 0, n - 1);
    }

    // Condition 2 (only task B)
    else if (a[n - 1] == 1) {
        // Last task is of type B
        // so can't perform it again
        if (last == 2)

            // Increase count
            return 1 + solve(a, 0, n - 1);
        else

            // Perform task B
            return solve(a, 2, n - 1);
    }

    // Condition 3 (only task A )
    else if (a[n - 1] == 2) {
        // Last task is of type A
        // so can't perform it again
        if (last == 1)

            // Increase count
            return 1 + solve(a, 0, n - 1);
        else

            // Perform task A
            return solve(a, 1, n - 1);
    }

    // Condition 4 (both task A and B)
    else {
        // Last task is of type A
        if (last == 1)

            // Perform task B
            return solve(a, 2, n - 1);

        // Last task is of type B
        else if (last == 2)

            // Perform task A
            return solve(a, 1, n - 1);
        else

            // Perform the minimum among both
            return Math.Min(solve(a, 2, n - 1),
                       solve(a, 1, n - 1));
    }
}

public static void Main()
{
    // Number of days
    int N = 4;
    int []arr = { 0, 1, 3, 2 };

    Console.Write(solve(arr, 0, N));

}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

function solve(a, last, n)
{
    // Base case
    if (n == 0)
        return 0;

    // Condition 1 (no task) so does nothing
    if (a[n - 1] == 0) {
        // Increase count
        return 1 + solve(a, 0, n - 1);
    }

    // Condition 2 (only task B)
    else if (a[n - 1] == 1) {
        // Last task is of type B
        // so can't perform it again
        if (last == 2)

            // Increase count
            return 1 + solve(a, 0, n - 1);
        else

            // Perform task B
            return solve(a, 2, n - 1);
    }

    // Condition 3 (only task A )
    else if (a[n - 1] == 2) {
        // Last task is of type A
        // so can't perform it again
        if (last == 1)

            // Increase count
            return 1 + solve(a, 0, n - 1);
        else

            // Perform task A
            return solve(a, 1, n - 1);
    }

    // Condition 4 (both task A and B)
    else {
        // Last task is of type A
        if (last == 1)

            // Perform task B
            return solve(a, 2, n - 1);

        // Last task is of type B
        else if (last == 2)

            // Perform task A
            return solve(a, 1, n - 1);
        else

            // Perform the minimum among both
            return Math.min(solve(a, 2, n - 1),
                       solve(a, 1, n - 1));
    }
}

// Number of days
let N = 4;
let arr = [ 0, 1, 3, 2 ];

document.write(solve(arr, 0, N));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
2
```

**高效途径:**对上述途径进行优化[可采用动态规划](http://www.geeksforgeeks.org/dynamic-programming/)。使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)来存储先前的状态，以便可以利用那些先前的状态来计算进一步的结果。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[101][3];

int solve(int a[], int last, int n)
{
    // Base case
    if (n == 0)
        return 0;

    // If the value is pre-calculated return it
    if (dp[n][last] != -1)
        return dp[n][last];

    // Condition 1 (no task) so does nothing
    if (a[n - 1] == 0) {
        // Increase count
        return dp[n][last] = 1
                             + solve(a, 0, n - 1);
    }
    // Condition 2 (only task B)
    else if (a[n - 1] == 1) {
        // Last task is of type B
        // so can't perform it again
        if (last == 2)

            // Increase count
            return dp[n][last] = 1
                                 + solve(a, 0, n - 1);
        else
            // Perform task B
            return dp[n][last]
                   = solve(a, 2, n - 1);
    }

    // Condition 3 (only task A )
    else if (a[n - 1] == 2) {
        // Last task is of type A so can't

        if (last == 1)

            // Increase count
            return dp[n][last] = 1
                                 + solve(a, 0, n - 1);
        else

            // Perform task A
            return dp[n][last]
                   = solve(a, 1, n - 1);
    }
    // Condition 4 (both task A and B)
    else {
        // Last task is of type A
        if (last == 1)

            // Perform task B
            return dp[n][last]
                   = solve(a, 2, n - 1);

        // Last task is of type B
        else if (last == 2)
            return dp[n][last]
                   = solve(a, 1, n - 1);

        // Perform task A
        else

            // Perform the minimum among both
            return dp[n][last]
                   = min(solve(a, 2, n - 1),
                         solve(a, 1, n - 1));
    }
}

int main()
{
    int N = 4;
    int arr[] = { 0, 1, 3, 2 };

    // Initialize the space with -1
    memset(dp, -1, sizeof(dp));

    cout << solve(arr, 0, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

public class GFG
{

static int dp[][] = new int[101][3];

static int solve(int []a, int last, int n)
{
    // Base case
    if (n == 0)
        return 0;

    // If the value is pre-calculated return it
    if (dp[n][last] != -1)
        return dp[n][last];

    // Condition 1 (no task) so does nothing
    if (a[n - 1] == 0) {
        // Increase count
        return dp[n][last] = 1
                             + solve(a, 0, n - 1);
    }
    // Condition 2 (only task B)
    else if (a[n - 1] == 1) {
        // Last task is of type B
        // so can't perform it again
        if (last == 2)

            // Increase count
            return dp[n][last] = 1
                                 + solve(a, 0, n - 1);
        else
            // Perform task B
            return dp[n][last]
                   = solve(a, 2, n - 1);
    }

    // Condition 3 (only task A )
    else if (a[n - 1] == 2) {
        // Last task is of type A so can't

        if (last == 1)

            // Increase count
            return dp[n][last] = 1
                                 + solve(a, 0, n - 1);
        else

            // Perform task A
            return dp[n][last]
                   = solve(a, 1, n - 1);
    }
    // Condition 4 (both task A and B)
    else {
        // Last task is of type A
        if (last == 1)

            // Perform task B
            return dp[n][last]
                   = solve(a, 2, n - 1);

        // Last task is of type B
        else if (last == 2)
            return dp[n][last]
                   = solve(a, 1, n - 1);

        // Perform task A
        else

            // Perform the minimum among both
            return dp[n][last]
                   = Math.min(solve(a, 2, n - 1),
                         solve(a, 1, n - 1));
    }
}

public static void main(String args[])
{
    // Number of days
    int N = 4;
    int []arr = { 0, 1, 3, 2 };

    for(int i = 0; i < 101; i++) {
        for(int j = 0; j < 3; j++) {
            dp[i][j] = -1;
        }
    }

    System.out.println(solve(arr, 0, N));

}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
dp = [0] * 101

def solve(a, last, n):

    # Base case
    if (n == 0):
        return 0

    # If the value is pre-calculated return it
    if (dp[n][last] != -1):
        return dp[n][last]

    # Condition 1 (no task) so does nothing
    if (a[n - 1] == 0):

        # Increase count
        dp[n][last] = 1 + solve(a, 0, n - 1)

        return dp[n][last]

    # Condition 2 (only task B)
    elif (a[n - 1] == 1):

        # Last task is of type B
        # so can't perform it again
        if (last == 2):

            # Increase count
            dp[n][last] = 1 + solve(a, 0, n - 1)
            return dp[n][last]
        else:

            # Perform task B
            dp[n][last] = solve(a, 2, n - 1)
            return dp[n][last]

    # Condition 3 (only task A )
    elif (a[n - 1] == 2):

        # Last task is of type A so can't
        if (last == 1):

            # Increase count
            dp[n][last] = 1 + solve(a, 0, n - 1)
            return dp[n][last]
        else:
            dp[n][last] = solve(a, 1, n - 1)

            # Perform task A
            return dp[n][last]

    # Condition 4 (both task A and B)
    else:

        # Last task is of type A
        if (last == 1):
            dp[n][last] = solve(a, 2, n - 1)

            # Perform task B
            return dp[n][last]

        # Last task is of type B
        elif (last == 2):
            dp[n][last] = solve(a, 1, n - 1)
            return dp[n][last]

        # Perform task A
        else:
            dp[n][last] = min(solve(a, 2, n - 1),
                              solve(a, 1, n - 1))

            # Perform the minimum among both
            return dp[n][last]

# Driver code
N = 4
arr = [ 0, 1, 3, 2 ]

# Initialize the space with -1
for i in range(len(dp)):
    dp[i] = [-1] * 3

print(solve(arr, 0, N))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# Program to implement
// the above approach
using System;

class GFG
{

static int [,]dp = new int[101, 3];

static int solve(int []a, int last, int n)
{
    // Base case
    if (n == 0)
        return 0;

    // If the value is pre-calculated return it
    if (dp[n, last] != -1)
        return dp[n, last];

    // Condition 1 (no task) so does nothing
    if (a[n - 1] == 0) {
        // Increase count
        return dp[n, last] = 1
                             + solve(a, 0, n - 1);
    }
    // Condition 2 (only task B)
    else if (a[n - 1] == 1) {
        // Last task is of type B
        // so can't perform it again
        if (last == 2)

            // Increase count
            return dp[n, last] = 1
                                 + solve(a, 0, n - 1);
        else
            // Perform task B
            return dp[n, last]
                   = solve(a, 2, n - 1);
    }

    // Condition 3 (only task A )
    else if (a[n - 1] == 2) {
        // Last task is of type A so can't

        if (last == 1)

            // Increase count
            return dp[n, last] = 1
                                 + solve(a, 0, n - 1);
        else

            // Perform task A
            return dp[n, last]
                   = solve(a, 1, n - 1);
    }
    // Condition 4 (both task A and B)
    else {
        // Last task is of type A
        if (last == 1)

            // Perform task B
            return dp[n, last]
                   = solve(a, 2, n - 1);

        // Last task is of type B
        else if (last == 2)
            return dp[n, last]
                   = solve(a, 1, n - 1);

        // Perform task A
        else

            // Perform the minimum among both
            return dp[n, last]
                   = Math.Min(solve(a, 2, n - 1),
                         solve(a, 1, n - 1));
    }
}

public static void Main()
{
    // Number of days
    int N = 4;
    int []arr = { 0, 1, 3, 2 };

    for(int i = 0; i < 101; i++) {
        for(int j = 0; j < 3; j++) {
            dp[i, j] = -1;
        }
    }

    Console.Write(solve(arr, 0, N));

}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
  <script>

// JavaScript Program to implement
// the above approach

let  dp = new Array(101)
function solve(a, last, n)
{

    // Base case
    if (n == 0)
        return 0;

    // If the value is pre-calculated return it
    if (dp[n][last] != -1)
        return dp[n][last];

    // Condition 1 (no task) so does nothing
    if (a[n - 1] == 0) {
        // Increase count
        return dp[n][last] = 1
                             + solve(a, 0, n - 1);
    }

    // Condition 2 (only task B)
    else if (a[n - 1] == 1)
    {

        // Last task is of type B
        // so can't perform it again
        if (last == 2)

            // Increase count
            return dp[n][last] = 1
                                 + solve(a, 0, n - 1);
        else
            // Perform task B
            return dp[n][last]
                   = solve(a, 2, n - 1);
    }

    // Condition 3 (only task A )
    else if (a[n - 1] == 2)
    {

        // Last task is of type A so can't
        if (last == 1)

            // Increase count
            return dp[n][last] = 1
                                 + solve(a, 0, n - 1);
        else

            // Perform task A
            return dp[n][last]
                   = solve(a, 1, n - 1);
    }

    // Condition 4 (both task A and B)
    else
    {

        // Last task is of type A
        if (last == 1)

            // Perform task B
            return dp[n][last]
                   = solve(a, 2, n - 1);

        // Last task is of type B
        else if (last == 2)
            return dp[n][last]
                   = solve(a, 1, n - 1);

        // Perform task A
        else

            // Perform the minimum among both
            return dp[n][last]
                   = min(solve(a, 2, n - 1),
                         solve(a, 1, n - 1));
    }
}

    let N = 4;
    let arr = [ 0, 1, 3, 2 ];

    // Initialize the space with -1
    for(let i=0;i<dp.length;i++)
    {
        dp[i] = new Array(3).fill(-1);
    }

   document.write(solve(arr, 0, N) + "<br>")

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

**时间复杂度:** O(N)，其中 N 是 arr[]的大小。
**辅助空间:** O(N)，其中 N 是 arr[]的大小。