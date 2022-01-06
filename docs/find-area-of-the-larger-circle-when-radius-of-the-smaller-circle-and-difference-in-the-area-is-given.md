# 给定小圆的半径和面积差时，求大圆的面积

> 原文:[https://www . geeksforgeeks . org/当给出较小圆的半径和面积差时，找到较大圆的面积/](https://www.geeksforgeeks.org/find-area-of-the-larger-circle-when-radius-of-the-smaller-circle-and-difference-in-the-area-is-given/)

给定两个整数 **r** 和 **d** ，其中 **r** 是较小圆的半径， **d** 是该圆与某个较大半径圆的面积之差。任务是找到大圆的面积。
**举例:**

> **输入:** r = 4，d = 5
> **输出:** 55.24
> 小圆面积= 3.14 * 4 * 4 = 50.24
> 55.24–50.24 = 5
> **输入:** r = 12，d = 3
> **输出:** 455.16

**逼近:**让小圆和大圆的半径分别为 **r** 和 **R** ，面积之差为 **d** 即**PI * R<sup>2</sup>–PI * R<sup>2</sup>= d**，其中 **PI = 3.14**
Or， **R <sup>2</sup> =(其中
现在大圆的面积可以计算为**PI * R<sup>2</sup>T27】。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const double PI = 3.14;

// Function to return the area
// of the bigger circle
double find_area(int r, int d)
{
    // Find the radius of
    // the bigger circle
    double R = d / PI;
    R += pow(r, 2);
    R = sqrt(R);

    // Calculate the area of
    // the bigger circle
    double area = PI * pow(R, 2);
    return area;
}

// Driver code
int main()
{
    int r = 4, d = 5;

    cout << find_area(r, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static double PI = 3.14;

    // Function to return the area
    // of the bigger circle
    static double find_area(int r, int d)
    {
        // Find the radius of
        // the bigger circle
        double R = d / PI;
        R += Math.pow(r, 2);
        R = Math.sqrt(R);

        // Calculate the area of
        // the bigger circle
        double area = PI * Math.pow(R, 2);
        return area;
    }

    // Driver code
    public static void main(String[] args)
    {
        int r = 4, d = 5;

        System.out.println(find_area(r, d));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
PI = 3.14
from math import pow, sqrt

# Function to return the area
# of the bigger circle
def find_area(r, d):

    # Find the radius of
    # the bigger circle
    R = d / PI
    R += pow(r, 2)
    R = sqrt(R)

    # Calculate the area of
    # the bigger circle
    area = PI * pow(R, 2)
    return area

# Driver code
if __name__ == '__main__':
    r = 4
    d = 5

    print(find_area(r, d))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

public class GFG
{
    static double PI = 3.14;

    // Function to return the area
    // of the bigger circle
    static double find_area(int r, int d)
    {
        // Find the radius of
        // the bigger circle
        double R = d / PI;
        R += Math.Pow(r, 2);
        R = Math.Sqrt(R);

        // Calculate the area of
        // the bigger circle
        double area = PI * Math.Pow(R, 2);
        return area;
    }

    // Driver code
    static public void Main ()
    {

        int r = 4, d = 5;
        Console.Write(find_area(r, d));
    }
}

// This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
const PI = 3.14;

// Function to return the area
// of the bigger circle
function find_area($r, $d)
{

    // Find the radius of
    // the bigger circle
    $R = $d / PI;
    $R += pow($r, 2);
    $R = sqrt($R);

    // Calculate the area of
    // the bigger circle
    $area = PI * pow($R, 2);
    return $area;
}

// Driver Code
$r = 4;
$d = 5;

echo (find_area($r, $d));

// This code is contributed by Naman_Garg
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

 let PI = 3.14;

// Function to return the area
// of the bigger circle
function find_area(r, d)
{
    // Find the radius of
    // the bigger circle
    let R = d / PI;
    R += Math.pow(r, 2);
    R = Math.sqrt(R);

    // Calculate the area of
    // the bigger circle
    let area = PI * Math.pow(R, 2);
    return area;
}

// Driver code
let r = 4, d = 5;
    document.write( find_area(r,d).toFixed(2));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
55.24
```