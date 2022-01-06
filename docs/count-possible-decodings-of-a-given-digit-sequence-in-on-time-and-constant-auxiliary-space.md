# 计算给定数字序列在 O(N)时间和恒定辅助空间内的可能解码次数

> 原文:[https://www . geeksforgeeks . org/给定时间常数辅助空间中给定数字序列的可能解码数/](https://www.geeksforgeeks.org/count-possible-decodings-of-a-given-digit-sequence-in-on-time-and-constant-auxiliary-space/)

给定一个数字序列 **S** ，任务是找到给定数字序列的可能解码数，其中 1 代表‘A’，2 代表‘B’……以此类推，直到 26，其中 26 代表‘Z’。

**示例:**

> **输入:** S = "121"
> **输出:** 3
> 可能的解码是“ABA”、“AU”、“LA”
> 
> **输入:**S = " 1234 "
> T3】输出: 3
> 可能的解码是“ABCD”、“LCD”、“AWD”

**方法:**为了解决 O(N)时间复杂度的这个问题，使用了[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。并且为了将辅助空间复杂度降低到 O(1)，我们使用了在[斐波那契数帖](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)中讨论的递归关系的空间优化版本。
与斐波那契数类似，任何当前第 i <sup>个</sup>指数的关键观测值都可以使用其前两个指数来计算。因此计算第 i <sup>个</sup>指标的[递推关系](https://www.geeksforgeeks.org/different-types-recurrence-relations-solutions/)可以表示为

```
// Condition to check last
// digit can be included or not
if (digit[i-1] is not '0')
     count[i] += count[i-1]

// Condition to check the last
// two digits contribution
if (digit[i-2] is 1 or 
   (digit[i-2] is 2 and 
    digit[i-1] is less than 7))
     count[i] += count[i-2]
```

下面是上述方法的实现:

## C++

```
// C++ implementation to count decodings

#include <bits/stdc++.h>
using namespace std;

// A Dynamic Programming based function
// to count decodings in digit sequence
int countDecodingDP(string digits, int n)
{
    // For base condition "01123"
    // should return 0
    if (digits[0] == '0')
        return 0;

    int count0 = 1, count1 = 1, count2;

    // Using last two calculated values,
    // calculate for ith index
    for (int i = 2; i <= n; i++) {
        count2 = ((int)(digits[i - 1] != '0') *  count1) +
                  (int)((digits[i - 2] == '1') or
                  (digits[i - 2] == '2' and
                   digits[i - 1] < '7')) * count0;
        count0 = count1;
        count1 = count2;
    }

    // Return the required answer
    return count1;
}

// Driver Code
int main()
{
    string digits = "1234";
    int n = digits.size();

    // Function call
    cout << countDecodingDP(digits, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count decodings
class GFG{

// A Dynamic programming based function
// to count decodings in digit sequence
static int countDecodingDP(String digits, int n)
{

    // For base condition "01123"
    // should return 0
    if (digits.charAt(0) == '0')
    {
        return 0;
    }

    int count0 = 1, count1 = 1, count2;

    // Using last two calculated values,
    // calculate for ith index
    for(int i = 2; i <= n; i++)
    {
        int dig1 = 0, dig2, dig3 = 0;

        // Change boolean to int
        if(digits.charAt(i - 1) != '0')
        {
            dig1 = 1;
        }
        if(digits.charAt(i - 2) == '1')
        {
            dig2 = 1;
        }
        else
            dig2 = 0;

        if(digits.charAt(i - 2) == '2' &&
           digits.charAt(i - 1) < '7')
        {
            dig3 = 1;
        }
        count2 = dig1 * count1 +
                 dig2 + dig3 * count0;

        count0 = count1;
        count1 = count2;
    }

    // Return the required answer
    return count1;
}

// Driver Code
public static void main(String[] args)
{
    String digits = "1234";
    int n = digits.length();

    // Function call
    System.out.print(countDecodingDP(digits, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation
# to count decodings

# A Dynamic programming based
# function to count decodings
# in digit sequence
def countDecodingDP(digits, n):

    # For base condition "01123"
    # should return 0
    if (digits[0] == '0'):
        return 0;   

    count0 = 1; count1 = 1;

    # Using last two calculated values,
    # calculate for ith index
    for i in range(2, n + 1):
        dig1 = 0; dig3 = 0;

        # Change boolean to int
        if (digits[i-1] != '0'):
            dig1 = 1;

        if (digits[i - 2] == '1'):
            dig2 = 1;
        else:
            dig2 = 0;

        if (digits[i - 2] == '2' and
            digits[i-1] < '7'):
            dig3 = 1;

        count2 = dig1 * count1 +
                 dig2 + dig3 * count0;

        count0 = count1;
        count1 = count2;   

    # Return the required answer
    return count1;

# Driver Code
if __name__ == '__main__':
    digits = "1234";
    n = len(digits);

    # Function call
    print(countDecodingDP(digits, n));

# This code is contributed by gauravrajput1
```

## C#

```
// C# implementation to count decodings
using System;

class GFG{

// A Dynamic programming based function
// to count decodings in digit sequence
static int countDecodingDP(String digits, int n)
{

    // For base condition "01123"
    // should return 0
    if (digits[0] == '0')
    {
        return 0;
    }

    int count0 = 1, count1 = 1, count2;

    // Using last two calculated values,
    // calculate for ith index
    for(int i = 2; i <= n; i++)
    {
        int dig1 = 0, dig2, dig3 = 0;

        // Change bool to int
        if(digits[i - 1] != '0')
        {
            dig1 = 1;
        }
        if(digits[i - 2] == '1')
        {
            dig2 = 1;
        }
        else
            dig2 = 0;

        if(digits[i - 2] == '2' &&
           digits[i - 1] < '7')
        {
            dig3 = 1;
        }
        count2 = dig1 * count1 +
                 dig2 + dig3 * count0;

        count0 = count1;
        count1 = count2;
    }

    // Return the required answer
    return count1;
}

// Driver Code
public static void Main(String[] args)
{
    String digits = "1234";
    int n = digits.Length;

    // Function call
    Console.Write(countDecodingDP(digits, n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to count decodings

// A Dynamic Programming based function
// to count decodings in digit sequence
function countDecodingDP(digits, n)
{
    // For base condition "01123"
    // should return 0
    if (digits[0] == '0')
        return 0;

    var count0 = 1, count1 = 1, count2;

    // Using last two calculated values,
    // calculate for ith index
    for (var i = 2; i <= n; i++) {
        count2 = ((digits[i - 1] != '0') *  count1) +
                  ((digits[i - 2] == '1') ||
                  (digits[i - 2] == '2' &&
                   digits[i - 1] < '7')) * count0;
        count0 = count1;
        count1 = count2;
    }

    // Return the required answer
    return count1;
}

// Driver Code
var digits = "1234";
var n = digits.length;
// Function call
document.write( countDecodingDP(digits, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】辅助空间复杂度: O(1)
**相关文章:** [计算给定数字序列的可能解码次数](https://www.geeksforgeeks.org/count-possible-decodings-given-digit-sequence/)