# 最大化(a+b)的值，使得(a*a-b*b = N)

> 原文:[https://www . geeksforgeeks . org/a+b 的价值最大化-a 平方与 b 平方之差为-n/](https://www.geeksforgeeks.org/maximize-value-of-a-plus-b-such-that-the-difference-of-a-square-and-b-square-is-n/)

给定一个奇数 **N** ，任务是找到(a+b)的最大值(其中 **a** 和 **b** 是整数)，使得**(a<sup>2</sup>–b<sup>2</sup>= N)**
**示例:**

```
Input: N = 1
Output: 1
Since a*a - b*b = 1 
The maximum value occurs when a = 1 and b = 0\. 
Thus, a + b = 1.

Input: N = 3
Output: 3
Since a*a - b*b = 3 
The maximum value occurs when a = 2 and b = 1\. 
Thus, a + b = 3.
```

**进场:**

*   给定

```
a*a - b*b = N
=> (a+b)*(a-b) = N
=> (a+b) = N/(a-b)
```

*   现在让上面的等式为真

```
We know that 
|a - b| ≥ 1

Therefore,
a + b ≤ N
```

*   现在为了最大化(a + b)的价值，

```
Maximising a + b ≤ N

=> a + b = N
```

*   因此，当我们需要最大化(a + b)的值时，N 是(a+b)的最大值，使得(a*a-b*b = N)。

以下是上述方法的实现:

## C++

```
// C++ program to maximize the value
// of (a+b) such that (a*a-b*b = N)

#include <bits/stdc++.h>
using namespace std;

// Function to maximize the value
// of (a+b) such that (a*a-b*b = n)
int maxValue(int n)
{
    return n;
}

// Driver code
int main()
{
    int n = 1;

    cout << maxValue(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximize the value
// of (a+b) such that (a*a-b*b = N)
class GFG
{

// Function to maximize the value
// of (a+b) such that (a*a-b*b = n)
static int maxValue(int n)
{
    return n;
}

// Driver code
public static void main(String[] args)
{
    int n = 1;

    System.out.print(maxValue(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to maximize the value
# of (a+b) such that (a*a-b*b = N)

# Function to maximize the value
# of (a+b) such that (a*a-b*b = n)
def maxValue(n) :

    return n;

# Driver code
if __name__ == "__main__" :

    n = 1;

    print(maxValue(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to maximize the value
// of (a+b) such that (a*a-b*b = N)
using System;

class GFG
{

    // Function to maximize the value
    // of (a+b) such that (a*a-b*b = n)
    static int maxValue(int n)
    {
        return n;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 1;

        Console.Write(maxValue(n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to maximize the value
// of (a+b) such that (a*a-b*b = N)

// Function to maximize the value
// of (a+b) such that (a*a-b*b = n)
function maxValue(n)
{
    return n;
}

// Driver code
var n = 1;
document.write(maxValue(n));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** ![O(1)  ](img/9cbdffa02bee5194f6140e6dd1bd796e.png "Rendered by QuickLaTeX.com")