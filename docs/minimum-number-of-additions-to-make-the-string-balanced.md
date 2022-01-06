# 使弦平衡的最小添加次数

> 原文:[https://www . geeksforgeeks . org/最少添加次数使字符串平衡/](https://www.geeksforgeeks.org/minimum-number-of-additions-to-make-the-string-balanced/)

给定一个由小写字符组成的字符串 **str** ，任务是找到需要添加到字符串中的最小字符数，以使其平衡。当且仅当每个字符的出现次数相等时，一个字符串被称为是平衡的。
**例:**

> **输入:** str = "geeksforgeeks"
> **输出:** 15
> 加 2 'g '、2 'k '、2 's '、3 'f '、3 'o '和 3 'r '。
> **输入:** str = "abcd"
> **输出:** 0
> 字符串已经平衡。

**方法:**为了尽量减少所需的添加，每个字符的频率必须等于最频繁出现的元素的频率。首先，创建一个频率数组，找出给定字符串中所有字符的频率。现在，所需的答案将是频率数组中每个字符的频率与最大频率的绝对差值之和。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 26

// Function to return the minimum additions
// required to balance the given string
int minimumAddition(string str, int len)
{

    // To store the frequency of
    // the characters of str
    int freq[MAX] = { 0 };

    // Update the frequency of the characters
    for (int i = 0; i < len; i++) {
        freq[str[i] - 'a']++;
    }

    // To store the maximum frequency from the array
    int maxFreq = *max_element(freq, freq + MAX);

    // To store the minimum additions required
    int minAddition = 0;
    for (int i = 0; i < MAX; i++) {

        // Every character's frequency must be
        // equal to the frequency of the most
        // frequently occurring character
        if (freq[i] > 0) {
            minAddition += abs(maxFreq - freq[i]);
        }
    }

    return minAddition;
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int len = str.length();

    cout << minimumAddition(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach 
class GFG 
{
    final static int MAX = 26; 

    static int max_element(int freq[])
    {
        int max_ele = freq[0];
        for(int i = 0; i < MAX; i++)
        {
            if(max_ele < freq[i])
                max_ele = freq[i];
        }
        return max_ele;
    }

    // Function to return the minimum additions 
    // required to balance the given string 
    static int minimumAddition(String str, int len) 
    { 

        // To store the frequency of 
        // the characters of str 
        int freq[] = new int[MAX];

        // Update the frequency of the characters 
        for (int i = 0; i < len; i++) 
        { 
            freq[str.charAt(i) - 'a']++; 
        } 

        // To store the maximum frequency from the array 
        int maxFreq = max_element(freq); 

        // To store the minimum additions required 
        int minAddition = 0; 
        for (int i = 0; i < MAX; i++) 
        { 

            // Every character's frequency must be 
            // equal to the frequency of the most 
            // frequently occurring character 
            if (freq[i] > 0) 
            { 
                minAddition += Math.abs(maxFreq - freq[i]); 
            } 
        } 
        return minAddition; 
    } 

    // Driver code 
    public static void main (String[] args)
    { 
        String str = "geeksforgeeks"; 
        int len = str.length(); 

        System.out.println(minimumAddition(str, len)); 
    } 
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 26

# Function to return the minimum additions
# required to balance the given str1ing
def minimumAddition(str1, Len):

    # To store the frequency of
    # the characters of str1
    freq = [0 for i in range(MAX)]

    # Update the frequency of the characters
    for i in range(Len):
        freq[ord(str1[i]) - ord('a')] += 1

    # To store the maximum frequency from the array
    maxFreq = max(freq)

    # To store the minimum additions required
    minAddition = 0
    for i in range(MAX):

        # Every character's frequency must be
        # equal to the frequency of the most
        # frequently occurring character
        if (freq[i] > 0):
            minAddition += abs(maxFreq - freq[i])

    return minAddition

# Driver code
str1 = "geeksforgeeks"
Len = len(str1)

print(minimumAddition(str1, Len))

# This code is contributed Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG 
{
    static int MAX = 26; 

    static int max_element(int []freq)
    {
        int max_ele = freq[0];
        for(int i = 0; i < MAX; i++)
        {
            if(max_ele < freq[i])
                max_ele = freq[i];
        }
        return max_ele;
    }

    // Function to return the minimum additions 
    // required to balance the given string 
    static int minimumAddition(String str, int len) 
    { 

        // To store the frequency of 
        // the characters of str 
        int []freq = new int[MAX];

        // Update the frequency of the characters 
        for (int i = 0; i < len; i++) 
        { 
            freq[str[i] - 'a']++; 
        } 

        // To store the maximum frequency from the array 
        int maxFreq = max_element(freq); 

        // To store the minimum additions required 
        int minAddition = 0; 
        for (int i = 0; i < MAX; i++) 
        { 

            // Every character's frequency must be 
            // equal to the frequency of the most 
            // frequently occurring character 
            if (freq[i] > 0) 
            { 
                minAddition += Math.Abs(maxFreq - freq[i]); 
            } 
        } 
        return minAddition; 
    } 

    // Driver code 
    public static void Main (String[] args)
    { 
        String str = "geeksforgeeks"; 
        int len = str.Length; 

        Console.WriteLine(minimumAddition(str, len)); 
    } 
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let MAX = 26; 

    function max_element(freq)
    {
        let max_ele = freq[0];
        for(let i = 0; i < MAX; i++)
        {
            if(max_ele < freq[i])
                max_ele = freq[i];
        }
        return max_ele;
    }

    // Function to return the minimum additions 
    // required to balance the given string 
    function minimumAddition(str, len) 
    { 

        // To store the frequency of 
        // the characters of str 
        let freq = new Array(MAX);
        freq.fill(0);

        // Update the frequency of the characters 
        for (let i = 0; i < len; i++) 
        { 
            freq[str[i].charCodeAt() - 'a'.charCodeAt()]++; 
        } 

        // To store the maximum frequency from the array 
        let maxFreq = max_element(freq); 

        // To store the minimum additions required 
        let minAddition = 0; 
        for (let i = 0; i < MAX; i++) 
        { 

            // Every character's frequency must be 
            // equal to the frequency of the most 
            // frequently occurring character 
            if (freq[i] > 0) 
            { 
                minAddition += Math.abs(maxFreq - freq[i]); 
            } 
        } 
        return minAddition; 
    } 

    let str = "geeksforgeeks"; 
    let len = str.length; 

    document.write(minimumAddition(str, len)); 

</script>
```

**Output:** 

```
15
```