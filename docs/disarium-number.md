# 分类编号

> 原文:[https://www.geeksforgeeks.org/disarium-number/](https://www.geeksforgeeks.org/disarium-number/)

给定一个数字“n”，找出它是否是 Disarium。如果一个数的数字加上它们各自的位置的和等于这个数本身，这个数就叫做双元数。

**示例:**

```
Input   : n = 135
Output  : Yes 
1^1 + 3^2 + 5^3 = 135
Therefore, 135 is a Disarium number

Input   : n = 89
Output  : Yes 
8^1+9^2 = 89
Therefore, 89 is a Disarium number

Input   : n = 80
Output  : No
8^1 + 0^2 = 8
```

这个想法是首先计算给定数字的位数。一旦我们有了计数，我们遍历从最右边开始的所有数字(使用%运算符)，将其幂增加到数字计数，并减少数字计数。

以下是上述想法的实现。

## C++

```
// C++ program to check whether a number is Desoriam
// or not
#include<bits/stdc++.h>
using namespace std;

// Finds count of digits in n
int countDigits(int n)
{
    int count_digits = 0;

    // Count number of digits in n
    int x = n;
    while (x)
    {
        x = x/10;

        // Count the no. of digits
        count_digits++;
    }
    return count_digits;
}

// Function to check whether a number is disarium or not
bool check(int n)
{
    // Count digits in n.
    int count_digits = countDigits(n);

    // Compute sum of terms like digit multiplied by
    // power of position
    int sum = 0; // Initialize sum of terms
    int x = n;
    while (x)
    {
        // Get the rightmost digit
        int r = x%10;

        // Sum the digits by powering according to
        // the positions
        sum = sum + pow(r, count_digits--);
        x = x/10;
    }

    // If sum is same as number, then number is
    return (sum == n);
}

//Driver code to check if number is disarium or not
int main()
{
    int n = 135;
    if( check(n))
        cout << "Disarium Number";
    else
        cout << "Not a Disarium Number";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether a number is Desoriam
// or not

class Test
{
    // Method to check whether a number is disarium or not
    static boolean check(int n)
    {
        // Count digits in n.
        int count_digits = Integer.toString(n).length();

        // Compute sum of terms like digit multiplied by
        // power of position
        int sum = 0; // Initialize sum of terms
        int x = n;
        while (x!=0)
        {
            // Get the rightmost digit
            int r = x%10;

            // Sum the digits by powering according to
            // the positions
            sum = (int) (sum + Math.pow(r, count_digits--));
            x = x/10;
        }

        // If sum is same as number, then number is
        return (sum == n);
    }

    // Driver method
    public static void main(String[] args)
    {
        int n = 135;

        System.out.println(check(n) ? "Disarium Number" : "Not a Disarium Number");
    }
}
```

## 计算机编程语言

```
# Python program to check whether a number is Desarium
# or not
import math

# Method to check whether a number is disarium or not
def check(n) :

    # Count digits in n.
    count_digits = len(str(n))

    # Compute sum of terms like digit multiplied by
    # power of position
    sum = 0  # Initialize sum of terms
    x = n
    while (x!=0) :

        # Get the rightmost digit
        r = x % 10

        # Sum the digits by powering according to
        # the positions
        sum = (int) (sum + math.pow(r, count_digits))
        count_digits = count_digits - 1
        x = x/10

    # If sum is same as number, then number is
    if sum == n :
        return 1
    else :
        return 0

# Driver method
n = 135
if (check(n) == 1) :
    print "Disarium Number"
else :
    print "Not a Disarium Number"

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check whether a number
// is Desoriam or not
using System;

class GFG{

// Method to check whether a number
// is disarium or not
static bool check(int n)
{

    // Count digits in n.
    int count_digits = n.ToString().Length;

    // Compute sum of terms like digit
    // multiplied by power of position
    // Initialize sum of terms
    int sum = 0;
    int x = n;

    while (x != 0)
    {

        // Get the rightmost digit
        int r = x % 10;

        // Sum the digits by powering according
        // to the positions
        sum = (int)(sum + Math.Pow(
              r, count_digits--));
        x = x / 10;
    }

    // If sum is same as number,
    // then number is
    return (sum == n);
}

// Driver code
public static void Main(string[] args)
{
    int n = 135;

    Console.Write(check(n) ? "Disarium Number" :
                       "Not a Disarium Number");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to check whether a number is Desoriam
// or not
// Method to check whether a number is disarium or not
function check(n)
    {

        // Count digits in n.
        var count_digits = Number.toString();

        // Compute sum of terms like digit multiplied by
        // power of position
        var sum = 0; // Initialize sum of terms
        var x = n;
        while (x!=0)
        {
            // Get the rightmost digit
            var r = x%10;

            // Sum the digits by powering according to
            // the positions
            sum = (sum + Math.pow(r, count_digits--));
            x = x/10;
        }

        // If sum is same as number, then number is
        return (sum = n);
    }

    // Driver method
        var n = 135;

        document.write(check(n) ? "Disarium Number" : "Not a Disarium Number");

// This code is contributed by shivanisinghss2110
</script>
```

**输出:**

```
Disarium Number
```

本文由 **Sahil Chhabra(KILLER)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。