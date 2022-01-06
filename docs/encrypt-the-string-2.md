# 加密字符串–2

> 原文:[https://www.geeksforgeeks.org/encrypt-the-string-2/](https://www.geeksforgeeks.org/encrypt-the-string-2/)

给定由 **N、**小写英文字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，也给定一个字符串，通过首先将由相同字符组成的字符串的每个[子串替换为该字符和子串大小的](https://www.geeksforgeeks.org/program-print-substrings-given-string/)[十六进制表示](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)的连接，然后[反转整个字符串](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/)来加密，任务是找到加密的字符串。

**注意:**所有十六进制字母都要转换成小写字母。

**示例:**

> **输入:**S = " aaaaaaaaaaaa "
> T3】输出:ba
> T6】说明:
> 
> 1.  首先将给定的字符串转换为“a11”**，即写入字符及其频率。**
> 2.  **然后，将“a11”改为“ab”，因为 11 是十六进制的b 。**
> 3.  **然后，最后反转字符串，即“巴”。**
> 
> ****输入:**S =【ABC】
> T3】输出: 1c1b1a**

****方法:**这个问题可以通过[迭代字符串 S 的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)来解决。按照以下步骤解决此问题:**

*   **初始化一个空的[字符串](https://www.geeksforgeeks.org/string-data-structure/) 说， **ans** 来存储答案。**
*   **[使用变量 **i** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S、**的字符，并执行以下步骤:

    *   从索引 **i** 开始，找到具有相同字符的子串**S【I】、**的计数，并将其存储在一个变量中，比如说，**计数**。
    *   现在[将计数转换为十六进制表示](https://www.geeksforgeeks.org/program-decimal-hexadecimal-conversion/)，并附加字符 **S[i]** 及其频率十六进制表示。** 
*   **最后[反转字符串](https://www.geeksforgeeks.org/reverse-a-string-in-java/) **ans** 然后打印出来。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to convert Decimal to Hex
string convertToHex(int num)
{

    string temp = "";
    while (num != 0) {
        int rem = num % 16;
        char c;
        if (rem < 10) {
            c = rem + 48;
        }
        else {
            c = rem + 87;
        }
        temp += c;
        num = num / 16;
    }

    return temp;
}

// Function to encrypt the string
string encryptString(string S, int N)
{

    string ans = "";

    // Iterate the characters
    // of the string
    for (int i = 0; i < N; i++) {

        char ch = S[i];
        int count = 0;
        string hex;

        // Iterate until S[i] is equal to ch
        while (i < N && S[i] == ch) {

            // Update count and i
            count++;
            i++;
        }

        // Decrement i by 1
        i--;

        // Convert count to hexadecimal
        // representation
        hex = convertToHex(count);

        // Append the character
        ans += ch;

        // Append the characters frequency
        // in hexadecimal representation
        ans += hex;
    }

    // Reverse the obtained answer
    reverse(ans.begin(), ans.end());

    // Return required answer
    return ans;
}

// Driver Code
int main()
{

    // Given Input
    string S = "abc";
    int N = S.size();

    // Function Call
    cout << encryptString(S, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for above approach
import java.awt.*;
import java.util.*;
class GFG
{

    // Function to convert Decimal to Hex
    static String convertToHex(int num)
    {

        StringBuilder temp = new StringBuilder();
        while (num != 0) {
            int rem = num % 16;
            char c;
            if (rem < 10) {
                c = (char) (rem + 48);
            }
            else {
                c = (char) (rem + 87);
            }
            temp.append(c);
            num = num / 16;
        }

        return temp.toString();
    }

    // Function to encrypt the string
    static String encryptString(String S, int N)
    {

        StringBuilder ans = new StringBuilder();

        // Iterate the characters
        // of the string
        for (int i = 0; i < N; i++) {

            char ch = S.charAt(i);
            int count = 0;
            String hex;

            // Iterate until S[i] is equal to ch
            while (i < N && S.charAt(i) == ch) {

                // Update count and i
                count++;
                i++;
            }

            // Decrement i by 1
            i--;

            // Convert count to hexadecimal
            // representation
            hex = convertToHex(count);

            // Append the character
            ans.append(ch);

            // Append the characters frequency
            // in hexadecimal representation
            ans.append(hex);
        }

        // Reverse the obtained answer
        ans.reverse();

        // Return required answer
        return ans.toString();
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        String S = "abc";
        int N = S.length();

        // Function Call
        System.out.println(encryptString(S, N));
    }
}

// This code is contributed by hritikrommie.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to convert Decimal to Hex
def convertToHex(num):

    temp = ""
    while (num != 0):
        rem = num % 16
        c = 0

        if (rem < 10):
            c = rem + 48
        else:
            c = rem + 87

        temp += chr(c)
        num = num // 16

    return temp

# Function to encrypt the string
def encryptString(S, N):

    ans = ""

    # Iterate the characters
    # of the string
    for i in range(N):
        ch = S[i]
        count = 0

        # Iterate until S[i] is equal to ch
        while (i < N and S[i] == ch):

            # Update count and i
            count += 1
            i += 1

        # Decrement i by 1
        i -= 1

        # Convert count to hexadecimal
        # representation
        hex = convertToHex(count)

        # Append the character
        ans += ch

        # Append the characters frequency
        # in hexadecimal representation
        ans += hex

    # Reverse the obtained answer
    ans = ans[::-1]

    # Return required answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    S = "abc"
    N = len(S)

    # Function Call
    print(encryptString(S, N))

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for above approach
using System;
class GFG
{

    // Function to convert Decimal to Hex
    static string convertToHex(int num)
    {

        string temp = "";
        while (num != 0) {
            int rem = num % 16;
            char c;
            if (rem < 10) {
                c = (char) (rem + 48);
            }
            else {
                c = (char) (rem + 87);
            }
            temp = temp + c;
            num = num / 16;
        }

        return temp;
    }

    // Function to encrypt the string
    static string encryptString(string S, int N)
    {

        string ans = "";

        // Iterate the characters
        // of the string
        for (int i = 0; i < N; i++) {

            char ch = S[i];
            int count = 0;
            string hex;

            // Iterate until S[i] is equal to ch
            while (i < N && S[i] == ch) {

                // Update count and i
                count++;
                i++;
            }

            // Decrement i by 1
            i--;

            // Convert count to hexadecimal
            // representation
            hex = convertToHex(count);

            // Append the character
            ans = ans + ch;

            // Append the characters frequency
            // in hexadecimal representation
            ans = ans + hex;
        }

        // Reverse the obtained answer
        char[] Ans = ans.ToCharArray();
        Array.Reverse(Ans);
        ans = new string(Ans);

        // Return required answer
        return ans;
    }

  static void Main ()
  {
    // Given Input
    string S = "abc";
    int N = S.Length;

    // Function Call
    Console.WriteLine(encryptString(S, N));
  }
}

// This code is contributed by suresh07.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to convert Decimal to Hex
function convertToHex(num) {

    let temp = "";
    while (num != 0) {
        let rem = num % 16;
        let c = 0;
        if (rem < 10) {
            c = rem + 48;
        }
        else {
            c = rem + 87;
        }
        temp += String.fromCharCode(c);
        num = Math.floor(num / 16);
    }

    return temp;
}

// Function to encrypt the string
function encryptString(S, N) {

    let ans = "";

    // Iterate the characters
    // of the string
    for (let i = 0; i < N; i++) {

        let ch = S[i];
        let count = 0;
        let hex;

        // Iterate until S[i] is equal to ch
        while (i < N && S[i] == ch) {

            // Update count and i
            count++;
            i++;
        }

        // Decrement i by 1
        i--;

        // Convert count to hexadecimal
        // representation
        hex = convertToHex(count);

        // Append the character
        ans += ch;

        // Append the characters frequency
        // in hexadecimal representation
        ans += hex;
    }

    // Reverse the obtained answer
    ans = ans.split('').reverse().join("");

    // Return required answer
    return ans;
}

// Driver Code

// Given Input
let S = "abc";
let N = S.length;

// Function Call
document.write(encryptString(S, N));

</script>
```

****Output:** 

```
1c1b1a
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**