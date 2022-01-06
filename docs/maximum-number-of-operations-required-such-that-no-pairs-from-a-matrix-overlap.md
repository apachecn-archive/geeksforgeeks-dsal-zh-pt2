# 要求的最大运算次数，使得矩阵中没有对重叠

> 原文:[https://www . geesforgeks . org/最大操作数-要求-这样-矩阵中没有对-重叠/](https://www.geeksforgeeks.org/maximum-number-of-operations-required-such-that-no-pairs-from-a-matrix-overlap/)

给定一个整数 **N** 后跟一个矩阵 **V[][]** ，该矩阵由以 **X** 的升序排列的对 **{X，Y}** 组成，任务是对于以 X 的升序排列的每一对，可以执行以下操作:

*   将配对 **{X，Y}** 转换为**{ X–Y，X}**
*   将配对 **{X，Y}** 转换为 **{X，X+Y}**
*   将配对改为 **{X，X}**

任务是找到所需的加法和减法运算的计数，使得没有两对重叠。

**示例:**

> **输入:** N = 5，V[] = {{1，2} {2，1} {5，10} {10，9} {19，1}}
> **输出:** 3
> **解释:**
> {1，2}:操作 1 将对修改为{-1，1}。
> {2，1}:操作 2 将配对修改为{2，3}。
> {5，10}:操作 3 将该对修改为{5，5}
> {10，9}:操作 3 将该对修改为{10，10}
> {19，1}:操作 2 将该对修改为{19，20}。
> 因此，没有一对重叠。因此，所需的加法和减法运算的计数是 3。
> 
> **输入:** N = 3，V[][] = {{10，20} {15，10} {20，16 } }
> T3】输出: 2

**方法:**
主要思想是观察答案，在任何情况下**都不会超过 N** ，因为三个操作中的任何一个都不能在一对上应用两次。按照以下步骤解决问题:

*   始终为第一对选择**操作 1** ，因为 X 是第一对的最小值。
*   最后一对始终选择**操作 2** ，因为 X 是最后一对的最大值。
*   对于其余对，检查应用**操作 1** 是否违反规则。如果它不违反规则，那么它将总是最大化结果。否则，检查**操作 2** 。如果两个操作中的任何一个适用，增加**计数**。
*   如果两个规则都不适用，请执行操作 3。
*   最后打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum count of operations
int find_max(vector<pair<int, int> > v, int n)
{
    // Initialize count by 0
    int count = 0;

    if (n >= 2)
        count = 2;

    else
        count = 1;

    // Iterate over remaining pairs
    for (int i = 1; i < n - 1; i++) {

        // Check if first operation
        // is applicable
        if (v[i - 1].first
            < (v[i].first - v[i].second))
            count++;

        // Check if 2nd operation is applicable
        else if (v[i + 1].first
                 > (v[i].first + v[i].second)) {
            count++;
            v[i].first = v[i].first + v[i].second;
        }

        // Otherwise
        else
            continue;
    }

    // Return  the count of operations
    return count;
}

// Driver Code
int main()
{
    int n = 3;
    vector<pair<int, int> > v;

    v.push_back({ 10, 20 });
    v.push_back({ 15, 10 });
    v.push_back({ 20, 16 });

    cout << find_max(v, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find maximum count of operations
static int find_max(Vector<pair> v, int n)
{
    // Initialize count by 0
    int count = 0;

    if (n >= 2)
        count = 2;
    else
        count = 1;

    // Iterate over remaining pairs
    for(int i = 1; i < n - 1; i++)
    {

        // Check if first operation
        // is applicable
        if (v.get(i - 1).first <
           (v.get(i).first - v.get(i).second))
            count++;

        // Check if 2nd operation is applicable
        else if (v.get(i + 1).first >
                (v.get(i).first + v.get(i).second))
        {
            count++;
            v.get(i).first = v.get(i).first +
                             v.get(i).second;
        }

        // Otherwise
        else
            continue;
    }

    // Return the count of operations
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3;
    Vector<pair> v = new Vector<>();

    v.add(new pair(10, 20));
    v.add(new pair(15, 10));
    v.add(new pair(20, 16));

    System.out.print(find_max(v, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find maximum count of
# operations
def find_max(v, n):

    # Initialize count by 0
    count = 0

    if(n >= 2):
        count = 2
    else:
        count = 1

    # Iterate over remaining pairs
    for i in range(1, n - 1):

        # Check if first operation
        # is applicable
        if(v[i - 1][0] > (v[i][0] +
                          v[i][1])):
            count += 1

        # Check if 2nd operation is applicable
        elif(v[i + 1][0] > (v[i][0] +
                            v[i][1])):
            count += 1
            v[i][0] = v[i][0] + v[i][1]

        # Otherwise
        else:
            continue

    # Return the count of operations
    return count

# Driver Code
n = 3
v = []

v.append([ 10, 20 ])
v.append([ 15, 10 ])
v.append([ 20, 16 ])

print(find_max(v, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find maximum count of operations
static int find_max(List<pair> v, int n)
{

    // Initialize count by 0
    int count = 0;

    if (n >= 2)
        count = 2;
    else
        count = 1;

    // Iterate over remaining pairs
    for(int i = 1; i < n - 1; i++)
    {

        // Check if first operation
        // is applicable
        if (v[i - 1].first <
           (v[i].first - v[i].second))
            count++;

        // Check if 2nd operation is applicable
        else if (v[i + 1].first >
                (v[i].first + v[i].second))
        {
            count++;
            v[i].first = v[i].first +
                         v[i].second;
        }

        // Otherwise
        else
            continue;
    }

    // Return the count of operations
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 3;
    List<pair> v = new List<pair>();

    v.Add(new pair(10, 20));
    v.Add(new pair(15, 10));
    v.Add(new pair(20, 16));

    Console.Write(find_max(v, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript Program to implement the above approach

    // Function to find maximum count of operations
    function find_max(v, n)
    {
        // Initialize count by 0
        let count = 0;

        if (n >= 2)
            count = 2;

        else
            count = 1;

        // Iterate over remaining pairs
        for (let i = 1; i < n - 1; i++) {

            // Check if first operation
            // is applicable
            if (v[i - 1][0]
                < (v[i][0] - v[i][1]))
                count++;

            // Check if 2nd operation is applicable
            else if (v[i + 1][0]
                     > (v[i][0] + v[i][1])) {
                count++;
                v[i][0] = v[i][0] + v[i][1];
            }

            // Otherwise
            else
                continue;
        }

        // Return  the count of operations
        return count;
    }

    let n = 3;
    let v = [ [10, 20], [15, 10], [20, 16] ];

    document.write(find_max(v, n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*