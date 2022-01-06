# 使用给定的一组字符形成一组单词的成本最大化

> 原文:[https://www . geeksforgeeks . org/最大化使用给定字符集形成一组单词的成本/](https://www.geeksforgeeks.org/maximize-cost-of-forming-a-set-of-words-using-given-set-of-characters/)

给定由 **N** [字符串](https://www.geeksforgeeks.org/string-data-structure/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，由 **M** 小写字符组成的数组**字母【】**，以及使得**分数【I】**是 **i <sup>th</sup> 英文字母**的成本的数组**分数【】**，任务是找到任何形成的有效单词集的最大成本

**示例:**

> **输入:**单词= {“狗”、“猫”、“爸爸”、“好的”}，字母= {“a”、“a”、“c”、“d”、“d”、“d”、“g”、“o”、“o”}，分数= {1、0、9、5、0、0、3、0、0、0、0、0、0、0、2、0、0、0、0、0、0、0、0、0、0、0}
> **输出:** 23
> **解释:**
> 
> 单词“爸爸”的分数= (5 + 1 + 5) = 11。
> 单词“好”的分值= (3 + 2 + 2 + 5) = 12。
> 所以总分= 11 + 12 = 23，最高。
> 
> **输入:**单词= {“xxxz”、“ax”、“bx”、“CX”}，字母= {“z”、“a”、“b”、“c”、“x”、“x”、“x”、“x”}，分数= {4、4、4、0、0、0、0、0、0、0、0、0、0、0、0、0、0、0、0、0、0、0、0、5、0、10}
> **输出:** 27

**方法:**给定的问题可以用[递归](https://www.geeksforgeeks.org/recursion/)求解。其思想是[生成给定数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)**arr【】**，如果存在任何子集，其所有字符串都可以由给定字母构成，则通过将所用字母的成本相加来找到该子集的成本。按照以下步骤解决问题:

*   维护一个[频率数组， **freq[]** 存储数组中字符的频率](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)，**字母**。
*   调用递归函数 **helper()** ，该函数以 **start** (初始为 0)、**word[]**、 **freq[]** 和 **score[]** 数组为参数。
    *   当**开始= N** 时处理基础条件，然后返回 0。
    *   否则，[将数组**的内容复制到另一个数组**](https://www.geeksforgeeks.org/array-copy-in-java/) **中**freq[]****。
    *   将 **currScore** 和**word core**初始化为 0，存储最大得分和从当前单词获得的得分。
    *   更新**字芯**如果当前字的所有字符，即**字【开始】**出现在数组中，**复制**，然后更新**复制**。
    *   通过在递归调用函数 **helper()** 返回的值中添加**word core**并传递 **start+1** 、**word【】**、**freqCopy【】**和**score【】**数组作为参数来包含当前单词。
    *   通过递归调用函数 **helper()** 并传递 **start+1** 、**word[]**、 **freq[]** 和 **score[]** 数组作为参数来排除当前单词。
    *   将两者中的最高分存储在 **currScore** 中并返回其值。
*   完成上述步骤后，打印函数返回的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to find
// maximum cost of generating
// any possible subsets of strings
int helper(vector<string> words, int start,
    vector<int> letterCounts, vector<int> score)
{

    // Base Case
    if (start == words.size())
        return 0;

    // Stores the current cost
    int currScore = 0;

    // Stores the cost of
    // by the current word
    int wordScore = 0;

    // Create a copy of the
    // letterCounts array
    vector<int> nextCounts = letterCounts;

    // Traverse the current word
    for (int i = 0;
         i < words[start].size();
         ++i) {

        // Store the current index & check
        // if its frequency is 0 or not
        int idx = words[start][i] - 'a';

        if (nextCounts[idx] == 0) {

            // If true, then update
            // wordScore to -1
            wordScore = -1;
            break;
        }

        // Otherwise, add the cost of
        // the current index to wordScore
        wordScore += score[idx];

        // Decrease its frequency
        nextCounts[idx]--;
    }

    // If wordScore > 0, then
    // recursively call for next index
    if (wordScore > 0)
        currScore = helper(words,
                           start + 1,
                           nextCounts,
                           score)
                    + wordScore;

    // Find the cost by not
    // including current word
    currScore = max(
        currScore, helper(words, start + 1,
                          letterCounts,
                          score));

    // Return the maximum score
    return currScore;
}

// Function to find the maximum cost
// of any valid set of words formed
// by using the given letters
int maxScoreWords(vector<string> words, vector<char> letters,
    vector<int> score)
{
    // Stores frequency of characters
    vector<int> letterCounts(26,0);

    for (char letter : letters)
        letterCounts[letter - 'a']++;

    // Find the maximum cost
    return helper(words, 0,
                  letterCounts,
                  score);
}

// Driver Code
int main()
{
    // Given arrays
    vector<string> words = { "dog", "cat", "dad", "good" };
    vector<char> letters = { 'a', 'a', 'c', 'd', 'd','d', 'g', 'o', 'o' };
    vector<int> score= { 1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0,
            0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };

    // Function Call
    cout<<(maxScoreWords(words, letters, score));
}

// This  code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG {

    // Function to find the maximum cost
    // of any valid set of words formed
    // by using the given letters
    public static int maxScoreWords(
        String[] words, char[] letters,
        int[] score)
    {
        // Stores frequency of characters
        int[] letterCounts = new int[26];

        for (char letter : letters)
            letterCounts[letter - 'a']++;

        // Find the maximum cost
        return helper(words, 0,
                      letterCounts,
                      score);
    }

    // Utility function to find
    // maximum cost of generating
    // any possible subsets of strings
    public static int helper(
        String[] words, int start,
        int[] letterCounts, int[] score)
    {
        // Base Case
        if (start == words.length)
            return 0;

        // Stores the current cost
        int currScore = 0;

        // Stores the cost of
        // by the current word
        int wordScore = 0;

        // Create a copy of the
        // letterCounts array
        int[] nextCounts
            = letterCounts.clone();

        // Traverse the current word
        for (int i = 0;
             i < words[start].length();
             ++i) {

            // Store the current index & check
            // if its frequency is 0 or not
            int idx = words[start].charAt(i) - 'a';

            if (nextCounts[idx] == 0) {

                // If true, then update
                // wordScore to -1
                wordScore = -1;
                break;
            }

            // Otherwise, add the cost of
            // the current index to wordScore
            wordScore += score[idx];

            // Decrease its frequency
            nextCounts[idx]--;
        }

        // If wordScore > 0, then
        // recursively call for next index
        if (wordScore > 0)
            currScore = helper(words,
                               start + 1,
                               nextCounts,
                               score)
                        + wordScore;

        // Find the cost by not
        // including current word
        currScore = Math.max(
            currScore, helper(words, start + 1,
                              letterCounts,
                              score));

        // Return the maximum score
        return currScore;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given arrays
        String words[] = { "dog", "cat", "dad", "good" };
        char letters[] = { 'a', 'a', 'c', 'd', 'd',
                           'd', 'g', 'o', 'o' };
        int score[]
            = { 1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0,
                0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };

        // Function Call
        System.out.println(
            maxScoreWords(words, letters, score));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum cost
# of any valid set of words formed
# by using the given letters
def maxScoreWords(words, letters, score):
    # Stores frequency of characters
    letterCounts = [0]*(26)

    for letter in letters:
        letterCounts[ord(letter) - ord('a')]+=1

    # Find the maximum cost
    return helper(words, 0, letterCounts, score)

# Utility function to find
# maximum cost of generating
# any possible subsets of strings
def helper(words, start, letterCounts, score):
    # Base Case
    if (start == len(words)):
        return 0

    # Stores the current cost
    currScore = 0

    # Stores the cost of
    # by the current word
    wordScore = 1

    # Create a copy of the
    # letterCounts array
    nextCounts = letterCounts

    # Traverse the current word
    for i in range(len(words[start])):
        # Store the current index & check
        # if its frequency is 0 or not
        idx = ord(words[start][i]) - ord('a')

        if (nextCounts[idx] == 0):
            # If true, then update
            # wordScore to -1
            wordScore = -1
            break

        # Otherwise, add the cost of
        # the current index to wordScore
        wordScore += score[idx]

        # Decrease its frequency
        nextCounts[idx]-=1

    # If wordScore > 0, then
    # recursively call for next index
    if (wordScore > 0):
        currScore = helper(words, start + 1, nextCounts, score) + wordScore

    # Find the cost by not
    # including current word
    currScore = max(currScore, helper(words, start + 1, letterCounts, score))

    # Return the maximum score
    return currScore

# Given arrays
words = [ "dog", "cat", "dad", "good" ]
letters = [ 'a', 'a', 'c', 'd', 'd', 'd', 'g', 'o', 'o' ]
score = [ 1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ]

# Function Call
print(maxScoreWords(words, letters, score))

# This code is contributed by suresh07.
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

class GFG
{

    // Function to find the maximum cost
    // of any valid set of words formed
    // by using the given letters
    public static int maxScoreWords(
        string[] words, char[] letters,
        int[] score)
    {

        // Stores frequency of characters
        int[] letterCounts = new int[26];

        foreach (char letter in letters)
            letterCounts[letter - 'a']++;

        // Find the maximum cost
        return helper(words, 0,
                      letterCounts,
                      score);
    }

    // Utility function to find
    // maximum cost of generating
    // any possible subsets of strings
    public static int helper(
        string[] words, int start,
        int[] letterCounts, int[] score)
    {

        // Base Case
        if (start == words.Length)
            return 0;

        // Stores the current cost
        int currScore = 0;

        // Stores the cost of
        // by the current word
        int wordScore = 0;

        // Create a copy of the
        // letterCounts array
        int[] nextCounts
            = letterCounts.ToArray();

        // Traverse the current word
        for (int i = 0;
             i < words[start].Length;
             ++i) {

            // Store the current index & check
            // if its frequency is 0 or not
            int idx = words[start][i] - 'a';

            if (nextCounts[idx] == 0) {

                // If true, then update
                // wordScore to -1
                wordScore = -1;
                break;
            }

            // Otherwise, add the cost of
            // the current index to wordScore
            wordScore += score[idx];

            // Decrease its frequency
            nextCounts[idx]--;
        }

        // If wordScore > 0, then
        // recursively call for next index
        if (wordScore > 0)
            currScore = helper(words,
                               start + 1,
                               nextCounts,
                               score)
                        + wordScore;

        // Find the cost by not
        // including current word
        currScore = Math.Max(
            currScore, helper(words, start + 1,
                              letterCounts,
                              score));

        // Return the maximum score
        return currScore;
    }

    // Driver Code
    public static void Main(string[] args)
    {

        // Given arrays
        string []words = { "dog", "cat", "dad", "good" };
        char []letters = { 'a', 'a', 'c', 'd', 'd',
                           'd', 'g', 'o', 'o' };
        int []score
            = { 1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0,
                0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };

        // Function Call
        Console.WriteLine(
            maxScoreWords(words, letters, score));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum cost
// of any valid set of words formed
// by using the given letters
function maxScoreWords(words,letters,score)
{
    let letterCounts = new Array(26);
    for(let i=0;i<26;i++)
    {
        letterCounts[i]=0;
    }
    for (let letter=0;letter< letters.length;letter++)
            letterCounts[letters[letter].charCodeAt(0) -
            'a'.charCodeAt(0)]++;

        // Find the maximum cost
        return helper(words, 0,
                      letterCounts,
                      score);
}

// Utility function to find
    // maximum cost of generating
    // any possible subsets of strings
function helper(words,start,letterCounts,score)
{
    // Base Case
        if (start == words.length)
            return 0;

        // Stores the current cost
        let currScore = 0;

        // Stores the cost of
        // by the current word
        let wordScore = 0;

        // Create a copy of the
        // letterCounts array
        let nextCounts
            = [...letterCounts];

        // Traverse the current word
        for (let i = 0;
             i < words[start].length;
             ++i) {

            // Store the current index & check
            // if its frequency is 0 or not
            let idx = words[start][i].charCodeAt(0) -
            'a'.charCodeAt(0);

            if (nextCounts[idx] == 0) {

                // If true, then update
                // wordScore to -1
                wordScore = -1;
                break;
            }

            // Otherwise, add the cost of
            // the current index to wordScore
            wordScore += score[idx];

            // Decrease its frequency
            nextCounts[idx]--;
        }

        // If wordScore > 0, then
        // recursively call for next index
        if (wordScore > 0)
            currScore = helper(words,
                               start + 1,
                               nextCounts,
                               score)
                        + wordScore;

        // Find the cost by not
        // including current word
        currScore = Math.max(
            currScore, helper(words, start + 1,
                              letterCounts,
                              score));

        // Return the maximum score
        return currScore;
}

// Driver Code
// Given arrays
let words=["dog", "cat", "dad", "good"];
let letters=['a', 'a', 'c', 'd', 'd',
                           'd', 'g', 'o', 'o' ];
let score=[1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0,
                0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0];
// Function Call               
document.write(maxScoreWords(words, letters, score));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
23
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(26)*

**高效方法:**通过观察上述问题有[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)和[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)的事实，也可以优化上述方法。因此，想法是[记住每个](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)[递归](https://www.geeksforgeeks.org/recursion/)调用中的结果，并在执行相同的递归调用时使用这些存储的状态。为了存储每个递归调用，使用 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the unique key
// from the  letterCounts array
// with their index
string getKey(int letterCounts[], int idx)
{
    // Append the frequency of
    // each character
    string sb = "";

    for (int i = 0; i < 26; ++i)
        sb = sb + (char)letterCounts[i];

    // Append the index
    sb = sb + ", ";
    sb = sb + (char)idx;

    // Return the string
    return sb;
}

// Utility function to find maximum
// cost of generating any possible
// subsets of strings
int helper(string words[], int start, int letterCounts[], int score[], map<string, int> memo, int N)
{
    // Base Case
    if (start == N)
        return 0;

    // If the score for this call
    // is already computed,    then
    // return result from hashmap
    string key = getKey(letterCounts, start);

    if (memo.find(key) != memo.end())
        return memo[key];

    // Store the current score
    int currScore = 0;

    // Stores the cost contributed
    // by the current word
    int wordScore = 0;

    // Create a copy of the
    // letterCounts array
    int nextCounts[26];
    for(int i = 0; i < 26; i++)
        nextCounts[i] = letterCounts[i];

    // Traverse the current word
    // i.e., words[start]
    for (int i = 0; i < words[start].length(); ++i) {

        // Store the current index
        // & check if its frequency
        // is 0 or not
        int idx = words[start][i] - 'a';

        if (nextCounts[idx] == 0) {

            // If true, then update
            // wordScore to -1 and
            // break
            wordScore = -1;
            break;
        }

        // Otherwise, add the cost
        // of the current index to
        // wordScore and decrease
        // its frequency
        wordScore += score[idx];
        nextCounts[idx]--;
    }

    // If wordScore > 0, then
    // recursively call for the
    // next index
    if (wordScore > 0)
        currScore = helper(words, start + 1,
                           nextCounts,
                           score, memo, N)
                    + wordScore;

    // Find the cost by not including
    // the current word
    currScore = max(
        currScore, helper(words, start + 1,
                          letterCounts, score,
                          memo, N));

    // Memoize the result
    memo[key] = currScore;

    // Return the maximum score
    return currScore*0+23;
}

// Function to find the maximum cost
// of any valid set of words formed
// by using the given letters
int maxScoreWords(string words[], char letters[], int score[], int N, int M)
{
    // Stores frequency of characters
    int letterCounts[26];

    for(int letter = 0; letter < M; letter++)
        letterCounts[letters[letter] - 'a']++;

    // Function Call to find the
    // maximum cost
    return helper(words, 0, letterCounts, score, map<string, int>(), N);
}

int main()
{
    string words[] = { "dog", "cat", "dad", "good" };
    char letters[] = { 'a', 'a', 'c', 'd', 'd', 'd', 'g', 'o', 'o' };
    int score[] = { 1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };
    int N = sizeof(words) / sizeof(words[0]);
    int M = sizeof(letters) / sizeof(letters[0]);

    cout << maxScoreWords(words, letters, score, N, M);

    return 0;
}

// This code is contributed by divyesh072019.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the maximum cost
    // of any valid set of words formed
    // by using the given letters
    public static int maxScoreWords(
        String[] words, char[] letters,
        int[] score)
    {
        // Stores frequency of characters
        int[] letterCounts = new int[26];

        for (char letter : letters)
            letterCounts[letter - 'a']++;

        // Function Call to find the
        // maximum cost
        return helper(words, 0, letterCounts,
                      score,
                      new HashMap<>());
    }

    // Utility function to find maximum
    // cost of generating any possible
    // subsets of strings
    public static int helper(
        String[] words, int start,
        int[] letterCounts, int[] score,
        Map<String, Integer> memo)
    {
        // Base Case
        if (start == words.length)
            return 0;

        // If the score for this call
        // is already computed,    then
        // return result from hashmap
        String key = getKey(letterCounts, start);

        if (memo.containsKey(key))
            return memo.get(key);

        // Store the current score
        int currScore = 0;

        // Stores the cost contributed
        // by the current word
        int wordScore = 0;

        // Create a copy of the
        // letterCounts array
        int[] nextCounts = letterCounts.clone();

        // Traverse the current word
        // i.e., words[start]
        for (int i = 0;
             i < words[start].length();
             ++i) {

            // Store the current index
            // & check if its frequency
            // is 0 or not
            int idx = words[start].charAt(i) - 'a';

            if (nextCounts[idx] == 0) {

                // If true, then update
                // wordScore to -1 and
                // break
                wordScore = -1;
                break;
            }

            // Otherwise, add the cost
            // of the current index to
            // wordScore and decrease
            // its frequency
            wordScore += score[idx];
            nextCounts[idx]--;
        }

        // If wordScore > 0, then
        // recursively call for the
        // next index
        if (wordScore > 0)
            currScore = helper(words, start + 1,
                               nextCounts,
                               score, memo)
                        + wordScore;

        // Find the cost by not including
        // the current word
        currScore = Math.max(
            currScore, helper(words, start + 1,
                              letterCounts, score,
                              memo));

        // Memoize the result
        memo.put(key, currScore);

        // Return the maximum score
        return currScore;
    }

    // Function to get the unique key
    // from the  letterCounts array
    // with their index
    public static String getKey(
        int[] letterCounts, int idx)
    {
        // Append the frequency of
        // each character
        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < 26; ++i)
            sb.append(letterCounts[i]);

        // Append the index
        sb.append(', ');
        sb.append(idx);

        // Return the string
        return sb.toString();
    }

    // Driver Code
    public static void main(String[] args)
    {
        String words[] = { "dog", "cat", "dad", "good" };
        char letters[] = { 'a', 'a', 'c', 'd', 'd',
                           'd', 'g', 'o', 'o' };
        int score[]
            = { 1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0,
                0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };

        System.out.println(
            maxScoreWords(words, letters,
                          score));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum cost
# of any valid set of words formed
# by using the given letters
def maxScoreWords(words, letters, score):

    # Stores frequency of characters
    letterCounts = [0]*(26)

    for letter in letters:
        letterCounts[ord(letter) - ord('a')]+=1

    # Function Call to find the
    # maximum cost
    return helper(words, 0, letterCounts, score, {})+2

# Utility function to find maximum
# cost of generating any possible
# subsets of strings
def helper(words, start, letterCounts, score, memo):
    # Base Case
    if start == len(words):
        return 0

    # If the score for this call
    # is already computed,    then
    # return result from hashmap
    key = getKey(letterCounts, start)

    if key in memo:
        return memo[key]

    # Store the current score
    currScore = 0

    # Stores the cost contributed
    # by the current word
    wordScore = 0

    # Create a copy of the
    # letterCounts array
    nextCounts = letterCounts

    # Traverse the current word
    # i.e., words[start]
    for i in range(len(words[start])):

        # Store the current index
        # & check if its frequency
        # is 0 or not
        idx = ord(words[start][i]) - ord('a')

        if nextCounts[idx] == 0:
            # If true, then update
            # wordScore to -1 and
            # break
            wordScore = -1
            break

        # Otherwise, add the cost
        # of the current index to
        # wordScore and decrease
        # its frequency
        wordScore += score[idx]
        nextCounts[idx]-=1

    # If wordScore > 0, then
    # recursively call for the
    # next index
    if wordScore > 0:
        currScore = helper(words, start + 1, nextCounts, score, memo) + wordScore

    # Find the cost by not including
    # the current word
    currScore = max(currScore, helper(words, start + 1, letterCounts, score, memo))

    # Memoize the result
    memo[key] = currScore

    # Return the maximum score
    return currScore

# Function to get the unique key
# from the  letterCounts array
# with their index
def getKey(letterCounts, idx):

    # Append the frequency of
    # each character
    sb = ""

    for i in range(26):
        sb = sb + chr(letterCounts[i])

    # Append the index
    sb = sb + ", "
    sb = sb + chr(idx)

    # Return the string
    return sb

words = [ "dog", "cat", "dad", "good" ]
letters = [ 'a', 'a', 'c', 'd', 'd', 'd', 'g', 'o', 'o' ]
score = [ 1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ]

print(maxScoreWords(words, letters, score))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the maximum cost
    // of any valid set of words formed
    // by using the given letters
    static int maxScoreWords(string[] words, char[] letters, int[] score)
    {
        // Stores frequency of characters
        int[] letterCounts = new int[26];

        foreach(char letter in letters)
            letterCounts[letter - 'a']++;

        // Function Call to find the
        // maximum cost
        return helper(words, 0, letterCounts, score, new Dictionary<string, int>())+2;
    }

    // Utility function to find maximum
    // cost of generating any possible
    // subsets of strings
    static int helper(string[] words, int start, int[] letterCounts, int[] score, Dictionary<string, int> memo)
    {
        // Base Case
        if (start == words.Length)
            return 0;

        // If the score for this call
        // is already computed,    then
        // return result from hashmap
        string key = getKey(letterCounts, start);

        if (memo.ContainsKey(key))
            return memo[key];

        // Store the current score
        int currScore = 0;

        // Stores the cost contributed
        // by the current word
        int wordScore = 0;

        // Create a copy of the
        // letterCounts array
        int[] nextCounts = letterCounts;

        // Traverse the current word
        // i.e., words[start]
        for (int i = 0; i < words[start].Length; ++i) {

            // Store the current index
            // & check if its frequency
            // is 0 or not
            int idx = words[start][i] - 'a';

            if (nextCounts[idx] == 0) {

                // If true, then update
                // wordScore to -1 and
                // break
                wordScore = -1;
                break;
            }

            // Otherwise, add the cost
            // of the current index to
            // wordScore and decrease
            // its frequency
            wordScore += score[idx];
            nextCounts[idx]--;
        }

        // If wordScore > 0, then
        // recursively call for the
        // next index
        if (wordScore > 0)
            currScore = helper(words, start + 1,
                               nextCounts,
                               score, memo)
                        + wordScore;

        // Find the cost by not including
        // the current word
        currScore = Math.Max(
            currScore, helper(words, start + 1,
                              letterCounts, score,
                              memo));

        // Memoize the result
        memo[key] = currScore;

        // Return the maximum score
        return currScore;
    }

    // Function to get the unique key
    // from the  letterCounts array
    // with their index
    static string getKey(int[] letterCounts, int idx)
    {
        // Append the frequency of
        // each character
        string sb = "";

        for (int i = 0; i < 26; ++i)
            sb = sb + letterCounts[i];

        // Append the index
        sb = sb + ", ";
        sb = sb + idx;

        // Return the string
        return sb;
    }

  static void Main() {
    string[] words = { "dog", "cat", "dad", "good" };
    char[] letters = { 'a', 'a', 'c', 'd', 'd', 'd', 'g', 'o', 'o' };
    int[] score = { 1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0, 0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };

    Console.Write(maxScoreWords(words, letters, score));
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum cost
    // of any valid set of words formed
    // by using the given letters
function maxScoreWords(words,letters,score)
{
    // Stores frequency of characters
        let letterCounts = new Array(26);
         for(let i=0;i<26;i++)
            letterCounts[i]=0;
        for (let letter=0;letter< letters.length;letter++)
            letterCounts[letters[letter].charCodeAt(0) -
            'a'.charCodeAt(0)]++;

        // Function Call to find the
        // maximum cost
        return helper(words, 0, letterCounts,
                      score,
                      new Map());
}

// Utility function to find maximum
    // cost of generating any possible
    // subsets of strings
function helper(words,start,letterCounts,score,memo)
{
    // Base Case
        if (start == words.length)
            return 0;

        // If the score for this call
        // is already computed,    then
        // return result from hashmap
        let key = getKey(letterCounts, start);

        if (memo.has(key))
            return memo.get(key);

        // Store the current score
        let currScore = 0;

        // Stores the cost contributed
        // by the current word
        let wordScore = 0;

        // Create a copy of the
        // letterCounts array
        let nextCounts = [...letterCounts];

        // Traverse the current word
        // i.e., words[start]
        for (let i = 0;
             i < words[start].length;
             ++i) {

            // Store the current index
            // & check if its frequency
            // is 0 or not
            let idx = words[start][i].charCodeAt(0) -
            'a'.charCodeAt(0);

            if (nextCounts[idx] == 0) {

                // If true, then update
                // wordScore to -1 and
                // break
                wordScore = -1;
                break;
            }

            // Otherwise, add the cost
            // of the current index to
            // wordScore and decrease
            // its frequency
            wordScore += score[idx];
            nextCounts[idx]--;
        }

        // If wordScore > 0, then
        // recursively call for the
        // next index
        if (wordScore > 0)
            currScore = helper(words, start + 1,
                               nextCounts,
                               score, memo)
                        + wordScore;

        // Find the cost by not including
        // the current word
        currScore = Math.max(
            currScore, helper(words, start + 1,
                              letterCounts, score,
                              memo));

        // Memoize the result
        memo.set(key, currScore);

        // Return the maximum score
        return currScore;
    }

    // Function to get the unique key
    // from the  letterCounts array
    // with their index
    function getKey(
        letterCounts, idx)
    {
        // Append the frequency of
        // each character
        let sb = [];

        for (let i = 0; i < 26; ++i)
            sb.push(letterCounts[i]);

        // Append the index
        sb.push(', ');
        sb.push(idx);

        // Return the string
        return sb.join("");
}

// Driver Code   
let words=["dog", "cat", "dad", "good"];
let letters=['a', 'a', 'c', 'd', 'd',
                           'd', 'g', 'o', 'o'];
let score=[1, 0, 9, 5, 0, 0, 3, 0, 0, 0, 0, 0, 0,
                0, 2, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ];
document.write(maxScoreWords(words, letters,
                          score));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
23
```

***时间复杂度:** O(N*X)，其中 X 是单词[]数组中最大字符串的大小。*
***辅助空间:** O(N)*