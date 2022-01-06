# 从包含所有给定单词的给定字符串中找到一个子字符串的最小起始索引

> 原文:[https://www . geesforgeks . org/find-最小起始索引-从给定字符串开始-包含所有给定单词的连续方式/](https://www.geeksforgeeks.org/find-least-start-index-of-a-substring-from-given-string-that-contains-all-the-given-words-in-a-contiguous-manner/)

给定一个字符串 **S** 和一个长度相等的**单词数组**(字符串) **arr[]。**任务是以**连续**的方式找到包含所有给定单词的子串的**最小开始索引**。如果没有找到这样的索引，返回 **-1** 。
注意:单词可以是任意顺序。

**示例:**

> **输入**:arr[]= {“bat”、“bal”、“cat”}，S =“helloctabybalbatcatyo”
> T3】输出 : 11
> **解释**:从索引 11 开始的子串包含所有 3 个连续的单词。
> 
> **输入** : arr[ ] = {"hat "，" mat"}，S = " askfndsubsdlvnsk "
> **输出** : -1
> **解释**:没有连续包含两个单词的子串。

**方法:**这个任务可以通过在最小索引处找到任意一个单词，然后从第一个单词的结束索引处开始模拟这个过程，检查所有其他单词是否都出现在连续的位置来解决。
按照步骤解决问题:

*   将所有单词存储在一个 [<u>无序集合</u>](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/) 中，说出 **st、**以在恒定时间内查找单词。
*   遍历字符串，从长度为 **M** (每个单词的长度)的每个索引处开始检查子字符串，一旦找到存在于 **S、**中的有效子字符串，就开始模拟前一个子字符串结束索引后的过程，并检查所有其他单词是否以连续的方式存在。
*   如果所有单词都是以连续的方式找到的，则返回找到的最小索引，否则返回-1。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the min index
int minIndex(string arr[], string S, int N, int M)
{
    // Unordered set to store all words
    unordered_set<string> st;

    // Insert each word in the set
    for (int i = 0; i < N; i++)
        st.insert(arr[i]);

    // Traverse over the string s
    for (int i = 0; i < S.size() - M; i++) {
        // Substring to check whether
        // it is part of array of
        // words or not
        string x = S.substr(i, M);

        // Variables to check the condition, store the
        // index and keep count of words
        int p = 0, k = -1, d = N;

        // If substring is one of the words
        if (st.find(x) != st.end()) {

            // Store the index
            k = i;

            // Decrement d
            d--;

            // Check further
            for (int j = i + M; j < S.size() - M; j += M) {

                // Substring to check
                // whether it is part of
                // array of words or not
                string y = S.substr(j, M);

                // If substring is not part of word
                if (d == 0)
                    break;
                if (st.find(y) == st.end()) {
                    p = 1;
                    i = j - 1;
                    break;
                }
                d--;
            }
        }

        // If index is found, return the index
        if (p == 0 and k != -1)
            return k;
    }

    // If no index found, return -1
    return -1;
}

// Driver Code
int main()
{

    // Input
    string arr[] = { "bat", "bal", "cat" };
    string S = "hellocatbyebalbatcatyo";
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = arr[0].size();

    // Function call to find the minimum index
    cout << minIndex(arr, S, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the min index
static int minIndex(String arr[], String S, int N, int M)
{

    // Unordered set to store all words
    HashSet<String> st = new HashSet<String>();

    // Insert each word in the set
    for (int i = 0; i < N; i++)
        st.add(arr[i]);

    // Traverse over the String s
    for (int i = 0; i < S.length() - M; i++)
    {

        // SubString to check whether
        // it is part of array of
        // words or not
        String x = S.substring(i, i+M);

        // Variables to check the condition, store the
        // index and keep count of words
        int p = 0, k = -1, d = N;

        // If subString is one of the words
        if (st.contains(x)) {

            // Store the index
            k = i;

            // Decrement d
            d--;

            // Check further
            for (int j = i + M; j < S.length() - M; j += M) {

                // SubString to check
                // whether it is part of
                // array of words or not
                String y = S.substring(j, j+M);

                // If subString is not part of word
                if (d == 0)
                    break;
                if (!st.contains(y)) {
                    p = 1;
                    i = j - 1;
                    break;
                }
                d--;
            }
        }

        // If index is found, return the index
        if (p == 0 && k != -1)
            return k;
    }

    // If no index found, return -1
    return -1;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    String arr[] = { "bat", "bal", "cat" };
    String S = "hellocatbyebalbatcatyo";
    int N = arr.length;
    int M = arr[0].length();
    // Function call to find the minimum index
    System.out.print(minIndex(arr, S, N, M));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the min index
def minIndex(arr, S, N, M):

   # Unordered set to store all words
    st = set(arr)

    # Insert each word in the set
    for i in range(len(S)-M):
        x = S[i: i+M]

         # Variables to check the condition, store the
        # index and keep count of words
        p = 0
        k = -1
        d = N

        # If substring is one of the words
        if x in st:

          # Store the index
            k = i

           # Decrement d
            d -= 1

            # Traverse over the string s
            for j in range(i+M, len(S)-M, M):

               # Substring to check
                # whether it is part of
                # array of words or not
                y = S[j: j+M]

                # If substring is not part of word
                if d == 0:
                    break
                if y not in st:
                    p = 1
                    i = j-1
                    break
                d -= 1

        # If index is found, return the index
        if p == 0 and k != -1:
            return k

    # If no index found return -1     
    return -1

# Driver code
arr = ["bat", "bal", "cat"]
S = "hellocatbyebalbatcatyo"
N = len(arr)
M = len(arr[0])
print(minIndex(arr, S, N, M))

# This code is contributed by parthmanchanda81
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the min index
static int minIndex(string []arr, string S, int N, int M)
{
    // Unordered set to store all words
    HashSet<string> st = new HashSet<string>();

    // Insert each word in the set
    for (int i = 0; i < N; i++)
        st.Add(arr[i]);

    // Traverse over the string s
    for (int i = 0; i < S.Length - M; i++) {
        // Substring to check whether
        // it is part of array of
        // words or not
        string x = S.Substring(i, M);

        // Variables to check the condition, store the
        // index and keep count of words
        int p = 0, k = -1, d = N;

        // If substring is one of the words
        if (st.Contains(x)) {

            // Store the index
            k = i;

            // Decrement d
            d--;

            // Check further
            for (int j = i + M; j < S.Length - M; j += M) {

                // Substring to check
                // whether it is part of
                // array of words or not
                string y = S.Substring(j, M);

                // If substring is not part of word
                if (d == 0)
                    break;
                if (st.Contains(y)==false) {
                    p = 1;
                    i = j - 1;
                    break;
                }
                d--;
            }
        }

        // If index is found, return the index
        if (p == 0 && k != -1)
            return k;
    }

    // If no index found, return -1
    return -1;
}

// Driver Code
public static void Main()
{

    // Input
    string []arr = { "bat", "bal", "cat" };
    string S = "hellocatbyebalbatcatyo";
    int N = arr.Length;
    int M = arr[0].Length;

    // Function call to find the minimum index
    Console.Write(minIndex(arr, S, N, M));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the min index
function minIndex(arr, S, N, M) {
  // Unordered set to store all words
  let st = new Set();

  // Insert each word in the set
  for (let i = 0; i < N; i++) st.add(arr[i]);

  // Traverse over the string s
  for (let i = 0; i < S.length - M; i++) {
    // Substring to check whether
    // it is part of array of
    // words or not
    let x = S.substr(i, M);
    console.log(x);
    // Variables to check the condition, store the
    // index and keep count of words
    let p = 0,
      k = -1,
      d = N;

    // If substring is one of the words
    if (st.has(x)) {
      // Store the index
      k = i;

      // Decrement d
      d--;

      // Check further
      for (let j = i + M; j < S.length - M; j += M) {
        // Substring to check
        // whether it is part of
        // array of words or not
        let y = S.substr(j, M);

        // If substring is not part of word
        if (d == 0) break;
        if (!st.has(y)) {
          p = 1;
          i = j - 1;
          break;
        }
        d--;
      }
    }

    // If index is found, return the index
    if (p == 0 && k != -1) return k;
  }

  // If no index found, return -1
  return -1;
}

// Driver Code

// Input
let arr = ["bat", "bal", "cat"];
let S = "hellocatbyebalbatcatyo";
let N = arr.length;
let M = arr[0].length;

// Function call to find the minimum index
document.write(minIndex(arr, S, N, M));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
11
```

***时间复杂度***:O(S * M)**S**为字符串长度 **M** 为每个单词的长度
***辅助空格*** : O(N)，N 为字数