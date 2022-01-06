# 动态编程|高投入与低投入任务问题

> 原文:[https://www . geesforgeks . org/dynamic-programming-high-effort-vs-low-effort-tasks-problem/](https://www.geeksforgeeks.org/dynamic-programming-high-effort-vs-low-effort-tasks-problem/)

给你 n 天时间，每天(di)你可以执行高投入任务(hi)或低投入任务(li)或无任务，条件是只有在前一天选择无任务时，你才能选择高投入任务。写一个程序，找出你能在这 n 天内完成的最大任务量。
**例:**

```
No. of days (n) = 5
Day      L.E.   H.E
1        1       3
2        5       6
3        4       8
4        5       7
5        3       6
Maximum amount of tasks 
        = 3 + 5 + 4 + 5 + 3 
        = 20
```

**最优子结构**
要找到第一天完成的最大任务量，我们需要比较两个选择:

1.  那一天去做高强度的任务，然后找到直到第(1–2)天完成的最大任务量。
2.  去做当天工作量较小的任务，找到第(I–1)天完成的最大任务量。

设高[1…n]为第 I 天高投入任务量的输入数组，低[1…n]为第 I 天低投入任务量的输入数组。
设 max_task (high []，low []，I)为返回到第二天为止完成的最大任务量的函数，那么它将返回 max(high[i] + max_task(high，low，(I–2))、low [i] + max_task (high，low，(I–1))))
因此，该问题具有最优子结构性质，因为该问题可以使用子问题的解来解决。
**重叠子问题**
下面是高努力与低努力任务问题的简单递归实现。实现简单地遵循上面提到的递归结构。因此，高投入与低投入任务问题同时具有动态规划问题的两个特性。

## C++

```
// A naive recursive C++ program to find maximum
// tasks.
#include <iostream>
using namespace std;

// Returns the maximum among the 2 numbers
int max(int x, int y)
{
    return (x > y ? x : y);
}

// Returns maximum amount of task that can be
// done till day n
int maxTasks(int high[], int low[], int n)
{
    // If n is less than equal to 0, then no
    // solution exists
    if (n <= 0)
        return 0;

    /* Determines which task to choose on day n,
    then returns the maximum till that day */
    return max(high[n - 1] + maxTasks(high, low, (n - 2)),
            low[n - 1] + maxTasks(high, low, (n - 1)));
}

// Driver code
int main()
{
    int n = 5;
    int high[] = {3, 6, 8, 7, 6};
    int low[] = {1, 5, 4, 5, 3};
    cout << maxTasks(high, low, n);
    return 0;
}

// This code is contributed by Shubhamsingh10
```

## C

```
// A naive recursive C program to find maximum
// tasks.
#include<stdio.h>

// Returns the maximum among the 2 numbers
int max(int x, int y)
{
    return (x > y ? x : y);
}

// Returns maximum amount of task that can be
// done till day n
int maxTasks(int high[], int low[], int n)
{
    // If n is less than equal to 0, then no
    // solution exists
    if (n <= 0)
        return 0;

    /* Determines which task to choose on day n,
       then returns the maximum till that day */
    return max(high[n-1] + maxTasks(high, low, (n-2)),
              low[n-1] + maxTasks(high, low, (n-1)));
}

// Driver program to test above function
int main()
{
    int n = 5;
    int high[] = {3, 6, 8, 7, 6};
    int low[] = {1, 5, 4, 5, 3};
    printf("%dn", maxTasks(high, low, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A naive recursive Java program
// to find maximum tasks.

class GFG{

    // Returns maximum amount of task
    // that can be done till day n
    static int maxTasks(int high[], int low[], int n)
    {

        // If n is less than equal to 0,
        // then no solution exists
        if (n <= 0)
            return 0;

        /* Determines which task to choose on day n,
            then returns the maximum till that day */
        return Math.max(high[n - 1] + maxTasks(high, low, (n - 2)),
                low[n - 1] + maxTasks(high, low, (n - 1)));
    }

    // Driver code
    public static void main(String []args)
    {
        int n = 5;
        int high[] = {3, 6, 8, 7, 6};
        int low[] = {1, 5, 4, 5, 3};
        System.out.println( maxTasks(high, low, n));
    }
}

// This code is contributed by Ita_c.
```

## 蟒蛇 3

```
# A naive recursive Python3 program to
# find maximum tasks.

# Returns maximum amount of task
# that can be done till day n
def maxTasks(high, low, n) :

    # If n is less than equal to 0,
    # then no solution exists
    if (n <= 0) :
        return 0

    # Determines which task to choose on day n,
    # then returns the maximum till that day
    return max(high[n - 1] + maxTasks(high, low, (n - 2)),
               low[n - 1] + maxTasks(high, low, (n - 1)));

# Driver Code
if __name__ == "__main__" :

    n = 5;
    high = [3, 6, 8, 7, 6]
    low = [1, 5, 4, 5, 3]
    print(maxTasks(high, low, n));

# This code is contributed by Ryuga
```

