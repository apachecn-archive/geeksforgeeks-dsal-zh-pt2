# 通过将另一个字符串作为子字符串删除来最小化字符串的长度

> 原文:[https://www . geeksforgeeks . org/通过从字符串中删除另一个字符串作为子字符串来最小化字符串长度/](https://www.geeksforgeeks.org/minimize-length-of-a-string-by-removing-occurrences-of-another-string-from-it-as-a-substring/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和一个字符串 **T** ，任务是在移除字符串 **S** 中作为子字符串的所有可能出现的字符串 **T** 之后，找到字符串 **S** 可以减少到的最小可能长度。

**示例:**

> **输入:** S = "aabcbcbd "，T = "abc"
> **输出:** 2
> **解释:**
> 删除子串{S[1]，…，S[3]}并将剩余字符串修改为“abcbd”。
> 删除子字符串{S[0]..S[2]}，结果字符串修改为“bd”。
> 所以，要求的答案是 2。
> 
> **输入:** S = "asdfbc "，T = "xyz"
> **输出:** 0
> **说明:**
> 在 S 中没有出现字符串“xyz”作为子串

**方法:**思路是[迭代给定字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并初始化一个辅助字符串，检查新形成的字符串是否作为给定字符串中的子字符串出现。如果发现是真的，那么只需从给定的字符串中删除该子字符串。

按照以下步骤解决此问题:

1.  首先，通过[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并跟踪遇到的字符来识别子字符串 **T** 。
2.  但是，当子串被移除时，剩余部分的连接是昂贵的，因为每个字符必须向后移动 **M** 个位置。
3.  为了避免这种情况，维护一个字符串，比如 **temp** ，它只包含到目前为止迭代的字符。
4.  因此，如果所需的子字符串出现在 **temp** 中，那么只需在恒定的计算时间内删除最后一个 **M** 字符。
5.  最后，在执行所有操作后，打印字符串的最小长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to minimize length of
// string S after removing all
// occurrences of string T as substring
void minLength(string& S, string& T,
               int N, int M)
{
    string temp;

    // Count of characters
    // required to be removed
    int subtract = 0;

    // Iterate over the string
    for (int i = 0; i < N; ++i) {

        // Insert the current
        // character to temp
        temp.push_back(S[i]);

        // Check if the last M
        // characters forms t or not
        if (temp.size() >= M) {

            // Getting the last M
            // characters. If they
            // are equal to t then
            // remove the last M
            // characters from the temp string
            if (temp.substr(temp.size() - M, M) == T) {

                // Incrementing subtract by M
                subtract += M;

                // Removing last M
                // characters from the
                // string
                int cnt = 0;
                while (cnt != M) {
                    temp.pop_back();
                    ++cnt;
                }
            }
        }
    }

    // Print the final answer
    cout << (N - subtract) << "\n";
}

// Driver Code
int main()
{
    // Given string S & T
    string S = "aabcbcbd", T = "abc";

    // Length of string S
    int N = S.size();

    // Length of string T
    int M = T.size();

    // Prints the count of
    // operations required
    minLength(S, T, N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to minimize length of
// string S after removing all
// occurrences of string T as substring
static void minLength(String S, String T,
                      int N, int M)
{
    String temp = "";

    // Count of characters
    // required to be removed
    int subtract = 0;

    // Iterate over the string
    for(int i = 0; i < N; ++i)
    {

        // Insert the current
        // character to temp
        temp += S.charAt(i);

        // Check if the last M
        // characters forms t or not
        if (temp.length() >= M)
        {

            // Getting the last M characters.
            // If they are equal to t then
            // remove the last M characters
            // from the temp string
            if (T.equals(
                temp.substring(temp.length() - M,
                               temp.length())))
            {

                // Incrementing subtract by M
                subtract += M;

                // Removing last M
                // characters from the
                // string
                int cnt = 0;
                while (cnt != M)
                {
                    temp = temp.substring(
                        0, temp.length() - 1);
                    ++cnt;
                }
            }
        }
    }

    // Print the final answer
    System.out.println((N - subtract));
}

// Driver Code
public static void main(String[] args)
{

    // Given string S & T
    String S = "aabcbcbd", T = "abc";

    // Length of string S
    int N = S.length();

    // Length of string T
    int M = T.length();

    // Prints the count of
    // operations required
    minLength(S, T, N, M);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to minimize length of
# string S after removing all
# occurrences of string T as substring
def minLength(S, T, N, M):
    temp = "";

    # Count of characters
    # required to be removed
    subtract = 0;

    # Iterate over the string
    for i in range(N):

        # Insert the current
        # character to temp
        temp += S[i];

        # Check if the last M
        # characters forms t or not
        if (len(temp) >= M):

            # Getting the last M characters.
            # If they are equal to t then
            # remove the last M characters
            # from the temp string
            if (T ==(temp[len(temp) - M: len(temp)])):

                # Incrementing subtract by M
                subtract += M;

                # Removing last M
                # characters from the
                # string
                cnt = 0;
                while (cnt != M):
                    temp = temp[0: len(temp) - 1];
                    cnt+= 1;

    # Print the final answer
    print((N - subtract));

# Driver Code
if __name__ == '__main__':

    # Given string S & T
    S = "aabcbcbd";
    T = "abc";

    # Length of string S
    N = len(S);

    # Length of string T
    M = len(T);

    # Prints the count of
    # operations required
    minLength(S, T, N, M);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to minimize length of
// string S after removing all
// occurrences of string T as substring
static void minLength(String S, String T,
                      int N, int M)
{
    String temp = "";

    // Count of characters
    // required to be removed
    int subtract = 0;

    // Iterate over the string
    for(int i = 0; i < N; ++i)
    {

        // Insert the current
        // character to temp
        temp += S[i];

        // Check if the last M
        // characters forms t or not
        if (temp.Length >= M)
        {

            // Getting the last M characters.
            // If they are equal to t then
            // remove the last M characters
            // from the temp string
            if (T.Equals(
                temp.Substring(temp.Length - M, M)))
            {

                // Incrementing subtract by M
                subtract += M;

                // Removing last M
                // characters from the
                // string
                int cnt = 0;

                while (cnt != M)
                {
                    temp = temp.Substring(
                        0, temp.Length - 1);
                    ++cnt;
                }
            }
        }
    }

    // Print the readonly answer
    Console.WriteLine((N - subtract));
}

// Driver Code
public static void Main(String[] args)
{

    // Given string S & T
    String S = "aabcbcbd", T = "abc";

    // Length of string S
    int N = S.Length;

    // Length of string T
    int M = T.Length;

    // Prints the count of
    // operations required
    minLength(S, T, N, M);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to minimize length of
// string S after removing all
// occurrences of string T as substring
function minLength(S, T,
                      N, M)
{
    let temp = "";

    // Count of characters
    // required to be removed
    let subtract = 0;

    // Iterate over the string
    for(let i = 0; i < N; ++i)
    {

        // Insert the current
        // character to temp
        temp += S[i];

        // Check if the last M
        // characters forms t or not
        if (temp.length >= M)
        {

            // Getting the last M characters.
            // If they are equal to t then
            // remove the last M characters
            // from the temp string
            if (T ==
                temp.substr(temp.length - M,
                               temp.length))
            {

                // Incrementing subtract by M
                subtract += M;

                // Removing last M
                // characters from the
                // string
                let cnt = 0;
                while (cnt != M)
                {
                    temp = temp.substr(
                        0, temp.length - 1);
                    ++cnt;
                }
            }
        }
    }

    // Print the final answer
    document.write((N - subtract));
}

    // Driver Code

      // Given string S & T
    let S = "aabcbcbd", T = "abc";

    // Length of string S
    let N = S.length;

    // Length of string T
    let M = T.length;

    // Prints the count of
    // operations required
    minLength(S, T, N, M);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)