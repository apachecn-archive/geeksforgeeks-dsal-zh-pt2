# 产生连续差异所需的最小数组插入数< = K

> 原文:[https://www . geesforgeks . org/minimum-array-insertions-需要进行连续差异/](https://www.geeksforgeeks.org/minimum-array-insertions-required-to-make-consecutive-difference/)

给定一个代表建筑物高度的整数数组 *H* 和一个整数 *K* 。任务是按照以下规则从第一栋建筑到达最后一栋建筑:

1.  只有当**| H<sub>I</sub>–H<sub>j</sub>|<= K**且建筑物在阵列中一个接一个出现时，才能从高度为**H<sub>I</sub>T7】的建筑物到达高度为**H<sub>j</sub>T3】的建筑物。****
2.  如果到达一个建筑是不可能的，那么可以在两个建筑之间插入一些中等高度的建筑。

找到在第 2 步中完成的最小插入次数，以便能够从第一个建筑到最后一个建筑。
**例:**

> **输入:** H[] = {2，4，8，16}，K = 3
> **输出:** 3
> 在高度 4 和 8 的建筑之间增加 1 栋高度 5 的建筑。
> 在 8、16 层高的建筑之间分别增加 2 栋 11、14 层高的建筑。
> **输入:** H[] = {5，55，100，1000}，K = 10
> **输出:** 97

**进场:**

*   从 *1 到 n-1* 运行一个循环，检查 ABS(H[I]–H[I-1])<= k
*   如果上述条件为真，则跳到循环的下一次迭代。
*   如果条件为假，则所需的插入将等于 ceil(diff/K)–1，其中 diff = ABS(H[I]–H[I-1])
*   打印最后的插入总数。

以下是上述方法的实现:

## C++

```
// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum
// number of insertions required
int minInsertions(int H[], int n, int K)
{
    // Initialize insertions to 0
    int inser = 0;

    for (int i = 1; i < n; ++i) {
        float diff = abs(H[i] - H[i - 1]);

        if (diff <= K)
            continue;
        else
            inser += ceil(diff / K) - 1;
    }

    // return total insertions
    return inser;
}

// Driver program
int main()
{
    int H[] = { 2, 4, 8, 16 }, K = 3;
    int n = sizeof(H) / sizeof(H[0]);
    cout << minInsertions(H, n, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG{
// Function to return minimum
// number of insertions required
static int minInsertions(int[] H, int n, int K)
{
    // Initialize insertions to 0
    int inser = 0;

    for (int i = 1; i < n; ++i) {
        float diff = Math.abs(H[i] - H[i - 1]);

        if (diff <= K)
            continue;
        else
            inser += Math.ceil(diff / K) - 1;
    }

    // return total insertions
    return inser;
}

// Driver program
public static void main(String[] args)
{
    int[] H = new int[]{ 2, 4, 8, 16 };
    int K = 3;
    int n = H.length;
    System.out.println(minInsertions(H, n, K));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of above approach
import math

# Function to return minimum
# number of insertions required
def minInsertions(H, n, K):

    # Initialize insertions to 0
    inser = 0;

    for i in range(1, n):
        diff = abs(H[i] - H[i - 1]);

        if (diff <= K):
            continue;
        else:
            inser += math.ceil(diff / K) - 1;

    # return total insertions
    return inser;

# Driver Code
H = [2, 4, 8, 16 ];
K = 3;
n = len(H);
print(minInsertions(H, n, K));

# This code is contributed
# by mits
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
// Function to return minimum
// number of insertions required
static int minInsertions(int[] H,
                         int n, int K)
{
    // Initialize insertions to 0
    int inser = 0;

    for (int i = 1; i < n; ++i)
    {
        float diff = Math.Abs(H[i] - H[i - 1]);

        if (diff <= K)
            continue;
        else
            inser += (int)Math.Ceiling(diff / K) - 1;
    }

    // return total insertions
    return inser;
}

// Driver Code
static void Main()
{
    int[] H = new int[]{ 2, 4, 8, 16 };
    int K = 3;
    int n = H.Length;
    Console.WriteLine(minInsertions(H, n, K));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to return minimum
// number of insertions required
function minInsertions($H, $n, $K)
{
    // Initialize insertions to 0
    $inser = 0;

    for ($i = 1; $i < $n; ++$i)
    {
        $diff = abs($H[$i] - $H[$i - 1]);

        if ($diff <= $K)
            continue;
        else
            $inser += ceil($diff / $K) - 1;
    }

    // return total insertions
    return $inser;
}

// Driver Code
$H = array(2, 4, 8, 16 );
$K = 3;
$n = sizeof($H);
echo minInsertions($H, $n, $K);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to return minimum
// number of insertions required
function minInsertions( H, n, K)
{
    // Initialize insertions to 0
    var inser = 0;

    for (var i = 1; i < n; ++i) {
        var diff = Math.abs(H[i] - H[i - 1]);

        if (diff <= K)
            continue;
        else
            inser += Math.ceil(diff / K) - 1;
    }

    // return total insertions
    return inser;
}

var H = [ 2, 4, 8, 16 ];
var K = 3;
var n = H.length;
document.write(minInsertions(H, n, K));

// This code is contributed by SoumikMondal
</script>
```

**Output**

```
3
```

**时间复杂度:** O(N)

**辅助空间:** O(1)