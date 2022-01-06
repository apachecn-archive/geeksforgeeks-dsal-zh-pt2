# 一行中没有重叠的元素的最大数量

> 原文:[https://www . geeksforgeeks . org/最大元素数量-不重叠在一行中/](https://www.geeksforgeeks.org/maximum-number-of-elements-without-overlapping-in-a-line/)

给定两个相同大小的数组 **X** 和**L****N**。 **X <sub>i</sub>** 代表无限直线中的位置。 **L <sub>i</sub>** 代表 ith 元素可以覆盖两侧的范围。任务是选择最大数量的元素，使得如果两个选定的元素覆盖右侧或左侧线段，则不会重叠。
**注:**数组 **X** 排序。
**例:**

> **输入:** x[] = {10，15，19，20}，L[] = {4，1，3，1}
> **输出:** 4
> 假设，第一个元素覆盖左侧段【6，10】
> 第二个元素覆盖左侧段【14，15】
> 第三个元素覆盖左侧段【16，19】
> 第四个元素覆盖右侧段【20，21】
> **输入:**

**进场:**
这个问题可以通过[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)解决。我们总是可以让第一个元素覆盖左线段，最后一个元素覆盖右线段。对于其他元素，如果可能的话，首先试着给出左线段，否则试着给出右线段。如果它们都不可能，那么离开元素。
以下是上述方法的实施:

## C++

```
// CPP program to find maximum number of
// elements without overlapping in a line
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum number of
// elements without overlapping in a line
int Segment(int x[], int l[], int n)
{
    // If n = 1, then answer is one
    if (n == 1)
        return 1;

    // We can always make 1st element to cover
    // left segment and nth the right segment
    int ans = 2;

    for (int i = 1; i < n - 1; i++)
    {
        // If left segment for ith element doesnt overlap
        // with i - 1 th element then do left
        if (x[i] - l[i] > x[i - 1])
            ans++;

        // else try towards right if possible
        else if (x[i] + l[i] < x[i + 1])
        {
            // update x[i] to right endpoint of
            // segment covered by it
            x[i] = x[i] + l[i];
            ans++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int x[] = {1, 3, 4, 5, 8}, l[] = {10, 1, 2, 2, 5};

    int n = sizeof(x) / sizeof(x[0]);

    // Function call
    cout << Segment(x, l, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of
// elements without overlapping in a line
import java.util.*;

class GFG
{

// Function to find maximum number of
// elements without overlapping in a line
static int Segment(int x[], int l[], int n)
{
    // If n = 1, then answer is one
    if (n == 1)
        return 1;

    // We can always make 1st element to cover
    // left segment and nth the right segment
    int ans = 2;

    for (int i = 1; i < n - 1; i++)
    {
        // If left segment for ith element
        // doesn't overlap with i - 1 th
        // element then do left
        if (x[i] - l[i] > x[i - 1])
            ans++;

        // else try towards right if possible
        else if (x[i] + l[i] < x[i + 1])
        {
            // update x[i] to right endpoint of
            // segment covered by it
            x[i] = x[i] + l[i];
            ans++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int x[] = {1, 3, 4, 5, 8},
        l[] = {10, 1, 2, 2, 5};

    int n = x.length;

    // Function call
    System.out.println(Segment(x, l, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find maximum number of
# elements without overlapping in a line

# Function to find maximum number of
# elements without overlapping in a line
def Segment(x, l, n):

    # If n = 1, then answer is one
    if (n == 1):
        return 1

    # We can always make 1st element to cover
    # left segment and nth the right segment
    ans = 2

    for i in range(1, n - 1):

        # If left segment for ith element doesnt overlap
        # with i - 1 th element then do left
        if (x[i] - l[i] > x[i - 1]):
            ans += 1

        # else try towards right if possible
        elif (x[i] + l[i] < x[i + 1]):

            # update x[i] to right endpoof
            # segment covered by it
            x[i] = x[i] + l[i]
            ans += 1

    # Return the required answer
    return ans

# Driver code
x = [1, 3, 4, 5, 8]
l = [10, 1, 2, 2, 5]

n = len(x)

# Function call
print(Segment(x, l, n))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to find maximum number of
// elements without overlapping in a line
using System;

class GFG
{

// Function to find maximum number of
// elements without overlapping in a line
static int Segment(int []x, int []l, int n)
{
    // If n = 1, then answer is one
    if (n == 1)
        return 1;

    // We can always make 1st element to cover
    // left segment and nth the right segment
    int ans = 2;

    for (int i = 1; i < n - 1; i++)
    {
        // If left segment for ith element
        // doesn't overlap with i - 1 th
        // element then do left
        if (x[i] - l[i] > x[i - 1])
            ans++;

        // else try towards right if possible
        else if (x[i] + l[i] < x[i + 1])
        {
            // update x[i] to right endpoint of
            // segment covered by it
            x[i] = x[i] + l[i];
            ans++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []x = {1, 3, 4, 5, 8};
    int []l = {10, 1, 2, 2, 5};

    int n = x.Length;

    // Function call
    Console.WriteLine(Segment(x, l, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find maximum number of
// elements without overlapping in a line

// Function to find maximum number of
// elements without overlapping in a line
function Segment(x, l, n) {
    // If n = 1, then answer is one
    if (n == 1)
        return 1;

    // We can always make 1st element to cover
    // left segment and nth the right segment
    let ans = 2;

    for (let i = 1; i < n - 1; i++) {
        // If left segment for ith element doesnt overlap
        // with i - 1 th element then do left
        if (x[i] - l[i] > x[i - 1])
            ans++;

        // else try towards right if possible
        else if (x[i] + l[i] < x[i + 1]) {
            // update x[i] to right endpolet of
            // segment covered by it
            x[i] = x[i] + l[i];
            ans++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code

let x = [1, 3, 4, 5, 8], l = [10, 1, 2, 2, 5];

let n = x.length;

// Function call
document.write(Segment(x, l, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
 4 
```

**时间复杂度:** O(N)