# 使数字神奇的最小操作

> 原文:[https://www . geesforgeks . org/minimum-operations-make-number-magic/](https://www.geeksforgeeks.org/minimal-operations-make-number-magical/)

给定一个 6 位数，计算需要替换的最小位数，以使数字变得神奇。如果前三位数的总和等于后三位数的总和，这个数字就被认为是神奇的。在一个操作中，我们可以在任意位置选择一个数字，并用任意数字替换它。

**示例:**

```
Input: 123456 
Output: 2 
Explanation : Replace 4 with 0 and 5 with 0,
              then number = 123006, where 
              1 + 2 + 3 = 0 + 0 + 6,
              hence number of replacements
              done = 2  

Input: 111000
Output: 1
Explanation: Replace 0 with 3, then 
             number = 111030, where 
             1 + 1 + 1 = 0 + 3 + 0,
             hence number of replacements
             done = 1
```

**方法:**
最好的方法是查看所有神奇的数字和需要更换的数量。运行一个生成所有 6 位数的循环。检查这个数字是否神奇，如果是，那么简单地计算需要替换的数量，并与 ans 进行比较，如果它更小，那么使它成为 ans，并在最后返回 ans。

下面是上述方法的实现。

## C++

```
// CPP program to make a number magical
#include "bits/stdc++.h"
using namespace std;

// function to calculate the minimal changes
int calculate(string s)
{
    // maximum digits that can be changed
    int ans = 6;

    // nested loops to generate all 6
    // digit numbers
    for (int i = 0; i < 10; ++i) {
        for (int j = 0; j < 10; ++j) {
            for (int k = 0; k < 10; ++k) {
                for (int l = 0; l < 10; ++l) {
                    for (int m = 0; m < 10; ++m) {
                        for (int n = 0; n < 10; ++n) {
                            if (i + j + k == l + m + n) {

                                // counter to count the number
                                // of change required
                                int c = 0;

                                // if first digit is equal
                                if (i != s[0] - '0')
                                    c++;

                                // if 2nd digit is equal   
                                if (j != s[1] - '0')
                                    c++;

                                // if 3rd digit is equal   
                                if (k != s[2] - '0')
                                    c++;

                                // if 4th digit is equal   
                                if (l != s[3] - '0')
                                    c++;

                                // if 5th digit is equal   
                                if (m != s[4] - '0')
                                    c++;

                                // if 6th digit is equal   
                                if (n != s[5] - '0')
                                    c++;

                                // checks if less then the
                                // previous calculate changes
                                if (c < ans)
                                    ans = c;
                            }
                        }
                    }
                }
            }
        }
    }

    // returns the answer
    return ans;
}

// driver program to test the above function
int main()
{
    // number stored in string
    string s = "123456";

    // prints the minimum operations
    cout << calculate(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to make a number magical
import java.io.*;

class GFG {

// function to calculate the minimal changes
static int calculate(String s)
{
    // maximum digits that can be changed
    int ans = 6;

    // nested loops to generate
    // all 6 digit numbers
    for (int i = 0; i < 10; ++i) {
        for (int j = 0; j < 10; ++j) {
            for (int k = 0; k < 10; ++k) {
                for (int l = 0; l < 10; ++l) {
                    for (int m = 0; m < 10; ++m) {
                        for (int n = 0; n < 10; ++n) {
                            if (i + j + k == l + m + n) {

                                // counter to count the number
                                // of change required
                                int c = 0;

                                // if first digit is equal
                                if (i != s.charAt(0) - '0')
                                    c++;

                                // if 2nd digit is equal
                                if (j != s.charAt(1) - '0')
                                    c++;

                                // if 3rd digit is equal
                                if (k != s.charAt(2) - '0')
                                    c++;

                                // if 4th digit is equal
                                if (l != s.charAt(3) - '0')
                                    c++;

                                // if 5th digit is equal
                                if (m != s.charAt(4) - '0')
                                    c++;

                                // if 6th digit is equal
                                if (n != s.charAt(5) - '0')
                                    c++;

                                // checks if less then the
                                // previous calculate changes
                                if (c < ans)
                                    ans = c;
                            }
                        }
                    }
                }
            }
        }
    }

    // returns the answer
    return ans;
}

   // Driver code
    static public void main (String[] args)
    {
        // number stored in string
        String s = "123456";

        // prints the minimum operations
        System.out.println(calculate(s));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to make a number magical

# function to calculate the minimal changes
def calculate( s):

    # maximum digits that can be changed
    ans = 6

    # nested loops to generate all 6
    # digit numbers
    for i in range(10):
        for j in range(10):
            for k in range(10):
                for l in range(10):
                    for  m in range(10):
                        for n in range(10):
                            if (i + j + k == l + m + n):

                                # counter to count the number
                                # of change required
                                c = 0

                                # if first digit is equal
                                if (i != ord(s[0]) - ord('0')):
                                    c+=1

                                # if 2nd digit is equal   
                                if (j != ord(s[1]) - ord('0')):
                                    c+=1

                                # if 3rd digit is equal   
                                if (k != ord(s[2]) - ord('0')):
                                    c+=1

                                # if 4th digit is equal   
                                if (l != ord(s[3]) - ord('0')):
                                    c+=1

                                # if 5th digit is equal   
                                if (m != ord(s[4]) - ord('0')):
                                    c+=1

                                # if 6th digit is equal   
                                if (n != ord(s[5]) - ord('0')):
                                    c+=1

                                # checks if less then the
                                # previous calculate changes
                                if (c < ans):
                                    ans = c

    # returns the answer
    return ans

# driver program to test the above function
if __name__ == "__main__":

    # number stored in string
    s = "123456"

    # prints the minimum operations
    print(calculate(s))
```

## C#

```
// C# program to make a number magical
using System;

class GFG {

// function to calculate the minimal changes
static int calculate(string s)
{
    // maximum digits that can be changed
    int ans = 6;

    // nested loops to generate
    // all 6 digit numbers
    for (int i = 0; i < 10; ++i) {
        for (int j = 0; j < 10; ++j) {
            for (int k = 0; k < 10; ++k) {
                for (int l = 0; l < 10; ++l) {
                    for (int m = 0; m < 10; ++m) {
                        for (int n = 0; n < 10; ++n) {
                            if (i + j + k == l + m + n) {

                                // counter to count the number
                                // of change required
                                int c = 0;

                                // if first digit is equal
                                if (i != s[0] - '0')
                                    c++;

                                // if 2nd digit is equal
                                if (j != s[1] - '0')
                                    c++;

                                // if 3rd digit is equal
                                if (k != s[2] - '0')
                                    c++;

                                // if 4th digit is equal
                                if (l != s[3] - '0')
                                    c++;

                                // if 5th digit is equal
                                if (m != s[4] - '0')
                                    c++;

                                // if 6th digit is equal
                                if (n != s[5] - '0')
                                    c++;

                                // checks if less then the
                                // previous calculate changes
                                if (c < ans)
                                    ans = c;
                            }
                        }
                    }
                }
            }
        }
    }

    // returns the answer
    return ans;
}

    // Driver code
    static public void Main ()
    {
        // number stored in string
        string s = "123456";

        // prints the minimum operations
        Console.WriteLine(calculate(s));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to make a number magical

// function to calculate
// the minimal changes
function calculate($s)
{
    // maximum digits that
    // can be changed
    $ans = 6;

    // nested loops to generate
    //  all 6 digit numbers
    for ($i = 0; $i < 10; ++$i) {
        for ($j = 0; $j < 10; ++$j) {
            for ($k = 0; $k < 10; ++$k) {
                for ( $l = 0; $l < 10; ++$l) {
                    for ($m = 0; $m < 10; ++$m) {
                        for ( $n = 0; $n < 10; ++$n) {
                            if ($i + $j + $k == $l + $m + $n) {

                                // counter to count the number
                                // of change required
                                $c = 0;

                                // if first digit is equal
                                if ($i != $s[0] - '0')
                                    $c++;

                                // if 2nd digit is equal
                                if ($j != $s[1] - '0')
                                    $c++;

                                // if 3rd digit is equal
                                if ($k != $s[2] - '0')
                                    $c++;

                                // if 4th digit is equal
                                if ($l != $s[3] - '0')
                                    $c++;

                                // if 5th digit is equal
                                if ($m != $s[4] - '0')
                                    $c++;

                                // if 6th digit is equal
                                if ($n != $s[5] - '0')
                                    $c++;

                                // checks if less then the
                                // previous calculate changes
                                if ($c < $ans)
                                    $ans = $c;
                            }
                        }
                    }
                }
            }
        }
    }

    // returns the answer
    return $ans;
}

// Driver Code
// number stored in string
$s = "123456";

// prints the minimum operations
echo calculate($s);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to make a number magical

// Function to calculate the minimal changes
function calculate(s)
{

    // Maximum digits that can be changed
    let ans = 6;

    // Nested loops to generate
    // all 6 digit numbers
    for(let i = 0; i < 10; ++i)
    {
        for(let j = 0; j < 10; ++j)
        {
            for(let k = 0; k < 10; ++k)
            {
                for(let l = 0; l < 10; ++l)
                {
                    for(let m = 0; m < 10; ++m)
                    {
                        for(let n = 0; n < 10; ++n)
                        {
                            if (i + j + k == l + m + n)
                            {

                                // Counter to count the number
                                // of change required
                                let c = 0;

                                // If first digit is equal
                                if (i != s[0] - '0')
                                    c++;

                                // If 2nd digit is equal
                                if (j != s[1] - '0')
                                    c++;

                                // If 3rd digit is equal
                                if (k != s[2] - '0')
                                    c++;

                                // If 4th digit is equal
                                if (l != s[3] - '0')
                                    c++;

                                // If 5th digit is equal
                                if (m != s[4] - '0')
                                    c++;

                                // If 6th digit is equal
                                if (n != s[5] - '0')
                                    c++;

                                // Checks if less then the
                                // previous calculate changes
                                if (c < ans)
                                    ans = c;
                            }
                        }
                    }
                }
            }
        }
    }

    // Returns the answer
    return ans;
}

// Driver code

// Number stored in string
let s = "123456";

// Prints the minimum operations
document.write(calculate(s));

// This code is contributed by suresh07 

</script>
```

**输出:**

```
2
```

**时间复杂度:**o(10^6)
T3】辅助空间: O(1)

本文由 ***拉贾·维克拉玛迪特亚*** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。