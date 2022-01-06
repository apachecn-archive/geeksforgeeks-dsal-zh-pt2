# 计算将 N 分成三个三角形的方法

> 原文:[https://www . geeksforgeeks . org/n 分裂成三元组形成三角形的方式计数/](https://www.geeksforgeeks.org/count-of-ways-to-split-n-into-triplets-forming-a-triangle/)

给定一个整数 **N** ，任务是找到将 **N** 分割成有序的三胞胎的方法数量，这三胞胎可以一起形成一个三角形。

**示例:**

> **输入:** N = 15
> **输出:**可能的三角形总数为 28
> 
> **输入:** N = 9
> **输出:**可能的三角形总数为 10

**方法:**为了解决问题，需要进行以下观察:

> 如果 **N** 被拆分成 3 个整数 a、b 和 c，那么 a、b 和 c 需要满足以下条件才能组成三角形:
> 
> *   a + b > c
>     
> *   a + c > b
>     
> *   b + c > a

因此，使用嵌套循环迭代范围**【1，N】**以生成三元组，并针对每个三元组检查其是否形成三角形。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// required number of ways
int Numberofways(int n)
{
    int count = 0;

    for (int a = 1; a < n; a++) {

        for (int b = 1; b < n; b++) {

            int c = n - (a + b);

            // Check if a, b and c can
            // form a triangle
            if (a + b > c && a + c > b
                && b + c > a) {
                count++;
            }
        }
    }

    // Return number of ways
    return count;
}

// Driver Code
int main()
{
    int n = 15;

    cout << Numberofways(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;

class GFG {

    // Function to return the
    // required number of ways
    static int Numberofways(int n)
    {
        int count = 0;

        for (int a = 1; a < n; a++) {

            for (int b = 0; b < n; b++) {

                int c = n - (a + b);

                // Check if a, b, c can
                // form a triangle
                if (a + b > c && a + c > b
                    && b + c > a) {
                    count++;
                }
            }
        }

        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 15;

        System.out.println(Numberofways(n));
    }
}
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to return the
# required number of ways
def Numberofways(n):
    count = 0
    for a in range(1, n):
        for b in range(1, n):

            c = n - (a + b)

            # Check if a, b, c can form a triangle
            if(a < b + c and b < a + c and c < a + b):
                count += 1

    return count

# Driver code
n = 15
print(Numberofways(n))
```

## C#

```
// C# Program to implement
// the above approach

using System;

class GFG {

    // Function to return the
    // required number of ways
    static int Numberofways(int n)
    {
        int count = 0;
        for (int a = 1; a < n; a++) {
            for (int b = 1; b < n; b++) {
                int c = n - (a + b);

                // Check if a, b, c can form
                // a triangle or not
                if (a + b > c && a + c > b
                    && b + c > a) {
                    count++;
                }
            }
        }

        // Return number of ways
        return count;
    }

    // Driver Code
    static public void Main()
    {
        int n = 15;

        Console.WriteLine(Numberofways(n));
    }
}
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to return the
// required number of ways
function Numberofways(n)
{
    var count = 0;

    for (var a = 1; a < n; a++)
    {
        for (var b = 1; b < n; b++)
        {
            var c = n - (a + b);

            // Check if a, b and c can
            // form a triangle
            if (a + b > c && a + c > b
                && b + c > a)
            {
                count++;
            }
        }
    }

    // Return number of ways
    return count;
}

// Driver Code
var n = 15;
document.write( Numberofways(n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
28
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*