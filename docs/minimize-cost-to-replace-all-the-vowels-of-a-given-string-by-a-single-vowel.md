# 将给定字符串的所有元音替换为单个元音的成本降至最低

> 原文:[https://www . geesforgeks . org/最小化按单个元音替换给定字符串的所有元音的成本/](https://www.geeksforgeeks.org/minimize-cost-to-replace-all-the-vowels-of-a-given-string-by-a-single-vowel/)

给定一个字符串 **S，**的任务是找到将给定字符串中的所有[元音](https://www.geeksforgeeks.org/program-count-vowels-string-iterative-recursive/) **{a，e，I，o，u}** 转换为其中任何一个的最小成本。转换元音的成本由 [ASCII](https://www.geeksforgeeks.org/program-print-ascii-value-character/) 值的变化给出。
**举例:**

> **输入:**S = " geeks forgeeks "
> T3】输出: 10
> **解释:**
> e 的计数= 4
> o 的计数= 1
> 从‘o’到‘e’的转换成本 ABS(‘o’–‘e’)= 10。
> 因此，输出为 10。
> **输入:** S =【编码】
> **输出:** 6
> **解释:**
> 从‘o’到‘I’的转换成本 ABS(‘o’–‘I’)= 6。
> 因此，输出为 10。

**方法:**
思路是计算将字符串中的每个元音转换为其中一个元音的单独成本 **{a，e，I，o，u}** ，选择成本最小的元音。按照以下步骤操作:

*   初始化 5 个变量 ***cA、cE、cI、cO、*** 和 ***cU*** 成本为 **0** ，分别存储元音**的成本{a、e、I、o、u}** 。
*   遍历字符串，并为每个元音找到将其转换为所有其他元音的成本，并将其分别存储在变量 ***cA、cE、cI、cO、*** 和 ***cU*** 中。
*   将所有元音转换为单个元音的最小成本由 ***min(cA，cE，cI，cO，cU)给出。**T3】*

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that return true if the
// given character is a vowel
bool isVowel(char ch)
{
    if (ch == 'a' or ch == 'e'
        or ch == 'i' or ch == 'o'
        or ch == 'u')
        return true;
    else
        return false;
}

// Function to return the minimum
// cost to convert all the vowels
// of a string to a single one
int minCost(string S)
{
    // Stores count of
    // respective vowels
    int cA = 0;
    int cE = 0;
    int cI = 0;
    int cO = 0;
    int cU = 0;

    // Iterate through the string
    for (int i = 0; i < S.size(); i++) {

        // If a vowel is encountered
        if (isVowel(S[i])) {

            // Calculate the cost
            cA += abs(S[i] - 'a');
            cE += abs(S[i] - 'e');
            cI += abs(S[i] - 'i');
            cO += abs(S[i] - 'o');
            cU += abs(S[i] - 'u');
        }
    }

    // Return the minimum cost
    return min(min(min(min(cA, cE),
                    cI),
                cO),
            cU);
}

// Driver Code
int main()
{
    string S = "geeksforgeeks";

    cout << minCost(S) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that return true if the
// given character is a vowel
static boolean isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u')
        return true;
    else
        return false;
}

// Function to return the minimum
// cost to convert all the vowels
// of a string to a single one
static int minCost(String S)
{

    // Stores count of
    // respective vowels
    int cA = 0;
    int cE = 0;
    int cI = 0;
    int cO = 0;
    int cU = 0;

    // Iterate through the string
    for(int i = 0; i < S.length(); i++)
    {

        // If a vowel is encountered
        if (isVowel(S.charAt(i)))
        {

            // Calculate the cost
            cA += Math.abs(S.charAt(i) - 'a');
            cE += Math.abs(S.charAt(i) - 'e');
            cI += Math.abs(S.charAt(i) - 'i');
            cO += Math.abs(S.charAt(i) - 'o');
            cU += Math.abs(S.charAt(i) - 'u');
        }
    }

    // Return the minimum cost
    return Math.min(Math.min(Math.min(Math.min(cA, cE),
                                         cI), cO), cU);
}

// Driver code
public static void main(String[] args)
{
    String S = "geeksforgeeks";

    System.out.println(minCost(S));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that return true if the
# given character is a vowel
def isVowel(ch):

    if (ch == 'a' or ch == 'e' or
        ch == 'i' or ch == 'o' or
        ch == 'u'):
        return True;
    else:
        return False;

# Function to return the minimum
# cost to convert all the vowels
# of a string to a single one
def minCost(S):

    # Stores count of
    # respective vowels
    cA = 0;
    cE = 0;
    cI = 0;
    cO = 0;
    cU = 0;

    # Iterate through the string
    for i in range(len(S)):

        # If a vowel is encountered
        if (isVowel(S[i])):

            # Calculate the cost
            cA += abs(ord(S[i]) - ord('a'));
            cE += abs(ord(S[i]) - ord('e'));
            cI += abs(ord(S[i]) - ord('i'));
            cO += abs(ord(S[i]) - ord('o'));
            cU += abs(ord(S[i]) - ord('u'));

    # Return the minimum cost
    return min(min(min(min(cA, cE), cI), cO), cU);

# Driver code
S = "geeksforgeeks";

print(minCost(S))

# This code is contributed by grand_master
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that return true if the
// given character is a vowel
static bool isVowel(char ch)
{
    if (ch == 'a' || ch == 'e' ||
        ch == 'i' || ch == 'o' ||
        ch == 'u')
        return true;
    else
        return false;
}

// Function to return the minimum
// cost to convert all the vowels
// of a string to a single one
static int minCost(String S)
{

    // Stores count of
    // respective vowels
    int cA = 0;
    int cE = 0;
    int cI = 0;
    int cO = 0;
    int cU = 0;

    // Iterate through the string
    for(int i = 0; i < S.Length; i++)
    {

        // If a vowel is encountered
        if (isVowel(S[i]))
        {

            // Calculate the cost
            cA += Math.Abs(S[i] - 'a');
            cE += Math.Abs(S[i] - 'e');
            cI += Math.Abs(S[i] - 'i');
            cO += Math.Abs(S[i] - 'o');
            cU += Math.Abs(S[i] - 'u');
        }
    }

    // Return the minimum cost
    return Math.Min(Math.Min(
           Math.Min(Math.Min(cA, cE),
                       cI), cO), cU);
}

// Driver code
public static void Main(String[] args)
{
    String S = "geeksforgeeks";

    Console.WriteLine(minCost(S));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program f|| the above approach

// Function that return true if the
// given character is a vowel
function isVowel(ch)
{
    if (ch == 'a' || ch == 'e'
        || ch == 'i' || ch == 'o'
        || ch == 'u')
        return true;
    else
        return false;
}

// Function to return the minimum
// cost to convert all the vowels
// of a string to a single one
function minCost(S)
{
    // St||es count of
    // respective vowels
    var cA = 0;
    var cE = 0;
    var cI = 0;
    var cO = 0;
    var cU = 0;

    // Iterate through the string
    for(var i = 0; i < S.length; i++) {

        // If a vowel is encountered
        if (isVowel(S[i])) {

            // Calculate the cost
            cA += Math.abs(S.charCodeAt(i) - 'a'.charCodeAt(0));
            cE += Math.abs(S.charCodeAt(i) - 'e'.charCodeAt(0));
            cI += Math.abs(S.charCodeAt(i) - 'i'.charCodeAt(0));
            cO += Math.abs(S.charCodeAt(i) - 'o'.charCodeAt(0));
            cU += Math.abs(S.charCodeAt(i) - 'u'.charCodeAt(0));
        }
    }

    // Return the Math.minimum cost
    return Math.min(Math.min(Math.min(Math.min(cA, cE),
                    cI),
                cO),
            cU);
}

// Driver Code
var S = "geeksforgeeks";
document.write(minCost(S));

// This code is contributed by importantly.
</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*