# 根据给定的字母数量最大化长度为 3 的回文串

> 原文:[https://www . geeksforgeeks . org/maximize-回文长度字符串-3-可能从给定的字母计数/](https://www.geeksforgeeks.org/maximize-palindromic-strings-of-length-3-possible-from-given-count-of-alphabets/)

给定一个大小为 **26** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，代表字符**“a”到【z】**的频率，任务是从指定的字母计数中找到长度为 **3** 的[回文字符串](https://www.geeksforgeeks.org/string-palindrome/)的最大数量。

**示例:**

> **输入:** arr[] = {4，5，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0}
> **输出:** 3
> **解释:**一种可能的解决方法是取两个‘b’字符和一个‘a’字符，组成字符串“bab”。现在，剩下 3 'a '和 3 'b '，从中可以生成字符串“aaa”和“bbb”。因此，总共可以形成 3 个回文串。
> 
> **输入:** arr[] = {2，1，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0，0}
> **输出:** 1
> **解释:**唯一可能的回文串是“aba”。

**方法:**给定的问题可以基于以下观察来解决:

1.  通过首先使可能的字符串只具有一种类型的字符，可以最大化字符串的数量。
2.  然后取一种类型的两个字符和另一种类型的一个字符，组成一个字符串。
3.  如果仍然存在出现多于 1 个的字符，那么在这些字符中取 3，形成 2 个“ACA”和“BCB”类型的字符串。
4.  如果再剩下两个出现两次的字符，那么组成一个字符串，再加一个来回答。
5.  之后，将只剩下只出现一次的字符或出现两次的字符。

按照以下步骤解决问题:

*   初始化一个变量，**用 **0** 重置**以存储可以形成的大小为 3 的最大[回文串](https://www.geeksforgeeks.org/string-palindrome/)的计数。
*   初始化一个变量，用 **0** 初始化 **C1** 和 **C2** ，分别存储频率为 1 和 2 的字符数
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)、 **arr[]** ，将 **res** 递增 **arr[i]/3** ，将 **arr[i]** 设置为 **arr[i]%3** ，如果 **arr[i]%3** 为 **1** ，则将 **C1** 递增 **1** ，否则，递增 **C2**
*   遍历后，将 **res** 增加 **min (C1、C2)** 并更新 **C1** 和 **C2** 。然后，将 **res** 增加 C2/3 的**两倍，更新 **C2** 。最后，将 **res** 增加 **C2/2** 。**
*   最后，打印 **res** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number
// of palindromic string of length 3
void maximum_pallindromic(int arr[])
{
    // Stores the final count of
    // palindromic strings
    int res = 0;
    int c1 = 0, c2 = 0;

    // Traverse the array
    for (int i = 0; i < 26; i++) {

        // Increment res by arr[i]/3,
        // i.e forming string of
        // only i +'a' character
        res += arr[i] / 3;

        // Store remainder
        arr[i] = arr[i] % 3;

        // Increment c1 by one, if
        // current frequency is 1
        if (arr[i] == 1)
            c1++;

        // Increment c2 by one, if
        // current frequency is 2
        else if (arr[i] == 2)
            c2++;
    }

    // Count palindromic strings of
    // length 3 having the character
    // at the ends different from that
    // present in the middle
    res += min(c1, c2);
    int t = min(c1, c2);

    // Update c1 and c2
    c1 -= t;
    c2 -= t;

    // Increment res by 2 * c2/3
    res += 2 * (c2 / 3);
    c2 %= 3;
    res += c2 / 2;

    // Finally print the result
    cout << res;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 4, 5, 0, 0, 0, 0, 0, 0,
                  0, 0, 0, 0, 0, 0, 0, 0, 0,
                  0, 0, 0, 0, 0, 0, 0, 0, 0 };

    // Function Call
    maximum_pallindromic(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to count maximum number
// of palindromic String of length 3
static void maximum_pallindromic(int arr[])
{

    // Stores the final count of
    // palindromic Strings
    int res = 0;
    int c1 = 0, c2 = 0;

    // Traverse the array
    for (int i = 0; i < 26; i++)
    {

        // Increment res by arr[i]/3,
        // i.e forming String of
        // only i +'a' character
        res += arr[i] / 3;

        // Store remainder
        arr[i] = arr[i] % 3;

        // Increment c1 by one, if
        // current frequency is 1
        if (arr[i] == 1)
            c1++;

        // Increment c2 by one, if
        // current frequency is 2
        else if (arr[i] == 2)
            c2++;
    }

    // Count palindromic Strings of
    // length 3 having the character
    // at the ends different from that
    // present in the middle
    res += Math.min(c1, c2);
    int t = Math.min(c1, c2);

    // Update c1 and c2
    c1 -= t;
    c2 -= t;

    // Increment res by 2 * c2/3
    res += 2 * (c2 / 3);
    c2 %= 3;
    res += c2 / 2;

    // Finally print the result
    System.out.print(res);
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 4, 5, 0, 0, 0, 0, 0, 0,
                  0, 0, 0, 0, 0, 0, 0, 0, 0,
                  0, 0, 0, 0, 0, 0, 0, 0, 0 };

    // Function Call
    maximum_pallindromic(arr);
}
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count maximum number
# of palindromic string of length 3
def maximum_pallindromic(arr):

    # Stores the final count of
    # palindromic strings
    res = 0
    c1 = 0
    c2 = 0

    # Traverse the array
    for i in range(26):

        # Increment res by arr[i]/3,
        # i.e forming string of
        # only i +'a' character
        res += arr[i] // 3

        # Store remainder
        arr[i] = arr[i] % 3

        # Increment c1 by one, if
        # current frequency is 1
        if (arr[i] == 1):
            c1 += 1

        # Increment c2 by one, if
        # current frequency is 2
        elif (arr[i] == 2):
            c2 += 1

    # Count palindromic strings of
    # length 3 having the character
    # at the ends different from that
    # present in the middle
    res += min(c1, c2)
    t = min(c1, c2)

    # Update c1 and c2
    c1 -= t
    c2 -= t

    # Increment res by 2 * c2/3
    res += 2 * (c2 // 3)
    c2 %= 3
    res += c2 // 2

    # Finally print the result
    print(res)

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [ 4, 5, 0, 0, 0, 0, 0, 0,
            0, 0, 0, 0, 0, 0, 0, 0, 0,
            0, 0, 0, 0, 0, 0, 0, 0, 0 ]

    # Function Call
    maximum_pallindromic(arr)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to count maximum number
// of palindromic String of length 3
static void maximum_pallindromic(int []arr)
{

    // Stores the readonly count of
    // palindromic Strings
    int res = 0;
    int c1 = 0, c2 = 0;

    // Traverse the array
    for (int i = 0; i < 26; i++)
    {

        // Increment res by arr[i]/3,
        // i.e forming String of
        // only i +'a' character
        res += arr[i] / 3;

        // Store remainder
        arr[i] = arr[i] % 3;

        // Increment c1 by one, if
        // current frequency is 1
        if (arr[i] == 1)
            c1++;

        // Increment c2 by one, if
        // current frequency is 2
        else if (arr[i] == 2)
            c2++;
    }

    // Count palindromic Strings of
    // length 3 having the character
    // at the ends different from that
    // present in the middle
    res += Math.Min(c1, c2);
    int t = Math.Min(c1, c2);

    // Update c1 and c2
    c1 -= t;
    c2 -= t;

    // Increment res by 2 * c2/3
    res += 2 * (c2 / 3);
    c2 %= 3;
    res += c2 / 2;

    // Finally print the result
    Console.Write(res);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 4, 5, 0, 0, 0, 0, 0, 0,
                  0, 0, 0, 0, 0, 0, 0, 0, 0,
                  0, 0, 0, 0, 0, 0, 0, 0, 0 };

    // Function Call
    maximum_pallindromic(arr);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count maximum number
// of palindromic string of length 3
function maximum_pallindromic(arr)
{
    // Stores the final count of
    // palindromic strings
    var res = 0;
    var c1 = 0, c2 = 0;

    // Traverse the array
    for (var i = 0; i < 26; i++) {

        // Increment res by arr[i]/3,
        // i.e forming string of
        // only i +'a' character
        res += parseInt(arr[i] / 3);

        // Store remainder
        arr[i] = (arr[i] % 3);

        // Increment c1 by one, if
        // current frequency is 1
        if (arr[i] == 1)
            c1++;

        // Increment c2 by one, if
        // current frequency is 2
        else if (arr[i] == 2)
            c2++;
    }

    // Count palindromic strings of
    // length 3 having the character
    // at the ends different from that
    // present in the middle
    res += Math.min(c1, c2);
    var t = Math.min(c1, c2);

    // Update c1 and c2
    c1 -= t;
    c2 -= t;

    // Increment res by 2 * c2/3
    res += 2 * parseInt(c2 / 3);
    c2 %= 3;
    res += parseInt(c2 / 2);

    // Finally print the result
    document.write( res);
}

// Driver Code
// Given array
var arr = [ 4, 5, 0, 0, 0, 0, 0, 0,
            0, 0, 0, 0, 0, 0, 0, 0, 0,
            0, 0, 0, 0, 0, 0, 0, 0, 0 ];
// Function Call
maximum_pallindromic(arr);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)