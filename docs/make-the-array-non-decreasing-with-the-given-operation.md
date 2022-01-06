# 给定操作使数组不递减

> 原文:[https://www . geeksforgeeks . org/使数组不随给定操作递减/](https://www.geeksforgeeks.org/make-the-array-non-decreasing-with-the-given-operation/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是通过对每个数组元素最多应用一次给定的操作来检查是否有可能使数组不递减。在一次操作中，可以减少一个元素，即**arr[I]= arr[I]–1**。
**举例:**

> **输入:** arr[] = {1，2，1，2，3}
> **输出:**是
> 在第 2 个<sup>和第 4 个<sup>元素上应用给定的操作。
> 现在，数组变为{1，1，1，1，3}
> **输入:** arr[] = {1，3，1}
> **输出:**否</sup></sup>

**方法:**按照递增的顺序处理元素，并且只要可以，就减少当前元素，而不使其小于前一个元素。(因此，第一个元素应该总是减少。)如果在任何时候当前元素小于前一个元素，那么无论执行什么操作，答案都是“否”。
这个策略是最优的原因是，减少一个数字会使处理列表中的下一个元素更容易(或至少更容易)，因为当前一个数字较低时，下一个元素可能取的任何值都仍然有效，事实上，减少前一个数字会扩大下一个集合的可能值的范围。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to make array non-decreasing
bool isPossible(int a[], int n)
{
    // Take the first element
    int cur = a[0];

    // Perform the operation
    cur--;

    // Traverse the array
    for (int i = 1; i < n; i++) {

        // Next element
        int nxt = a[i];

        // If next element is greater than the
        // current element then decrease
        // it to increase the possibilities
        if (nxt > cur)
            nxt--;

        // It is not possible to make the
        // array non-decreasing with
        // the given operation
        else if (nxt < cur)
            return false;

        // Next element is now the current
        cur = nxt;
    }

    // The array can be made non-decreasing
    // with the given operation
    return true;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 1, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    if (isPossible(a, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to make array non-decreasing
static boolean isPossible(int a[], int n)
{
    // Take the first element
    int cur = a[0];

    // Perform the operation
    cur--;

    // Traverse the array
    for (int i = 1; i < n; i++)
    {

        // Next element
        int nxt = a[i];

        // If next element is greater than the
        // current element then decrease
        // it to increase the possibilities
        if (nxt > cur)
            nxt--;

        // It is not possible to make the
        // array non-decreasing with
        // the given operation
        else if (nxt < cur)
            return false;

        // Next element is now the current
        cur = nxt;
    }

    // The array can be made non-decreasing
    // with the given operation
    return true;
}

// Driver code
public static void main(String []args)
{
    int a[] = { 1, 2, 1, 2, 3 };
    int n = a.length;

    if (isPossible(a, n))
        System.out.printf("Yes");
    else
        System.out.printf("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to make array non-decreasing
def isPossible(a, n) :

    # Take the first element
    cur = a[0];

    # Perform the operation
    cur -= 1;

    # Traverse the array
    for i in range(1, n) :

        # Next element
        nxt = a[i];

        # If next element is greater than the
        # current element then decrease
        # it to increase the possibilities
        if (nxt > cur) :
            nxt -= 1;

        # It is not possible to make the
        # array non-decreasing with
        # the given operation
        elif (nxt < cur) :
            return False;

        # Next element is now the current
        cur = nxt;

    # The array can be made non-decreasing
    # with the given operation
    return True;

# Driver code
if __name__ == "__main__" :

    a = [ 1, 2, 1, 2, 3 ];
    n = len(a);

    if (isPossible(a, n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to make array non-decreasing
static Boolean isPossible(int []a, int n)
{
    // Take the first element
    int cur = a[0];

    // Perform the operation
    cur--;

    // Traverse the array
    for (int i = 1; i < n; i++)
    {

        // Next element
        int nxt = a[i];

        // If next element is greater than the
        // current element then decrease
        // it to increase the possibilities
        if (nxt > cur)
            nxt--;

        // It is not possible to make the
        // array non-decreasing with
        // the given operation
        else if (nxt < cur)
            return false;

        // Next element is now the current
        cur = nxt;
    }

    // The array can be made non-decreasing
    // with the given operation
    return true;
}

// Driver code
public static void Main(String []args)
{
    int []a = { 1, 2, 1, 2, 3 };
    int n = a.Length;

    if (isPossible(a, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to make array non-decreasing
function isPossible(a, n)
{

    // Take the first element
    var cur = a[0];

    // Perform the operation
    cur--;

    // Traverse the array
    for(var i = 1; i < n; i++)
    {

        // Next element
        var nxt = a[i];

        // If next element is greater than the
        // current element then decrease
        // it to increase the possibilities
        if (nxt > cur)
            nxt--;

        // It is not possible to make the
        // array non-decreasing with
        // the given operation
        else if (nxt < cur)
            return false;

        // Next element is now the current
        cur = nxt;
    }

    // The array can be made non-decreasing
    // with the given operation
    return true;
}

// Driver Code
var a = [ 1, 2, 1, 2, 3 ];
var n = a.length;

if (isPossible(a, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
Yes
```