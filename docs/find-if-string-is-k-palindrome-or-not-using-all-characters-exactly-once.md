# 查找字符串是否是 K-回文或不使用所有字符一次

> 原文:[https://www . geesforgeks . org/find-if-string-is-k-回文-or-not-use-all-characters-恰好一次/](https://www.geeksforgeeks.org/find-if-string-is-k-palindrome-or-not-using-all-characters-exactly-once/)

给定一个字符串 **str** 和一个整数 **K** ，任务是检查是否有可能使用字符串的所有字符一次生成字符串 **K 回文**。
**示例:**

> **输入:** str = "poor "，K = 3
> **输出:** Yes
> 获取 3 个回文的一种方法是:oo，p，r
> 
> **输入:** str = "fun "，K = 5
> **输出:**否
> 2 个回文不能用 3 个不同的字母构成。因此不可能。

**进场:**

1.  如果字符串的大小小于 k，就不可能得到 k 个回文。
2.  如果字符串的大小等于 k，得到 k 个回文总是可能的。我们给 k 个字符串中的每一个 1 个字符，它们都是回文，因为长度为 1 的字符串总是回文。
3.  如果字符串的大小大于 k，那么有些字符串可能超过 1 个字符。
    *   创建一个 hashmap 来存储每个字符的频率，因为出现次数为偶数的字符可以以 2 为一组分布。
    *   检查出现次数为奇数的字符数是否小于或等于 k，我们可以说 k 个回文总是可以生成的，否则不行。

下面是上述方法的实现:

## C++

```
// C++ program to find if string is K-Palindrome
// or not using all characters exactly once

#include <bits/stdc++.h>
using namespace std;

void iskPalindromesPossible(string s, int k)
{
    // when size of string is less than k
    if (s.size() < k) {
        cout << "Not Possible" << endl;
        return;
    }

    // when size of string is equal to k
    if (s.size() == k) {
        cout << "Possible" << endl;
        return;
    }

    // when size of string is greater than k

    // to store the frequencies of the characters
    map<char, int> freq;
    for (int i = 0; i < s.size(); i++)
        freq[s[i]]++;

    // to store the count of characters
    // whose number of occurrences is odd.
    int count = 0;

    // iterating over the map
    for (auto it : freq) {
        if (it.second % 2 == 1)
            count++;
    }
    if (count > k)
        cout << "No" << endl;
    else
        cout << "Yes" << endl;
}

// Driver code
int main()
{

    string str = "poor";
    int K = 3;
    iskPalindromesPossible(str, K);

    str = "geeksforgeeks";
    K = 10;
    iskPalindromesPossible(str, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if String
// is K-Palindrome or not using 
// all characters exactly once
import java.util.*;

class GFG{

static void iskPalindromesPossible(String s,
                                   int k)
{

    // When size of String is less than k
    if (s.length() < k)
    {
        System.out.print("Not Possible" + "\n");
        return;
    }

    // When size of String is equal to k
    if (s.length() == k)
    {
        System.out.print("Possible" + "\n");
        return;
    }

    // When size of String is greater than k
    // to store the frequencies of the characters
    HashMap<Character,
            Integer> freq = new HashMap<Character,
                                        Integer>();
    for(int i = 0; i < s.length(); i++)
       if(freq.containsKey(s.charAt(i)))
       {
           freq.put(s.charAt(i), 
           freq.get(s.charAt(i)) + 1);
       }
       else
       {
           freq.put(s.charAt(i), 1);
       }

    // To store the count of characters
    // whose number of occurrences is odd.
    int count = 0;

    // Iterating over the map
    for(Map.Entry<Character, 
                  Integer> it : freq.entrySet()) 
    {
       if (it.getValue() % 2 == 1)
           count++;
    }

    if (count > k)
        System.out.print("No" + "\n");
    else
        System.out.print("Yes" + "\n");
}

// Driver code
public static void main(String[] args)
{
    String str = "poor";
    int K = 3;
    iskPalindromesPossible(str, K);

    str = "geeksforgeeks";
    K = 10;
    iskPalindromesPossible(str, K);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Find if string is K-Palindrome or not using all characters exactly once
# Python 3 program to find if string is K-Palindrome
# or not using all characters exactly once

def iskPalindromesPossible(s, k):

    # when size of string is less than k
    if (len(s)<k):
        print("Not Possible")
        return

    # when size of string is equal to k
    if (len(s) == k):
        print("Possible")
        return

    # when size of string is greater than k

    # to store the frequencies of the characters
    freq = dict.fromkeys(s,0)
    for i in range(len(s)):
        freq[s[i]] += 1

    #to store the count of characters
    # whose number of occurrences is odd.
    count = 0

    # iterating over the map
    for value in freq.values():
        if (value % 2 == 1):
            count += 1
    if (count > k):
        print("No")
    else:
        print("Yes")

# Driver code
if __name__ == '__main__':
    str1 = "poor"
    K = 3
    iskPalindromesPossible(str1, K)

    str = "geeksforgeeks"
    K = 10
    iskPalindromesPossible(str, K)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to find if String
// is K-Palindrome or not using 
// all characters exactly once
using System;
using System.Collections.Generic;

class GFG{

static void iskPalindromesPossible(String s,
                                   int k)
{

    // When size of String is less than k
    if (s.Length < k)
    {
        Console.Write("Not Possible" + "\n");
        return;
    }

    // When size of String is equal to k
    if (s.Length == k)
    {
        Console.Write("Possible" + "\n");
        return;
    }

    // When size of String is greater than k
    // to store the frequencies of the characters
    Dictionary<int, 
               int> freq = new Dictionary<int,
                                          int>();
    for(int i = 0; i < s.Length; i++)
        if(freq.ContainsKey(s[i]))
        {
            freq[s[i]] = freq[s[i]] + 1;
        }
        else
        {
            freq.Add(s[i], 1);
        }

    // To store the count of characters
    // whose number of occurrences is odd.
    int count = 0;

    // Iterating over the map
    foreach(KeyValuePair<int, int> it in freq) 
    {
        if (it.Value % 2 == 1)
            count++;
    }

    if (count > k)
        Console.Write("No" + "\n");
    else
        Console.Write("Yes" + "\n");
}

// Driver code
public static void Main(String[] args)
{
    String str = "poor";
    int K = 3;
    iskPalindromesPossible(str, K);

    str = "geeksforgeeks";
    K = 10;
    iskPalindromesPossible(str, K);
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
Yes
Yes

```