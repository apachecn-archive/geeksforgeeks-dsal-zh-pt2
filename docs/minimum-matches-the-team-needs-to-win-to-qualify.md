# 球队获得参赛资格所需的最少比赛次数

> 原文:[https://www . geesforgeks . org/最小匹配-团队需要赢才能获得资格/](https://www.geeksforgeeks.org/minimum-matches-the-team-needs-to-win-to-qualify/)

给定两个整数 **X** 和 **Y** ，其中 **X** 表示**合格所需的积分数**，而 **Y** 表示**剩余的匹配数**。球队赢场得 **2 分，输**场得 **1 分。任务是找到球队需要赢得的最少比赛次数，以便有资格参加下一轮比赛。
**举例:**** 

> **输入:** X = 10，Y = 5
> **输出:** 5
> 球队需要赢下所有比赛才能拿到 10 分。
> **输入:** X = 6，Y = 5
> **输出:** 1
> 如果球队单场获胜，其余 4 场比赛失利，他们仍然会出线。

一种**天真的方法**是通过迭代从 **0** 到 **Y** 的所有值来检查，并找出给我们 **X** 点的第一个值。
一种**有效的方法**是对将要赢得的比赛数量执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)以找出比赛的最小数量。最初**低= 0****高= X** ，然后我们检查条件**(mid * 2+(y–mid))≥X**。如果条件成立，则检查左半部分是否存在任何较低值，即**高=中-1**，否则检查右半部分，即**低=中+ 1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number of
// matches to win to qualify for next round
int findMinimum(int x, int y)
{

    // Do a binary search to find
    int low = 0, high = y;
    while (low <= high) {

        // Find mid element
        int mid = (low + high) >> 1;

        // Check for condition
        // to qualify for next round
        if ((mid * 2 + (y - mid)) >= x)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return low;
}

// Driver Code
int main()
{
    int x = 6, y = 5;
    cout << findMinimum(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the minimum number of
// matches to win to qualify for next round
static int findMinimum(int x, int y)
{

    // Do a binary search to find
    int low = 0, high = y;
    while (low <= high)
    {

        // Find mid element
        int mid = (low + high) >> 1;

        // Check for condition
        // to qualify for next round
        if ((mid * 2 + (y - mid)) >= x)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return low;
}

// Driver Code
public static void main (String[] args)
{
    int x = 6, y = 5;
    System.out.println(findMinimum(x, y));
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum number of
# matches to win to qualify for next round
def findMinimum(x, y):

    # Do a binary search to find
    low = 0
    high = y
    while (low <= high):

        # Find mid element
        mid = (low + high) >> 1

        # Check for condition
        # to qualify for next round
        if ((mid * 2 + (y - mid)) >= x):
            high = mid - 1
        else:
            low = mid + 1
    return low

# Driver Code
if __name__ == '__main__':
    x = 6
    y = 5
    print(findMinimum(x, y))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum number of
// matches to win to qualify for next round
static int findMinimum(int x, int y)
{

    // Do a binary search to find
    int low = 0, high = y;
    while (low <= high)
    {

        // Find mid element
        int mid = (low + high) >> 1;

        // Check for condition
        // to qualify for next round
        if ((mid * 2 + (y - mid)) >= x)
            high = mid - 1;
        else
            low = mid + 1;
    }
    return low;
}

// Driver code
static public void Main()
{
    int x = 6, y = 5;
    Console.WriteLine(findMinimum(x, y));
}
}

// This Code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum number of
// matches to win to qualify for next round
function findMinimum($x, $y)
{

    // Do a binary search to find
    $low = 0; $high = $y;
    while ($low <= $high)
    {

        // Find mid element
        $mid = ($low + $high) >> 1;

        // Check for condition$
        // to qualify for next round
        if (($mid * 2 + ($y - $mid)) >= $x)
            $high = $mid - 1;
        else
            $low = $mid + 1;
    }
    return $low;
}

// Driver Code
$x = 6; $y = 5;
echo findMinimum($x, $y);

// This code has been contributed
// by 29AjayKumar
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum number of
    // matches to win to qualify for next round
    function findMinimum(x, y)
    {

        // Do a binary search to find
        let low = 0, high = y;
        while (low <= high) {

            // Find mid element
            let mid = (low + high) >> 1;

            // Check for condition
            // to qualify for next round
            if ((mid * 2 + (y - mid)) >= x)
                high = mid - 1;
            else
                low = mid + 1;
        }
        return low;
    }

    let x = 6, y = 5;
    document.write(findMinimum(x, y));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(log y)