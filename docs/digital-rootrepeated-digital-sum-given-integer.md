# 给定大整数的数字根(重复数字和)

> 原文:[https://www . geesforgeks . org/digital-root repeated-digital-sum-given-integer/](https://www.geeksforgeeks.org/digital-rootrepeated-digital-sum-given-integer/)

正整数的数字根是通过对整数的数字求和得到的。如果结果值是个位数，那么这个位数就是数字根。如果结果值包含两位或两位以上的数字，则将这些数字相加，并重复该过程。为了获得一个位数，这种情况会持续很长时间。
给定一个数字，任务是找到它的数字根。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。
问于[ACM-ICPC](http://acm.zju.edu.cn/onlinejudge/showProblem.do?problemId=115)T4**例:**T7】

```
Input : num = "1234"
Output : 1
Explanation : The sum of 1+2+3+4 = 10, 
              digSum(x) == 10
              Hence ans will be 1+0 = 1

Input : num = "5674"
Output : 4 
```

我们在下面的帖子中讨论了一个适合长时间使用的数字解决方案。
[求一个数的位数的和，直到和变成个位数](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)
在这篇文章中，对大数也讨论了类似的方法。

**方法 1**

找到 65785412
**的数字根步骤:**

1.  找出一个数字的所有数字
2.  把所有的数字一个一个加起来
3.  如果最后的总和是两位数，再次相加使其成为一位数
4.  以个位数获得的结果是数字的数字根

**示例:**
**输入:** 65785412
查找数字根:(6+5+7+8+5+4+1+2)= 38 =>11 =>(1+1)= 2
**输出:** 2

**方法二**

这个想法是基于这样一个事实，对于一个非零数字 num，如果数字可被 9 整除，数字根就是 9，否则数字根就是 num % 9。(详见[http://www.sjsu.edu/faculty/watkins/Digitsum0.htm](http://www.sjsu.edu/faculty/watkins/Digitsum0.htm))
找到 65785412
T4【步骤:

1.  数字总和= 6 + 5 + 7 + 8 + 5 + 4 + 1 + 2 = 38
2.  因为 38 不是 9 的倍数，所以数字根是 38 % 9 = 2。

## C++

```
// C++ program to find  digital root of a number
#include<bits/stdc++.h>
using namespace std;

// Returns digital root of num
int digitalRoot(string num)
{
    // If num is 0.
    if (num.compare("0") == 0)
        return 0;

    // Count sum of digits under mod 9
    int ans = 0;
    for (int i=0; i<num.length(); i++)
        ans = (ans + num[i]-'0') % 9;

    // If digit sum is multiple of 9, answer
    // 9, else remainder with 9.
    return (ans == 0)? 9 : ans % 9;
}

// Driver code
int main()
{
    string num = "65785412";

    // Calling digitalRoot function
    cout<< digitalRoot(num) <<endl;

    return 0;
}

// Note: Special case when num = "00..."
// program will not give correct output.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for digital root
import java.util.*;

public class GfG {

    static int digroot(int n)
    {
        int root = 0;

        // Loop to do sum while
        // sum is not less than
        // or equal to 9
        while (n > 0 || root > 9)
        {
             if (n == 0) {
                n = root;
                root = 0;
            }

            root += n % 10;
            n /= 10;
        }
        return root;
    }

    // Driver code
    public static void main(String argc[])
    {
        int n = 65785412;
        System.out.println(digroot(n));
    }
}

// This code is contributed by Gitanjali.
// This code will run for 0000 testcase also.
```

## 蟒蛇 3

```
# Python3 program to find digital root
# of a number
import math

# Returns digital root of num
def digitalRoot(num):

    # If num is 0.
    if (num == "0"):
        return 0

    # Count sum of digits under mod 9
    ans = 0
    for i in range (0, len(num)):
        ans = (ans + int(num[i])) % 9

    # If digit sum is multiple of 9, answer
    # 9, else remainder with 9.
    if(ans == 0):
        return 9
    else:
        return ans % 9

# Driver method
num = "65785412"

# Calling digitalRoot function
print (digitalRoot(num))

# This code is contributed by Gitanjali.
```

## C#

```
// C# code for digital root
using System;

class GfG {

    static int digroot(int n)
    {
        int root = 0;

        // Loop to do sum while
        // sum is not less than
        // or equal to 9
        while (n > 0 || root > 9)
        {
            if (n == 0) {
                n = root;
                root = 0;
            }

            root += n % 10;
            n /= 10;
        }
        return root;
    }

    // Driver code
    public static void Main()
    {
        int n = 65785412;
        Console.Write(digroot(n));
    }
}

// This code is contributed by Smitha
// This code will run for 0000 testcase also.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// digital root of a number

// Returns digital root of num
function digroot($n)
{
    $root = 0;

    // Loop to do sum while
    // sum is not less than
    // or equal to 9
    while ($n > 0 || $root > 9)
    {
        if ($n == 0)
        {
            $n = $root;
            $root = 0;
        }

        $root += $n % 10;
        $n /= 10;
    }
    return $root;
}

// Driver code
$num = 65785412;

// Calling digitalRoot function
echo digroot($num);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript code for digital root

    function digroot(n)
    {
        let root = 0;

        // Loop to do sum while
        // sum is not less than
        // or equal to 9
        while (n > 0 || root > 9)
        {
            if (n == 0) {
                n = root;
                root = 0;
            }

            root += n % 10;
            n = parseInt(n / 10, 10);
        }
        return root;
    }

    let n = 65785412;
      document.write(digroot(n));

</script>
```

**输出:**

```
2
```

本文由**希夫·普拉塔普·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。