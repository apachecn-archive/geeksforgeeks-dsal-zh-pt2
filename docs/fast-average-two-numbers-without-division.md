# 两个数无除法的快速平均

> 原文:[https://www . geeksforgeeks . org/fast-average-两数不除/](https://www.geeksforgeeks.org/fast-average-two-numbers-without-division/)

给定两个数字，不用除法求它们平均值的下限。

```
Input : x = 10, y = 12
Output : 11

Input : x = 10, y = 7
Output : 8
We take floor of sum.
```

想法是用[右移运算符](https://www.geeksforgeeks.org/bitwise-shift-operators-in-java/)，而不是做(x + y)/2，我们做(x + y) > > 1

## C++

```
// C++ program to find average without using
// division.
#include <bits/stdc++.h>
using namespace std;

int floorAvg(int x, int y) {
     return (x + y) >> 1; }

int main() {
  int x = 10, y = 20;
  cout << "Average = " << floorAvg(x, y) <<endl;
  return 0;
}

// This code is contributed by famously.
```

## C

```
// C program to find average without using
// division.
#include <stdio.h>

int floorAvg(int x, int y) {
     return (x + y) >> 1; }

int main() {
  int x = 10, y = 20;
  printf("\n\nAverage = %d\n\n", floorAvg(x, y));
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find average
// without using division
class GFG
{
    static int floorAvg(int x, int y) {
    return (x + y) >> 1; }

    // Driver code
    public static void main (String[] args)
    {
        int x = 10, y = 20;
        System.out.print(floorAvg(x, y));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find average
# without using division.
def floorAvg(x, y):
    return (x + y) >> 1

# Driver code
x = 10
y = 20

print("Average ", floorAvg(x, y))

# This code is contributed by sunny singh
```

## C#

```
// C# program to find average
// without using division
using System;

class GFG
{
    static int floorAvg(int x, int y)
    {
      return (x + y) >> 1;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int x = 10, y = 20;
        Console.Write("Average = ");
        Console.Write(floorAvg(x, y));
    }
}

// This code is contributed by parashar...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find average
// without using division.

// function returns
// the average
function floorAvg($x, $y)
{
    return ($x + $y) >> 1;

}

    // Driver Code
    $x = 10;
    $y = 20;
    echo "Average = ", floorAvg($x, $y);

// This Code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// average without using
// division.
function floorAvg(x, y)
{
    return (x + y) >> 1;
}

// Driver code
var x = 10, y = 20;

document.write("Average = " + floorAvg(x, y));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
Average = 15
```

**应用:**
我们在很多标准算法中需要两个数的平均下限，比如[合并排序](https://www.geeksforgeeks.org/merge-sort/)[二分搜索法](https://www.geeksforgeeks.org/binary-search/)等。由于我们使用按位运算符而不是除法，所以上述求平均值的方法更快。