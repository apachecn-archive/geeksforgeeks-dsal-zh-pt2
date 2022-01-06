# 计算一个范围内的一元数

> 原文:[https://www . geesforgeks . org/count-一元范围内的数字/](https://www.geeksforgeeks.org/count-unary-numbers-in-a-range/)

给定两个数字 A 和 B，A <=B, the task is to find the number of unary numbers between A and B, both inclusive.
**一元数字**:考虑数字 28。如果我们取其位数的平方和，2*2 + 8*8，我们得到 68。再取位数的平方和，得到 6*6 + 8*8=100。再做一次，我们得到 1*1 + 0*0 + 0*0 = 1。任何这样的数，最终导致 1，被称为一元数。

**例:**

```
Input : A = 1, B = 10
Output : 3

Input : A = 100, B = 150
Output : 7
```

其思想是递归计算数字的平方和，每次递归向下时，用计算出的和替换数字。
递归的**基本情况**为:

*   如果总和减为 1 或 7，则答案为真。
*   如果总和如果减少到 1 和 7 以外的一位数整数，则回答为假。

下面是这个问题的递归实现:

## C++

```
// CPP program to count unary numbers
// in a range

#include <iostream>
using namespace std;

// Function to check if a number is unary
bool isUnary(int n)
{
    /// Base case. Note that if we repeat
    // above process for 7, we get 1.
    if (n == 1 || n == 7)
        return true;
    else if (n / 10 == 0)
        return false;

    /// rec case
    int x, sum = 0;
    while (n != 0) {
        x = n % 10;
        sum = sum + x * x;
        n = n / 10;
    }

    isUnary(sum);
}

// Function to count unary numbers
// in a range
int countUnary(int a, int b)
{
    int count = 0;

    for (int i = a; i <= b; i++) {
        if (isUnary(i) == 1)
            count++;
    }

    return count;
}

// Driver Code
int main()
{
    int a = 1000, b = 1099;

    cout << countUnary(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to count unary numbers
// in a range

import java.io.*;

class GFG {

// Function to check if a number is unary
static boolean isUnary(int n)
{
    /// Base case. Note that if we repeat
    // above process for 7, we get 1.
    if (n == 1 || n == 7)
        return true;
    else if (n / 10 == 0)
        return false;

    /// rec case
    int x, sum = 0;
    while (n != 0) {
        x = n % 10;
        sum = sum + x * x;
        n = n / 10;
    }

return isUnary(sum);
}

// Function to count unary numbers
// in a range
static int countUnary(int a, int b)
{
    int count = 0;

    for (int i = a; i <= b; i++) {
        if (isUnary(i) == true)
            count++;
    }

    return count;
}

// Driver Code

    public static void main (String[] args) {

    int a = 1000, b = 1099;
    System.out.println (countUnary(a, b));

    }
//This code is contributed by ajit    
}
```

## 蟒蛇 3

```
# Python 3 program to count unary numbers
# in a range

# Function to check if a number is unary
def isUnary(n):

    # Base case. Note that if we repeat
    # above process for 7, we get 1.
    if (n == 1 or n == 7):
        return True
    elif (int(n / 10) == 0):
        return False

    # rec case
    sum = 0
    while (n != 0):
        x = n % 10
        sum = sum + x * x
        n = int(n / 10)

    return isUnary(sum)

# Function to count unary numbers
# in a range
def countUnary(a, b):
    count = 0

    for i in range(a, b + 1, 1):
        if (isUnary(i) == 1):
            count += 1

    return count

# Driver Code
if __name__ == '__main__':
    a = 1000
    b = 1099

    print(countUnary(a, b))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
//C# program to count unary numbers
// in a range
using System;

public class GFG {

// Function to check if a number is unary
static bool isUnary(int n)
{
    /// Base case. Note that if we repeat
    // above process for 7, we get 1.
    if (n == 1 || n == 7)
        return true;
    else if (n / 10 == 0)
        return false;

    /// rec case
    int x, sum = 0;
    while (n != 0) {
        x = n % 10;
        sum = sum + x * x;
        n = n / 10;
    }

return isUnary(sum);
}

// Function to count unary numbers
// in a range
static int countUnary(int a, int b)
{
    int count = 0;

    for (int i = a; i <= b; i++) {
        if (isUnary(i) == true)
            count++;
    }

    return count;
}

// Driver Code

    public static void Main () {

    int a = 1000, b = 1099;
    Console.WriteLine(countUnary(a, b));

    }
//This code is contributed by 29AjayKumar 
}
```

## java 描述语言

```
<script>

    // Javascript program to count unary
    // numbers in a range

    // Function to check if a number is unary
    function isUnary(n)
    {
        /// Base case. Note that if we repeat
        // above process for 7, we get 1.
        if (n == 1 || n == 7)
            return true;
        else if (parseInt(n / 10, 10) == 0)
            return false;

        /// rec case
        let x, sum = 0;
        while (n != 0) {
            x = n % 10;
            sum = sum + x * x;
            n = parseInt(n / 10, 10);
        }

        return isUnary(sum);
    }

    // Function to count unary numbers
    // in a range
    function countUnary(a, b)
    {
        let count = 0;

        for (let i = a; i <= b; i++) {
            if (isUnary(i) == true)
                count++;
        }

        return count;
    }

    let a = 1000, b = 1099;
    document.write(countUnary(a, b));

</script>
```

**Output:** 

```
13
```