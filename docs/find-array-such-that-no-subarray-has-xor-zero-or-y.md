# 查找数组，使得没有子数组具有异或 0 或 Y

> 原文:[https://www . geesforgeks . org/find-array-so-no-subarray-has-xor-zero-or-y/](https://www.geeksforgeeks.org/find-array-such-that-no-subarray-has-xor-zero-or-y/)

给定两个整数 **X** (1 ≤ X ≤ 15)和 **Y** 。任务是找到最大可能长度的数组 **N** ，使得数组中的所有元素位于 **1** 和 **2 <sup>X</sup>** 之间，并且不存在子数组，使得子数组的 xor 值为 **0** 或 **Y** 。如果存在多个答案，则打印其中任何一个。如果不存在这样的数组，则打印 **-1**
**示例:**

> **输入:** X = 3，Y = 5
> **输出:**1 3 1
> (1 ^ 3)= 2
> (3 ^ 1)= 2
> (1 ^ 3 ^ 1)= 3
> **输入:** X = 1，Y = 1
> **输出:** -1

**方法:**主要思想是构建所需数组的前缀 xor，然后从中构建数组。让前缀异或数组成为 **pre[]** 。
现在，前缀数组中任意两对的 XOR 表示 **(pre[l] ^ pre[r])** 将表示原始数组的某个子数组的 XOR，即**arr[l+1]^ arr[l+2]^…^ arr[r]**。
因此，现在问题简化为从 **pre[]** 数组的元素构造数组，使得没有一对元素具有等于 **0** 或 **Y** 的按位异或，并且其长度应该最大。
注意**没有一对数字的按位异或和等于 0** 只是表示**不能两次使用同一个数字**。
如果 **Y ≥ 2 <sup>X</sup>** 那么没有一对小于 **2 <sup>X</sup>** 的数字会有一个等于 **Y** 的按位异或，所以你可以任意顺序使用从 **1** 到**2<sup>X</sup>–1**的所有数字。否则，您可以想到形成对的数字，其中每对由 **2** 个数字组成，按位异或和等于 **Y** 。从任何一对中，如果将一个数字添加到数组中，就不能再添加另一个。然而，这两对是相互独立的:你在一对中的选择不会影响任何其他对。因此，你可以在任意一对中选择任意一个数字，然后按照你想要的顺序添加它们。构造数组 **pre[]** 后，可以使用:**arr[I]= pre[I]^ pre[I–1]构造原始数组。**
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length array
void maxLengthArr(int x, int y)
{
    // To store if an element is
    // already taken or not
    bool ex[(1 << x)];

    // To store visited numbers
    ex[0] = 1;
    vector<int> pre({ 0 });

    // For all possible values of pre[]
    for (int i = 1; i < (1 << x); i++) {

        // If it is already taken
        if (ex[i ^ y])
            continue;

        pre.push_back(i);
        ex[i] = 1;
    }

    // Not possible
    if (pre.size() == 1) {
        cout << "-1";
        return;
    }

    // Print the array constructing it
    // from the prefix-xor array
    for (int i = 1; i < pre.size(); i++)
        cout << (pre[i] ^ pre[i - 1]) << " ";
}

// Driver code
int main()
{
    int X = 3, Y = 5;

    maxLengthArr(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the maximum length array
static void maxLengthArr(int x, int y)
{
    // To store if an element is
    // already taken or not
    boolean[] ex = new boolean[(1 << x)];

    // To store visited numbers
    ex[0] = true;
    Vector<Integer> pre = new Vector<Integer>();
    pre.add(0);

    // For all possible values of pre[]
    for (int i = 1; i < (1 << x); i++)
    {

        // If it is already taken
        if (ex[i ^ y])
            continue;

        pre.add(i);
        ex[i] = true;
    }

    // Not possible
    if (pre.size() == 1)
    {
        System.out.print("-1");
        return;
    }

    // Print the array constructing it
    // from the prefix-xor array
    for (int i = 1; i < pre.size(); i++)
        System.out.print((pre.get(i) ^
                          pre.get(i - 1)) + " ");
}

// Driver code
public static void main(String[] args)
{
    int X = 3, Y = 5;

    maxLengthArr(X, Y);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the maximum length array
def maxLengthArr(x, y) :

    # To store if an element is
    # already taken or not
    ex = [0] * (1 << x);

    # To store visited numbers
    ex[0] = 1;
    pre = [0];

    # For all possible values of pre[]
    for i in range(1, (1 << x)) :

        # If it is already taken
        if (ex[i ^ y]) :
            continue;

        pre.append(i);
        ex[i] = 1;

    # Not possible
    if (len(pre) == 1) :
        print("-1", end = "");
        return;

    # Print the array constructing it
    # from the prefix-xor array
    for i in range(1, len(pre)) :
        print(pre[i] ^ pre[i - 1], end = " ");

# Driver code
if __name__ == "__main__" :

    X = 3; Y = 5;
    maxLengthArr(X, Y);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the maximum length array
    static void maxLengthArr(int x, int y)
    {
        // To store if an element is
        // already taken or not
        bool[] ex = new bool[(1 << x)];

        // To store visited numbers
        ex[0] = true;
        var pre = new List<int>();
        pre.Add(0);

        // For all possible values of pre[]
        for (int i = 1; i < (1 << x); i++)
        {
            // If it is already taken
            if (ex[i ^ y])
                continue;

            pre.Add(i);
            ex[i] = true;
        }

        // Not possible
        if (pre.Count == 1)
        {
            Console.Write("-1");
            return;
        }

        // Print the array constructing it
        // from the prefix-xor array
        for (int i = 1; i < pre.Count; i++)
            Console.Write((pre[i] ^ pre[i - 1]) + " ");
    }

    // Driver code
    public static void Main(String[] args)
    {
        int X = 3, Y = 5;
        maxLengthArr(X, Y);
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the maximum length array
function maxLengthArr(x, y)
{
    // To store if an element is
    // already taken or not
    let ex = new Array((1 << x)).fill(0);

    // To store visited numbers
    ex[0] = 1;
    let pre = [];
    pre.push(0);

    // For all possible values of pre[]
    for (let i = 1; i < (1 << x); i++) {

        // If it is already taken
        if (ex[i ^ y])
            continue;

        pre.push(i);
        ex[i] = 1;
    }

    // Not possible
    if (pre.length == 1) {
        document.write("-1");
        return;
    }

    // Print the array constructing it
    // from the prefix-xor array
    for (let i = 1; i < pre.length; i++)
        document.write((pre[i] ^ pre[i - 1]) + " ");
}

// Driver code
    let X = 3, Y = 5;

    maxLengthArr(X, Y);

</script>
```

**Output:** 

```
1 3 1
```