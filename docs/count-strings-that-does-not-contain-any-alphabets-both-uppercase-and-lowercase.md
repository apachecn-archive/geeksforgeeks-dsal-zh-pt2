# 统计不包含任何字母大小写的字符串

> 原文:[https://www . geesforgeks . org/count-strings-不包含任何字母-大写和小写/](https://www.geeksforgeeks.org/count-strings-that-does-not-contain-any-alphabets-both-uppercase-and-lowercase/)

给定一个包含 **N** 个字符串的[个字符串的数组](https://www.geeksforgeeks.org/string-data-structure/)**arr【】**，任务是计算不包含字母表中大写和小写字符的字符串的数量。

**示例:**

> **输入:**arr[]**=**{“abcdA”、“abcd”、“abcdB”、“ABC”}
> **输出:** 2
> **解释:**第一个字符串包含字母‘a’的大写和小写字符。同样，第三个字符串也包含字母“b”的大写和小写字符。因此，有效字符串的计数是 3。
> 
> **输入:**arr[]= {“XYZ”、“abc”、“NMO”}
> **输出:** 3

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，方法是迭代所有给定的字符串，并针对每个字母表检查给定的字符串是否包含其大写和小写对应项。请按照以下步骤解决此问题:

1.  创建一个变量**计数**来存储所需的计数。用 **0** 初始化。
2.  现在，遍历[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中的每个字符串，并为每个字符串[将其小写字符的频率](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)存储在一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)、 **M** 中。
3.  现在遍历该字符串，对于每个大写字母，检查其小写字母对应的频率是否大于零。如果是，则将**计数**的值增加 1。
4.  返回**计**为最终答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of strings that
// do not contain the uppercase and
// lowercase character of same alphabet
int countStrings(vector<string>& arr)
{
    // Variable to store the answer
    int count = 0;

    // Loop to iterate through
    // the array arr[]
    for (auto x : arr) {
        bool isAllowed = 1;

        // Vector to store the frequency
        // of lowercase characters
        unordered_map<char, int> M;

        // Iterator through the
        // current string
        for (auto y : x) {
            if (y - 'a' >= 0 and y - 'a' < 26) {
                M[y]++;
            }
        }

        for (auto y : x) {

            // Check if any uppercase letter
            // have its lowercase version
            if (y - 'A' >= 0 and y - 'A' < 26
                and M[tolower(y)] > 0) {
                isAllowed = 0;
                break;
            }
        }

        // If current string is not a valid
        // string, increment the count
        if (isAllowed) {
            count += 1;
        }
    }

    // Return Answer
    return count;
}

// Driver Code
int main()
{
    vector<string> arr
        = { "abcdA", "abcd", "abcdB", "abc" };
    cout << countStrings(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find count of Strings that
// do not contain the uppercase and
// lowercase character of same alphabet
static int countStrings(String[]arr)
{

    // Variable to store the answer
    int count = 0;

    // Loop to iterate through
    // the array arr[]
    for (String x : arr) {
        boolean isAllowed = true;

        // Vector to store the frequency
        // of lowercase characters
        HashMap<Character,Integer> M = new HashMap<Character,Integer>();

        // Iterator through the
        // current String
        for (char y : x.toCharArray()) {
            if (y - 'a' >= 0 && y - 'a' < 26) {
                 if(M.containsKey(y)){
                        M.put(y, M.get(y)+1);
                    }
                    else{
                        M.put(y, 1);
                    }
            }
        }

        for (char y : x.toCharArray()) {

            // Check if any uppercase letter
            // have its lowercase version
            if (y - 'A' >= 0 && y - 'A' < 26 && M.containsKey(Character.toLowerCase(y))
                && M.get(Character.toLowerCase(y)) > 0) {
                isAllowed = false;
                break;
            }
        }

        // If current String is not a valid
        // String, increment the count
        if (isAllowed) {
            count += 1;
        }
    }

    // Return Answer
    return count;
}

// Driver Code
public static void main(String[] args)
{
    String []arr
        = { "abcdA", "abcd", "abcdB", "abc" };
    System.out.print(countStrings(arr));
}
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find count of strings that
# do not contain the uppercase and
# lowercase character of same alphabet
def countStrings(arr):
    # Variable to store the answer
    count = 0

    # Loop to iterate through
    # the array arr[]
    for x in arr:
        isAllowed = 1

        # Vector to store the frequency
        # of lowercase characters
        M = {}

        # Iterator through the
        # current string
        for y in x:
            if (ord(y) - ord('a') >= 0 and ord(y) - ord('a') < 26):
                if(y in M):
                    M[y] += 1
                else:
                    M[y] = 1

        for y in x:

            # Check if any uppercase letter
            # have its lowercase version
            if (ord(y) - ord('A') >= 0 and ord(y) - ord('A') < 26 and M[y.lower()] > 0):
                isAllowed = 0
                break

        # If current string is not a valid
        # string, increment the count
        if (isAllowed):
            count += 1

    # Return Answer
    return count

# Driver Code

arr = ["abcdA", "abcd", "abcdB", "abc"]
print(countStrings(arr))

# This code is contributed by gfgking.
```

## C#

```
// C# code for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to find count of strings that
// do not contain the uppercase and
// lowercase character of same alphabet
static int countStrings(ArrayList arr)
{

    // Variable to store the answer
    int count = 0;

    // Loop to iterate through
    // the array arr[]
    foreach (string x in arr) {
        bool isAllowed = true;

        // To store the frequency
        // of lowercase characters
        Dictionary<char, int> M =
          new Dictionary<char, int>();

        // Iterator through the
        // current string
        foreach (char y in x) {
            if (y - 'a' >= 0 && y - 'a' < 26) {
              if (M.ContainsKey(y))
                {
                    M[y] = M[y] + 1;
                }
                else
                {
                    M.Add(y, 1);
                }
            }
        }

        foreach (char y in x) {

            // Check if any uppercase letter
            // have its lowercase version
            if (y - 'A' >= 0  && y - 'A' < 26
                && M[Char.ToLower(y)] > 0) {
                isAllowed = false;
                break;
            }
        }

        // If current string is not a valid
        // string, increment the count
        if (isAllowed) {
            count += 1;
        }
    }

    // Return Answer
    return count;
}

// Driver Code
public static void Main()
{
    ArrayList arr = new ArrayList();

    arr.Add("abcdA");
    arr.Add("abcd");
    arr.Add("abcdB");
    arr.Add("abc");

    Console.Write(countStrings(arr));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

     // JavaScript Program to implement
     // the above approach

     // Function to find count of strings that
     // do not contain the uppercase and
     // lowercase character of same alphabet
     function countStrings(arr)
     {

         // Variable to store the answer
         let count = 0;

         // Loop to iterate through
         // the array arr[]
         for (let x of arr)
         {
             let isAllowed = 1;

             // Vector to store the frequency
             // of lowercase characters
             let M = new Map();

             // Iterator through the
             // current string
             for (let i = 0; i < x.length; i++) {
                 y = x[i];
                 if (y.charCodeAt(0) - 'a'.charCodeAt(0) >= 0 && y.charCodeAt(0) - 'a'.charCodeAt(0) < 26) {
                     if (M.has(y)) {
                         M.set(y, M.get(y) + 1);
                     }
                     else {
                         M.set(y, 1);
                     }
                 }
             }

             for (i = 0; i < x.length; i++)
             {
                 y = x[i];

                 // Check if any uppercase letter
                 // have its lowercase version
                 if (y.charCodeAt(0) - 'A'.charCodeAt(0) >= 0 && y.charCodeAt(0) - 'A'.charCodeAt(0) < 26
                     && M.get(y.toLowerCase()) > 0) {
                     isAllowed = 0;
                     break;
                 }
             }

             // If current string is not a valid
             // string, increment the count
             if (isAllowed) {
                 count += 1;
             }
         }

         // Return Answer
         return count;
     }

     // Driver Code
     let arr
         = ["abcdA", "abcd", "abcdB", "abc"];
     document.write(countStrings(arr));

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
2
```

***时间复杂度:** O(N * M)，其中 M 为最长字符串的长度*
***辅助空间:** O(1)*