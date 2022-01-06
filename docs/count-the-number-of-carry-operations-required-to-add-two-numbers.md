# 计算两个数相加所需的进位操作次数

> 原文:[https://www . geeksforgeeks . org/count-进位操作的次数-需要添加两个数字/](https://www.geeksforgeeks.org/count-the-number-of-carry-operations-required-to-add-two-numbers/)

给定两个数字，任务是找出两个数字相加时所需的进位操作数，如下所示。

> 1234
> +
> 5678
> —
> 6912
> ——

**例:**

```
Input: n = 1234, k = 5678
Output: 2

4+8 = 2 and carry 1
carry+3+7 = carry 1
carry+2+6 = 9, carry 0
carry+1+5 = 6

Input: n = 555, k = 555
Output: 3
```

**方法:**将 n 和 k 的值存储在字符串中。

1.  将进位变量和计数变量初始化为 0。
2.  现在，从字符串的最后一个索引开始检查，直到两个字符串都结束(一个字符串可能比另一个字符串小)。
3.  在每次迭代中将两个值(注意 ascii 值)和进位相加，并检查总和是否大于 10。
4.  如果大于 10，则简单地将计数值增加 1，并使进位等于 1，否则使进位等于 0。
5.  最后，打印你的答案，这是计数。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// carry operations
int count_carry(string a, string b)
{
    // Initialize the value of carry to 0
    int carry = 0;

    // Counts the number of carry operations
    int count = 0;

    // Initialize len_a and len_b with the sizes of strings
    int len_a = a.length(), len_b = b.length();

    while (len_a != 0 || len_b != 0) {

        // Assigning the ascii value of the character
        int x = 0, y = 0;
        if (len_a > 0) {
            x = a[len_a - 1] - '0';
            len_a--;
        }
        if (len_b > 0) {
            y = b[len_b - 1] - '0';
            len_b--;
        }

        // Add both numbers/digits
        int sum = x + y + carry;

        // If sum > 0, increment count
        // and set carry to 1
        if (sum >= 10) {
            carry = 1;
            count++;
        }

        // Else, set carry to 0
        else
            carry = 0;
    }

    return count;
}

// Driver code
int main()
{

    string a = "9555", b = "555";

    int count = count_carry(a, b);
    if (count == 0)
        cout << "0\n";
    else if (count == 1)
        cout << "1\n";
    else
        cout << count << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of 
// above approach
import java.io.*;

class GFG 
{

// Function to count the number 
// of carry operations
static int count_carry(String a, String b)
{
    // Initialize the value 
    // of carry to 0
    int carry = 0;

    // Counts the number of
    // carry operations
    int count = 0;

    // Initialize len_a and len_b 
    // with the sizes of strings
    int len_a = a.length(),     
        len_b = b.length();

    while (len_a != 0 || len_b != 0) 
    {

        // Assigning the ascii value 
        // of the character
        int x = 0, y = 0;
        if (len_a > 0) 
        {
            x = a.charAt(len_a - 1) - '0';
            len_a--;
        }
        if (len_b > 0) 
        {
            y = b.charAt(len_b - 1) - '0';
            len_b--;
        }

        // Add both numbers/digits
        int sum = x + y + carry;

        // If sum > 0, increment count
        // and set carry to 1
        if (sum >= 10) 
        {
            carry = 1;
            count++;
        }

        // Else, set carry to 0
        else
            carry = 0;
    }

    return count;
}

// Driver code
public static void main (String[] args)
{
    String a = "9555", b = "555";
    int count = count_carry(a, b);
    if (count == 0)
        System.out.println("0\n");
    else if (count == 1)
        System.out.println("1\n");
    else
        System.out.println(count);
}
}

// This code is contributed by Shashank
```

## 蟒蛇 3

```
# Python3 implementation of 
# above approach 

# Function to count the number 
# of carry operations 
def count_carry(a, b):

    # Initialize the value of 
    # carry to 0 
    carry = 0; 

    # Counts the number of carry
    # operations 
    count = 0; 

    # Initialize len_a and len_b
    # with the sizes of strings 
    len_a = len(a);
    len_b = len(b); 

    while (len_a != 0 or len_b != 0):

        # Assigning the ascii value
        # of the character 
        x = 0;
        y = 0; 
        if (len_a > 0): 
            x = int(a[len_a - 1]) + int('0'); 
            len_a -= 1; 

        if (len_b > 0):
            y = int(b[len_b - 1]) + int('0'); 
            len_b -= 1; 

        # Add both numbers/digits 
        sum = x + y + carry; 

        # If sum > 0, increment count 
        # and set carry to 1 
        if (sum >= 10):
            carry = 1; 
            count += 1; 

        # Else, set carry to 0 
        else:
            carry = 0; 

    return count; 

# Driver code 
a = "9555";
b = "555"; 

count = count_carry(a, b); 
if (count == 0): 
    print("0"); 
elif (count == 1): 
    print("1"); 
else:
    print(count); 

# This code is contributed by mits
```

## C#

```
// C# implementation of 
// above approach
using System; 

class GFG 
{

// Function to count the number 
// of carry operations
static int count_carry(string a, string b)
{
    // Initialize the value 
    // of carry to 0
    int carry = 0;

    // Counts the number of
    // carry operations
    int count = 0;

    // Initialize len_a and len_b 
    // with the sizes of strings
    int len_a = a.Length,     
        len_b = b.Length;

    while (len_a != 0 || len_b != 0) 
    {

        // Assigning the ascii value 
        // of the character
        int x = 0, y = 0;
        if (len_a > 0) 
        {
            x = a[len_a - 1] - '0';
            len_a--;
        }
        if (len_b > 0) 
        {
            y = b[len_b - 1] - '0';
            len_b--;
        }

        // Add both numbers/digits
        int sum = x + y + carry;

        // If sum > 0, increment count
        // and set carry to 1
        if (sum >= 10) 
        {
            carry = 1;
            count++;
        }

        // Else, set carry to 0
        else
            carry = 0;
    }

    return count;
}

// Driver code
public static void Main ()
{
    string a = "9555", b = "555";
    int count = count_carry(a, b);
    if (count == 0)
        Console.Write("0\n");
    else if (count == 1)
        Console.Write("1\n");
    else
        Console.Write(count);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach 

// Function to count the number  
// of carry operations 
function count_carry($a, $b) 
{ 
    // Initialize the value of 
    // carry to 0 
    $carry = 0; 

    // Counts the number of carry
    // operations 
    $count = 0; 

    // Initialize len_a and len_b
    // with the sizes of strings 
    $len_a = strlen($a);
    $len_b = strlen($b); 

    while ($len_a != 0 || $len_b != 0)
    { 

        // Assigning the ascii value
        // of the character 
        $x = 0;
        $y = 0; 
        if ($len_a > 0) 
        { 
            $x = $a[$len_a - 1] - '0'; 
            $len_a--; 
        } 
        if ($len_b > 0) 
        { 
            $y = $b[$len_b - 1] - '0'; 
            $len_b--; 
        } 

        // Add both numbers/digits 
        $sum = $x + $y + $carry; 

        // If sum > 0, increment count 
        // and set carry to 1 
        if ($sum >= 10)
        { 
            $carry = 1; 
            $count++; 
        } 

        // Else, set carry to 0 
        else
            $carry = 0; 
    } 

    return $count; 
} 

// Driver code 
$a = "9555";
$b = "555"; 

$count = count_carry($a, $b); 
if ($count == 0) 
    echo "0\n"; 
else if ($count == 1) 
    echo "1\n"; 
else
    echo $count , "\n"; 

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function to count the number 
    // of carry operations
    function count_carry(a, b)
    {
        // Initialize the value 
        // of carry to 0
        let carry = 0;

        // Counts the number of
        // carry operations
        let count = 0;

        // Initialize len_a and len_b 
        // with the sizes of strings
        let len_a = a.length, len_b = b.length;

        while (len_a != 0 || len_b != 0) 
        {

            // Assigning the ascii value 
            // of the character
            let x = 0, y = 0;
            if (len_a > 0) 
            {
                x = a[len_a - 1] - '0';
                len_a--;
            }
            if (len_b > 0) 
            {
                y = b[len_b - 1] - '0';
                len_b--;
            }

            // Add both numbers/digits
            let sum = x + y + carry;

            // If sum > 0, increment count
            // and set carry to 1
            if (sum >= 10) 
            {
                carry = 1;
                count++;
            }

            // Else, set carry to 0
            else
                carry = 0;
        }

        return count;
    }

    let a = "9555", b = "555";
    let count = count_carry(a, b);
    if (count == 0)
        document.write("0" + "</br>");
    else if (count == 1)
        document.write("1" + "</br>");
    else
        document.write(count);

</script>
```

**Output:** 

```
4
```