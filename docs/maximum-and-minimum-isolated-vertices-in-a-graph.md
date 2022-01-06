# 图中最大和最小孤立顶点

> 原文:[https://www . geesforgeks . org/最大和最小孤立图中顶点/](https://www.geeksforgeeks.org/maximum-and-minimum-isolated-vertices-in-a-graph/)

给定图的 n 个顶点和 m 条边。找出图中可能的最小数量和最大数量的孤立顶点。
**例:**

```
Input : 4 2
Output : Minimum 0
         Maximum 1

1--2 3--4 <---Minimum -  No isolated vertex
1--2   <--- Maximum - 1 Isolated vertex i.e. 4
   |
   3

Input : 5 2
Output : Minimum 1
         Maximum 2

1--2 3--4 5  <-- Minimum - 1 isolated vertex i.e. 5
1--2   4  5  <-- Maximum - 2 isolated vertex i.e. 4 and 5
   |
   3
```

1.  对于最小数量的孤立顶点，我们只通过一条边连接两个顶点。每个顶点应该只连接到另一个顶点，每个顶点应该有一个度
    因此，如果边的数量是‘m’，并且如果‘n’个顶点<= 2 *‘m’条边，则不存在孤立的顶点，并且如果该条件为假，则存在 n-2*m 个孤立的顶点。
2.  对于最大数量的孤立顶点，我们创建一个多边形，这样每个顶点都与其他顶点相连，并且每个顶点都与其他顶点有一条对角线。因此，从 n 边多边形的一个顶点到另一个顶点的对角线数是 n*(n-3)/2，连接相邻顶点的边数是 n。因此，边的总数是 n*(n-1)/2。

下面是上述方法的实现。

## C++

```
// CPP program to find maximum/minimum number
// of isolated vertices.
#include <bits/stdc++.h>
using namespace std;

// Function to find out the minimum and
// maximum number of isolated vertices
void find(int n, int m)
{
    // Condition to find out minimum number
    // of isolated vertices
    if (n <= 2 * m)
        cout << "Minimum " << 0 << endl;
    else
        cout << "Minimum " << n - 2 * m << endl;

    // To find out maximum number of isolated
    // vertices
    // Loop to find out value of number of
    // vertices that are connected
    int i;
    for (i = 1; i <= n; i++) {
        if (i * (i - 1) / 2 >= m)
            break;
    }
    cout << "Maximum " << n - i;
}

// Driver Function
int main()
{
    // Number of vertices
    int n = 4;

    // Number of edges
    int m = 2;

    // Calling the function to maximum and
    // minimum number of isolated vertices
    find(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum/minimum number
// of isolated vertices.

import java.io.*;

class GFG {

// Function to find out the minimum and
// maximum number of isolated vertices
 static void find(int n, int m)
{
    // Condition to find out minimum number
    // of isolated vertices
    if (n <= 2 * m)
        System.out.println( "Minimum " + 0);
    else
        System.out.println( "Minimum " + (n - 2 * m));

    // To find out maximum number of isolated
    // vertices
    // Loop to find out value of number of
    // vertices that are connected
    int i;
    for (i = 1; i <= n; i++) {
        if (i * (i - 1) / 2 >= m)
            break;
    }
    System.out.println( "Maximum " + (n - i));
}

// Driver Function

    public static void main (String[] args) {

    // Number of vertices
    int n = 4;

    // Number of edges
    int m = 2;

    // Calling the function to maximum and
    // minimum number of isolated vertices
    find(n, m);
    }
}
//This code is contributed by inder_verma.
```

## 蟒蛇 3

```
# Python3 program to find maximum/minimum
# number of isolated vertices.

# Function to find out the minimum and
# maximum number of isolated vertices
def find(n, m) :

    # Condition to find out minimum
    # number of isolated vertices
    if (n <= 2 * m):
        print("Minimum ", 0)
    else:
        print("Minimum ", n - 2 * m )

    # To find out maximum number of
    # isolated vertices
    # Loop to find out value of number
    # of vertices that are connected
    for i in range(1, n + 1):
        if (i * (i - 1) // 2 >= m):
            break

    print("Maximum ", n - i)

# Driver Code
if __name__ == '__main__':

    # Number of vertices
    n = 4

    # Number of edges
    m = 2

    # Calling the function to maximum and
    # minimum number of isolated vertices
    find(n, m)

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program to find maximum/
// minimum number of isolated vertices.
using System;

class GFG
{

// Function to find out the
// minimum and maximum number
// of isolated vertices
static void find(int n, int m)
{
    // Condition to find out minimum
    // number of isolated vertices
    if (n <= 2 * m)
        Console.WriteLine("Minimum " + 0);
    else
        Console.WriteLine("Minimum " +
                         (n - 2 * m));

    // To find out maximum number
    // of isolated vertices
    // Loop to find out value of
    // number of vertices that
    // are connected
    int i;
    for (i = 1; i <= n; i++)
    {
        if (i * (i - 1) / 2 >= m)
            break;
    }
    Console.WriteLine("Maximum " + (n - i));
}

// Driver Code
public static void Main ()
{

    // Number of vertices
    int n = 4;

    // Number of edges
    int m = 2;

    // Calling the function to 
    // maximum and minimum number
    // of isolated vertices
    find(n, m);
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum/minimum
// number of isolated vertices.

// Function to find out the
// minimum and maximum number
// of isolated vertices
function find($n, $m)
{
    // Condition to find out minimum
    // number of isolated vertices
    if ($n <= 2 * $m)
        echo "Minimum 0\n";
    else
        echo "Minimum " , ($n - 2 * $m);

    // To find out maximum number
    // of isolated vertices
    // Loop to find out value of number
    // of vertices that are connected
    for ($i = 1; $i <= $n; $i++)
    {
        if ($i * ($i - 1) / 2 >= $m)
            break;
    }
    echo "Maximum " , ($n - $i);
}

// Driver Code

// Number of vertices
$n = 4;

// Number of edges
$m = 2;

// Calling the function to
// maximum and minimum number
// of isolated vertices
find($n, $m);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>
    // Javascript program to find maximum/
    // minimum number of isolated vertices.

    // Function to find out the
    // minimum and maximum number
    // of isolated vertices
    function find(n, m)
    {

        // Condition to find out minimum
        // number of isolated vertices
        if (n <= 2 * m)
            document.write("Minimum " + 0 + "</br>");
        else
            document.write("Minimum " + (n - 2 * m) + "</br>");

        // To find out maximum number
        // of isolated vertices
        // Loop to find out value of
        // number of vertices that
        // are connected
        let i;
        for (i = 1; i <= n; i++)
        {
            if (i * parseInt((i - 1) / 2, 10) >= m)
                break;
        }
        document.write("Maximum " + (n - i));
    }

    // Number of vertices
    let n = 4;

    // Number of edges
    let m = 2;

    // Calling the function to 
    // maximum and minimum number
    // of isolated vertices
    find(n, m);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
Minimum 0
Maximum 1
```

**时间复杂度**–O(n)