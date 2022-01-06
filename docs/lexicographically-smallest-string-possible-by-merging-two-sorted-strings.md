# 通过合并两个已排序的字符串，字典上最小的字符串

> 原文:[https://www . geesforgeks . org/按字典顺序排列-通过合并可能的最小字符串-两个排序的字符串/](https://www.geeksforgeeks.org/lexicographically-smallest-string-possible-by-merging-two-sorted-strings/)

给定两个长度分别为 **N** 和 **M** 的[排序字符串](https://www.geeksforgeeks.org/sort-string-characters/)**【S1】**和 **S2** ，任务是通过合并两个给定字符串并不改变字符的出现顺序来构建字典上可能的最小字符串。

**示例:**

> **输入:**S1 =“eefgkors”，S2 =“eegks”
> T3】输出:“eegefggkkors”
> **解释:**
> 字符串“eegefggkkors”是在给定的两个字符串 S1 和 S2 合并后，按字典顺序可以形成的最小字符串。
> 
> **输入:**S1 =“aabcdtx”，S2 =“achillp”
> 输出:“aabccdhilptx”

**天真方法:**最简单的方法是[连接给定的两个字符串](https://www.geeksforgeeks.org/c-program-to-concatenate-two-strings-without-using-strcat/)和[对结果字符串](https://www.geeksforgeeks.org/sort-string-characters/)进行排序，以获得字典上最小的字符串。

***时间复杂度:**O(N+M)* log(N+M)*
T5**辅助空间:** O(N + M)

**高效方法:**通过比较给定字符串的字符，使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)可以优化上述方法，然后相应地构建所需的字符串。
按照以下步骤解决问题:

*   初始化两个指针，说 **ptr1** 和 **ptr2** ，分别指向两个字符串 **S1** 和 **S2** 的开头。
*   初始化一个字符串**和** **= " "，**来存储结果字典上最小的字符串。
*   迭代至 **ptr1** 小于**N****ptr 2**小于 **M** ，执行以下步骤:
    *   如果**S1【ptr 1】**小于**S2【ptr 2】**，则在字符串**和**后附加字符**S1【ptr 1】**。递增 **ptr1** 。
    *   否则，将字符**S2【ptr 2】**附加到字符串**和**中。增量 **ptr2** 。
*   完成上述步骤后，其中一个指针没有到达字符串的末尾。
*   因此，将字符串的所有剩余字符添加到字符串**和**的末尾。
*   打印**和**作为结果字符串。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find lexicographically
// smallest string possible by merging
// two sorted strings
void mergeStrings(string s1, string s2)
{
    // Stores length of string s1
    int len1 = s1.size();

    // Stores length of string s2
    int len2 = s2.size();

    // Pointer to beginning
    // of string1 i.e., s1
    int pntr1 = 0;

    // Pointer to beginning
    // of string2 i.e., s2
    int pntr2 = 0;

    // Stores the final string
    string ans = "";

    // Traverse the strings
    while (pntr1 < len1 && pntr2 < len2) {

        // Append the smaller of the
        // two current characters
        if (s1[pntr1] < s2[pntr2]) {
            ans += s1[pntr1];
            pntr1++;
        }

        else {
            ans += s2[pntr2];
            pntr2++;
        }
    }

    // Append the remaining characters
    // of any of the two strings
    if (pntr1 < len1) {
        ans += s1.substr(pntr1, len1);
    }
    if (pntr2 < len2) {
        ans += s2.substr(pntr2, len2);
    }

    // Print the final string
    cout << ans;
}

// Driver Code
int main()
{
    string S1 = "abdcdtx";
    string S2 = "achilp";

    // Function Call
    mergeStrings(S1, S2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find lexicographically
// smallest string possible by merging
// two sorted strings
static void mergeStrings(String s1, String s2)
{

    // Stores length of string s1
    int len1 = s1.length();

    // Stores length of string s2
    int len2 = s2.length();

    // Pointer to beginning
    // of string1 i.e., s1
    int pntr1 = 0;

    // Pointer to beginning
    // of string2 i.e., s2
    int pntr2 = 0;

    // Stores the final string
    String ans = "";

    // Traverse the strings
    while (pntr1 < len1 && pntr2 < len2)
    {

        // Append the smaller of the
        // two current characters
        if (s1.charAt(pntr1) < s2.charAt(pntr2))
        {
            ans += s1.charAt(pntr1);
            pntr1++;
        }

        else
        {
            ans += s2.charAt(pntr2);
            pntr2++;
        }
    }

    // Append the remaining characters
    // of any of the two strings
    if (pntr1 < len1)
    {
        ans += s1.substring(pntr1, len1);
    }
    if (pntr2 < len2)
    {
        ans += s2.substring(pntr2, len2);
    }

    // Print the final string
    System.out.println(ans);
}

// Driver Code
public static void main (String[] args)
{
    String S1 = "abdcdtx";
    String S2 = "achilp";

    // Function Call
    mergeStrings(S1, S2);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find lexicographically
# smallest possible by merging
# two sorted strings
def mergeStrings(s1, s2):

    # Stores length of s1
    len1 = len(s1)

    # Stores length of s2
    len2 = len(s2)

    # Pointer to beginning
    # of string1 i.e., s1
    pntr1 = 0

    # Pointer to beginning
    # of string2 i.e., s2
    pntr2 = 0

    # Stores the final string
    ans = ""

    # Traverse the strings
    while (pntr1 < len1 and pntr2 < len2):

        # Append the smaller of the
        # two current characters
        if (s1[pntr1] < s2[pntr2]):
            ans += s1[pntr1]
            pntr1 += 1
        else:
            ans += s2[pntr2]
            pntr2 += 1

    # Append the remaining characters
    # of any of the two strings
    if (pntr1 < len1):
        ans += s1[pntr1:pntr1 + len1]

    if (pntr2 < len2):
        ans += s2[pntr2:pntr2 + len2]

    # Print the final string
    print (ans)

# Driver Code
if __name__ == '__main__':
    S1 = "abdcdtx"
    S2 = "achilp"

    # Function Call
    mergeStrings(S1, S2)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find lexicographically
  // smallest string possible by merging
  // two sorted strings
  static void mergeStrings(string s1, string s2)
  {

    // Stores length of string s1
    int len1 = s1.Length;

    // Stores length of string s2
    int len2 = s2.Length;

    // Pointer to beginning
    // of string1 i.e., s1
    int pntr1 = 0;

    // Pointer to beginning
    // of string2 i.e., s2
    int pntr2 = 0;

    // Stores the final string
    string ans = "";

    // Traverse the strings
    while (pntr1 < len1 && pntr2 < len2) {

      // Append the smaller of the
      // two current characters
      if (s1[pntr1] < s2[pntr2]) {
        ans += s1[pntr1];
        pntr1++;
      }

      else {
        ans += s2[pntr2];
        pntr2++;
      }
    }

    // Append the remaining characters
    // of any of the two strings
    if (pntr1 < len1) {
      ans += s1.Substring(pntr1, len1 - pntr1);
    }
    if (pntr2 < len2) {
      ans += s2.Substring(pntr2, len2 - pntr2);
    }

    // Print the final string
    Console.WriteLine(ans);
  }

  // Driver Code
  public static void Main()
  {
    string S1 = "abdcdtx";
    string S2 = "achilp";

    // Function Call
    mergeStrings(S1, S2);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find lexicographically
// smallest string possible by merging
// two sorted strings
function mergeStrings( s1,  s2)
{
    // Stores length of string s1
    var len1 = s1.length;

    // Stores length of string s2
    var len2 = s2.length;

    // Pointer to beginning
    // of string1 i.e., s1
    var pntr1 = 0;

    // Pointer to beginning
    // of string2 i.e., s2
    var pntr2 = 0;

    // Stores the final string
    var ans = "";

    // Traverse the strings
    while (pntr1 < len1 && pntr2 < len2) {

        // Append the smaller of the
        // two current characters
        if (s1[pntr1] < s2[pntr2]) {
            ans += s1[pntr1];
            pntr1++;
        }

        else {
            ans += s2[pntr2];
            pntr2++;
        }
    }

    // Append the remaining characters
    // of any of the two strings
    if (pntr1 < len1) {
        ans += s1.substr(pntr1, len1);
    }
    if (pntr2 < len2) {
        ans += s2.substr(pntr2, len2);
    }

    // Print the final string
    document.write( ans);
}

// Driver Code
var S1 = "abdcdtx";
var S2 = "achilp";
// Function Call
mergeStrings(S1, S2);

</script>
```

**Output:** 

```
aabcdcdhilptx
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N + M)*