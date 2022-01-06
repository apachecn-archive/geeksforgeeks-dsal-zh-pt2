# 找出和 N 最小的绝对差的一对

> 原文:[https://www . geesforgeks . org/find-a-pair-with-sum-n-having-mini-absolute-difference/](https://www.geeksforgeeks.org/find-a-pair-with-sum-n-having-minimum-absolute-difference/)

给定一个整数 **N** ，任务是找到一对截然不同的 **X** 和 **Y** 使得 **X + Y = N** 和[ABS(X–Y)](https://www.geeksforgeeks.org/program-to-find-absolute-value-of-a-given-number/)最小。

**示例:**

> **输入:** N = 11
> **输出:** 5 6
> **说明:**
> X = 5，Y = 6 满足给定方程。
> 因此，abs 的最小绝对值(X–Y)= 1。
> 
> **输入:**N = 12
> T3】输出: 5 7

**天真法:**解决这个问题最简单的方法是生成 **X** 和 **Y** 的所有可能值，其和等于 **N** 并打印 **X** 和 **Y** 的值，这给出了[ABS(X–Y)](https://www.geeksforgeeks.org/program-to-find-absolute-value-of-a-given-number/)的最小绝对值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> **如果 N % 2 == 1** ，则配对 **(N / 2)** 和 **(N / 2 + 1)** 的绝对差值最小。
> 否则，对**(N/2–1)**和 **(N / 2 + 1)** 的绝对差值最小。

按照以下步骤解决问题:

*   [检查 **N** 是否为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现属实，则打印**(N/2)****(N/2+1)**的楼层值作为所需答案。
*   否则，打印**(N/2–1)**和 **(N / 2 + 1)** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value of X and Y
// having minimum value of abs(X - Y)
void findXandYwithminABSX_Y(int N)
{
    // If N is an odd number
    if (N % 2 == 1) {
        cout << (N / 2) << " " << (N / 2 + 1);
    }

    // If N is an even number
    else {
        cout << (N / 2 - 1) << " " << (N / 2 + 1);
    }
}

// Driver Code
int main()
{
    int N = 12;
    findXandYwithminABSX_Y(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG {

    // Function to find the value
    // of X and Y having minimum
    // value of Math.abs(X - Y)
    static void findXandYwithminABSX_Y(int N)
    {
        // If N is an odd number
        if (N % 2 == 1) {
            System.out.print((N / 2) + " " + (N / 2 + 1));
        }

        // If N is an even number
        else {
            System.out.print((N / 2 - 1) + " "
                             + (N / 2 + 1));
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 12;
        findXandYwithminABSX_Y(N);
    }
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the value of X and Y
# having minimum value of abs(X - Y)

def findXandYwithminABSX_Y(N):

    # If N is an odd number
    if (N % 2 == 1):
        print((N // 2), (N // 2 + 1))

    # If N is an even number
    else:
        print((N // 2 - 1), (N // 2 + 1))

# Driver Code
if __name__ == '__main__':

    N = 12

    findXandYwithminABSX_Y(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG {

    // Function to find the value
    // of X and Y having minimum
    // value of Math.abs(X - Y)
    static void findXandYwithminABSX_Y(int N)
    {
        // If N is an odd number
        if (N % 2 == 1) {
            Console.Write((N / 2) + " " + (N / 2 + 1));
        }

        // If N is an even number
        else {
            Console.Write((N / 2 - 1) + " " + (N / 2 + 1));
        }
    }

    // Driver Code
    public static void Main()
    {
        int N = 12;
        findXandYwithminABSX_Y(N);
    }
}

// This code is contributed by bgangwar59
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

function findXandYwithminABSX_Y($N){

    // If N is an odd number
    if ($N % 2 == 1)
  {
    return ($N / 2) . " " . ($N / 2 + 1);
  }

  // If N is an even number
  else
  {
    return ($N /2 -1) . " " . ($N / 2 + 1);
  }

}

// Driver code  
$N = 12;
echo(findXandYwithminABSX_Y($N));

?>
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to find the value of X and Y
// having minimum value of abs(X - Y)
function findXandYwithminABSX_Y(N)
{

    // If N is an odd number
    if (N % 2 == 1)
    {
        document.write((N / 2) + " " + (N / 2 + 1));
    }

    // If N is an even number
    else
    {
        document.write((N / 2 - 1) + " " + (N / 2 + 1));
    }
}

// Driver Code

    let N = 12;
    findXandYwithminABSX_Y(N);

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
5 7
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)