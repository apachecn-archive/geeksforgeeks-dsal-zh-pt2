# 在给定饮酒量的情况下，判断杯子是否会空

> 原文:[https://www . geeksforgeeks . org/find-如果给定饮酒率，杯子将是空的或不空的/](https://www.geeksforgeeks.org/find-if-the-glass-will-be-empty-or-not-when-the-rate-of-drinking-is-given/)

给定一个直径等于 **D** 厘米的圆柱玻璃。玻璃杯中水的初始高度等于距离底部的 **H** 厘米。你以每秒**米**毫升的速度喝水。但是如果你不喝杯子里的水，水位会每秒增加 **N** 厘米。任务是找到使玻璃变空所需的时间，或者找到是否有可能使玻璃变空。
**举例:**

> **输入:** D = 1，H = 1，M = 1，N = 1
> **输出:** 3.65979
> **输入:** D = 1，H = 2，M = 3，N = 100
> **输出:** -1

**进场:**这是一道几何题。已知玻璃的面积为**派* r<sup>2</sup>T5【其中 **r** 代表半径即 **(D / 2)** 。因此，要找出每秒钟水消耗的速率，用给定的体积(已知 1 毫升等于 1 立方厘米)除以面积。
如果该值小于水倒入玻璃杯的速度，如果没有喝，则答案为**否**否则玻璃杯可能是空的。
找时间，除以**h/(v/(pie * r<sup>2</sup>)–e)**就是玻璃变空的时间。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

double pie = 3.1415926535897;

// Function to return the time when
// the glass will be empty
double findsolution(double d, double h,
                    double m, double n)
{
    double k = (4 * m) / (pie * d * d);

    // Check the condition when the
    // glass will never be empty
    if (n > k)
        return -1;

    // Find the time
    double ans = (h / (k - n));
    return ans;
}

// Driver code
int main()
{
    double d = 1, h = 1, m = 1, n = 1;

    cout << findsolution(d, h, m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

static double pie = 3.1415926535897;

// Function to return the time when
// the glass will be empty
static double findsolution(double d, double h,
                    double m, double n)
{
    double k = (4 * m) / (pie * d * d);

    // Check the condition when the
    // glass will never be empty
    if (n > k)
        return -1;

    // Find the time
    double ans = (h / (k - n));
    return ans;
}

// Driver code
public static void main(String[] args)
{
    double d = 1, h = 1, m = 1, n = 1;

    System.out.printf("%.5f",findsolution(d, h, m, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
pie = 3.1415926535897

# Function to return the time when
# the glass will be empty
def findsolution(d, h, m, n):

    k = (4 * m) / (pie * d * d)

    # Check the condition when the
    # glass will never be empty
    if (n > k):
        return -1

    # Find the time
    ans = (h / (k - n))
    return round(ans, 5)

# Driver code
d = 1
h = 1
m = 1
n = 1

print(findsolution(d, h, m, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static double pie = 3.1415926535897;

// Function to return the time when
// the glass will be empty
static double findsolution(double d, double h,
                           double m, double n)
{
    double k = (4 * m) / (pie * d * d);

    // Check the condition when the
    // glass will never be empty
    if (n > k)
        return -1;

    // Find the time
    double ans = (h / (k - n));
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    double d = 1, h = 1, m = 1, n = 1;

    Console.Write("{0:F5}",
            findsolution(d, h, m, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
    const pie = 3.1415926535897;

    // Function to return the time when
    // the glass will be empty
    function findsolution(d , h , m , n) {
        var k = (4 * m) / (pie * d * d);

        // Check the condition when the
        // glass will never be empty
        if (n > k)
            return -1;

        // Find the time
        var ans = (h / (k - n));
        return ans;
    }

    // Driver code

        var d = 1, h = 1, m = 1, n = 1;

         document.write(findsolution(d, h, m, n).toFixed(5));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
3.65979
```