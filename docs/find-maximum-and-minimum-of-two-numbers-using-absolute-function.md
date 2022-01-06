# 使用绝对函数

求两个数的最大值和最小值

> 原文:[https://www . geesforgeks . org/find-两个数的最大值和最小值-使用绝对函数/](https://www.geeksforgeeks.org/find-maximum-and-minimum-of-two-numbers-using-absolute-function/)

给定两个数字，任务是使用绝对函数打印给定数字的最大值和最小值。
**例:**

```
Input: 99, 18
Output: Maximum = 99
        Minimum = 18

Input: -10, 20
Output: Maximum = 20
        Minimum = -10

Input: -1, -5
Output: Maximum = -1
        Minimum = -5
```

**方法:**
这个问题可以通过应用 [**绝对函数**](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)[**BODMAS 法则**](https://www.geeksforgeeks.org/expression-evaluation/) 的概念来解决。

*   **最大值:**

```
[(x + y + abs(x - y)) / 2]

```

*   **最小值:**

```
[(x + y - abs(x - y)) / 2]
```

让我们考虑两个数 x 和 y，其中 x = 20，y = 70。
**为最大值:**

```
[(x + y + abs(x - y)) / 2]
=> [(20 + 70)+ abs(20-70)) / 2]
=> 140 / 2 = 70 [MAXIMUM]
```

**最小值:**

```
[(x + y - abs(x - y)) / 2]
=> [(20 + 70) - abs(20-70)) / 2]
=> 40 / 2 = 20 [MINIMUM]
```

## C++

```
// C++ program to find maximum and
// minimum using Absolute function
#include <bits/stdc++.h>
using namespace std;

// Function to return maximum
// among the two numbers
int maximum(int x, int y)
{
        return ((x + y + abs(x - y)) / 2);
}

// Function to return minimum
// among the two numbers
int minimum(int x, int y)
{
        return ((x + y - abs(x - y)) / 2);
}

// Driver code
int main()
{
    int x = 99, y = 18;

    // Displaying the maximum value
    cout <<"Maximum: " << maximum(x, y) << endl;

    // Displaying the minimum value
    cout << "Minimum: " << minimum(x, y) << endl;
    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// C program to find maximum and
// minimum using Absolute function

#include <stdio.h>
#include <stdlib.h>

// Function to return maximum
// among the two numbers
int maximum(int x, int y)
{
        return ((x + y + abs(x - y)) / 2);
}

// Function to return minimum
// among the two numbers
int minimum(int x, int y)
{
        return ((x + y - abs(x - y)) / 2);
}

// Driver code
void main()
{
    int x = 99, y = 18;

    // Displaying the maximum value
    printf("Maximum: %d\n", maximum(x, y));

    // Displaying the minimum value
    printf("Minimum: %d\n", minimum(x, y));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum and 
// minimum using Absolute function 
class GFG
{

    // Function to return maximum 
    // among the two numbers 
    static int maximum(int x, int y) 
    { 
            return ((x + y + Math.abs(x - y)) / 2); 
    } 

    // Function to return minimum 
    // among the two numbers 
    static int minimum(int x, int y) 
    { 
            return ((x + y - Math.abs(x - y)) / 2); 
    } 

    // Driver code 
    public static void main (String[] args)
    { 
        int x = 99, y = 18; 

        // Displaying the maximum value 
        System.out.println("Maximum: " + maximum(x, y)); 

        // Displaying the minimum value 
        System.out.println("Minimum: " + minimum(x, y)); 
    } 
}

// This code is contributed by AnkitRai01
```

## C#

```
// C# program to find maximum and 
// minimum using Absolute function
using System;

class GFG
{

    // Function to return maximum 
    // among the two numbers 
    static int maximum(int x, int y) 
    { 
            return ((x + y + Math.Abs(x - y)) / 2); 
    } 

    // Function to return minimum 
    // among the two numbers 
    static int minimum(int x, int y) 
    { 
            return ((x + y - Math.Abs(x - y)) / 2); 
    } 

    // Driver code 
    public static void Main()
    { 
        int x = 99, y = 18; 

        // Displaying the maximum value 
        Console.WriteLine("Maximum: " + maximum(x, y)); 

        // Displaying the minimum value 
        Console.WriteLine("Minimum: " + minimum(x, y)); 
    } 
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find maximum and
# minimum using Absolute function

# Function to return maximum
# among the two numbers
def maximum(x, y):
        return ((x + y + abs(x - y)) // 2)

# Function to return minimum
# among the two numbers
def minimum(x, y):
        return ((x + y - abs(x - y)) // 2)

# Driver code
x = 99
y = 18

# Displaying the maximum value
print("Maximum:", maximum(x, y))

# Displaying the minimum value
print("Minimum:", minimum(x, y))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript program to find maximum and
// minimum using Absolute function

    // Function to return maximum
    // among the two numbers
    function maximum(x,y)
    {
            return ((x + y + Math.abs(x - y)) / 2);
    }

    // Function to return minimum
    // among the two numbers
    function minimum(x,y)
    {
            return ((x + y - Math.abs(x - y)) / 2);
    }

    // Driver code

        let x = 99, y = 18;

        // Displaying the maximum value
        document.write("Maximum: " + maximum(x, y)+"<br>");

        // Displaying the minimum value
        document.write("Minimum: " + minimum(x, y));

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
Maximum: 99
Minimum: 18
```