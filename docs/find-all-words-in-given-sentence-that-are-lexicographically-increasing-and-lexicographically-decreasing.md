# 找出给定句子中所有按词典顺序递增和递减的单词

> 原文:[https://www . geesforgeks . org/find-给定句子中的所有单词都是按词典顺序递增和递减的/](https://www.geeksforgeeks.org/find-all-words-in-given-sentence-that-are-lexicographically-increasing-and-lexicographically-decreasing/)

给定一个表示大小为 **N** 的名为**字符串**的句子的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)，任务是找到句子中所有有效的单词，这些单词按照字典顺序按照递增顺序和递减顺序以及它们的计数进行排序。

> **注意:**有效词为:-
> 
> *   单词不包含数字。
> *   大于大小的字 **1** 。

**示例:**

> **输入:** str="geeks for geeks"
> **输出:**
> 1“for”
> 0
> **解释:**“for”是按递增顺序(1)按字典顺序排序的单词。没有一个单词是按降序(0)排列的。
> 
> **输入:** str= "我们以 4 次跑赢了比赛"
> **输出:**
> 1“被”
> 3“我们”、“赢了”、“该”
> **说明:**“被”按递增顺序(1)排序，而“我们”、“赢了”和“该”按递减顺序(3)按字典顺序排序。

**方法:**逐字遍历字符串并检查每个单词是按字典顺序递增还是按字典顺序递减的想法。根据找到的类型打印每个单词。

按照以下步骤详细了解该方法:

*   首先遍历给定字符串中的单词，分别在 **count1** 和 **count2** 中统计按字典顺序递增和按字典顺序递减的单词数。
*   现在首先打印存储在 count1 中的按词典顺序递增的单词数
*   然后一个字一个字地遍历字符串，打印所有按字典顺序递增的单词。
*   对按字典顺序递减的单词重复最后两个步骤。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if string is
// sorted in increasing order
bool issorted(string s)
{
    // using transform() function and ::tolower in STL
    transform(s.begin(), s.end(), s.begin(), ::tolower);

    for (int i = 0; i < s.size() - 1; i++) {
        if (s[i] > s[i + 1] or isdigit(s[i])) {
            return false;
        }
    }
    return true;
}

// Function to check ifstring is
// sorted in decreasing order
bool issortedre(string s)
{
    // using transform() function and ::tolower in STL
    transform(s.begin(), s.end(), s.begin(), ::tolower);

    for (int i = 0; i < s.size() - 1; i++) {
        if (s[i] < s[i + 1] or isdigit(s[i])) {
            return false;
        }
    }
    return true;
}

// Function to count
// the required absolute difference
void count(string s)
{
    stringstream ss(s);
    string word;
    int count1 = 0, count2 = 0;

    // Checking validity of word
    while (ss >> word) {
        if (word.size() == 1)
            continue;

        // Counting the valid words
        // in increasing order
        if (issorted(word)) {
            count1++;
        }

        // Counting the valid words
        // in decreasing order
        else if (issortedre(word)) {
            count2++;
        }
    }

    stringstream ss1(s);

    // Printing count of
    // lexicographically increasing words
    cout << count1 << " ";

    // Print all lexicographically
    // increasing words
    while (ss1 >> word) {
        if (word.size() == 1)
            continue;

        // Printing all valid words
        // in increasing order
        if (issorted(word)) {
            cout << "\"" << word << "\" ";
        }
    }
    cout << endl;

    stringstream ss2(s);

    // Printing count of
    // lexicographically increasing words
    cout << count2 << " ";

    // Print all lexicographically
    // increasing words
    while (ss2 >> word) {
        if (word.size() == 1)
            continue;

        // Printing all valid words
        // in decreasing order
        else if (issortedre(word)) {
            cout << "\"" << word << "\" ";
        }
    }
    cout << endl;
}

