# 获得给定字符串所需的从末尾到前面的 X 或 Y 字符的最少追加次数

> 原文:[https://www . geeksforgeeks . org/从前端到前端获取给定字符串所需的最小附加字符数/](https://www.geeksforgeeks.org/minimum-number-of-appends-of-x-or-y-characters-from-the-end-to-the-front-required-to-obtain-given-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和两个正整数 **X** 和 **Y** ，任务是找到获取原始字符串所需的最小操作数。在每次操作中，在每次操作中分别从字符串的末尾向字符串的前面追加 **X** 或 **Y** 字符。

**示例:**

> **输入:**S =“geeksgeerks”，X = 5，Y = 3
> **输出:** 3
> **解释:**
> 下面是执行的操作:
> **操作 1:** 从字符串 S 的后面追加 5 个字符到字符串 S 的前面，现在更新后的字符串是“GeeksGeeksfor”。
> **操作 2:** 从字符串 S 的后面追加 3 个字符到字符串 S 的前面，现在更新后的字符串是“forGeeksGeeks”。
> **操作 3:** 从字符串 S 的后面追加 5 个字符到字符串 S 的前面，现在更新后的字符串是“GeeksforGeeks”。
> 因此，所需操作的最小计数为 3。
> 
> **输入:**S =“AbcDef”，X = 1，Y = 2
> **输出:** 4
> **说明:**
> 下面是执行的操作:
> **操作 1:** 从字符串 S 的后面追加 1 个字符到字符串 S 的前面，现在更新后的字符串是“fAbcDe”。
> **操作 2:** 从字符串 S 的后面追加 2 个字符到字符串 S 的前面，现在更新后的字符串是“fDeAbc”。
> **操作 3:** 从字符串 S 的后面追加 1 个字符到字符串 S 的前面，现在更新后的字符串是“cfDeAb”。
> **操作 4:** 从字符串 S 的后面追加 2 个字符到字符串 S 的前面，现在更新后的字符串是“AbcDef”。
> 因此，所需的最小操作数为 4。

**方法:**思路是将给定字符串中的 **X** 和 **Y** 字符分别追加到字符串的前面，并在执行操作时记录操作的次数。以下是步骤:

*   将计数初始化为存储最小操作的 **0** 。
*   将给定的字符串 **S** 存储在另一个需要执行操作的字符串(比如**新字符串**)中。
*   现在在**新字符串**上执行以下操作，直到它等于 **S** :
    *   从字符串**新闻字符串**的末尾追加 **X** 字符，并将**计数**增加 **1** 。
    *   如果**新闻字符串**与字符串 **S** 相同。
    *   从字符串**的末尾追加 **Y** 字符，新字符串**将**计数**增加 **1** 。
    *   如果**新闻字符串**与字符串 **S** 相同。
*   完成上述步骤后，打印**计数**的值，作为所需的最小操作次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the minimum operations
// required to get the given string after
// appending m or n characters from the end
// to the front of the string in each operation
int minimumOperations(string orig_str, int m, int n)
{

    // Store the original string
    string orig = orig_str;

    // Stores the count of operations
    int turn = 1;
    int j = 1;

    // Traverse the string
    for(auto i : orig_str)
    {

        // Cut m letters from end
        string m_cut = orig_str.substr(
            orig_str.length() - m);

        orig_str.erase(orig_str.length() - m);

        // Add cut m letters to beginning
        orig_str = m_cut + orig_str;

        // Update j
        j = j + 1;

        // Check if strings are the same
        if (orig != orig_str)
        {
            turn = turn + 1;

            // Cut n letters from end
            string n_cut = orig_str.substr(
                orig_str.length() - n);
            orig_str.erase(orig_str.length() - n);

            // Add cut n letters to beginning
            orig_str = n_cut + orig_str;

            // Update j
            j = j + 1;
        }

        // Check if strings are the same
        if (orig == orig_str)
        {
            break;
        }

        // Update the turn
        turn = turn + 1;
    }
    cout << turn;
}

// Driver Code
int main()
{

    // Given string S
    string S = "GeeksforGeeks";

    int X = 5, Y = 3;

    // Function Call
    minimumOperations(S, X, Y);
    return 0;
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the minimum operations
// required to get the given string after
// appending m or n characters from the end
// to the front of the string in each operation
static void minimumOperations(String orig_str,
                              int m, int n)
{

    // Store the original string
    String orig = orig_str;

    // Stores the count of operations
    int turn = 1;
    int j = 1;

    // Traverse the string
    for(int i = 0; i < orig_str.length(); i++)
    {

        // Cut m letters from end
        String m_cut = orig_str.substring(
            orig_str.length() - m);

        orig_str = orig_str.substring(
            0, orig_str.length() - m);

        // Add cut m letters to beginning
        orig_str = m_cut + orig_str;

        // Update j
        j = j + 1;

        // Check if strings are the same
        if (!orig.equals(orig_str))
        {
            turn = turn + 1;

            // Cut n letters from end
            String n_cut = orig_str.substring(
                orig_str.length() - n);
            orig_str = orig_str.substring(
                0, orig_str.length() - n);

            // Add cut n letters to beginning
            orig_str = n_cut + orig_str;

            // Update j
            j = j + 1;
        }

        // Check if strings are the same
        if (orig.equals(orig_str))
        {
            break;
        }

        // Update the turn
        turn = turn + 1;
    }
    System.out.println( turn );
}

// Driver Code
public static void main(String[] args)
{

    // Given string S
    String S = "GeeksforGeeks";

    int X = 5, Y = 3;

    // Function Call
    minimumOperations(S, X, Y);
}
}

// This code is contributed by akhilsaini
```

## 计算机编程语言

```
# Python program for the above approach

# Function to find the minimum operations
# required to get the given string after
# appending m or n characters from the end
# to the front of the string in each operation
def minimumOperations(orig_str, m, n):

    # Store the original string
    orig = orig_str

    # Stores the count of operations
    turn = 1
    j = 1

    # Traverse the string
    for i in orig_str:

        # Cut m letters from end
        m_cut = orig_str[-m:]

        orig_str = orig_str.replace(' ', '')[:-m]

        # Add cut m letters to beginning
        orig_str = m_cut + orig_str

        # Update j
        j = j + 1

        # Check if strings are the same
        if orig != orig_str:
            turn = turn + 1

            # Cut n letters from end
            n_cut = orig_str[-n:]
            orig_str = orig_str.replace(' ', '')[:-n]

            # Add cut n letters to beginning
            orig_str = n_cut + orig_str

            # Update j
            j = j + 1

        # Check if strings are the same
        if orig == orig_str:
            break

        # Update the turn
        turn = turn + 1

    print(turn)

# Driver Code

# Given string S
S = "GeeksforGeeks"

X = 5
Y = 3

# Function Call
minimumOperations(S, X, Y)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum operations
// required to get the given string after
// appending m or n characters from the end
// to the front of the string in each operation
static void minimumOperations(string orig_str, int m,
                              int n)
{

    // Store the original string
    string orig = orig_str;

    // Stores the count of operations
    int turn = 1;
    int j = 1;

    // Traverse the string
    for(int i = 0; i < orig_str.Length; i++)
    {

        // Cut m letters from end
        string m_cut = orig_str.Substring(
            orig_str.Length - m);

        orig_str = orig_str.Substring(
            0, orig_str.Length - m);

        // Add cut m letters to beginning
        orig_str = m_cut + orig_str;

        // Update j
        j = j + 1;

        // Check if strings are the same
        if (!orig.Equals(orig_str))
        {
            turn = turn + 1;

            // Cut n letters from end
            String n_cut = orig_str.Substring(
                orig_str.Length - n);
            orig_str = orig_str.Substring(
                0, orig_str.Length - n);

            // Add cut n letters to beginning
            orig_str = n_cut + orig_str;

            // Update j
            j = j + 1;
        }

        // Check if strings are the same
        if (orig.Equals(orig_str))
        {
            break;
        }

        // Update the turn
        turn = turn + 1;
    }
    Console.WriteLine(turn);
}

// Driver Code
public static void Main()
{

    // Given string S
    string S = "GeeksforGeeks";

    int X = 5, Y = 3;

    // Function Call
    minimumOperations(S, X, Y);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the minimum operations
    // required to get the given string after
    // appending m or n characters from the end
    // to the front of the string in each operation
    function minimumOperations(orig_str, m, n)
    {

        // Store the original string
        let orig = orig_str;

        // Stores the count of operations
        let turn = 1;
        let j = 1;

        // Traverse the string
        for(let i = 0; i < orig_str.length; i++)
        {

            // Cut m letters from end
            let m_cut = orig_str.substring(orig_str.length - m);

            orig_str = orig_str.substring(0, orig_str.length - m);

            // Add cut m letters to beginning
            orig_str = m_cut + orig_str;

            // Update j
            j = j + 1;

            // Check if strings are the same
            if (orig != orig_str)
            {
                turn = turn + 1;

                // Cut n letters from end
                let n_cut = orig_str.substring(orig_str.length - n);
                orig_str = orig_str.substring(0, orig_str.length - n);

                // Add cut n letters to beginning
                orig_str = n_cut + orig_str;

                // Update j
                j = j + 1;
            }

            // Check if strings are the same
            if (orig == orig_str)
            {
                break;
            }

            // Update the turn
            turn = turn + 1;
        }
        document.write(turn);
    }

    // Given string S
    let S = "GeeksforGeeks";

    let X = 5, Y = 3;

    // Function Call
    minimumOperations(S, X, Y);

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)