# 到达无限线上目标的最小移动次数|设定 2

> 原文:[https://www . geesforgeks . org/最小移动-到达-目标-无限线-集合-2/](https://www.geeksforgeeks.org/minimum-moves-reach-target-infinite-line-set-2/)

给定无限数线上的目标位置，(-无穷大到+无穷大)。从 0 开始，你必须按照描述的方式移动才能到达目标:在移动中，你可以向前或向后迈一步。找到达到目标所需的最小移动次数。

**示例:**

```
Input : target = 3
Output : 2
Explanation:
On the first move we step from 0 to 1.
On the second step we step from 1 to 3.

Input: target = 2
Output: 3
Explanation:
On the first move we step from 0 to 1.
On the second move we step  from 1 to -1.
On the third move we step from -1 to 2.
```

**进场:**

这个想法类似于 O(n)方法[中讨论的](https://www.geeksforgeeks.org/find-minimum-moves-reach-target-infinite-line/)。
继续加和= 1 + 2 +..+ n > =目标。求解这个二次方程给出最小的 n，使得和> = target，即求解 n ^ n(n+1)/2–target>= 0 中的 n 给出最小的 n.
如果和== target，答案为 n .现在下一个和大于 target 的情况。通过指数领先目标多少步来找出差异，即总和-目标。

**情况 1:** 差是偶数那么回答是 n，(因为总会有一个移动翻转会导致目标)。
**案例二:**差是奇数，那就多走一步，即加 n+1 求和，现在再取差。如果差是 n+1 就是答案，那么再走一步，这肯定会有所不同，即使答案是 n + 2。

**说明:**既然差是奇数。目标不是奇数就是偶数。

案例一:n 为偶数(1+2+3+……+n)，那么加 n + 1 就等于差为偶数。
情况 2 : n 是奇数那么加 n + 1 也没什么区别，即便如此，再走一步，也就是 n+2。

## C++

```
// CPP code to find minimum moves
// to reach target
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum steps
// to reach target
int StepstoReachTarget(int target)
{
    // Handling negatives
    // by symmetry
    target = abs(target);

    // Keep moving while sum is
    // smaller i.e calculating n
    int n = ceil((-1.0 + sqrt(1 + 8.0 * target)) / 2);
    int sum = n * (n + 1) / 2;

    if (sum == target)
        return n;

    int d = sum - target;

    // case 1 : d is even
    if ((d & 1) == 0)
        return n;

    // d is odd
    else
        return n + ((n & 1) ? 2 : 1);
}

// Driver code
int main()
{
    int target = 5;

    // Function call
    cout << StepstoReachTarget(target);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find minimum moves
// to reach target
import java.lang.*;

class GFG {

    // Function to find minimum steps
    // to reach target
    static int StepstoReachTarget(int target)
    {

        // Handling negatives
        // by symmetry
        target = Math.abs(target);

        // Keep moving while sum is
        // smaller i.e calculating n
        int n = (int)Math.ceil(
            (-1.0 + (int)Math.sqrt(1 + 8.0 * target)) / 2);

        int sum = n * (n + 1) / 2;

        if (sum == target)
            return n;

        int d = sum - target;

        // case 1 : d is even
        if ((d & 1) == 0)
            return n;

        // d is odd
        else
            return n + ((n & 1) != 0 ? 2 : 1);
    }

    // Driver code
    public static void main(String[] arg)
    {
        int target = 5;

        // Function call
        System.out.println(StepstoReachTarget(target));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python code to find minimum
# moves to reach target
import math

# Function to find minimum
# steps to reach target

def StepstoReachTarget(target):

    # Handling negatives
    # by symmetry
    target = abs(target)

    # Keep moving while sum is
    # smaller i.e calculating n
    n = math.ceil((-1.0 + math.sqrt(1 +
                                    8.0 * target)) / 2)
    sum = n * (n + 1) / 2

    if (sum == target):
        return n

    d = sum - target

    # case 1 : d is even
    if ((int(d) & 1) == 0):
        return n

    # d is odd
    else:
        if(int(d) & 1):
            return n + 2
        return n + 1

# Driver code
target = 5

# Function call
print(StepstoReachTarget(target))

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# code to find minimum moves
// to reach target
using System;

class GFG {

    // Function to find minimum steps
    // to reach target
    static int StepstoReachTarget(int target)
    {

        // Handling negatives
        // by symmetry
        target = Math.Abs(target);

        // Keep moving while sum is
        // smaller i.e calculating n
        int n = (int)Math.Ceiling(
            (-1.0 + (int)Math.Sqrt(1 + 8.0 * target)) / 2);

        int sum = n * (n + 1) / 2;

        if (sum == target)
            return n;

        int d = sum - target;

        // case 1 : d is even
        if ((d & 1) == 0)
            return n;

        // d is odd
        else
            return n + ((n & 1) != 0 ? 2 : 1);
    }

    // Driver code
    public static void Main()
    {
        int target = 5;

        // Function call
        Console.Write(StepstoReachTarget(target));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find minimum
// moves to reach target

// Function to find minimum
// steps to reach target
function StepstoReachTarget($target)
{
    // Handling negatives$
    // by symmetry$
    $target = abs($target);

    // Keep moving while sum is
    // smaller i.e calculating n
    $n = ceil((-1.0 + sqrt(1 +
                8.0 * $target)) / 2);
    $sum = $n * ($n + 1) / 2;

    if ($sum == $target)
        return $n;

    $d = $sum - $target;

    // case 1 : d is even
    if (($d & 1) == 0)
        return n;

    // d is odd
    else
        return $n + (($n & 1) ? 2 : 1);
}

// Driver code
$target = 5;

// Function call
echo StepstoReachTarget($target);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find minimum moves
// to reach target

// Function to find minimum steps
// to reach target
function StepstoReachTarget(target)
{

    // Handling negatives
    // by symmetry
    target = Math.abs(target);

    // Keep moving while sum is
    // smaller i.e calculating n
    let n = Math.ceil((-1.0 +
            Math.sqrt(1 + 8.0 * target)) / 2);

    let sum = n * (n + 1) / 2;

    if (sum == target)
        return n;

    let d = sum - target;

    // Case 1 : d is even
    if ((d & 1) == 0)
        return n;

    // d is odd
    else
        return n + ((n & 1) != 0 ? 2 : 1);
}

// Driver Code
let target = 5;

// Function call
document.write(StepstoReachTarget(target));

// This code is contributed by avijitmondal1998

</script>
```

**Output :** 

```
5
```