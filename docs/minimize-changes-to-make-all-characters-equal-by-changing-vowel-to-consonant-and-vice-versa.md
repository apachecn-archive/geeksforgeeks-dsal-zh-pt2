# 通过将元音改为辅音，使所有字符相等，反之亦然

> 原文:[https://www . geesforgeks . org/minimum-changes-to-make-all-characters-equal-by-change-元音-辅音-反之亦然/](https://www.geeksforgeeks.org/minimize-changes-to-make-all-characters-equal-by-changing-vowel-to-consonant-and-vice-versa/)

给定一个由小写字符组成的字符串**str[]**，任务是使该字符串的所有字符在最少的操作次数下相等，以便在每个操作中要么选择一个元音，然后将其更改为辅音，要么相反。

**示例:**

> **输入:**str[]=“geeksforgeeks”
> **输出:** 10
> **解释:**要使所有字符相等，请进行以下更改–
> 
> 1.  把“o”改成辅音(比如说“z”)，然后再改成“e”
> 2.  将每隔一个辅音(' g '，' k '，' s '，' f '，' r '，)改为' e '
> 
> 这导致字符串 str = " eeeeeeeeeeeee "并且执行的操作总数是 10。
> 
> **输入:** str[] =【编码】
> T3】输出: 6

**做法:**从问题中可以推导出，为了将辅音变成元音，需要 1 次操作，为了将元音变成元音或者将辅音变成辅音，需要 2 个步骤，因为在将元音变成元音的情况下，需要将元音变成辅音，然后再次变回元音，或者在将辅音变成辅音的情况下，需要将辅音变成元音，然后再次变回辅音。这个想法是保持两个变量——

*   **Cv** =将所有字符更改为最大出现元音的成本=辅音数量+(元音总数–最大出现元音的频率)* 2
*   **Cc** = 将所有字符更改为最大出现辅音的成本=元音数量+(辅音总数–最大出现辅音的频率)* 2

现在这两个中的最小值，即 **min(Cv，Cc)** 将给出我们可以变换字符串所需的最小步数。按照以下步骤解决问题:

*   将变量 **ans、元音**和**辅音**初始化为 **0** 存储答案、元音数和辅音数。
*   将两个变量**max _ 元音**和**max _ 辅音**初始化为 **INT_MIN** ，找出给定字符串中最大出现元音和最大出现辅音。
*   [初始化 2 个无序 _map < char，int>](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)**freq _ 元音[]****freq _ 辅音[]** 存储元音和辅音的频率。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下步骤:
    *   如果当前字符是元音，则通过 **1** 增加**元音**的数量，通过 **1** 增加其在地图中的频率，否则对辅音进行。
*   [遍历两个无序映射](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，找到最大出现的元音和辅音。
*   使用上述公式，计算 **ans。**
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of steps to make all characters equal
int operations(string s)
{

    // Initializing the variables
    int ans = 0;
    int vowels = 0, consonants = 0;
    int max_vowels = INT_MIN;
    int max_consonants = INT_MIN;

    // Store the frequency
    unordered_map<char, int> freq_consonants;
    unordered_map<char, int> freq_vowels;

    // Iterate over the string
    for (int i = 0; i < s.size(); i++) {
        if (s[i] == 'a' or s[i] == 'e' or s[i] == 'i'
            or s[i] == 'o' or s[i] == 'u') {

            // Calculate the total
            // number of vowels
            vowels += 1;

            // Storing frequency of
            // each vowel
            freq_vowels[s[i]] += 1;
        }
        else {

            // Count the consonants
            consonants += 1;

            // Storing the frequency of
            // each consonant
            freq_consonants[s[i]] += 1;
        }
    }

    // Iterate over the 2 maps
    for (auto it = freq_consonants.begin();
         it != freq_consonants.end(); it++) {

        // Maximum frequency of consonant
        max_consonants = max(
            max_consonants,
            it->second);
    }
    for (auto it = freq_vowels.begin();
         it != freq_vowels.end(); it++) {

        // Maximum frequency of vowel
        max_vowels
            = max(max_vowels,
                  it->second);
    }

    // Find the result
    ans = min((2 * (vowels - max_vowels)
               + consonants),
              (2 * (consonants - max_vowels)
               + consonants));

    return ans;
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";
    cout << operations(S);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys
from collections import defaultdict

# Function to find the minimum number
# of steps to make all characters equal
def operations(s):

    # Initializing the variables
    ans = 0
    vowels = 0
    consonants = 0
    max_vowels = -sys.maxsize-1
    max_consonants = -sys.maxsize-1

    # Store the frequency
    freq_consonants = defaultdict(int)
    freq_vowels = defaultdict(int)

    # Iterate over the string
    for i in range(len(s)):
        if (s[i] == 'a' or s[i] == 'e' or s[i] == 'i'
                or s[i] == 'o' or s[i] == 'u'):

            # Calculate the total
            # number of vowels
            vowels += 1

            # Storing frequency of
            # each vowel
            freq_vowels[s[i]] += 1

        else:

            # Count the consonants
            consonants += 1

            # Storing the frequency of
            # each consonant
            freq_consonants[s[i]] += 1

    # Iterate over the 2 maps
    for it in freq_consonants:

        # Maximum frequency of consonant
        max_consonants = max(
            max_consonants,
            freq_consonants[it])

    for it in freq_vowels:

        # Maximum frequency of vowel
        max_vowels = max(max_vowels,
                         freq_vowels[it])

    # Find the result
    ans = min((2 * (vowels - max_vowels)
               + consonants),
              (2 * (consonants - max_vowels)
               + consonants))

    return ans

# Driver Code
if __name__ == "__main__":

    S = "geeksforgeeks"
    print(operations(S))

    # This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum number
        // of steps to make all characters equal
        function operations(s) {

            // Initializing the variables
            let ans = 0;
            let vowels = 0, consonants = 0;
            let max_vowels = Number.MIN_VALUE;
            let max_consonants = Number.MIN_VALUE;

            // Store the frequency
            let freq_consonants = new Map();
            let freq_vowels = new Map();

            // Iterate over the string
            for (let i = 0; i < s.length; i++)
            {
                if (s.charAt(i) == 'a' || s.charAt(i) == 'e' || s.charAt(i) == 'i'
                    || s.charAt(i) == 'o' || s.charAt(i) == 'u') {

                    // Calculate the total
                    // number of vowels
                    vowels += 1;

                    // Storing frequency of
                    // each vowel
                    if (freq_vowels.has(s.charAt(i))) {
                        freq_vowels.set(s.charAt(i), freq_vowels.get(s.charAt(i)) + 1)
                    }
                    else {
                        freq_vowels.set(s.charAt(i), 1);
                    }

                }
                else {

                    // Count the consonants
                    consonants += 1;

                    // Storing the frequency of
                    // each consonant
                    if (freq_consonants.has(s.charAt(i))) {
                        freq_consonants.set(s.charAt(i), freq_consonants.get(s.charAt(i)) + 1)
                    }
                    else {
                        freq_consonants.set(s.charAt(i), 1);
                    }

                }
            }

            // Iterate over the 2 maps
            for (let [key, value] of freq_consonants) {

                // Maximum frequency of consonant
                max_consonants = Math.max(
                    max_consonants,
                    value);
            }
            for (let [key1, value1] of freq_vowels) {

                // Maximum frequency of vowel
                max_vowels
                    = Math.max(max_vowels,
                        value1);
            }

            // Find the result
            ans = Math.min((2 * (vowels - max_vowels)
                + consonants),
                (2 * (consonants - max_vowels)
                    + consonants));

            return ans;
        }

        // Driver Code
        let S = "geeksforgeeks";
        document.write(operations(S));

     // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)