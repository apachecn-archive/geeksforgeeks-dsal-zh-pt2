# 使用位运算求两个数的平均值

> 原文:[https://www . geesforgeks . org/find-两位数平均值-使用位操作/](https://www.geeksforgeeks.org/find-average-of-two-numbers-using-bit-operation/)

给定两个整数 **x** 和 **y** ，任务是使用位操作找到这些数的平均值，即 **(x + y) / 2** 。**注意**该方法给出的结果是计算平均值的下限。
**举例:**

> **输入:** x = 2，y = 4
> **输出:** 3
> (2 + 4) / 2 = 3
> **输入:** x = 10，y = 9
> **输出:** 9

**方法:**两个数的平均值 **x** 和 **y** 可以使用如下的位操作来计算:

> **(x&y)+((x ^ y)>t5】1)**T2】

其中 **&** 是按位 AND， **^** 是按位 XOR，而 **> > 1** 是右移 1 位。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the average
// of x and y using bit operations
int getAverage(int x, int y)
{
    // Calculate the average
    // Floor value of (x + y) / 2
    int avg = (x & y) + ((x ^ y) >> 1);

    return avg;
}

// Driver code
int main()
{
    int x = 10, y = 9;

    cout << getAverage(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the average
    // of x and y using bit operations
    static int getAverage(int x, int y)
    {

        // Calculate the average
        // Floor value of (x + y) / 2
        int avg = (x & y) + ((x ^ y) >> 1);

        return avg;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 10, y = 9;

        System.out.print(getAverage(x, y));
    }
}
```

## 计算机编程语言

```
# Python 3 implementation of the approach

# Function to return the average
# of x and y using bit operations
def getAverage(x, y):

    # Calculate the average
    # Floor value of (x + y) / 2
    avg = (x & y) + ((x ^ y) >> 1);

    return avg

# Driver code
x = 10
y = 9
print(getAverage(x, y))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the average
    // of x and y using bit operations
    static int getAverage(int x, int y)
    {

        // Calculate the average
        // Floor value of (x + y) / 2
        int avg = (x & y) + ((x ^ y) >> 1);

        return avg;
    }

    // Driver code
    public static void Main()
    {
        int x = 10, y = 9;

        Console.WriteLine(getAverage(x, y));
    }
}

// This code is contributed by AnkitRai01
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the average
// of x and y using bit operations
function getAverage($x, $y)
{
    // Calculate the average
    // Floor value of (x + y) / 2
    $avg = ($x & $y) + (($x ^ $y) >> 1);

    return $avg;
}

// Driver code
    $x = 10;
    $y = 9;

    echo getAverage($x, $y);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach   

    // Function to return the average
    // of x and y using bit operations
    function getAverage(x , y)
    {

        // Calculate the average
        // Floor value of (x + y) / 2
        var avg = (x & y) + ((x ^ y) >> 1);

        return avg;
    }

    // Driver code
    var x = 10, y = 9;
    document.write(getAverage(x, y));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
9
```