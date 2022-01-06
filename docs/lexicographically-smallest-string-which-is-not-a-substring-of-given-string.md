# 不是给定字符串的子串的最小大小的字典最小字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小字符串不是给定字符串的子字符串/](https://www.geeksforgeeks.org/lexicographically-smallest-string-which-is-not-a-substring-of-given-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **s** ，任务是在 **S** 中找到不作为[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)存在的最小字符的[字典最小字符串](https://www.geeksforgeeks.org/lexicographically-smallest-string-possible-by-inserting-given-character/)。

**示例:**

> **输入:**S =“aabacdefghijklmnopqrstuvwxyz”
> **输出:** ad
> **解释:**来自[a-z]的所有单个数字串出现在给定的字符串中，在两个字符串中，字符串{aa，ab，ac}出现，但给定的字符串中不存在“ad”。
> 
> **输入:** S =【极客暴走族】
> T3】输出: a
> 
> **输入:**S = " ABCD "
> T3】输出: e

**方法:**问题可以使用 [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) (广度优先搜索)算法解决。按照[字典顺序](https://www.geeksforgeeks.org/sort-an-array-of-strings-lexicographically-based-on-prefix/)生成所有[字符串](https://www.geeksforgeeks.org/string-data-structure/)，并检查它在给定字符串中是否作为[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)存在。按照以下步骤解决问题:

*   初始化一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如**集合**来存储给定字符串 **s.** 的所有[子串](https://www.geeksforgeeks.org/substring-in-cpp/)
*   [迭代给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并将所有[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)存储到集合中。
*   初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，比如**字符串队列**，按照字典顺序生成[字符串](https://www.geeksforgeeks.org/string-data-structure/)。
*   最初，将从“ **a** 到“ **z** 的所有个位数[字符串](https://www.geeksforgeeks.org/string-data-structure/)推入[队列](https://www.geeksforgeeks.org/queue-data-structure/)。
*   [迭代而](https://www.geeksforgeeks.org/java-while-loop-with-examples/) [队列](https://www.geeksforgeeks.org/queue-data-structure/)不为空:
    *   对于队列前**的当前[字符串](https://www.geeksforgeeks.org/string-data-structure/)，检查它是否出现在给定的[字符串](https://www.geeksforgeeks.org/string-data-structure/)中。**
    *   如果出现在给定的[字符串](https://www.geeksforgeeks.org/string-data-structure/)中，则将所有字符从 **a** 单独追加到 **z** 中，并将其推回到[队列](https://www.geeksforgeeks.org/queue-data-structure/)中，否则打印当前的[字符串](https://www.geeksforgeeks.org/string-data-structure/)并**返回**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest string of minimum characters
// not present as substring in string S
void lexicographicalSmallestString(string& S, int n)
{
    // Set which stores all substrings
    // of the string S
    set<string> collection;

    // Constructing all substrings of S
    for (int i = 0; i < n; ++i) {
        string cur;
        for (int j = i; j < n; ++j) {
            cur.push_back(S[j]);

            // Inserting the current
            // substring to set
            collection.insert(cur);
        }
    }

    queue<string> q;

    // Initializing BFS queue
    for (int i = 0; i < 26; ++i) {
        q.push(string(1, i + 'a'));
    }

    // Loop for the BFS Traversal
    while (!q.empty()) {

        // Stores the current
        // lexicographically smallest
        // string of min characters
        auto cur = q.front();
        q.pop();

        // If the current string is
        // not present as a substring
        // of the given string
        if (collection.find(cur) == collection.end()) {

            // Print Answer
            cout << cur << endl;
            return;
        }

        // Append characters from [a-z]
        // to the back of string cur
        // and push into the queue.
        for (int i = 0; i < 26; ++i) {
            cur.push_back(i + 'a');
            q.push(cur);
            cur.pop_back();
        }
    }
}

// Driver Code
int main()
{
    string S = "aabacdefghijklmnopqrstuvwxyz";
    int N = S.length();

    lexicographicalSmallestString(S, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

// Function to find the lexicographically
// smallest String of minimum characters
// not present as subString in String S
static void lexicographicalSmallestString(char[] S, int n)
{

    // Set which stores all subStrings
    // of the String S
    HashSet<String> collection = new HashSet<String>();

    // Constructing all subStrings of S
    for (int i = 0; i < n; ++i) {
        String cur="";
        for (int j = i; j < n; ++j) {
            cur+=(S[j]);

            // Inserting the current
            // subString to set
            collection.add(cur);
        }
    }

    Queue<String> q = new LinkedList<String>();

    // Initializing BFS queue
    for (int i = 0; i < 26; ++i) {
        q.add(String.valueOf((char)((i + 'a'))));
    }

    // Loop for the BFS Traversal
    while (!q.isEmpty()) {

        // Stores the current
        // lexicographically smallest
        // String of min characters
        String cur = q.peek();
        q.remove();

        // If the current String is
        // not present as a subString
        // of the given String
        if (!collection.contains(cur)) {

            // Print Answer
            System.out.print(cur +"\n");
            return;
        }

        // Append characters from [a-z]
        // to the back of String cur
        // and push into the queue.
        for (int i = 0; i < 26; ++i) {
            cur+=String.valueOf((char)((i + 'a')));
            q.add(cur);
            cur=cur.substring(0,cur.length()-1);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    String S = "aabacdefghijklmnopqrstuvwxyz";
    int N = S.length();

    lexicographicalSmallestString(S.toCharArray(), N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python  implementation of the above approach
from queue import Queue

# Function to find the lexicographically
# smallest string of minimum characters
# not present as substring in string S
def lexicographicalSmallestString(S, n):

    # Set which stores all substrings
    # of the string S
    collection = set()

    # Constructing all substrings of S
    for i in range(0, n):
        cur = ""
        for j in range(i, n):
            cur += (S[j])

            # Inserting the current
            # substring to set
            collection.add(cur)

    q = Queue()

    # Initializing BFS queue
    for i in range(0, 26):
        q.put(chr(i + ord('a')))

    # Loop for the BFS Traversal
    while (not q.empty()):

        # Stores the current
        # lexicographically smallest
        # string of min characters
        cur = q.get()

        # If the current string is
        # not present as a substring
        # of the given string
        if (not (cur in collection)):

            # Print Answer
            print(cur)
            return

        # Append characters from [a-z]
        # to the back of string cur
        # and push into the queue.
        for i in range(0, 26):
            q.put((cur + chr(i+ord('a'))))

# Driver Code
if __name__ == "__main__":

    S = "aabacdefghijklmnopqrstuvwxyz"
    N = len(S)

    lexicographicalSmallestString(S, N)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Function to find the lexicographically
// smallest String of minimum characters
// not present as subString in String S
static void lexicographicalSmallestString(char[] S, int n)
{

    // Set which stores all subStrings
    // of the String S
    HashSet<String> collection = new HashSet<String>();

    // Constructing all subStrings of S
    for (int i = 0; i < n; ++i) {
        String cur = "";
        for (int j = i; j < n; ++j) {
            cur += (S[j]);

            // Inserting the current
            // subString to set
            collection.Add(cur);
        }
    }

    Queue<String> q = new Queue<String>();

    // Initializing BFS queue
    for (int i = 0; i < 26; ++i) {
        q.Enqueue(String.Join("",(char)((i + 'a'))));
    }

    // Loop for the BFS Traversal
    while (q.Count != 0) {

        // Stores the current
        // lexicographically smallest
        // String of min characters
        String cur = q.Peek();
        q.Dequeue();

        // If the current String is
        // not present as a subString
        // of the given String
        if (!collection.Contains(cur)) {

            // Print Answer
            Console.Write(cur +"\n");
            return;
        }

        // Append characters from [a-z]
        // to the back of String cur
        // and push into the queue.
        for (int i = 0; i < 26; ++i) {
            cur += String.Join("",(char)((i + 'a')));
            q.Enqueue(cur);
            cur=cur.Substring(0,cur.Length-1);
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    String S = "aabacdefghijklmnopqrstuvwxyz";
    int N = S.Length;

    lexicographicalSmallestString(S.ToCharArray(), N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
// Javascript implementation of the above approach

// Function to find the lexicographically
// smallest string of minimum characters
// not present as substring in string S
function lexicographicalSmallestString(S, n)
{   

    // Set which stores all substrings
    // of the string S
    let collection = new Set();

    // Constructing all substrings of S
    for (let i = 0; i < n; ++i) {
        let cur = ""
        for (let j = i; j < n; ++j) {
            cur += S[j];

            // Inserting the current
            // substring to set
            collection.add(cur);
        }
    }

    let q = [];

    // Initializing BFS queue
    for (let i = 0; i < 26; ++i) {
        q.push(String.fromCharCode('a'.charCodeAt(0) + i));
    }

    // Loop for the BFS Traversal
    while (q.length) {

        // Stores the current
        // lexicographically smallest
        // string of min characters
        let cur = q[0];
        q.shift();

        // If the current string is
        // not present as a substring
        // of the given string
        if (!collection.has(cur)) {

            // Print Answer
            document.write(cur + '<br>');
            return;
        }

        // Append characters from [a-z]
        // to the back of string cur
        // and push into the queue.
        for (let i = 0; i < 26; ++i) {
            q.push(cur + (String.fromCharCode(i + 'a'.charCodeAt(0))));
        }
    }
}

// Driver Code

let S = "aabacdefghijklmnopqrstuvwxyz";
let N = S.length;

lexicographicalSmallestString(S, N);

// This code is contributed by gfgking.
```

**Output**

```
ad
```

***时间复杂度:**O(N<sup>2</sup>* log N)*
***辅助空间:** O(N <sup>2</sup> )*