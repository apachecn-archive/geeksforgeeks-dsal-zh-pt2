# 一次交换中可能出现的字典上最大的字符串

> 原文:[https://www . geesforgeks . org/按字典顺序排列的最大可能字符串一次交换/](https://www.geeksforgeeks.org/lexicographically-largest-string-possible-in-one-swap/)

给定长度为 **N** 的字符串 **str** ，任务是通过最多一次交换获得字典上最大的字符串。

***注意:**交换的字符可能不相邻。*

**示例:**

> **输入:** str = "string"
> **输出:** tsring
> **解释:**
> 通过交换**ST**ring->**ts**ring 获得的字典上最大的字符串。
> 
> **输入:** str = "zyxw"
> **输出:** zyxw
> **解释:**
> 给定的字符串在字典上已经是最大的了

**方法:**
为了解决上述问题，主要思想是使用[排序](https://www.geeksforgeeks.org/sorting-algorithms/)并为给定的字符串计算可能的最大字典序字符串。对给定字符串进行降序排序后，从给定字符串中找到第一个不匹配字符**，并用排序字符串中最后一个出现的不匹配字符替换。**

> ****插图:**T2
> 按降序排列的字符串。
> 第一个无与伦比的角色排在第一位。该字符需要与排序字符串中该位置的字符交换，这将产生字典上最大的字符串。当用“s”替换“g”时，得到的字符串是**“seekg”**，这是一次交换后字典上最大的字符串。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation to find the
// lexicographically largest string
// by atmost at most one swap

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// lexicographically largest
// string possible by swapping
// at most one character
string findLargest(string s)
{
    int len = s.size();

    // Stores last occurrence
    // of every character
    int loccur[26];

    // Initialize with -1 for
    // every character
    memset(loccur, -1, sizeof(loccur));

    for (int i = len - 1; i >= 0; --i) {

        // Keep updating the last
        // occurrence of each character
        int chI = s[i] - 'a';
        // If a previously unvisited
        // character occurs
        if (loccur[chI] == -1) {
            loccur[chI] = i;
        }
    }
    // Stores the sorted string
    string sorted_s = s;
    sort(sorted_s.begin(), sorted_s.end(),
        greater<int>());

    for (int i = 0; i < len; ++i) {
        if (s[i] != sorted_s[i]) {

            // Character to replace
            int chI = sorted_s[i] - 'a';

            // Find the last occurrence
            // of this character
            int last_occ = loccur[chI];

            // Swap this with the last
            // occurrence
            swap(s[i], s[last_occ]);
            break;
        }
    }

    return s;
}

// Driver Program
int main()
{
    string s = "yrstvw";
    cout << findLargest(s);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation to find the
// lexicographically largest string
// by atmost at most one swap
import java.util.*;
import java.lang.*;

class GFG{

// Function to return the
// lexicographically largest
// string possible by swapping
// at most one character
static String findLargest(StringBuilder s)
{
    int len = s.length();

    // Stores last occurrence
    // of every character
    int[] loccur = new int[26];

    // Initialize with -1 for
    // every character
    Arrays.fill(loccur, -1);

    for(int i = len - 1; i >= 0; --i)
    {

        // Keep updating the last
        // occurrence of each character
        int chI = s.charAt(i) - 'a';

        // If a previously unvisited
        // character occurs
        if (loccur[chI] == -1)
        {
            loccur[chI] = i;
        }
    }

    // Stores the sorted string
    char[] sorted_s = s.toString().toCharArray();

    Arrays.sort(sorted_s);
    reverse(sorted_s);

    for(int i = 0; i < len; ++i)
    {
        if (s.charAt(i) != sorted_s[i])
        {

            // Character to replace
            int chI = sorted_s[i] - 'a';

            // Find the last occurrence
            // of this character
            int last_occ = loccur[chI];

            // Swap this with the last
            // occurrence
            char tmp = s.charAt(i);
            s.setCharAt(i, s.charAt(last_occ));
            s.setCharAt(last_occ, tmp);

            break;
        }
    }
    return s.toString();
}

// Function to reverse array
static void reverse(char a[])
{
    int i, n = a.length;

    for(i = 0; i < n / 2; i++)
    {
        char t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Driver Code
public static void main(String[] args)
{
    StringBuilder s = new StringBuilder("yrstvw");

    System.out.println(findLargest(s));
}
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 implementation to find the 
# lexicographically largest string 
# by atmost at most one swap

# Function to return the 
# lexicographically largest 
# string possible by swapping 
# at most one character
def findLargest(s):
    Len = len(s)

    # Stores last occurrence 
    # of every character
    # Initialize with -1 for 
    # every character
    loccur = [-1 for i in range(26)]

    for i in range(Len - 1, -1, -1):

        # Keep updating the last 
        # occurrence of each character
        chI = ord(s[i]) - ord('a')

        # If a previously unvisited 
        # character occurs
        if(loccur[chI] == -1):
            loccur[chI] = i

    # Stores the sorted string
    sorted_s = sorted(s, reverse = True)
    for i in range(Len):
        if(s[i] != sorted_s[i]):

            # Character to replace
            chI = (ord(sorted_s[i]) -
                   ord('a'))

            # Find the last occurrence 
            # of this character
            last_occ = loccur[chI]
            temp = list(s)

            # Swap this with the last 
            # occurrence
            temp[i], temp[last_occ] = (temp[last_occ],
                                       temp[i])
            s = "".join(temp)
            break
    return s

# Driver code
s = "yrstvw"
print(findLargest(s))

# This code is contributed by avanitrachhadiya2155
```

## **C#**

```
// C# implementation to find the
// lexicographically largest string
// by atmost at most one swap
using System;
using System.Collections.Generic;

class GFG{

// Function to return the
// lexicographically largest
// string possible by swapping
// at most one character
static string findLargest(char[] s)
{
    int len = s.Length;

    // Stores last occurrence
    // of every character
    int[] loccur = new int[26];

    // Initialize with -1 for
    // every character
    Array.Fill(loccur, -1);

    for(int i = len - 1; i >= 0; --i)
    {

        // Keep updating the last
        // occurrence of each character
        int chI = s[i] - 'a';

        // If a previously unvisited
        // character occurs
        if (loccur[chI] == -1)
        {
            loccur[chI] = i;
        }
    }

    // Stores the sorted string
    char[] sorted_s = (new string(s)).ToCharArray();

    Array.Sort(sorted_s);
    Array.Reverse(sorted_s);

    for(int i = 0; i < len; ++i)
    {
        if (s[i] != sorted_s[i])
        {

            // Character to replace
            int chI = sorted_s[i] - 'a';

            // Find the last occurrence
            // of this character
            int last_occ = loccur[chI];

            // Swap this with the last
            // occurrence
            char temp = s[i];
            s[i] = s[last_occ];
            s[last_occ] = temp;
            break;
        }
    }
    return (new string(s));
}

// Driver Code
static void Main()
{
    string str = "yrstvw";
    char[] s = str.ToCharArray();

    Console.WriteLine(findLargest(s));
}
}

// This code is contributed by divyesh072019
```

## **java 描述语言**

```
<script>

    // Javascript implementation to find the
    // lexicographically largest string
    // by atmost at most one swap

    // Function to return the
    // lexicographically largest
    // string possible by swapping
    // at most one character
    function findLargest(s)
    {
        let len = s.length;

        // Stores last occurrence
        // of every character
        let loccur = new Array(26);

        // Initialize with -1 for
        // every character
        loccur.fill(-1);

        for(let i = len - 1; i >= 0; --i)
        {

            // Keep updating the last
            // occurrence of each character
            let chI = s[i].charCodeAt() - 'a'.charCodeAt();

            // If a previously unvisited
            // character occurs
            if (loccur[chI] == -1)
            {
                loccur[chI] = i;
            }
        }

        // Stores the sorted string
        let sorted_s = s.join("").split('');

        sorted_s.sort();
        sorted_s.reverse();

        for(let i = 0; i < len; ++i)
        {
            if (s[i] != sorted_s[i])
            {

                // Character to replace
                let chI = sorted_s[i].charCodeAt() - 'a'.charCodeAt();

                // Find the last occurrence
                // of this character
                let last_occ = loccur[chI];

                // Swap this with the last
                // occurrence
                let temp = s[i];
                s[i] = s[last_occ];
                s[last_occ] = temp;
                break;
            }
        }
        return (s.join(""));
    }

    let str = "yrstvw";
    let s = str.split('');

    document.write(findLargest(s));

</script>
```

****Output:** 

```
ywstvr
```**