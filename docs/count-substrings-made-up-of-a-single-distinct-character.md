# 统计由单个不同字符组成的子字符串

> 原文:[https://www . geesforgeks . org/count-substrings-由单个不同字符组成/](https://www.geeksforgeeks.org/count-substrings-made-up-of-a-single-distinct-character/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是计算由单个不同字符组成的[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的数量。
***注意:**对于相同子串的重复出现，统计所有重复。*

**示例:**

> **输入:**str =**“**geeksforgeeks”
> **输出:** 15
> **解释:**由单个不同字符组成的所有子字符串为{“g”“e”“ee”“e”“k”“s”“f”“o”“r”“g”“e”“ee”“e”“k”“s”}。
> 
> **输入:**输出: 12

**天真方法:**解决这个问题最简单的方法是[从给定的字符串中生成所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)计算仅由单个不同字符组成的[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的数量。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**按照以下步骤优化上述方法:

*   初始化一个变量，比如**和**，来存储这些子串的计数。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，检查前一个字符，比如 **pre** ，是否与当前字符相同。
*   当发现前一个字符和当前字符相同时，增加**子字符**并添加到答案中。
*   如果发现前一个字符和当前字符不同，则重新初始化**子节点**到 **1** 。

下面是上述方法的实现:

## C++

```
#include <iostream>
using namespace std;

  // Function to count the number
  // of substrings made up of a
  // single distinct character
  void countSubstrings(string s)
  {

    // Stores the required count
    int ans = 0;

    // Stores the count of substrings
    // possible by using current character
    int subs = 1;

    // Stores the previous character
    char pre = '0';

    // Traverse the string
    for (auto& i : s)
    {

      // If current character is same
      // as the previous character
      if(pre == i)
      {

        // Increase count of substrings
        // possible with current character
        subs += 1;
      }
      else
      {

        // Reset count  of substrings
        // possible with current character
        subs = 1;
      }

      // Update count of substrings
      ans += subs;

      // Update previous character
      pre = i;
    }
    cout << ans <<endl;
  }

// Driver code
int main()
{

    string s = "geeksforgeeks";
    countSubstrings(s);

    return 0;
}

// This code is contributed by splevel62.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to count the number
  // of substrings made up of a
  // single distinct character
  static void countSubstrings(String s)
  {

    // Stores the required count
    int ans = 0;

    // Stores the count of substrings
    // possible by using current character
    int subs = 1;

    // Stores the previous character
    char pre = '0';

    // Traverse the string
    for(char i : s.toCharArray())
    {

      // If current character is same
      // as the previous character
      if(pre == i)
      {

        // Increase count of substrings
        // possible with current character
        subs += 1;
      }
      else
      {

        // Reset count  of substrings
        // possible with current character
        subs = 1;
      }

      // Update count of substrings
      ans += subs;

      // Update previous character
      pre = i;
    }
    System.out.println(ans);
  }

// Driver Code
public static void main(String[] args)
{
    String s = "geeksforgeeks";
    countSubstrings(s);
}
}

// This code is contributed by souravghosh0416.
```

## 蟒蛇 3

```
# Python3 Program to
# implement the above approach

# Function to count the number
# of substrings made up of a
# single distinct character

def countSubstrings(s):

    # Stores the required count
    ans = 0

    # Stores the count of substrings
    # possible by using current character
    subs = 1

    # Stores the previous character
    pre = ''

    # Traverse the string
    for i in s:

        # If current character is same
        # as the previous character
        if pre == i:

            # Increase count of substrings
            # possible with current character
            subs += 1
        else:

            # Reset count  of substrings
            # possible with current character
            subs = 1

        # Update count of substrings
        ans += subs

        # Update previous character
        pre = i

    print(ans)

# Driver Code
s = 'geeksforgeeks'
countSubstrings(s)
```

## C#

```
// C# Program to
// implement the above approach
using System;
class GFG {

  // Function to count the number
  // of substrings made up of a
  // single distinct character
  static void countSubstrings(string s)
  {

    // Stores the required count
    int ans = 0;

    // Stores the count of substrings
    // possible by using current character
    int subs = 1;

    // Stores the previous character
    char pre = '0';

    // Traverse the string
    foreach(char i in s)
    {

      // If current character is same
      // as the previous character
      if(pre == i)
      {

        // Increase count of substrings
        // possible with current character
        subs += 1;
      }
      else
      {

        // Reset count  of substrings
        // possible with current character
        subs = 1;
      }

      // Update count of substrings
      ans += subs;

      // Update previous character
      pre = i;
    }
    Console.WriteLine(ans);
  }

  // Driver code
  static void Main() {
    string s = "geeksforgeeks";
    countSubstrings(s);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript Program to implement
    // the above approach

    // Function to count the number
    // of substrings made up of a
    // single distinct character
    function countSubstrings(s)
    {

      // Stores the required count
      let ans = 0;

      // Stores the count of substrings
      // possible by using current character
      let subs = 1;

      // Stores the previous character
      let pre = '0';

      // Traverse the string
      for(let i = 0; i < s.length; i++)
      {

        // If current character is same
        // as the previous character
        if(pre == s[i])
        {

          // Increase count of substrings
          // possible with current character
          subs += 1;
        }
        else
        {

          // Reset count  of substrings
          // possible with current character
          subs = 1;
        }

        // Update count of substrings
        ans += subs;

        // Update previous character
        pre = s[i];
      }
      document.write(ans);
    }

    let s = "geeksforgeeks";
    countSubstrings(s);

</script>
```

**Output:** 

```
15
```

***时间复杂度** : O(N)*
***辅助空间** : O(1)*