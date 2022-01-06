# 计算给定数字序列的可能解码数

> 原文:[https://www . geeksforgeeks . org/count-可能-decodings-给定-数字-序列/](https://www.geeksforgeeks.org/count-possible-decodings-given-digit-sequence/)

让 1 代表‘A’，2 代表‘B’等。给定一个数字序列，计算给定数字序列的可能解码次数。

**示例:**

```
Input:  digits[] = "121"
Output: 3
// The possible decodings are "ABA", "AU", "LA"

Input: digits[] = "1234"
Output: 3
// The possible decodings are "ABCD", "LCD", "AWD"
```

一个空的数字序列被认为有一个解码。可以假设输入包含从 0 到 9 的有效数字，并且没有前导 0，没有额外的尾随 0，也没有两个或更多连续 0。

这个问题是递归的，可以分解为子问题。我们从给定数字序列的末尾开始。我们将解码总数初始化为 0。我们重复两个子问题。
1)如果最后一个数字不为零，对剩余的(n-1)个数字重复，并将结果加到总计数中。
2)如果最后两位数字构成有效字符(或小于 27)，对剩余的(n-2)位重复，并将结果加到总数中。

下面是上述方法的实现。

## C++

```
// C++ implementation to count number of
// decodings that can be formed from a
// given digit sequence
#include <cstring>
#include <iostream>
using namespace std;

// recuring function to find
// ways in how many ways a
// string can be decoded of length
// greater than 0 and starting with
// digit 1 and greater.
int countDecoding(char* digits, int n)
{
    // base cases
    if (n == 0 || n == 1)
        return 1;
    if (digits[0] == '0')
        return 0;

    // for base condition "01123" should return 0
    // Initialize count
    int count = 0;

    // If the last digit is not 0,
    // then last digit must add
    // to the number of words
    if (digits[n - 1] > '0')
        count = countDecoding(digits, n - 1);

    // If the last two digits form a number smaller
    // than or equal to 26, then consider
    // last two digits and recur
    if (digits[n - 2] == '1'
        || (digits[n - 2] == '2'
        && digits[n - 1] < '7'))
        count += countDecoding(digits, n - 2);

    return count;
}

// Given a digit sequence of length n,
// returns count of possible decodings by
// replacing 1 with A, 2 with B, ... 26 with Z
int countWays(char* digits, int n)
{
    if (n == 0 || (n == 1 && digits[0] == '0'))
        return 0;
    return countDecoding(digits, n);
}

// Driver code
int main()
{
    char digits[] = "1234";
    int n = strlen(digits);
    cout << "Count is " << countWays(digits, n);
    return 0;
}
// Modified by Atanu Sen
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A naive recursive Java implementation
// to count number of decodings that
// can be formed from a given digit sequence

class GFG {

    // recuring function to find
    // ways in how many ways a
    // string can be decoded of length
    // greater than 0 and starting with
    // digit 1 and greater.
    static int countDecoding(char[] digits, int n)
    {
        // base cases
        if (n == 0 || n == 1)
            return 1;

        // for base condition "01123" should return 0
        if (digits[0] == '0')
            return 0;

        // Initialize count
        int count = 0;

        // If the last digit is not 0, then
        // last digit must add to
        // the number of words
        if (digits[n - 1] > '0')
            count = countDecoding(digits, n - 1);

        // If the last two digits form a number
        // smaller than or equal to 26,
        // then consider last two digits and recur
        if (digits[n - 2] == '1'
            || (digits[n - 2] == '2'
                && digits[n - 1] < '7'))
            count += countDecoding(digits, n - 2);

        return count;
    }

    // Given a digit sequence of length n,
    // returns count of possible decodings by
    // replacing 1 with A, 2 with B, ... 26 with Z
    static int countWays(char[] digits, int n)
    {
        if (n == 0 || (n == 1 && digits[0] == '0'))
            return 0;
        return countDecoding(digits, n);
    }

    // Driver code
    public static void main(String[] args)
    {
        char digits[] = { '1', '2', '3', '4' };
        int n = digits.length;
        System.out.printf("Count is %d",
                          countWays(digits, n));
    }
}

// This code is contributed by Smitha Dinesh Semwal.
// Modified by Atanu Sen
```

