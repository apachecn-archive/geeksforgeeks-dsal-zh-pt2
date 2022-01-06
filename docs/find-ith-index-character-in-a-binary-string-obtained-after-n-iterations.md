# 在 n 次迭代后获得的二进制字符串中找到第 I 个索引字符

> 原文:[https://www . geesforgeks . org/find-with-index-二进制字符串中的字符-n 次迭代后获得/](https://www.geeksforgeeks.org/find-ith-index-character-in-a-binary-string-obtained-after-n-iterations/)

给定十进制数 m，将其转换为二进制字符串并应用 n 次迭代。在每次迭代中，0 变成“01”，1 变成“10”。在第 n 次迭代后，在字符串中查找(基于索引)索引字符。

**示例:**

```
Input : m = 5, n = 2, i = 3
Output : 1

Input :m = 3, n = 3, i = 6
Output : 1
```

[推荐:请先在“<u>”上解，再进行解。</u>](https://practice.geeksforgeeks.org/problems/find-k-th-character-in-string/0)

<u>1.将十进制数改为二进制数，并将其存储在字符串 s 中。
2。在每次迭代中运行循环 n 次。运行另一个字符串长度为 s 的循环，将 0 转换为“01”，将 1 转换为“10”，并存储在另一个字符串 s1 中。每次迭代完成后，将字符串 s1 分配给 s.
3。最后，返回字符串 s 中 ith 索引的值。</u>

## <u>C++</u>

```
// C++ Program to find ith character in
// a binary string.
#include <bits/stdc++.h>
using namespace std;

// Function to store binary Representation
void binary_conversion(string &s, int m) {
  while (m) {
    int tmp = m % 2;
    s += tmp + '0';
    m = m / 2;
  }
  reverse(s.begin(), s.end());
}

// Function to find ith character
int find_character(int n, int m, int i) {

  string s;

  // Function to change decimal to binary
  binary_conversion(s, m);

  string s1 = "";
  for (int x = 0; x < n; x++) {
    for (int y = 0; y < s.length(); y++) {
      if (s[y] == '1')
        s1 += "10";
      else
        s1 += "01";     
    }

    // Assign s1 string in s string
    s = s1;
    s1 = "";
  }
  return s[i] - '0';
}

// Driver Function
int main() {
  int m = 5, n = 2, i = 8;
  cout << find_character(n, m, i);
  return 0;
}
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java Program to find ith
// character in a binary String.
import java.io.*;
import java.util.Arrays;

class GFG
{
static String s = "";
static String ReverseString(String s)
{
    char[] arr = s.toCharArray();
    for(int i = 0;
            i < arr.length / 2; i++)
    {
        char temp = arr[i];
        arr[i] = arr[arr.length - i -1];
        arr[arr.length - i - 1] = temp;
    }
    return new String(arr);
}

// Function to store
// binary Representation
static void binary_conversion(int m)
{
    while (m != 0)
    {
        int tmp = m % 2;
        s += Integer.toString(tmp);
        m = (int)(m / 2);
    }

    s = ReverseString(s);
}

// Function to find
// ith character
static int find_character(int n,
                          int m,
                          int i)
{    
    // Function to change
    // decimal to binary
    binary_conversion(m);

    String s1 = "";
    for (int x = 0; x < n; x++)
    {
        for (int y = 0;
                 y < s.length(); y++)
        {
            if (s.charAt(y) == '1')
            s1 += "10";
            else
            s1 += "01";    
        }

        // Assign s1 String
        // in s String
        s = s1;
        s1 = "";
    }

    return s.charAt(i) - '0';
}

// Driver Code
public static void main(String args[])
{
    int m = 5, n = 2, i = 8;
    System.out.print(
               find_character(n, m, i));
}
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## <u>蟒蛇 3</u>

```
# Python3 Program to find ith character in
# a binary string.

# Function to store binary Representation
def binary_conversion(s, m):
    while(m):
        temp = m % 2
        s += str(temp)
        m = m // 2

    return s[::-1]

# Function to find ith character
def find_character(n, m, i):
    s = ""

# Function to change decimal to binary
    s = binary_conversion(s, m)
    s1 = ""

    for x in range(n):
        for j in range(len(s)):
            if s[j] == "1":
                s1 += "10"
            else:
                s1 += "01"

    # Assign s1 string in s string    
        s = s1
        s1 = ""
    e = ord(s[i])
    r = ord('0')

    return e-r

# Driver code
m, n, i = 5, 2, 8

print(find_character(n,m,i))

# This code is contributed by mohit kumar 29
```

## <u>C#</u>

```
// C# Program to find ith
// character in a binary string.
using System;

class GFG
{
    static string ReverseString(string s)
    {
        char[] arr = s.ToCharArray();
        Array.Reverse(arr);
        return new string(arr);
    }

    // Function to store
    // binary Representation
    static void binary_conversion(ref string s,
                                  int m)
    {
        while (m != 0)
        {
            int tmp = m % 2;
            s += tmp.ToString();
            m = (int)(m / 2);
        }

        s = ReverseString(s);
    }

    // Function to find
    // ith character
    static int find_character(int n,
                              int m, int i)
    {    
        string s = "";

        // Function to change
        // decimal to binary
        binary_conversion(ref s, m);

        string s1 = "";
        for (int x = 0; x < n; x++)
        {
            for (int y = 0; y < s.Length; y++)
            {
                if (s[y] == '1')
                s1 += "10";
                else
                s1 += "01";    
            }

            // Assign s1 string
            // in s string
            s = s1;
            s1 = "";
        }

        return s[i] - '0';
    }

    // Driver Code
    static void Main()
    {
        int m = 5, n = 2, i = 8;
        Console.Write(find_character(n, m, i));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## <u>java 描述语言</u>

```
<script>
// Javascript Program to find ith
// character in a binary String.

let  s = "";

function ReverseString(s)
{
    let arr = s.split("");
    for(let i = 0;
            i < arr.length / 2; i++)
    {
        let temp = arr[i];
        arr[i] = arr[arr.length - i -1];
        arr[arr.length - i - 1] = temp;
    }
    return arr.join("");
}

// Function to store
// binary Representation
function binary_conversion(m)
{
    while (m != 0)
    {
        let tmp = m % 2;
        s += tmp.toString();
        m = Math.floor(m / 2);
    }

    s = ReverseString(s);
}

// Function to find
// ith character
function find_character(n,m,i)
{
    // Function to change
    // decimal to binary
    binary_conversion(m);

    let s1 = "";
    for (let x = 0; x < n; x++)
    {
        for (let y = 0;
                 y < s.length; y++)
        {
            if (s[y] == '1')
                s1 += "10";
            else
                s1 += "01";    
        }

        // Assign s1 String
        // in s String
        s = s1;
        s1 = "";
    }

    return s[i] - '0';
}

// Driver Code
let m = 5, n = 2, i = 8;
document.write(find_character(n, m, i));

// This code is contributed by patel2127
</script>
```

<u>**Output:** 

```
1
```</u> 

<u>参考 [Set-2](https://www.geeksforgeeks.org/find-ith-index-character-in-a-binary-string-obtained-after-n-iterations-set-2/) 获得优化的解决方案。</u>