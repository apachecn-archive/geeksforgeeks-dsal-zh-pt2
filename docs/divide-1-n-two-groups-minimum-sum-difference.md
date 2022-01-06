# 将 1 到 n 分成两个和差最小的组

> 原文:[https://www . geesforgeks . org/divide-1-n-two-group-mini-sum-difference/](https://www.geeksforgeeks.org/divide-1-n-two-groups-minimum-sum-difference/)

给定正整数 n，使得 n > 2。将 1 到 n 的数分成两组，使每组之和的绝对差最小。打印任意两个组，在第一行和下一行打印该组的元素。
**例:**

```
Input : 5
Output : 2
         5 2
         3
         4 3 1
Here sum of group 1 is 7 and sum of group 2 is 8.
Their absolute difference is 1 which is minimum.
We can have multiple correct answers. (1, 2, 5) and 
(3, 4) is another such group.

Input : 6
Output : 2
         6 4
         4
         5 3 2 1
```

我们总是可以把 n 个整数的和分成两组，这样它们和的绝对差就是 0 或 1。所以群的和最多相差 1。我们把群 1 的和定义为 n 个元素和的一半。
现在运行一个从 n 到 1 的循环，如果插入的元素不超过组 1 的总和，则将 I 插入组 1，否则将 I 插入组 2。

## C++

```
// CPP program to divide n integers
// in two groups such that absolute
// difference of their sum is minimum
#include <bits/stdc++.h>
using namespace std;

// To print vector along size
void printVector(vector<int> v)
{
    // Print vector size
    cout << v.size() << endl;

    // Print vector elements
    for (int i = 0; i < v.size(); i++)
        cout << v[i] << " ";

    cout << endl;
}

// To divide n in two groups such that
// absolute difference of their sum is
// minimum
void findTwoGroup(int n)
{
    // Find sum of all elements upto n
    int sum = n * (n + 1) / 2;

    // Sum of elements of group1
    int group1Sum = sum / 2;

    vector<int> group1, group2;

    for (int i = n; i > 0; i--) {

        // If sum is greater then or equal
        // to 0 include i in group 1
        // otherwise include in group2
        if (group1Sum - i >= 0) {

            group1.push_back(i);

            // Decrease sum of group1
            group1Sum -= i;
        }
        else {
            group2.push_back(i);
        }
    }

    // Print both the groups
    printVector(group1);
    printVector(group2);
}

// Driver program to test above functions
int main()
{
    int n = 5;
    findTwoGroup(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to divide n integers
// in two groups such that absolute
// difference of their sum is minimum
import java.io.*;
import java.util.*;

class GFG
{
    // To print vector along size
    static void printVector(Vector<Integer> v)
    {
        // Print vector size
        System.out.println(v.size());

        // Print vector elements
        for (int i = 0; i < v.size(); i++)
            System.out.print(v.get(i) + " ");

        System.out.println();
    }

    // To divide n in two groups such that
    // absolute difference of their sum is
    // minimum
    static void findTwoGroup(int n)
    {
        // Find sum of all elements upto n
        int sum = n * (n + 1) / 2;

        // Sum of elements of group1
        int group1Sum = sum / 2;

        Vector<Integer> group1 = new Vector<Integer>();
        Vector<Integer> group2 = new Vector<Integer>();

        for (int i = n; i > 0; i--) {

            // If sum is greater then or equal
            // to 0 include i in group1
            // otherwise include in group2
            if (group1Sum - i >= 0) {

                group1.add(i);

                // Decrease sum of group1
                group1Sum -= i;
            }
            else {
                group2.add(i);
            }
        }

        // Print both the groups
        printVector(group1);
        printVector(group2);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5;
        findTwoGroup(n);
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python program to divide n integers
# in two groups such that absolute
# difference of their sum is minimum
import math

# To print vector along size
def printVector( v):

    # Print vector size
    print(len(v))

    # Print vector elements
    for i in range( 0, len(v)):
        print(v[i] , end =  " ")

    print()

# To divide n in two groups such that
# absolute difference of their sum is
# minimum
def findTwoGroup(n):

    # Find sum of all elements upto n
    sum = n * (n + 1) / 2

    # Sum of elements of group1
    group1Sum = sum / 2

    group1=[]
    group2=[]
    for i in range(n, 0, -1):

        # If sum is greater then or equal
        # to 0 include i in group 1
        # otherwise include in group2
        if (group1Sum - i >= 0) :
            group1.append(i)

            # Decrease sum of group1
            group1Sum -= i

        else :
            group2.append(i)

    # Print both the groups
    printVector(group1)
    printVector(group2)

# driver code
n = 5
findTwoGroup(n)

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to divide n integers
// in two groups such that absolute
// difference of their sum is minimum
using System;
using System.Collections;

class GFG
{
// To print vector along size
static void printVector(ArrayList v)
{
    // Print vector size
    Console.WriteLine(v.Count);

    // Print vector elements
    for (int i = 0; i < v.Count; i++)
        Console.Write(v[i] + " ");

    Console.WriteLine();
}

// To divide n in two groups
// such that absolute difference
// of their sum is minimum
static void findTwoGroup(int n)
{
    // Find sum of all elements upto n
    int sum = n * (n + 1) / 2;

    // Sum of elements of group1
    int group1Sum = sum / 2;

    ArrayList group1 = new ArrayList();
    ArrayList group2 = new ArrayList();

    for (int i = n; i > 0; i--)
    {

        // If sum is greater then
        // or equal to 0 include i
        // in group1 otherwise
        // include in group2
        if (group1Sum - i >= 0)
        {
            group1.Add(i);

            // Decrease sum of group1
            group1Sum -= i;
        }
        else
        {
            group2.Add(i);
        }
    }

    // Print both the groups
    printVector(group1);
    printVector(group2);
}

// Driver code
public static void Main()
{
    int n = 5;
    findTwoGroup(n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to divide n
// integers in two groups
// such that absolute
// difference of their
// sum is minimum

// To print vector
// along size
function printVector($v)
{
    // Print vector size
    echo count($v) . "\n";

    // Print vector elements
    for ($i = 0;
         $i < count($v); $i++)
        echo $v[$i] . " ";

    echo "\n";
}

// To divide n in two groups
// such that absolute difference
// of their sum is minimum
function findTwoGroup($n)
{
    // Find sum of all
    // elements upto n
    $sum = $n * ($n + 1) / 2;

    // Sum of elements
    // of group1
    $group1Sum = (int)($sum / 2);

    $group1;
    $group2;
    $x = 0;
    $y = 0;

    for ($i = $n; $i > 0; $i--)
    {

        // If sum is greater then
        // or equal to 0 include
        // i in group 1 otherwise
        // include in group2
        if ($group1Sum - $i >= 0)
        {

            $group1[$x++] = $i;

            // Decrease sum
            // of group1
            $group1Sum -= $i;
        }
        else
        {
            $group2[$y++] = $i;
        }
    }

    // Print both the groups
    printVector($group1);
    printVector($group2);
}

// Driver Code
$n = 5;
findTwoGroup($n);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// Javascript program to divide n integers
// in two groups such that absolute
// difference of their sum is minimum

// To print vector along size
function printVector(v)
{
    // Print vector size
    document.write( v.length + "<br>");

    // Print vector elements
    for (var i = 0; i < v.length; i++)
        document.write( v[i] + " ");

    document.write("<br>");
}

// To divide n in two groups such that
// absolute difference of their sum is
// minimum
function findTwoGroup(n)
{
    // Find sum of all elements upto n
    var sum = n * (n + 1) / 2;

    // Sum of elements of group1
    var group1Sum = parseInt(sum / 2);

    var group1 = [], group2 = [];

    for (var i = n; i > 0; i--) {

        // If sum is greater then or equal
        // to 0 include i in group 1
        // otherwise include in group2
        if (group1Sum - i >= 0) {

            group1.push(i);

            // Decrease sum of group1
            group1Sum -= i;
        }
        else {
            group2.push(i);
        }
    }

    // Print both the groups
    printVector(group1);
    printVector(group2);
}

// Driver program to test above functions
var n = 5;
findTwoGroup(n);

</script>
```

**输出:**

```
2
5 2
3
4 3 1
```