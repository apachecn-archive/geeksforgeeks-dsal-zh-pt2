# 不含 3 个相邻字符可插入的 X 最大个数为 X

> 原文:[https://www . geeksforgeeks . org/可插入的最大 x 个相邻字符数为-x/](https://www.geeksforgeeks.org/maximum-count-of-x-that-can-be-inserted-with-no-3-adjacent-characters-are-x/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)、**字符串**和一个字符 **X** ，任务是找到要插入到字符串中的字符 **X** 的最大数量，使得没有三个连续的字符等于 **X** 。如果找不到这样的字符串，则打印 **-1** 。

**示例:**

> **输入:**str = " xxxy "，X = X
> **输出:** 3
> **说明:**
> 在位置 4 插入一个‘X’:“xxxy”。
> 在位置 7 插入两个‘x’:“xxyxxxx”
> 现在不能再插入‘x’了，因为这会导致大小为 3 的子串，其中包含所有的 x。
> 因此所需计数为 3。
> 
> **输入:** str = "gfg "，X = ' X '
> T3】输出: 8

**方法:**思路是统计 **X** 可以插入的所有位置，然后减去字符串中已经存在的 **X** 的个数。
以下是步骤:

1.  可以插入到字符串中的 **X** 的最大数量是 **2 * (N + 1)** 个字符，因为可以在字符串的开始和结束以及每个连续字符之间插入两个 **X** 。
2.  现在，找到大小为 **1** 或 **2** 的连续 **X** 的组数，并将其存储在变量 **countX** 中。
3.  给定字符串中可以插入的 **X** 的数量为 **2 *(要插入的位置数+1)–找到的 Xs** 的数量。
4.  总之，一个简单的数学公式，**2 *(N+1)–(N–Xs)**可以用来找到最终的答案。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to find maximum count of
// X that are to be inserted into str such that
// no three consecutive characters are equal to X
int maxNumberOfXAddedUtil(string str, char X)
{

    // Stores count of consecutive X
    int countX = 0;

    // Stores count of characters which
    // is not equal to X
    int countNotX = 0;

    // Iterate over characters of string, str
    for (int i = 0; i < str.size(); i++)
    {

        // If current character is X
        if (str[i] == X)
        {

            // Update  countX
            countX++;
        }

        // If countX is less
        // than 3
        else if (countX < 3)
        {

            // Update countNotX
            countNotX++;

            // Update countX
            countX = 0;
        }
    }

    // If countX is greater than
    // or equal to 3
    if (countX >= 3)
        return -1;
    else
        return 2 * (countNotX + 1) - (str.size() - countNotX);
}

// Function to find maximum count of X that
// are to be inserted into str such that no
// three consecutive characters are equal to X
static void maxNumberOfXAdded(string str, char X)
{

    int ans = maxNumberOfXAddedUtil(str, X);

    // Print the answer
    cout << (ans);
}

// Driver code
int main()
{

    // Given string
    string str = "xxyxy";

    char X = 'x';

    // Function Call
    maxNumberOfXAdded(str, X);
}

// This code is contributed by amreshkumar3.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

public class Main {

    // Utility function to find maximum count of
    // X that are to be inserted into str such that
    // no three consecutive characters are equal to X
    static int maxNumberOfXAddedUtil(String str, char X)
    {

        // Stores count of consecutive X
        int countX = 0;

        // Stores count of characters which
        // is not equal to X
        int countNotX = 0;

        // Iterate over characters of string, str
        for (int i = 0; i < str.length(); i++) {

            // If current character is X
            if (str.charAt(i) == X) {

                // Update  countX
                countX++;
            }

            // If countX is less
            // than 3
            else if (countX < 3) {

                // Update countNotX
                countNotX++;

                // Update countX
                countX = 0;
            }
        }

        // If countX is greater than
        // or equal to 3
        if (countX >= 3)
            return -1;
        else
            return 2 * (countNotX + 1)
                - (str.length() - countNotX);
    }

    // Function to find maximum count of X that
    // are to be inserted into str such that no
    // three consecutive characters are equal to X
    static void maxNumberOfXAdded(String str, char X)
    {

        int ans = maxNumberOfXAddedUtil(str, X);

        // Print the answer
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given string
        String str = "xxyxy";

        char X = X;

        // Function Call
        maxNumberOfXAdded(str, X);
    }
}
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Utility function to find maximum count of
    // X that are to be inserted into str such that
    // no three consecutive characters are equal to X
    static int maxNumberOfXAddedUtil(string str, char X)
    {

        // Stores count of consecutive X
        int countX = 0;

        // Stores count of characters which
        // is not equal to X
        int countNotX = 0;

        // Iterate over characters of string, str
        for (int i = 0; i < str.Length; i++) {

            // If current character is X
            if (str[i] == X) {

                // Update  countX
                countX++;
            }

            // If countX is less
            // than 3
            else if (countX < 3) {

                // Update countNotX
                countNotX++;

                // Update countX
                countX = 0;
            }
        }

        // If countX is greater than
        // or equal to 3
        if (countX >= 3)
            return -1;
        else
            return 2 * (countNotX + 1)
                - (str.Length - countNotX);
    }

    // Function to find maximum count of X that
    // are to be inserted into str such that no
    // three consecutive characters are equal to X
    static void maxNumberOfXAdded(string str, char X)
    {

        int ans = maxNumberOfXAddedUtil(str, X);

        // Print the answer
        Console.Write(ans);
    }

// Driver Code
public static void Main()
{
     // Given string
        string str = "xxyxy";

        char X = 'x';

        // Function Call
        maxNumberOfXAdded(str, X);
}
}

// This code is contributed by target_2.
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)