# 查找字符串 S 的另一个子串的所有子串的字谜

> 原文:[https://www . geesforgeks . org/find-all-substrings-即字符串中另一个子字符串的字谜/](https://www.geeksforgeeks.org/find-all-substrings-that-are-anagrams-of-another-substring-of-the-string-s/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是[找到字符串**S**T7】中的所有子字符串，这是字符串 **S** 中另一个不同子字符串的](https://www.geeksforgeeks.org/program-print-substrings-given-string/)[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。不同的子字符串意味着子字符串从不同的索引开始。

**示例:**

> **输入:** S = "aba"
> **输出:** a a ab ba
> **解释:**
> 以下子串是字符串 S 的另一个子串的字谜:
> 
> 1.  **“a”:**子串“a”是子串“a”的字谜(= {S[0]})。
> 2.  **“a”:**子串“a”是子串“a”的字谜(= {S[2]})。
> 3.  **“ab”:**子串“ab”是子串“ba”的字谜(= {S[1]，S[2]})。
> 4.  **“ba”:**子串“ba”是子串“ab”的字谜(= {S[0]，S[2]})。
> 
> **输入:**S = " ABCD "
> T3】输出: []

**方法:**通过存储字符串 **S** 的每个子串的[字谜并打印结果子串，使用](https://www.geeksforgeeks.org/count-total-anagram-substrings/)[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)可以解决给定的问题。按照以下步骤解决给定的问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，存储字符串 **S** 每个子串的所有字谜。
*   [生成 S](https://www.geeksforgeeks.org/program-print-substrings-given-string/) 的所有可能的子串，对于每个子串，说 **str** 将子串存储在映射了关键字的 HashMap 中作为排序后的字符串 **str** 。
*   [遍历 HashMap](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/) 并打印与每个键关联的所有字符串，每个字符串关联的字符串数至少为**1**。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach

import collections

# Function to find all the substrings
# whose anagram exist as a different
# substring in S
def findAnagrams(S):

    # Stores the lists of anagrams of
    # each substring of S
    Map = collections.defaultdict(list)

    # Stores the length of S
    N = len(S)

    # Generate all substrings of S
    for i in range(N):
        for j in range(i, N):

            # Store the current substring
            # of the string S
            curr = S[i: j + 1]

            # Key is the sorted substring
            key = "".join(sorted(curr))

            # Add the sorted substring
            # to the dictionary
            Map[key].append(curr)

    # Store the final result
    result = []

    # Iterate over values of dictionary
    for vals in Map.values():

        # If length of list > 1
        if len(vals) > 1:

            # Print all the strings
            for v in vals:
                  print(v, end =" ")   

# Driver Code

S = "aba"
findAnagrams(S)
```

**Output:** 

```
ab ba a a
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*