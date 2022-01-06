# 通过给定操作将 str1 转换为 str2 的最小成本

> 原文:[https://www . geeksforgeeks . org/用给定的操作将 str1 转换为 str2 的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-convert-str1-to-str2-with-the-given-operations/)

给定两个相等长度的字符串 **str1** 和 **str2** ，仅由字符 **'a'** 和 **'b'** 组成。可以在 **str1** 上进行以下操作:

1.  任何角色都可以用 **1** 单位成本从**‘a’**变成**‘b’**或者从**‘b’**变成**‘a’**。
2.  任意两个字符 **str1[i]** 和 **str1[j]** 都可以和**| I–j |**对调。

任务是找到将 **str1** 转换为 **str2** 所需的最小成本。
**例:**

> **输入:**str 1 =“abb”，str 2 =“baa”
> T3】输出: 2
> 交换(str1[0]，str1[1])，str 1 =“Bab”和成本= 1
> 将 str 1[2]=“b”改为“a”，str 1 =“baa”和成本= 2
> **输入:**str 1 =“abab”，str 2 =“AABB”
> **输出:**

**方法:**可以观察到，交换将仅在连续的字符上执行，因为如果字符不连续，则交换的成本将≥ 2，这将给出大于或等于使用第一种类型的操作改变那些字符的成本。现在，对于每两个连续的字符，如果它们在两个字符串中都不同，那么交换这些字符会产生 1 个单位成本，而当两个字符分别改变时会产生 2 个单位成本。否则更改两个字符串中不同的字符(当前或下一个)。最后，打印计算出的成本。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// cost to convert str1 to sr2
int minCost(string str1, string str2, int n)
{
    int cost = 0;

    // For every character of str1
    for (int i = 0; i < n; i++) {

        // If current character is not
        // equal in both the strings
        if (str1[i] != str2[i]) {

            // If the next character is also different in both
            // the strings then these characters can be swapped
            if (i < n - 1 && str1[i + 1] != str2[i + 1]) {
                swap(str1[i], str1[i + 1]);
                cost++;
            }

            // Change the current character
            else {
                cost++;
            }
        }
    }
    return cost;
}

// Driver code
int main()
{
    string str1 = "abb", str2 = "bba";
    int n = str1.length();

    cout << minCost(str1, str2, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum
// cost to convert str1 to sr2
static int minCost(char []str1,
                   char []str2, int n)
{
    int cost = 0;

    // For every character of str1
    for (int i = 0; i < n; i++)
    {

        // If current character is not
        // equal in both the strings
        if (str1[i] != str2[i])
        {

            // If the next character is also different in both
            // the strings then these characters can be swapped
            if (i < n - 1 && str1[i + 1] != str2[i + 1])
            {
                swap(str1, i, i + 1);
                cost++;
            }

            // Change the current character
            else
            {
                cost++;
            }
        }
    }
    return cost;
}

static void swap(char []arr, int i, int j)
{
    char temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// Driver code
public static void main(String[] args)
{
    String str1 = "abb", str2 = "bba";
    int n = str1.length();

    System.out.println(minCost(str1.toCharArray(),
                               str2.toCharArray(), n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# cost to convert str1 to sr2
def minCost(str1, str2, n):

    cost = 0

    # For every character of str1
    for i in range(n):

        # If current character is not
        # equal in both the strings
        if (str1[i] != str2[i]):

            # If the next character is also different in both
            # the strings then these characters can be swapped
            if (i < n - 1 and str1[i + 1] != str2[i + 1]):
                swap(str1[i], str1[i + 1])
                cost += 1

            # Change the current character
            else:
                cost += 1

    return cost

# Driver code
if __name__ == '__main__':

    str1 = "abb"
    str2 = "bba"
    n = len(str1)

    print(minCost(str1, str2, n))

# This code is contributed by ashutosh450
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum
    // cost to convert str1 to sr2
    static int minCost(string str1,
                       string str2, int n)
    {
        int cost = 0;

        char[] array = str1.ToCharArray();

        // For every character of str1
        for (int i = 0; i < n; i++)
        {

            // If current character is not
            // equal in both the strings
            if (str1[i] != str2[i])
            {

                // If the next character is also different in both
                // the strings then these characters can be swapped
                if (i < n - 1 && str1[i + 1] != str2[i + 1])
                {
                    char temp = array[i];
                    array[i] = array[i + 1];
                    array[i + 1] = temp ;

                    cost++;
                }

                // Change the current character
                else
                {
                    cost++;
                }
            }
        }
        return cost;
    }

    // Driver code
    static public void Main ()
    {
        string str1 = "abb", str2 = "bba";
        int n = str1.Length;

        Console.WriteLine(minCost(str1, str2, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum
    // cost to convert str1 to sr2
    function minCost(str1, str2, n)
    {
        let cost = 0;

        let array = str1.split('');

        // For every character of str1
        for (let i = 0; i < n; i++)
        {

            // If current character is not
            // equal in both the strings
            if (str1[i] != str2[i])
            {

                // If the next character is also different in both
                // the strings then these characters can be swapped
                if (i < n - 1 && str1[i + 1] != str2[i + 1])
                {
                    let temp = array[i];
                    array[i] = array[i + 1];
                    array[i + 1] = temp ;

                    cost++;
                }

                // Change the current character
                else
                {
                    cost++;
                }
            }
        }
        return cost;
    }

    let str1 = "abb", str2 = "bba";
    let n = str1.length;

    document.write(minCost(str1, str2, n));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
2
```