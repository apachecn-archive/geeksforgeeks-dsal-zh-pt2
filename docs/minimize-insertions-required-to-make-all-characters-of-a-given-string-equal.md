# 最小化使给定字符串的所有字符相等所需的插入次数

> 原文:[https://www . geesforgeks . org/minimum-insertions-required-to-make-all-characters-of-给定字符串-equal/](https://www.geeksforgeeks.org/minimize-insertions-required-to-make-all-characters-of-a-given-string-equal/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到需要插入的最小字符数，使得字符串中的所有字符都相同，条件是:

> 如果将**“1”**插入到弦中，则最靠近插入的**“1”**的所有**“0”**被翻转，反之亦然。

**示例:**

> **输入:** S = "11100"
> **输出:** 1
> **解释:**
> **操作 1:** 在给定字符串的最后插入**‘1’**将 **S** 修改为**“111001”**。将**“1”**加到最后会将最近的**“0”**翻转到插入的**“1”**。因此，得到的字符串是**“111111”**。
> 完成上述操作后，字符串的所有字符都是相同的。因此，操作计数为 1。
> 
> **输入:**S = " 0101010101 "
> T3】输出: 9

**进场:**思路是基于以下观察通过[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决这个问题:

*   可以看出，将**‘1’**s 或**‘0’**s 的一个连续段反转，在此操作中会减少一个段的数量。因此，只要重复这个操作，就可以将所有内容整合到一个部分中。所需操作的数量等于**部分–1**。
*   更简单地说，计算不相等的相邻字符对的总数，这样反转其中一个字符就可以将整个子字符串转换为相似的子字符串。

按照以下步骤解决问题:

*   初始化一个变量，比如**计数**，存储不同相邻字符的计数。
*   [遍历字符串](https://www.geeksforgeeks.org/c-string-class-and-its-applications/)并检查当前字符和下一个字符是否不同，然后增加**计数**的值。
*   完成上述步骤后，打印**计数**的值，作为最小所需操作。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of operations required to make
// all characters of the string same
int minOperations(string& S)
{
    // Stores count of operations
    int count = 0;

    // Traverse the string
    for (int i = 1; i < S.length(); i++) {

        // Check if adjacent
        // characters are same or not
        if (S[i] != S[i - 1]) {

            // Increment count
            count += 1;
        }
    }

    // Print the count obtained
    cout << count;
}

// Driver Code
int main()
{
    string S = "0101010101";
    minOperations(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to calculate the minimum
  // number of operations required to make
  // all characters of the string same
  static void minOperations(String S)
  {

    // Stores count of operations
    int count = 0;

    // Traverse the string
    for (int i = 1; i < S.length(); i++)
    {

      // Check if adjacent
      // characters are same or not
      if (S.charAt(i) != S.charAt(i - 1))
      {

        // Increment count
        count += 1;
      }
    }

    // Print the count obtained
     System.out.print(count);
  }

  // Driver Code
  public static void main(String[] args)
  {
    String S = "0101010101";
    minOperations(S);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to calculate the minimum
# number of operations required to make
# all characters of the string same
def minOperations(S):

  # Stores count of operations
    count = 0;

    # Traverse the string
    for i in range(1, len(S)):

        # Check if adjacent
        # characters are same or not
        if (S[i] != S[i - 1]):

            # Increment count
            count += 1;

    # Prthe count obtained
    print(count);

# Driver Code
if __name__ == '__main__':
    S = "0101010101";
    minOperations(S);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to calculate the minimum
  // number of operations required to make
  // all characters of the string same
  static void minOperations(string S)
  {

    // Stores count of operations
    int count = 0;

    // Traverse the string
    for (int i = 1; i < S.Length; i++)
    {

      // Check if adjacent
      // characters are same or not
      if (S[i] != S[i - 1])
      {

        // Increment count
        count += 1;
      }
    }

    // Print the count obtained
    Console.Write(count);
  }

  // Driver Code
  public static void Main()
  {
    string S = "0101010101";
    minOperations(S);
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to calculate the minimum
      // number of operations required to make
      // all characters of the string same
      function minOperations(S) {
        // Stores count of operations
        var count = 0;

        // Traverse the string
        for (var i = 1; i < S.length; i++) {
          // Check if adjacent
          // characters are same or not
          if (S[i] !== S[i - 1]) {
            // Increment count
            count += 1;
          }
        }

        // Print the count obtained
        document.write(count);
      }

      // Driver Code
      var S = "0101010101";
      minOperations(S);
    </script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)