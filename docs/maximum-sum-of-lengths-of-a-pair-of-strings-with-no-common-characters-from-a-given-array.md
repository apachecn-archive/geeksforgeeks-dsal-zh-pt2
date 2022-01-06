# 给定数组中没有公共字符的一对字符串的最大长度总和

> 原文:[https://www . geesforgeks . org/给定数组中没有公共字符的字符串对的最大长度总和/](https://www.geeksforgeeks.org/maximum-sum-of-lengths-of-a-pair-of-strings-with-no-common-characters-from-a-given-array/)

给定一个由 **N** [字符串](https://www.geeksforgeeks.org/string-data-structure/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为所有唯一的对 **(i，j)** 找到字符串[长度的最大和](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)**arr【I】**和**arr【j】**，其中字符串**arr【I】**和**arr【j】**不包含公共

**示例:**

> **输入:**arr[]=[“abcd”、“cat”、“lto”、“car”、“wxyz”、“abcdef”]
> **输出:** 8
> **解释:**
> 字符串“ABCD”和“wxyz”中没有共同的字符。因此，两个字符串的长度之和= 4 + 4 = 8，这在所有可能的对中是最大的。
> 
> **输入:**arr[]=[“ABCD”、“def”、“fghi”、“ijklm”]
> **输出:** 8

**天真方法:**解决给定问题的最简单方法是[生成字符串数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，并打印出字符串对的[长度之和](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)的最大值，这些字符串对之间没有[共同的字符](https://www.geeksforgeeks.org/check-if-there-is-any-common-character-in-two-given-strings/)。

***时间复杂度:** O(N <sup>2</sup> * M)，其中 **M** 为字符串* *的最大* [*长度。*
***辅助空间:** O(M)*](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)

**高效方法:**上述方法也可以利用[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)的思想进行优化。其思想是将每个字符串转换成其等效的[位掩码整数](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)，然后找到没有共同字符的字符串对，其长度之和最大。按照以下步骤解决问题:

*   [初始化一个大小为 **N** 的向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **掩码**，以将[字符串的](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)[位“或”位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)存储在[数组](https://www.geeksforgeeks.org/array-data-structure/)中，该数组由[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **字构成。**
*   将变量**最大长度**初始化为 **0** 存储答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，其中 **M** 是[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)的长度，并将**掩码【I】**的值设置为**掩码【I】| 1<<(单词【I】【j】–‘a’)**。
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，I】**，如果**掩码【I】**和**掩码【j】**的值[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)不是 **0** ，则将**最大长度**的值设置为**最大长度**或**字【I】的最大值。length() +字数[j]。长度()**。
*   完成上述步骤后，打印**最大长度**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// length of pair of strings having
// no common characters
int maxSum(vector<string>& words)
{
    // Stores the bitmask of each strings
    vector<int> mask(words.size());

    // Initialize the result as zero
    int result = 0;

    // Iterate the given vector
    for (int i = 0; i < words.size(); ++i) {

        // For each of character
        for (char c : words[i]) {

            // If the ith value of
            // mask |= 1 left shift
            // that character - a
            mask[i] |= 1 << (c - 'a');
        }

        // Check for eack ith character,
        // if the ith and jth value of
        // mask are not same, then add
        // and maximize them
        for (int j = 0; j < i; ++j) {
            if (!(mask[i] & mask[j])) {
                result
                    = max(result, int(words[i].size()
                                      + words[j].size()));
            }
        }
    }

    // Return maximum sum of lengths
    // of strings
    return result;
}

// Driver Code
int main()
{
    vector<string> words = { "abcd", "def",
                             "fghi", "ijklm" };
    cout << maxSum(words);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the maximum sum of
    // length of pair of strings having
    // no common characters
    public static int maxSum(String[] words) {
        // Stores the bitmask of each strings
        int[] mask = new int[words.length];

        // Initialize the result as zero
        int result = 0;

        // Iterate the given vector
        for (int i = 0; i < words.length; ++i) {

            // For each of character
            for (char c : words[i].toCharArray()) {

                // If the ith value of
                // mask |= 1 left shift
                // that character - a
                mask[i] |= 1 << (c - 'a');
            }

            // Check for eack ith character,
            // if the ith and jth value of
            // mask are not same, then add
            // and maximize them
            for (int j = 0; j < i; ++j) {
                if ((mask[i] & mask[j]) < 1) {
                    result = Math.max(result, (int) words[i].length() + words[j].length());
                }
            }
        }

        // Return maximum sum of lengths
        // of strings
        return result;
    }

    // Driver Code
    public static void main(String args[]) {
        String[] words = { "abcd", "def", "fghi", "ijklm" };
        System.out.println(maxSum(words));

    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Function to find the maximum sum of
# length of pair of strings having
# no common characters
def maxSum(words):

    # Stores the bitmask of each strings
    mask = [0]*len(words)

    # Initialize the result as zero
    result = 0

        # Iterate the given vector
    for i in range(len(words)):
        for c in words[i]:

            # If the ith value of
            # mask |= 1 left shift
            # that character - a
            mask[i] |= 1 << (ord(c)-97)

         #  Check for eack ith character,
        # if the ith and jth value of
        # mask are not same, then add
        # and maximize them
        for j in range(i):
            if not(mask[i] & mask[j]):
                result = max(result, len(words[i])+len(words[j]))

     # Return maximum sum of lengths
    # of strings           
    return result

# Driver code
words = ["abcd", "def", "fghi", "ijklm"]
print(maxSum(words))

# This code is contributed by Parth Manchanda
```

## C#

```
using System;

public class GFG {

    public static int maxSum(String[] words)
    {
        // Stores the bitmask of each strings
        int[] mask = new int[words.Length];

        // Initialize the result as zero
        int result = 0;

        // Iterate the given vector
        for (int i = 0; i < words.Length; ++i) {

            // For each of character
            foreach  (char c in words[i]) {

                // If the ith value of
                // mask |= 1 left shift
                // that character - a
                mask[i] |= 1 << (c - 'a');
            }

            // Check for eack ith character,
            // if the ith and jth value of
            // mask are not same, then add
            // and maximize them
            for (int j = 0; j < i; ++j) {
                if ((mask[i] & mask[j]) < 1) {
                    result = Math.Max(
                        result, (int)words[i].Length
                                    + words[j].Length);
                }
            }
        }

        // Return maximum sum of lengths
        // of strings
        return result;
    }

    static public void Main()
    {
        String[] words = { "abcd", "def", "fghi", "ijklm" };
        Console.WriteLine(maxSum(words));
    }
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum sum of
// length of pair of strings having
// no common characters
function maxSum(words)
{

    // Stores the bitmask of each strings
    let mask = new Array(words.length);

    // Initialize the result as zero
    let result = 0;

    // Iterate the given vector
    for(let i = 0; i < words.length; ++i)
    {

        // For each of character
        for(let c = words[i]; c < words[i].length; c++)
        {

            // If the ith value of
            // mask |= 1 left shift
            // that character - a
            mask[i] |= 1 << (words[i].charCodeAt(0) -
                                  'a'.charCodeAt(0));
        }

        // Check for eack ith character,
        // if the ith and jth value of
        // mask are not same, then add
        // and maximize them
        for(let j = 0; j < i; ++j)
        {
            if (!(mask[i] & mask[j]))
            {
                result = Math.max(result, words[i].length +
                                          words[j].length);
            }
        }
    }

    // Return maximum sum of lengths
    // of strings
    return result;
}

// Driver Code
let words = [ "abcd", "def",
              "fghi", "ijklm" ];

document.write(maxSum(words));

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(max(N*M，N <sup>2</sup> )，其中 M 为弦* *的最大* [*长度。*
***辅助空间:** O(N)*](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)