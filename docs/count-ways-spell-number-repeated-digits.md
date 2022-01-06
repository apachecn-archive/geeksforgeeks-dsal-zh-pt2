# 用重复的数字数出拼写数字的方法

> 原文:[https://www . geesforgeks . org/count-way-拼写-数字-重复数字/](https://www.geeksforgeeks.org/count-ways-spell-number-repeated-digits/)

给定一个包含数字的字符串。该数字可能包含许多相同的连续数字。任务是数出拼写数字的方法。
比如考虑 8884441100，可以简单地拼为三八三四双二和双零。一个也可以拼为双八，八，四，双四，二，二，双零。

**示例:**

```
Input :  num = 100
Output : 2
The number 100 has only 2 possibilities, 
1) one zero zero 
2) one double zero.

Input : num = 11112
Output: 8
1 1 1 1 2, 11 1 1 2, 1 1 11 2, 1 11 1 2
11 11 2, 1 111 2, 111 1 2, 1111 2

Input : num = 8884441100
Output: 64

Input : num = 12345
Output: 1

Input : num = 11111
Output: 16
```

这是一个简单的排列组合问题。如果我们以问题中给出的测试用例为例，11112。答案取决于 1111 的可能组合数量。“1111”的组合数是 2^3 = 8。由于我们的组合将取决于我们是否选择特定的 1，对于“2”，只有一种可能性 2^0 = 1，因此“11112”的答案将是 8*1 = 8。

因此，这种方法是计算字符串中特定的连续数字，并将 2^(count-1 数与之前的结果相乘。

## C++

```
// C++ program to count number of ways we
// can spell a number
#include<bits/stdc++.h>
using namespace std;
typedef long long int ll;

// Function to calculate all possible spells of
// a number with repeated digits
// num --> string which is favourite number
ll spellsCount(string num)
{
    int n = num.length();

    // final count of total possible spells
    ll result = 1;

    // iterate through complete number
    for (int i=0; i<n; i++)
    {
       // count contiguous frequency of particular
       // digit num[i]
       int count = 1;
       while (i < n-1 && num[i+1] == num[i])
       {
           count++;
           i++;
       }

       // Compute 2^(count-1) and multiply with result 
       result = result * pow(2, count-1);
    }
    return result;
}

// Driver program to run the case
int main()
{
    string num = "11112";
    cout << spellsCount(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of ways we
// can spell a number
class GFG {

    // Function to calculate all possible
    // spells of a number with repeated digits
    // num --> string which is favourite number
    static long spellsCount(String num)
    {

        int n = num.length();

        // final count of total possible spells
        long result = 1;

        // iterate through complete number
        for (int i = 0; i < n; i++) {

            // count contiguous frequency of
            // particular digit num[i]
            int count = 1;

            while (i < n - 1 && num.charAt(i + 1)
                               == num.charAt(i)) {

                count++;
                i++;
            }

            // Compute 2^(count-1) and multiply
            // with result
            result = result *
                     (long)Math.pow(2, count - 1);
        }
        return result;
    }

    public static void main(String[] args)
    {

        String num = "11112";

        System.out.print(spellsCount(num));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to count number of
# ways we can spell a number

# Function to calculate all possible
# spells of a number with repeated
# digits num --> string which is
# favourite number
def spellsCount(num):

    n = len(num);

    # final count of total
    # possible spells
    result = 1;

    # iterate through complete
    # number
    i = 0;
    while(i<n):

        # count contiguous frequency
        # of particular digit num[i]
        count = 1;
        while (i < n - 1 and
               num[i + 1] == num[i]):

            count += 1;
            i += 1;

        # Compute 2^(count-1) and
        # multiply with result
        result = result * int(pow(2, count - 1));
        i += 1;
    return result;

# Driver Code
num = "11112";
print(spellsCount(num));

# This code is contributed
# by mits
```

## C#

```
// C# program to count number of ways we
// can spell a number
using System;

class GFG {

    // Function to calculate all possible
    // spells of a number with repeated
    // digits num --> string which is
    // favourite number
    static long spellsCount(String num)
    {

        int n = num.Length;

        // final count of total possible
        // spells
        long result = 1;

        // iterate through complete number
        for (int i = 0; i < n; i++)
        {

            // count contiguous frequency of
            // particular digit num[i]
            int count = 1;

            while (i < n - 1 && num[i + 1]
                                == num[i])
            {
                count++;
                i++;
            }

            // Compute 2^(count-1) and multiply
            // with result
            result = result *
                    (long)Math.Pow(2, count - 1);
        }

        return result;
    }

    // Driver code
    public static void Main()
    {

        String num = "11112";

        Console.Write(spellsCount(num));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// number of ways we
// can spell a number

// Function to calculate
// all possible spells of
// a number with repeated
// digits num --> string
// which is favourite number
function spellsCount($num)
{
    $n = strlen($num);

    // final count of total
    // possible spells
    $result = 1;

    // iterate through
    // complete number
    for ($i = 0; $i < $n; $i++)
    {
    // count contiguous frequency
    // of particular digit num[i]
    $count = 1;
    while ($i < $n - 1 &&
           $num[$i + 1] == $num[$i])
    {
        $count++;
        $i++;
    }

    // Compute 2^(count-1) and
    // multiply with result
    $result = $result *
              pow(2, $count - 1);
    }
    return $result;
}

// Driver Code
$num = "11112";
echo spellsCount($num);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to count number of
// ways we can spell a number

// Function to calculate all possible
// spells of a number with repeated
// digits num --> string which is
// favourite number
function spellsCount(num)
{
    let n = num.length;

    // Final count of total possible
    // spells
    let result = 1;

    // Iterate through complete number
    for (let i = 0; i < n; i++)
    {

        // Count contiguous frequency of
        // particular digit num[i]
        let count = 1;

        while (i < n - 1 &&
               num[i + 1] == num[i])
        {
            count++;
            i++;
        }

        // Compute 2^(count-1) and multiply
        // with result
        result = result *
                 Math.pow(2, count - 1);
    }
    return result;
}

// Driver code
let num = "11112";

document.write(spellsCount(num));

// This code is contributed by code_hunt

</script>
```

**输出:**

```
8
```

如果你有另一种方法来解决这个问题，那么请分享。
本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。