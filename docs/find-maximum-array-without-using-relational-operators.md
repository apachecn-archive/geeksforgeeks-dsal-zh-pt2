# 在不使用关系运算符的情况下找到数组中的最大值

> 原文:[https://www . geesforgeks . org/find-max-array-不使用关系运算符/](https://www.geeksforgeeks.org/find-maximum-array-without-using-relational-operators/)

给定一个非负整数的数组 A[]，在不使用[关系运算符](https://www.geeksforgeeks.org/operators-in-c-set-2-relational-and-logical-operators/)的情况下找到数组中的最大值。
**例:**

```
Input : A[] = {2, 3, 1, 4, 5}
Output : 5

Input : A[] = {23, 17, 93}
Output : 93
```

我们用重复减法找出最大值。为了找到两个数之间的最大值，我们取一个初始化为零的变量计数器。我们不断减小这两个值，直到它们都等于零(注意:第一个变为零的值不再减小)，同时增加计数器。当两个值都变为零时，计数器增加到两个值的最大值。我们首先找到前两个数字的最大值，然后逐一与数组的其余元素进行比较，以找到整体最大值。
以下是上述思路的实现。

## C++

```
#include <iostream>
using namespace std;

// Function to find maximum between two non-negative
// numbers without using relational operator.
int maximum(int x, int y)
{
    int c = 0;

    // Continues till both becomes zero.
    while(x || y)
    {
        // decrement if the value is not already zero
        if(x)
        x--;

        if(y)
        y--;
        c++;
    }
    return c;
}

// Function to find maximum in an array.
int arrayMaximum(int A[], int N)
{
    // calculating maximum of first two numbers
    int mx = A[0];

    // Iterating through each of the member of the array
    // to calculate the maximum
    for (int i = N-1; i; i--)

        // Finding the maximum between current maximum
       // and current value.
        mx = maximum(mx, A[i]);

    return mx;
}

// Driver code
int main()
{
    // Array declaration
    int A[] = {4, 8, 9, 18};
    int N = sizeof(A) / sizeof(A[0]);

    // Calling Function to find the maximum of the Array
    cout << arrayMaximum(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {

    // Function to find maximum between two
    // non-negative numbers without using
    // relational operator.
    static int maximum(int x, int y)
    {
        int c = 0;

        // Continues till both becomes zero.
        while (x > 0 || y > 0) {

            // decrement if the value is not
            // already zero
            if (x > 0)
                x--;

            if (y > 0)
                y--;
            c++;
        }

        return c;
    }

    // Function to find maximum in an array.
    static int arrayMaximum(int A[], int N)
    {

        // calculating maximum of first
        // two numbers
        int mx = A[0];

        // Iterating through each of the
        // member of the array to calculate
        // the maximum
        for (int i = N - 1; i > 0; i--)

            // Finding the maximum between
            // current maximum and current
            // value.
            mx = maximum(mx, A[i]);

        return mx;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Array declaration
        int A[] = { 4, 8, 9, 18 };
        int N = A.length;

        // Calling Function to find the maximum
        // of the Array
        System.out.print(arrayMaximum(A, N));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Function to find maximum between two
# non-negative numbers without using
# relational operator.
def maximum(x, y):
    c = 0

    # Continues till both becomes zero.
    while(x or y):

        # decrement if the value is
        # not already zero
        if(x):
            x -= 1

        if(y):
            y -= 1
        c += 1

    return c

# Function to find maximum in an array.
def arrayMaximum(A, N):

    # calculating maximum of
    # first two numbers
    mx = A[0]

    # Iterating through each of
    # the member of the array
    # to calculate the maximum
    i = N - 1
    while(i):

        # Finding the maximum between
        # current maximum and current value.
        mx = maximum(mx, A[i])
        i -= 1

    return mx

# Driver code
if __name__ == '__main__':

    # Array declaration
    A = [4, 8, 9, 18]
    N = len(A)

    # Calling Function to find the
    # maximum of the Array
    print(arrayMaximum(A, N))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to Find maximum
// in an array without using
// Relational Operators
using System;

class GFG
{

    // Function to find maximum
    // between two non-negative
    // numbers without using
    // relational operator.
    static int maximum(int x,
                       int y)
    {
        int c = 0;

        // Continues till
        // both becomes zero.
        while (x > 0 || y > 0)
        {

            // decrement if
            // the value is not
            // already zero
            if (x > 0)
                x--;

            if (y > 0)
                y--;
            c++;
        }

        return c;
    }

    // Function to find
    // maximum in an array.
    static int arrayMaximum(int []A,
                            int N)
    {

        // calculating
        // maximum of first
        // two numbers
        int mx = A[0];

        // Iterating through
        // each of the member
        // of the array to
        // calculate the maximum
        for (int i = N - 1;
                 i > 0; i--)

            // Finding the maximum
            // between current
            // maximum and current
            // value.
            mx = maximum(mx, A[i]);

        return mx;
    }

    // Driver code
    public static void Main()
    {

        // Array declaration
        int []A = { 4, 8, 9, 18 };
        int N = A.Length;

        // Calling Function to
        // find the maximum
        // of the Array
        Console.WriteLine(arrayMaximum(A, N));
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to find maximum
// between two non-negative
// numbers without using
// relational operator.
function maximum($x, $y)
{
    $c = 0;

    // Continues till
    // both becomes zero.
    while($x or $y)
    {
        // decrement if the value
        // is not already zero
        if($x)
        $x--;

        if($y)
        $y--;
        $c++;
    }
    return $c;
}

// Function to find
// maximum in an array.
function arrayMaximum($A, $N)
{
    // calculating maximum of
    // first two numbers
    $mx = $A[0];

    // Iterating through each of
    // the member of the array
    // to calculate the maximum
    for ( $i = $N - 1; $i; $i--)

        // Finding the maximum
        // between current maximum
        // and current value.
        $mx = maximum($mx, $A[$i]);

    return $mx;
}

// Driver code

// Array declaration
$A = array(4, 8, 9, 18);
$N = count($A);

// Calling Function to find
// the maximum of the Array
echo arrayMaximum($A, $N);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to Find maximum
    // in an array without using
    // Relational Operators

    // Function to find maximum
    // between two non-negative
    // numbers without using
    // relational operator.
    function maximum(x, y)
    {
        let c = 0;

        // Continues till
        // both becomes zero.
        while (x > 0 || y > 0)
        {

            // decrement if
            // the value is not
            // already zero
            if (x > 0)
                x--;

            if (y > 0)
                y--;
            c++;
        }

        return c;
    }

    // Function to find
    // maximum in an array.
    function arrayMaximum(A, N)
    {

        // calculating
        // maximum of first
        // two numbers
        let mx = A[0];

        // Iterating through
        // each of the member
        // of the array to
        // calculate the maximum
        for (let i = N - 1; i > 0; i--)

            // Finding the maximum
            // between current
            // maximum and current
            // value.
            mx = maximum(mx, A[i]);

        return mx;
    }

    // Array declaration
    let A = [ 4, 8, 9, 18 ];
    let N = A.length;

    // Calling Function to
    // find the maximum
    // of the Array
    document.write(arrayMaximum(A, N));

    // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
18
```

代码的时间复杂度将是 **O(N*max)** ，其中 max 是数组元素的最大值。
**限制**:只有当数组包含所有非负整数时，这才会起作用。