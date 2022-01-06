# 包含偶数个元音的最长子串的长度

> 原文:[https://www . geesforgeks . org/包含偶数个元音的最长子串长度/](https://www.geeksforgeeks.org/length-of-the-longest-substring-that-contains-even-number-of-vowels/)

给定一个由 **N** 个小写字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找出由偶数个[个元音](https://www.geeksforgeeks.org/count-the-number-of-vowels-occurred-in-the-substrings-of-given-string/)组成的最长[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的长度。

**示例:**

> **输入:** S= "bcbcbc"
> **输出:** 6
> **解释:**
> 考虑子串 S[0，5]，即“bcbcbc”是最长的子串，因为所有元音:a、e、I、o 和 u 出现 0(为偶数)的次数。
> 
> **输入:**S = " ebbaa "
> T3】输出: 4

**天真方法:**解决给定问题最简单的方法是[从给定的字符串**S**T5】生成所有可能的子串，对于每个子串，检查子串中所有元音的](https://www.geeksforgeeks.org/program-print-substrings-given-string/)[频率是否为偶数](https://www.geeksforgeeks.org/count-the-number-of-vowels-occurred-in-the-substrings-of-given-string/)。如果发现**为真**，则更新所需字符串的最大长度。检查所有子字符串后，打印获得的最大长度。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)进行优化。想法是初始化一个字符串，说大小为 **5** 的 **temp** 对应的 **5** 元音(a，e，I，o，u)全部为 **0s** ，其中 **s[i] = 0** 表示 **i <sup>th</sup>** 元音出现偶数次。现在，遍历给定的字符串，找到字符串的相同状态，从[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中 **temp** 并更新最大长度。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**为 **0** ，存储所需的结果。
*   初始化一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)，称 **5** 大小的**温度**为**“00000”**。
*   创建一个[散列表](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)、 **M** 来存储字符串 **temp** 的出现索引，并将 **M** 中 **temp** 的值初始化为 **-1** 。
*   [使用变量 **i** 在范围**【0，N–1】**内遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** ，并执行以下步骤:
    *   如果字符 **S[i]** 是元音，则更新字符串 **temp** 。
    *   如果字符串 **temp** 在地图 **M** 中为[，则将地图 **M** 中的值存储在变量 **X** 中，并将 **ans** 的值更新为 **ans** 和**(I–X)**的最大值。](https://www.geeksforgeeks.org/check-key-present-cpp-map-unordered_map/)
    *   否则，将地图 **M** 中**温度**的值更新为 **i** 。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest substring having even number
// of vowels
int longestSubstring(string s)
{
    // Create two hashmaps
    unordered_map<string, int> indexes;
    unordered_map<char, int> chars(
        { { 'a', 0 }, { 'e', 1 },
          { 'i', 2 }, { 'o', 3 },
          { 'u', 4 } });

    // Keep the track of frequencies
    // of the vowels
    string evenOdd = "00000";
    indexes[evenOdd] = -1;

    // Stores the maximum length
    int length = 0;

    // Traverse the given string S
    for (int i = 0; i < s.size(); ++i) {

        char c = s[i];

        // Find character in the map
        auto it = chars.find(c);

        // If it is a vowel, then update
        // the frequency
        if (it != chars.end()) {
            evenOdd[it->second]
                = evenOdd[it->second]
                          == '0'
                      ? '1'
                      : '0';
        }

        // Find the index of occurence
        // of the string evenOdd in map
        auto lastIndex = indexes.find(evenOdd);

        if (lastIndex == indexes.end()) {
            indexes[evenOdd] = i;
        }

        // Update the maximum length
        else {
            length = max(
                length, i - lastIndex->second);
        }
    }

    // Print the maximum length
    cout << length;
}

// Driver Code
int main()
{
    string S = "bcbcbc";
    longestSubstring(S);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of the
# longest substring having even number
# of vowels
def longestSubstring(s):

    # Create two hashmaps
    indexes = {}
    chars = {}
    chars['a'] = 0
    chars['e'] = 1
    chars['i'] = 2
    chars['o'] = 3
    chars['u'] = 4

    # Keep the track of frequencies
    # of the vowels
    evenOdd = "00000"
    evenOdd = [i for i in evenOdd]
    indexes["".join(evenOdd)] = -1

    # Stores the maximum length
    length = 0

    # Traverse the given string S
    for i in range(len(s)):
        c = s[i]

        # Find character in the map

        # If it is a vowel, then update
        # the frequency
        if (c in chars):
            evenOdd[chars[it]] = '1' if evenOdd[chars[it]] else '0'

        # Find the index of occurence
        # of the string evenOdd in map
        if ("".join(evenOdd) not in indexes):
            indexes["".join(evenOdd)] = i

        # Update the maximum length
        else:
            length = max(
                length, i - indexes["".join(evenOdd)])

    # Print the maximum length
    print(length)

# Driver Code
if __name__ == '__main__':

    S = "bcbcbc"

    longestSubstring(S)

# This code is contributed by mohit kumar 29
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)