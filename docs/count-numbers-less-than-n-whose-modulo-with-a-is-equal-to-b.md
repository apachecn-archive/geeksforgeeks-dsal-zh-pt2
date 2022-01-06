# 计数小于 N 的数，其与 A 的模等于 B

> 原文:[https://www . geesforgeks . org/count-numbers-小于 n-其与 a 的模等于 b/](https://www.geeksforgeeks.org/count-numbers-less-than-n-whose-modulo-with-a-is-equal-to-b/)

给定三个非负整数 **A** 、 **B** 和 **N** ，其中 **A** 为*非零*，任务是找出小于或等于 **N** 的整数个数，其与 **A** 的模给出值 **B** 。

**示例:**

> **输入:** A = 6，B = 3，N = 15
> **输出:** 3
> **说明:**数字 3、9、15 小于等于 N (= 15)，它们与 A (= 6)的模等于 B (= 3)。因此，这类数字的计数是 3。
> 
> **输入:** A = 4，B = 1，C = 8
> T3】输出: 2

**方法:**给定的问题可以通过使用基于[数学](https://www.geeksforgeeks.org/mathematical-algorithms/)的观察来解决。按照以下步骤解决问题:

*   如果 **B** 的值至少为**A**，则打印 **0** ，因为不能有任何以 **A** 为模给出值 **B** 的数字。
*   否则，如果 **B** 的值为 **0** ，则打印 **C / A** 的值，作为以 **A** 为模得出值 **B** 的数字的计数。
*   否则，请执行以下步骤:
    *   用 **C / A** 的[底价](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)初始化一个变量，比如 ans。
    *   如果 **(ans * A + B)** 的值小于或等于 **N** ，则将 **ans** 的值增加 **1** 。
    *   完成上述步骤后，打印**和**的值，作为以 **A** 为模得出数值 **B** 的数字的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count numbers less than
// N, whose modulo with A gives B
void countValues(int A, int B, int C)
{
    // If the value of B at least A
    if (B >= A) {
        cout << 0;
        return;
    }

    // If the value of B is 0 or not
    if (B == 0) {
        cout << C / A;
        return;
    }

    // Stores the resultant count
    // of numbers less than N
    int ans = C / A;

    if (ans * A + B <= C) {

        // Update the value of ans
        ans++;
    }

    // Print the value of ans
    cout << ans;
}

// Driver Code
int main()
{
    int A = 6, B = 3, N = 15;
    countValues(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class MyClass
{

// Function to count numbers less than
// N, whose modulo with A gives B
static void countValues(int A, int B, int C)
{

    // If the value of B at least A
    if (B >= A) {
        System.out.println(0);
        return;
    }

    // If the value of B is 0 or not
    if (B == 0) {
        System.out.println(C / A);
        return;
    }

    // Stores the resultant count
    // of numbers less than N
    int ans = C / A;

    if (ans * A + B <= C) {

        // Update the value of ans
        ans++;
    }

    // Print the value of ans
    System.out.println(ans);
}

// Driver Code
public static void main(String args[])
{
    int A = 6, B = 3, N = 15;
    countValues(A, B, N);

}  
}

// This code in contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count numbers less than
# N, whose modulo with A gives B
def countValues(A, B, C):

    # If the value of B at least A
    if (B >= A):
        print(0)
        return

    # If the value of B is 0 or not
    if (B == 0):
        print(C // A)
        return

    # Stores the resultant count
    # of numbers less than N
    ans = C//A

    if (ans * A + B <= C):

        # Update the value of ans
        ans += 1

    # Print the value of ans
    print(ans)

# Driver Code
if __name__ == '__main__':

    A = 6
    B = 3
    N = 15

    countValues(A, B, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count numbers less than
// N, whose modulo with A gives B
static void countValues(int A, int B, int C)
{

    // If the value of B at least A
    if (B >= A)
    {
        Console.Write(0);
        return;
    }

    // If the value of B is 0 or not
    if (B == 0)
    {
        Console.Write(C / A);
        return;
    }

    // Stores the resultant count
    // of numbers less than N
    int ans = C / A;

    if (ans * A + B <= C)
    {

        // Update the value of ans
        ans++;
    }

    // Print the value of ans
    Console.Write(ans);
}

// Driver code
public static void Main()
{
    int A = 6, B = 3, N = 15;
    countValues(A, B, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count numbers less than
// N, whose modulo with A gives B
function countValues(A, B, C)
{
    // If the value of B at least A
    if (B >= A) {
        document.write(0);
        return;
    }

    // If the value of B is 0 or not
    if (B == 0) {
        document.write(parseInt(C / A));
        return;
    }

    // Stores the resultant count
    // of numbers less than N
    let ans = parseInt(C / A);

    if (ans * A + B <= C) {

        // Update the value of ans
        ans++;
    }

    // Print the value of ans
    document.write(ans);
}

// Driver Code
    let A = 6, B = 3, N = 15;
    countValues(A, B, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)