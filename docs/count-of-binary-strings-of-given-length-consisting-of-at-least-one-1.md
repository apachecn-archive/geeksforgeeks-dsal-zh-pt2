# 给定长度的二进制字符串的计数，至少包含一个 1

> 原文:[https://www . geesforgeks . org/给定长度的二进制字符串计数至少由一个 1 组成/](https://www.geeksforgeeks.org/count-of-binary-strings-of-given-length-consisting-of-at-least-one-1/)

给定一个整数 **N** ，任务是打印长度为 N 的二进制字符串的数量，其中至少有一个‘1’。

**示例:**

> **输入:** 2
> **输出:** 3
> **解释:**
> “01”、“10”和“11”是可能的字符串
> 
> **输入:** 3
> **输出:** 7
> **解释:**
> “001”“011”“010”“100”“101”“110”“111”是可能的字符串

**进场:**
我们可以观察到:

> 只有一个长度为 N 的字符串不包含任何 1，只有 0 填充的字符串。
> 由于**2<sup>N</sup>T4】的字符串可能长度为 N，所以需要的答案是**2<sup>N</sup>–1**。**

按照以下步骤解决问题:

*   初始化 X = 1。
*   通过对 X，N-1 次执行[按位左移](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)，计算到**2<sup>N</sup>T3。**
*   最后，打印 X–1 作为所需答案。

以下是我们方法的实施情况:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return
// the count of strings
long count_strings(long n)
{
    int x = 1;

    // Calculate pow(2, n)
    for (int i = 1; i < n; i++) {
        x = (1 << x);
    }

    // Return pow(2, n) - 1
    return x - 1;
}

// Driver Code
int main()
{
    long n = 3;

    cout << count_strings(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to return
// the count of Strings
static long count_Strings(long n)
{
    int x = 1;

    // Calculate Math.pow(2, n)
    for(int i = 1; i < n; i++)
    {
       x = (1 << x);
    }

    // Return Math.pow(2, n) - 1
    return x - 1;
}

// Driver Code
public static void main(String[] args)
{
    long n = 3;

    System.out.print(count_Strings(n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return
# the count of Strings
def count_Strings(n):

    x = 1;

    # Calculate pow(2, n)
    for i in range(1, n):
        x = (1 << x);

    # Return pow(2, n) - 1
    return x - 1;

# Driver Code
if __name__ == '__main__':

    n = 3;

    print(count_Strings(n));

# This code is contributed by Princi Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return
// the count of Strings
static long count_Strings(long n)
{
    int x = 1;

    // Calculate Math.Pow(2, n)
    for(int i = 1; i < n; i++)
    {
       x = (1 << x);
    }

    // Return Math.Pow(2, n) - 1
    return x - 1;
}

// Driver Code
public static void Main(String[] args)
{
    long n = 3;

    Console.Write(count_Strings(n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to return
    // the count of Strings
    function count_Strings(n)
    {
        var x = 1;

        // Calculate Math.pow(2, n)
        for (i = 1; i < n; i++) {
            x = (1 << x);
        }

        // Return Math.pow(2, n) - 1
        return x - 1;
    }

    // Driver Code

        var n = 3;

        document.write(count_Strings(n));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*