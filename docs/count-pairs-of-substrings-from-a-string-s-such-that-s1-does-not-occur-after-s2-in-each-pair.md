# 对字符串 S 中的子字符串对进行计数，使得 S1 不会出现在每对子字符串中的 S2 之后

> 原文:[https://www . geeksforgeeks . org/count-成对子串-from-string-s-so-S1-not-after-after-S2-in-per-pair/](https://www.geeksforgeeks.org/count-pairs-of-substrings-from-a-string-s-such-that-s1-does-not-occur-after-s2-in-each-pair/)

给定三个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**、 **str1** 和 **str2** ，任务是将 **str1** 和 **str2** 作为字符串 **str** 中的一个子字符串进行计数，使得在每一对中 **str1** 的起始索引小于或等于 **str2** 。

**示例:**

> **输入:** str = "geeksforgeeksfor "，str1 = "geeks "，str2 = "for"
> **输出:** 3
> **解释:**
> str1 的起始索引为{ 0，8 }
> str2 的起始索引为{ 5，13 }
> 可能的对使得 str 1 小于或等于 str 2 的起始索引为{ (0，5)，(0，13)，(8，13) }
> 因此
> 
> **输入:** str = "geeksforgeeks "，str1 = "geek "，str2 = "for"
> **输出:** 1

**方法:**思路是在字符串 **str** 中找到[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **str2** 的起始索引，在字符串**的每个起始索引处，str2** 按 **str1** 的起始索引计数递增对的计数，直到**I<sup>th</sup>T15**的索引。最后，打印获得的配对总数。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntPairs** ，存储 **str1** 和 **str2** 的对的计数，使得 **str1** 的起始索引小于或等于 **str2** 。
*   初始化一个变量，比如说 **cntStr1** ，存储起始索引小于等于 **i** 的[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)、 **str1** 在**串**中的计数。
*   迭代范围**【0，N-1】**。对于字符串 **str** 的每一个**I<sup>th</sup>T5】索引，检查起始索引等于 **i** 的字符串 **str** 中是否存在子字符串 **str1** 。如果发现为真，则将 **cntStr1** 的值增加 **1** 。**
*   对于每个 **i <sup>第</sup>T3】个索引，检查在起始索引等于 **i** 的字符串中是否存在[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/) **str2** 。如果发现为真，则将 **cntPairs** 的值增加 **cntStr1** 。**
*   最后，打印 **cntPairs** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of pairs of str1
// and str2 in str such that starting index of
// str1 less than or equal to str2
int CountSubstring(string str, string str1, string str2)
{

    // Stores count of pairs of str1 and str2
    // such that the start index of str1 is
    // less than or equal to str2
    int cntPairs = 0;

    // Stores count of substring str1 in
    // str whose start index is up to i
    int cntStr1 = 0;

    // Iterate over the range [0, N -1]
    for (int i = 0; i < str.length(); i++) {

        // If substring str1 whose
        // start index is i
        if (str.substr(i, str1.length())
            == str1) {

            // Update cntStr1
            cntStr1++;
        }

        // If substring str2 whose
        // start index is i
        else if (str.substr(i, str2.length())
                 == str2) {

            // Update cntPairs
            cntPairs += cntStr1;
        }
    }

    return cntPairs;
}

// Driver Code
int main()
{

    string str = "geeksforgeeksfor";
    string str1 = "geeks", str2 = "for";

    cout << CountSubstring(str, str1, str2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
public class GFG {

    // Driver Code
    public static void main(String[] args)
    {
        String str = new String("geeksforgeeksfor");
        String str1 = new String("geeks");
        String str2 = new String("for");

        System.out.println(CountSubstring(
            str, str1, str2));
    }

    // Function to find the count of pairs of str1
    // and str2 in str such that starting index of
    // str1 less than or equal to str2
    static int CountSubstring(String str,
                              String str1,
                              String str2)
    {

        // Stores count of pairs of str1 and str2
        // such that the start index of str1 is
        // less than or equal to str2
        int cntPairs = 0;

        // Stores count of substring str1 in
        // str whose start index is up to i
        int cntStr1 = 0;

        // Stores length of str
        int N = str.length();

        // Stores length of str1
        int s1 = str1.length();

        // Stores length of str2
        int s2 = str2.length();

        // Iterate over the range [0, N -1]
        for (int i = 0; i < N; i++) {

            // If substring str1 whose
            // starting index is i
            if (((i + s1) <= N)
                && (str.substring(
                        i, (i + s1)))
                           .compareTo(str1)
                       == 0) {

                // Update cntStr1
                cntStr1++;
            }

            // If substring str2 whose
            // starting index is i
            else if (((i + s2) <= N)
                     && (str.substring(
                             i, (i + s2)))
                                .compareTo(str2)
                            == 0) {

                // Update cntPairs
                cntPairs += cntStr1;
            }
        }

        return cntPairs;
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the count of pairs of str1
# and str2 in str such that starting index of
# str1 less than or equal to str2
def CountSubstring(str, str1, str2):

    # Stores count of pairs of str1 and str2
    # such that the start index of str1 is
    # less than or equal to str2
    cntStr1 = 0

    # Stores count of substring str1 in
    # str whose start index is up to i
    cntPairs = 0

    # Iterate over the range [0, N -1]
    for i in range(len(str)):

        # If substring str1 whose
        # start index is i
        if str[i : i + len(str1)] == str1:

            # Update cntStr1
            cntStr1 += 1

        # If substring str2 whose
        # start index is i   
        elif str[i : i + len(str2)] == str2:

            # Update cntPairs
            cntPairs += cntStr1

    return cntPairs

# Driver Code
str = 'geeksforgeeksfor'
str1 = 'geeks'
str2 = 'for'       

print(CountSubstring(str, str1, str2))       

# This code is contributed by dharanendralv23
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the count of pairs of str1
// and str2 in str such that starting index of
// str1 less than or equal to str2 
static int CountSubstring(String str,
                          String str1,
                          String str2)
{

    // Stores count of pairs of str1 and str2
    // such that the start index of str1 is
    // less than or equal to str2
    int cntPairs = 0;

    // Stores count of substring str1 in
    // str whose start index is up to i
    int cntStr1 = 0;

    // Stores length of str
    int N = str.Length;

    // Stores length of str1
    int s1 = str1.Length;

    // Stores length of str2
    int s2 = str2.Length;

    // Iterate over the range [0, N -1]
    for(int i = 0; i < N; i++)
    {

        // If substring str1 whose
        // starting index is i
        if (((i + s1) <= N) &&
            (str.Substring(i, s1)).Equals(str1))
        {

            // Update cntStr1
            cntStr1++;
        }

        // If substring str2 whose
        // starting index is i
        else if (((i + s2) <= N) &&
                 (str.Substring(i, s2)).Equals(str2))
        {

            // Update cntPairs
            cntPairs += cntStr1;
        }
    }
    return cntPairs;
}

// Driver code
static public void Main()
{
    String str = "geeksforgeeksfor";        
    String str1 = "geeks";   
    String str2 = "for";

    Console.Write(CountSubstring(str, str1, str2));        
}
}

// This code is contributed by dharanendralv23
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to find the count of pairs of str1
// and str2 in str such that starting index of
// str1 less than or equal to str2
function CountSubstring(str, str1, str2)
{

    // Stores count of pairs of str1 and str2
    // such that the start index of str1 is
    // less than or equal to str2
    var cntPairs = 0;

    // Stores count of substring str1 in
    // str whose start index is up to i
    var cntStr1 = 0;

    // Iterate over the range [0, N -1]
    for (let i = 0; i < str.length; i++) {

        // If substring str1 whose
        // start index is i
        if (str.substr(i, str1.length)
            == str1) {

            // Update cntStr1
            cntStr1++;
        }

        // If substring str2 whose
        // start index is i
        else if (str.substr(i, str2.length)
                 == str2) {

            // Update cntPairs
            cntPairs += cntStr1;
        }
    }

    return cntPairs;
}

// Driver Code

var str = "geeksforgeeksfor";
var str1 = "geeks", str2 = "for";

console.log( CountSubstring(str, str1, str2));

// This code is contributed by ukasp. 
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(| str | *(| str 1 |+| str 2 |)*
***辅助空间:** O(1)*