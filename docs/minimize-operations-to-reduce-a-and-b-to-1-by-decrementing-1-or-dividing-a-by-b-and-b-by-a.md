# 通过减 1 或将 A 除以 B and B 再除以 A

来最小化将 A 和 B 减 1 的操作

> 原文:[https://www . geesforgeks . org/minimum-operations-to-reduction-a-b-1-1-减 1 或-a-b-b-除-a/](https://www.geeksforgeeks.org/minimize-operations-to-reduce-a-and-b-to-1-by-decrementing-1-or-dividing-a-by-b-and-b-by-a/)

给定两个正整数 **A** 和 **B** 。任务是尽量减少将 **A** 和 **B** 减少到 **1** 所需的操作。有两种类型的操作:

1.  将 **A** 或 **B** 减少 **1** 。
2.  将 **A** 除以 **B** 或 **B** 除以 **A** 或仅当除法的余数为 **0** 时同时执行两次除法。

**示例:**

> **输入:** A = 13，B = 5
> **输出:** 6
> **说明:**下面是将 A 和 B 减 1 的操作。
> 
> 最初 A = 13，B = 5
> 第一步:减量 A 1:A = 12，B = 5
> 第二步:减量 B 1:A = 12，B = 4
> 第三步:A 除以 B 并赋给 A : A = 3，B = 4
> 第四步:减量 A 1:A = 2，B = 4
> 第五步:B 除以 A 并赋给 B : A = 2， B = 2
> 第 6 步:将 A 除以 B and B 再除以 A，分别分配给 A 和 B:A = 1，B = 1
> 因此，将 A 和 B 减少到 1 总共需要 6 步。 这是最小的可能。
> 
> **输入:** A = 3，B = 27
> T3】输出: 3

**方法:**这个问题可以用[递归](https://www.geeksforgeeks.org/recursion/)解决。创建一个递归，取一个变量 **cntOperations = 0** 来记录执行的操作数量。对于基础条件，检查 **A=1** 和 **B=1** ，然后返回 **cntOperations** 否则，检查每个可以执行的操作。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to find minimum operation
// required to reduce A and B to 1
int solve(int A, int B, int ans = 0)
{
    // Base Condition: When A and B reduced to 1
    if (A == 1 && B == 1) {
        return ans;
    }

    // If A and B are equal
    if (A % B == 0 && B % A == 0) {
        return solve(A / B, B / A, ans + 1);
    }

    // If A is divisible by B
    else if (A % B == 0 && B % A != 0) {
        return solve(A / B, B, ans + 1);
    }

    // If B is divisible by A
    else if (A % B != 0 && B % A == 0) {
        return solve(A, B / A, ans + 1);
    }

    // If A-1 is even
    else if ((A - 1) % 2 == 0) {
        return solve(A - 1, B, ans + 1);
    }

    // If B-1 is even
    else if ((B - 1) % 2 == 0) {
        return solve(A, B - 1, ans + 1);
    }

    else {

        // If A is less than B
        if (A < B) {
            return solve(A - 1, B, ans + 1);
        }

        // If B is less than A
        else {
            return solve(A, B - 1, ans + 1);
        }
    }
}

// Driver Code
int main()
{
    int A = 13;
    int B = 5;

    cout << solve(A, B);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG
{

    // Recursive function to find minimum operation
    // required to reduce A and B to 1
    public static int solve(int A, int B, int ans)
    {

        // Base Condition: When A and B reduced to 1
        if (A == 1 && B == 1) {
            return ans;
        }

        // If A and B are equal
        if (A % B == 0 && B % A == 0) {
            return solve(A / B, B / A, ans + 1);
        }

        // If A is divisible by B
        else if (A % B == 0 && B % A != 0) {
            return solve(A / B, B, ans + 1);
        }

        // If B is divisible by A
        else if (A % B != 0 && B % A == 0) {
            return solve(A, B / A, ans + 1);
        }

        // If A-1 is even
        else if ((A - 1) % 2 == 0) {
            return solve(A - 1, B, ans + 1);
        }

        // If B-1 is even
        else if ((B - 1) % 2 == 0) {
            return solve(A, B - 1, ans + 1);
        }

        else {

            // If A is less than B
            if (A < B) {
                return solve(A - 1, B, ans + 1);
            }

            // If B is less than A
            else {
                return solve(A, B - 1, ans + 1);
            }
        }
    }

    // Driver Code
    public static void main(String args[]) {
        int A = 13;
        int B = 5;

        System.out.println(solve(A, B, 0));
    }
}

// This code is contributed by gfgking,
```

## 蟒蛇 3

```
# python program for above approach

# Recursive function to find minimum operation
# required to reduce A and B to 1
def solve(A, B, ans=0):

    # Base Condition: When A and B reduced to 1
    if (A == 1 and B == 1):
        return ans

    # If A and B are equal
    if (A % B == 0 and B % A == 0):
        return solve(A // B, B // A, ans + 1)

    # If A is divisible by B
    elif (A % B == 0 and B % A != 0):
        return solve(A // B, B, ans + 1)

    # If B is divisible by A
    elif (A % B != 0 and B % A == 0):
        return solve(A, B // A, ans + 1)

    # If A-1 is even
    elif ((A - 1) % 2 == 0):
        return solve(A - 1, B, ans + 1)

    # If B-1 is even
    elif ((B - 1) % 2 == 0):
        return solve(A, B - 1, ans + 1)

    else:

        # If A is less than B
        if (A < B):
            return solve(A - 1, B, ans + 1)

        # If B is less than A
        else:
            return solve(A, B - 1, ans + 1)

# Driver Code
if __name__ == "__main__":

    A = 13
    B = 5

    print(solve(A, B))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Recursive function to find minimum operation
    // required to reduce A and B to 1
    static int solve(int A, int B, int ans)
    {

        // Base Condition: When A and B reduced to 1
        if (A == 1 && B == 1) {
            return ans;
        }

        // If A and B are equal
        if (A % B == 0 && B % A == 0) {
            return solve(A / B, B / A, ans + 1);
        }

        // If A is divisible by B
        else if (A % B == 0 && B % A != 0) {
            return solve(A / B, B, ans + 1);
        }

        // If B is divisible by A
        else if (A % B != 0 && B % A == 0) {
            return solve(A, B / A, ans + 1);
        }

        // If A-1 is even
        else if ((A - 1) % 2 == 0) {
            return solve(A - 1, B, ans + 1);
        }

        // If B-1 is even
        else if ((B - 1) % 2 == 0) {
            return solve(A, B - 1, ans + 1);
        }

        else {

            // If A is less than B
            if (A < B) {
                return solve(A - 1, B, ans + 1);
            }

            // If B is less than A
            else {
                return solve(A, B - 1, ans + 1);
            }
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int A = 13;
        int B = 5;
        Console.WriteLine(solve(A, B, 0));
    }
}

// This code is contributed by dwivediyash
```

## java 描述语言

```
<script>
    // JavaScript program for above approach

    // Recursive function to find minimum operation
    // required to reduce A and B to 1
    const solve = (A, B, ans = 0) => {
        // Base Condition: When A and B reduced to 1
        if (A == 1 && B == 1) {
            return ans;
        }

        // If A and B are equal
        if (A % B == 0 && B % A == 0) {
            return solve(parseInt(A / B), parseInt(B / A), ans + 1);
        }

        // If A is divisible by B
        else if (A % B == 0 && B % A != 0) {
            return solve(parseInt(A / B), B, ans + 1);
        }

        // If B is divisible by A
        else if (A % B != 0 && B % A == 0) {
            return solve(A, parseInt(B / A), ans + 1);
        }

        // If A-1 is even
        else if ((A - 1) % 2 == 0) {
            return solve(A - 1, B, ans + 1);
        }

        // If B-1 is even
        else if ((B - 1) % 2 == 0) {
            return solve(A, B - 1, ans + 1);
        }

        else {

            // If A is less than B
            if (A < B) {
                return solve(A - 1, B, ans + 1);
            }

            // If B is less than A
            else {
                return solve(A, B - 1, ans + 1);
            }
        }
    }

    // Driver Code
    let A = 13;
    let B = 5;

    document.write(solve(A, B));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
6
```

**时间复杂度:** O(最大值(A，B))

**辅助空间:** O(1)