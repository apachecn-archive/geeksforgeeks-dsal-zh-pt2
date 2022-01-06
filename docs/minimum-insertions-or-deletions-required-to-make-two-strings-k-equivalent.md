# 使两个字符串 K 等价所需的最少插入或删除次数

> 原文:[https://www . geesforgeks . org/minimum-insertions-or-deletes-required-make-two-string-k-equivalent/](https://www.geeksforgeeks.org/minimum-insertions-or-deletions-required-to-make-two-strings-k-equivalent/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **str1** 和 **str2** ，任务是通过在 **str2** 中插入一个字符或从 **str2** 中移除一个字符，找到将字符串 **str1** 的每个字符映射到字符串 **K ( < 1000)** 相似字符所需的最小操作数。

**示例:**

> **输入:**str 1 =“aab”，str 2 =“aaabb”
> T3】输出: 0
> **解释:**
> 将{str2[0]，str2[1]}映射到 str1[0]
> 将{str2[2]，str2[3]}映射到 str1[1]。
> 将{str2[4]、str2[5]}映射到 str1[2]
> 因为不需要操作来将 **str1** 的每个字符映射到 str2 的 K(= 2)个相似字符。
> 因此，要求输出为 0。
> 
> **输入:**str 1 =“aaa”，str2 =“BBB”
> **输出:** 6
> **解释:**
> 删除 str2[0]，str2[1]，str2[2]，插入“aaa”将 str 2 修改为“AAA”。
> 将{ str2[0] }映射到 str1[0]，将 str2[1]映射到 str1[1]，将{str2[2]}映射到 str1[2]。
> 因此，要求输出为 6。

**方法:**要解决这个问题，选择 **K** 的最佳值，使得所需的操作次数最少。要选择 **K** 的最佳值，迭代 **K** 的所有可能值，并记录每个值所需的操作次数。最后，打印获得的最小计数。按照以下步骤解决问题:

1.  初始化两个数组，比如 **a1[]** 和 **a2[]** ，分别存储 **str1** 和 **str2** 的每个不同字符的[频率。](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)
2.  迭代所有可能的 **K** 值，并在**和**中记录到目前为止的最小值:
    *   迭代范围**【0，25】**，检查以下条件:
        *   如果某个字符不在 **str1** 中，而在 **str2** 中，则所有这些字符都应从 **str2** 中删除。因此，**计数**应相应更新。
        *   如果某个字符出现在 **str1** 中，则通过该字符在 **str2** 中的频率与当前值 **K** 的绝对差值乘以该字符在 **str1** 中的频率来更新**计数**。
    *   用**计数**更新**和**。
3.  最后打印得到的计数，即 **ans**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of operations
// required to map each character of str1 to K
// same characters of str2
int minOperations(string str1, string str2)
{

    // Store frequency of each
    // distinct character of str1
    int a1[26] = { 0 };

    // Store frequency of each
    // distinct character of str2
    int a2[26] = { 0 };

    // Iterate over each character
    // of the string, str1
    for (auto x : str1) {

        // Update frequency of
        // current character
        a1[x - 'a']++;
    }

    // Iterate over each character
    // of the string, str2
    for (auto x : str2) {

        // Update frequency of
        // current character
        a2[x - 'a']++;
    }

    // Stores minimum count of operations
    // required to map each character of
    // str1 to K same characters of str2
    int ans = INT_MAX;

    // Iterate over all
    // possible values of K
    for (int k = 1; k < 1001; k++) {

        // Stores count of operations required
        // to map each character of str1 to k
        // same characters of str2
        int count = 0;

        // Iterate over possible characters
        for (int i = 0; i < 26; i++) {

            // If (i + 'a') is not
            // present in str1
            if (a1[i] == 0) {

                // Update count by removing
                // character from str2
                count += a2[i];
            }

            // If a character is
            // present in str1
            else {

                // Update count by inserting
                // character into str2
                count += abs(a1[i] * k - a2[i]);
            }
        }

        // Update the answer
        ans = min(ans, count);
    }
    return ans;
}

// Driver Code
int main()
{
    string str1 = "aaa";
    string str2 = "bbb";

    // Function Call
    cout << minOperations(str1, str2) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{
  // Function to find minimum count of operations
  // required to map each character of str1 to K
  // same characters of str2
  static int minOperations(String str1, String str2)
  {

    // Store frequency of each
    // distinct character of str1
    int[] a1 = new int[26];

    // Store frequency of each
    // distinct character of str2
    int[] a2 = new int[26];

    // Iterate over each character
    // of the string, str1
    for (int x = 0; x < str1.length(); x++)
    {

      // Update frequency of
      // current character
      a1[str1.charAt(x) - 'a']++;
    }

    // Iterate over each character
    // of the string, str2
    for (int x = 0; x < str2.length(); x++)
    {

      // Update frequency of
      // current character
      a2[str2.charAt(x) - 'a']++;
    }

    // Stores minimum count of operations
    // required to map each character of
    // str1 to K same characters of str2
    int ans = Integer.MAX_VALUE;

    // Iterate over all
    // possible values of K
    for (int k = 1; k < 1001; k++)
    {

      // Stores count of operations required
      // to map each character of str1 to k
      // same characters of str2
      int count = 0;

      // Iterate over possible characters
      for (int i = 0; i < 26; i++)
      {

        // If (i + 'a') is not
        // present in str1
        if (a1[i] == 0)
        {

          // Update count by removing
          // character from str2
          count += a2[i];
        }

        // If a character is
        // present in str1
        else
        {

          // Update count by inserting
          // character into str2
          count += Math.abs(a1[i] * k - a2[i]);
        }
      }

      // Update the answer
      ans = Math.min(ans, count);
    }
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    String str1 = "aaa";
    String str2 = "bbb";

    // Function Call
    System.out.println(minOperations(str1, str2));
  }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find minimum count of operations
# required to map each character of str1 to K
# same characters of str2
import sys
def minOperations(str1, str2):

  # Store frequency of each
    # distinct character of str1
    a1 = [0] * 26;

    # Store frequency of each
    # distinct character of str2
    a2 = [0] * 26;

    # Iterate over each character
    # of the string, str1
    for x in range(len(str1)):

        # Update frequency of
        # current character
        a1[ord(str1[x]) - ord('a')] += 1;

    # Iterate over each character
    # of the string, str2
    for x in range(len(str2)):

        # Update frequency of
        # current character
        a2[ord(str2[x]) - ord('a')] += 1;

    # Stores minimum count of operations
    # required to map each character of
    # str1 to K same characters of str2
    ans = sys.maxsize;

    # Iterate over all
    # possible values of K
    for k in range(1, 1001):

        # Stores count of operations required
        # to map each character of str1 to k
        # same characters of str2
        count = 0;

        # Iterate over possible characters
        for i in range(26):

            # If (i + 'a') is not
            # present in str1
            if (a1[i] == 0):

                # Update count by removing
                # character from str2
                count += a2[i];

            # If a character is
            # present in str1
            else:

                # Update count by inserting
                # character into str2
                count += abs(a1[i] * k - a2[i]);

        # Update the answer
        ans = min(ans, count);
    return ans;

# Driver code
if __name__ == '__main__':
    str1 = "aaa";
    str2 = "bbb";

    # Function Call
    print(minOperations(str1, str2));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find minimum count of operations
// required to map each character of str1 to K
// same characters of str2
static int minOperations(string str1, string str2)
{

    // Store frequency of each
    // distinct character of str1
    int[] a1 = new int[26];

    // Store frequency of each
    // distinct character of str2
    int[] a2 = new int[26];

    // Iterate over each character
    // of the string, str1
    foreach(char x in str1)
    {

        // Update frequency of
        // current character
        a1[x - 'a']++;
    }

    // Iterate over each character
    // of the string, str2
    foreach(char x in str2)
    {

        // Update frequency of
        // current character
        a2[x - 'a']++;
    }

    // Stores minimum count of operations
    // required to map each character of
    // str1 to K same characters of str2
    int ans = Int32.MaxValue;

    // Iterate over all
    // possible values of K
    for(int k = 1; k < 1001; k++)
    {

        // Stores count of operations required
        // to map each character of str1 to k
        // same characters of str2
        int count = 0;

        // Iterate over possible characters
        for(int i = 0; i < 26; i++)
        {

            // If (i + 'a') is not
            // present in str1
            if (a1[i] == 0)
            {

                // Update count by removing
                // character from str2
                count += a2[i];
            }

            // If a character is
            // present in str1
            else
            {

                // Update count by inserting
                // character into str2
                count += Math.Abs(a1[i] * k - a2[i]);
            }
        }

        // Update the answer
        ans = Math.Min(ans, count);
    }
    return ans;
}

// Driver code
static void Main()
{
    string str1 = "aaa";
    string str2 = "bbb";

    // Function Call
    Console.WriteLine(minOperations(str1, str2));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to find minimum count of operations
    // required to map each character of str1 to K
    // same characters of str2
    function minOperations(str1, str2)
    {

      // Store frequency of each
      // distinct character of str1
      let a1 = new Array(26);
      a1.fill(0);

      // Store frequency of each
      // distinct character of str2
      let a2 = new Array(26);
      a2.fill(0);

      // Iterate over each character
      // of the string, str1
      for(let x = 0; x < str1.length; x++)
      {

        // Update frequency of
        // current character
        a1[str1[x].charCodeAt() - 'a'.charCodeAt()]++;
      }

      // Iterate over each character
      // of the string, str2
      for(let x = 0; x < str2.length; x++)
      {

        // Update frequency of
        // current character
        a2[str2[x].charCodeAt() - 'a'.charCodeAt()]++;
      }

      // Stores minimum count of operations
      // required to map each character of
      // str1 to K same characters of str2
      let ans = Number.MAX_VALUE;

      // Iterate over all
      // possible values of K
      for(let k = 1; k < 1001; k++)
      {

        // Stores count of operations required
        // to map each character of str1 to k
        // same characters of str2
        let count = 0;

        // Iterate over possible characters
        for(let i = 0; i < 26; i++)
        {

          // If (i + 'a') is not
          // present in str1
          if (a1[i] == 0)
          {

            // Update count by removing
            // character from str2
            count += a2[i];
          }

          // If a character is
          // present in str1
          else
          {

            // Update count by inserting
            // character into str2
            count += Math.abs(a1[i] * k - a2[i]);
          }
        }

        // Update the answer
        ans = Math.min(ans, count);
      }
      return ans;
    }

    let str1 = "aaa";
    let str2 = "bbb";

    // Function Call
    document.write(minOperations(str1, str2));

</script>
```

**Output:** 

```
6
```

***时间复杂度:**T3】O(N+26 * K)
T5】T6】辅助空间:T8】O(N)*