# 将两个字符串合并成给定大小的块

> 原文:[https://www . geesforgeks . org/merge-two-string-chunks-给定大小/](https://www.geeksforgeeks.org/merge-two-strings-chunks-given-size/)

给定两个字符串“a”和“b”以及一个数字 k，我们的目标是将这些字符串合并成一个字符串 **s** ，这样它在最终的字符串中交替包含来自这些字符串的 k 个字符组。

**例:**

```
Input: a = "durability", 
      b = "essence
      k = 3
Output: duressabienclitey

Input: a = "determination"
      b = "stance"
      k = 3
Output: detstaermnceination
```

在第二个例子中，我们从**确定**和**站姿**中交替选择三个字符的组来制作字符串。但是当**站位**的绳子完全用完之后，我们加入了**决心**剩下的绳子。

解决这个问题的方法是交替添加两个字符串的字符组，直到其中一个字符串结束。然后我们只需将剩余字符串的剩余部分按原样添加到答案中。

## c++

```
// C++ program to merge n number of strings
#include <bits/stdc++.h>
using namespace std;

// Function performing the calculations
void solve(string a, string b, int k)
{
    string s = "";

    // Length of string a
    int la = a.length();

    // Length f string b
    int lb = b.length();
    int l = la + lb;

    // Pointers for string
    // a and string b
    int indexa = 0, indexb = 0;
    while (l > 0) {

        // pa and pb denote the number
        // of characters of both
        // a and b extracted
        int pa = 0, pb = 0;

        // If entire substring of length
        // k can be extracted
        if (la - indexa >= k) {

            // Please refer below link for
            // details of library function
            // https://www.geeksforgeeks.org/stdsubstr-in-ccpp/
            s = s + a.substr(indexa, k);
            indexa = indexa + k;
            pa = k;
        }

        // If the remaining string is
        // of length less than k
        else if (la - indexa < k && la - indexa > 0) {
            s = s + a.substr(indexa, la - indexa);
            pa = la - indexa;
            indexa = la;
        }

        // If the string has been
        // traversed
        else if (indexa >= la)
            pa = 0;

        // If entire substring of
        // length k can be extracted
        if (lb - indexb >= k) {
            s = s + b.substr(indexb, k);
            pb = k;
            indexb = indexb + k;
        }

        // If the remaining string is of
        // length less than k
        else if (lb - indexb < k && lb - indexb > 0) {
            s = s + b.substr(indexb, lb - indexb);
            pb = lb - indexb;
            indexb = lb;
        }

        // If the string has been
        // traversed
        else if (indexb >= lb)
            pb = 0;
        l = l - pa - pb;
    }
    cout << s;
}

// Driver function
int main()
{
    string a = "determination", b = "stance";
    int k = 3;
    solve(a, b, k);
    return 0;
}
```

## Java

```
// Java program to merge
// n number of strings
import java.io.*;
class msc {
    // Function performing calculations
    public static void solve(String a,
                             String b, int k)
    {
        String s = "";

        // Length of string a
        int la = a.length();

        // Length f string b
        int lb = b.length();
        int l = la + lb;

        // Pointers for string a and string b
        int indexa = 0, indexb = 0;
        while (l > 0) {

            // pa and pb denote the number
            // of characters of both
            // a and b extracted
            int pa = 0, pb = 0;

            // If entire substring of
            // length k can be extracted
            if (la - indexa >= k) {
                s = s + a.substring(indexa, indexa + k);
                indexa = indexa + k;
                pa = k;
            }

            // If the remaining string is
            // of length less than k
            else if (la - indexa < k && la - indexa > 0) {
                s = s + a.substring(indexa, la);
                pa = la - indexa;
                indexa = la;
            }

            // If the string has been
            // traversed
            else if (indexa >= la)
                pa = 0;

            // If entire substring of
            // length k can be extracted
            if (lb - indexb >= k) {
                s = s + b.substring(indexb, indexb + k);
                pb = k;
                indexb = indexb + k;
            }

            // If the remaining string
            // is of length less than k
            else if (lb - indexb < k && lb - indexb > 0) {
                s = s + b.substring(indexb, lb);
                pb = lb - indexb;
                indexb = lb;
            }

            // If the string has been
            // traversed
            else if (indexb >= lb)
                pb = 0;
            l = l - pa - pb;
        }
        System.out.println(s);
    }

    // Driver function
    public static void main(String args[])
        throws IOException
    {
        String a = "determination", b = "stance";
        int k = 3;
        solve(a, b, k);
    }
}
```

## python 3

```
# Python3 program to merge n number of strings

# Function performing the calculations
def solve(a, b, k):
    s = ""

    # Length of string a
    la = len(a)

    # Length f string b
    lb = len(b)
    l = la + lb

    # Pointers for string
    # a and string b
    indexa = indexb = 0

    while l:
        # pa and pb denote the number
        # of characters of both
        # a and b extracted
        pa = pb = 0

        # If entire substring of length
        # k can be extracted
        if la - indexa >= k:
            s = s + a[indexa : indexa + k]
            indexa = indexa + k
            pa = k

        # If the remaining string is
        # of length less than k
        elif la - indexa < k and la - indexa:
            s = s + a[indexa : la]
            pa = la - indexa
            indexa = la

        # If the string has been
        # traversed
        elif indexa >= la:
            pa = 0

        # If entire substring of
        # length k can be extracted
        if lb - indexb >= k:
            s = s + b[indexb : indexb+k]
            pb = k
            indexb = indexb + k

        # If the remaining string is of
        # length less than k
        elif lb - indexb < k and lb - indexb:
            s = s + b[indexb : lb]
            pb = lb - indexb
            indexb = lb

        # If the string has been
        # traversed
        elif indexb >= lb:
            pb = 0
        l = l - pa - pb

    print(s)

# Driver function
a = "determination"; b = "stance"
k = 3
solve(a, b, k)

# This code is contributed by Ansu Kumari
```

## c#

```
// C# program to merge
// n number of strings
using System;

class GFG
{
    // Function performing
    // the calculations
    static void solve(string a,
                      string b,
                      int k)
    {
        string s = "";

        // Length of string a
        int la = a.Length;

        // Length f string b
        int lb = b.Length;
        int l = la + lb;

        // Pointers for string
        // a and string b
        int indexa = 0, indexb = 0;
        while (l > 0)
        {

            // pa and pb denote the
            // number of characters
            // a and b extracted
            int pa = 0, pb = 0;

            // If entire substring
            // of length k can be
            // extracted
            if (la - indexa >= k)
            {
                s = s + a.Substring(indexa, k);
                indexa = indexa + k;
                pa = k;
            }

            // If the remaining string
            // is of length less than k
            else if (la - indexa < k &&
                     la - indexa > 0)
            {
                s = s + a.Substring(indexa,
                                    la - indexa);
                pa = la - indexa;
                indexa = la;
            }

            // If the string has
            // been traversed
            else if (indexa >= la)
                pa = 0;

            // If entire substring
            // of length k can be
            // extracted
            if (lb - indexb >= k)
            {
                s = s + b.Substring(indexb, k);
                pb = k;
                indexb = indexb + k;
            }

            // If the remaining string
            // is of length less than k
            else if (lb - indexb < k &&
                     lb - indexb > 0)
            {
                s = s + b.Substring(indexb,
                               lb - indexb);
                pb = lb - indexb;
                indexb = lb;
            }

            // If the string has
            // been traversed
            else if (indexb >= lb)
                pb = 0;
            l = l - pa - pb;
        }
        Console.Write(s);
    }

    // Driver Code
    static void Main()
    {
        string a = "determination",
               b = "stance";
        int k = 3;
        solve(a, b, k);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

**输出:**

```
detstaermnceination
```