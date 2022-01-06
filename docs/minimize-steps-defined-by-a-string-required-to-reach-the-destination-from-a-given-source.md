# 最小化从给定源到达目的地所需的字符串所定义的步骤

> 原文:[https://www . geeksforgeeks . org/最小化步骤-由字符串定义-需要从给定的源到达目的地/](https://www.geeksforgeeks.org/minimize-steps-defined-by-a-string-required-to-reach-the-destination-from-a-given-source/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**和四个整数**X<sub>1</sub>T7】、**Y<sub>1</sub>T11】、**X<sub>2</sub>T15】和**Y<sub>2</sub>T19】，其中 **(X <sub>1</sub> ，Y <sub>1</sub> )** 表示源坐标和**给定一个字符串 **str** ，任务是找到从源到达目的地所需的以下四种类型的最小步数:**********

*   **If str[i] = 'E':** 将 **(X <sub>1</sub> 、Y <sub>1</sub> )** 转换为 **(X <sub>1</sub> + 1、Y <sub>1</sub> )。**
*   **If str[i] = 'W':** 将 **(X <sub>1</sub> 、Y <sub>1</sub> )** 转换为**(X<sub>1</sub>–1、Y <sub>1</sub> )。**
*   **If str[i] = 'N':** 将 **(X <sub>1</sub> 、Y <sub>1</sub> )** 转换为 **(X <sub>1</sub> 、Y <sub>1</sub> + 1)。**
*   **If str[i] = 'S':** 将 **(X <sub>1</sub> 、Ysub > 1)** 转换为 **(X <sub>1</sub> 、Y<sub>1</sub>–1)。**

如果无法到达目的地，打印 **-1** 。
**注意:**不必总是使用**str【I】**，可以跳过。但是跳过的字符会增加使用的步骤。

**示例**

> **输入:** str = "SESNW "，x1 = 0，y1 = 0，x2 = 1，y2 = 1
> **输出:** 4
> **说明:**
> 要从 **(0，0)** 移动到 **(1，1)** ，需要一个**“E”**和一个**“N”**。
> 因此，子串“SESN”定义的路径确保到达目的地{(0，0) - >跳过 S - > E(1，0) - >跳过 S - > (1，1)}。
> 因此，遍历的字符串最小长度为 4。
> 
> **输入:**str = " Nnnnnnn "，x1 = 1，y1 = 1，x2 = 1，y2 = 2
> **输出:** 1
> **解释:**
> 从当前位置(1，1)开始，它可以使用第一个 **'N'** 方向移动到坐标(1，2)。
> 因此，字符串遍历的最小长度为 1。

**方法:**想法是遍历字符串并执行移动，直到到达目的地。以下是步骤:

1.  初始化四个变量 **pos1、pos2、pos3** 和 **pos4** 分别存储 **E、W、N、S** 的位置。
2.  现在，检查 **(x1，y1)** 是否等于 **(x2，y2)** ，那么当前位置已经是目的地，所以打印 **0** 。
3.  否则，[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并检查以下四个条件:
    *   如果 **x2 > x1** 然后迭代，直到一个**‘E’**出现，并在 **pos1** 中更新该索引。
    *   如果 **x2 < x1** 然后迭代，直到一个**‘W’**出现，并在 **pos2** 中更新该索引。
    *   如果 **y2 > y1** 然后迭代，直到一个**‘N’**出现，并在 **pos3** 中更新该索引。
    *   如果 **y2 < y1** 那么迭代直到一个**的**到来，并在 **pos4** 中更新该索引。
4.  执行上述操作后，检查 **x1！= x2** 和 **y1！= y2** 然后打印 **"-1"** 表示无法到达目的地。
5.  否则，求 **pos1、pos2、pos3、pos4** 的最大值并打印出来。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum length
// of string required to reach from
// source to destination
void minimum_length(int x1, int y1,
                    int x2, int y2,
                    string str)
{
    // Size of the string
    int n = str.size();

    // Stores the index of the four
    // directions E, W, N, S
    int pos1, pos2, pos3, pos4;
    pos1 = -1;
    pos2 = -1;
    pos3 = -1;
    pos4 = -1;

    // If destination reached
    if (x1 == x2 && y1 == y2) {
        cout << 0 << endl;
    }

    // Iterate over the string
    else {
        for (int i = 0; i < n; i++) {

            // Move east
            if (x2 > x1) {

                // Change x1 according
                // to direction E
                if (str[i] == 'E') {
                    x1 = x1 + 1;
                    if (x1 == x2) {
                        pos1 = i;
                    }
                }
            }

            // Move west
            if (x2 < x1) {

                // Change x1 according
                // to direction W
                if (str[i] == 'W') {
                    x1 = x1 - 1;
                    if (x1 == x2) {
                        pos2 = i;
                    }
                }
            }

            // Move north
            if (y2 > y1) {

                // Change y1 according
                // to direction N
                if (str[i] == 'N') {
                    y1 = y1 + 1;
                    if (y1 == y2) {
                        pos3 = i;
                    }
                }
            }

            // Move south
            if (y2 < y1) {

                // Change y1 according
                // to direction S
                if (str[i] == 'S') {
                    y1 = y1 - 1;
                    if (y1 == y2) {
                        pos4 = i;
                    }
                }
            }
        }

        int z;
        // Store the max of all positions
        z = max(max(max(pos1, pos2),
                    pos3),
                pos4);

        // Print the minimum length of
        // string required
        if (x1 == x2 && y1 == y2) {
            cout << z + 1 << endl;
        }

        // Otherwise, it is impossible
        else {
            cout << "-1" << endl;
        }
    }
}

// Driver Code
int main()
{
    // Given string
    string str = "SESNW";

    // Given source and destination
    int x1 = 0, x2 = 1, y1 = 0, y2 = 1;

    // Function Call
    minimum_length(x1, y1, x2, y2, str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function to find the minimum length
// of string required to reach from
// source to destination
static void minimum_length(int x1, int y1,
                           int x2, int y2,
                           String str)
{

    // Size of the string
    int n = str.length();

    // Stores the index of the four
    // directions E, W, N, S
    int pos1, pos2, pos3, pos4;
    pos1 = -1;
    pos2 = -1;
    pos3 = -1;
    pos4 = -1;

    // If destination reached
    if (x1 == x2 && y1 == y2)
    {
        System.out.println("0");
    }

    // Iterate over the string
    else
    {
        for(int i = 0; i < n; i++)
        {

            // Move east
            if (x2 > x1)
            {

                // Change x1 according
                // to direction E
                if (str.charAt(i) == 'E')
                {
                    x1 = x1 + 1;

                    if (x1 == x2)
                    {
                        pos1 = i;
                    }
                }
            }

            // Move west
            if (x2 < x1)
            {

                // Change x1 according
                // to direction W
                if (str.charAt(i) == 'W')
                {
                    x1 = x1 - 1;

                    if (x1 == x2)
                    {
                        pos2 = i;
                    }
                }
            }

            // Move north
            if (y2 > y1)
            {

                // Change y1 according
                // to direction N
                if (str.charAt(i) == 'N')
                {
                    y1 = y1 + 1;

                    if (y1 == y2)
                    {
                        pos3 = i;
                    }
                }
            }

            // Move south
            if (y2 < y1)
            {

                // Change y1 according
                // to direction S
                if (str.charAt(i) == 'S')
                {
                    y1 = y1 - 1;

                    if (y1 == y2)
                    {
                        pos4 = i;
                    }
                }
            }
        }
        int z;

        // Store the max of all positions
        z = Math.max(pos1,
            Math.max(Math.max(pos2, pos3),
                              pos4));

        // Print the minimum length of
        // string required
        if (x1 == x2 && y1 == y2)
        {
             System.out.println(z + 1); 
        }

        // Otherwise, it is impossible
        else
        {
             System.out.println("-1");
        }
    }
}

// Driver Code
public static void main (String[] args)
throws java.lang.Exception
{

    // Given string
    String str = "SESNW";

    // Given source and destination
    int x1 = 0, x2 = 1, y1 = 0, y2 = 1;

    // Function call
    minimum_length(x1, y1, x2, y2, str);
}
}

// This code is contributed by bikram2001jha
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum length
# of string required to reach from
# source to destination
def minimum_length(x1, y1, x2, y2, str):

    # Size of the string
    n = len(str)

    # Stores the index of the four
    # directions E, W, N, S
    pos1 = -1
    pos2 = -1
    pos3 = -1
    pos4 = -1

    # If destination reached
    if (x1 == x2 and y1 == y2):
        print("0")

    # Iterate over the string
    else:
        for i in range(n):

            # Move east
            if (x2 > x1):

                # Change x1 according
                # to direction E
                if (str[i] == 'E'):
                    x1 = x1 + 1

                    if (x1 == x2):
                        pos1 = i

            # Move west
            if (x2 < x1):

                # Change x1 according
                # to direction W
                if (str[i] == 'W'):
                    x1 = x1 - 1

                    if (x1 == x2):
                        pos2 = i

            # Move north
            if (y2 > y1):

                # Change y1 according
                # to direction N
                if (str[i] == 'N'):
                    y1 = y1 + 1

                    if (y1 == y2):
                        pos3 = i

            # Move south
            if (y2 < y1):

                # Change y1 according
                # to direction S
                if (str[i] == 'S'):
                    y1 = y1 - 1

                    if (y1 == y2):
                        pos4 = i

        z = 0

        # Store the max of all positions
        z = max(pos1, max(max(pos2, pos3), pos4))

        # Print the minimum length of
        # string required
        if (x1 == x2 and y1 == y2):
            print(z + 1)

        # Otherwise, it is impossible
        else:
            print("-1")

# Driver Code

# Given string
str = "SESNW"

# Given source and destination
x1 = 0
x2 = 1
y1 = 0
y2 = 1

# Function call
minimum_length(x1, y1, x2, y2, str)

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum length
// of string required to reach from
// source to destination
static void minimum_length(int x1, int y1,
                           int x2, int y2,
                           string str)
{

    // Size of the string
    int n = str.Length;

    // Stores the index of the four
    // directions E, W, N, S
    int pos1, pos2, pos3, pos4;
    pos1 = -1;
    pos2 = -1;
    pos3 = -1;
    pos4 = -1;

    // If destination reached
    if (x1 == x2 && y1 == y2)
    {
        Console.WriteLine("0");
    }

    // Iterate over the string
    else
    {
        for(int i = 0; i < n; i++)
        {

            // Move east
            if (x2 > x1)
            {

                // Change x1 according
                // to direction E
                if (str[i] == 'E')
                {
                    x1 = x1 + 1;

                    if (x1 == x2)
                    {
                        pos1 = i;
                    }
                }
            }

            // Move west
            if (x2 < x1)
            {

                // Change x1 according
                // to direction W
                if (str[i] == 'W')
                {
                    x1 = x1 - 1;

                    if (x1 == x2)
                    {
                        pos2 = i;
                    }
                }
            }

            // Move north
            if (y2 > y1)
            {

                // Change y1 according
                // to direction N
                if (str[i] == 'N')
                {
                    y1 = y1 + 1;

                    if (y1 == y2)
                    {
                        pos3 = i;
                    }
                }
            }

            // Move south
            if (y2 < y1)
            {

                // Change y1 according
                // to direction S
                if (str[i] == 'S')
                {
                    y1 = y1 - 1;

                    if (y1 == y2)
                    {
                        pos4 = i;
                    }
                }
            }
        }
        int z;

        // Store the max of all positions
        z = Math.Max(pos1,
            Math.Max(Math.Max(pos2, pos3),
                              pos4));

        // Print the minimum length of
        // string required
        if (x1 == x2 && y1 == y2)
        {
             Console.WriteLine(z + 1); 
        }

        // Otherwise, it is impossible
        else
        {
             Console.WriteLine("-1");
        }
    }
}

// Driver Code
public static void Main ()
{

    // Given string
    string str = "SESNW";

    // Given source and destination
    int x1 = 0, x2 = 1, y1 = 0, y2 = 1;

    // Function call
    minimum_length(x1, y1, x2, y2, str);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum length
// of string required to reach from
// source to destination
function minimum_length(x1, y1,
                    x2,  y2,
                     str)
{

    // Size of the string
    var n = str.length;

    // Stores the index of the four
    // directions E, W, N, S
    var pos1, pos2, pos3, pos4;
    pos1 = -1;
    pos2 = -1;
    pos3 = -1;
    pos4 = -1;

    // If destination reached
    if (x1 == x2 && y1 == y2) {
        document.write(0+"<br>");
    }

    // Iterate over the string
    else {
        for (var i = 0; i < n; i++) {

            // Move east
            if (x2 > x1) {

                // Change x1 according
                // to direction E
                if (str[i] == 'E') {
                    x1 = x1 + 1;
                    if (x1 == x2) {
                        pos1 = i;
                    }
                }
            }

            // Move west
            if (x2 < x1) {

                // Change x1 according
                // to direction W
                if (str[i] == 'W') {
                    x1 = x1 - 1;
                    if (x1 == x2) {
                        pos2 = i;
                    }
                }
            }

            // Move north
            if (y2 > y1) {

                // Change y1 according
                // to direction N
                if (str[i] == 'N')
                {
                    y1 = y1 + 1;
                    if (y1 == y2)
                    {
                        pos3 = i;
                    }
                }
            }

            // Move south
            if (y2 < y1) {

                // Change y1 according
                // to direction S
                if (str[i] == 'S') {
                    y1 = y1 - 1;
                    if (y1 == y2) {
                        pos4 = i;
                    }
                }
            }
        }
        var z;

        // Store the max of all positions
        z = Math.max(Math.max(Math.max(pos1, pos2),
                    pos3),
                pos4);

        // Print the minimum length of
        // string required
        if (x1 == x2 && y1 == y2) {
            document.write(z + 1 + "<br>" );
        }

        // Otherwise, it is impossible
        else {
            document.write("-1<br>");;
        }
    }
}

// Driver Code

// Given string
var str = "SESNW";

// Given source and destination
var x1 = 0, x2 = 1, y1 = 0, y2 = 1;

// Function Call
minimum_length(x1, y1, x2, y2, str);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*