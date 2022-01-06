# 通过字符 ASCII 值的最小增量或减量数使字符串的所有字符相同

> 原文:[https://www . geeksforgeeks . org/将字符串中的所有字符按最小的 ascii 字符值增量或减量数进行相同操作/](https://www.geeksforgeeks.org/make-all-characters-of-a-string-same-by-minimum-number-of-increments-or-decrements-of-ascii-values-of-characters/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过将任意字符的 [ASCII 值增加/减少任意次数 **1** 来使该字符串的所有字符相同。
**注意:**所有字符必须改为原字符串的一个字符。](https://www.geeksforgeeks.org/program-print-ascii-value-character/)

**示例:**

> **输入:** S =【极客】
> **输出:** 20
> **说明:**
> 通过使字符串的所有字符等于‘g’可以获得最小的运算次数。
> 将 2 'e 的 ASCII 值增加 2。
> 将“k”的 ASCII 值减少 4，
> 将“s”的 ASCII 值减少 12。
> 因此，所需的操作数量= 2 + 2 + 4 + 12 = 20
> 
> **输入:** S =【蛋糕】
> **输出:** 12
> **说明:**
> 通过使字符串的所有字符都等于‘c’可以获得最小的运算次数。
> 将“a”的 ASCII 值增加 2。
> 将“e”的 ASCII 值减 2。
> 将“k”的 ASCII 值减少 8。
> 因此，所需操作数= 2 + 2 + 8 = 12

**天真方法:**解决问题最简单的方法是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，对于每个不同的字符，计算使字符串的所有字符与该字符相同所需的操作总数。最后，打印任何字符所需的最小操作数。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过观察到只有当字符等于排序字符串中的中间字符时才能达到**最小运算次数**来优化。
按照以下步骤解决问题:

*   [按非递减顺序对字符串的字符进行排序](https://www.geeksforgeeks.org/sort-string-characters/)。
*   现在，要用最少的操作次数使所有字符相等，请使字符等于排序字符串中间的字符。
*   找到排序字符串中间的字符为 **mid = S[N / 2]** 。
*   初始化一个变量，比如 **total_operations** ，以存储使字符串的所有字符相等所需的最小操作数。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，对于遇到的每个字符，通过添加当前字符和**中间的**的绝对差值来更新 **total_operations** 。
*   将 **total_operations** 打印为所需的最小操作数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if all characters
// of the string can be made the same
int sameChar(string S, int N)
{

    // Sort the string
    sort(S.begin(), S.end());

    // Calculate ASCII value
    // of the median character
    int mid = S[N / 2];

    // Stores the minimum number of
    // operations required to make
    // all characters equal
    int total_operations = 0;

    // Traverse the string
    for (int i = 0; i < N; i++) {

        // Calculate absolute value of
        // current character and median character
        total_operations
            += abs(int(S[i]) - mid);
    }

    // Print the minimum number of
    // operations required
    cout << total_operations;
}

// Driver Code
int main()
{
    string S = "geeks";
    int N = S.size();

    sameChar(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;
class GFG {

  // Function to check if all characters
  // of the string can be made the same
  static void sameChar(String S, int N)
  {

    char temp[] = S.toCharArray();

    // Sort the string
    Arrays.sort(temp);

    String s = new String(temp);

    // Calculate ASCII value
    // of the median character
    int mid = s.charAt(N / 2);

    // Stores the minimum number of
    // operations required to make
    // all characters equal
    int total_operations = 0;

    // Traverse the string
    for (int i = 0; i < N; i++) {

      // Calculate absolute value of
      // current character and median character
      total_operations
        += Math.abs(((s.charAt(i) - 0) - mid));
    }

    // Print the minimum number of
    // operations required
    System.out.print(total_operations);
  }

  // Driver Code
  public static void main(String[] args)
  {
    String S = "geeks";
    int N = S.length();

    sameChar(S, N);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if all characters
# of the string can be made the same
def sameChar(S, N):

    # Sort the string
    S = ''.join(sorted(S))

    # Calculate ASCII value
    # of the median character
    mid = ord(S[N // 2])

    # Stores the minimum number of
    # operations required to make
    # all characters equal
    total_operations = 0

    # Traverse the string
    for i in range(N):

        # Calculate absolute value of
        # current character and median character
        total_operations += abs(ord(S[i]) - mid)

    # Print the minimum number of
    # operations required
    print(total_operations)

# Driver Code
S = "geeks"
N = len(S)
sameChar(S, N)

# This code is contributed by subhammahato348.
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

  // Function to check if all characters
  // of the string can be made the same
  static void sameChar(String S, int N)
  {

    char[] temp = S.ToCharArray();

    // Sort the string
    Array.Sort(temp);

    String s = new String(temp);

    // Calculate ASCII value
    // of the median character
    int mid = s[N / 2];

    // Stores the minimum number of
    // operations required to make
    // all characters equal
    int total_operations = 0;

    // Traverse the string
    for (int i = 0; i < N; i++) {

      // Calculate absolute value of
      // current character and median character
      total_operations += Math.Abs((s[i] - 0) - mid);
    }

    // Print the minimum number of
    // operations required
    Console.Write(total_operations);
  }

  // Driver Code
  static public void Main()
  {

    String S = "geeks";
    int N = S.Length;

    sameChar(S, N);
  }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to check if all characters
      // of the string can be made the same
      function sameChar(S, N) {
        // Sort the string
        var arr = S.split("");
        var sorted = arr.sort();
        S = sorted.join("");

        // Calculate ASCII value
        // of the median character
        var mid = S[parseInt(N / 2)].charCodeAt(0);

        // Stores the minimum number of
        // operations required to make
        // all characters equal
        var total_operations = 0;

        // Traverse the string
        for (var i = 0; i < N; i++) {
          // Calculate absolute value of
          // current character and median character
          total_operations += Math.abs(S[i].charCodeAt(0) - mid);
        }

        // Print the minimum number of
        // operations required
        document.write(total_operations);
      }

      // Driver Code
      var S = "geeks";
      var N = S.length;
      sameChar(S, N);
    </script>
```

**Output:** 

```
20
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*