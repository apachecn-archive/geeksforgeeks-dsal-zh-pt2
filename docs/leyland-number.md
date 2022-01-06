# 莱兰号

> 原文:[https://www.geeksforgeeks.org/leyland-number/](https://www.geeksforgeeks.org/leyland-number/)

在数论中，莱兰数是形式为 **x <sup>y</sup> + y <sup>x</sup>** 的数，其中 x 和 y 是大于 1 和 1 的整数<y<= x。
给定一个正整数 **N** 。任务是以升序打印第一个 N 个 Leyland 编号。前几个莱兰数字是 8、17、32、54、57、100、……
**示例:**

```
Input : N = 1
Output : 8
22 + 22 = 4 + 4 = 8.

Input : N = 6
Output : 100
```

运行两个循环的想法，一个用于 x，另一个用于 y。外部循环从 2 到 n 开始，对于外部循环的每次迭代，运行内部循环从 2 t x 开始。并将 x <sup>y</sup> + y <sup>x</sup> 存储在数组中。计算完所有值后，对它们进行排序并打印前 n 个数字。
以下是本办法的实施情况:

## C++

```
// CPP program to print first N Leyland Numbers.
#include <bits/stdc++.h>
#define MAX 100
using namespace std;

// Print first n Leyland Number.
void leyland(int n)
{
    vector<int> ans;

    // Outer loop for x from 2 to n.
    for (int x = 2; x <= n; x++) {

        // Inner loop for y from 2 to x.
        for (int y = 2; y <= x; y++) {

            // Calculating x^y + y^x
            int temp = pow(x, y) + pow(y, x);

            ans.push_back(temp);
        }
    }

    // Sorting the all Leyland Number.
    sort(ans.begin(), ans.end());

    // Printing first n Leyland number.
    for (int i = 0; i < n; i++)
        cout << ans[i] << " ";
}

// Driven Program
int main()
{
    int n = 6;
    leyland(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print first N
// Leyland Numbers.
import java.util.*;
import java.lang.*;

public class GFG{

    private static final int MAX = 0;

    // Print first n Leyland Number.
    public static void leyland(int n)
    {
        List<Integer> ans = new ArrayList<Integer>();

        // Outer loop for x from 2 to n.
        for (int x = 2; x <= n; x++) {

            // Inner loop for y from 2 to x.
            for (int y = 2; y <= x; y++) {

                // Calculating x^y + y^x
                int temp = (int)Math.pow(x, y) +
                           (int)Math.pow(y, x);

                ans.add(temp);
            }
        }

        // Sorting the all Leyland Number.
        Collections.sort(ans);

        // Printing first n Leyland number.
        for (int i = 0; i < n; i++)
            System.out.print(ans.get(i) + " ");
    }

    // Driven Program
    public static void main(String args[])
    {
        int n = 6;
        leyland(n);
    }
}

// This code is contributed by Sachin Bisht
```

## 蟒蛇 3

```
# Python3 program to print first N
# Leyland Numbers.
import math

# Print first n Leyland Number.
def leyland(n):
    ans = []
    x = 2
    y = 2

    # Outer loop for x from 2 to n.
    while x <= n :

        # Inner loop for y from 2 to x.
        y = 2
        while y <= x :

            # Calculating x^y + y^x
            temp = pow(x, y) + pow(y, x)

            ans.append(temp);
            y = y + 1
        x = x + 1

    # Sorting the all Leyland Number.
    ans.sort();

    i = 0

    # Printing first n Leyland number.
    while i < n :
        print(ans[i], end = " ")
        i = i + 1

# Driver Code
n = 6
leyland(n)

# This code is contributed by rishabh_jain
```

## C#

```
// C# program to print
// first N Leyland Numbers.
using System;
using System.Collections;

class GFG
{

    // Print first n
    // Leyland Number.
    public static void leyland(int n)
    {
        ArrayList ans = new ArrayList();

        // Outer loop for x
        // from 2 to n.
        for (int x = 2; x <= n; x++)
        {

            // Inner loop for
            // y from 2 to x.
            for (int y = 2; y <= x; y++)
            {

                // Calculating x^y + y^x
                int temp = (int)Math.Pow(x, y) +
                           (int)Math.Pow(y, x);

                ans.Add(temp);
            }
        }

        // Sorting the all
        // Leyland Number.
        ans.Sort();

        // Printing first
        // n Leyland number.
        for (int i = 0 ; i < n; i++)
        {
            Console.Write(ans[i] + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int n = 6;
        leyland(n);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// first N Leyland Numbers.
$MAX = 100;

// Print first n
// Leyland Number.
function leyland($n)
{
    $ans;
    $index = 0;

    // Outer loop for
    // x from 2 to n.
    for ($x = 2; $x <= $n; $x++)
    {

        // Inner loop for
        // y from 2 to x.
        for ($y = 2; $y <= $x; $y++)
        {

            // Calculating x^y + y^x
            $temp = pow($x, $y) +
                    pow($y, $x);

            $ans[$index] = $temp;
            $index++;
        }
    }

    // Sorting the all
    // Leyland Number.
    sort($ans);

    // Printing first
    // n Leyland number.
    for ($i = 0; $i < $n; $i++)
        echo $ans[$i]. " ";
}

// Driver Code
$n = 6;
leyland($n);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to print
// first N Leyland Numbers.
let MAX = 100;

// Print first n
// Leyland Number.
function leyland(n)
{
    let ans = [];
    let index = 0;

    // Outer loop for
    // x from 2 to n.
    for (let x = 2; x <= n; x++)
    {

        // Inner loop for
        // y from 2 to x.
        for (let y = 2; y <= x; y++)
        {

            // Calculating x^y + y^x
            let temp = Math.pow(x, y) +
                    Math.pow(y, x);

            ans[index] = temp;
            index++;
        }
    }

    // Sorting the all
    // Leyland Number.
    console.log(ans)
    ans = ans.sort((a, b)=>a-b);
    console.log(ans)
    // Printing first
    // n Leyland number.
    for (let i = 0; i < n; i++)
        document.write(ans[i] + " ");
}

// Driver Code
let n = 6;
leyland(n);

// This code is contributed
// by _saurabh_jaiswal

</script>
```

**输出:**

```
8 17 32 54 57 100
```