# 最大化字符串的分区，使得字符串的每个字符出现在一个子字符串中

> 原文:[https://www . geesforgeks . org/最大化字符串分区，使得字符串中的每个字符都出现在一个子字符串中/](https://www.geeksforgeeks.org/maximized-partitions-of-a-string-such-that-each-character-of-the-string-appears-in-one-substring/)

给定一个字符串 **S** ，将给定的字符串拆分成尽可能多的子字符串，这样给定字符串中的每个字符都出现在一个子字符串中，并打印所有这些可能的部分。任务是打印这些子字符串。

**示例:**

> **输入:**S = " ababcbacadefegdehijhkij "
> **输出:**
> ababcbaca defegde hijhkij
> **说明:**
> a、b、c 只出现在第一个字符串中。
> d、e、f、g 只出现在第二串中。
> h、I、j、k、l 只出现在第三串。
> **输入:** S = "acbbcc"
> **输出:**
> a cbbcc
> **解释:**
> a 仅出现在第一个字符串中。
> b、c 只出现在第二串中。

**方法:按照以下步骤解决问题:**

1.  存储字符串中所有字符出现的最后一个[索引。](https://www.geeksforgeeks.org/find-last-index-character-string/)
2.  由于字符串只包含小写字母，只需使用固定大小的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**26**来存储每个字符的最后索引。
3.  初始化一个空字符串 **ans = ""** 并遍历给定的字符串，然后按照以下步骤操作:
    *   如果字符的最后一个位置大于当前索引，则将当前字符添加到字符串 ans 中，并增加分区的长度。
    *   如果当前字符的最后位置等于当前索引，则打印存储在 **ans** 中的当前字符串，并将 **ans** 初始化为 **""** 以存储字符串的下一个分区。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the substrings
void print_substring(string s)
{
    int n = s.size();

    // Stores the substrings
    string str = "";

    // Stores last index of
    // characters of string s
    vector<int> ans;

    if (n == 0) {
        cout << "-1";
        return;
    }

    // Find the last position of
    // each character in the string
    vector<int> last_pos(26, -1);

    for (int i = n - 1; i >= 0; --i) {

        // Update the last index
        if (last_pos[s[i] - 'a'] == -1) {
            last_pos[s[i] - 'a'] = i;
        }
    }

    int minp = -1;

    // Iterate the given string
    for (int i = 0; i < n; ++i) {

        // Get the last index of s[i]
        int lp = last_pos[s[i] - 'a'];

        // Extend the current partition
        // characters last pos
        minp = max(minp, lp);

        // If the current pos of
        // character equals the min pos
        // then the end of partition
        if (i == minp) {

            // Add the respective character first
            str += s[i];

            // Store the partition's
            // len and reset variables
            cout << str << ' ';

            // Update the minp and str
            minp = -1;
            str = "";
        }
        else {
            str += s[i];
        }
    }
}

// Driver Code
int main()
{
    // Input string
    string S = "ababcbacadefegdehijhklij";

    // Function call
    print_substring(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to print all the substrings
    public static void print_substring(String s)
    {
        int n = s.length();

        // Stores the substrings
        String str = "";

        // Stores last index of
        // characters of string s
        Vector<Integer> ans = new Vector<Integer>();

        if (n == 0) {
            System.out.print("-1");
            return;
        }

        // Find the last position of
        // each character in the string
        int[] last_pos = new int[26];
        Arrays.fill(last_pos, -1);

        for (int i = n - 1; i >= 0; --i) {

            // Update the last index
            if (last_pos[s.charAt(i) - 'a'] == -1) {
                last_pos[s.charAt(i) - 'a'] = i;
            }
        }

        int minp = -1;

        // Iterate the given string
        for (int i = 0; i < n; ++i) {

            // Get the last index of s[i]
            int lp = last_pos[s.charAt(i) - 'a'];

            // Extend the current partition
            // characters last pos
            minp = Math.max(minp, lp);

            // If the current pos of
            // character equals the min pos
            // then the end of partition
            if (i == minp) {

                // Add the respective character first
                str += s.charAt(i);

                // Store the partition's
                // len and reset variables
                System.out.print(str + ' ');

                // Update the minp and str
                minp = -1;
                str = "";
            }
            else {
                str += s.charAt(i);
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input string
        String S = "ababcbacadefegdehijhklij";

        // Function call
        print_substring(S);
    }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print all the substrings
def print_substring(s):

    n = len(s)

    # Stores the substrings
    str = ""

    # Stores last index of
    # characters of string s
    ans = []

    if (n == 0):
        print("-1")
        return

    # Find the last position of
    # each character in the string
    last_pos = [-1] * 26

    for i in range(n - 1, -1, -1):

        # Update the last index
        if (last_pos[ord(s[i]) - ord('a')] == -1):
            last_pos[ord(s[i]) - ord('a')] = i

    minp = -1

    # Iterate the given string
    for i in range(n):

        # Get the last index of s[i]
        lp = last_pos[ord(s[i]) - ord('a')]

        # Extend the current partition
        # characters last pos
        minp = max(minp, lp)

        # If the current pos of
        # character equals the min pos
        # then the end of partition
        if (i == minp):

            #Add the respective character to the string
            str += s[i]

            # Store the partition's
            # len and reset variables
            print(str, end = " ")

            # Update the minp and str
            minp = -1
            str = ""

        else:
            str += s[i]

# Driver Code

# Input string
S = "ababcbacadefegdehijhklij"

# Function call
print_substring(S)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print all the substrings
public static void print_substring(String s)
{
    int n = s.Length;

    // Stores the substrings
    String str = "";

    // Stores last index of
    // characters of string s
    //List<int> ans = new List<int>();

    if (n == 0)
    {
        Console.Write("-1");
        return;
    }

    // Find the last position of
    // each character in the string
    int[] last_pos = new int[26];
    for(int i = 0; i < 26; i++)
        last_pos[i] = -1;

    for(int i = n - 1; i >= 0; --i)
    {

        // Update the last index
        if (last_pos[s[i] - 'a'] == -1)
        {
            last_pos[s[i] - 'a'] = i;
        }
    }

    int minp = -1;

    // Iterate the given string
    for(int i = 0; i < n; ++i)
    {

        // Get the last index of s[i]
        int lp = last_pos[s[i] - 'a'];

        // Extend the current partition
        // characters last pos
        minp = Math.Max(minp, lp);

        // If the current pos of
        // character equals the min pos
        // then the end of partition
        if (i == minp)
        {
            //Add respective character to the string 
            str += s[i];

            // Store the partition's
            // len and reset variables
            Console.Write(str + ' ');

            // Update the minp and str
            minp = -1;
            str = "";
        }
        else
        {
            str += s[i];
        }
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Input string
    String S = "ababcbacadefegdehijhklij";

    // Function call
    print_substring(S);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

 // Function to print all the substrings
    function print_substring(s)
    {
        let n = s.length;

        // Stores the substrings
        let str = "";

        // Stores last index of
        // characters of string s
        let ans = [];

        if (n == 0) {
            document.write("-1");
            return;
        }

        // Find the last position of
        // each character in the string
        let last_pos = Array(26).fill(-1);

        for (let i = n - 1; i >= 0; --i) {

            // Update the last index
            if (last_pos[s[i].charCodeAt() - 'a'.charCodeAt()] == -1) {
                last_pos[s[i].charCodeAt() - 'a'.charCodeAt()] = i;
            }
        }

        let minp = -1;

        // Iterate the given string
        for (let i = 0; i < n; ++i) {

            // Get the last index of s[i]
            let lp = last_pos[s[i].charCodeAt() - 'a'.charCodeAt()];

            // Extend the current partition
            // characters last pos
            minp = Math.max(minp, lp);

            // If the current pos of
            // character equals the min pos
            // then the end of partition
            if (i == minp) {

                // Add the respective character first
                str += s[i];

                // Store the partition's
                // len and reset variables
                document.write(str + ' ');

                // Update the minp and str
                minp = -1;
                str = "";
            }
            else {
                str += s[i];
            }
        }
    }

// Driver Code

     // Input string
        let S = "ababcbacadefegdehijhklij";

        // Function call
        print_substring(S);

 // This code is contributed by avijitmondal998.
</script>
```

**Output**

```
ababcbaca defegde hijhklij 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)