// Driver Code
int main()
{
    string s = "We won the match by 4 runs";

    count(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

  static boolean isdigit(char c) {
    return c >= '0' && c <= '9';
  }

  // Function to check if String is
  // sorted in increasing order
  public static boolean issorted(String s)
  {

    // using transform() function and ::tolower in STL
    s = s.toLowerCase();

    for (int i = 0; i < s.length() - 1; i++) {
      if (s.charAt(i) > s.charAt(i + 1) || isdigit(s.charAt(i))) {
        return false;
      }
    }
    return true;
  }

  // Function to check ifString is
  // sorted in decreasing order
  public static boolean issortedre(String s)
  {

    // using transform() function and ::tolower in STL
    s = s.toLowerCase();

    for (int i = 0; i < s.length() - 1; i++) {
      if (s.charAt(i) < s.charAt(i + 1) || isdigit(s.charAt(i))) {
        return false;
      }
    }
    return true;
  }

  // Function to count
  // the required absolute difference
  public static void count(String s) {
    String[] ss = s.split(" ");
    String word;
    int count1 = 0, count2 = 0;

    // Checking validity of word
    for (int i = 0; i < ss.length; i++) {
      word = ss[i];
      if (word.length() == 1)
        continue;

      // Counting the valid words
      // in increasing order
      if (issorted(word)) {
        count1++;
      }

      // Counting the valid words
      // in decreasing order
      else if (issortedre(word)) {
        count2++;
      }
    }

    String[] ss1 = s.split(" ");

    // Printing count of
    // lexicographically increasing words
    System.out.print(count1 + " ");

    // Print all lexicographically
    // increasing words
    for (int i = 0; i < ss1.length; i++) {
      word = ss1[i];
      if (word.length() == 1)
        continue;

      // Printing all valid words
      // in increasing order
      if (issorted(word)) {
        System.out.print("\"" + word + "\" ");
      }
    }
    System.out.println();

    String[] ss2 = s.split(" ");

    // Printing count of
    // lexicographically increasing words
    System.out.print(count2 + " ");

    // Print all lexicographically
    // increasing words
    for (int i = 0; i < ss2.length; i++) {
      word = ss2[i];
      if (word.length() == 1)
        continue;

      // Printing all valid words
      // in decreasing order
      else if (issortedre(word)) {
        System.out.print("\"" + word + "\" ");
      }
    }
    System.out.println();
  }

  // Driver Code
  public static void main(String args[]) {
    String s = "We won the match by 4 runs";

    count(s);
  }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach
def isCharNumber(c):
    return c >= '0' and c <= '9'

# Function to check if string is
# sorted in increasing order
def issorted(s):

    # using transform() function and ::tolower in STL
    s = s.lower()

    for i in range(len(s) - 1):
        if (ord(s[i]) > ord(s[i + 1]) or isCharNumber(s[i])):
            return False
    return True

# Function to check ifstring is
# sorted in decreasing order
def issortedre(s):

    # using transform() function and ::tolower in STL
    s = s.lower()

    for i in range(len(s) - 1):
        if (ord(s[i]) < ord(s[i + 1]) or isCharNumber(s[i])):
            return False
    return True

# Function to count
# the required absolute difference
def count(s):

    word = ""
    count1 = 0
    count2 = 0
    ss = s.split(" ")

    # Checking validity of word
    for i in range(len(ss)):
        word = ss[i]
        if (len(word) == 1):
            continue

        # Counting the valid words
        # in increasing order
        if (issorted(word)):
            count1 += 1

        # Counting the valid words
        # in decreasing order
        elif (issortedre(word)):
            count2 += 1

    # Printing count of
    # lexicographically increasing words
    print(count1, end=" ")

    # Print all lexicographically
    # increasing words
    for i in range(len(ss)):
        word = ss[i]
        if (len(word) == 1):
            continue

        # Printing all valid words
        # in increasing order
        if (issorted(word)):
            print(f" {word} ")

    # Printing count of
    # lexicographically increasing words
    print(count2, end=" ")

    # Print all lexicographically
    # increasing words
    for i in range(len(ss)):
        word = ss[i]
        if (len(word) == 1):
            continue

        # Printing all valid words
        # in decreasing order
        elif (issortedre(word)):
            print(f" {word} ", end=" ")

# Driver Code
s = "We won the match by 4 runs"
count(s)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static bool isdigit(char c)
{
    return c >= '0' && c <= '9';
}

// Function to check if String is
// sorted in increasing order
public static bool issorted(String s)
{

    // Using transform() function and ::tolower in STL
    s = s.ToLower();

    for(int i = 0; i < s.Length - 1; i++)
    {
        if (s[i] > s[i + 1] || isdigit(s[i]))
        {
            return false;
        }
    }
    return true;
}

// Function to check ifString is
// sorted in decreasing order
public static bool issortedre(String s)
{

    // Using transform() function and ::tolower in STL
    s = s.ToLower();

    for(int i = 0; i < s.Length - 1; i++)
    {
        if (s[i] < s[i + 1] || isdigit(s[i]))
        {
            return false;
        }
    }
    return true;
}

// Function to count the
// required absolute difference
public static void count(String s)
{
    String[] ss = s.Split(' ');
    String word;
    int count1 = 0, count2 = 0;

    // Checking validity of word
    for(int i = 0; i < ss.Length; i++)
    {
        word = ss[i];
        if (word.Length == 1)
            continue;

        // Counting the valid words
        // in increasing order
        if (issorted(word))
        {
            count1++;
        }

        // Counting the valid words
        // in decreasing order
        else if (issortedre(word))
        {
            count2++;
        }
    }
    String[] ss1 = s.Split(' ');

    // Printing count of lexicographically
    // increasing words
    Console.Write(count1 + " ");

    // Print all lexicographically
    // increasing words
    for(int i = 0; i < ss1.Length; i++)
    {
        word = ss1[i];
        if (word.Length == 1)
            continue;

        // Printing all valid words
        // in increasing order
        if (issorted(word))
        {
            Console.Write("\"" + word + "\" ");
        }
    }
    Console.WriteLine();

    String[] ss2 = s.Split(' ');

    // Printing count of lexicographically
    // increasing words
    Console.Write(count2 + " ");

    // Print all lexicographically
    // increasing words
    for(int i = 0; i < ss2.Length; i++)
    {
        word = ss2[i];
        if (word.Length == 1)
            continue;

        // Printing all valid words
        // in decreasing order
        else if (issortedre(word))
        {
            Console.Write("\"" + word + "\" ");
        }
    }
    Console.WriteLine();
}

// Driver Code
public static void Main(String []args)
{
    String s = "We won the match by 4 runs";

    count(s);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       function isCharNumber(c) {
           return c >= '0' && c <= '9';
       }

       // Function to check if string is
       // sorted in increasing order
       function issorted(s)
       {

           // using transform() function and ::tolower in STL
           s = s.toLowerCase()

           for (let i = 0; i < s.length - 1; i++) {
               if (s[i].charCodeAt(0) > s[i + 1].charCodeAt(0) || isCharNumber(s[i])) {
                   return false;
               }
           }
           return true;
       }

       // Function to check ifstring is
       // sorted in decreasing order
       function issortedre(s)
       {

           // using transform() function and ::tolower in STL
           s = s.toLowerCase();

           for (let i = 0; i < s.length - 1; i++) {
               if (s[i].charCodeAt(0) < s[i + 1].charCodeAt(0) || isCharNumber(s[i])) {
                   return false;
               }
           }
           return true;
       }

       // Function to count
       // the required absolute difference
       function count(s) {

           let word;
           let count1 = 0, count2 = 0;
           let ss = s.split(" ");

           // Checking validity of word
           for (let i = 0; i < ss.length; i++) {
               word = ss[i]
               if (word.length == 1)
                   continue;

               // Counting the valid words
               // in increasing order
               if (issorted(word)) {
                   count1++;
               }

               // Counting the valid words
               // in decreasing order
               else if (issortedre(word)) {
                   count2++;
               }
           }

           // Printing count of
           // lexicographically increasing words
           document.write(count1 + " ");

           // Print all lexicographically
           // increasing words
           for (let i = 0; i < ss.length; i++) {
               word = ss[i];
               if (word.length == 1)
                   continue;

               // Printing all valid words
               // in increasing order
               if (issorted(word)) {
                   document.write(" " + word + " ")
               }
           }
           document.write('<br>');

           // Printing count of
           // lexicographically increasing words
           document.write(count2 + " ");

           // Print all lexicographically
           // increasing words
           for (let i = 0; i < ss.length; i++) {
               word = ss[i];
               if (word.length == 1)
                   continue;

               // Printing all valid words
               // in decreasing order
               else if (issortedre(word)) {
                   document.write(" " + word + " ")
               }
           }
           document.write('<br>');
       }

       // Driver Code
       let s = "We won the match by 4 runs";
       count(s);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
1 "by" 
3 "We" "won" "the"
```

***时间复杂度:** O(N^2)*
***辅助空间:** O(N)*