# 尽量减少相同索引字符的互换，使两个字符串的 ASCII 值之和为奇数

> 原文:[https://www . geeksforgeeks . org/minimum-互换相同索引字符-使两个字符串的 ascii 字符值之和为奇数/](https://www.geeksforgeeks.org/minimize-swaps-of-same-indexed-characters-to-make-sum-of-ascii-value-of-characters-of-both-the-strings-odd/)

给定两个由小写字母组成的 **N** -length [字符串](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) **S** 和 **T** ，任务是最小化使两个字符串的字符的 ASCII 值之和为奇数所需的相同索引元素的交换次数。如果不能使 ASCII 值之和为奇数，则打印 **"-1"** 。

**示例:**

> ***输入:**S =“ACD”，T =“DBF”*
> T5】**输出:** 1
> ***解释:***
> *交换 S[1]和 T[1]将 S 修改为“abd”，将 T 修改为“dcf”。*
> *字符串 S 的字符 ASCII 值之和= 97 + 98 + 100 = 297 ( **奇数**)。*
> *字符串的字符 ASCII 值之和 T = 100 + 99 + 102 = 301 ( **奇数**)。*
> 
> ***输入:** S = "aey "，T = " cgj "*
> T5**输出:** -1

**方法:**按照以下步骤解决问题:

*   计算字符串 **S** 和 **T** 字符的 ASCII 值之和，并分别存储在变量 **sum1** 和 **sum2** 中。
*   如果 **sum1** 和 **sum2** 已经是奇数，那么打印 **0** ，因为不需要互换。
*   如果 **sum1** 和 **sum2** 的奇偶校验不同，打印 **-1** ，因为两个字符串的奇偶校验总和不能相同。
*   如果 **sum1** 和 **sum2** 都是**偶数**，那么[遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 和 **T** 。如果存在任何具有奇数 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)的字符，则仅通过 **1** 交换就可以使两个字符串的字符的 ASCII 值之和为奇数。否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of swaps
// required to make the sum of ASCII values
// of the characters of both strings odd
void countSwaps(string S, string T)
{
    // Initialize alphabets with value
    int value[26];

    // Initialize values for each
    // alphabet
    for (int i = 0; i < 26; i++)
        value[i] = i + 1;

    // Size of the string
    int N = S.size();

    // Sum of string S
    int sum1 = 0;

    // Sum of string T
    int sum2 = 0;

    // Stores whether there is any
    // index i such that S[i] and
    // T[i] have different parities
    bool flag = false;

    // Traverse the strings
    for (int i = 0; i < N; i++) {

        // Update sum1 and sum2
        sum1 += value[S[i] - 'a'];
        sum2 += value[T[i] - 'a'];

        // If S[i] and T[i] have
        // different parities
        if ((value[S[i] - 'a'] % 2 == 0
             && value[T[i] - 'a'] % 2 == 1)

            || (value[S[i] - 'a'] % 2 == 1
                && value[T[i] - 'a'] % 2 == 0))

            flag = false;
    }

    // If sum1 and sum2 are both odd
    if (sum1 % 2 == 1
        && sum2 % 2 == 1)
        cout << "0\n";

    // If sum1 and sum2 are both even
    else if (sum1 % 2 == 0
             && sum2 % 2 == 0) {

        // If exists print 1
        if (flag)
            cout << "1";

        // Otherwise
        else
            cout << "-1";
    }

    // If sum1 and sum2 are
    // of different parities
    else {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    string S = "acd";
    string T = "dbf";

    // Function Call
    countSwaps(S, T);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to count the number of swaps
  // required to make the sum of ASCII values
  // of the characters of both strings odd
  static void countSwaps(String S, String T)
  {

    // Initialize alphabets with value
    int[] value = new int[26];

    // Initialize values for each
    // alphabet
    for (int i = 0; i < 26; i++)
      value[i] = i + 1;

    // Size of the string
    int N = S.length();

    // Sum of string S
    int sum1 = 0;

    // Sum of string T
    int sum2 = 0;

    // Stores whether there is any
    // index i such that S[i] and
    // T[i] have different parities
    boolean flag = false;

    // Traverse the strings
    for (int i = 0; i < N; i++) {

      // Update sum1 and sum2
      sum1 += value[S.charAt(i) - 'a'];
      sum2 += value[T.charAt(i) - 'a'];

      // If S[i] and T[i] have
      // different parities
      if ((value[S.charAt(i) - 'a'] % 2 == 0
           && value[T.charAt(i) - 'a'] % 2 == 1)

          || (value[S.charAt(i) - 'a'] % 2 == 1
              && value[T.charAt(i) - 'a'] % 2 == 0))

        flag = false;
    }

    // If sum1 and sum2 are both odd
    if (sum1 % 2 == 1
        && sum2 % 2 == 1)
      System.out.println("0\n");

    // If sum1 and sum2 are both even
    else if (sum1 % 2 == 0
             && sum2 % 2 == 0) {

      // If exists print 1
      if (flag)
        System.out.println("1");

      // Otherwise
      else
        System.out.println("-1");
    }

    // If sum1 and sum2 are
    // of different parities
    else {
      System.out.println("-1");
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    String S = "acd";
    String T = "dbf";

    // Function Call
    countSwaps(S, T);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of swaps
# required to make the sum of ASCII values
# of the characters of both strings odd
def countSwaps(S, T):

    # Initialize alphabets with value
    value = [0]*26

    # Initialize values for each
    # alphabet
    for i in range(26):
        value[i] = i + 1

    # Size of the string
    N = len(S)

    # Sum of S
    sum1 = 0

    # Sum of T
    sum2 = 0

    # Stores whether there is any
    # index i such that S[i] and
    # T[i] have different parities
    flag = False

    # Traverse the strings
    for i in range(N):

        # Update sum1 and sum2
        sum1 += value[ord(S[i]) - ord('a')]
        sum2 += value[ord(T[i]) - ord('a')]

        # If ord(S[i]) anord('a)rd(T[i]) haord('a)
        # different parities
        if (value[ord(S[i]) - ord('a')] % 2 == 0
            and value[ord(T[i]) - ord('a')] % 2 == 1
            or value[ord(S[i]) - ord('a')] % 2 == 1
            and value[ord(T[i]) - ord('a')] % 2 == 0):

            flag = False

    # If sum1 and sum2 are both odd
    if (sum1 % 2 == 1 and sum2 % 2 == 1):
        print("0")

    # If sum1 and sum2 are both even
    elif (sum1 % 2 == 0 and sum2 % 2 == 0):

        # If exists pr1
        if (flag):
            print("1")

        # Otherwise
        else:
            print("-1")

    # If sum1 and sum2 are
    # of different parities
    else:
        print("-1")

# Driver Code
if __name__ == '__main__':
    S = "acd"
    T = "dbf"

    # Function Call
    countSwaps(S, T)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to count the number of swaps
// required to make the sum of ASCII values
// of the characters of both strings odd
static void countSwaps(string S, string T)
{

    // Initialize alphabets with value
    int[] value = new int[26];

    // Initialize values for each
    // alphabet
    for (int i = 0; i < 26; i++)
        value[i] = i + 1;

    // Size of the string
    int N = S.Length;

    // Sum of string S
    int sum1 = 0;

    // Sum of string T
    int sum2 = 0;

    // Stores whether there is any
    // index i such that S[i] and
    // T[i] have different parities
    bool flag = false;

    // Traverse the strings
    for (int i = 0; i < N; i++) {

        // Update sum1 and sum2
        sum1 += value[S[i] - 'a'];
        sum2 += value[T[i] - 'a'];

        // If S[i] and T[i] have
        // different parities
        if ((value[S[i] - 'a'] % 2 == 0
             && value[T[i] - 'a'] % 2 == 1)

            || (value[S[i] - 'a'] % 2 == 1
                && value[T[i] - 'a'] % 2 == 0))

            flag = false;
    }

    // If sum1 and sum2 are both odd
    if (sum1 % 2 == 1
        && sum2 % 2 == 1)
        Console.Write("0\n");

    // If sum1 and sum2 are both even
    else if (sum1 % 2 == 0
             && sum2 % 2 == 0) {

        // If exists print 1
        if (flag)
            Console.Write("1");

        // Otherwise
        else
            Console.Write("-1");
    }

    // If sum1 and sum2 are
    // of different parities
    else {
        Console.Write("-1");
    }
}

// Driver Code
public static void Main(String[] args)
{
    string S = "acd";
    string T = "dbf";

    // Function Call
    countSwaps(S, T);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to count the number of swaps
      // required to make the sum of ASCII values
      // of the characters of both strings odd
      function countSwaps(S, T)
      {

        // Initialize alphabets with value
        var value = [...Array(26)];

        // Initialize values for each
        // alphabet
        for (var i = 0; i < 26; i++) value[i] = i + 1;

        // Size of the string
        var N = S.length;

        // Sum of string S
        var sum1 = 0;

        // Sum of string T
        var sum2 = 0;

        // Stores whether there is any
        // index i such that S[i] and
        // T[i] have different parities
        var flag = false;

        // Traverse the strings
        for (var i = 0; i < N; i++) {
          // Update sum1 and sum2
          sum1 += value[S[i] - "a"];
          sum2 += value[T[i] - "a"];

          // If S[i] and T[i] have
          // different parities
          if (
            (value[S[i] - "a"] % 2 === 0 && value[T[i] - "a"] % 2 === 1) ||
            (value[S[i] - "a"] % 2 === 1 && value[T[i] - "a"] % 2 === 0)
          )
            flag = false;
        }

        // If sum1 and sum2 are both odd
        if (sum1 % 2 === 1 && sum2 % 2 === 1) document.write("0 <br>");
        // If sum1 and sum2 are both even
        else if (sum1 % 2 === 0 && sum2 % 2 === 0) {
          // If exists print 1
          if (flag) document.write("1");
          // Otherwise
          else document.write("-1");
        }

        // If sum1 and sum2 are
        // of different parities
        else {
          document.write("-1");
        }
      }

      // Driver Code
      var S = "aey";
      var T = "cgj";

      // Function Call
      countSwaps(S, T);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
-1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(26)