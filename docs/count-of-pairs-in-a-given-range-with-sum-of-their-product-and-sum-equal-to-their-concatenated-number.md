# 给定范围内的配对计数，其乘积和之和等于它们的连接数

> 原文:[https://www . geesforgeks . org/给定范围内的配对计数加上它们的乘积和总和等于它们的串联数/](https://www.geeksforgeeks.org/count-of-pairs-in-a-given-range-with-sum-of-their-product-and-sum-equal-to-their-concatenated-number/)

给定两个数字 **A** 和 **B** ，任务是找出范围**【A，B】**内的对 **(X，Y)** 的个数，使得 **(X * Y) + (X + Y)** 等于 **X** 和 **Y**
**的串联形成的数:**

> **输入:** A = 1，B = 9
> **输出:** 9
> **说明:**
> 对(1，9)、(2，9)、(3，9)、(4，9)、(5，9)、(6，9)、(7，9)、(8，9)和(9，9)是必需的对。
> **输入:** A = 4，B = 10
> **输出:** 7
> **说明:**对(4，9)、(5，9)、(6，9)、(7，9)、(8，9)、(9，9)和(10，9)满足要求条件。

**方法:**
我们可以观察到任何数量的形式【9，99，999，9999，…。]用所有其他值满足条件。

> **说明:**
> 如果 Y = 9，则 x 的所有值都满足所需条件。
> {1*9 + (1 + 9) = 19，2*9 + (2 + 9) = 29，…..11*9 + (11 + 9) = 119 …..
> 同样，对于 Y = 99，1*99 + 1 + 99 = 199，2*99 + 2 + 99 = 299，…

因此，请按照以下步骤解决问题:

1.  计算形式{9，99，999，9999，…}的 Y 的可能值的数量。}在范围【A、B】内，储存在**郡**
2.  将范围[A，B]中的 X 的可能值数计为 **countX**

```
countX = (B - A + 1)
```

2.  所需计数将是 X 和 Y 的可能计数的乘积，即

```
answer = countX * countY
```

以下是上述方法的实现:

## C++

```
// C++ program to count
// all the possible pairs
// with X*Y + (X + Y) equal to
// number formed by
// concatenating X and Y

#include <bits/stdc++.h>
using namespace std;

// Function for counting pairs
int countPairs(int A, int B)
{

    int countY = 0,
        countX = (B - A) + 1,
        next_val = 9;

    // Count possible values
    // of Y
    while (next_val <= B) {
        if (next_val >= A) {
            countY += 1;
        }
        next_val = next_val * 10 + 9;
    }

    return (countX * countY);
}

// Driver Code
int main()
{
    int A = 1;
    int B = 16;
    cout << countPairs(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// all the possible pairs
// with X*Y + (X + Y) equal to
// number formed by
// concatenating X and Y
import java.util.*;
class GFG{

// Function for counting pairs
static int countPairs(int A, int B)
{
    int countY = 0,
        countX = (B - A) + 1,
        next_val = 9;

    // Count possible values
    // of Y
    while (next_val <= B)
    {
        if (next_val >= A)
        {
            countY += 1;
        }
        next_val = next_val * 10 + 9;
    }
    return (countX * countY);
}

// Driver Code
public static void main(String args[])
{
    int A = 1;
    int B = 16;
    System.out.print(countPairs(A, B));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 program to count
# all the possible pairs
# with X*Y + (X + Y) equal to
# number formed by
# concatenating X and Y

# Function for counting pairs
def countPairs(A, B):

    countY = 0
    countX = (B - A) + 1
    next_val = 9

    # Count possible values
    # of Y
    while (next_val <= B):
        if (next_val >= A):
            countY += 1
        next_val = next_val * 10 + 9

    return (countX * countY)

# Driver Code
if __name__ == '__main__':

    A = 1
    B = 16

    print(countPairs(A, B))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count
// all the possible pairs
// with X*Y + (X + Y) equal to
// number formed by
// concatenating X and Y
using System;
class GFG{

// Function for counting pairs
static int countPairs(int A, int B)
{
    int countY = 0,
        countX = (B - A) + 1,
        next_val = 9;

    // Count possible values
    // of Y
    while (next_val <= B)
    {
        if (next_val >= A)
        {
            countY += 1;
        }
        next_val = next_val * 10 + 9;
    }
    return (countX * countY);
}

// Driver Code
public static void Main()
{
    int A = 1;
    int B = 16;
    Console.Write(countPairs(A, B));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>
// javascript program to count
// all the possible pairs
// with X*Y + (X + Y) equal to
// number formed by
// concatenating X and Y

    // Function for counting pairs
    function countPairs(A , B)
    {
        var countY = 0, countX = (B - A) + 1, next_val = 9;

        // Count possible values
        // of Y
        while (next_val <= B)
        {
            if (next_val >= A)
            {
                countY += 1;
            }
            next_val = next_val * 10 + 9;
        }
        return (countX * countY);
    }

    // Driver Code
        var A = 1;
        var B = 16;
        document.write(countPairs(A, B));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
16
```

***时间复杂度:**O(log<sub>10</sub>(B))*
***空间复杂度:** O(1)*