## 蟒蛇 3

```
# Recursive implementation of numDecodings
def numDecodings(s: str) -> int:
    if len(s) == 0
    or (len(s) == 1
        and s[0] == '0'):
        return 0
    return numDecodingsHelper(s, len(s))

def numDecodingsHelper(s: str, n: int) -> int:
    if n == 0 or n == 1:
        return 1
    count = 0
    if s[n-1] > "0":
        count = numDecodingsHelper(s, n-1)
    if (s[n - 2] == '1'
        or (s[n - 2] == '2'
            and s[n - 1] < '7')):
        count += numDecodingsHelper(s, n - 2)
    return count

# Driver code
digits = "1234"
print("Count is ", numDecodings(digits))
# This code is contributed by Frank Hu
```

## C#

```
// A naive recursive C# implementation
// to count number of decodings that
// can be formed from a given digit sequence
using System;

class GFG {

    // recuring function to find
    // ways in how many ways a
    // string can be decoded of length
    // greater than 0 and starting with
    // digit 1 and greater.
    static int countDecoding(char[] digits, int n)
    {

        // base cases
        if (n == 0 || n == 1)
            return 1;

        // Initialize count
        int count = 0;

        // If the last digit is not 0, then
        // last digit must add to
        // the number of words
        if (digits[n - 1] > '0')
            count = countDecoding(digits, n - 1);

        // If the last two digits form a number
        // smaller than or equal to 26, then
        // consider last two digits and recur
        if (digits[n - 2] == '1'
            || (digits[n - 2] == '2'
                && digits[n - 1] < '7'))
            count += countDecoding(digits, n - 2);

        return count;
    }

    // Given a digit sequence of length n,
    // returns count of possible decodings by
    // replacing 1 with A, 2 with B, ... 26 with Z
    static int countWays(char[] digits, int n)
    {
        if (n == 0 || (n == 1 && digits[0] == '0'))
            return 0;
        return countDecoding(digits, n);
    }

    // Driver code
    public static void Main()
    {
        char[] digits = { '1', '2', '3', '4' };
        int n = digits.Length;
        Console.Write("Count is ");
        Console.Write(countWays(digits, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A naive recursive PHP implementation
// to count number of decodings that can
// be formed from a given digit sequence

//recuring function to find
//ways in how many ways a
//string can be decoded of length
//greater than 0 and starting with
//digit 1 and greater.
function countDecoding(&$digits, $n)
{
    // base cases
    if ($n == 0 || $n == 1)
        return 1;

    $count = 0; // Initialize count

    // If the last digit is not 0, then last
    // digit must add to the number of words
    if ($digits[$n - 1] > '0')
        $count = countDecoding($digits, $n - 1);

    // If the last two digits form a number
    // smaller than or equal to 26, then
    // consider last two digits and recur
    if ($digits[$n - 2] == '1' ||
       ($digits[$n - 2] == '2' &&
        $digits[$n - 1] < '7') )
        $count += countDecoding($digits, $n - 2);

    return $count;
}

// Given a digit sequence of length n,
// returns count of possible decodings by
// replacing 1 with A, 2 with B, ... 26 with Z
function countWays(&$digits, $n){
  if($n==0 || ($n == 1 && $digits[0] == '0'))
     return 0;
  return countDecoding($digits, $n);
}

// Driver Code
$digits = "1234";
$n = strlen($digits);
echo "Count is " . countWays($digits, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// A naive recursive JavaScript implementation
// to count number of decodings that
// can be formed from a given digit sequence   

    // recuring function to find
    // ways in how many ways a
    // string can be decoded of length
    // greater than 0 and starting with
    // digit 1 and greater.
    function countDecoding(digits, n)
    {
        // base cases
        if (n == 0 || n == 1)
        {
            return 1;
        }
        // for base condition "01123" should return 0
        if (digits[0] == '0')
        {
            return 0;
        }

        // Initialize count
        let count = 0;

        // If the last digit is not 0, then
        // last digit must add to
        // the number of words
        if (digits[n - 1] > '0')
        {
            count = countDecoding(digits, n - 1);
        }
        // If the last two digits form a number
        // smaller than or equal to 26,
        // then consider last two digits and recur
        if (digits[n - 2] == '1'
            || (digits[n - 2] == '2'
                && digits[n - 1] < '7'))
        {
            count += countDecoding(digits, n - 2);
        }
        return count;
    }
    // Given a digit sequence of length n,
    // returns count of possible decodings by
    // replacing 1 with A, 2 with B, ... 26 with Z
    function countWays(digits, n)
    {
        if (n == 0 || (n == 1 && digits[0] == '0'))
        {
            return 0;
        }
        return countDecoding(digits, n);
    }

    // Driver code
    digits=['1', '2', '3', '4'];
    let n = digits.length;
    document.write("Count is ",countWays(digits, n));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Count is 3
```

