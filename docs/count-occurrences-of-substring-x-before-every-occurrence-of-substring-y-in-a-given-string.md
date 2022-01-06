# 在给定字符串中每次出现子串 Y 之前，统计子串 X 的出现次数

> 原文:[https://www . geesforgeks . org/count-出现次数-substring-x-每次出现前-substring-y-in-给定字符串/](https://www.geeksforgeeks.org/count-occurrences-of-substring-x-before-every-occurrence-of-substring-y-in-a-given-string/)

给定分别由 **N** 、 **A** 和 **B** 字符组成的三个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 、 **X** 和 **Y** ，任务是在给定字符串 **S** 中的子字符串 **Y** 每次出现之前找到子字符串 **X** 的出现次数。

**示例:**

> **输入**S =“abcdeffabc”，X =“def”，Y =“ABC”
> **输出:** 0 2
> **解释:**
> Y 的第一次出现(=“ABC”):X 的出现次数(=“def”)= 0。
> Y 的第二次出现:X 的出现次数= 0。
> 
> **输入:** S = "accccbbbbbbaaa "，X = "a "，Y = " b "
> T3】输出:0 6 6 6 6

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如**计数**，它存储 **X** 的总出现次数。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   如果范围**【I，B】**内的子串等于 **Y** ，那么将**计数**增加 **1** 。
    *   如果范围**【I，A】**内的子串等于 **X** ，则打印**计数**的值作为字符串 **Y** 在字符串 **X** 当前出现之前的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count occurrences of
// the string Y in the string S for
// every occurrence of X in S
void countOccurrences(string S,
                      string X,
                      string Y)
{
    // Stores the count of
    // occurrences of X
    int count = 0;

    // Stores the lengths of the
    // three strings
    int N = S.length(), A = X.length();
    int B = Y.length();

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If the current substring
        // is Y, then increment the
        // value of count by 1
        if (S.substr(i, B) == Y)
            count++;

        // If the current substring
        // is X, then print the count
        if (S.substr(i, A) == X)
            cout << count << " ";
    }
}

// Driver Code
int main()
{
    string S = "abcdefdefabc";
    string X = "abc";
    string Y = "def";
    countOccurrences(S, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to count occurrences of
    // the string Y in the string S for
    // every occurrence of X in S
    static void countOccurrences(String S, String X,
                                 String Y)
    {
        // Stores the count of
        // occurrences of X
        int count = 0;

        // Stores the lengths of the
        // three strings
        int N = S.length(), A = X.length();
        int B = Y.length();

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // If the current substring
            // is Y, then increment the
            // value of count by 1
            if (S.substring(i, Math.min(N, i + B))
                    .equals(Y))
                count++;

            // If the current substring
            // is X, then print the count
            if (S.substring(i, Math.min(N, i + A))
                    .equals(X))
                System.out.print(count + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "abcdefdefabc";
        String X = "abc";
        String Y = "def";
        countOccurrences(S, X, Y);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count occurrences of
# the string Y in the string S for
# every occurrence of X in S
def countOccurrences(S, X, Y):

    # Stores the count of
    # occurrences of X
    count = 0

    # Stores the lengths of the
    # three strings
    N = len(S)
    A = len(X)
    B = len(Y)

    # Traverse the string S
    for  i in range( 0,  N):

        # If the current substring
        # is Y, then increment the
        # value of count by 1
        if (S[i: i+B] == Y):
            count+=1

        # If the current substring
        # is X, then print the count
        if (S[i:i+A] == X):
            print(count, end = " ")

# Driver Code
S = "abcdefdefabc"
X = "abc"
Y = "def"
countOccurrences(S, X, Y)

# This code is contributed by rohitsingh07052.
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Function to count occurrences of
    // the string Y in the string S for
    // every occurrence of X in S
    static void countOccurrences(string S, string X,
                                 string Y)
    {
        // Stores the count of
        // occurrences of X
        int count = 0;

        // Stores the lengths of the
        // three strings
        int N = S.Length, A = X.Length;
        int B = Y.Length;
        int P = Math.Min(A, Math.Min(N, B));

        // Traverse the string S
        for (int i = 0; i < N - P + 1; i++) {

            // If the current substring
            // is Y, then increment the
            // value of count by 1

            if (S.Substring(i, Math.Min(N, B)).Equals(Y))
                count++;

            // If the current substring
            // is X, then print the count
            if (S.Substring(i, Math.Min(N, A)).Equals(X))
                Console.Write(count + " ");
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string S = "abcdefdefabc";
        string X = "abc";
        string Y = "def";
        countOccurrences(S, X, Y);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Js program for the above approach

// Function to count occurrences of
// the string Y in the string S for
// every occurrence of X in S
function countOccurrences( S, X, Y){
    // Stores the count of
    // occurrences of X
    let count = 0;
    // Stores the lengths of the
    // three strings
    let N = S.length, A = X.length;
    let B = Y.length;
    // Traverse the string S
    for (let i = 0; i < N; i++) {
        // If the current substring
        // is Y, then increment the
        // value of count by 1
        if (S.substr(i, B) == Y)
            count++;

        // If the current substring
        // is X, then print the count
        if (S.substr(i, A) == X)
            document.write(count," ");
    }
}

// Driver Code
let S = "abcdefdefabc", X = "abc", Y = "def";
countOccurrences(S, X, Y);

</script>
```

**Output:** 

```
0 2
```

***时间复杂度:** O(N*(A + B))*
***辅助空间:** O(1)*