## C#

```
// A naive recursive C# program
// to find maximum tasks.
using System;

class GFG
{

    // Returns maximum amount of task
    // that can be done till day n
    static int maxTasks(int[] high,
                    int[] low, int n)
    {

        // If n is less than equal to 0,
        // then no solution exists
        if (n <= 0)
            return 0;

        /* Determines which task to choose on day n,
            then returns the maximum till that day */
        return Math.Max(high[n - 1] +
            maxTasks(high, low, (n - 2)), low[n - 1] +
            maxTasks(high, low, (n - 1)));
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        int[] high = {3, 6, 8, 7, 6};
        int[] low = {1, 5, 4, 5, 3};
        Console.Write( maxTasks(high, low, n));
    }
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive recursive PHP program to find maximum
// tasks.

// Returns maximum amount of task that can be
// done till day n
function maxTasks($high, $low, $n)
{
    // If n is less than equal to 0, then no
    // solution exists
    if ($n <= 0)
        return 0;

    /* Determines which task to choose on day n,
    then returns the maximum till that day */
    return max($high[$n - 1] + maxTasks($high, $low, ($n - 2)),
                $low[$n - 1] + maxTasks($high, $low, ($n - 1)));
}

// Driver Code
$n = 5;
$high = array(3, 6, 8, 7, 6);
$low = array(1, 5, 4, 5, 3);
print(maxTasks($high, $low, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// A naive recursive Java program
// to find maximum tasks.

    // Returns maximum amount of task
    // that can be done till day n
    function maxTasks(high, low, n)
    {

        // If n is less than equal to 0,
        // then no solution exists
        if (n <= 0)
            return 0;

        /* Determines which task to choose on day n,
            then returns the maximum till that day */
        return Math.max(high[n - 1] + maxTasks(high, low, (n - 2)),
                low[n - 1] + maxTasks(high, low, (n - 1)));
    }

    // Driver code

        let n = 5;
        let high = [3, 6, 8, 7, 6];
        let low = [1, 5, 4, 5, 3];
        document.write( maxTasks(high, low, n));;

</script>
```

**输出:**

```
20
```

需要注意的是，上面的函数一次又一次地计算相同的子问题。
因此，该问题具有重叠子问题性质。因此，高投入与低投入任务问题同时具有动态规划问题的特性。
**动态规划解决方案**

## C++

```
// A DP based C++ program to find maximum tasks.
#include <iostream>
using namespace std;

// Returns the maximum among the 2 numbers
int max(int x, int y)
{
    return (x > y ? x : y);
}

// Returns maximum amount of task that can be
// done till day n
int maxTasks(int high[], int low[], int n)
{
    // An array task_dp that stores the maximum
    // task done
    int task_dp[n+1];

    // If n = 0, no solution exists
    task_dp[0] = 0;

    // If n = 1, high effort task on that day will
    // be the solution
    task_dp[1] = high[0];

    // Fill the entire array determining which
    // task to choose on day i
    for (int i = 2; i <= n; i++)
        task_dp[i] = max(high[i-1] + task_dp[i-2],
                         low[i-1] + task_dp[i-1]);
    return task_dp[n];
}

// Driver program to test above function
int main()
{
    int n = 5;
    int high[] = {3, 6, 8, 7, 6};
    int low[] = {1, 5, 4, 5, 3};
    cout << maxTasks(high, low, n);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// A DP based C++ program to find maximum tasks.
#include<stdio.h>

// Returns the maximum among the 2 numbers
int max(int x, int y)
{
    return (x > y ? x : y);
}

// Returns maximum amount of task that can be
// done till day n
int maxTasks(int high[], int low[], int n)
{
    // An array task_dp that stores the maximum
    // task done
    int task_dp[n+1];

    // If n = 0, no solution exists
    task_dp[0] = 0;

    // If n = 1, high effort task on that day will
    // be the solution
    task_dp[1] = high[0];

    // Fill the entire array determining which
    // task to choose on day i
    for (int i = 2; i <= n; i++)
        task_dp[i] = max(high[i-1] + task_dp[i-2],
                         low[i-1] + task_dp[i-1]);
    return task_dp[n];
}

// Driver program to test above function
int main()
{
    int n = 5;
    int high[] = {3, 6, 8, 7, 6};
    int low[] = {1, 5, 4, 5, 3};
    printf("%d", maxTasks(high, low, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A DP based Java program to find maximum tasks.
class GFG
{

// Returns the maximum among the 2 numbers
static int max(int x, int y)
{
    return (x > y ? x : y);
}

// Returns maximum amount of task that can be
// done till day n
static int maxTasks(int []high, int []low, int n)
{
    // An array task_dp that stores the maximum
    // task done
    int[] task_dp = new int[n + 1];

    // If n = 0, no solution exists
    task_dp[0] = 0;

    // If n = 1, high effort task on that day will
    // be the solution
    task_dp[1] = high[0];

    // Fill the entire array determining which
    // task to choose on day i
    for (int i = 2; i <= n; i++)
        task_dp[i] = Math.max(high[i - 1] + task_dp[i - 2],
                        low[i - 1] + task_dp[i - 1]);
    return task_dp[n];
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    int []high = {3, 6, 8, 7, 6};
    int []low = {1, 5, 4, 5, 3};
    System.out.println(maxTasks(high, low, n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# A DP based Python3 program to find maximum tasks.
# Returns the maximum among the 2 numbers
def max1(x, y):

    return x if(x > y) else y;

# Returns maximum amount of task
# that can be done till day n
def maxTasks(high, low, n):

    # An array task_dp that stores
    # the maximum task done
    task_dp = [0] * (n + 1);

    # If n = 0, no solution exists
    task_dp[0] = 0;

    # If n = 1, high effort task
    # on that day will be the solution
    task_dp[1] = high[0];

    # Fill the entire array determining
    # which task to choose on day i
    for i in range(2, n + 1):
        task_dp[i] = max(high[i - 1] + task_dp[i - 2],
                          low[i - 1] + task_dp[i - 1]);
    return task_dp[n];

# Driver code
n = 5;
high = [3, 6, 8, 7, 6];
low = [1, 5, 4, 5, 3];
print(maxTasks(high, low, n));

# This code is contributed by mits
```

