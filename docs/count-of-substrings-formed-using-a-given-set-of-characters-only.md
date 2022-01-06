# 仅使用给定字符集形成的子字符串计数

> 原文:[https://www . geeksforgeeks . org/substrings-count-formed-仅使用给定的字符集/](https://www.geeksforgeeks.org/count-of-substrings-formed-using-a-given-set-of-characters-only/)

给定一个字符串 **str** 和一个由 **K** 个字符组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从给定的字符数组 **arr[]** 中找到仅包含字符的 **str** 的子字符串数量。

**注意:**字符串**字符串**和 **arr[]** 只包含小写字母。

**示例:**

> **输入:**S =“abcb”，K = 2，charArray[] = {'a '，' b'}
> **输出:** 4
> **解释:**
> 子串使用可用字符为“a”、“ab”、“b”、“b”
> 
> **输入:**S =“aabdbbtr”，K = 4，charArray[] = {'e '，' a '，' r '，' t'}
> **输出:** 6
> **解释:**
> 子串“a”、“aa”、“a”、“t”、“tr”、“r”使用可用字符。

**朴素方法:**朴素方法是[为给定的字符串生成所有可能的子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并检查每个子字符串是否由数组中的给定字符组成 **arr[]** 。如果是，则计数该子串，否则检查下一个子串。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述简单方法可以进行优化，因为我们将删除由给定数组中不存在的字符构成的子字符串的数量 **arr[]** 。以下是步骤:

*   将数组**arr【】**中的字符存储在一个大小为 26 的布尔数组中，这样就可以在 *O(1)* 时间内搜索到任何字符。
*   长度为 N 的字符串组成的子字符串总数为 **(N*(N+1))/2** ，初始化计数为 **(N*(N+1))/2** 。
*   从左到右遍历字符串，并使用变量**最后位置**存储字符串中最后一个字符的索引，该字符不在数组 **arr[]** 中
*   如果在遍历字符串时，我们遇到任何不在**arr【】**中的字符，那么我们将减去包含该字符的子字符串的数量，并且其起点将大于 **lastPos** 的值。假设我们在索引 **i** 处，那么要减去的子串数量将由下式给出

```
(i - lastPos)*(N - i)
```

*   每当我们遇到一个在**charArray【】**中不可用的角色时，更新 **lastPos** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// substrings that can be formed
// using given characters
void numberofsubstrings(string str, int k,
                        char charArray[])
{
    int N = str.length();

    // Boolean array for storing
    // the available characters
    bool available[26] = { 0 };

    // Mark indices of all
    // available characters as 1
    for (int i = 0; i < k; i++) {
        available[charArray[i] - 'a'] = 1;
    }

    // Initialize lastPos as -1
    int lastPos = -1;

    // Initialize ans with the total
    // no of possible substrings
    int ans = (N * (N + 1)) / 2;

    // Traverse the string from
    // left to right
    for (int i = 0; i < N; i++) {

        // If the current character
        // is not present in B
        if (available[str[i] - 'a'] == 0) {

            // Subtract the total possible
            // substrings
            ans -= ((i - lastPos)
                    * (N - i));

            // Update the value of
            // lastpos to current index
            lastPos = i;
        }
    }

    // Print the final answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    // Given String
    string str = "abcb";
    int k = 2;

    // Given character array
    char charArray[k] = { 'a', 'b' };

    // Function Call
    numberofsubstrings(str, k, charArray);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to find the number of
// substrings that can be formed
// using given characters
public static void numberofsubstrings(String str, int k,
                                      char charArray[])
{
    int N = str.length();

    // Boolean array for storing
    // the available characters
    int available[] = new int[26];
    Arrays.fill(available, 0);

    // Mark indices of all
    // available characters as 1
    for(int i = 0; i < k; i++)
    {
       available[charArray[i] - 'a'] = 1;
    }

    // Initialize lastPos as -1
    int lastPos = -1;

    // Initialize ans with the total
    // no of possible substrings
    int ans = (N * (N + 1)) / 2;

    // Traverse the string from
    // left to right
    for(int i = 0; i < N; i++)
    {

       // If the current character
       // is not present in B
       if (available[str.charAt(i) - 'a'] == 0)
       {

           // Subtract the total possible
           // substrings
           ans -= ((i - lastPos) * (N - i));

           // Update the value of
           // lastpos to current index
           lastPos = i;
       }
    }

    // Print the final answer
    System.out.println(ans);
}

// Driver Code
public static void main(String args[])
{

    // Given String
    String str = "abcb";
    int k = 2;

    // Given character array
    char []charArray = {'a', 'b'};

    // Function Call
    numberofsubstrings(str, k, charArray);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of
# substrings that can be formed
# using given characters
def numberofsubstrings(str, k, charArray):

    N = len(str)

    # Boolean array for storing
    # the available characters
    available = [0] * 26

    # Mark indices of all
    # available characters as 1
    for i in range(0, k):
        available[ord(charArray[i]) -
                  ord('a')] = 1

    # Initialize lastPos as -1
    lastPos = -1

    # Initialize ans with the total
    # no of possible substrings
    ans = (N * (N + 1)) / 2

    # Traverse the string from
    # left to right
    for i in range(0, N):

        # If the current character
        # is not present in B
        if (available[ord(str[i]) -
                      ord('a')] == 0):

            # Subtract the total possible
            # substrings
            ans -= ((i - lastPos) * (N - i))

            # Update the value of
            # lastpos to current index
            lastPos = i

    # Print the final answer
    print(int(ans))

# Driver Code

# Given String
str = "abcb"
k = 2

# Given character array
charArray = [ 'a', 'b' ]

# Function call
numberofsubstrings(str, k, charArray)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the number of
// substrings that can be formed
// using given characters
public static void numberofsubstrings(String str, int k,
                                      char []charArray)
{
    int N = str.Length;

    // Boolean array for storing
    // the available characters
    int []available = new int[26];

    // Mark indices of all
    // available characters as 1
    for(int i = 0; i < k; i++)
    {
       available[charArray[i] - 'a'] = 1;
    }

    // Initialize lastPos as -1
    int lastPos = -1;

    // Initialize ans with the total
    // no of possible substrings
    int ans = (N * (N + 1)) / 2;

    // Traverse the string from
    // left to right
    for(int i = 0; i < N; i++)
    {

       // If the current character
       // is not present in B
       if (available[str[i] - 'a'] == 0)
       {

           // Subtract the total possible
           // substrings
           ans -= ((i - lastPos) * (N - i));

           // Update the value of
           // lastpos to current index
           lastPos = i;
       }
    }

    // Print the final answer
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(String []args)
{

    // Given String
    String str = "abcb";
    int k = 2;

    // Given character array
    char []charArray = {'a', 'b'};

    // Function Call
    numberofsubstrings(str, k, charArray);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the number of
// substrings that can be formed
// using given characters
function numberofsubstrings(str, k, charArray)
{
    var N = str.length;

    // Boolean array for storing
    // the available characters
    var available = [ 26 ];

    // Mark indices of all
    // available characters as 1
    for(var i = 0; i < k; i++)
    {
    available[charArray[i] - 'a'] = 1;
    }

    // Initialize lastPos as -1
    var lastPos = -1;

    // Initialize ans with the total
    // no of possible substrings
    var ans = (N * (N + 1)) / 2;

    // Traverse the string from
    // left to right
    for(var i = 0; i < N; i++)
    {

    // If the current character
    // is not present in B
    if (available[str.charAt(i) - 'a'] == 0)
    {

        // Subtract the total possible
        // substrings
        ans -= ((i - lastPos) * (N - i));

        // Update the value of
        // lastpos to current index
        lastPos = i;
    }
    }

    // Print the final answer
    document.write(ans);
}

// Driver Code
    // Given String
    var str = "abcb";
    var k = 2;

    // Given character array
    var charArray = ['a', 'b'];

    // Function Call
    numberofsubstrings(str, k, charArray);

// This code is contributed by shivanisinghss2110.

</script>
```

**Output:**

```
4
```

**时间复杂度:** *O(N)* ，N 为弦的长度
**辅助空间:** *O(1)*