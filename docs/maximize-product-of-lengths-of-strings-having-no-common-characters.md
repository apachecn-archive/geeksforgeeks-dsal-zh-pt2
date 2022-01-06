# 最大化没有共同字符的字符串长度的乘积

> 原文:[https://www . geeksforgeeks . org/最大化无公共字符字符串长度的乘积/](https://www.geeksforgeeks.org/maximize-product-of-lengths-of-strings-having-no-common-characters/)

给定由 **N** [串](https://www.geeksforgeeks.org/string-data-structure/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为所有唯一的对 **(i，j)** 找到串[长度的最大乘积](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)**arr【I】**和**arr【j】**，其中串**arr【I】**和**arr【j】**不包含

**示例:**

> **输入:**arr[]= {“abcw”、“baz”、“foo”、“bar”、“xtfn”、“abcdef”}
> **输出:** 16
> **解释:**字符串“abcw”和“xtfn”中没有共同的字符。因此，两个字符串长度的乘积= 4 * 4 = 16，这在所有可能的对中是最大的。
> 
> **输入:**arr[]= {“a”、“aa”、“aaa”、“AAAA”}
> T3】输出: 0

**天真方法:**解决给定问题的最简单方法是[生成字符串数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，并打印字符串长度[的乘积的最大值](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)对之间没有共同字符。

***时间复杂度:** O(N <sup>2</sup> * M)，其中 **M** 为字符串* *的最大* [*长度。*
***辅助空间:** O(M)*](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)

**高效方法:**上述方法也可以通过将每个字符串转换为其[位掩码整数等价物](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)来优化。按照以下步骤解决问题:

*   初始化一个变量，说出**答案**，该变量存储无公共字符的[对字符串长度的最大乘积](https://www.geeksforgeeks.org/count-common-characters-in-two-strings/)。
*   初始化[数组](https://www.geeksforgeeks.org/array-data-structure/) **位[]** ，存储数组 **arr[]** 中所有给定字符串的整数等价物。
*   [在范围**【0，N–1】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于字符串**arr【I】**中的每个字符 **ch** ，将**位【I】**更新为**位【I】**和**(1<<(arr【I】–‘a’)**的[位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。
*   现在，[生成所有可能的数组对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **位[]** ，并执行以下步骤:
    *   如果**位【I】**和**位**的[位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为 **0** ，则将**答案**的值更新为**答案**的最大值和**位【I】**和**位【j】**中设置位的[计数的乘积。
        否则，检查下一个可能的配对。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
*   完成以上步骤后，打印**答案**中的值作为最终最大乘积。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to count the number
// of set bits in the integer n
int countSetBits(int n)
{

    // Stores the count
    // of set bits in n
    int count = 0;

    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }

    // Return the count
    return count;
}

// Function to find the maximum
// product of pair of strings
// having no common characters
void maximumProduct(vector<string> words)
{

    // Stores the integer
    // equivalent of the strings
    vector<int> bits(words.size(), 0);

    // Traverse the array of strings
    for(int i = 0; i < words.size(); i++)
    {

        // Traverse the current string
        for(int j = 0; j < words[i].length(); j++)
        {

            // Store the current bit
            // position in bits[i]
            bits[i] = bits[i] | 1 << (words[i][j] - 'a');
        }
    }

    // Store the required result
    int result = 0;

    // Traverse the array, bits[]
    // to get all unique pairs (i, j)
    for(int i = 0; i < bits.size(); i++)
    {
        for(int j = i + 1; j < bits.size(); j++)
        {

            // Check whether the strings
            // have no common characters
            if ((bits[i] & bits[j]) == 0)
            {
                int L = countSetBits(bits[i]);
                int R = countSetBits(bits[j]);

                // Update the overall
                // maximum product
                result = max(L * R, result);
            }
        }
    }

    // Print the maximum product
    cout << result;
}

// Driver Code
int main()
{
    vector<string> arr = { "abcw", "baz", "foo",
                           "bar", "xtfn", "abcdef" };
    maximumProduct(arr);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to count the number
    // of set bits in the integer n
    public static int countSetBits(int n)
    {
        // Stores the count
        // of set bits in n
        int count = 0;

        while (n > 0) {
            count += n & 1;
            n >>= 1;
        }

        // Return the count
        return count;
    }

    // Function to find the maximum
    // product of pair of strings
    // having no common characters
    public static void maximumProduct(
        String[] words)
    {
        // Stores the integer
        // equivalent of the strings
        int[] bits = new int[words.length];

        // Traverse the array of strings
        for (int i = 0;
             i < words.length; i++) {

            // Traverse the current string
            for (int j = 0;
                 j < words[i].length();
                 j++) {

                // Store the current bit
                // position in bits[i]
                bits[i] = bits[i]
                          | 1 << (words[i].charAt(j)
                                  - 'a');
            }
        }

        // Store the required result
        int result = 0;

        // Traverse the array, bits[]
        // to get all unique pairs (i, j)
        for (int i = 0;
             i < bits.length; i++) {

            for (int j = i + 1;
                 j < bits.length; j++) {

                // Check whether the strings
                // have no common characters
                if ((bits[i] & bits[j]) == 0) {

                    int L = countSetBits(
                        bits[i]);
                    int R = countSetBits(
                        bits[j]);

                    // Update the overall
                    // maximum product
                    result
                        = Math.max(L * R, result);
                }
            }
        }

        // Print the maximum product
        System.out.println(result);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String arr[] = { "abcw", "baz",
                         "foo", "bar",
                         "xtfn", "abcdef" };
        maximumProduct(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number
# of set bits in the integer n
def countSetBits(n):

    # Stores the count
    # of set bits in n
    count = 0

    while (n > 0):
        count += n & 1
        n >>= 1

    # Return the count
    return count

# Function to find the maximum
# product of pair of strings
# having no common characters
def maximumProduct(words):

    # Stores the integer
    # equivalent of the strings
    bits = [0 for i in range(len(words))]

    # Traverse the array of strings
    for i in range(len(words)):

        # Traverse the current string
        for j in range(len(words[i])):

            # Store the current bit
            # position in bits[i]
            bits[i] = bits[i] | 1 << (ord(words[i][j]) - 97)

    # Store the required result
    result = 0

    # Traverse the array, bits[]
    # to get all unique pairs (i, j)
    for i in range(len(bits)):
        for j in range(i + 1, len(bits)):

            # Check whether the strings
            # have no common characters
            if ((bits[i] & bits[j]) == 0):
                L = countSetBits(bits[i])
                R = countSetBits(bits[j])

                # Update the overall
                # maximum product
                result = max(L * R, result)

    # Print the maximum product
    print(result)

# Driver Code
if __name__ == '__main__':

    arr = [ "abcw", "baz", "foo",
            "bar", "xtfn", "abcdef" ]
    maximumProduct(arr)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

        // Function to count the number
    // of set bits in the integer n
    public static int countSetBits(int n)
    {

        // Stores the count
        // of set bits in n
        int count = 0;

        while (n > 0) {
            count += n & 1;
            n >>= 1;
        }

        // Return the count
        return count;
    }

    // Function to find the maximum
    // product of pair of strings
    // having no common characters
    public static void maximumProduct(
        string[] words)
    {

        // Stores the integer
        // equivalent of the strings
        int[] bits = new int[words.Length];

        // Traverse the array of strings
        for (int i = 0;
             i < words.Length; i++)
        {

            // Traverse the current string
            for (int j = 0;
                 j < words[i].Length;
                 j++) {

                // Store the current bit
                // position in bits[i]
                bits[i] = bits[i]
                          | 1 << (words[i][j]
                                  - 'a');
            }
        }

        // Store the required result
        int result = 0;

        // Traverse the array, bits[]
        // to get all unique pairs (i, j)
        for (int i = 0;
             i < bits.Length; i++) {

            for (int j = i + 1;
                 j < bits.Length; j++) {

                // Check whether the strings
                // have no common characters
                if ((bits[i] & bits[j]) == 0) {

                    int L = countSetBits(
                        bits[i]);
                    int R = countSetBits(
                        bits[j]);

                    // Update the overall
                    // maximum product
                    result
                        = Math.Max(L * R, result);
                }
            }
        }

        // Print the maximum product
        Console.WriteLine(result);
    }

  // Driver code
    static public void Main (){
    string[] arr = { "abcw", "baz",
                         "foo", "bar",
                         "xtfn", "abcdef" };
        maximumProduct(arr);
    }
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the number
// of set bits in the integer n
function countSetBits(n) {

    // Stores the count
    // of set bits in n
    let count = 0;

    while (n > 0) {
        count += n & 1;
        n >>= 1;
    }

    // Return the count
    return count;
}

// Function to find the maximum
// product of pair of strings
// having no common characters
function maximumProduct(words) {

    // Stores the integer
    // equivalent of the strings
    let bits = new Array(words.length).fill(0);

    // Traverse the array of strings
    for (let i = 0; i < words.length; i++) {

        // Traverse the current string
        for (let j = 0; j < words[i].length; j++) {

            // Store the current bit
            // position in bits[i]
            bits[i] = bits[i] | 1 <<
                    (words[i][j].charCodeAt(0) - 'a'.charCodeAt(0));
        }
    }

    // Store the required result
    let result = 0;

    // Traverse the array, bits[]
    // to get all unique pairs (i, j)
    for (let i = 0; i < bits.length; i++) {
        for (let j = i + 1; j < bits.length; j++) {

            // Check whether the strings
            // have no common characters
            if ((bits[i] & bits[j]) == 0) {
                let L = countSetBits(bits[i]);
                let R = countSetBits(bits[j]);

                // Update the overall
                // maximum product
                result = Math.max(L * R, result);
            }
        }
    }

    // Print the maximum product
    document.write(result);
}

// Driver Code

let arr = ["abcw", "baz", "foo",
    "bar", "xtfn", "abcdef"];
maximumProduct(arr);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
16
```

***时间复杂度:** O(N <sup>2</sup> ，其中 M 为字符串* *的最大* [*长度。*
***辅助空间:** O(N)*](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)