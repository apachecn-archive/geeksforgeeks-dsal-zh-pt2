# 从前 N 个数字中计算出相邻元素对的可能组合

> 原文:[https://www . geeksforgeeks . org/count-从第一个 n-numbers 开始计算具有相邻元素的配对的可能组合/](https://www.geeksforgeeks.org/count-possible-combinations-of-pairs-with-adjacent-elements-from-first-n-numbers/)

给定一个数字 N，任务是统计使用相邻元素形成的所有可能的对组合。
**注**:如果一个元素已经存在于一对中，则不能在下一对中拾取。例如:对于{1，2，3}: {1，2}和{2，3}将不会被视为正确的组合。
**示例:**

```
Input : N = 4
Output : 5
Explanation : If N = 4, the possible combinations are:
{1}, {2}, {3}, {4}
{1, 2}, {3, 4}
{1}, {2, 3}, {4}
{1}, {2}, {3, 4}
{1, 2}, {3}, {4}

Input : N = 5
Output : 8
```

**方法:**将问题分解成更小的子问题。如果有 N 个数字，并且有两种情况要么一个数字是单独的，要么它是成对的，如果一个数字是单独的，找到剩下的配对(n-1)个数字的方法，或者如果它是成对的，找到剩下的配对(n-2)个数字的方法。如果只剩下 2 个数字，它们可以单独或成对生成 2 个组合，如果只剩下一个数字，它将是单个的，所以只有 1 个组合。
以下是上述办法的实施情况:

## C++

```
#include <bits/stdc++.h>
using namespace std;
// Function to count the number of ways
int ways(int n)
{
    // If there is a single number left
    // it will form singleton
    if (n == 1) {
        return 1;
    }
    // if there are just 2 numbers left,
    // they will form a pair
    if (n == 2) {
        return 2;
    }
    else {
        return ways(n - 1) + ways(n - 2);
    }
}

// Driver Code
int main()
{
    int n = 5;

    cout << "Number of ways = " << ways(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG
{

// Function to count the number of ways
static int ways(int n)
{
    // If there is a single number left
    // it will form singleton
    if (n == 1)
    {
        return 1;
    }

    // if there are just 2 numbers left,
    // they will form a pair
    if (n == 2)
    {
        return 2;
    }
    else
    {
        return ways(n - 1) + ways(n - 2);
    }
}

// Driver Code
public static void main (String[] args)
{
    int n = 5;

    System.out.println("Number of ways = " + ways(n));
}
}
```

## 蟒蛇 3

```
# Python3 code implementation of the above program

# Function to count the number of ways
def ways(n) :

    # If there is a single number left
    # it will form singleton
    if (n == 1) :
        return 1;

    # if there are just 2 numbers left,
    # they will form a pair
    if (n == 2) :
        return 2;

    else :
        return ways(n - 1) + ways(n - 2);

# Driver Code
if __name__ == "__main__" :

    n = 5;

    print("Number of ways = ", ways(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above code
using System;

class GFG
{

// Function to count the number of ways
static int ways(int n)
{
    // If there is a single number left
    // it will form singleton
    if (n == 1)
    {
        return 1;
    }

    // if there are just 2 numbers left,
    // they will form a pair
    if (n == 2)
    {
        return 2;
    }
    else
    {
        return ways(n - 1) + ways(n - 2);
    }
}

// Driver Code
public static void Main()
{
    int n = 5;

    Console.WriteLine("Number of ways = " + ways(n));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the above code

    // Function to count the number of ways
    function ways(n)
    {
        // If there is a single number left
        // it will form singleton
        if (n == 1)
        {
            return 1;
        }

        // if there are just 2 numbers left,
        // they will form a pair
        if (n == 2)
        {
            return 2;
        }
        else
        {
            return ways(n - 1) + ways(n - 2);
        }
    }

    let n = 5;

    document.write("Number of ways = " + ways(n));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
Number of ways = 8
```