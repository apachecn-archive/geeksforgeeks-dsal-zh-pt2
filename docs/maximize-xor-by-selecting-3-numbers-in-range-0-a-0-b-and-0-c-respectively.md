# 分别选择[0，A]，[0，B]和[0，C]范围内的 3 个数字

，最大化异或运算

> 原文:[https://www . geesforgeks . org/maximum-xor-by-select-3-numbers-in-range-0-a-0-b-和-0-c-分别/](https://www.geeksforgeeks.org/maximize-xor-by-selecting-3-numbers-in-range-0-a-0-b-and-0-c-respectively/)

给定 3 个整数 **A** 、 **B** 、 **C** ，任务是分别从范围【0，A】、【0，B】、【0，C】中选择一个，求三个数的最大[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值。

**示例:**

> **输入:** A = 1，B = 2，C = 4
> **输出:** 7
> **解释:**最大 XOR 可以通过选择 1(从[0，1]开始)、2(从[0，2]开始)& 4(从[0，4]开始)即 **1⊕ 2⊕ 4 = 7** 来计算
> 
> **输入:** A = 6，B = 2，C = 10
> **输出:** 15
> **说明:**最大异或可以通过选择 5(从[0，6]开始)、1(从[0，2]开始)& 10(从[0，10]开始)即 **5⊕ 1⊕ 10 = 15 来计算。**

**天真方法:**生成上述范围内所有可能的三元组，并计算最大可能异或。

**时间复杂度:O(A*B*C)**

**辅助空间:O(1)**

**有效方法:**

为了找到异或运算的最大值，异或的值应该使每个位都是一个设置位，即在 32 位数字中，目标是从左到右获得最多 1 个设置。这可以通过以下步骤完成:

1.  创建一个变量**和**，它将存储可能的最大异或值，并将其初始化为零。
2.  为了创建一个 32 位的值，这将是最大可能的 xor，运行一个从最高有效位到最低有效位的循环。
3.  现在每一位:
    *   创建一个变量 **cur** ，它将存储设置该位的最小数量。
    *   检查每个范围 A，B，C，并尝试找到一个在该位置有一个设置位的数字。这可以通过将 A，B & C 与 cur 进行比较来实现，即如果来自 A，B & C 的任何数字大于或等于 cur，则它将在该位置包含一个设置位。如果在 A、B、C 中的任何一个数中发现了一个设置位，那么最大异或也将在该位置包含设置位。
    *   现在，如果找到一个设置位，那么将 cur 添加到 ans 中以设置其中的位，并通过 cur 减少找到设置位的数字的值(从 A、B、C)以取消设置该位，因为它不能再次使用。
    *   对每一位做以上步骤，计算出答案的最终值。
4.  完成上述步骤后，打印所需的结果。

**实施:**

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// maximum triplet XOR form 3 ranges
int maximumTripletXOR(int A, int B, int C)
{
    // Initialize a variable
    // to store the answer
    int ans = 0;
    for (int i = 30; i >= 0; i--) {

        // create minimum number
        // that have a set bit
        // at ith position
        int cur = 1 << i;

        // Check for each number
        // and try to greedily choose
        // the bit if possible
        // If A >= cur then A also have a
        // set bit at ith position
        if (A >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from A
            A -= cur;
        }

        // Check for B
        else if (B >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from B
            B -= cur;
        }

        // Check for C
        else if (C >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from C
            C -= cur;
        }

        // If any of the above conditions
        // is not satisfied then
        // there is no way to turn that bit ON.
    }
    return ans;
}

// Driver Code
int main()
{
    int A = 6;
    int B = 2;
    int C = 10;
    cout << maximumTripletXOR(A, B, C);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.util.*;

class GFG{

// Function to calculate
// maximum triplet XOR form 3 ranges
static int maximumTripletXOR(int A, int B, int C)
{

    // Initialize a variable
    // to store the answer
    int ans = 0;
    for (int i = 30; i >= 0; i--) {

        // create minimum number
        // that have a set bit
        // at ith position
        int cur = 1 << i;

        // Check for each number
        // and try to greedily choose
        // the bit if possible
        // If A >= cur then A also have a
        // set bit at ith position
        if (A >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from A
            A -= cur;
        }

        // Check for B
        else if (B >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from B
            B -= cur;
        }

        // Check for C
        else if (C >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from C
            C -= cur;
        }

        // If any of the above conditions
        // is not satisfied then
        // there is no way to turn that bit ON.
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int A = 6;
    int B = 2;
    int C = 10;
    System.out.print(maximumTripletXOR(A, B, C));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to calculate
# maximum triplet XOR form 3 ranges
def maximumTripletXOR(A, B, C):

    # Initialize a variable
    # to store the answer
    ans = 0

    for i in range(30, -1,-1):

        # create minimum number
        # that have a set bit
        # at ith position
        cur = 1 << i

        # Check for each number
        # and try to greedily choose
        # the bit if possible
        # If A >= cur then A also have a
        # set bit at ith position
        if (A >= cur):

            # Increment the answer
            ans += cur

            # Subtract this value from A
            A -= cur
        # Check for B
        elif (B >= cur):

            # Increment the answer
            ans += cur

            # Subtract this value from B
            B -= cur

        # Check for C
        elif (C >= cur):
            # Increment the answer
            ans += cur

            # Subtract this value from C
            C -= cur

        # If any of the above conditions
        # is not satisfied then
        # there is no way to turn that bit ON.

    return ans

# Driver Code

A = 6
B = 2
C = 10
print(maximumTripletXOR(A, B, C))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# Program to implement
// the above approach
using System;

class GFG{

// Function to calculate
// maximum triplet XOR form 3 ranges
static int maximumTripletXOR(int A, int B, int C)
{

    // Initialize a variable
    // to store the answer
    int ans = 0;
    for (int i = 30; i >= 0; i--) {

        // create minimum number
        // that have a set bit
        // at ith position
        int cur = 1 << i;

        // Check for each number
        // and try to greedily choose
        // the bit if possible
        // If A >= cur then A also have a
        // set bit at ith position
        if (A >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from A
            A -= cur;
        }

        // Check for B
        else if (B >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from B
            B -= cur;
        }

        // Check for C
        else if (C >= cur) {

            // Increment the answer
            ans += cur;

            // Subtract this value from C
            C -= cur;
        }

        // If any of the above conditions
        // is not satisfied then
        // there is no way to turn that bit ON.
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int A = 6;
    int B = 2;
    int C = 10;
    Console.Write(maximumTripletXOR(A, B, C));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to calculate maximum
// triplet XOR form 3 ranges
function maximumTripletXOR(A, B, C)
{

    // Initialize a variable
    // to store the answer
    let ans = 0;
    for(let i = 30; i >= 0; i--)
    {

        // Create minimum number
        // that have a set bit
        // at ith position
        let cur = 1 << i;

        // Check for each number
        // and try to greedily choose
        // the bit if possible
        // If A >= cur then A also have a
        // set bit at ith position
        if (A >= cur)
        {

            // Increment the answer
            ans += cur;

            // Subtract this value from A
            A -= cur;
        }

        // Check for B
        else if (B >= cur)
        {

            // Increment the answer
            ans += cur;

            // Subtract this value from B
            B -= cur;
        }

        // Check for C
        else if (C >= cur)
        {

            // Increment the answer
            ans += cur;

            // Subtract this value from C
            C -= cur;
        }

        // If any of the above conditions
        // is not satisfied then
        // there is no way to turn that bit ON.
    }
    return ans;
}

// Driver Code
let A = 6;
let B = 2;
let C = 10;

document.write(maximumTripletXOR(A, B, C));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
15
```

**时间复杂度:** O(1)

**辅助空间:** O(1)