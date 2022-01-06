# 按照排序顺序找到所有可能的字符映射

> 原文:[https://www . geeksforgeeks . org/find-所有可能的字符排序顺序映射/](https://www.geeksforgeeks.org/find-all-the-possible-mappings-of-characters-in-a-sorted-order/)

给定一个数字，按排序顺序找出所有可能的字符映射。
**例:**

```
Input: 123
Output: ABC
         AW
         LC
Explanation:  
1 = A; 2 = B; 3 = C; 12 = L; 23 = W 

                 {1, 2, 3}                          
                /        \                          
               /          \                         
       "A"{2, 3}           "L"{3}                      
           /      \          /   \                  
          /        \        /     \
        "AB"{3}  "A"{23}  "LC"    null
        /  \        /  \
       /    \      /    \
      "ABC" null  "AW"  null 

Input : 2122
Output : BABB
         BAV
         BLB
         UBB
         UV
```

**进场:**

1.  创建了一个递归函数，该函数接受一个包含以字符形式存储的数字的输入字符数组、一个输出字符数组和两个可用于遍历这两个数组的变量(比如 I 和 j)。
2.  使用递归，获得输入数组中第 i <sup>个</sup>数字的字符，并将与该数字对应的映射字符存储在输出数组中的第 j <sup>个</sup>索引处。
3.  将有两次递归调用。第一次呼叫每次处理一个位数，而第二次呼叫每次处理两个位数。
4.  一次处理两位数时，数字应该始终小于 26，因为组合后，相应的字符必须位于 A 到 z 之间。
5.  最后，在基本情况下，当整个输入字符串被处理后，输出数组被打印出来。

下面是上述方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find all the possible
// string mappings of a given number
// in a sorted order
#include <bits/stdc++.h>
using namespace std;

// Function to find the string mappings
void mapped(char inputarr[], char outputarr[],
            int i, int j)
{

    // Base case
    if (inputarr[i] == '\0') {
        outputarr[j] = '\0';
        cout << outputarr << endl;
        return;
    }

    // Convert the character to integer
    int digit = inputarr[i] - '0';

    // To store the characters corresponding
    // to the digits which are further
    // stored in outputarr[]
    char ch = digit + 'A' - 1;
    outputarr[j] = ch;

    // First recursive call taking one digit at a time
    mapped(inputarr, outputarr, i + 1, j + 1);

    if (inputarr[i + 1] != '\0') {
        int second_digit = inputarr[i + 1] - '0';
        int number = digit * 10 + second_digit;

        if (number <= 26) {
            ch = number + 'A' - 1;
            outputarr[j] = ch;

            // Second recursive call processing
            // two digits at a time
            mapped(inputarr, outputarr, i + 2, j + 1);
        }
    }
}

// Driver code
int main()
{
    char inputarr[] = { '1', '2', '3' };
    int m = pow(2, 3) - 1;
    int n = sizeof(m) / sizeof(int);
    char outputarr[n];

    mapped(inputarr, outputarr, 0, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all the possible
// string mappings of a given number
// in a sorted order

class GFG
{

    // Function to find the string mappings
    static void mapped(char inputarr[], char outputarr[],
                        int i, int j)
    {

        // Base case
        if (i >= inputarr.length)
        {
            String str = new String(outputarr);
            System.out.println(str.substring(0, j));
            return;
        }

        // Convert the character to integer
        int digit = inputarr[i] - '0';

        // To store the characters corresponding
        // to the digits which are further
        // stored in outputarr[]
        char ch = (char)(digit + (int)('A') - 1);
        outputarr[j] = ch;

        // First recursive call taking one digit at a time
        mapped(inputarr, outputarr, i + 1, j + 1);

        if (i + 1 < inputarr.length)
        {
            int second_digit = inputarr[i + 1] - '0';
            int number = digit * 10 + second_digit;

            if (number <= 26)
            {
                ch = (char)(number + (int)'A' - 1);
                outputarr[j] = ch;

                // Second recursive call processing
                // two digits at a time
                mapped(inputarr, outputarr, i + 2, j + 1);
            }
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        char inputarr[] = { '1', '2', '3' };
        int m = (int)Math.pow(2, 3) - 1;
        int n = 1;
        char outputarr[] = new char[m];

        mapped(inputarr, outputarr, 0, 0);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find all the possible
# string mappings of a given number
# in a sorted order

# Function to find the string mappings
def mapped(inputarr, outputarr, i, j):

    # Base case
    if (i == len(inputarr)):
        print("".join(outputarr[:j]))
        return

    # Convert the character to integer
    digit = ord(inputarr[i]) - ord('0')

    # To store the characters corresponding
    # to the digits which are further
    # stored in outputarr[]
    ch = digit + ord('A') - 1
    outputarr[j] = chr(ch)

    # First recursive call taking one digit at a time
    mapped(inputarr, outputarr, i + 1, j + 1)

    if (i + 1 < len(inputarr) and [i + 1] != '\0'):
        second_digit = ord(inputarr[i + 1]) - ord('0')
        number = digit * 10 + second_digit

        if (number <= 26):
            ch = number + ord('A') - 1
            outputarr[j] = chr(ch)

            # Second recursive call processing
            # two digits at a time
            mapped(inputarr, outputarr, i + 2, j + 1)

# Driver code
inputarr = ['1', '2', '3']
m = pow(2, 3) - 1
n = 1
outputarr = ['0'] * m

mapped(inputarr, outputarr, 0, 0)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find all the possible
// string mappings of a given number
// in a sorted order
using System;

class GFG
{

    // Function to find the string mappings
    static void mapped(char []inputarr, char []outputarr,
                        int i, int j)
    {

        // Base case
        if (i >= inputarr.Length)
        {
            string str = new string(outputarr);
            Console.WriteLine(str.Substring(0, j));
            return;
        }

        // Convert the character to integer
        int digit = inputarr[i] - '0';

        // To store the characters corresponding
        // to the digits which are further
        // stored in outputarr[]
        char ch = (char)(digit + (int)('A') - 1);
        outputarr[j] = ch;

        // First recursive call taking one digit at a time
        mapped(inputarr, outputarr, i + 1, j + 1);

        if (i + 1 < inputarr.Length)
        {
            int second_digit = inputarr[i + 1] - '0';
            int number = digit * 10 + second_digit;

            if (number <= 26)
            {
                ch = (char)(number + (int)'A' - 1);
                outputarr[j] = ch;

                // Second recursive call processing
                // two digits at a time
                mapped(inputarr, outputarr, i + 2, j + 1);
            }
        }
    }

    // Driver code
    public static void Main ()
    {
        char []inputarr = { '1', '2', '3' };
        int m = (int)Math.Pow(2, 3) - 1;
        int n = 1;
        char []outputarr = new char[m];

        mapped(inputarr, outputarr, 0, 0);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to find all the possible
// string mappings of a given number
// in a sorted order

 // Function to find the string mappings
function mapped(inputarr,outputarr,i,j)
{
    // Base case
        if (i >= inputarr.length)
        {
            let str = (outputarr).join("");
            document.write(str.substring(0, j)+"<br>");
            return;
        }

        // Convert the character to integer
        let digit = inputarr[i].charCodeAt(0) -
        '0'.charCodeAt(0);

        // To store the characters corresponding
        // to the digits which are further
        // stored in outputarr[]
        let ch =
        String.fromCharCode(digit + ('A').charCodeAt(0) - 1);
        outputarr[j] = ch;

        // First recursive call taking one digit at a time
        mapped(inputarr, outputarr, i + 1, j + 1);

        if (i + 1 < inputarr.length)
        {
            let second_digit = inputarr[i + 1].charCodeAt(0) -
            '0'.charCodeAt(0);
            let number = digit * 10 + second_digit;

            if (number <= 26)
            {
                ch =
                String.fromCharCode(number + 'A'.charCodeAt(0) - 1);
                outputarr[j] = ch;

                // Second recursive call processing
                // two digits at a time
                mapped(inputarr, outputarr, i + 2, j + 1);
            }
        }
}
// Driver code
let inputarr=['1', '2', '3'];
let m = Math.pow(2, 3) - 1;
let n = 1;
let outputarr = new Array(m);
 mapped(inputarr, outputarr, 0, 0);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
ABC
AW
LC
```