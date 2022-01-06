# 尽量减少所需的字符对的互换，使得字符串中没有两个相邻的字符是相同的

> 原文:[https://www . geesforgeks . org/minimum-交换字符对-必需-字符串中没有两个相邻字符相同/](https://www.geeksforgeeks.org/minimize-swaps-of-pairs-of-characters-required-such-that-no-two-adjacent-characters-in-the-string-are-same/)

给定一个由 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到需要交换的最小字符对数，使得相邻的两个字符不相同。如果不可能，则打印**-1”**。

**示例:**

> **输入:** S = "ABAACD"
> **输出:** 1
> **解释:**交换 S[3]和 S[4]将给定字符串 S 修改为“ABACAD”。由于没有两个相邻字符相同，因此所需的最小操作数为 1。
> 
> **输入:**S =【AABA】
> **输出:** -1

**方法:**给定的问题可以通过[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来解决。其思想是生成一对索引交换的所有可能组合，然后如果生成的字符串没有相邻字符相同，则使用最小交换，然后打印执行的最小交换操作数。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **minimumSwaps(字符串& str，int & minimumSwaps，int swaps=0，int idx)** 并执行以下操作:
    *   如果字符串 **str** 的相邻字符不同，那么将**最小互换**的值更新为**最小互换**和**互换**的最小值。
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【idx，N】**，并执行以下操作:
        *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N】**，并执行以下操作:
            *   互换[弦](https://www.geeksforgeeks.org/category/data-structures/c-strings/)中 **i** 和 **j** 位置的字符。
            *   调用[函数](https://www.geeksforgeeks.org/functions-in-c/) **minimumSwaps(str，minimumSwaps，swaps+1，i + 1)** 找到其他可能的交换对，生成结果字符串。
            *   交换字符串 **S** 中 **i** 和 **j** 位置的字符。
*   初始化变量，将 **ansSwaps** 设为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 来存储所需的最小交换次数。
*   调用函数 **minimumSwaps(str，ansSwaps)** 找到使所有相邻字符不同所需的最小交换次数。
*   完成上述步骤后，如果**ansswap**的值为 **INT_MAX，**则打印 **-1** 。否则，打印 **ansSwaps** 的值作为最终的最小交换。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if S
// contains any pair of
// adjacent characters that are same
bool check(string& S)
{
    // Traverse the string S
    for (int i = 1; i < S.length(); i++) {

        // If current pair of adjacent
        // characters are the same
        if (S[i - 1] == S[i]) {
            return false;
        }
    }

    // Return true
    return true;
}

// Utility function to find the minimum number
// of swaps of pair of characters required
// to make all pairs of adjacent characters different
void minimumSwaps(string& S, int& ansSwaps,
                  int swaps = 0, int idx = 0)
{
    // Check if the required string
    // is formed already
    if (check(S)) {
        ansSwaps = min(ansSwaps, swaps);
    }

    // Traverse the string S
    for (int i = idx;
         i < S.length(); i++) {

        for (int j = i + 1;
             j < S.length(); j++) {

            // Swap the characters at i
            // and j position
            swap(S[i], S[j]);
            minimumSwaps(S, ansSwaps,
                         swaps + 1, i + 1);

            // Swap for Backtracking
            // Step
            swap(S[i], S[j]);
        }
    }
}

// Function to find the minimum number
// of swaps of pair of characters required
// to make all pairs of adjacent characters different
void findMinimumSwaps(string& S)
{

    // Stores the resultant minimum
    // number of swaps required
    int ansSwaps = INT_MAX;

    // Function call to find the
    // minimum swaps required
    minimumSwaps(S, ansSwaps);

    // Print the result
    if (ansSwaps == INT_MAX)
        cout << "-1";
    else
        cout << ansSwaps;
}

// Driver Code
int main()
{
    string S = "ABAACD";
    findMinimumSwaps(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{
    static int ansSwaps ;

// Function to check if S
// contains any pair of
// adjacent characters that are same
static boolean check(char[] S)
{

    // Traverse the String S
    for (int i = 1; i < S.length; i++) {

        // If current pair of adjacent
        // characters are the same
        if (S[i - 1] == S[i]) {
            return false;
        }
    }

    // Return true
    return true;
}

// Utility function to find the minimum number
// of swaps of pair of characters required
// to make all pairs of adjacent characters different
static void minimumSwaps(char[] S,
                  int swaps, int idx)
{

    // Check if the required String
    // is formed already
    if (check(S)) {
        ansSwaps = Math.min(ansSwaps, swaps);
    }

    // Traverse the String S
    for (int i = idx;
         i < S.length; i++) {

        for (int j = i + 1;
             j < S.length; j++) {

            // Swap the characters at i
            // and j position
            swap(S,i,j);
            minimumSwaps(S,
                         swaps + 1, i + 1);

            // Swap for Backtracking
            // Step
            S= swap(S,i,j);
        }
    }
}
static char[] swap(char []arr, int i, int j){
    char temp= arr[i];
    arr[i]=arr[j];
    arr[j]=temp;
    return arr;
}

// Function to find the minimum number
// of swaps of pair of characters required
// to make all pairs of adjacent characters different
static void findMinimumSwaps(char[] S)
{

    // Stores the resultant minimum
    // number of swaps required
    ansSwaps = Integer.MAX_VALUE;

    // Function call to find the
    // minimum swaps required
    minimumSwaps(S, 0,0);

    // Print the result
    if (ansSwaps == Integer.MAX_VALUE)
        System.out.print("-1");
    else
        System.out.print(ansSwaps);
}

// Driver Code
public static void main(String[] args)
{
    String S = "ABAACD";
    findMinimumSwaps(S.toCharArray());

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys
ansSwaps = 0

# Function to check if S
# contains any pair of
# adjacent characters that are same
def check(S):

    # Traverse the String S
    for i in range(1, len(S)):

        # If current pair of adjacent
        # characters are the same
        if (S[i - 1] == S[i]):
            return False

    # Return true
    return True

# Utility function to find the minimum number
# of swaps of pair of characters required
# to make all pairs of adjacent characters different
def minimumSwaps(S, swaps , idx):
    global ansSwaps

    # Check if the required String
    # is formed already
    if (check(S)):
        ansSwaps = 1+min(ansSwaps, swaps)

    # Traverse the String S
    for i in range(idx, len(S)):
        for j in range(i + 1, len(S)):

            # Swap the characters at i
            # and j position
            swap(S, i, j)
            minimumSwaps(S, swaps + 1, i + 1)

            # Swap for Backtracking
            # Step
            S = swap(S, i, j)

def swap(arr , i , j):
    temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
    return arr

# Function to find the minimum number
# of swaps of pair of characters required
# to make all pairs of adjacent characters different
def findMinimumSwaps(S):
    global ansSwaps

    # Stores the resultant minimum
    # number of swaps required
    ansSwaps = sys.maxsize

    # Function call to find the
    # minimum swaps required
    minimumSwaps(S, 0,0)

    # Print the result
    if (ansSwaps == sys.maxsize):
        print("-1")
    else:
        print(ansSwaps)

S = "ABAACD"
findMinimumSwaps(S.split())

# This code is contributed by rameshtravel07.
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{
    static int ansSwaps ;

// Function to check if S
// contains any pair of
// adjacent characters that are same
static bool check(char[] S)
{

    // Traverse the String S
    for (int i = 1; i < S.Length; i++) {

        // If current pair of adjacent
        // characters are the same
        if (S[i - 1] == S[i]) {
            return false;
        }
    }

    // Return true
    return true;
}

// Utility function to find the minimum number
// of swaps of pair of characters required
// to make all pairs of adjacent characters different
static void minimumSwaps(char[] S,
                  int swaps, int idx)
{

    // Check if the required String
    // is formed already
    if (check(S)) {
        ansSwaps = Math.Min(ansSwaps, swaps);
    }

    // Traverse the String S
    for (int i = idx;
         i < S.Length; i++) {

        for (int j = i + 1;
             j < S.Length; j++) {

            // Swap the characters at i
            // and j position
            swap(S,i,j);
            minimumSwaps(S,
                         swaps + 1, i + 1);

            // Swap for Backtracking
            // Step
            S= swap(S,i,j);
        }
    }
}
static char[] swap(char []arr, int i, int j){
    char temp= arr[i];
    arr[i]=arr[j];
    arr[j]=temp;
    return arr;
}

// Function to find the minimum number
// of swaps of pair of characters required
// to make all pairs of adjacent characters different
static void findMinimumSwaps(char[] S)
{

    // Stores the resultant minimum
    // number of swaps required
    ansSwaps = int.MaxValue;

    // Function call to find the
    // minimum swaps required
    minimumSwaps(S, 0,0);

    // Print the result
    if (ansSwaps == int.MaxValue)
        Console.Write("-1");
    else
        Console.Write(ansSwaps);
}

// Driver Code
public static void Main(String[] args)
{
    String S = "ABAACD";
    findMinimumSwaps(S.ToCharArray());

}
}

// This code is contributed by 29AjayKumar.
```

## java 描述语言

```
<script>

// javascript program for the above approach
var ansSwaps ;

// Function to check if S
// contains any pair of
// adjacent characters that are same
function check(S)
{

    // Traverse the String S
    for (var i = 1; i < S.length; i++) {

        // If current pair of adjacent
        // characters are the same
        if (S[i - 1] == S[i]) {
            return false;
        }
    }

    // Return true
    return true;
}

// Utility function to find the minimum number
// of swaps of pair of characters required
// to make all pairs of adjacent characters different
function minimumSwaps(S, swaps , idx)
{

    // Check if the required String
    // is formed already
    if (check(S)) {
        ansSwaps = Math.min(ansSwaps, swaps);
    }

    // Traverse the String S
    for (var i = idx;
         i < S.length; i++) {

        for (var j = i + 1;
             j < S.length; j++) {

            // Swap the characters at i
            // and j position
            swap(S,i,j);
            minimumSwaps(S,
                         swaps + 1, i + 1);

            // Swap for Backtracking
            // Step
            S= swap(S,i,j);
        }
    }
}
function swap(arr , i , j){
    var temp= arr[i];
    arr[i]=arr[j];
    arr[j]=temp;
    return arr;
}

// Function to find the minimum number
// of swaps of pair of characters required
// to make all pairs of adjacent characters different
function findMinimumSwaps(S)
{

    // Stores the resultant minimum
    // number of swaps required
    ansSwaps = Number.MAX_VALUE;

    // Function call to find the
    // minimum swaps required
    minimumSwaps(S, 0,0);

    // Print the result
    if (ansSwaps == Number.MAX_VALUE)
        document.write("-1");
    else
        document.write(ansSwaps);
}

// Driver Code

    var S = "ABAACD";
    findMinimumSwaps(S.split(''));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>3</sup>* 2<sup>N</sup>)*
***辅助空间:** O(1)*