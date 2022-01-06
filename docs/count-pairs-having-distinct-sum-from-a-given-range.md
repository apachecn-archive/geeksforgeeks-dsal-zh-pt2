# 对给定范围内具有不同总和的配对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-with-distinct-sum-from-a-给定范围/](https://www.geeksforgeeks.org/count-pairs-having-distinct-sum-from-a-given-range/)

给定两个正整数 **L** 和 **R** ，任务是从总和不同的范围**【L，R】**中找到元素对的数量。

**示例:**

> **输入:** L = 2，R = 3
> **输出:** 3
> **解释:**
> 所有可能的元素对都在范围[2，3]内{(2，2)、(2，3)、(3，2)、(3，3)}。因为对(2，3)和(3，2)的和相等，所以具有不同和的对的计数是 3。
> 
> **输入:** L = 2，R = 2
> T3】输出: 1

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **firstNum** ，来存储两个对可以得到的最小和，即 **2 * L** 。
*   初始化一个变量，比如 **lastNum** ，以存储两个对可以获得的最高和，即 **2 * R** 。
*   初始化一个变量，比如 **cntPairs** ，以存储具有不同和的对的计数，即**lastNum–first num+1**。
*   最后，打印 **cntPairs** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count pairs made
// up of elements from the range
// [L, R] having distinct sum
long countPairs(long L, long R)
{

    // Stores the least sum which
    // can be formed by the pairs
    long firstNum = 2 * L;

    // Stores the highest sum which
    // can be formed by the pairs
    long lastNum = 2 * R;

    // Stores the count of pairs
    // having distinct sum
    long Cntpairs = lastNum - firstNum + 1;

    // Print the count of pairs
    cout << Cntpairs;
}

// Driver Code
int main()
{
    long L = 2, R = 3;

    // Function call to count
    // the number of pairs
    // having distinct sum in
    // the range [L, R]
    countPairs(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach

import java.io.*;

class GFG {

    // Function to count pairs made
    // up of elements from the range
    // [L, R] having distinct sum
    static void countPairs(long L, long R)
    {

        // Stores the least sum which
        // can be formed by the pairs
        long firstNum = 2 * L;

        // Stores the highest sum which
        // can be formed by the pairs
        long lastNum = 2 * R;

        // Stores the count of pairs
        // having distinct sum
        long Cntpairs = lastNum - firstNum + 1;

        // Print the count of pairs
        System.out.println(Cntpairs);
    }

    // Driver Code
    public static void main(String[] args)
    {
        long L = 2, R = 3;

        // Function call to count
        // the number of pairs
        // having distinct sum in
        // the range [L, R]
        countPairs(L, R);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to count pairs made
# up of elements from the range
# [L, R] having distinct sum
def countPairs(L, R):

    # Stores the least sum which
    # can be formed by the pairs
    firstNum = 2 * L

    # Stores the highest sum which
    # can be formed by the pairs
    lastNum = 2 * R

    # Stores the count of pairs
    # having distinct sum
    Cntpairs = lastNum - firstNum + 1

    # Print the count of pairs
    print (Cntpairs)

# Driver Code
if __name__ == '__main__':
    L,R = 2,3

    # Function call to count
    # the number of pairs
    # having distinct sum in
    # the range [L, R]
    countPairs(L, R)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for
// the above approach

using System;

public class GFG {

    // Function to count pairs made
    // up of elements from the range
    // [L, R] having distinct sum
    static void countPairs(long L, long R)
    {

        // Stores the least sum which
        // can be formed by the pairs
        long firstNum = 2 * L;

        // Stores the highest sum which
        // can be formed by the pairs
        long lastNum = 2 * R;

        // Stores the count of pairs
        // having distinct sum
        long Cntpairs = lastNum - firstNum + 1;

        Console.WriteLine(Cntpairs);
    }

    // Driver Code
    static public void Main()
    {
        long L = 2, R = 3;

        // Function call to count
        // the number of pairs
        // having distinct sum in
        // the range [L, R]
        countPairs(L, R);
    }
}
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to count pairs made
// up of elements from the range
// [L, R] having distinct sum

function countPairs(L,R)
{
    // Stores the least sum which
        // can be formed by the pairs
        let firstNum = 2 * L;

        // Stores the highest sum which
        // can be formed by the pairs
        let lastNum = 2 * R;

        // Stores the count of pairs
        // having distinct sum
        let Cntpairs = lastNum - firstNum + 1;

        // Print the count of pairs
        document.write(Cntpairs+"<br>");
}

// Driver Code
let L = 2, R = 3;

// Function call to count
// the number of pairs
// having distinct sum in
// the range [L, R]
countPairs(L, R);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)