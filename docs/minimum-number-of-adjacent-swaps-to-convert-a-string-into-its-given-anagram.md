# 将字符串转换为其给定字谜的最小相邻互换次数

> 原文:[https://www . geeksforgeeks . org/将字符串转换为给定字谜的最小相邻互换次数/](https://www.geeksforgeeks.org/minimum-number-of-adjacent-swaps-to-convert-a-string-into-its-given-anagram/)

给定两个字符串 **s1** 和 **s2** ，任务是找到将 **s1** 转换为 **s2** 所需的最小步数。唯一允许的操作是交换第一个字符串中的相邻元素。每次交换都被视为一个步骤。
**举例:**

> **输入:**S1 =“ABCD”，S2 =“cdab”
> T3】输出: 4
> 交换 2 <sup>nd</sup> 和 3 <sup>rd</sup> 元素，abcd = > acbd
> 交换 1 <sup>st</sup> 和 2 <sup>nd</sup> 元素，acbd = > cabd
> 交换 3 <sup>rd</sup> 和 4 <sup>th
> **输入:**S1 =“abcdefdeggi”，S2 =“fjicbedge”
> **输出:** 17</sup>

**方法:**使用两个指针 **i** 和 **j** 分别表示第一和第二根弦。初始化 **i** 和 **j** 至 **0** 。
迭代第一个字符串，找到 **j** 的位置，使 **s1[j] = s2[i]** 通过将值增加到 **j** 来实现。继续交换相邻元素 **j** 和**j–1**并减少 **j** 直到其大于 **i** 。
现在第一个字符串的 **i <sup>第</sup>** 元素等于第二个字符串，因此增加 **i** 的值。
该技术将给出最少的步骤数，因为没有不必要的交换。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if s1
// and s2 are anagrams of each other
bool isAnagram(string s1, string s2)
{
    sort(s1.begin(), s1.end());
    sort(s2.begin(), s2.end());
    if (s1 == s2)
        return 1;
    return 0;
}

// Function to return the minimum swaps required
int CountSteps(string s1, string s2, int size)
{
    int i = 0, j = 0;
    int result = 0;

    // Iterate over the first string and convert
    // every element equal to the second string
    while (i < size) {
        j = i;

        // Find index element of first string which
        // is equal to the ith element of second string
        while (s1[j] != s2[i]) {
            j += 1;
        }

        // Swap adjacent elements in first string so
        // that element at ith position becomes equal
        while (i < j) {

            // Swap elements using temporary variable
            char temp = s1[j];
            s1[j] = s1[j - 1];
            s1[j - 1] = temp;
            j -= 1;
            result += 1;
        }
        i += 1;
    }
    return result;
}

// Driver code
int main()
{
    string s1 = "abcd";
    string s2 = "cdab";

    int size = s2.size();

    // If both the strings are anagrams
    // of each other then only they
    // can be made equal
    if (isAnagram(s1, s2))
        cout << CountSteps(s1, s2, size);
    else
        cout << -1;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function that returns true if s1
// and s2 are anagrams of each other
static boolean isAnagram(String s1, String s2)
{
    s1 = sortString(s1);
    s2 = sortString(s2);
    return (s1.equals(s2));
}

// Method to sort a string alphabetically
public static String sortString(String inputString)
{
    // convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // return new sorted string
    return new String(tempArray);
}

// Function to return the minimum swaps required
static int CountSteps(char []s1, char[] s2, int size)
{
    int i = 0, j = 0;
    int result = 0;

    // Iterate over the first string and convert
    // every element equal to the second string
    while (i < size)
    {
        j = i;

        // Find index element of first string which
        // is equal to the ith element of second string
        while (s1[j] != s2[i])
        {
            j += 1;
        }

        // Swap adjacent elements in first string so
        // that element at ith position becomes equal
        while (i < j)
        {

            // Swap elements using temporary variable
            char temp = s1[j];
            s1[j] = s1[j - 1];
            s1[j - 1] = temp;
            j -= 1;
            result += 1;
        }
        i += 1;
    }
    return result;
}

// Driver code
public static void main(String[] args)
{
    String s1 = "abcd";
    String s2 = "cdab";

    int size = s2.length();

    // If both the strings are anagrams
    // of each other then only they
    // can be made equal
    if (isAnagram(s1, s2))
        System.out.println(CountSteps(s1.toCharArray(), s2.toCharArray(), size));
    else
        System.out.println(-1);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that returns true if s1
# and s2 are anagrams of each other
def isAnagram(s1, s2) :
    s1 = list(s1);
    s2 = list(s2);
    s1 = s1.sort();
    s2 = s2.sort();

    if (s1 == s2) :
        return 1;

    return 0;

# Function to return the minimum swaps required
def CountSteps(s1, s2, size) :
    s1 = list(s1);
    s2 = list(s2);

    i = 0;
    j = 0;
    result = 0;

    # Iterate over the first string and convert
    # every element equal to the second string
    while (i < size) :
        j = i;

        # Find index element of first string which
        # is equal to the ith element of second string
        while (s1[j] != s2[i]) :
            j += 1;

        # Swap adjacent elements in first string so
        # that element at ith position becomes equal
        while (i < j) :

            # Swap elements using temporary variable
            temp = s1[j];
            s1[j] = s1[j - 1];
            s1[j - 1] = temp;
            j -= 1;
            result += 1;

        i += 1;

    return result;

# Driver code
if __name__ == "__main__":

    s1 = "abcd";
    s2 = "cdab";

    size = len(s2);

    # If both the strings are anagrams
    # of each other then only they
    # can be made equal
    if (isAnagram(s1, s2)) :
        print(CountSteps(s1, s2, size));
    else :
        print(-1);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;
using System.Linq;

class GFG
{

// Function that returns true if s1
// and s2 are anagrams of each other
static Boolean isAnagram(String s1, String s2)
{
    s1 = sortString(s1);
    s2 = sortString(s2);
    return (s1.Equals(s2));
}

// Method to sort a string alphabetically
public static String sortString(String inputString)
{
    // convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // sort tempArray
    Array.Sort(tempArray);

    // return new sorted string
    return new String(tempArray);
}

// Function to return the minimum swaps required
static int CountSteps(char []s1, char[] s2, int size)
{
    int i = 0, j = 0;
    int result = 0;

    // Iterate over the first string and convert
    // every element equal to the second string
    while (i < size)
    {
        j = i;

        // Find index element of first string which
        // is equal to the ith element of second string
        while (s1[j] != s2[i])
        {
            j += 1;
        }

        // Swap adjacent elements in first string so
        // that element at ith position becomes equal
        while (i < j)
        {

            // Swap elements using temporary variable
            char temp = s1[j];
            s1[j] = s1[j - 1];
            s1[j - 1] = temp;
            j -= 1;
            result += 1;
        }
        i += 1;
    }
    return result;
}

// Driver code
public static void Main(String[] args)
{
    String s1 = "abcd";
    String s2 = "cdab";

    int size = s2.Length;

    // If both the strings are anagrams
    // of each other then only they
    // can be made equal
    if (isAnagram(s1, s2))
        Console.WriteLine(CountSteps(s1.ToCharArray(), s2.ToCharArray(), size));
    else
        Console.WriteLine(-1);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function that returns true if s1
    // and s2 are anagrams of each other
    function isAnagram(s1, s2)
    {
        s1 = sortString(s1);
        s2 = sortString(s2);
        return (s1 == s2);
    }

    // Method to sort a string alphabetically
    function sortString(inputString)
    {
        // convert input string to char array
        let tempArray = inputString.split('');

        // sort tempArray
        tempArray.sort();

        // return new sorted string
        return tempArray.join("");
    }

    // Function to return the minimum swaps required
    function CountSteps(s1, s2, size)
    {
        let i = 0, j = 0;
        let result = 0;

        // Iterate over the first string and convert
        // every element equal to the second string
        while (i < size)
        {
            j = i;

            // Find index element of first string which
            // is equal to the ith element of second string
            while (s1[j] != s2[i])
            {
                j += 1;
            }

            // Swap adjacent elements in first string so
            // that element at ith position becomes equal
            while (i < j)
            {

                // Swap elements using temporary variable
                let temp = s1[j];
                s1[j] = s1[j - 1];
                s1[j - 1] = temp;
                j -= 1;
                result += 1;
            }
            i += 1;
        }
        return result;
    }

    let s1 = "abcd";
    let s2 = "cdab";

    let size = s2.length;

    // If both the strings are anagrams
    // of each other then only they
    // can be made equal
    if (isAnagram(s1, s2))
        document.write(CountSteps(s1.split(''), s2.split(''), size) + "</br>");
    else
        document.write(-1 + "</br>");

</script>
```

**Output:** 

```
4
```