上述代码的时间复杂度是指数级的。如果我们仔细看一下上面的程序，可以观察到递归解类似于[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。因此，我们可以使用[动态规划](https://www.geeksforgeeks.org/tag/dynamic-programming/)优化上述解决方案，使其在 O(n)时间内工作。

下面是相同的实现。

## C++

```
// A Dynamic Programming based C++
// implementation to count decodings
#include <iostream>
#include <cstring>
using namespace std;

// A Dynamic Programming based function
// to count decodings
int countDecodingDP(char *digits, int n)
{
    // A table to store results of subproblems
    int count[n+1];
    count[0] = 1;
    count[1] = 1;
    //for base condition "01123" should return 0
    if(digits[0]=='0') 
         return 0;
    for (int i = 2; i <= n; i++)
    {
        count[i] = 0;

        // If the last digit is not 0,
        // then last digit must add to the number of words
        if (digits[i-1] > '0')
            count[i] = count[i-1];

        // If second last digit is smaller
        // than 2 and last digit is smaller than 7,
        // then last two digits form a valid character
        if (digits[i-2] == '1' ||
              (digits[i-2] == '2' && digits[i-1] < '7') )
            count[i] += count[i-2];
    }
    return count[n];
}

// Driver program to test above function
int main()
{
    char digits[] = "1234";
    int n = strlen(digits);
    cout << "Count is " << countDecodingDP(digits, n);
    return 0;
}
// Modified by Atanu Sen
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based Java
// implementation to count decodings
import java.io.*;

class GFG
{

// A Dynamic Programming based
// function to count decodings
static int countDecodingDP(char digits[],
                           int n)
{
    // A table to store results of subproblems
    int count[] = new int[n + 1];
    count[0] = 1;
    count[1] = 1;
    if(digits[0]=='0')   //for base condition "01123" should return 0
          return 0;
    for (int i = 2; i <= n; i++)
    {
        count[i] = 0;

        // If the last digit is not 0,
        // then last digit must add to
        // the number of words
        if (digits[i - 1] > '0')
            count[i] = count[i - 1];

        // If second last digit is smaller
        // than 2 and last digit is smaller
        // than 7, then last two digits
        // form a valid character
        if (digits[i - 2] == '1' ||
           (digits[i - 2] == '2' &&
            digits[i - 1] < '7'))
            count[i] += count[i - 2];
    }
    return count[n];
}

// Driver Code
public static void main (String[] args)
{
    char digits[] = {'1','2','3','4'};
    int n = digits.length;
    System.out.println("Count is " +
               countDecodingDP(digits, n));
}
}

// This code is contributed by anuj_67
// Modified by Atanu Sen
```

## 蟒蛇 3

```
# A Dynamic Programming based Python3
# implementation to count decodings

# A Dynamic Programming based function
# to count decodings
def countDecodingDP(digits, n):

    count = [0] * (n + 1); # A table to store
                           # results of subproblems
    count[0] = 1;
    count[1] = 1;

    for i in range(2, n + 1):

        count[i] = 0;

        # If the last digit is not 0, then last
        # digit must add to the number of words
        if (digits[i - 1] > '0'):
            count[i] = count[i - 1];

        # If second last digit is smaller than 2
        # and last digit is smaller than 7, then
        # last two digits form a valid character
        if (digits[i - 2] == '1' or
           (digits[i - 2] == '2' and
            digits[i - 1] < '7') ):
            count[i] += count[i - 2];

    return count[n];

# Driver Code
digits = "1234";
n = len(digits);
print("Count is" ,
       countDecodingDP(digits, n));

# This code is contributed by mits
```

## C#

```
// A Dynamic Programming based C#
// implementation to count decodings
using System;

class GFG
{

// A Dynamic Programming based
// function to count decodings
static int countDecodingDP(char[] digits,
                           int n)
{
    // A table to store results of subproblems
    int[] count = new int[n + 1];
    count[0] = 1;
    count[1] = 1;

    for (int i = 2; i <= n; i++)
    {
        count[i] = 0;

        // If the last digit is not 0,
        // then last digit must add to
        // the number of words
        if (digits[i - 1] > '0')
            count[i] = count[i - 1];

        // If second last digit is smaller
        // than 2 and last digit is smaller
        // than 7, then last two digits
        // form a valid character
        if (digits[i - 2] == '1' ||
           (digits[i - 2] == '2' &&
            digits[i - 1] < '7'))
            count[i] += count[i - 2];
    }
    return count[n];
}

// Driver Code
public static void Main()
{
    char[] digits = {'1','2','3','4'};
    int n = digits.Length;
    Console.WriteLine("Count is " +
            countDecodingDP(digits, n));
}
}

// This code is contributed
// by Akanksha Rai
// Modified by Atanu Sen
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based
// php implementation to count decodings

// A Dynamic Programming based function to count decodings
function countDecodingDP($digits, $n)
{
    // A table to store results of subproblems
    $count[$n+1]=array();
    $count[0] = 1;
    $count[1] = 1;

    for ($i = 2; $i <= $n; $i++)
    {
        $count[$i] = 0;

        // If the last digit is not 0, then last digit must add to
        // the number of words
        if ($digits[$i-1] > '0')
            $count[$i] = $count[$i-1];

        // If second last digit is smaller than 2 and last digit is
        // smaller than 7, then last two digits form a valid character
        if ($digits[$i-2] == '1' || ($digits[$i-2] == '2' && $digits[$i-1] < '7') )
            $count[$i] += $count[$i-2];
    }
    return $count[$n];
}

// Driver program to test above function
    $digits = "1234";
    $n = strlen($digits);
    echo  "Count is " , countDecodingDP($digits, $n);

#This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// A Dynamic Programming based Javascript
// implementation to count decodings

// A Dynamic Programming based
// function to count decodings
function countDecodingDP(digits, n)
{

    // A table to store results of subproblems
    let count = new Array(n + 1);
    count[0] = 1;
    count[1] = 1;

    // For base condition "01123" should return 0
    if (digits[0] == '0')  
          return 0;

    for(let i = 2; i <= n; i++)
    {
        count[i] = 0;

        // If the last digit is not 0,
        // then last digit must add to
        // the number of words
        if (digits[i - 1] > '0')
            count[i] = count[i - 1];

        // If second last digit is smaller
        // than 2 and last digit is smaller
        // than 7, then last two digits
        // form a valid character
        if (digits[i - 2] == '1' ||
           (digits[i - 2] == '2' &&
            digits[i - 1] < '7'))
            count[i] += count[i - 2];
    }
    return count[n];
}

// Driver Code
let digits = [ '1','2','3','4' ];
let n = digits.length;

document.write("Count is " +
               countDecodingDP(digits, n));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Count is 3
```

上述解决方案的时间复杂度为 O(n)，需要 O(n)个辅助空间。我们可以通过使用[斐波那契数帖](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)中讨论的空间优化版本，将辅助空间减少到 O(1)。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息