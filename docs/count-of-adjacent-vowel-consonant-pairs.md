# 相邻元音辅音对的计数

> 原文:[https://www . geesforgeks . org/相邻元音辅音对计数/](https://www.geeksforgeeks.org/count-of-adjacent-vowel-consonant-pairs/)

给定一个字符串，任务是计算相邻对的数量，使得对的第一个元素是辅音，第二个元素是元音。也就是说，找出配对数(I，i+1)，使得这个字符串的第 I 个字符是辅音，第(i+1)个字符是元音。
**例:**

```
Input :  str = "bazeci"
Output : 3

Input : str = "abu"
Output : 1
```

**算法** :

1.  我们必须找到所有可能的相邻辅音-元音对。
2.  将所有的元音都插入一个集合或散列中，这样我们就可以在恒定时间内检查当前字符是元音还是辅音。
3.  我们对前 n-1 个元素进行循环，检查第 I 个字符是否是辅音，第 i+1 个字符是否是元音。
4.  如果是这样，我们增加计数，否则我们继续到字符串的末尾。

以下是上述方法的实现:

## C++

```
// C++ Program to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the adjacent pairs of
// consonant and vowels in the string
int countPairs(string s)
{
    // Using a set to store the vowels so that
    // checking each character becomes easier
    set<char> st;
    st.insert('a');
    st.insert('e');
    st.insert('i');
    st.insert('o');
    st.insert('u');

    // Variable to store number of
    // consonant-vowel pairs
    int count = 0;

    int n = s.size();

    for (int i = 0; i < n - 1; i++) {

        // If the ith character is not found in the set,
        // means it is a consonant
        // And if the (i+1)th character is found in the set,
        // means it is a vowel
        // We increment the count of such pairs
        if (st.find(s[i]) == st.end() && st.find(s[i + 1]) != st.end())
            count++;
    }

    return count;
}

// Driver Code
int main()
{
    string s = "geeksforgeeks";

    cout << countPairs(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the above approach
import java.util.*;

class Sol
{

// Function to count the adjacent pairs of
// consonant and vowels in the String
static int countPairs(String s)
{
    // Using a set to store the vowels so that
    // checking each character becomes easier
    Set<Character> st=new HashSet<Character>();
    st.add('a');
    st.add('e');
    st.add('i');
    st.add('o');
    st.add('u');

    // Variable to store number of
    // consonant-vowel pairs
    int count = 0;

    int n = s.length();

    for (int i = 0; i < n - 1; i++)
    {

        // If the ith character is not found in the set,
        // means it is a consonant
        // And if the (i+1)th character is found in the set,
        // means it is a vowel
        // We increment the count of such pairs
        if (st.contains(s.charAt(i)) && !st.contains(s.charAt(i + 1)))
            count++;
    }

    return count;
}

// Driver Code
public static void main(String args[])
{
    String s = "geeksforgeeks";

    System.out.println( countPairs(s));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 Program to implement the above approach

# Function to count the adjacent pairs of
# consonant and vowels in the string
def countPairs(s) :

    # Using a set to store the vowels so that
    # checking each character becomes easier
    st = set();
    st.add('a');
    st.add('e');
    st.add('i');
    st.add('o');
    st.add('u');

    # Variable to store number of
    # consonant-vowel pairs
    count = 0;

    n = len(s);

    for i in range(n - 1) :

        # If the ith character is not found in the set,
        # means it is a consonant
        # And if the (i+1)th character is found in the set,
        # means it is a vowel
        # We increment the count of such pairs
        if (s[i] not in st and s[i + 1] in st) :
            count += 1;

    return count;

# Driver Code
if __name__ == "__main__" :

    s = "geeksforgeeks";

    print(countPairs(s));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to count the adjacent pairs of
// consonant and vowels in the String
static int countPairs(String s)
{
    // Using a set to store the vowels so that
    // checking each character becomes easier
    HashSet<char> st = new HashSet<char>();
    st.Add('a');
    st.Add('e');
    st.Add('i');
    st.Add('o');
    st.Add('u');

    // Variable to store number of
    // consonant-vowel pairs
    int count = 0;

    int n = s.Length;

    for (int i = 0; i < n - 1; i++)
    {

        // If the ith character is not found in the set,
        // means it is a consonant
        // And if the (i+1)th character is found in the set,
        // means it is a vowel
        // We increment the count of such pairs
        if (st.Contains(s[i]) && !st.Contains(s[i + 1]))
            count++;
    }

    return count;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "geeksforgeeks";

    Console.Write( countPairs(s));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the adjacent pairs of
// consonant and vowels in the String
function countPairs(s)
{
    // Using a set to store the vowels so that
    // checking each character becomes easier
    let st=new Set();
    st.add('a');
    st.add('e');
    st.add('i');
    st.add('o');
    st.add('u');

    // Variable to store number of
    // consonant-vowel pairs
    let count = 0;

    let n = s.length;

    for (let i = 0; i < n - 1; i++)
    {

        // If the ith character is not found in the set,
        // means it is a consonant
        // And if the (i+1)th character is found in the set,
        // means it is a vowel
        // We increment the count of such pairs
        if (st.has(s[i]) && !st.has(s[i + 1]))
            count++;
    }

    return count;
}

// Driver Code

     let s = "geeksforgeeks";

    document.write( countPairs(s));

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
3
```

**时间复杂度** : O(N)，其中 N 为字符串的长度。
**辅助空间** : O(1)。我们在 Hash 中使用了额外的空间来存储元音，但是因为元音的数量只有 5 个，所以使用的额外空间被认为是恒定的。