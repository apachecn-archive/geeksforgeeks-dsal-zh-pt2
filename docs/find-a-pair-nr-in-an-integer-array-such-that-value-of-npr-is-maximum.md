# 在一个整数数组中找到一对(n，r)，使得 nPr 的值最大

> 原文:[https://www . geesforgeks . org/find-a-pair-NR-in-a-integer-array-so-value-NPR-is-maximum/](https://www.geeksforgeeks.org/find-a-pair-nr-in-an-integer-array-such-that-value-of-npr-is-maximum/)

给定一个非负整数数组**arr【】**，任务是找到一对 **(n，r)** 使得**T5】nP<sub>r</sub>T9】是最大可能且 **r ≤ n** 。**

> **<sup>n</sup> P <sub>r</sub> = n！/(n–r)！**

**示例:**

> **输入:** arr[] = {5，2，3，4，1}
> **输出:** n = 5 和 r = 4
> T6】5P<sub>4</sub>= 5！/ (5 – 4)!= 120，这是最大可能值。
> 
> **输入:** arr[] = {0，2，3，4，1，6，8，9}
> **输出:** n = 9，r = 8

**天真法:**简单的方法是考虑每一个 **(n，r)** 对，计算 **<sup>n</sup> P <sub>r</sub>** 值，找出其中最大值。

**高效进场:**自**T3】nP<sub>r</sub>= n！/(n–r)！= n *(n–1)*(n–2)*……*(n–r+1)**。
用很少的数学就可以说明 **n** 最大而**n–r**最小时**nP<sub>r</sub>T14】会最大。问题现在归结为从给定的数组中找到最大的 2 个元素。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to print the pair (n, r)
// such that nPr is maximum possible
void findPair(int arr[], int n)
{

    // There should be atleast 2 elements
    if (n < 2) {
        cout << "-1";
        return;
    }

    int i, first, second;
    first = second = -1;

    // Findex the largest 2 elements
    for (i = 0; i < n; i++) {
        if (arr[i] > first) {
            second = first;
            first = arr[i];
        }
        else if (arr[i] > second) {
            second = arr[i];
        }
    }

    cout << "n = " << first
         << " and r = " << second;
}

// Driver code
int main()
{
    int arr[] = { 0, 2, 3, 4, 1, 6, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findPair(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to print the pair (n, r)
    // such that nPr is maximum possible
    static void findPair(int arr[], int n)
    {

        // There should be atleast 2 elements
        if (n < 2)
        {
            System.out.print("-1");
            return;
        }

        int i, first, second;
        first = second = -1;

        // Findex the largest 2 elements
        for (i = 0; i < n; i++)
        {
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }
            else if (arr[i] > second)
            {
                second = arr[i];
            }
        }

        System.out.println("n = " + first +
                           " and r = " + second);
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 0, 2, 3, 4, 1, 6, 8, 9 };
        int n = arr.length;

        findPair(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the pair (n, r)
# such that nPr is maximum possible
def findPair(arr, n):

    # There should be atleast 2 elements
    if (n < 2):
        print("-1")
        return

    i = 0
    first = -1
    second = -1

    # Findex the largest 2 elements
    for i in range(n):
        if (arr[i] > first):
            second = first
            first = arr[i]
        elif (arr[i] > second):
            second = arr[i]

    print("n =", first, "and r =", second)

# Driver code
arr = [0, 2, 3, 4, 1, 6, 8, 9]
n = len(arr)

findPair(arr, n)

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function to print the pair (n, r)
    // such that nPr is maximum possible
    static void findPair(int[] arr, int n)
    {

        // There should be atleast 2 elements
        if (n < 2)
        {
            Console.Write("-1");
            return;
        }

        int i, first, second;
        first = second = -1;

        // Findex the largest 2 elements
        for (i = 0; i < n; i++)
        {
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }
            else if (arr[i] > second)
            {
                second = arr[i];
            }
        }

        Console.WriteLine("n = " + first +
                          " and r = " + second);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 0, 2, 3, 4, 1, 6, 8, 9 };
        int n = arr.Length;

        findPair(arr, n);
    }
}

// This code is contributed by CodeMech
```

## java 描述语言

```
<script>

// Java Script  implementation of the approach

    // Function to print the pair (n, r)
    // such that nPr is maximum possible
    function findPair(arr,n)
    {

        // There should be atleast 2 elements
        if (n < 2)
        {
            document.write("-1");
            return;
        }

        let i, first, second;
        first = second = -1;

        // Findex the largest 2 elements
        for (i = 0; i < n; i++)
        {
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }
            else if (arr[i] > second)
            {
                second = arr[i];
            }
        }

         document.write("n = " + first +
                           " and r = " + second);
    }

    // Driver code

        let arr = [ 0, 2, 3, 4, 1, 6, 8, 9 ];
        let n = arr.length;

        findPair(arr, n);

// This code is contributed by sravan kumar
</script>
```

**Output:** 

```
n = 9 and r = 8
```