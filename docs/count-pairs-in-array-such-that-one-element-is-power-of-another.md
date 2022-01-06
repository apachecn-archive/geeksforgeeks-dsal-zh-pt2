# 对数组中的对进行计数，使得一个元素是另一个元素的幂

> 原文:[https://www . geesforgeks . org/count-pairs-in-array-这样一个元素就是另一个元素的幂/](https://www.geeksforgeeks.org/count-pairs-in-array-such-that-one-element-is-power-of-another/)

给定一个数组 **arr[]** ，任务是计算数组中的对，使得每个对中的一个元素是另一个元素的幂。
**例:**

```
Input: arr[] = {16, 2, 3, 9}
Output: 2
The 2 pairs are (16, 2) and (3, 9)

Input: arr[] = {2, 3, 5, 7}
Output: 0
```

**进场:**

*   将数组作为输入后，首先我们需要[找出该数组](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)中所有可能的对。
*   所以，从数组中找出配对
*   然后对于每一对，检查一个元素是否是另一个元素的幂。如果是，则将所需计数增加 1。
*   检查完所有配对后，返回或打印该配对的计数。

以下是上述方法的实现:

## C++

```
// C++ program to count pairs in array
// such that one element is power of another

#include <bits/stdc++.h>
using namespace std;

// Function to check if given number number y
// is power of x
bool isPower(int x, int y)
{
    // log function to calculate value
    int res1 = log(y) / log(x);
    double res2 = log(y) / log(x);

    // compare to the result1
    // or result2 both are equal
    return (res1 == res2);
}

// Function to find pairs from array
int countPower(int arr[], int n)
{
    int res = 0;

    // Iterate through all pairs
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // Increment count if one is
            // the power of other
            if (isPower(arr[i], arr[j])
                || isPower(arr[j], arr[i]))
                res++;

    return res;
}

// Driver code
int main()
{
    int a[] = { 16, 2, 3, 9 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countPower(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs in array
// such that one element is power of another

class GFG
{

    // Function to check if given number number y
    // is power of x
    static boolean isPower(int x, int y)
    {
        // log function to calculate value
        int res1 = (int)(Math.log(y) / Math.log(x));
        double res2 = Math.log(y) / Math.log(x);

        // compare to the result1
        // or result2 both are equal
        return (res1 == res2);
    }

    // Function to find pairs from array
    static int countPower(int arr[], int n)
    {
        int res = 0;

        // Iterate through all pairs
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)

                // Increment count if one is
                // the power of other
                if (isPower(arr[i], arr[j])
                    || isPower(arr[j], arr[i]))
                    res++;

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { 16, 2, 3, 9 };
        int n =a.length;
        System.out.println(countPower(a, n));
    }

}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to count pairs in array
# such that one element is power of another

from math import log

# Function to check if given number number y
# is power of x
def isPower(x, y) :

    # log function to calculate value
    res1 = log(y) // log(x);
    res2 = log(y) / log(x);

    # compare to the result1
    # or result2 both are equal
    return (res1 == res2);

# Function to find pairs from array
def countPower( arr, n) :

    res = 0;

    # Iterate through all pairs
    for i in range(n) :
        for j in range(i + 1, n) :
            # Increment count if one is
            # the power of other
            if isPower(arr[i], arr[j]) or isPower(arr[j], arr[i]) :
                res += 1;

    return res;

# Driver code
if __name__ == "__main__" :

    a = [ 16, 2, 3, 9 ];
    n = len(a);

    print(countPower(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to count pairs in array
// such that one element is power of another

using System;

public class GFG
{

    // Function to check if given number number y
    // is power of x
    static bool isPower(int x, int y)
    {
        // log function to calculate value
        int res1 = (int)(Math.Log(y) / Math.Log(x));
        double res2 = Math.Log(y) / Math.Log(x);

        // compare to the result1
        // or result2 both are equal
        return (res1 == res2);
    }

    // Function to find pairs from array
    static int countPower(int []arr, int n)
    {
        int res = 0;

        // Iterate through all pairs
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)

                // Increment count if one is
                // the power of other
                if (isPower(arr[i], arr[j])
                    || isPower(arr[j], arr[i]))
                    res++;

        return res;
    }

    // Driver code
    public static void Main ()
    {
        int []a = { 16, 2, 3, 9 };
        int n =a.Length;
        Console.WriteLine(countPower(a, n));
    }

}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to count pairs in array
// such that one element is power of another

// Function to check if given number number y
// is power of x
function isPower(x, y)
{
    // log function to calculate value
    var res1 = parseInt(Math.log(y) / Math.log(x));
    var res2 = Math.log(y) / Math.log(x);

    // compare to the result1
    // or result2 both are equal
    return (res1 == res2);
}

// Function to find pairs from array
function countPower(arr, n)
{
    var res = 0;

    // Iterate through all pairs
    for (var i = 0; i < n; i++)
        for (var j = i + 1; j < n; j++)

            // Increment count if one is
            // the power of other
            if (isPower(arr[i], arr[j])
                || isPower(arr[j], arr[i]))
                res++;

    return res+1;
}

// Driver code
var a = [ 16, 2, 3, 9 ];
var n = a.length;
document.write(countPower(a, n));

// This code is contributed by rutvik_56.

</script>
```

**Output:** 

```
2
```

时间复杂度:O(n <sup>2</sup> )

辅助空间:0(1)