# 根据给定条件可以创建的最大对象数量

> 原文:[https://www . geesforgeks . org/根据给定条件可以创建的最大对象数/](https://www.geeksforgeeks.org/maximum-number-of-objects-that-can-be-created-as-per-given-conditions/)

给定类型-1 的 **N** 项和类型-2 的 **M** 项。一个对象可以由类型-1 的 **2 项**和 **1 项类型-2 的**或类型-2 的 **2 项**和 **1 项类型-1 的**件创建。任务是从给定数量的每种类型的项目中找到可以创建的最大对象数量。
**示例:**

> **输入:** N = 8，M = 7
> **输出:** 5
> **说明:**
> 3 对 2 型-1 和 1 型-2 对象。
> 2 对 1 型-1 和 2 型-2 对象。
> **输入:** N = 20，M = 3
> **输出:** 3
> **解释:**
> 3 对 2 type-1 和 1 type-2 对象。

**进场:**
按照以下步骤解决问题:

*   创建两个变量**初始**和**最终**。
*   初始值= N 的最小值，m
*   final =将 N + M 除以 3(因为对象由 3 个组件组成)。
*   初始和最终的最小值是可以从给定的 N-1 型和 M-2 型项目创建的最大对象数。

以下是上述方法的实现:

## C++

```
// C++ program for the above problem
#include <bits/stdc++.h>
using namespace std;

// Function for finding
// the maximum number of
// objects from N type-1 and
// M type-2 items

int numberOfObjects(int N, int M)
{
    // storing minimum of N and M
    int initial = min(N, M);

    // storing maximum number of
    // objects from given items
    int final = (N + M) / 3;

    return min(initial, final);
}

// Driver Code
int main()
{
    int N = 8;
    int M = 7;
    cout << numberOfObjects(N, M)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
class GFG{

// Function for finding
// the maximum number of
// objects from N type-1 and
// M type-2 items
static int numberOfObjects(int N, int M)
{

    // Storing minimum of N and M
    int initial = Math.min(N, M);

    // Storing maximum number of
    // objects from given items
    int last = (N + M) / 3;

    return Math.min(initial, last);
}

// Driver Code
public static void main(String[] args)
{
    int N = 8;
    int M = 7;

    System.out.println(numberOfObjects(N, M));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above problem

# Function for finding
# the maximum number of
# objects from N type-1 and
# M type-2 items
def numberOfObjects(N, M):

    # Storing minimum of N and M
    initial = min(N, M)

    # Storing maximum number of
    # objects from given items
    final = (N + M) // 3

    return min(initial, final)

# Driver Code
if __name__ == '__main__':

    N = 8
    M = 7

    print(numberOfObjects(N, M))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above problem
using System;
class GFG{

// Function for finding
// the maximum number of
// objects from N type-1 and
// M type-2 items
static int numberOfObjects(int N, int M)
{

    // Storing minimum of N and M
    int initial = Math.Min(N, M);

    // Storing maximum number of
    // objects from given items
    int last = (N + M) / 3;

    return Math.Min(initial, last);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 8;
    int M = 7;

    Console.Write(numberOfObjects(N, M));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>
// JavaScript program for the above problem

// Function for finding
// the maximum number of
// objects from N type-1 and
// M type-2 items
function numberOfObjects(N, M)
{

    // storing minimum of N and M
    let initial = Math.min(N, M);

    // storing maximum number of
    // objects from given items
    let final = Math.floor((N + M) / 3);
    return Math.min(initial, final);
}

// Driver Code
    let N = 8;
    let M = 7;
    document.write(numberOfObjects(N, M)
        + "<br>");

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(1)*
***辅助空间复杂度:** O(1)*