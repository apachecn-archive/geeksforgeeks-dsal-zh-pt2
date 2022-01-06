# 使用回文树的最长回文子串|集合 3

> 原文:[https://www . geesforgeks . org/long-回文-substring-use-回文-tree-set-3/](https://www.geeksforgeeks.org/longest-palindromic-substring-using-palindromic-tree-set-3/)

给定一个字符串，找出最长的子字符串，即回文。例如，如果给定的字符串是“forgeeksskeegfor”，则输出应该是“geeksskeeg”。

**先决条件:** [回文树](https://www.geeksforgeeks.org/palindromic-tree-introduction-implementation/) | [最长回文子串](https://www.geeksforgeeks.org/longest-palindrome-substring-set-1/)

**回文树的结构:**
回文树的实际结构接近有向图。它实际上是两个共享一些公共节点的树的合并结构(为了更好地理解，请参见下图)。树节点通过存储它们的索引来存储给定字符串的回文子串。
此树由两种边组成:
1。插入边(加权边)
2。最大回文后缀(未加权)

**插入边:**
从节点 u 到具有一定权重 x 的 v 的插入边意味着节点 v 是通过在 u 处的字符串的前端和末端插入 x 而形成的。由于“u”已经是回文，因此节点 v 处的结果字符串也将是回文。x 将是每个边的单个字符。因此，一个节点最多可以有 26 条插入边(考虑小写字母字符串)。
**最大回文后缀边:**
顾名思义，对于一个节点，这条边将指向它的最大回文后缀字符串节点。我们不会将整个字符串本身视为最大回文后缀，因为这没有意义(自循环)。为了简单起见，我们将它称为后缀边(除了完整的字符串之外，我们指的是最大后缀)。很明显，每个节点只有 1 个后缀边，因为我们不会在树中存储重复的字符串。
我们将创建所有的回文子串，然后返回我们得到的最后一个，因为这将是迄今为止最长的回文子串。
因为回文树按照某个字符的到达顺序存储回文，所以最长的总是在我们树数组的最后一个索引处。
**以下是上述方法的实施:**

## C++

```
// CPP code for Longest Palindromic substring
// using Palindromic Tree data structure
#include <bits/stdc++.h>
using namespace std;

#define MAXN  1000

struct Node
{
    // store start and end indexes of current
    // Node inclusively
    int start, end;

    // stores length of substring
    int length;

    // stores insertion Node for all characters a-z
    int insertionEdge[26];

    // stores the Maximum Palindromic Suffix Node for
    // the current Node
    int suffixEdge;
};

// two special dummy Nodes as explained above
Node root1, root2;

// stores Node information for constant time access
Node tree[MAXN];

// Keeps track the current Node while insertion
int currNode;
string s;
int ptr;

// Function to insert edge in tree
void insert(int currIndex)
{
    // Finding X, such that s[currIndex]
    // + X + s[currIndex] is palindrome.
    int temp = currNode;

    while (true)
    {
        int currLength = tree[temp].length;
        if (currIndex - currLength >= 1 &&
            (s[currIndex] == s[currIndex -
             currLength - 1]))
                        break;

        temp = tree[temp].suffixEdge;
    }

    // Check if s[currIndex] + X +
    // s[currIndex] is already Present in tree.
    if (tree[temp].insertionEdge[s[currIndex] -
        'a'] != 0)
    {
        currNode =
        tree[temp].insertionEdge[s[currIndex]
                   - 'a'];

        return;
    }

    // Else Create new node;
    ptr++;

    tree[temp].insertionEdge[s[currIndex]
               - 'a'] = ptr;

    tree[ptr].end = currIndex;

    tree[ptr].length = tree[temp].length + 2;

    tree[ptr].start = tree[ptr].end -
                      tree[ptr].length + 1;

    // Setting suffix edge for newly Created Node.

    currNode = ptr;
    temp = tree[temp].suffixEdge;

    // Longest Palindromic suffix for a
    // string of length 1 is a Null string.
    if (tree[currNode].length == 1) {
        tree[currNode].suffixEdge = 2;
        return;
    }

    // Else
    while (true) {
        int currLength = tree[temp].length;

        if (currIndex - currLength >= 1 &&
            (s[currIndex] ==
             s[currIndex - currLength - 1]))
                break;

        temp = tree[temp].suffixEdge;
    }

    tree[currNode].suffixEdge =
        tree[temp].insertionEdge[s[currIndex] - 'a'];
}

// Driver code
int main()
{
    // Imaginary root's suffix edge points to
    // itself, since for an imaginary string
    // of length = -1 has an imaginary suffix
    // string. Imaginary root.
    root1.length = -1;
    root1.suffixEdge = 1;

    // NULL root's suffix edge points to
    // Imaginary root, since for a string
    // of length = 0 has an imaginary suffix string.
    root2.length = 0;
    root2.suffixEdge = 1;

    tree[1] = root1;
    tree[2] = root2;

    ptr = 2;
    currNode = 1;
    s = "forgeeksskeegfor";
    for (int i = 0; i < s.size(); i++)
            insert(i);

    // last will be the index of our last substring
    int last = ptr;

    for (int i = tree[last].start;
         i <= tree[last].end; i++)
                cout << s[i];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code for Longest Palindromic subString 
// using Palindromic Tree data structure 
class GFG 
{

    static final int MAXN = 1000;

    static class Node
    {
        // store start and end indexes of current
        // Node inclusively
        int start, end;

        // stores length of subString
        int length;

        // stores insertion Node for all characters a-z
        int[] insertionEdge = new int[26];

        // stores the Maximum Palindromic Suffix Node for
        // the current Node
        int suffixEdge;
    };

    // two special dummy Nodes as explained above
    static Node root1, root2;

    // stores Node information for constant time access
    static Node[] tree = new Node[MAXN];

    // Keeps track the current Node while insertion
    static int currNode;
    static char[] s;
    static int ptr;

    // Function to insert edge in tree
    static void insert(int currIndex)
    {
        // Finding X, such that s[currIndex]
        // + X + s[currIndex] is palindrome.
        int temp = currNode;

        while (true) {
            int currLength = tree[temp].length;
            if (currIndex - currLength >= 1 && 
                (s[currIndex] == s[currIndex - currLength - 1]))
                break;

            temp = tree[temp].suffixEdge;
        }

        // Check if s[currIndex] + X +
        // s[currIndex] is already Present in tree.
        if (tree[temp].insertionEdge[s[currIndex] - 'a'] != 0)
        {
            currNode = tree[temp].insertionEdge[s[currIndex] - 'a'];

            return;
        }

        // Else Create new node;
        ptr++;

        tree[temp].insertionEdge[s[currIndex] - 'a'] = ptr;

        tree[ptr].end = currIndex;

        tree[ptr].length = tree[temp].length + 2;

        tree[ptr].start = tree[ptr].end - tree[ptr].length + 1;

        // Setting suffix edge for newly Created Node.

        currNode = ptr;
        temp = tree[temp].suffixEdge;

        // Longest Palindromic suffix for a
        // String of length 1 is a Null String.
        if (tree[currNode].length == 1)
        {
            tree[currNode].suffixEdge = 2;
            return;
        }

        // Else
        while (true)
        {
            int currLength = tree[temp].length;

            if (currIndex - currLength >= 1 && 
                (s[currIndex] == s[currIndex - currLength - 1]))
                break;

            temp = tree[temp].suffixEdge;
        }

        tree[currNode].suffixEdge = 
        tree[temp].insertionEdge[s[currIndex] - 'a'];
    }

    // Driver code
    public static void main(String[] args) 
    {
        // Imaginary root's suffix edge points to
        // itself, since for an imaginary String
        // of length = -1 has an imaginary suffix
        // String. Imaginary root.
        root1 = new Node();
        root1.length = -1;
        root1.suffixEdge = 1;

        // null root's suffix edge points to
        // Imaginary root, since for a String
        // of length = 0 has an imaginary suffix String.
        root2 = new Node();
        root2.length = 0;
        root2.suffixEdge = 1;
        for (int i = 0; i < MAXN; i++)
            tree[i] = new Node();
        tree[1] = root1;
        tree[2] = root2;

        ptr = 2;
        currNode = 1;
        s = "forgeeksskeegfor".toCharArray();
        for (int i = 0; i < s.length; i++)
            insert(i);

        // last will be the index of our last subString
        int last = ptr;

        for (int i = tree[last].start; i <= tree[last].end; i++)
            System.out.print(s[i]);

    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code for Longest Palindromic 
# substring using Palindromic Tree 
# data structure 

class Node: 

    def __init__(self, length = None, 
                       suffixEdge = None):

        # store start and end indexes 
        # of current Node inclusively 
        self.start = None
        self.end = None

        # Stores length of substring 
        self.length = length 

        # stores insertion Node for all
        # characters a-z 
        self.insertionEdge = [0] * 26

        # stores the Maximum Palindromic 
        # Suffix Node for the current Node 
        self.suffixEdge = suffixEdge 

# Function to insert edge in tree 
def insert(currIndex): 

    global currNode, ptr

    # Finding X, such that s[currIndex] 
    # + X + s[currIndex] is palindrome. 
    temp = currNode 

    while True: 

        currLength = tree[temp].length 
        if (currIndex - currLength >= 1 and
           (s[currIndex] == s[currIndex -
            currLength - 1])): 
            break

        temp = tree[temp].suffixEdge 

    # Check if s[currIndex] + X + 
    # s[currIndex] is already Present in tree. 
    if tree[temp].insertionEdge[ord(s[currIndex]) - 
                                ord('a')] != 0: 

        currNode = tree[temp].insertionEdge[ord(s[currIndex]) - 
                                            ord('a')] 
        return

    # Else Create new node 
    ptr += 1

    tree[temp].insertionEdge[ord(s[currIndex]) - 
                             ord('a')] = ptr 

    tree[ptr].end = currIndex 

    tree[ptr].length = tree[temp].length + 2

    tree[ptr].start = (tree[ptr].end - 
                       tree[ptr].length + 1)

    # Setting suffix edge for newly Created Node. 
    currNode = ptr 
    temp = tree[temp].suffixEdge 

    # Longest Palindromic suffix for a 
    # string of length 1 is a Null string. 
    if tree[currNode].length == 1: 
        tree[currNode].suffixEdge = 2
        return

    # Else 
    while True: 
        currLength = tree[temp].length 

        if (currIndex - currLength >= 1 and
            s[currIndex] == s[currIndex - 
                              currLength - 1]): 
            break

        temp = tree[temp].suffixEdge 

    tree[currNode].suffixEdge = \
    tree[temp].insertionEdge[ord(s[currIndex]) - ord('a')] 

# Driver code 
if __name__ == "__main__":

    MAXN = 1000

    # Imaginary root's suffix edge points to 
    # itself, since for an imaginary string 
    # of length = -1 has an imaginary suffix 
    # string. Imaginary root.
    root1 = Node(-1, 1) 

    # NULL root's suffix edge points to 
    # Imaginary root, since for a string of 
    # length = 0 has an imaginary suffix string. 
    root2 = Node(0, 1)

    # Stores Node information for 
    # constant time access 
    tree = [Node() for i in range(MAXN)] 

    # Keeps track the Current Node 
    # while insertion 
    currNode, ptr = 1, 2

    tree[1] = root1 
    tree[2] = root2 

    s = "forgeeksskeegfor"
    for i in range(0, len(s)): 
        insert(i) 

    # last will be the index of our
    # last substring 
    last = ptr 
    for i in range(tree[last].start,
                   tree[last].end + 1): 
        print(s[i], end = "") 

# This code is contributed by Rituraj Jain
```

## C#

```
// C# code for longest Palindromic subString 
// using Palindromic Tree data structure 
using System;

class GFG 
{

    static readonly int MAXN = 1000;

    class Node
    {
        // store start and end indexes of current
        // Node inclusively
        public int start, end;

        // stores length of subString
        public int Length;

        // stores insertion Node for all characters a-z
        public int[] insertionEdge = new int[26];

        // stores the Maximum Palindromic Suffix Node for
        // the current Node
        public int suffixEdge;
    };

    // two special dummy Nodes as explained above
    static Node root1, root2;

    // stores Node information for constant time access
    static Node[] tree = new Node[MAXN];

    // Keeps track the current Node while insertion
    static int currNode;
    static char[] s;
    static int ptr;

    // Function to insert edge in tree
    static void insert(int currIndex)
    {
        // Finding X, such that s[currIndex]
        // + X + s[currIndex] is palindrome.
        int temp = currNode;

        while (true)
        {
            int currLength = tree[temp].Length;
            if (currIndex - currLength >= 1 && 
                (s[currIndex] == s[currIndex - currLength - 1]))
                break;

            temp = tree[temp].suffixEdge;
        }

        // Check if s[currIndex] + X +
        // s[currIndex] is already Present in tree.
        if (tree[temp].insertionEdge[s[currIndex] - 'a'] != 0)
        {
            currNode = tree[temp].insertionEdge[s[currIndex] - 'a'];

            return;
        }

        // Else Create new node;
        ptr++;

        tree[temp].insertionEdge[s[currIndex] - 'a'] = ptr;

        tree[ptr].end = currIndex;

        tree[ptr].Length = tree[temp].Length + 2;

        tree[ptr].start = tree[ptr].end - tree[ptr].Length + 1;

        // Setting suffix edge for newly Created Node.
        currNode = ptr;
        temp = tree[temp].suffixEdge;

        // longest Palindromic suffix for a
        // String of length 1 is a Null String.
        if (tree[currNode].Length == 1)
        {
            tree[currNode].suffixEdge = 2;
            return;
        }

        // Else
        while (true)
        {
            int currLength = tree[temp].Length;

            if (currIndex - currLength >= 1 && 
                (s[currIndex] == s[currIndex - currLength - 1]))
                break;

            temp = tree[temp].suffixEdge;
        }

        tree[currNode].suffixEdge = 
        tree[temp].insertionEdge[s[currIndex] - 'a'];
    }

    // Driver code
    public static void Main(String[] args) 
    {
        // Imaginary root's suffix edge points to
        // itself, since for an imaginary String
        // of length = -1 has an imaginary suffix
        // String. Imaginary root.
        root1 = new Node();
        root1.Length = -1;
        root1.suffixEdge = 1;

        // null root's suffix edge points to
        // Imaginary root, since for a String
        // of length = 0 has an imaginary suffix String.
        root2 = new Node();
        root2.Length = 0;
        root2.suffixEdge = 1;
        for (int i = 0; i < MAXN; i++)
            tree[i] = new Node();
        tree[1] = root1;
        tree[2] = root2;

        ptr = 2;
        currNode = 1;
        s = "forgeeksskeegfor".ToCharArray();
        for (int i = 0; i < s.Length; i++)
            insert(i);

        // last will be the index of our last subString
        int last = ptr;

        for (int i = tree[last].start; i <= tree[last].end; i++)
            Console.Write(s[i]);

    }
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
geeksskeeg

```