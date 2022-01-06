# 给定三个数字的数字组成的最大数字

> 原文:[https://www . geesforgeks . org/给定三位数的最大数字格式/](https://www.geeksforgeeks.org/maximum-number-formed-from-the-digits-of-given-three-numbers/)

给定 **3** 四位整数 **A** 、 **B** 和 **C** ，任务是打印给定数字中相同位置所有数字取最大数字组成的数字。

**示例:**

> **输入:** A = 3521，B = 2452，C = 1352
> T3】输出:3552
> T6】说明:
> 
> 1.  位于第 1<sup>位的位数的最大值等于最大值(A[3] = 1，B[3] = 2，C[3] = 2) 2。</sup>
> 2.  位于第 10<sup>位的数字的最大值等于最大值(A[2] = 2，B[2] = 5，C[2] = 5) 5。</sup>
> 3.  第 100<sup>位的最大位数等于最大值(A[1] = 5，B[1] = 4，C[1] = 3) 5。</sup>
> 4.  第 1000<sup>位的最大位数等于最大值(A[0] = 3，B[0] = 3，C[0] = 1) 3。</sup>
> 
> 因此，形成的数字是 3552。
> 
> **输入:** A = 11，B = 12，C = 22
> T3】输出: 22

**方法:**这个问题可以通过[迭代给定整数的数字](https://www.geeksforgeeks.org/c-program-to-print-all-digits-of-a-given-number/)来解决。按照以下步骤解决问题:

*   初始化一个变量，说 **ans** 为 **0** 和 **P** 为 **1** 来存储可能的最大数字和一个数字的位置值。
*   迭代至 **A、B** 和 **C** 大于 **0** 并执行以下步骤:
    *   找出数字 **A、B** 和 **C** 的单位位数字，分别存储在变量中，如 **a、b** 和 **c** 。
    *   将 **A** 更新为 **A/10** 、 **B** 更新为 **B/10** 、 **C** 更新为 **C/10** 。
    *   按 **P*max(a，b，c)** 递增**和**，然后将 **P** 更新为 **P*10。**
*   最后，完成以上步骤后，打印 **ans** 中存储的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// formed by taking the maximum digit
// at the same position from each number
int findkey(int A, int B, int C)
{
    // Stores the result
    int ans = 0;

    // Stores the position value of a
    // digit
    int cur = 1;

    while (A > 0) {

        // Stores the digit at the unit
        // place
        int a = A % 10;
        // Stores the digit at the unit
        // place
        int b = B % 10;
        // Stores the digit at the unit
        // place
        int c = C % 10;

        // Update A, B and C
        A = A / 10;
        B = B / 10;
        C = C / 10;

        // Stores the maximum digit
        int m = max(a, max(c, b));

        // Increment ans cur*a
        ans += cur * m;

        // Update cur
        cur = cur * 10;
    }
    // Return ans
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int A = 3521, B = 2452, C = 1352;

    // Function call
    cout << findkey(A, B, C);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

// Function to find the maximum number
// formed by taking the maximum digit
// at the same position from each number
static int findkey(int A, int B, int C)
{

    // Stores the result
    int ans = 0;

    // Stores the position value of a
    // digit
    int cur = 1;

    while (A > 0) {

        // Stores the digit at the unit
        // place
        int a = A % 10;

        // Stores the digit at the unit
        // place
        int b = B % 10;

        // Stores the digit at the unit
        // place
        int c = C % 10;

        // Update A, B and C
        A = A / 10;
        B = B / 10;
        C = C / 10;

        // Stores the maximum digit
        int m = Math.max(a, Math.max(c, b));

        // Increment ans cur*a
        ans += cur * m;

        // Update cur
        cur = cur * 10;
    }
    // Return ans
    return ans;
}

// Driver Code
public static void main(String args[])
{
    // Given Input
    int A = 3521, B = 2452, C = 1352;

    // Function call
    System.out.println(findkey(A, B, C));
    }
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Py program for the above approach

# Function to find the maximum number
# formed by taking the maximum digit
# at the same position from each number
def findkey(A, B, C):
    # Stores the result
    ans = 0

    # Stores the position value of a
    # digit
    cur = 1

    while (A > 0):

        # Stores the digit at the unit
        # place
        a = A % 10
        # Stores the digit at the unit
        # place
        b = B % 10
        # Stores the digit at the unit
        # place
        c = C % 10

        # Update A, B and C
        A = A // 10
        B = B // 10
        C = C // 10

        # Stores the maximum digit
        m = max(a, max(c, b))

        # Increment ans cur*a
        ans += cur * m

        # Update cur
        cur = cur * 10

    # Return ans
    return ans

# Driver Code
if __name__ == '__main__':
    # Given Input
    A = 3521
    B = 2452
    C = 1352

    # Function call
    print (findkey(A, B, C))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum number
// formed by taking the maximum digit
// at the same position from each number
static int findkey(int A, int B, int C)
{

    // Stores the result
    int ans = 0;

    // Stores the position value of a
    // digit
    int cur = 1;

    while (A > 0) {

        // Stores the digit at the unit
        // place
        int a = A % 10;

        // Stores the digit at the unit
        // place
        int b = B % 10;

        // Stores the digit at the unit
        // place
        int c = C % 10;

        // Update A, B and C
        A = A / 10;
        B = B / 10;
        C = C / 10;

        // Stores the maximum digit
        int m = Math.Max(a, Math.Max(c, b));

        // Increment ans cur*a
        ans += cur * m;

        // Update cur
        cur = cur * 10;
    }
    // Return ans
    return ans;
}

// Driver Code
static public void Main ()
{

    // Given Input
    int A = 3521, B = 2452, C = 1352;

    // Function call
    Console.Write(findkey(A, B, C));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the maximum number
// formed by taking the maximum digit
// at the same position from each number
function findkey(A,  B, C)
{

    // Stores the result
    let ans = 0;

    // Stores the position value of a
    // digit
    let cur = 1;

    while (A > 0)
    {

        // Stores the digit at the unit
        // place
        let a = A % 10;

        // Stores the digit at the unit
        // place
        let b = B % 10;

        // Stores the digit at the unit
        // place
        let c = C % 10;

        // Update A, B and C
        A = Math.floor(A / 10);
        B = Math.floor(B / 10);
        C = Math.floor(C / 10);

        // Stores the maximum digit
        let m = Math.max(a, Math.max(c, b));

        // Increment ans cur*a
        ans += cur * m;

        // Update cur
        cur = cur * 10;
    }

    // Return ans
    return ans;
}

// Driver Code
// Given Input
    let A = 3521, B = 2452, C = 1352;

    // Function call
     document.write(findkey(A, B, C));

    // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
3552
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*