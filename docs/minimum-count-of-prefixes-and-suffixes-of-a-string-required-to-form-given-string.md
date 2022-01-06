# 形成给定字符串所需的字符串前缀和后缀的最小数量

> 原文:[https://www . geeksforgeeks . org/字符串构成给定字符串所需的最小前缀和后缀数/](https://www.geeksforgeeks.org/minimum-count-of-prefixes-and-suffixes-of-a-string-required-to-form-given-string/)

给定两个[字符串](https://www.geeksforgeeks.org/python-strings/) **str1** 和 **str2，**任务是找到构成字符串 **str1 所需的[前缀](https://www.geeksforgeeks.org/check-if-a-string-starts-with-any-of-the-given-prefixes-in-java/)和[后缀](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/) 的最小数量。**如果任务不可能，返回“-1”。

**示例:**

> **输入**:str 1 =“hello world”，str2 =“owordhell”
> **输出** : 2
> **解释**:以上字符串可以组成“HELLOWORLD”，是字符串 str 2 的后缀和前缀
> 
> **输入** : str = "GEEKSFORGEEKS "，wrd = " sforzek "
> **输出** : 3
> **解释**:【geek "+" sforzek+" s "

**逼近**:上述问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/array-class-c/) **dp** ，其中第 I 个元素**arr【I】**将存储形成前缀索引 **i** 所需的最小连接
*   将 **dp** 数组的**DP【0】= 0**和其他值初始化为 **-1**
*   初始化一个[HashSet](https://www.geeksforgeeks.org/hashset-in-java/)T2 设置
*   从左到右迭代字符串 **str1** ，在每个索引 **i** :
    *   将[子串](https://www.geeksforgeeks.org/substring-in-java/)从索引 0 添加到当前索引 **i** 到 HashSet **集合**
*   从右到左，在每个索引处重复字符串**str 1****I**:
    *   将[子串](https://www.geeksforgeeks.org/substring-in-java/)从索引 **i** 到结束索引添加到 HashSet **集合**
*   检查字符串 **str1** 中的所有子字符串，并相应地更新 **dp、**
*   最终答案将存储在**DP【N】、**中，其中 **N** 是字符串 **str1** 的长度

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of
// concatenation of prefix and suffix
// of str2 to make str1
int partCount(string str1, string str2)
{

    // Initialize a set
    unordered_set<string> set;

    // Initialize a temporary string
    string temp = "";

    int l1 = str1.length(), l2 = str2.length();

    // Iterate the string str2
    // from left to right
    for (int i = 0; i < l2; i++) {

        // Add current character
        // to string temp
        temp += str2[i];

        // Insert the prefix into hashset
        set.insert(temp);
    }

    // Re-initialize temp string
    // to empty string
    temp = "";

    // Iterate the string in reverse direction
    for (int i = l2 - 1; i >= 0; i--) {

        // Add current character to temp
        temp += str2[i];

        // Reverse the string temp
        reverse(temp.begin(), temp.end());

        // Insert the suffix into the hashet
        set.insert(temp);

        // Reverse the string temp again
        reverse(temp.begin(), temp.end());
    }

    // Initialize dp array to store the answer
    int dp[str1.length() + 1];

    memset(dp, -1, sizeof(dp));
    dp[0] = 0;

    // Check for all substrings starting
    // and ending at every indices
    for (int i = 0; i < l1; i++) {
        for (int j = 1; j <= l1 - i; j++) {

            // HashSet contains the substring
            if (set.count(str1.substr(i, j))) {

                if (dp[i] == -1) {
                    continue;
                }
                if (dp[i + j] == -1) {
                    dp[i + j] = dp[i] + 1;
                }
                else {

                    // Minimum of dp[i + j] and
                    // dp[i] + 1 will be stored
                    dp[i + j]
                        = min(dp[i + j], dp[i] + 1);
                }
            }
        }
    }

    // Return the answer
    return dp[str1.size()];
}

// Driver Code
int main()
{
    string str = "GEEKSFORGEEKS",
           wrd = "SFORGEEK";

    // Print the string
    cout << partCount(str, wrd);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.Arrays;
import java.util.HashSet;

class GFG {

    // Function to find minimum number of
    // concatenation of prefix and suffix
    // of str2 to make str1
    public static int partCount(String str1, String str2) {

        // Initialize a set
        HashSet<String> set = new HashSet<String>();

        // Initialize a temporary string
        String temp = "";

        int l1 = str1.length(), l2 = str2.length();

        // Iterate the string str2
        // from left to right
        for (int i = 0; i < l2; i++) {

            // Add current character
            // to string temp
            temp += str2.charAt(i);

            // Insert the prefix into hashset
            set.add(temp);
        }

        // Re-initialize temp string
        // to empty string
        temp = "";

        // Iterate the string in reverse direction
        for (int i = l2 - 1; i >= 0; i--) {

            // Add current character to temp
            temp += str2.charAt(i);

            // Reverse the string temp
            temp = new StringBuffer(temp).reverse().toString();

            // Insert the suffix into the hashet
            set.add(temp);

            // Reverse the string temp again
            temp = new StringBuffer(temp).reverse().toString();

        }

        // Initialize dp array to store the answer
        int[] dp = new int[str1.length() + 1];
        Arrays.fill(dp, -1);
        dp[0] = 0;

        // Check for all substrings starting
        // and ending at every indices
        for (int i = 0; i < l1; i++) {
            for (int j = 1; j <= l1 - i; j++) {

                // HashSet contains the substring
                if (set.contains(str1.substring(i, i + j))) {

                    if (dp[i] == -1) {
                        continue;
                    }
                    if (dp[i + j] == -1) {
                        dp[i + j] = dp[i] + 1;
                    } else {

                        // Minimum of dp[i + j] and
                        // dp[i] + 1 will be stored
                        dp[i + j] = Math.min(dp[i + j], dp[i] + 1);
                    }
                }
            }
        }

        // Return the answer
        return dp[str1.length()];
    }

    // Driver Code
    public static void main(String args[]) {
        String str = "GEEKSFORGEEKS", wrd = "SFORGEEK";

        // Print the string
        System.out.println(partCount(str, wrd));
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python3 implementation for the above approach

# Function to find minimum number of
# concatenation of prefix and suffix
# of str2 to make str1
def partCount(str1, str2):

    # Initialize a set
    se = set()

    # Initialize a temporary string
    temp = ""

    l1 = len(str1)
    l2 = len(str2)

    # Iterate the string str2
    # from left to right
    for i in range(0, l2):

                # Add current character
                # to string temp
        temp += str2[i]

        # Insert the prefix into hashset
        se.add(temp)

        # Re-initialize temp string
        # to empty string
    temp = []

    # Iterate the string in reverse direction
    for i in range(l2 - 1, -1, -1):

                # Add current character to temp
        temp.append(str2[i])

        # Reverse the string temp
        temp.reverse()

        # Insert the suffix into the hashet
        se.add(''.join(temp))

        # Reverse the string temp again
        temp.reverse()

        # Initialize dp array to store the answer
    dp = [-1 for _ in range(len(str1) + 1)]
    dp[0] = 0

    # Check for all substrings starting
    # and ending at every indices
    for i in range(0, l1, 1):
        for j in range(1, l1 - i + 1):

                        # HashSet contains the substring
            if (str1[i:i+j] in se):

                if (dp[i] == -1):
                    continue

                if (dp[i + j] == -1):
                    dp[i + j] = dp[i] + 1

                else:

                    # Minimum of dp[i + j] and
                    # dp[i] + 1 will be stored
                    dp[i + j] = min(dp[i + j], dp[i] + 1)

        # Return the answer
    return dp[len(str1)]

# Driver Code
if __name__ == "__main__":

    str = "GEEKSFORGEEKS"
    wrd = "SFORGEEK"

    # Print the string
    print(partCount(str, wrd))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

class GFG
{
    public static string Reverse(string Input)
    {

    // Converting string to character array
    char[] charArray = Input.ToCharArray();

    // Declaring an empty string
    string reversedString = String.Empty;

    // Iterating the each character from right to left
    for(int i = charArray.Length - 1; i > -1; i--)
    {

        // Append each character to the reversedstring.
        reversedString += charArray[i];
    }

    // Return the reversed string.
    return reversedString;
    }

    // Function to find minimum number of
    // concatenation of prefix and suffix
    // of str2 to make str1
    public static int partCount(string str1, string str2) {

        // Initialize a set
        HashSet<String> set = new HashSet<String>();

        // Initialize a temporary string
        string temp = "";

        int l1 = str1.Length, l2 = str2.Length;

        // Iterate the string str2
        // from left to right
        for (int i = 0; i < l2; i++) {

            // Add current character
            // to string temp
            temp += str2[i];

            // Insert the prefix into hashset
            set.Add(temp);
        }

        // Re-initialize temp string
        // to empty string
        temp = "";

        // Iterate the string in reverse direction
        for (int i = l2 - 1; i >= 0; i--) {

            // Add current character to temp
            temp += str2[i];

            // Reverse the string temp
            temp = Reverse(temp);

            // Insert the suffix into the hashet
            set.Add(temp);

            // Reverse the string temp again
            temp = Reverse(temp);

        }

        // Initialize dp array to store the answer
        int[] dp = new int[str1.Length + 1];
        for(int j=0; j<dp.Length;j++)
        {
            dp[j] = -1;
        }

        dp[0] = 0;

        // Check for all substrings starting
        // and ending at every indices
        for (int i = 0; i < l1; i++) {
            for (int j = 1; j <= l1 - i; j++) {

                // HashSet contains the substring
                if (set.Contains(str1.Substring(i, j))) {

                    if (dp[i] == -1) {
                        continue;
                    }
                    if (dp[i + j] == -1) {
                        dp[i + j] = dp[i] + 1;
                    } else {

                        // Minimum of dp[i + j] and
                        // dp[i] + 1 will be stored
                        dp[i + j] = Math.Min(dp[i + j], dp[i] + 1);
                    }
                }
            }
        }

        // Return the answer
        return dp[str1.Length];
    }

    // Driver code
    static public void Main(String[] args)
    {
        string str = "GEEKSFORGEEKS", wrd = "SFORGEEK";

        // Print the string
        Console.WriteLine(partCount(str, wrd));
    }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find minimum number of
       // concatenation of prefix and suffix
       // of str2 to make str1
       function partCount(str1, str2) {

           // Initialize a set
           let set = new Set();

           // Initialize a temporary string
           let temp = "";

           let l1 = str1.length, l2 = str2.length;

           // Iterate the string str2
           // from left to right
           for (let i = 0; i < l2; i++) {

               // Add current character
               // to string temp
               temp = temp + str2.charAt(i);

               // Insert the prefix into hashset
               set.add(temp);
           }

           // Re-initialize temp string
           // to empty string
           temp = "";

           // Iterate the string in reverse direction
           for (let i = l2 - 1; i >= 0; i--) {

               // Add current character to temp
               temp = temp + str2.charAt(i);

               // Reverse the string temp
               temp = temp.split('').reduce((r, c) => c + r, '');

               // Insert the suffix into the hashet
               set.add(temp);

               // Reverse the string temp again
               temp = temp.split('').reduce((r, c) => c + r, '');
           }

           // Initialize dp array to store the answer
           let dp = new Array(str1.length + 1).fill(-1);

           dp[0] = 0;

           // Check for all substrings starting
           // and ending at every indices
           for (let i = 0; i < l1; i++) {
               for (let j = 1; j <= l1 - i; j++) {

                   // HashSet contains the substring
                   if (set.has(str1.substring(i, j))) {

                       if (dp[i] == -1) {
                           continue;
                       }
                       if (dp[i + j] == -1) {
                           dp[i + j] = dp[i] + 1;
                       }
                       else {

                           // Minimum of dp[i + j] and
                           // dp[i] + 1 will be stored
                           dp[i + j]
                               = Math.min(dp[i + j], dp[i] + 1);
                       }
                   }
               }
           }

           // Return the answer
           return dp[str1.length] + 1;
       }

       // Driver Code
       let str = "GEEKSFORGEEKS"
       let wrd = "SFORGEEK";

       // Print the string
       document.write(partCount(str, wrd));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
3
```

**时间复杂度:** O(N^3)，其中 n 是 str 1
T3】辅助空间的长度: O(N^2)