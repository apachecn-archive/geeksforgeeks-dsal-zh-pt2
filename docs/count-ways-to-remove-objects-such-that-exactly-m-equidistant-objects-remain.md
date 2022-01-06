# 计算移除物体的方法，以便精确地保留 M 个等距物体

> 原文:[https://www . geesforgeks . org/count-way-to-remove-objects-这样-恰好-m-等距-objects-retain/](https://www.geeksforgeeks.org/count-ways-to-remove-objects-such-that-exactly-m-equidistant-objects-remain/)

给定一个整数 **N** ，代表彼此相邻放置的对象，任务是计算移除对象的方法数量，以便在移除对象后，精确地留下 **M** 对象，并且每个相邻对象之间的距离相等。

**示例:**

> **输入:** N = 5，M = 3
> **输出:** 4
> **解释:**
> 让初始排列为**A<sub>1</sub>A<sub>2</sub>A<sub>3</sub>A<sub>4</sub>A<sub>5</sub>T20】。
> 以下安排是可能的:**
> 
> 1.  A<sub>1</sub>A<sub>2</sub>A<sub>3</sub>_ _
> 2.  _ A<sub>2</sub>A<sub>3</sub>A<sub>4</sub>_
> 3.  _ _ A<sub>3</sub>A<sub>4</sub>A<sub>5</sub>
> 4.  A<sub>1</sub>_ A<sub>3</sub>_ A<sub>5</sub>
> 
> 因此，可能的排列总数是 4。
> 
> **输入:** N = 2，M = 1
> T3】输出: 2

**方法:**这个想法是基于这样的观察，即带有 **D** 相邻空间的 **M** 物体的排列需要**(M+(M–1)* D)**长度，比如 **L** 。对于这种安排，有**(N–L+1)**选项。所以思路是从 **0** 到 **L** **≤ N** 迭代 **D** ，并据此找到路数。
按照以下步骤解决问题:

*   如果 **M** 的值为 **1** ，那么可能的排列数为 **N** 。因此，打印 **N** 的值。
*   否则，请执行以下步骤:
    *   初始化两个变量，说 **ans** 到 **0，**存储所需排列的总数。
    *   [使用变量 **D** 迭代一个循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)。请执行以下步骤:
        *   将 **D** 当前值所需的总长度存储在一个变量中，比如说 **L** 为**M+(M–1)* D**。
        *   如果 **L** 的值大于 **N** ，则[脱离回路](https://www.geeksforgeeks.org/break-statement-cc/)。
        *   否则，通过将值**(N–L+1)**添加到变量**和**来更新排列数。
*   完成上述步骤后，打印**和**的值作为排列总数。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of ways of
// removing objects such that after removal,
// exactly M equidistant objects remain
void waysToRemove(int n, int m)
{
    // Store the resultant
    // number of arrangements
    int ans = 0;

    // Base Case: When only
    // 1 object is left
    if (m == 1) {

        // Print the result and return
        cout << n;
        return;
    }

    // Iterate until len <= n and increment
    // the distance in each iteration
    for (int d = 0; d >= 0; d++) {

        // Total length if adjacent
        // objects are d distance apart
        int len = m + (m - 1) * d;

        // If len > n
        if (len > n)
            break;

        // Update the number of ways
        ans += (n - len) + 1;
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int N = 5, M = 3;
    waysToRemove(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the number of ways of
// removing objects such that after removal,
// exactly M equidistant objects remain
static void waysToRemove(int n, int m)
{

    // Store the resultant
    // number of arrangements
    int ans = 0;

    // Base Case: When only
    // 1 object is left
    if (m == 1)
    {

        // Print the result and return
        System.out.println(n);
        return;
    }

    // Iterate until len <= n and increment
    // the distance in each iteration
    for(int d = 0; d >= 0; d++)
    {

        // Total length if adjacent
        // objects are d distance apart
        int len = m + (m - 1) * d;

        // If len > n
        if (len > n)
            break;

        // Update the number of ways
        ans += (n - len) + 1;
    }

    // Print the result
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    int N = 5, M = 3;

    waysToRemove(N, M);
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of ways of
# removing objects such that after removal,
# exactly M equidistant objects remain
def waysToRemove(n, m):

    # Store the resultant
    # number of arrangements
    ans = 0

    # Base Case: When only
    # 1 object is left
    if (m == 1):

        # Print the result and return
        print(n)
        return

    d = 0

    # Iterate until len <= n and increment
    # the distance in each iteration
    while d >= 0:

        # Total length if adjacent
        # objects are d distance apart
        length = m + (m - 1) * d

        # If length > n
        if (length > n):
            break

        # Update the number of ways
        ans += (n - length) + 1

        d += 1

    # Print the result
    print(ans)

# Driver Code
if __name__ == "__main__" :

    N = 5
    M = 3

    waysToRemove(N, M)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to count the number of ways of
// removing objects such that after removal,
// exactly M equidistant objects remain
static void waysToRemove(int n, int m)
{

    // Store the resultant
    // number of arrangements
    int ans = 0;

    // Base Case: When only
    // 1 object is left
    if (m == 1)
    {

        // Print the result and return
        Console.Write(n);
        return;
    }

    // Iterate until len <= n and increment
    // the distance in each iteration
    for(int d = 0; d >= 0; d++)
    {

        // Total length if adjacent
        // objects are d distance apart
        int len = m + (m - 1) * d;

        // If len > n
        if (len > n)
            break;

        // Update the number of ways
        ans += (n - len) + 1;
    }

    // Print the result
    Console.Write(ans);
}

// Driver code
static void Main()
{
    int N = 5, M = 3;
    waysToRemove(N, M);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of ways of
// removing objects such that after removal,
// exactly M equidistant objects remain
function waysToRemove( n, m)
{
    // Store the resultant
    // number of arrangements
    var ans = 0;

    // Base Case: When only
    // 1 object is left
    if (m == 1) {

        // Print the result and return
        document.write( n);
        return;
    }

    // Iterate until len <= n and increment
    // the distance in each iteration
    for (var d = 0; d >= 0; d++) {

        // Total length if adjacent
        // objects are d distance apart
        var len = m + (m - 1) * d;

        // If len > n
        if (len > n)
            break;

        // Update the number of ways
        ans += (n - len) + 1;
    }

    // Print the result
    document.write( ans);
}

// Driver Code
var N = 5, M = 3;
waysToRemove(N, M);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)