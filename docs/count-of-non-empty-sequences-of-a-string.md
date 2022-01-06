# 字符串的非空序列计数

> 原文:[https://www . geesforgeks . org/非空字符串序列计数/](https://www.geeksforgeeks.org/count-of-non-empty-sequences-of-a-string/)

给定一个字符串 s，任务是找到可能的非空字母序列的数量。
**例:**

```
Input: "AAB"
Output: 8 
Explanation:
1) A
2) AA
3) AAB
4) AB
5) ABA
6) B
7) BA
8) BAA
Total 8 possibilities

Input: "AAABBC"
Output: 188
```

**进场:**有两种可能要么把当前角色带到我们的答案，要么离开。我们可以解决这个问题
为了检查重复，我们可以将集合作为一个数据结构，并将我们的答案放在那里，我们的计数将是集合的大小。
以下是上述办法的实施:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function which will
// calculate all the possibilities
// recursively
void recurr(string& tiles, vector<bool> vis, string ans,
            set<string>& se)
{
    if (ans.size() > 0) {
        // Check that the string
        // is already there or not
        if (se.count(ans))
            return;
        // Else put in set
        se.insert(ans);
    }
    // Run for all the
    // possibilities
    for (int i = 0; i < tiles.size(); i++) {
        // If already taken
        // then don't do anything
        if (vis[i])
            continue;
        vis[i] = true;
        // Else take it and
        // call recurr function
        recurr(tiles, vis, ans + tiles[i], se);
        vis[i] = false;
    }
}

// Driver code
int main()
{

    string s = "AAABBC";
    string curr = "";

    set<string> se;
    vector<bool> vis(s.size(), false);
    recurr(s, vis, curr, se);

    int ans = se.size();
    cout << ans << '\n';

    // uncomment following to print all generated strings
    /*
    for(auto i: se)
            cout<<i<<endl;
    */

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    static HashSet<String> se = new HashSet<String>();
    static String tiles;

    // Recursive function which will
    // calculate all the possibilities
    // recursively
    static void recurr(Vector<Boolean> vis, String ans)
    {

        // Check that the string
        // is already there or not
        if(ans.length()>0)
        {
            if(se.contains(ans))
            {
                return;
            }

            // Else put in set
            se.add(ans);
        }

        // Run for all the
        // possibilities
        for(int i = 0; i < tiles.length(); i++)
        {
            // If already taken
            // then don't do anything
            if (vis.get(i))
                continue;
            vis.set(i, true);

            // Else take it and
            //call recurr function
            recurr(vis, ans + tiles.charAt(i));
            vis.set(i, false);
        }
    }

    public static void main(String[] args)
    {
        tiles = "AAABBC";
        String curr = "";

        Vector<Boolean> vis = new Vector<Boolean>();
        for(int i = 0; i < tiles.length(); i++)
        {
            vis.add(false);
        }

        recurr(vis, curr);
        System.out.print(se.size());
    }
}

// This code is contributed by rameshtravel07.
```

## 计算机编程语言

```
# Python3 program for
# the above approach

# Recursive function which will
# calculate all the possibilities
# recursively

def recurr(vis, ans):
    global tiles, se
    if (len(ans) > 0):

        # Check that the string
        # is already there or not
        if (ans in se):
            return

        # Else put in set
        se[ans] = 1

    # Run for all the
    # possibilities
    for i in range(len(tiles)):

        # If already taken
        # then don't do anything
        if (vis[i]):
            continue
        vis[i] = True

        # Else take it and
        # call recurr function
        recurr(vis, ans + tiles[i])
        vis[i] = False

# Driver code
tiles = "AAABBC"
curr = ""

se = dict()
vis = [False] * (len(tiles))
recurr(vis, curr)
print(len(se))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    static HashSet<string> se = new HashSet<string>();
    static string tiles;

    // Recursive function which will
    // calculate all the possibilities
    // recursively
    static void recurr(List<bool> vis, string ans)
    {

        // Check that the string
        // is already there or not
        if(ans.Length>0)
        {
            if(se.Contains(ans))
            {
                return;
            }

            // Else put in set
            se.Add(ans);
        }

        // Run for all the
        // possibilities
        for(int i = 0; i < tiles.Length; i++)
        {
            // If already taken
            // then don't do anything
            if (vis[i])
                continue;
            vis[i] = true;

            // Else take it and
            //call recurr function
            recurr(vis, ans + tiles[i]);
            vis[i] = false;
        }
    }

  static void Main() {
    tiles = "AAABBC";
    string curr = "";

    List<bool> vis = new List<bool>();
    for(int i = 0; i < tiles.Length; i++)
    {
        vis.Add(false);
    }

    recurr(vis, curr);
    Console.WriteLine(se.Count);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// Javascript program for
// the above approach

// Recursive function which will
// calculate all the possibilities
// recursively

function recurr(vis, ans)
{

    // Check that the string
    // is already there or not
    if(ans.length>0)
    {
        if(se.has(ans))
        {
            return;
        }

        // Else put in set
        se.add(ans);
    }
    // Run for all the
    // possibilities
    for(let i=0;i<tiles.length;i++)
    {
        // If already taken
        // then don't do anything
        if (vis[i])
            continue;
        vis[i] = true;

        // Else take it and
        //call recurr function
        recurr(vis, ans + tiles[i]);
        vis[i] = false;
    }
}

// Driver code

let tiles = "AAABBC";
let curr = "";

let se = new Set();
let vis = new Array(tiles.length);
for(let i = 0; i < tiles.length; i++)
{
    vis[i] = false;
}

recurr(vis, curr);
document.write(se.size);

// This code is contributed by ab2127
</script>
```

**Output**

```
188
```

**另一种方法:**想法是保持字符串中字符的频率，然后通过选择字符串中的每个字符将计数增加 1 并减少频率，[递归地](https://www.geeksforgeeks.org/recursion/)调用字符的其余频率。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count
// of the number of strings
void countNumberOfStringsUtil(
    vector<int>& freq, int& count)
{
    // Loop to iterate over the
    // frequency of character of string
    for (int i = 0; i < 26; i++) {
        if (freq[i] > 0) {
            // reduce the frequency of
            // current element
            freq[i]--;
            count++;

            // recursive call
            countNumberOfStringsUtil(freq,count);
            freq[i]++; // backtrack
        }
    }
}

// Function to count the number of
// non-empty sequences
int countNumberOfStrings(string s) {
    // store the frequency of each character
    vector<int> freq(26, 0);

    // Maintain the frequency
    for (int i = 0; i < s.size(); i++) {
        freq[s[i] - 'A']++;
    }

    int count = 0;
    countNumberOfStringsUtil(freq, count);

    return count;
}

// Driver Code
int main()
{

    string s = "AAABBC";

    // Function Call
    cout << countNumberOfStrings(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.io.*;
import java.util.*;

class GFG
{
  public static int count = 0;

  // Function to find the count
  // of the number of strings
  public static void countNumberOfStringsUtil(int[] freq)
  {

    // Loop to iterate over the
    // frequency of character of string
    for(int i = 0; i < 26; i++)
    {
      if(freq[i] > 0)
      {

        // reduce the frequency of
        // current element
        freq[i]--;
        count++;

        // recursive call
        countNumberOfStringsUtil(freq);
        freq[i]++;// backtrack
      }
    }       
  }

  // Function to count the number of
  // non-empty sequences
  public static int countNumberOfStrings(String s)
  {

    // store the frequency of each character
    int[] freq = new int[26];
    Arrays.fill(freq, 0);

    // Maintain the frequency
    for(int i = 0; i < s.length(); i++)
    {
      freq[s.charAt(i) - 'A']++;
    }

    countNumberOfStringsUtil(freq);
    return count;
  }

  // Driver Code
  public static void main (String[] args)
  {
    String s = "AAABBC";

    // Function Call
    System.out.println(countNumberOfStrings(s));
  }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
count = 0

# Function to find the count
# of the number of strings
def countNumberOfStringsUtil(freq,
                             Count):
    global count
    count = Count

    # Loop to iterate over the
    # frequency of character of string
    for i in range(26):
        if(freq[i] > 0):

            # Reduce the frequency of
            # current element
            freq[i] -= 1
            count+=1

            # Recursive call
            countNumberOfStringsUtil(freq,
                                     count);
            # Backtrack
            freq[i] += 1

# Function to count the number of
# non-empty sequences
def countNumberOfStrings(s):

    global count
    global freq

    # store the frequency
    # of each character
    freq = [0 for i in range(26)]

    # Maintain the frequency
    for i in range(len(s)):
        freq[ord(s[i]) -
             ord('A')] += 1

    countNumberOfStringsUtil(freq,
                             count);
    return count

# Driver Code
s = "AAABBC"

# Function Call
print(countNumberOfStrings(s))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections.Generic;
class GFG {

   static int count = 0;

  // Function to find the count
  // of the number of strings
  static void countNumberOfStringsUtil(int[] freq)
  {

    // Loop to iterate over the
    // frequency of character of string
    for(int i = 0; i < 26; i++)
    {
      if(freq[i] > 0)
      {

        // reduce the frequency of
        // current element
        freq[i]--;
        count++;

        // recursive call
        countNumberOfStringsUtil(freq);
        freq[i]++;// backtrack
      }
    }      
  }

  // Function to count the number of
  // non-empty sequences
  public static int countNumberOfStrings(string s)
  {

    // store the frequency of each character
    int[] freq = new int[26];
    Array.Fill(freq, 0);

    // Maintain the frequency
    for(int i = 0; i < s.Length; i++)
    {
      freq[s[i] - 'A']++;
    }

    countNumberOfStringsUtil(freq);
    return count;
  }

  static void Main() {
    string s = "AAABBC";

    // Function Call
    Console.Write(countNumberOfStrings(s));
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach
let count = 0;

// Function to find the count
  // of the number of strings
function countNumberOfStringsUtil(freq)
{
    // Loop to iterate over the
    // frequency of character of string
    for(let i = 0; i < 26; i++)
    {
      if(freq[i] > 0)
      {

        // reduce the frequency of
        // current element
        freq[i]--;
        count++;

        // recursive call
        countNumberOfStringsUtil(freq);
        freq[i]++;// backtrack
      }
    }      
}

// Function to count the number of
  // non-empty sequences
function countNumberOfStrings(s)
{

    // store the frequency of each character
    let freq = new Array(26);
    for(let i = 0; i < freq.length; i++)
    {   
        freq[i] = 0;
    }

    // Maintain the frequency
    for(let i = 0; i < s.length; i++)
    {
      freq[s[i].charCodeAt(0) - 'A'.charCodeAt(0)]++;
    }

    countNumberOfStringsUtil(freq);
    return count;
}

// Driver Code
let s = "AAABBC";

// Function Call
document.write(countNumberOfStrings(s));

// This code is contributed by unknown2108
</script>
```

**Output**

```
188
```