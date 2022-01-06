# 基于参赛者之间最终距离的赛道长度

> 原文:[https://www . geeksforgeeks . org/基于参赛者最终距离的赛道长度/](https://www.geeksforgeeks.org/length-of-race-track-based-on-the-final-distance-between-participants/)

给定三个整数 **A，B** 和 **C** ，任务是找出一条赛道的长度，如果有三名选手参加比赛，第一名选手以 **A** 米的优势击败第二名选手，第一名选手以 **B** 米的优势击败第三名选手，第二名选手以 **C** 米的优势击败第三名选手。

**示例:**

> **输入:** A = 11，B = 90，C = 80
> T3】输出: 880
> 
> **输入:** A = 10，B = 20，C = 12
> T3】输出: 60

**进场:**
设 X 为赛道长度。

**情况 1:** 当第一位选手完成比赛时，3 位选手所跑的距离为:
第一位= X，第二位= X–A，第三位= X–B
让第一位选手完成比赛所用的时间为 **T <sub>1</sub> 。**

**情况 2:** 当第二名选手完成比赛时，剩下的 2 名选手所能跑的距离为:
秒= X，三分= X–C
让第二名选手完成比赛所用的时间为 **T <sub>2</sub> 。**

在情况 1 和情况 2 中，第二和第三赛车的速度比将是恒定的，这意味着:

> **=>((x–a)/t<sub>【1】</sub>)/(x–b)/t<sub>【1】</sub>=(x/t<sub>【2】</sub>)/(x–c)/t<sub>【2】</sub>)【t]**
> **=><sup>–a* x–c * x+a * c = x<sup>–b * x</sup></sup>****=>a ***

以下是上述方案的实施情况:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define int long long

int32_t main()
{
    int A = 11;
    int B = 90;
    int C = 80;

    int ans = C * A;
    ans = ans / (C + A - B);

    cout << ans << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the
// above approach

import java.util.Scanner;

class GFG {
    public static void main(String args[])
    {
        int a = 11;
        int b = 90;
        int c = 80;

        System.out.println(c * a
                           / (c + a - b));
    }
}
```

## 蟒蛇 3

```
# Python3 Program for the
# above approach

# Function to get the length
# of the race track
def findlength(a, b, c):
    # return the answer
    return c * a/(c + a-b)

a = 11
b = 90
c = 80

print(findlength(a, b, c))
```

## C#

```
// C# program for the above approach
using System;
class GFG{

static void Main()
{
    int a = 11;
    int b = 90;
    int c = 80;

    Console.WriteLine(c * a / (c + a - b));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Driver Code
let a = 11;
let b = 90;
let c = 80;

document.write(c * a / (c + a - b));

// This code is contributed by sanjoy_62   

</script>
```

**Output:** 

```
880
```

**注:**这是在**邮差(SDE 实习)**T4 问的面试问题