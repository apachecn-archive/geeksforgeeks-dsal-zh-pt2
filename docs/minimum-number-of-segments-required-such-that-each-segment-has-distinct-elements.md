# 所需的最少分段数，使得每个分段具有不同的元素

> 原文:[https://www . geeksforgeeks . org/所需的最小段数，以便每个段都有不同的元素/](https://www.geeksforgeeks.org/minimum-number-of-segments-required-such-that-each-segment-has-distinct-elements/)

给定一个整数数组，任务是找到数组元素可以分成的最小段数，以便所有段都包含不同的元素。

**示例:**

```
Input: n=6 ; Array: 1, 7, 4, 3, 3, 8
Output: 2
Explanation:
Optimal way to create segments here is {1, 7, 4, 3} {3, 8}
Clearly, the answer is the maximum frequency of any element within the array i.e. '2'.
as '3' is the element which appears the most in the array (twice).

Input : n=5 ; Array: 2, 2, 3, 3, 3, 5
Output : 3
```

**进场:**

*   最佳方法是将所有不同的元素放在一个片段中。
*   然后，将所有其他出现多次的元素一个接一个地放入新的片段中，这样就不会有片段包含重复的元素。
*   所以，答案是给定数组中任何元素的最大频率。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the
// minimum segments required
void CountSegments(int N, int a[])
{
    // all values are '0' initially
    int frequency[10001] = { 0 };

    // count of segments
    int c = 0;

    // store frequency of every element
    for (int i = 0; i < N; i++) {
        frequency[a[i]]++;
    }

    // find maximum frequency
    for (int i = 0; i <= 10000; i++)
        c = max(c, frequency[i]);

    cout << c << "\n";
}

// Driver code
int main()
{
    int N = 6;
    int a[] = { 1, 3, 4, 3, 2, 3 };

    CountSegments(N, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

// Function that counts the
// minimum segments required
static void CountSegments(int N, int a[])
{
    // all values are '0' initially
    int frequency[] =  new int[10001];

    // count of segments
    int c = 0;

    // store frequency of every element
    for (int i = 0; i < N; i++) {
        frequency[a[i]]++;
    }

    // find maximum frequency
    for (int i = 0; i <= 10000; i++)
        c = Math.max(c, frequency[i]);

    System.out.println( c);
}

       // Driver code
    public static void main (String[] args) {
        int N = 6;
    int []a = { 1, 3, 4, 3, 2, 3 };

    CountSegments(N, a);
    }
}

// This Code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that counts the
# minimum segments required
def CountSegments(N, a):

    # all values are '0' initially
    frequency = [0] * 10001

    # count of segments
    c = 0

    # store frequency of every element
    for i in range(N) :
        frequency[a[i]] += 1

    # find maximum frequency
    for i in range(10001):
        c = max(c, frequency[i])

    print(c)

# Driver code
if __name__ == "__main__":
    N = 6
    a = [ 1, 3, 4, 3, 2, 3 ]
    CountSegments(N, a)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that counts the
// minimum segments required
static void CountSegments(int N, int []a)
{
    // all values are '0' initially
    int []frequency = new int[10001];

    // count of segments
    int c = 0;

    // store frequency of every element
    for (int i = 0; i < N; i++)
    {
        frequency[a[i]]++;
    }

    // find maximum frequency
    for (int i = 0; i <= 10000; i++)
        c = Math.Max(c, frequency[i]);

    Console.WriteLine( c);
}

// Driver code
public static void Main ()
{
    int N = 6;
    int []a = { 1, 3, 4, 3, 2, 3 };

    CountSegments(N, a);
}
}

// This code is contributed
// by inder_verma
```

## java 描述语言

```
<script>

// js implementation of the approach

// Function that counts the
// minimum segments required
function CountSegments(N,a)
{
    // all values are '0' initially
    var frequency = new Array(10001).fill(0);

    // count of segments
    let c = 0;

    // store frequency of every element
    for (var i = 0; i < N; i++)
    {
        frequency[a[i]]++;
    }

    // find maximum frequency
    for (var i = 0; i <= 10000; i++)
        c = Math.max(c, frequency[i]);

    document.write(c);
}

// Driver code

var N = 6;
var a = [1, 3, 4, 3, 2, 3 ];

CountSegments(N, a);

</script>
```

**Output:** 

```
3
```