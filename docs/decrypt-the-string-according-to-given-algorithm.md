# 根据给定算法

解密字符串

> 原文:[https://www . geesforgeks . org/根据给定算法解密字符串/](https://www.geeksforgeeks.org/decrypt-the-string-according-to-given-algorithm/)

给定由字母和数字字符组成的加密字符串 **str** ，任务是解密该字符串并找到加密消息。
为了解密信息，找出代表单个字母字符的每一串数字字符，这些字符可以通过用 26 计算数字的模来获得，从范围[0，25]中找到的值可以用字符['a '，' z']来映射。
**例如**如果**str = " 32ytaacv4ui 30 HF 10 HJ 18 "**那么数字字符的簇将是 **{32，4，30，10，18}** ，其给出 **{6，4，4，10，18}** 在用 26 执行模数后，可以映射到 **{'g '，' e '，' e '，' k '，' s'}**

> **输入:**str = " this 50hi 4 huji 70 "
> **输出:**极客
> **输入:** str = "a1s2d3f3"
> **输出:** bcdd

**方法:**思路是在字符串中逐个遍历每个字符，然后检查是否是数字字符。如果是，则将其连接成一个字符串。最后，用 26 对数字串取模。
在做模运算时，我们不能简单地做 x % 26，因为这个数字可能太大，会导致整数溢出。
对此，我们将逐一处理所有数字，并使用属性
**(A * B)mod C =((A mod C)*(B mod C))mod C**
然后，最终将每个整数解码回字符 0，1，2，3，…25 到' A '，' B '，' C '，…'z '，连接所有字符并打印最终结果。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int MOD = 26;

// Function that returns (num % 26)
int modulo_by_26(string num)
{
    // Initialize result
    int res = 0;

    // One by one process all digits of 'num'
    for (int i = 0; i < num.length(); i++)
        res = (res * 10 + (int)num[i] - '0') % MOD;

    return res;
}

// Function to return the decrypted string
string decrypt_message(string s)
{

    // To store the final decrypted answer
    string decrypted_str = "";

    string num_found_so_far = "";

    // One by one check for each character
    // if it is a numeric character
    for (int i = 0; i < s.length(); ++i) {

        if (s[i] >= '0' && s[i] <= '9') {
            num_found_so_far += s[i];
        }
        else if (num_found_so_far.length() > 0) {

            // Modulo the number found in the string by 26
            decrypted_str += 'a'
                             + modulo_by_26(num_found_so_far);

            num_found_so_far = "";
        }
    }

    if (num_found_so_far.length() > 0) {
        decrypted_str += 'a'
                         + modulo_by_26(num_found_so_far);
    }

    return decrypted_str;
}

// Driver code
int main()
{
    string s = "32ytAAcV4ui30hf10hj18";

    // Print the decrypted string
    cout << decrypt_message(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

static int MOD = 26;

// Function that returns (num % 26)
static int modulo_by_26(String num)
{

    // Initialize result
    int res = 0;

    // One by one process all digits of 'num'
    for(int i = 0; i < num.length(); i++)
    {
       res = ((res * 10 +
              (int)num.charAt(i) - '0') % MOD);
    }
    return res;
}

// Function to return the decrypted String
static String decrypt_message(String s)
{

    // To store the final decrypted answer
    String decrypted_str = "";
    String num_found_so_far = "";

    // One by one check for each character
    // if it is a numeric character
    for(int i = 0; i < s.length(); ++i)
    {
       if (s.charAt(i) >= '0' && s.charAt(i) <= '9')
       {
           num_found_so_far += s.charAt(i);
       }
       else if (num_found_so_far.length() > 0)
       {

           // Modulo the number found in the String by 26
           decrypted_str += (char)('a' +
                             modulo_by_26(num_found_so_far));
           num_found_so_far = "";
       }
    }
    if (num_found_so_far.length() > 0)
    {
        decrypted_str += (char)('a' +
                          modulo_by_26(num_found_so_far));
    }
    return decrypted_str;
}

// Driver code
public static void main(String[] args)
{
    String s = "32ytAAcV4ui30hf10hj18";

    // Print the decrypted string
    System.out.print(decrypt_message(s));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation of
# the approach
MOD = 26

# Function that returns
# (num % 26)
def modulo_by_26(num):

    # Initialize result
    res = 0

    # One by one process all
    # digits of 'num'
    for i in range(len(num)):
        res = ((res * 10 + ord(num[i]) -
                ord('0')) % MOD)

    return res

# Function to return the
# decrypted string
def decrypt_message(s):

    # To store the final
    # decrypted answer
    decrypted_str = ""

    num_found_so_far = ""

    # One by one check for
    # each character if it
    # is a numeric character
    for i in range(len(s)):

        if (s[i] >= '0' and
            s[i] <= '9'):
            num_found_so_far += s[i]
        elif (len(num_found_so_far) > 0):

            # Modulo the number found
            # in the string by 26
            decrypted_str += chr(ord('a') +
                            (modulo_by_26(num_found_so_far)))

            num_found_so_far = ""

    if (len(num_found_so_far) > 0):
        decrypted_str += chr(ord('a') +
                        (modulo_by_26(num_found_so_far)))

    return decrypted_str

# Driver code
if __name__ == "__main__":

    s = "32ytAAcV4ui30hf10hj18"

    # Print the decrypted string
    print(decrypt_message(s))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the approach
using System;
class GFG{

static int MOD = 26;

// Function that returns (num % 26)
static int modulo_by_26(String num)
{

    // Initialize result
    int res = 0;

    // One by one process all digits of 'num'
    for(int i = 0; i < num.Length; i++)
    {
        res = ((res * 10 +
               (int)num[i] - '0') % MOD);
    }
    return res;
}

// Function to return the decrypted String
static String decrypt_message(String s)
{

    // To store the readonly decrypted answer
    String decrypted_str = "";
    String num_found_so_far = "";

    // One by one check for each character
    // if it is a numeric character
    for(int i = 0; i < s.Length; ++i)
    {
        if (s[i] >= '0' && s[i] <= '9')
        {
            num_found_so_far += s[i];
        }
        else if (num_found_so_far.Length > 0)
        {

            // Modulo the number found
            // in the String by 26
            decrypted_str += (char)('a' +
                              modulo_by_26(num_found_so_far));
            num_found_so_far = "";
        }
    }
    if (num_found_so_far.Length > 0)
    {
        decrypted_str += (char)('a' +
                          modulo_by_26(num_found_so_far));
    }
    return decrypted_str;
}

// Driver code
public static void Main(String[] args)
{
    String s = "32ytAAcV4ui30hf10hj18";

    // Print the decrypted string
    Console.Write(decrypt_message(s));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let MOD = 26;

// Function that returns (num % 26)
function modulo_by_26(num)
{
    // Initialize result
    let res = 0;

    // One by one process all digits of 'num'
    for(let i = 0; i < num.length; i++)
    {
       res = ((res * 10 +
              num[i].charCodeAt(0) - '0'.charCodeAt(0)) % MOD);
    }
    return res;
}

// Function to return the decrypted String
function decrypt_message(s)
{
    // To store the final decrypted answer
    let decrypted_str = "";
    let num_found_so_far = "";

    // One by one check for each character
    // if it is a numeric character
    for(let i = 0; i < s.length; ++i)
    {
       if (s[i].charCodeAt(0) >= '0'.charCodeAt(0) &&
       s[i].charCodeAt(0) <= '9'.charCodeAt(0))
       {
           num_found_so_far += s[i];
       }
       else if (num_found_so_far.length > 0)
       {

           // Modulo the number found in the String by 26
           decrypted_str += String.fromCharCode('a'.charCodeAt(0) +
                             modulo_by_26(num_found_so_far));
           num_found_so_far = "";
       }
    }
    if (num_found_so_far.length > 0)
    {
        decrypted_str += String.fromCharCode('a'.charCodeAt(0) +
                          modulo_by_26(num_found_so_far));
    }
    return decrypted_str;
}

// Driver code

let s = "32ytAAcV4ui30hf10hj18";

// Print the decrypted string
document.write(decrypt_message(s));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
geeks
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)