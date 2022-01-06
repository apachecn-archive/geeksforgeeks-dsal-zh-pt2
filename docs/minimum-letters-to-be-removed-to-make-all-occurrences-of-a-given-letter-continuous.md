# 为使给定字母的所有出现连续，需要删除的最小字母数

> 原文:[https://www . geesforgeks . org/最少要删除的字母-使给定字母的所有出现次数连续/](https://www.geeksforgeeks.org/minimum-letters-to-be-removed-to-make-all-occurrences-of-a-given-letter-continuous/)

给定一个字符串 **str** 和一个字符 **K** ，任务是找到应该从该序列中移除的元素的最小数量，以便给定字符 **K** 的所有出现都成为连续的。

**示例:**

> **输入:** str = "ababababa "，K = 'a'
> **输出:** 4
> **解释:**
> 字符' b '的所有出现都应该被移除，以便使' a '的出现连续。
> 
> **输入:** str = "kprkkoinkopt "，K = ' K '
> T3】输出: 5

**方法:**想法是在给定字符 K 的第一次和最后一次出现之间找到除 **K** 以外的字符数。为了做到这一点，遵循以下步骤:

1.  找到第一个出现的字符 **K** 。
2.  查找字符 **K** 的最后一次出现。
3.  在索引之间迭代，找出除 k 之外的索引之间的字符数。这是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// deletions required to make the occurrences
// of the given character K continuous
int noOfDeletions(string str, char k)
{
    int ans = 0, cnt = 0, pos = 0;

    // Find the first occurrence of the given letter
    while (pos < str.length() && str[pos] != k) {
        pos++;
    }

    int i = pos;

    // Iterate from the first occurrence
    // till the end of the sequence
    while (i < str.length()) {

        // Find the index from where the occurrence
        // of the character is not continuous
        while (i < str.length() && str[i] == k) {
            i = i + 1;
        }

        // Update the answer with the number of
        // elements between non-consecutive occurrences
        // of the given letter
        ans = ans + cnt;
        cnt = 0;
        while (i < str.length() && str[i] != k) {
            i = i + 1;

            // Update the count for all letters
            // which are not equal to the given letter
            cnt = cnt + 1;
        }
    }

    // Return the count
    return ans;
}

// Driver code
int main()
{
    string str1 = "ababababa";
    char k1 = 'a';
    // Calling the function
    cout << noOfDeletions(str1, k1) << endl;

    string str2 = "kprkkoinkopt";
    char k2 = 'k';
    // Calling the function
    cout << noOfDeletions(str2, k2) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to find the minimum number of
// deletions required to make the occurrences
// of the given character K continuous
static int noOfDeletions(String str, char k)
{
    int ans = 0, cnt = 0, pos = 0;

    // Find the first occurrence of the given letter
    while (pos < str.length() && str.charAt(pos) != k) {
        pos++;
    }

    int i = pos;

    // Iterate from the first occurrence
    // till the end of the sequence
    while (i < str.length()) {

        // Find the index from where the occurrence
        // of the character is not continuous
        while (i < str.length() && str.charAt(i) == k) {
            i = i + 1;
        }

        // Update the answer with the number of
        // elements between non-consecutive occurrences
        // of the given letter
        ans = ans + cnt;
        cnt = 0;
        while (i < str.length() && str.charAt(i) != k) {
            i = i + 1;

            // Update the count for all letters
            // which are not equal to the given letter
            cnt = cnt + 1;
        }
    }

    // Return the count
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String str1 = "ababababa";
    char k1 = 'a';

    // Calling the function
    System.out.print(noOfDeletions(str1, k1) +"\n");

    String str2 = "kprkkoinkopt";
    char k2 = 'k';

    // Calling the function
    System.out.print(noOfDeletions(str2, k2) +"\n");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the minimum number of
# deletions required to make the occurrences
# of the given character K continuous
def noOfDeletions(string, k) :

    ans = 0; cnt = 0; pos = 0;

    # Find the first occurrence of the given letter
    while (pos < len(string) and string[pos] != k) :
        pos += 1;

    i = pos;

    # Iterate from the first occurrence
    # till the end of the sequence
    while (i < len(string)) :

        # Find the index from where the occurrence
        # of the character is not continuous
        while (i < len(string) and string[i] == k) :
            i = i + 1;

        # Update the answer with the number of
        # elements between non-consecutive occurrences
        # of the given letter
        ans = ans + cnt;
        cnt = 0;
        while (i < len(string) and string[i] != k) :
            i = i + 1;

            # Update the count for all letters
            # which are not equal to the given letter
            cnt = cnt + 1;

    # Return the count
    return ans;

# Driver code
if __name__ == "__main__" :

    str1 = "ababababa";
    k1 = 'a';

    # Calling the function
    print(noOfDeletions(str1, k1));

    str2 = "kprkkoinkopt";
    k2 = 'k';

    # Calling the function
    print(noOfDeletions(str2, k2));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to find the minimum number of
// deletions required to make the occurrences
// of the given character K continuous
static int noOfDeletions(String str, char k)
{
    int ans = 0, cnt = 0, pos = 0;

    // Find the first occurrence of the given letter
    while (pos < str.Length && str[pos] != k) {
        pos++;
    }

    int i = pos;

    // Iterate from the first occurrence
    // till the end of the sequence
    while (i < str.Length) {

        // Find the index from where the occurrence
        // of the character is not continuous
        while (i < str.Length && str[i] == k) {
            i = i + 1;
        }

        // Update the answer with the number of
        // elements between non-consecutive occurrences
        // of the given letter
        ans = ans + cnt;
        cnt = 0;
        while (i < str.Length && str[i] != k) {
            i = i + 1;

            // Update the count for all letters
            // which are not equal to the given letter
            cnt = cnt + 1;
        }
    }

    // Return the count
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    String str1 = "ababababa";
    char k1 = 'a';

    // Calling the function
    Console.Write(noOfDeletions(str1, k1) +"\n");

    String str2 = "kprkkoinkopt";
    char k2 = 'k';

    // Calling the function
    Console.Write(noOfDeletions(str2, k2) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the minimum number of
// deletions required to make the occurrences
// of the given character K continuous
function noOfDeletions(str, k)
{
    var ans = 0, cnt = 0, pos = 0;

    // Find the first occurrence of the given letter
    while (pos < str.length && str[pos] != k)
    {
        pos++;
    }

    var i = pos;

    // Iterate from the first occurrence
    // till the end of the sequence
    while (i < str.length)
    {

        // Find the index from where the occurrence
        // of the character is not continuous
        while (i < str.length && str[i] == k)
        {
            i = i + 1;
        }

        // Update the answer with the number of
        // elements between non-consecutive occurrences
        // of the given letter
        ans = ans + cnt;
        cnt = 0;
        while (i < str.length && str[i] != k)
        {
            i = i + 1;

            // Update the count for all letters
            // which are not equal to the given letter
            cnt = cnt + 1;
        }
    }

    // Return the count
    return ans;
}

// Driver code
var str1 = "ababababa";
var k1 = 'a';

// Calling the function
document.write( noOfDeletions(str1, k1) + "<br>");
var str2 = "kprkkoinkopt";
var k2 = 'k';

// Calling the function
document.write( noOfDeletions(str2, k2));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
4
5
```