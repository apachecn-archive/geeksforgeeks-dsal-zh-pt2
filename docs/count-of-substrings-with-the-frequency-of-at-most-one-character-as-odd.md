# 最多一个字符频率为奇数的子串计数

> 原文:[https://www . geesforgeks . org/最多一个字符为奇数的子字符串计数/](https://www.geeksforgeeks.org/count-of-substrings-with-the-frequency-of-at-most-one-character-as-odd/)

给定一个由 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/stdstring-class-in-c/) **S** ，任务是计算非空[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的总数，使得最多一个字符出现奇数次。

**例**:

> **输入** : S = "aba"
> **输出** : 4
> **解释**:有效子串为“a”、“b”、“a”和“aba”。因此，所需子字符串的总数为 4。
> 
> **输入**:【aabb】
> **输出** : 9
> **解释**:有效子串为“a”、“aa”、“aab”、“AABB”、“a”、“abb”、“b”、“bb”和“b”。

**逼近**:上述问题可以借助[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)使用[hashmap](https://www.geeksforgeeks.org/hashing-data-structure/)解决。按照以下步骤解决问题:

*   每个字符的[频率的奇偶校验可以存储在位掩码**掩码**中，其中**T5**I<sup>th</sup>T9】字符由**2<sup>I</sup>T13】表示。最初**掩码的值= 0** 。******](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)
*   创建一个[无序图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) **可见**，存储每个位掩码的出现频率。最初，**的值见【0】= 1**。
*   创建一个变量 **cnt** ，它存储有效子串的计数。最初， **cnt 的值= 0** 。
*   [对范围【0，N】](https://www.geeksforgeeks.org/range-based-loop-c/)和[中的每个 **i** 用代表字符串的第 **i <sup>个</sup>** 字符的整数对掩码值进行逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，并将 **cnt** 的值递增**所见【掩码】**。
*   对于每个有效的 **i** ，遍历**【a，z】**范围内的所有字符，通过翻转当前掩码中的 **j <sup>第</sup>T7】设置位来增加其频率，并在翻转 **j <sup>第</sup>T13】设置位后，通过位掩码的频率来增加 **cnt** 的值。****
*   存储在 **cnt** 中的值是要求的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of substrings
// such that at most one character occurs
// odd number of times
int uniqueSubstrings(string S)
{
    // Stores the frequency of the bitmasks
    unordered_map<int, int> seen;

    // Initial Condition
    seen[0] = 1;

    // Store the current value of the bitmask
    int mask = 0;

    // Stores the total count of the
    // valid substrings
    int cnt = 0;

    for (int i = 0; i < S.length(); ++i) {

        // XOR the mask with current character
        mask ^= (1 << (S[i] - 'a'));

        // Increment the count by mask count
        // of strings with all even frequencies
        cnt += seen[mask];

        for (int j = 0; j < 26; ++j) {
            // Increment count by mask count
            // of strings if exist with the
            // jth character having odd frequency
            cnt += seen[mask ^ (1 << j)];
        }
        seen[mask]++;
    }

    // Return Answer
    return cnt;
}

// Driver Code
int main()
{
    string word = "aabb";
    cout << uniqueSubstrings(word);

    return 0;
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the count of substrings
// such that at most one character occurs
// odd number of times
static int uniqueSubstrings(string S)
{

    // Stores the frequency of the bitmasks
    Dictionary<int,
               int> seen = new Dictionary<int,
                                          int>();

    // Initial Condition
    seen[0] = 1;

    // Store the current value of the bitmask
    int mask = 0;

    // Stores the total count of the
    // valid substrings
    int cnt = 0;

    for(int i = 0; i < S.Length; ++i)
    {

        // XOR the mask with current character
        mask ^= (1 << (S[i] - 'a'));

        // Increment the count by mask count
        // of strings with all even frequencies
        if (seen.ContainsKey(mask))
            cnt += seen[mask];

        for(int j = 0; j < 26; ++j)
        {

            // Increment count by mask count
            // of strings if exist with the
            // jth character having odd frequency
            if (seen.ContainsKey(mask ^ (1 << j)))
                cnt += seen[mask ^ (1 << j)];
        }
        if (seen.ContainsKey(mask))
            seen[mask]++;
        else
            seen[mask] = 1;
    }

    // Return Answer
    return cnt;
}

// Driver Code
public static void Main()
{
    string word = "aabb";

    Console.WriteLine(uniqueSubstrings(word));
}
}

// This code is contributed by ukasp
```

**Output:** 

```
9
```

***时间复杂度** : O(N)*
***辅助空间** : O(N)*