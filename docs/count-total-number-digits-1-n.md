# 从 1 到 n 统计数字总数

> 原文:[https://www . geesforgeks . org/count-total-number-digits-1-n/](https://www.geeksforgeeks.org/count-total-number-digits-1-n/)

给定一个数字 n，计算从 1 到 n 写所有数字所需的总位数。

**示例:**

```
Input : 13
Output : 17
Numbers from 1 to 13 are 1, 2, 3, 4, 5, 
6, 7, 8, 9, 10, 11, 12, 13.
So 1 - 9 require 9 digits and 10 - 13 require 8
digits. Hence 9 + 8 = 17 digits are required. 

Input : 4
Output : 4
Numbers are 1, 2, 3, 4 . Hence 4 digits are required.
```

**天真递归法–**
解决上述问题的天真方法是计算每个数字从 1 到 n 的长度，然后计算每个数字的长度之和。同样的递归实现是–

## C++

```
#include <bits/stdc++.h>
using namespace std;

int findDigits(int n)
{
    if (n == 1)
    {
        return 1;
    }

    // Changing number to String
    string s = to_string(n);

    // Add length of number to  total_sum
    return s.length() + findDigits(n - 1);
}

// Driver code  
int main()
{
    int n = 13;

    cout << findDigits(n) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class Main {

    static int findDigits(int n)
    {
        if (n == 1) {
            return 1;
        }
        // Changing number to String
        String s = String.valueOf(n);

        // add length of number to  total_sum
        return s.length() + findDigits(n - 1);
    }
    public static void main(String[] args)
    {
        int n = 13;
        System.out.println(findDigits(n));
    }
}
```

## 蟒蛇 3

```
def findDigits(N):

    if N == 1:
        return 1

    # Changing number to string
    s = str(N)

    # Add length of number to total_sum
    return len(s) + findDigits(N - 1)

# Driver Code

# Given N
N = 13

# Function call
print(findDigits(N))

# This code is contributed by vishu2908
```

## C#

```
using System;
using System.Collections;
class GFG{

static int findDigits(int n)
{
  if (n == 1)
  {
    return 1;
  }

  // Changing number to String
  string s = n.ToString();

  // add length of number to  total_sum
  return s.Length + findDigits(n - 1);
}

// Driver Code
public static void Main(string[] args)
{
  int n = 13;
  Console.Write(findDigits(n));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

function findDigits(n)
{
    if (n == 1)
    {
        return 1;
    }

    // Changing number to String
    let s = n.toString();

    // Add length of number to total_sum
    return (s.length + findDigits(n - 1));
}

// Driver code

    let n = 13;

    document.write( findDigits(n) + "<br>");

//This code is contributed by Mayank Tyagi
</script>
```

**输出:**

```
 17
```

**迭代法–(优化)**
要计算位数，我们必须计算**以 1、10、百分之一写入所需的总位数。**号的地点。考虑 n = 13，所以一位的数字是 1，2，3，4，5，6，7，8，9，0，1，2，3，十位的数字是 1，1，1，1。因此，从 1 到 13 的总 1 位数基本上是 13(13–0)，十位数是 4(13–9)。我们再举一个例子，n = 234，那么单位位置的数字是 1 ( 24 次)、2 ( 24 次)、3 ( 24 次)、4 ( 24 次)、5 ( 23 次)、6 ( 23 次)、7 (23 次)、8 ( 23 次)、9 ( 23 次)、0 ( 23 次)，因此 23 * 6 + 24 * 4 = 234。十位数是 234–9 = 225，因为从 1 到 234 只有 1–9 是个位数。最后，百分之一位数是 234–99 = 135，因为只有 1–99 是两位数。因此，我们必须写入的总位数是 234(234–1+1)+225(234–10+1)+135(234–100+1)= 594。所以，基本上我们要**从 n 开始减少 0，9，99，999 …得到 1，10，百分之一，千分之一…位的位数，然后求和得到需要的结果**。

下面是这个方法的实现。

## C++

```
// C++ program to count total number
// of digits we have to write
// from 1 to n
#include <bits/stdc++.h>
using namespace std;

int totalDigits(int n)
{

    // number_of_digits store total
    // digits we have to write
    int number_of_digits = 0;

    // In the loop we are decreasing
    // 0, 9, 99 ... from n till
    // ( n - i + 1 ) is greater than 0
    // and sum them to number_of_digits
    // to get the required sum
    for(int i = 1; i <= n; i *= 10)
        number_of_digits += (n - i + 1);

    return number_of_digits;
}

// Driver code
int main()
{
    int n = 13;

    cout << totalDigits(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total number of digits
// we have to write from 1 to n

public class GFG {
    static int totalDigits(int n)
    {
        // number_of_digits store total
        // digits we have to write
        int number_of_digits = 0;

        // In the loop we are decreasing
        // 0, 9, 99 ... from n till
        // ( n - i + 1 ) is greater than 0
        // and sum them to number_of_digits
        // to get the required sum
        for (int i = 1; i <= n; i *= 10)
            number_of_digits += (n - i + 1);

        return number_of_digits;
    }

    // Driver Method
    public static void main(String[] args)
    {
        int n = 13;
        System.out.println(totalDigits(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to count total number
# of digits we have to write from 1 to n

def totalDigits(n):

    # number_of_digits store total
    # digits we have to write
    number_of_digits = 0;

    # In the loop we are decreasing
    # 0, 9, 99 ... from n till
    #( n - i + 1 ) is greater than 0
    # and sum them to number_of_digits
    # to get the required sum
    for i in range(1, n, 10):
        number_of_digits = (number_of_digits +
                                 (n - i + 1));

    return number_of_digits;

# Driver code
n = 13;
s = totalDigits(n) + 1;
print(s);

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to count total number of
// digits we have to write from 1 to n
using System;

public class GFG {

    static int totalDigits(int n)
    {

        // number_of_digits store total
        // digits we have to write
        int number_of_digits = 0;

        // In the loop we are decreasing
        // 0, 9, 99 ... from n till
        // ( n - i + 1 ) is greater than 0
        // and sum them to number_of_digits
        // to get the required sum
        for (int i = 1; i <= n; i *= 10)
            number_of_digits += (n - i + 1);

        return number_of_digits;
    }

    // Driver Method
    public static void Main()
    {
        int n = 13;

        Console.WriteLine(totalDigits(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// total number of digits
// we have to write from
// 1 to n

// Function that return
// total number of digits
function totalDigits($n)
{

    // number_of_digits store total
    // digits we have to write
    $number_of_digits = 0;

    // In the loop we are decreasing
    // 0, 9, 99 ... from n till
    // ( n - i + 1 ) is greater than 0
    // and sum them to number_of_digits
    // to get the required sum
    for ($i = 1; $i <= $n; $i *= 10)
        $number_of_digits += ($n - $i + 1);

    return $number_of_digits;
}

    // Driver Code
    $n = 13;
    echo totalDigits($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript program to count total number
// of digits we have to write
// from 1 to n
function totalDigits(n)
{

    // number_of_digits store total
    // digits we have to write
    var number_of_digits = 0;

    // In the loop we are decreasing
    // 0, 9, 99 ... from n till
    // ( n - i + 1 ) is greater than 0
    // and sum them to number_of_digits
    // to get the required sum
    for(var i = 1; i <= n; i *= 10)
        number_of_digits += (n - i + 1);

    return number_of_digits;
}

// Driver code
var n = 13;
document.write(totalDigits(n));

</script>
```

**输出:**

```
 17
```

**时间复杂度:** O(Logn)

本文由 **Surya Priy** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。