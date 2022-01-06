# 计算第二天气温较高的剩余天数

> 原文:[https://www . geeksforgeeks . org/温度较高的第二天剩余天数/](https://www.geeksforgeeks.org/count-of-days-remaining-for-the-next-day-with-higher-temperature/)

给定一个每日温度的列表。对于每一天来说，任务是计算温度升高的第二天剩余的天数。如果没有可能变暖的天气，那么打印 **-1** 。
**例:**

> **输入:** arr[] = {73，74，75，71，69，72，76，73}
> **输出:** {1，1，4，2，1，1，-1，-1}
> **解释:**
> 对于 73 温度，下一个较暖温度是 74，其在距离 1 处
> 对于 74 温度，下一个较暖温度是 75，其在距离 1 处
> 对于 75 温度，下一个较暖温度是 74 距离 2
> 的下一个较暖温度为 72 对于 69°温度，距离 1
> 的下一个较暖温度为 72°对于 72°温度，距离 1
> 的下一个较暖温度为 76°对于 76°温度，没有有效的下一个较暖日
> 对于 73°温度，没有有效的下一个较暖日
> **输入:** arr[] = {75，74，73，72}
> **输出:** {-

**天真方法:**想法是迭代数组的每一个可能的对，并检查每个当前元素的下一个更大的温度。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效处理方式:**这个问题基本上要求找出当前指数距离下一个更大的[温度的指数到当前指数的温度有多远。解决这个问题的最佳方法是使用](https://www.geeksforgeeks.org/next-greater-element/)[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)。以下是步骤:

1.  使用当前索引迭代给定数组 **arr[]** 的每日温度。
2.  如果堆栈为空，则将当前索引推入堆栈。
3.  如果堆栈不为空，请执行以下操作:
    *   如果当前索引的温度低于堆栈顶部索引的温度，则推送当前索引。
    *   如果当前索引的温度高于堆栈顶部索引的温度，则将等待温度升高的天数更新为:

> 当前索引–堆栈顶部的索引

*   在输出列表中更新天数后，弹出堆栈。

1.  对堆中低于当前温度的所有指数重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to determine how many days
// required to wait for the next
// warmer temperature
void dailyTemperatures(vector<int>& T)
{
    int n = T.size();

    // To store the answer
    vector<int> daysOfWait(n, -1);
    stack<int> s;

    // Traverse all the temperatures
    for (int i = 0; i < n; i++) {

        // Check if current index is the
        // next warmer temperature of
        // any previous indexes
        while (!s.empty()
               && T[s.top()] < T[i]) {

            daysOfWait[s.top()]
                = i - s.top();

            // Pop the element
            s.pop();
        }

        // Push the current index
        s.push(i);
    }

    // Print waiting days
    for (int i = 0; i < n; i++) {
        cout << daysOfWait[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given temperatures
    vector<int> arr{ 73, 74, 75, 71,
                     69, 72, 76, 73 };

    // Function Call
    dailyTemperatures(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to determine how many days
// required to wait for the next
// warmer temperature
static void dailyTemperatures(int[] T)
{
    int n = T.length;

    // To store the answer
    int[] daysOfWait = new int[n];
    Arrays.fill(daysOfWait, -1);

    Stack<Integer> s = new Stack<>();

    // Traverse all the temperatures
    for(int i = 0; i < n; i++)
    {

        // Check if current index is the
        // next warmer temperature of
        // any previous indexes
        while (!s.isEmpty() && T[s.peek()] < T[i])
        {
            daysOfWait[s.peek()] = i - s.peek();

            // Pop the element
            s.pop();
        }

        // Push the current index
        s.push(i);
    }

    // Print waiting days
    for(int i = 0; i < n; i++)
    {
        System.out.print(daysOfWait[i] + " ");
    }
}

// Driver Code
public static void main (String[] args)
{

    // Given temperatures
    int[] arr = { 73, 74, 75, 71,
                  69, 72, 76, 73 };

    // Function call
    dailyTemperatures(arr);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to determine how many days
# required to wait for the next
# warmer temperature
def dailyTemperatures(T):

    n = len(T)

    # To store the answer
    daysOfWait = [-1] * n
    s = []

    # Traverse all the temperatures
    for i in range(n):

        # Check if current index is the
        # next warmer temperature of
        # any previous indexes
        while(len(s) != 0 and
              T[s[-1]] < T[i]):
            daysOfWait[s[-1]] = i - s[-1]

            # Pop the element
            s.pop(-1)

        # Push the current index
        s.append(i)

    # Print waiting days
    for i in range(n):
        print(daysOfWait[i], end = " ")

# Driver Code

# Given temperatures
arr = [ 73, 74, 75, 71,
        69, 72, 76, 73 ]

# Function call
dailyTemperatures(arr)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to determine how many days
// required to wait for the next
// warmer temperature
static void dailyTemperatures(int[] T)
{
    int n = T.Length;

    // To store the answer
    int[] daysOfWait = new int[n];
    for(int i = 0; i < n; i++)
        daysOfWait[i] = -1;

    Stack<int> s = new Stack<int>();

    // Traverse all the temperatures
    for(int i = 0; i < n; i++)
    {

        // Check if current index is the
        // next warmer temperature of
        // any previous indexes
        while (s.Count != 0 && T[s.Peek()] < T[i])
        {
            daysOfWait[s.Peek()] = i - s.Peek();

            // Pop the element
            s.Pop();
        }

        // Push the current index
        s.Push(i);
    }

    // Print waiting days
    for(int i = 0; i < n; i++)
    {
        Console.Write(daysOfWait[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given temperatures
    int[] arr = { 73, 74, 75, 71,
                  69, 72, 76, 73 };

    // Function call
    dailyTemperatures(arr);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to determine how many days
// required to wait for the next
// warmer temperature
function dailyTemperatures(T)
{
    var n = T.length;

    // To store the answer
    var daysOfWait = Array(n).fill(-1);
    var s = [];

    // Traverse all the temperatures
    for (var i = 0; i < n; i++) {

        // Check if current index is the
        // next warmer temperature of
        // any previous indexes
        while (s.length!=0
               && T[s[s.length-1]] < T[i]) {

            daysOfWait[s[s.length-1]]
                = i - s[s.length-1];

            // Pop the element
            s.pop();
        }

        // Push the current index
        s.push(i);
    }

    // Print waiting days
    for (var i = 0; i < n; i++) {
        document.write( daysOfWait[i] + " ");
    }
}

// Driver Code
// Given temperatures
var arr = [73, 74, 75, 71,
                 69, 72, 76, 73 ];
// Function Call
dailyTemperatures(arr);

</script>
```

**Output:** 

```
1 1 4 2 1 1 -1 -1
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*