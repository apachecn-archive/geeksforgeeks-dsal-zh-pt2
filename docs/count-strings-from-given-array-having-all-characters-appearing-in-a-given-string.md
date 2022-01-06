# 统计给定数组中所有字符都出现在给定字符串中的字符串

> 原文:[https://www . geeksforgeeks . org/count-strings-from-给定数组-让所有字符出现在给定字符串中/](https://www.geeksforgeeks.org/count-strings-from-given-array-having-all-characters-appearing-in-a-given-string/)

给定一个大小为 **N** 的[字符串数组](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/)**arr【】【**】,以及一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是从字符串 **S.** 中出现其所有字符的数组中找到字符串的数量

**示例:**

> **输入:**arr[][]= {“ab”、“aab”、“abaaaa”、“bbd”}，S =“ab”
> **输出:** 3
> **说明:**字符串“ab”具有字符串 S 中出现的所有字符。
> 字符串“aab”具有字符串 S 中出现的所有字符。
> 字符串“abaaaa”具有字符串 S 中出现的所有字符
> 
> **输入:** arr[] = {“极客”、“for”、“极客”}，S = "ds"
> **输出:** 0

**方法:**思路是用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)解决问题。按照以下步骤解决问题:

1.  初始化一组无序的字符，比如有效的 T2，和一个计数器变量，比如 T4
2.  [将字符串 **S** 的所有字符插入到有效的集合](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) **中。**
3.  [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 并执行以下步骤:
    *   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**arr【I】**的字符，并借助设置**有效**检查字符串**arr【I】**的所有字符是否出现在字符串 **S** 中。
    *   如果发现为真，则增加 **cnt** 。
4.  最后，打印得到的结果 **cnt**

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// strings from an array having all
// characters appearing in the string S
int countStrings(string S, vector<string>& list)
{
    // Initialize a set to store all
    // distinct characters of string S
    unordered_set<char> valid;

    // Traverse over string S
    for (auto x : S) {

        // Insert characters
        // into the Set
        valid.insert(x);
    }

    // Stores the required count
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < list.size(); i++) {

        int j = 0;

        // Traverse over string arr[i]
        for (j = 0; j < list[i].size(); j++) {

            // Check if character in arr[i][j]
            // is present in the string S or not
            if (valid.count(list[i][j]))
                continue;
            else
                break;
        }
        // Increment the count if all the characters
        // of arr[i] are present in the string S
        if (j == list[i].size())
            cnt++;
    }

    // Finally, print the count
    return cnt;
}
// Driver code
int main()
{
    vector<string> arr = { "ab", "aab",
                           "abaaaa", "bbd" };
    string S = "ab";

    cout << countStrings(S, arr) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

// Function to count the number of
// Strings from an array having all
// characters appearing in the String S
static int countStrings(String S, String []list)
{

    // Initialize a set to store all
    // distinct characters of String S
    HashSet<Character> valid = new HashSet<Character>();

    // Traverse over String S
    for (char x : S.toCharArray())
    {

        // Insert characters
        // into the Set
        valid.add(x);
    }

    // Stores the required count
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < list.length; i++)
    {
        int j = 0;

        // Traverse over String arr[i]
        for (j = 0; j < list[i].length(); j++)
        {

            // Check if character in arr[i][j]
            // is present in the String S or not
            if (valid.contains(list[i].charAt(j)))
                continue;
            else
                break;
        }

        // Increment the count if all the characters
        // of arr[i] are present in the String S
        if (j == list[i].length())
            cnt++;
    }

    // Finally, print the count
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    String []arr = { "ab", "aab",
                           "abaaaa", "bbd" };
    String S = "ab";
    System.out.print(countStrings(S, arr) +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the number of
# strings from an array having all
# characters appearing in the string S
def countStrings(S, list):

    # Initialize a set to store all
    # distinct characters of  S
    valid = {}

    # Traverse over  S
    for x in S:

        # Insert characters
        # into the Set
        valid[x] = 1

    # Stores the required count
    cnt = 0

    # Traverse the array
    for i in range(len(list)):
        j = 0

        # Traverse over  arr[i]
        while j < len(list[i]):

            # Check if character in arr[i][j]
            # is present in the  S or not
            if (list[i][j] in valid):
                j += 1
                continue
            else:
                break
            j += 1

        # Increment the count if all the characters
        # of arr[i] are present in the  S
        if (j == len(list[i])):
            cnt += 1

    # Finally, print the count
    return cnt

# Driver code
if __name__ == '__main__':
    arr = ["ab", "aab", "abaaaa", "bbd"]
    S,l = "ab",[]

    print(countStrings(S, arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to count the number of
// Strings from an array having all
// characters appearing in the String S
static int countStrings(String S, String []list)
{

    // Initialize a set to store all
    // distinct characters of String S
    HashSet<char> valid = new HashSet<char>();

    // Traverse over String S
    foreach (char x in S.ToCharArray())
    {

        // Insert characters
        // into the Set
        valid.Add(x);
    }

    // Stores the required count
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < list.Length; i++)
    {
        int j = 0;

        // Traverse over String arr[i]
        for (j = 0; j < list[i].Length; j++)
        {

            // Check if character in arr[i,j]
            // is present in the String S or not
            if (valid.Contains(list[i][j]))
                continue;
            else
                break;
        }

        // Increment the count if all the characters
        // of arr[i] are present in the String S
        if (j == list[i].Length)
            cnt++;
    }

    // Finally, print the count
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    String []arr = { "ab", "aab",
                           "abaaaa", "bbd" };
    String S = "ab";
    Console.Write(countStrings(S, arr) +"\n");
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the number of
// strings from an array having all
// characters appearing in the string S
function countStrings(S, list)
{

    // Initialize a set to store all
    // distinct characters of string S
    let valid = new Set();

    // Traverse over string S
    for(let x of S)
    {

        // Insert characters
        // into the Set
        valid.add(x);
    }

    // Stores the required count
    let cnt = 0;

    // Traverse the array
    for(let i = 0; i < list.length; i++)
    {
        let j = 0;

        // Traverse over string arr[i]
        for(j = 0; j < list[i].length; j++)
        {

            // Check if character in arr[i][j]
            // is present in the string S or not
            if (valid.has(list[i][j]))
                continue;
            else
                break;
        }

        // Increment the count if all the characters
        // of arr[i] are present in the string S
        if (j == list[i].length)
            cnt++;
    }

    // Finally, print the count
    return cnt;
}

// Driver code
let arr = [ "ab", "aab",
            "abaaaa", "bbd" ];
let S = "ab";

document.write(countStrings(S, arr) + "<br>");

// This code contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*