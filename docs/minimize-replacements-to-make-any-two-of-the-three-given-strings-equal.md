# 尽量减少替换，使三个给定字符串中的任意两个相等

> 原文:[https://www . geeksforgeeks . org/最小化替换使三个给定字符串中的任意两个相等/](https://www.geeksforgeeks.org/minimize-replacements-to-make-any-two-of-the-three-given-strings-equal/)

给定三个长度相等的[字符串](https://www.geeksforgeeks.org/string-data-structure/)**A****B**和 **C** ，任务是找到可以执行的最小替换操作数，使得三个字符串中的任意两个变得相等。

**示例:**

> **输入:**A =“AAA”，B =“Bab”，C =“BBB”
> **输出:** 1
> **说明:**要使字符串 B 和 C 相等，B[1]=“A”可以替换为“B”。因此，替换后的字符串 B 变成了 B =“BBB”= C。因此，可以在 1 次操作中使 B 和 C 相等，这是最小的可能。
> 
> **输入:**A =“pqr”，B =“pqr”，C =“PPP”
> **输出:** 0
> **说明:**由于A 和 B 已经相等，不需要进行替换操作。

**逼近:**求所有三种可能情况的运算数，即 **A = B** 或 **B = C** 或 **A = C** ，取三者中的最小值，即可求解给定问题。使[串](https://www.geeksforgeeks.org/string-data-structure/) **X** 和 **Y** 相等所需的操作次数可以通过[遍历串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并跟踪索引以使 **X[i] ≠ Y[i]** 来计算。此类索引的计数是所需的操作数。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// replacement to make two strings equal
int minimumReplacement(string X, string Y)
{
    // Stores the operation count
    int cnt = 0;
    for (int i = 0; i < X.length(); i++)
        if (X[i] != Y[i])
            cnt++;

    // Return Answer
    return cnt;
}

// Function to find the minimum number of
// replacement to make any two strings
// out of the given three strings equal
int replacementOperations(
    string A, string B, string C)
{
    // Case where A and B will be equal
    int AB = minimumReplacement(A, B);

    // Case where A and C will be equal
    int AC = minimumReplacement(A, C);

    // Case where B and C will be equal
    int BC = minimumReplacement(B, C);

    // Return the minimum of the three
    // above calculated values
    return min(AB, min(AC, BC));
}

// Driver Code
int main()
{
    string A = "aaa";
    string B = "bab";
    string C = "bbb";

    cout << replacementOperations(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;
public class GFG
{

// Function to find the minimum number of
// replacement to make two strings equal
static int minimumReplacement(String X, String Y)
{

    // Stores the operation count
    int cnt = 0;
    for (int i = 0; i < X.length(); i++)
        if (X.charAt(i) != Y.charAt(i))
            cnt++;

    // Return Answer
    return cnt;
}

// Function to find the minimum number of
// replacement to make any two strings
// out of the given three strings equal
static int replacementOperations(
    String A, String B, String C)
{
    // Case where A and B will be equal
    int AB = minimumReplacement(A, B);

    // Case where A and C will be equal
    int AC = minimumReplacement(A, C);

    // Case where B and C will be equal
    int BC = minimumReplacement(B, C);

    // Return the minimum of the three
    // above calculated values
    return Math.min(AB, Math.min(AC, BC));
}

// Driver Code
public static void main(String args[])
{
    String A = "aaa";
    String B = "bab";
    String C = "bbb";

    System.out.println(replacementOperations(A, B, C));
}
}

// This code is contributed by Samim Hossain Mondal
```

## 蟒蛇 3

```
# Python program of the above approach

# Function to find the minimum number of
# replacement to make two strings equal
def minimumReplacement(X, Y):
    # Stores the operation count
    cnt = 0
    for i in range(len(X)):
        if (X[i] != Y[i]):
            cnt += 1

    # Return Answer
    return cnt

# Function to find the minimum number of
# replacement to make any two strings
# out of the given three strings equal
def replacementOperations(A, B, C):

    # Case where A and B will be equal
    AB = minimumReplacement(A, B)

    # Case where A and C will be equal
    AC = minimumReplacement(A, C)

    # Case where B and C will be equal
    BC = minimumReplacement(B, C)

    # Return the minimum of the three
    # above calculated values
    return min(AB, min(AC, BC))

# Driver Code
A = "aaa"
B = "bab"
C = "bbb"

print(replacementOperations(A, B, C))

# This code is contributed by saurabh_jaiswal.
```

## C#

```
// C# program of the above approach
using System;
using System.Collections;

class GFG
{

// Function to find the minimum number of
// replacement to make two strings equal
static int minimumReplacement(string X, string Y)
{

    // Stores the operation count
    int cnt = 0;
    for (int i = 0; i < X.Length; i++)
        if (X[i] != Y[i])
            cnt++;

    // Return Answer
    return cnt;
}

// Function to find the minimum number of
// replacement to make any two strings
// out of the given three strings equal
static int replacementOperations(
    string A, string B, string C)
{

    // Case where A and B will be equal
    int AB = minimumReplacement(A, B);

    // Case where A and C will be equal
    int AC = minimumReplacement(A, C);

    // Case where B and C will be equal
    int BC = minimumReplacement(B, C);

    // Return the minimum of the three
    // above calculated values
    return Math.Min(AB, Math.Min(AC, BC));
}

// Driver Code
public static void Main()
{
    string A = "aaa";
    string B = "bab";
    string C = "bbb";

    Console.Write(replacementOperations(A, B, C));
}
}

// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
// Javascript program of the above approach

// Function to find the minimum number of
// replacement to make two strings equal
function minimumReplacement(X, Y) {
  // Stores the operation count
  let cnt = 0;
  for (let i = 0; i < X.length; i++)
    if (X[i] != Y[i])
      cnt++;

  // Return Answer
  return cnt;
}

// Function to find the minimum number of
// replacement to make any two strings
// out of the given three strings equal
function replacementOperations(A, B, C) {
  // Case where A and B will be equal
  let AB = minimumReplacement(A, B);

  // Case where A and C will be equal
  let AC = minimumReplacement(A, C);

  // Case where B and C will be equal
  let BC = minimumReplacement(B, C);

  // Return the minimum of the three
  // above calculated values
  return Math.min(AB, Math.min(AC, BC));
}

// Driver Code

let A = "aaa";
let B = "bab";
let C = "bbb";

document.write(replacementOperations(A, B, C));
</script>
```

**Output**

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)