## C#

```
// A DP based C# program to find maximum tasks.
using System;

class GFG
{

// Returns the maximum among the 2 numbers
static int max(int x, int y)
{
    return (x > y ? x : y);
}

// Returns maximum amount of task that can be
// done till day n
static int maxTasks(int []high, int []low, int n)
{
    // An array task_dp that stores the maximum
    // task done
    int[] task_dp = new int[n + 1];

    // If n = 0, no solution exists
    task_dp[0] = 0;

    // If n = 1, high effort task on that day will
    // be the solution
    task_dp[1] = high[0];

    // Fill the entire array determining which
    // task to choose on day i
    for (int i = 2; i <= n; i++)
        task_dp[i] = max(high[i - 1] + task_dp[i - 2],
                        low[i - 1] + task_dp[i - 1]);
    return task_dp[n];
}

// Driver program to test above function
static void Main()
{
    int n = 5;
    int []high = {3, 6, 8, 7, 6};
    int []low = {1, 5, 4, 5, 3};
    Console.WriteLine(maxTasks(high, low, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A DP based PHP program to find maximum tasks.
// Returns the maximum among the 2 numbers
function max1($x, $y)
{
    return ($x > $y ? $x : $y);
}

// Returns maximum amount of task that can be
// done till day n
function maxTasks($high, $low, $n)
{
    // An array task_dp that stores the maximum
    // task done
    $task_dp = array($n + 1);

    // If n = 0, no solution exists
    $task_dp[0] = 0;

    // If n = 1, high effort task on that day will
    // be the solution
    $task_dp[1] = $high[0];

    // Fill the entire array determining which
    // task to choose on day i
    for ($i = 2; $i <= $n; $i++)
        $task_dp[$i] = max($high[$i - 1] + $task_dp[$i - 2],
                        $low[$i - 1] + $task_dp[$i - 1]);
    return $task_dp[$n];
}

// Driver code
{
    $n = 5;
    $high = array(3, 6, 8, 7, 6);
    $low = array(1, 5, 4, 5, 3);
    echo(maxTasks($high, $low, $n));
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// A DP based javascript program to find maximum tasks.

// Returns the maximum among the 2 numbers
function max(x , y)
{
    return (x > y ? x : y);
}

// Returns maximum amount of task that can be
// done till day n
function maxTasks(high , low , n)
{
    // An array task_dp that stores the maximum
    // task done
    var task_dp = Array.from({length: n+1}, (_, i) => 0);

    // If n = 0, no solution exists
    task_dp[0] = 0;

    // If n = 1, high effort task on that day will
    // be the solution
    task_dp[1] = high[0];

    // Fill the entire array determining which
    // task to choose on day i
    for (i = 2; i <= n; i++)
        task_dp[i] = Math.max(high[i - 1] + task_dp[i - 2],
                        low[i - 1] + task_dp[i - 1]);
    return task_dp[n];
}

// Driver code
var n = 5;
var high = [3, 6, 8, 7, 6];
var low = [1, 5, 4, 5, 3];
document.write(maxTasks(high, low, n));

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
20
```

**时间复杂度:** O(n)
本文由 **Akash Aggarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。