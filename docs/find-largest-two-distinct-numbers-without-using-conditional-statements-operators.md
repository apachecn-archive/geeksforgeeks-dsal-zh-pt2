# 不使用任何条件语句或运算符的两个不同数字中最大的一个

> 原文:[https://www . geesforgeks . org/find-最大-两个不同的数字-不使用条件语句-运算符/](https://www.geeksforgeeks.org/find-largest-two-distinct-numbers-without-using-conditional-statements-operators/)

给定两个不同的正数，任务是在不使用任何条件语句(if…)和运算符(？:在 C/C++/Java 中)。

**示例:**

```
Input: a = 14, b = 15
Output: 15

Input: a = 1233133, b = 124
Output: 1233133
```

**方法**是根据下面的表达式返回值:

> a * (bool)(a / b) + b * (bool)(b / a)

如果 a > b，表达式 a / b 将给出 1，如果 a < b (only after typecasting the result to bool). 
将给出 0。因此，答案将是 a + 0 或 0 + b 的形式，取决于哪一个更大。

## C++

```
// C++ program for above implementation
#include <iostream>
using namespace std;

// Function to find the largest number
int largestNum(int a, int b)
{
    return a * (bool)(a / b) + b * (bool)(b / a);
}

// Drivers code
int main()
{
    int a = 22, b = 1231;
    cout << largestNum(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above implementation
class GFG
{

    // Function to find the largest number
    static int largestNum(int a, int b)
    {
        return a * ((a / b) > 0 ? 1 : 0) + b * ((b / a) > 0 ? 1 : 0);
    }

    // Drivers code
    public static void main(String[] args)
    {
        int a = 22, b = 1231;
        System.out.print(largestNum(a, b));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Function to find the largest number
def largestNum(a, b):
    return a * (bool)(a // b) + \
           b * (bool)(b // a);

# Driver Code
a = 22;
b = 1231;
print(largestNum(a, b));

# This code is contributed by Rajput-Ji
```

## C#

```

// C# program for above implementation
using System;

class GFG
{

    // Function to find the largest number
    static int largestNum(int a, int b)
    {
        return a * ((a / b) > 0 ? 1 : 0) + b * ((b / a) > 0 ? 1 : 0);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int a = 22, b = 1231;
        Console.Write(largestNum(a, b));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above implementation

// Function to find the largest number
function largestNum($a, $b)
{
    return ($a * (boolean)floor(($a / $b))) +
           ($b * (boolean)floor(($b / $a)));
}

// Drivers code
$a = 22; $b = 1231;
echo(largestNum($a, $b));

// This code is contributed
// by Mukul Singh
```

## java 描述语言

```
<script>

// Javascript program for above implementation

// Function to find the largest number
function largestNum(a , b)
{
    return a * (parseInt(a / b) > 0 ? 1 : 0) +
           b * (parseInt(b / a) > 0 ? 1 : 0);
}

// Driver code
var a = 22, b = 1231;

document.write(largestNum(a, b));

// This code is contributed by shikhasingrajput

</script>
```

**Output:** 

```
1231
```