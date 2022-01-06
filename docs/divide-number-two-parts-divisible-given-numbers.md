# 将数字分成可被给定数字整除的两部分

> 原文:[https://www . geesforgeks . org/除数两部分可除数/](https://www.geeksforgeeks.org/divide-number-two-parts-divisible-given-numbers/)

给定一个字符串格式的大数，我们还会得到两个数字 f 和 s。我们需要将大数分成两个连续的部分，这样第一部分可以被 f 整除，第二部分可以被 s 整除。
**示例:**

```
Input: num = “246904096”
          f = 12345        
          s = 1024
Output: Yes
We can divide num into “24680” and “4096” 
which are divisible by f and s respectively.

Input : num = “1234”
          f = 1            
          s = 123
Output : No
We can not divide num into two parts under 
given constraint.
```

一个简单的解决方案是生成给定数的所有除法，并检查一个除法是否可以被整除。
我们可以通过存储给定字符串的每个前缀和后缀的余数来解决这个问题，如果在任何索引处，前缀提醒和后缀提醒都为零，那么我们知道我们可以在这个索引处断开字符串。以上示例
解释了该过程

```
String = “246904096”
All prefix reminders with 12345 are,

Prefix 2     reminder with 12345, 2
prefix 24      reminder with 12345, 24
prefix 246       reminder with 12345, 246
prefix 2469       reminder with 12345, 2469
prefix 24690       reminder with 12345, 0
prefix 246904       reminder with 12345, 4
prefix 2469040   reminder with 12345, 40
prefix 24690409  reminder with 12345, 409
prefix 246904096 reminder with 12345, 4096

All suffix reminder with 1024 are, 
Suffix 6     reminder with 1024, 6
Suffix 96     reminder with 1024, 96
Suffix 096     reminder with 1024, 96
Suffix 4096     reminder with 1024, 0
Suffix 04096     reminder with 1024, 0
Suffix 904096     reminder with 1024, 928
Suffix 6904096     reminder with 1024, 288
Suffix 46904096     reminder with 1024, 800
Suffix 246904096 reminder with 1024, 288
Now we can see that at index 5 both reminders
are 0, so the string can be broken into 24680
and 4096.
```

我们可以将第(I–1)个后缀提醒作为(Sr[I]= Sr[I–1]* 10+s[I])% f 来获取第(I)个后缀提醒，即只需将之前的提醒乘以 10 并加上当前数字，然后将提醒乘以 f 即可。
要将第(I)个前缀提醒作为(i + 1)个前缀提醒，我们可以这样做，(pr[i] = pr[i + 1] + s[i] * base) % s， 也就是说，将下一个提醒和当前数字乘以基础值，最后一个数字为 1，第二个最后一个数字为 10，以此类推，然后我们将按照 s 取提醒。
解的总时间复杂度将**O(N)**T4】

## C++

```
// C++ code to break the number string into
// two divisible parts by given numbers
#include <bits/stdc++.h>
using namespace std;

// method prints divisible parts if possible,
// otherwise prints 'Not possible'
void printTwoDivisibleParts(string num, int f, int s)
{
    int N = num.length();

    // creating arrays to store reminder
    int prefixReminder[N + 1];
    int suffixReminder[N + 1];

    suffixReminder[0] = 0;

    // looping over all suffix and storing
    // reminder with f
    for (int i = 1; i < N; i++)

        // getting suffix reminder from previous
        // suffix reminder
        suffixReminder[i] = (suffixReminder[i - 1] * 10 +
                            (num[i - 1] - '0')) % f;   

    prefixReminder[N] = 0;
    int base = 1;

    // looping over all prefix and storing
    // reminder with s
    for (int i = N - 1; i >= 0; i--) {

        // getting prefix reminder from next
        // prefix reminder
        prefixReminder[i] = (prefixReminder[i + 1] +
                           (num[i] - '0') * base) % s;

        // updating base value
        base = (base * 10) % s;
    }

    // now looping over all reminders to check
    // partition condition
    for (int i = 0; i < N; i++) {

        // if both reminders are 0 and digit itself
        // is not 0, then print result and return
        if (prefixReminder[i] == 0 &&
            suffixReminder[i] == 0 &&
            num[i] != '0') {
            cout << num.substr(0, i) << " "
                 << num.substr(i) << endl;
            return;
        }
    }

    // if we reach here, then string can' be
    // partitioned under constraints
    cout << "Not Possible\n";
}

// Driver code to test above methods
int main()
{
    string num = "246904096";
    int f = 12345;
    int s = 1024;
    printTwoDivisibleParts(num, f, s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to break the number string
// into two divisible parts by given numbers
public class DivisibleParts
{
    // method prints divisible parts if
    // possible, otherwise prints 'Not possible'
    static void printTwoDivisibleParts(String num,
                                     int f, int s)
    {
    int N = num.length();

    // creating arrays to store reminder
    int[] prefixReminder = new int[N + 1];
    int[] suffixReminder = new int[N + 1];

    suffixReminder[0] = 0;

    // looping over all suffix and storing
    // reminder with f
    for (int i = 1; i < N; i++)

        // getting suffix reminder from
        // previous suffix reminder
        suffixReminder[i] = (suffixReminder[i - 1] * 10 +
                        (num.charAt(i - 1) - '0')) % f;

    prefixReminder[N] = 0;
    int base = 1;

    // looping over all prefix and storing
    // reminder with s
    for (int i = N - 1; i >= 0; i--) {

        // getting prefix reminder from next
        // prefix reminder
        prefixReminder[i] = (prefixReminder[i + 1] +
                        (num.charAt(i ) - '0') * base) % s;

        // updating base value
        base = (base * 10) % s;
    }

    // now looping over all reminders to
    // check partition condition
    for (int i = 0; i < N; i++) {

        // if both reminders are 0 and digit
        // itself is not 0, then print result
        // and return
        if (prefixReminder[i] == 0 &&
            suffixReminder[i] == 0 &&
            num.charAt(i ) != '0') {
                System.out.println( num.substring(0, i)
                           +" " + num.substring(i));
            return;
        }
    }

    // if we reach here, then string can' be
    // partitioned under constraints
        System.out.println("Not Possible");

    }

    /* Driver program */
    public static void main(String[] args)
    {
    String num = "246904096";
    int f = 12345;
    int s = 1024;
    printTwoDivisibleParts(num, f, s);
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 code to break the
# number string into two
# divisible parts by given
# numbers

# method prints divisible
# parts if possible, otherwise
# prints 'Not possible'
def printTwoDivisibleParts(num, f, s):
    N = len(num);

    # creating arrays
    # to store reminder
    prefixReminder = [0]*(N + 1);
    suffixReminder = [0]*(N + 1);

    # looping over all
    # suffix and storing
    # reminder with f
    for i in range(1,N):

        # getting suffix
        # reminder from previous
        # suffix reminder
        suffixReminder[i] = (suffixReminder[i - 1] * 10 +
                            (ord(num[i - 1]) -
                                        48)) % f;

    base = 1;

    # looping over all
    # prefix and storing
    # reminder with s
    for i in range(N - 1,-1,-1):

        # getting prefix
        # reminder from next
        # prefix reminder
        prefixReminder[i] = (prefixReminder[i + 1] +
                            (ord(num[i]) - 48) *
                                        base) % s;

        # updating base value
        base = (base * 10) % s;

    # now looping over
    # all reminders to check
    # partition condition
    for i in range(N):

        # if both reminders are
        # 0 and digit itself
        # is not 0, then print
        # result and return
        if (prefixReminder[i] == 0 and suffixReminder[i] == 0 and num[i] != '0'):
            print(num[0:i],num[i:N]);
            return 0;

    # if we reach here, then
    # string can' be partitioned
    # under constraints
    print("Not Possible");

# Driver code
if __name__=='__main__':
    num = "246904096";
    f = 12345;
    s = 1024;
    printTwoDivisibleParts(num,f, s);

# This code is contributed
# by mits
```

## C#

```
// C# program to break the
// number string into two
// divisible parts by given
// numbers
using System;
class GFG
{
// method prints divisible
// parts if possible, otherwise
// prints 'Not possible'
static void printTwoDivisibleParts(String num,
                                   int f, int s)
{
int N = num.Length;

// creating arrays to
// store reminder
int[] prefixReminder = new int[N + 1];
int[] suffixReminder = new int[N + 1];

suffixReminder[0] = 0;

// looping over all
// suffix and storing
// reminder with f
for (int i = 1; i < N; i++)

    // getting suffix reminder from
    // previous suffix reminder
    suffixReminder[i] = (suffixReminder[i - 1] * 10 +
                        (num[i - 1] - '0')) % f;

prefixReminder[N] = 0;
int base1 = 1;

// looping over all
// prefix and storing
// reminder with s
for (int i = N - 1; i >= 0; i--)
{

    // getting prefix reminder
    // from next prefix reminder
    prefixReminder[i] = (prefixReminder[i + 1] +
                    (num[i] - '0') * base1) % s;

    // updating base1 value
    base1 = (base1 * 10) % s;
}

// now looping over all
// reminders to check
// partition condition
for (int i = 0; i < N; i++)
{

    // if both reminders are
    // 0 and digit itself is
    // not 0, then print result
    // and return
    if (prefixReminder[i] == 0 &&
        suffixReminder[i] == 0 &&
        num[i] != '0')
    {
            Console.WriteLine(num.Substring(0, i) +
                            " " + num.Substring(i));
        return;
    }
}

// if we reach here, then
// string can' be partitioned
// under constraints
    Console.WriteLine("Not Possible");

}

// Driver Code
public static void Main()
{
    String num = "246904096";
    int f = 12345;
    int s = 1024;
    printTwoDivisibleParts(num, f, s);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to break the
// number string into two
// divisible parts by given
// numbers

// method prints divisible
// parts if possible, otherwise
// prints 'Not possible'
function printTwoDivisibleParts($num, $f, $s)
{
    $N = strlen($num);

    // creating arrays
    // to store reminder
    $prefixReminder = array_fill(0, $N + 1, 0);
    $suffixReminder = array_fill(0, $N + 1, 0);

    // looping over all
    // suffix and storing
    // reminder with f
    for ($i = 1; $i < $N; $i++)

        // getting suffix
        // reminder from previous
        // suffix reminder
        $suffixReminder[$i] = ($suffixReminder[$i - 1] * 10 +
                              (ord($num[$i - 1]) -
                                        48)) % $f;

    $base = 1;

    // looping over all
    // prefix and storing
    // reminder with s
    for ($i = $N - 1; $i >= 0; $i--)
    {

        // getting prefix
        // reminder from next
        // prefix reminder
        $prefixReminder[$i] = ($prefixReminder[$i + 1] +
                              (ord($num[$i]) - 48) *
                                        $base) % $s;

        // updating base value
        $base = ($base * 10) % $s;
    }

    // now looping over
    // all reminders to check
    // partition condition
    for ($i = 0; $i < $N; $i++)
    {

        // if both reminders are
        // 0 and digit itself
        // is not 0, then print
        // result and return
        if ($prefixReminder[$i] == 0 &&
            $suffixReminder[$i] == 0 &&
            $num[$i] != '0')
        {
            echo substr($num, 0, $i)." ".
                    substr($num,$i)."\n";
            return;
        }
    }

    // if we reach here, then
    // string can' be partitioned
    // under constraints
    echo "Not Possible\n";
}

// Driver code
$num = "246904096";
$f = 12345;
$s = 1024;
printTwoDivisibleParts($num,
                       $f, $s);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>
// javascript program to break the
// number string into two
// divisible parts by given
// numbers

// method prints divisible
// parts if possible, otherwise
// prints 'Not possible'

function printTwoDivisibleParts( num,   f,  s)
{

var N = num.length;

// creating arrays to
// store reminder

var prefixReminder = []
var suffixReminder = []

suffixReminder[0] = 0;

// looping over all
// suffix and storing
// reminder with f

for (var i = 1; i < N; i++)

    // getting suffix reminder from
    // previous suffix reminder

    suffixReminder[i] = (suffixReminder[i - 1] * 10 +  (num[i - 1] - '0')) % f;

prefixReminder[N] = 0;
var base1 = 1;

// looping over all
// prefix and storing
// reminder with s

for (var i = N - 1; i >= 0; i--)
{

    // getting prefix reminder
    // from next prefix reminder
    prefixReminder[i] = (prefixReminder[i + 1] +  (num[i] - '0') * base1) % s;

    // updating base1 value
    base1 = (base1 * 10) % s;
}

// now looping over all
// reminders to check
// partition condition

for (var i = 0; i < N; i++)
{

    // if both reminders are
    // 0 and digit itself is
    // not 0, then print result
    // and return
    if (prefixReminder[i] == 0 && suffixReminder[i] == 0 &&  num[i] != '0')
    {
            document.write(num.substring(0, i) +   " " + num.substring(i));
             return;
    }
}

// if we reach here, then
// string can' be partitioned
// under constraints
    document.write("Not Possible");

}

// Driver Code

    var num = "246904096";
    var f = 12345;
    var s = 1024;
    printTwoDivisibleParts(num, f, s);

// This code is contributed by bunnyram19. 
</script>
```

**输出:**

```
24690 4096
```

**时间复杂度:** O(N)

**辅助空间:** O(N)
本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。