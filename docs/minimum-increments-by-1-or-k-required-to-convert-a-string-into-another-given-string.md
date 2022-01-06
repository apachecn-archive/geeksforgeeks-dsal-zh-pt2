# 将一个字符串转换为另一个给定字符串所需的 1 或 K 的最小增量

> 原文:[https://www . geeksforgeeks . org/将字符串转换为另一个给定字符串所需的最小增量 1 或 k/](https://www.geeksforgeeks.org/minimum-increments-by-1-or-k-required-to-convert-a-string-into-another-given-string/)

给定两个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **X** 和 **Y** ，这两个字符串都由 **N** 大写字母和一个整数 **K** 组成，任务是通过将字符串 **X** 转换为字符串 **Y** 所需的 **1** 或 **K** 找到字符串 **X** 中任意字符循环增量的最小计数。

> **循环递增:**将字符**‘Z’**递增 **1** 或 **K** 从字符**‘A’**开始。

**示例:**

> **输入:**X =“ABCT”，Y =“PBDI”，K = 13
> **输出:** 7
> **说明:**
> 将字符 A 转换为 P，需要的增量为 13 (A 到 N)、1 (N 到 O)、1 (O 到 P)。因此，总数为 3。
> B 字不变。因此，总计数仍为 3。
> 将字符 C 转换为 D。所需增量为 1 (C 到 D)。因此，总数为 4。
> 将字符 T 转换为 I。所需的增量为 13 (T 到 G)、1 (G 到 H)、1 (H 到 I)。因此，总数是 7。
> 
> **输入:**X =“ABCD”，Y =“ABCD”，K = 6
> T3】输出: 0

**方法:**按照以下步骤解决这个问题:

*   初始化一个变量，比如**计数**，存储将字符串 **X** 转换为字符串 **Y** 所需的最小增量。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **X** ，对于字符串 **X** 中的每个字符，有以下三种情况:
    *   当两个字符串 **X** 和 **Y** 中的字符相同时，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   当字符串 **Y** 中的字符大于 **X** 字符串时，将值**(Y[I]–X[I])/K**和**(Y[I]–X[I])**模 **K** 加到**计数**中。
    *   当字符串**中的字符 X** 大于字符串 **Y** 时，则从 **90** 中减去字符**X【I】**，从**Y【I】**中减去 **64** ，计算循环差，然后将**差**模 **K** 和**差/K** 加到**计数**中。
*   完成上述步骤后，打印**计数**作为所需的最小增量数。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count minimum increments
// by 1 or K required to convert X to Y
void countOperations(
  string X, string Y, int K)
{

  int count = 0;

  // Traverse the string X
  for (int i = 0; i < X.length(); i++)
  {

    int c = 0;

    // Case 1
    if (X[i] == Y[i])
      continue;

    // Case 2
    else if (X[i] < Y[i])
    {

      // Add the difference/K to
      // the count
      if ((Y[i] - X[i]) >= K) {
        c = (Y[i] - X[i]) / K;
      }

      // Add the difference%K to
      // the count
      c += (Y[i] - X[i]) % K;
    }

    // Case 3
    else {
      int t = 90 - X[i];
      t += Y[i] - 65 + 1;

      // Add the difference/K to
      // the count
      if (t >= K)
        c = t / K;

      // Add the difference%K to
      // the count
      c += (t % K);
    }
    count += c;
  }

  // Print the answer
  cout << count << endl;
}

// Driver Code
int main()
{
  string X = "ABCT", Y = "PBDI";
  int K = 6;
  countOperations(X, Y, K);
}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to count minimum increments
    // by 1 or K required to convert X to Y
    public static void countOperations(
        String X, String Y, int K)
    {
        // Convert String to character array
        char ch1[] = X.toCharArray();
        char ch2[] = Y.toCharArray();
        int count = 0;

        // Traverse the string X
        for (int i = 0; i < X.length(); i++) {

            int c = 0;

            // Case 1
            if (ch1[i] == ch2[i])
                continue;

            // Case 2
            else if (ch1[i] < ch2[i]) {

                // Add the difference/K to
                // the count
                if (((int)ch2[i]
                     - (int)ch1[i])
                    >= K) {
                    c = ((int)ch2[i]
                         - (int)ch1[i])
                        / K;
                }

                // Add the difference%K to
                // the count
                c += ((int)ch2[i]
                      - (int)ch1[i])
                     % K;
            }

            // Case 3
            else {
                int t = 90 - (int)ch1[i];
                t += (int)ch2[i] - 65 + 1;

                // Add the difference/K to
                // the count
                if (t >= K)
                    c = t / K;

                // Add the difference%K to
                // the count
                c += (t % K);
            }

            count += c;
        }

        // Print the answer
        System.out.print(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String X = "ABCT", Y = "PBDI";
        int K = 6;
        countOperations(X, Y, K);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count minimum increments
# by 1 or K required to convert X to Y
def countOperations(X, Y, K):
    count = 0

    # Traverse the string X
    for i in range(len(X)):
        c = 0

        # Case 1
        if (X[i] == Y[i]):
            continue

        # Case 2
        elif (X[i] < Y[i]):

            # Add the difference/K to
            # the count
            if ((ord(Y[i]) - ord(X[i])) >= K):
                c = (ord(Y[i]) - ord(X[i])) // K

            # Add the difference%K to
            # the count
            c += (ord(Y[i]) - ord(X[i])) % K

        # Case 3
        else:
            t = 90 - ord(X[i])
            t += ord(Y[i]) - 65 + 1

            # Add the difference/K to
            # the count
            if (t >= K):
                c = t // K

            # Add the difference%K to
            # the count
            c += (t % K)
        count += c

    # Print the answer
    print(count)

# Driver Code
X = "ABCT"
Y = "PBDI"
K = 6
countOperations(X, Y, K)

# This code is contributed by aditya7409.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to count minimum increments
  // by 1 or K required to convert X to Y
  static void countOperations(
    string X, string Y, int K)
  {
    // Convert String to character array
    char[] ch1 = X.ToCharArray();
    char[] ch2 = Y.ToCharArray();
    int count = 0;

    // Traverse the string X
    for (int i = 0; i < X.Length; i++) {

      int c = 0;

      // Case 1
      if (ch1[i] == ch2[i])
        continue;

      // Case 2
      else if (ch1[i] < ch2[i]) {

        // Add the difference/K to
        // the count
        if (((int)ch2[i]
             - (int)ch1[i])
            >= K) {
          c = ((int)ch2[i]
               - (int)ch1[i])
            / K;
        }

        // Add the difference%K to
        // the count
        c += ((int)ch2[i]
              - (int)ch1[i])
          % K;
      }

      // Case 3
      else {
        int t = 90 - (int)ch1[i];
        t += (int)ch2[i] - 65 + 1;

        // Add the difference/K to
        // the count
        if (t >= K)
          c = t / K;

        // Add the difference%K to
        // the count
        c += (t % K);
      }

      count += c;
    }

    // Print the answer
    Console.WriteLine(count);
  }

  // Driver code
  static void Main()
  {
    string X = "ABCT", Y = "PBDI";
    int K = 6;
    countOperations(X, Y, K);
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to count minimum increments
      // by 1 or K required to convert X to Y
      function countOperations(X, Y, K)
      {
        var count = 0;

        // Traverse the string X
        for (var i = 0; i < X.length; i++)
        {
          var c = 0;

          // Case 1
          if (X[i] === Y[i]) continue;

          // Case 2
          else if (X[i].charCodeAt(0) < Y[i].charCodeAt(0))
          {

            // Add the difference/K to
            // the count
            if (Y[i].charCodeAt(0) - X[i].charCodeAt(0) >= K)
            {
              c = (Y[i].charCodeAt(0) - X[i].charCodeAt(0)) / K;
            }

            // Add the difference%K to
            // the count
            c += (Y[i].charCodeAt(0) - X[i].charCodeAt(0)) % K;
          }

          // Case 3
          else {
            var t = 90 - X[i].charCodeAt(0);
            t += Y[i].charCodeAt(0) - 65 + 1;

            // Add the difference/K to
            // the count
            if (t >= K) {
              c = parseInt(t / K);
            }

            // Add the difference%K to
            // the count
            c += parseInt(t % K);
          }
          count = parseInt(count + c);
        }

        // Print the answer
        document.write(count + "<br>");
      }

      // Driver Code
      var X = "ABCT",
        Y = "PBDI";
      var K = 6;
      countOperations(X, Y, K);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
11
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)