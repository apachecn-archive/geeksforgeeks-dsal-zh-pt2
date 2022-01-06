# 用倒数计算三位数相差 X 的数字

> 原文:[https://www . geesforgeks . org/count-三位数-numbers-difference-x-with-its-reverse/](https://www.geeksforgeeks.org/count-three-digit-numbers-having-difference-x-with-its-reverse/)

给定一个整数 **X** ，任务是用其[反转](https://www.geeksforgeeks.org/write-a-program-to-reverse-digits-of-a-number/)来计算有差异的三位数总数 **X** 。如果不存在这样的号码，则打印-1。

**示例:**

> **输入:** X = 792
> **输出:** 10
> **解释:**
> 901–109 = 792
> 911–119 = 792
> 921–129 = 792
> 931–139 = 792
> 941–149 = 792
> 951–159 = 792【T11
> 
> **输入:**X = 0
> T3】输出: 90

**方法:**给定的问题可以基于以下观察来解决:

> 设 N = rpq
> 因此，N = 100r + 10q + p
> 因此，N = 100p + 10q + r 的反方
> 因此，问题化简为求解(100r+10q+p)–(r+10q+100p)= X
> ->99(r–p)= X
> ->r–p = X/99
> 因此，如果给定 **X** 为

根据以上观察，按照以下步骤解决问题:

*   检查 X 是否是 99 的倍数。如果发现不是真的，打印-1，因为不存在解决方案。
*   否则计算 **X / 99** 。使用数字[1，9]生成所有对，并检查每对的差值是否等于 **X / 99** 。
*   如果发现任何一对都是真的，则将计数增加 10，因为中间的数字可以被置换以放置所获得的对的范围[0，9]中的任何值。
*   最后，打印获得的计数值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count three-digit
// numbers having difference x
// with its reverse
int Count_Number(int x)
{
    int ans = 0;

    // if x is not multiple of 99
    if (x % 99 != 0) {

        // No solution exists
        ans = -1;
    }
    else {

        int diff = x / 99;

        // Generate all possible pairs
        // of digits [1, 9]
        for (int i = 1; i < 10; i++) {
            for (int j = 1; j < 10; j++) {

                // If any pair is obtained
                // with difference x / 99
                if ((i - j) == diff) {

                    // Increase count
                    ans += 10;
                }
            }
        }
    }

    // Return the count
    return ans;
}

// Driver Code
int main()
{
    int x = 792;
    cout << Count_Number(x) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to count three-digit
// numbers having difference x
// with its reverse
static int Count_Number(int x)
{
    int ans = 0;

    // If x is not multiple of 99
    if (x % 99 != 0)
    {

        // No solution exists
        ans = -1;
    }
    else
    {
        int diff = x / 99;

        // Generate all possible pairs
        // of digits [1, 9]
        for(int i = 1; i < 10; i++)
        {
            for(int j = 1; j < 10; j++)
            {

                // If any pair is obtained
                // with difference x / 99
                if ((i - j) == diff)
                {

                    // Increase count
                    ans += 10;
                }
            }
        }
    }

    // Return the count
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    int x = 792;

    System.out.println(Count_Number(x));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count three-digit
# numbers having difference x
# with its reverse
def Count_Number(x):

    ans = 0;

    # If x is not multiple
    # of 99
    if (x % 99 != 0):

        # No solution exists
        ans = -1;
    else:
        diff = x / 99;

        # Generate all possible pairs
        # of digits [1, 9]
        for i in range(1, 10):
            for j in range(1, 10):

                # If any pair is obtained
                # with difference x / 99
                if ((i - j) == diff):
                    # Increase count
                    ans += 10;

    # Return the count
    return ans;

# Driver Code
if __name__ == '__main__':

    x = 792;
    print(Count_Number(x));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to count three-digit
// numbers having difference x
// with its reverse
static int Count_Number(int x)
{
    int ans = 0;

    // If x is not multiple of 99
    if (x % 99 != 0)
    {

        // No solution exists
        ans = -1;
    }
    else
    {
        int diff = x / 99;

        // Generate all possible pairs
        // of digits [1, 9]
        for(int i = 1; i < 10; i++)
        {
            for(int j = 1; j < 10; j++)
            {

                // If any pair is obtained
                // with difference x / 99
                if ((i - j) == diff)
                {

                    // Increase count
                    ans += 10;
                }
            }
        }
    }

    // Return the count
    return ans;
}

// Driver Code
public static void Main()
{
    int x = 792;

    Console.WriteLine(Count_Number(x));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count three-digit
// numbers having difference x
// with its reverse
function Count_Number(x)
{
    let ans = 0;

    // If x is not multiple of 99
    if (x % 99 != 0)
    {

        // No solution exists
        ans = -1;
    }
    else
    {
        let diff = x / 99;

        // Generate all possible pairs
        // of digits [1, 9]
        for(let i = 1; i < 10; i++)
        {
            for(let j = 1; j < 10; j++)
            {

                // If any pair is obtained
                // with difference x / 99
                if ((i - j) == diff)
                {

                    // Increase count
                    ans += 10;
                }
            }
        }
    }

    // Return the count
    return ans;
}

// Driver code
let x = 792;

document.write(Count_Number(x));

// This code is contributed by splevel62

</script>
```

**Output**

```
10
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)