# 统计游戏中可以减少到零或更少的数字

> 原文:[https://www . geesforgeks . org/count-the-numbers-of-the-the-numbers-on-to-zero-or-less-in-a-game/](https://www.geeksforgeeks.org/count-the-numbers-that-can-be-reduced-to-zero-or-less-in-a-game/)

给定两个整数 **X** 和 **Y** 以及一组 **N** 整数。**玩家 A** 可以**将**数组的任意元素减少**X****玩家 B** 可以**将**数组的任意元素增加 **Y** 。任务是统计 **A** 可以减少到 **0** 或**少**的元素数量。他们都在无限时间内发挥最佳状态，A 先动。
**注:**一个数一旦减少到零或更少就不能增加。
**举例:**

> **输入:** a[] = {1，2，4，2，3}，X = 3，Y = 3
> **输出:** 2
> A 减少 2 到-1
> B 增加 1 到 4
> A 减少 2 到-1
> B 增加 4 到 7 游戏继续。
> **输入:** a[] = {1，2，4，2，3}，X = 3，Y = 2
> **输出:** 5

**进场:**由于游戏无限时间进行，如果 **X > Y** 我们打印 **N** 。现在需要针对 **X ≤ Y** 进行求解。数字可以有两种类型:

1.  不超过 **X** 的加 **Y** 表示**计数 1** ，可通过 **A** 减少至 **≤ 0** 。
2.  那些是 **< X** 并且在加上 **Y** 时超过 **X** 的说 **count2** 只有一半可以被 **A** 减少到 **≤ 0** ，因为他们正在进行最佳的比赛， **B** 会尝试增加这些数字中的任何一个，以便在他的每一个回合中变成 **> X** 。

所以，答案会是 **count1 + ((count2 + 1) / 2)** 。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of numbers
int countNumbers(int a[], int n, int x, int y)
{

    // Base case
    if (y < x)
        return n;

    // Count the numbers
    int count1 = 0, count2 = 0;
    for (int i = 0; i < n; i++) {

        if (a[i] + y <= x)
            count1++;
        else if (a[i] <= x)
            count2++;
    }

    int number = (count2 + 1) / 2 + count1;

    return number;
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 4, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    int x = 3, y = 3;
    cout << countNumbers(a, n, x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
    // Function to return the count of numbers
    static int countNumbers(int a[], int n, int x, int y)
    {

        // Base case
        if (y < x)
            return n;

        // Count the numbers
        int count1 = 0, count2 = 0;
        for (int i = 0; i < n; i++)
        {
            if (a[i] + y <= x)
                count1++;
            else if (a[i] <= x)
                count2++;
        }
        int number = (count2 + 1) / 2 + count1;
        return number;
    }

    // Driver Code
    public static void main(String []args)
    {
        int a[] = { 1, 2, 4, 2, 3 };
        int n = a.length;
        int x = 3, y = 3;
        System.out.println(countNumbers(a, n, x, y));   
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of numbers
def countNumbers( a,  n, x, y):

    # Base case
    if (y < x):
        return n

    # Count the numbers
    count1 = 0
    count2 = 0
    for i in range ( 0, n):

        if (a[i] + y <= x):
            count1 = count1 + 1
        elif (a[i] <= x):
            count2 = count2 + 1

    number = (count2 + 1) // 2 + count1

    return number

# Driver Code
a = [ 1, 2, 4, 2, 3 ]
n = len(a)

x = 3
y = 3
print(countNumbers(a, n, x, y))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the count of numbers
    static int countNumbers(int []a, int n, int x, int y)
    {

        // Base case
        if (y < x)
            return n;

        // Count the numbers
        int count1 = 0, count2 = 0;
        for (int i = 0; i < n; i++)
        {
            if (a[i] + y <= x)
                count1++;
            else if (a[i] <= x)
                count2++;
        }
        int number = (count2 + 1) / 2 + count1;
        return number;
    }

    // Driver Code
    public static void Main()
    {
        int [] a = { 1, 2, 4, 2, 3 };
        int n = a.Length;
        int x = 3, y = 3;
        Console.WriteLine(countNumbers(a, n, x, y));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of numbers
function countNumbers($a, $n, $x, $y)
{

    // Base case
    if ($y < $x)
        return $n;

    // Count the numbers
    $count1 = 0 ;
    $count2 = 0 ;
    for ($i = 0; $i < $n; $i++)
    {

        if ($a[$i] + $y <= $x)
            $count1++;
        else if ($a[$i] <= $x)
            $count2++;
    }

    $number = floor(($count2 + 1) / 2) + $count1;

    return $number;
}

// Driver Code
$a = array( 1, 2, 4, 2, 3 );
$n = sizeof($a);

$x = 3;
$y = 3;

echo countNumbers($a, $n, $x, $y);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the count of numbers
function countNumbers(a, n, x, y)
{

    // Base case
    if (y < x)
        return n;

    var i;
    // Count the numbers
    var count1 = 0, count2 = 0;
    for (i = 0; i < n; i++) {

        if (a[i] + y <= x)
            count1++;
        else if (a[i] <= x)
            count2++;
    }

    var number = (count2 + 1) / 2 + count1;

    return number;
}

// Driver Code
    var a = [1, 2, 4, 2, 3];
    var n = a.length;

    var x = 3, y = 3;
    document.write(parseInt(countNumbers(a, n, x, y)));

// This code is contributed by ipg2016107.
</script>
```

**Output:** 

```
2
```