# 通过只翻转一组连续的 0

来最大化十进制等值

> 原文:[https://www . geeksforgeeks . org/通过仅翻转一组连续的 0 来最大化十进制等值/](https://www.geeksforgeeks.org/maximize-the-decimal-equivalent-by-flipping-only-a-contiguous-set-of-0s/)

给定一个字符串形式的 [**二进制数**](https://www.geeksforgeeks.org/program-binary-decimal-conversion/) ，任务是打印一个二进制等价数，该等价数是通过只翻转一组连续的 0 来获得的，这样这个二进制数的十进制等价数是最大的。
***注意:**不要假设二进制数的开头有任何尾随零，即“0101”表示为“101”。*
**示例:**

> **输入:** s = "10101"
> **输出:** 11101
> **解释:**
> 这里我们只能翻转字符串“10101”(= 21)的第 2 个字符，将它改为“11101”(= 29)。因为我们被允许翻转一个连续的子阵列，任何更多的翻转将导致十进制当量的减少。
> **输入:** s = "1000"
> **输出:** 1111
> **解释:**
> 如果我们从位置 1 到 3 翻转连续字符，我们将得到 1111，这是 4 位中可能的最大数量，即 15。

**方法:**为了解决上面提到的问题，我们知道我们必须增加二进制等价物的值。因此，我们必须**在更高的位置**增加 1 的数量。显然，我们可以通过翻转最初出现的零来增加数字的值。遍历字符串并翻转第一个出现的 0，直到出现 1，在这种情况下，循环必须中断。打印结果字符串。
**以下是上述方法的实施:**

## C++

```
// C++ implementation to Maximize the value of
// the decimal equivalent given in the binary form
#include <bits/stdc++.h>
using namespace std;

// Function to print the binary number
void flip(string& s)
{
    for (int i = 0; i < s.length(); i++) {

        // Check if the current number is 0
        if (s[i] == '0') {

            // Find the continuous 0s
            while (s[i] == '0') {

                // Replace initially
                // occurring 0 with 1
                s[i] = '1';
                i++;
            }

            // Break out of loop if 1 occurs
            break;
        }
    }
}

// Driver code
int main()
{
    string s = "100010001";
    flip(s);

    cout << s;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to maximize the value of
// the decimal equivalent given in the binary form
import java.util.*;

class GFG{

// Function to print the binary number
static void flip(String s)
{
    StringBuilder sb = new StringBuilder(s);
    for(int i = 0; i < sb.length(); i++)
    {

       // Check if the current number is 0
       if (sb.charAt(i) == '0')
       {

           // Find the continuous 0s
           while (sb.charAt(i) == '0')
           {

               // Replace initially
               // occurring 0 with 1
               sb.setCharAt(i, '1');
               i++;
           }

           // Break out of loop if 1 occurs
           break;
       }
    }
    System.out.println(sb.toString());
}

// Driver code
public static void main(String[] args)
{
    String s = "100010001";
    flip(s);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to
# Maximize the value of the
# decimal equivalent given
# in the binary form

# Function to print the binary
# number
def flip(s):
    s = list(s)
    for i in range(len(s)):

        # Check if the current number
        # is 0
        if(s[i] == '0'):

            # Find the continuous 0s
            while(s[i] == '0'):

                # Replace initially
                # occurring 0 with 1
                s[i] = '1'
                i += 1
            s = ''.join(map(str, s))

            # return the string and
            # break the loop
            return s

# Driver code
s = "100010001"
print(flip(s))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation to maximize the value of
// the decimal equivalent given in the binary form
using System;

class GFG{

// Function to print the binary number
static String flip(char []s)
{
    for(int i = 0; i < s.Length; i++)
    {

       // Check if the current number is 0
       if (s[i] == '0')
       {

           // Find the continuous 0s
           while (s[i] == '0')
           {

               // Replace initially
               // occurring 0 with 1
               s[i] = '1';
               i++;
           }

           // Break out of loop if 1 occurs
           break;
       }
    }
    return new String(s);
}

// Driver code
public static void Main(String[] args)
{
    String s = "100010001";

    Console.WriteLine(flip(s.ToCharArray()));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

    // JavaScript implementation to maximize the value of
    // the decimal equivalent given in the binary form

    // Function to print the binary number
    function flip(s)
    {
        for(let i = 0; i < s.length; i++)
        {

           // Check if the current number is 0
           if (s[i] == '0')
           {

               // Find the continuous 0s
               while (s[i] == '0')
               {

                   // Replace initially
                   // occurring 0 with 1
                   s[i] = '1';
                   i++;
               }

               // Break out of loop if 1 occurs
               break;
           }
        }
        return s.join("");
    }

    let s = "100010001";

    document.write(flip(s.split('')));

</script>
```

**Output:** 

```
111110001
```

时间复杂度:O(|s|)

辅助空间:0(1)