# 一串单词之间的最小距离

> 原文:[https://www . geesforgeks . org/字符串单词间的最小距离/](https://www.geeksforgeeks.org/minimum-distance-between-words-of-a-string/)

给定一个字符串 **s** 和两个出现在 s 中的单词 **w1** 和 **w2** ，任务是找到 **w1** 和 **w2** 之间的最小距离。这里，距离是第一个单词和第二个单词之间的步数或单词数。

**示例:**

> **输入:** s =“极客为极客贡献练习”，w1 =“极客”，w2 =“练习”
> **输出:1**
> w1 和 w2 最接近的出现只有一个字。
> 
> **输入:** s =“快褐快褐青蛙”，w1 =“快”，w2 =“青蛙”
> T3】输出: 2

一个简单的方法是考虑 w1 的每一次出现。对于 w1 的每次出现，找到最近的 w2 并跟踪最小距离。

## C++

```
// C++ program to find Minimum Distance
// Between Words of a String
#include <bits/stdc++.h>
#include <sstream>
using namespace std;

// Function to implement split function
void split(const string &s, char delimiter,
                     vector<string> &words)
{
    string token;
    stringstream tokenStream(s);

    while (getline(tokenStream, token, delimiter))
        words.push_back(token);
}

// Function to calculate the minimum
// distance between w1 and w2 in s
int distance(string s, string w1, string w2)
{
    if (w1 == w2)
        return 0;

    // get individual words in a list
    vector<string> words;
    split(s, ' ', words);

    // assume total length of the string
    // as minimum distance
    int min_dist = words.size() + 1;

    // traverse through the entire string
    for (int index = 0; index < words.size(); index++)
    {
        if (words[index] == w1)
        {
            for (int search = 0;
                     search < words.size(); search++)
            {
                if (words[search] == w2)
                {
                    // the distance between the words is
                    // the index of the first word - the
                    // current word index
                    int curr = abs(index - search) - 1;

                    // comparing current distance with
                    // the previously assumed distance
                    if (curr < min_dist)
                        min_dist = curr;
                }
            }
        }
    }

    // w1 and w2 are same and adjacent
    return min_dist;
}

// Driver Code
int main(int argc, char const *argv[])
{
    string s = "geeks for geeks contribute practice";
    string w1 = "geeks";
    string w2 = "practice";
    cout << distance(s, w1, w2) << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Minimum Distance
// Between Words of a String
 class solution
 {

// Function to calculate the minimum
// distance between w1 and w2 in s
static int distance(String s,String w1,String w2)
{

    if (w1 .equals( w2) )
        return 0 ;

    // get individual words in a list
    String words[] = s.split(" ");

    // assume total length of the string
    // as minimum distance
    int min_dist = (words.length) + 1;

    // traverse through the entire string
    for (int index = 0;
         index < words.length ; index ++)
    {

        if (words[index] .equals( w1))
        {
            for (int search = 0;
                 search < words.length; search ++)
            {
                if (words[search] .equals(w2))
                {
                    // the distance between the words is
                    // the index of the first word - the
                    // current word index
                    int curr = Math.abs(index - search) - 1;

                    // comparing current distance with
                    // the previously assumed distance
                    if (curr < min_dist)
                    {
                        min_dist = curr ;
                    }
                }
            }
        }
    }

    // w1 and w2 are same and adjacent
    return min_dist;
}

// Driver code
public static void main(String args[])
{

String s = "geeks for geeks contribute practice";
String w1 = "geeks" ;
String w2 = "practice" ;

System.out.print( distance(s, w1, w2) );

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# function to calculate the minimum
# distance between w1 and w2 in s

def distance(s, w1, w2):

    if w1 == w2 :
       return 0

    # get individual words in a list
    words = s.split(" ")

    # assume total length of the string as
    # minimum distance
    min_dist = len(words)+1

    # traverse through the entire string
    for index in range(len(words)):

        if words[index] == w1:
            for search in range(len(words)):

                if words[search] == w2:

                    # the distance between the words is
                    # the index of the first word - the
                    # current word index
                    curr = abs(index - search) - 1;

                    # comparing current distance with
                    # the previously assumed distance
                    if curr < min_dist:
                       min_dist = curr

    # w1 and w2 are same and adjacent
    return min_dist

# Driver code
s = "geeks for geeks contribute practice"
w1 = "geeks"
w2 = "practice"
print(distance(s, w1, w2))
```

## C#

```
// C# program to find Minimum Distance
// Between Words of a String

using System;
 class solution
 {

// Function to calculate the minimum
// distance between w1 and w2 in s
static int distance(string s,string w1,string w2)
{

    if (w1 .Equals( w2) )
        return 0 ;

    // get individual words in a list
    string[] words = s.Split(" ");

    // assume total length of the string
    // as minimum distance
    int min_dist = (words.Length) + 1;

    // traverse through the entire string
    for (int index = 0;
         index < words.Length ; index ++)
    {

        if (words[index] .Equals( w1))
        {
            for (int search = 0;
                 search < words.Length; search ++)
            {
                if (words[search] .Equals(w2))
                {
                    // the distance between the words is
                    // the index of the first word - the
                    // current word index
                    int curr = Math.Abs(index - search) - 1;

                    // comparing current distance with
                    // the previously assumed distance
                    if (curr < min_dist)
                    {
                        min_dist = curr ;
                    }
                }
            }
        }
    }

    // w1 and w2 are same and adjacent
    return min_dist;
}

// Driver code
public static void Main()
{

string s = "geeks for geeks contribute practice";
string w1 = "geeks" ;
string w2 = "practice" ;

Console.Write( distance(s, w1, w2) );

}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Minimum Distance
// Between Words of a String

// Function to calculate the minimum
// distance between w1 and w2 in s
function distance($s, $w1, $w2)
{

    if ($w1 == $w2 )
        return 0 ;

    // get individual words in a list
    $words = explode(" ", $s);

    // assume total length of the string
    // as minimum distance
    $min_dist = sizeof($words) + 1;

    // traverse through the entire string
    for ($index = 0;
         $index < sizeof($words) ; $index ++)
    {

        if ($words[$index] == $w1)
        {
            for ($search = 0;
                 $search < sizeof($words); $search ++)
            {
                if ($words[$search] == $w2)
                {
                    // the distance between the words is
                    // the index of the first word - the
                    // current word index
                    $curr = abs($index - $search) - 1;

                    // comparing current distance with
                    // the previously assumed distance
                    if ($curr < $min_dist)
                    {
                        $min_dist = $curr ;
                    }
                }
            }
        }
    }

    // w1 and w2 are same and adjacent
    return $min_dist;
}

// Driver code
$s = "geeks for geeks contribute practice";
$w1 = "geeks" ;
$w2 = "practice" ;

echo distance($s, $w1, $w2) ;

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript program to find Minimum Distance
// Between Words of a String

// Function to calculate the minimum
// distance between w1 and w2 in s
function distance(s,w1,w2) {
    if (w1 ==( w2) )
        return 0 ;

    // get individual words in a list
    let words = s.split(" ");

    // assume total length of the string
    // as minimum distance
    let min_dist = (words.length) + 1;

    // traverse through the entire string
    for (let index = 0;
         index < words.length ; index ++)
    {

        if (words[index] == ( w1))
        {
            for (let search = 0;
                 search < words.length; search ++)
            {
                if (words[search] == (w2))
                {
                    // the distance between the words is
                    // the index of the first word - the
                    // current word index
                    let curr = Math.abs(index - search) - 1;

                    // comparing current distance with
                    // the previously assumed distance
                    if (curr < min_dist)
                    {
                        min_dist = curr ;
                    }
                }
            }
        }
    }

    // w1 and w2 are same and adjacent
    return min_dist;
}

    // Driver code
    let s = "geeks for geeks contribute practice";
    let w1 = "geeks" ;
    let w2 = "practice" ;
    document.write( distance(s, w1, w2) );

// This code is contributed by rag2127
</script>
```

**Output:** 

```
1
```

一个**有效的解决方案**是找到任何元素的第一次出现，然后跟踪前一个元素和当前元素。如果它们不同，并且距离小于当前最小值，请更新最小值。

## C++

```
// C++ program to extract words from
// a string using stringstream
#include<bits/stdc++.h>
using namespace std;

int distance(string s, string w1, string w2)
{

  if (w1 == w2)
  {
    return 0;
  }

  vector<string> words;

  // Used to split string around spaces.
  istringstream ss(s);

  string word; // for storing each word

  // Traverse through all words
  // while loop till we get
  // strings to store in string word
  while (ss >> word)
  {
    words.push_back(word);
  }

  int n = words.size();

  // assume total length of the string as
  // minimum distance
  int min_dist = n + 1;

  // Find the first occurrence of any of the two
  // numbers (w1 or w2) and store the index of
  // this occurrence in prev
  int prev = 0, i = 0;

  for (i = 0; i < n; i++)
  {

    if (words[i] == w1 || (words[i] == w2))
    {
      prev = i;
      break;
    }
  }

  // Traverse after the first occurrence
  while (i < n)
  {
    if (words[i] == w1 || (words[i] == w2))
    {

      // If the current element matches with
      // any of the two then check if current
      // element and prev element are different
      // Also check if this value is smaller than
      // minimum distance so far
      if ((words[prev] != words[i]) &&
          (i - prev) < min_dist)
      {
        min_dist = i - prev - 1;
        prev = i;
      }
      else
      {
        prev = i;
      }
    }
    i += 1;

  }
  return min_dist;
}

// Driver code
int main()
{
  string s = "geeks for geeks contribute practice";
  string w1 = "geeks";
  string w2 = "practice";
  cout<<distance(s, w1, w2);
}

// This code is contributed by rutvik_56.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to extract words from
// a string using stringstream
class GFG {

    static int distance(String s, String w1, String w2) {

        if (w1.equals(w2)) {
            return 0;
        }

       // get individual words in a list
        String[] words = s.split(" ");
        int n = words.length;

        // assume total length of the string as
        // minimum distance
        int min_dist = n + 1;

        // Find the first occurrence of any of the two
        // numbers (w1 or w2) and store the index of
        // this occurrence in prev
        int prev = 0, i = 0;
        for (i = 0; i < n; i++) {

            if (words[i].equals(w1) || words[i].equals(w2)) {
                prev = i;
                break;
            }
        }
        // Traverse after the first occurrence
        while (i < n) {
            if (words[i].equals(w1) || words[i].equals(w2)) {

                // If the current element matches with
                // any of the two then check if current
                // element and prev element are different
                // Also check if this value is smaller than
                // minimum distance so far
                if ((!words[prev].equals(words[i])) && (i - prev) < min_dist) {
                    min_dist = i - prev - 1;
                    prev = i;
                } else {
                    prev = i;
                }

            }
            i += 1;

        }
        return min_dist;
    }
// Driver code

    public static void main(String[] args) {
        String s = "geeks for geeks contribute practice";
        String w1 = "geeks";
        String w2 = "practice";
        System.out.println(distance(s, w1, w2));
// This code is contributed by princiRaj1992
    }
}
```

## C#

```
// C# program to extract words from
// a string using stringstream
using System;

class GFG
{

    static int distance(String s, String w1, String w2)
    {

        if (w1.Equals(w2))
        {
            return 0;
        }

        // get individual words in a list
        String[] words = s.Split(" ");
        int n = words.Length;

        // assume total length of the string as
        // minimum distance
        int min_dist = n + 1;

        // Find the first occurrence of any of the two
        // numbers (w1 or w2) and store the index of
        // this occurrence in prev
        int prev = 0, i = 0;
        for (i = 0; i < n; i++)
        {

            if (words[i].Equals(w1) || words[i].Equals(w2))
            {
                prev = i;
                break;
            }
        }

        // Traverse after the first occurrence
        while (i < n)
        {
            if (words[i].Equals(w1) || words[i].Equals(w2))
            {

                // If the current element matches with
                // any of the two then check if current
                // element and prev element are different
                // Also check if this value is smaller than
                // minimum distance so far
                if ((!words[prev].Equals(words[i])) &&
                                (i - prev) < min_dist)
                {
                    min_dist = i - prev - 1;
                    prev = i;
                }
                else
                {
                    prev = i;
                }
            }
            i += 1;

        }
        return min_dist;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "geeks for geeks contribute practice";
        String w1 = "geeks";
        String w2 = "practice";
        Console.Write(distance(s, w1, w2));
    }
}

// This code is contributed by Mohit kumar 29
```

## 蟒蛇 3

```
# Python3 program to extract words from
# a string using stringstream

def distance(s, w1, w2):

    if w1 == w2 :
       return 0

    # get individual words in a list
    words = s.split(" ")
    n = len(words)

    # assume total length of the string as
    # minimum distance
    min_dist = n+1

    # Find the first occurrence of any of the two
    # numbers (w1 or w2) and store the index of
    # this occurrence in prev
    for i in range(n):

        if words[i] == w1 or words[i] == w2:
            prev = i
            break

    # Traverse after the first occurrence
    while i < n:
        if words[i] == w1 or words[i] == w2:

            # If the current element matches with
            # any of the two then check if current
            # element and prev element are different
            # Also check if this value is smaller than
            # minimum distance so far
            if words[prev] != words[i] and (i - prev) < min_dist :
                min_dist = i - prev - 1
                prev = i
            else:
                prev = i
        i += 1       

    return min_dist

# Driver code
s = "geeks for geeks contribute practice"
w1 = "geeks"
w2 = "practice"
print(distance(s, w1, w2))
```

## java 描述语言

```
<script>

// Javascript program to extract words from
// a string using stringstream

function distance(s,w1,w2)
{
    if (w1 == (w2))
    {
            return 0;
        }

       // get individual words in a list
        let words = s.split(" ");
        let n = words.length;

        // assume total length of the string as
        // minimum distance
        let min_dist = n + 1;

        // Find the first occurrence of any of the two
        // numbers (w1 or w2) and store the index of
        // this occurrence in prev
        let prev = 0, i = 0;
        for (i = 0; i < n; i++)
        {

            if (words[i] == (w1) || words[i] == (w2))
            {
                prev = i;
                break;
            }
        }
        // Traverse after the first occurrence
        while (i < n)
        {
            if (words[i] == (w1) || words[i] == (w2))
            {

                // If the current element matches with
                // any of the two then check if current
                // element and prev element are different
                // Also check if this value is smaller than
                // minimum distance so far
                if ((words[prev] != (words[i])) && (i - prev) < min_dist) {
                    min_dist = i - prev - 1;
                    prev = i;
                } else {
                    prev = i;
                }

            }
            i += 1;
        }
        return min_dist;
}

// Driver code
let s = "geeks for geeks contribute practice";
let w1 = "geeks";
let w2 = "practice";
document.write(distance(s, w1, w2));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1
```

一个有效的解决方案是将单词 1 的索引存储在(lastpos)变量中，如果单词 1 再次出现，那么我们更新(lastpos ),如果单词 1 没有出现，那么简单地找到单词 1 和单词 2 的索引的差异。

## C++

```
// C++ program to find Minimum Distance
// Between Words of a String
#include <bits/stdc++.h>
using namespace std;

int shortestDistance(vector<string> &s, string word1, string word2)
    {
         if(word1==word2) return  0;
        int ans = INT_MAX;
       //To store the lastposition of word1
        int lastPos = -1;
        for(int i = 0 ; i < s.size() ; i++)
        {
            if(s[i] == word1 || s[i] == word2)
            {
               //first occurrence of word1
                if(lastPos == -1)
                   lastPos = i;
                else
                {
                    //if word1 repeated again we store the last position of word1
                    if(s[lastPos]==s[i])
                     lastPos = i;
                    else
                    {
                      //find the difference of position of word1 and word2
                        ans = min(ans , (i-lastPos)-1);
                        lastPos = i;
                    }
                }
            }
        }
        return ans;
}
//Driver code
int main() {
    vector<string> s{"geeks", "for", "geeks", "contribute",
     "practice"};
     string w1 = "geeks";
    string w2 = "practice";

    cout<<shortestDistance(s, w1, w2)<<"\n";

    return 0;
}

```