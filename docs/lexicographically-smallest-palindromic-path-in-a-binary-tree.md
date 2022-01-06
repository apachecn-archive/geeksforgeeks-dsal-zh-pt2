# 二叉树中字典最小的回文路径

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列-最小-回文-二叉树中的路径/](https://www.geeksforgeeks.org/lexicographically-smallest-palindromic-path-in-a-binary-tree/)

给定一棵[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，每个节点代表一个字母表，任务是找到字典上最小的回文[根到叶路径](https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/)。如果不存在回文路径，打印**“不存在回文路径”**。

**示例:**

> **输入:**
> a
> /\
> c b
> /\/\
> a g b x
> \
> a
> **输出:**
> abba
> ***解释:***
> 总共有 4 条根到叶路径，其中 2 条路径(即“aca”和“abba”)是回文路径，但由于“abba”在词典上较小
> 
> **输入:**
> a
> /\
> z k
> /\/\
> s e k u
> \
> e
> **输出:**
> 不存在回文路径

**方法:**按照步骤解决问题

1.  主要思想是使用[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)
2.  以预定的方式遍历树。
3.  继续将节点值存储在字符串中。
4.  一旦到达叶节点，检查从根到叶路径形成的字符串是否是回文 。
5.  如果它是回文，只有当它是[](https://www.geeksforgeeks.org/compare-two-strings-lexicographically-in-java/)****最小的回文路径**时，才将其存储在变量中。**
6.  **打印回文，如果它存在。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program
// for the above approach

#include <bits/stdc++.h>
using namespace std;

// Struct binary tree node
struct Node {
    char data;
    Node *left, *right;
};

// Function to create a new node
Node* newNode(char data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Function to check if the
// string is palindrome or not
bool checkPalindrome(string s)
{
    int low = 0, high = (int)s.size() - 1;

    while (low < high) {

        if (s[low] != s[high])
            return false;

        low++;
        high--;
    }

    return true;
}

// Function to find the lexicographically
// smallest palindromic path in the Binary Tree
void lexicographicallySmall(Node* root, string s,
                            string& finalAns)
{
    // Base case
    if (root == NULL)
        return;

    // Append current node's
    // data to the string
    s += root->data;

    // Check if a node is leaf or not
    if (!root->left and !root->right) {

        if (checkPalindrome(s)) {

            // Check for the 1st
            // Palindromic Path
            if (finalAns == "{content}quot;)
                finalAns = s;

            // Store lexicographically the
            // smallest palindromic path
            else
                finalAns = min(finalAns, s);
        }

        return;
    }

    // Recursively traverse left subtree
    lexicographicallySmall(root->left,
                           s, finalAns);

    // Recursively traverse right subtree
    lexicographicallySmall(root->right,
                           s, finalAns);
}

// Function to get smallest
// lexographical palindromic
// path
void getPalindromePath(Node* root)
{
    // Variable which stores
    // the final result
    string finalAns = "{content}quot;;

    // Function call to compute
    // lexicographically smallest
    // palindromic Path
    lexicographicallySmall(root, "",
                           finalAns);

    if (finalAns == "{content}quot;)
        cout << "No Palindromic Path exists";

    else
        cout << finalAns;
}
// Driver Code
int main()
{
    // Construct binary tree
    Node* root = newNode('a');
    root->left = newNode('c');
    root->left->left = newNode('a');
    root->left->right = newNode('g');
    root->right = newNode('b');
    root->right->left = newNode('b');
    root->right->right = newNode('x');
    root->right->left->right = newNode('a');

    getPalindromePath(root);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program
// for the above approach
import java.util.*;
class GFG
{
static String finalAns="";

// Struct binary tree node
static class Node
{
    char data;
    Node left, right;
};

// Function to create a new node
static Node newNode(char data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to check if the
// String is palindrome or not
static boolean checkPalindrome(String s)
{
    int low = 0, high = (int)s.length() - 1;
    while (low < high)
    {
        if (s.charAt(low) != s.charAt(high))
            return false;
        low++;
        high--;
    }
    return true;
}

// Function to find the lexicographically
// smallest palindromic path in the Binary Tree
static void lexicographicallySmall(Node root, String s)
{

    // Base case
    if (root == null)
        return;

    // Append current node's
    // data to the String
    s += root.data;

    // Check if a node is leaf or not
    if (root.left == null && root.right == null)
    {
        if (checkPalindrome(s))
        {

            // Check for the 1st
            // Palindromic Path
            if (finalAns == "{content}quot;)
                finalAns = s;

            // Store lexicographically the
            // smallest palindromic path
            else
                finalAns = finalAns.compareTo(s) <= 0 ? finalAns:s;
        }
        return;
    }

    // Recursively traverse left subtree
    lexicographicallySmall(root.left,
                           s);

    // Recursively traverse right subtree
    lexicographicallySmall(root.right,
                           s);
}

// Function to get smallest
// lexographical palindromic
// path
static void getPalindromePath(Node root)
{

    // Variable which stores
    // the final result
    finalAns = "{content}quot;;

    // Function call to compute
    // lexicographically smallest
    // palindromic Path
    lexicographicallySmall(root, "");
    if (finalAns == "{content}quot;)
        System.out.print("No Palindromic Path exists");
    else
        System.out.print(finalAns);
}

// Driver Code
public static void main(String[] args)
{

    // Conbinary tree
    Node root = newNode('a');
    root.left = newNode('c');
    root.left.left = newNode('a');
    root.left.right = newNode('g');
    root.right = newNode('b');
    root.right.left = newNode('b');
    root.right.right = newNode('x');
    root.right.left.right = newNode('a');
    getPalindromePath(root);
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program
# for the above approach

# Struct binary tree node
class Node:
    def __init__(self, d):
        self.data = d
        self.left = None
        self.right = None

# Function to check if the
# is palindrome or not
def checkPalindrome(s):
    low, high = 0, len(s) - 1
    while (low < high):
        if (s[low] != s[high]):
            return False
        low += 1
        high -= 1
    return True

# Function to find the lexicographically
# smallest palindromic path in the Binary Tree
def lexicographicallySmall(root, s):
    global finalAns

    # Base case
    if (root == None):
        return

    # Append current node's
    # data to the string
    s += root.data

    # Check if a node is leaf or not
    if (not root.left and not root.right):
        if (checkPalindrome(s)):

            # Check for the 1st
            # Palindromic Path
            if (finalAns == "{content}quot;):
                finalAns = s

            # Store lexicographically the
            # smallest palindromic path
            else:
                finalAns = min(finalAns, s)
        return

    # Recursively traverse left subtree
    lexicographicallySmall(root.left, s)

    # Recursively traverse right subtree
    lexicographicallySmall(root.right, s)

# Function to get smallest
# lexographical palindromic
# path
def getPalindromePath(root):
    global finalAns

    # Variable which stores
    # the final result
    finalAns = "{content}quot;

    # Function call to compute
    # lexicographically smallest
    # palindromic Path
    lexicographicallySmall(root, "")
    if (finalAns == "{content}quot;):
        print("No Palindromic Path exists")
    else:
        print(finalAns)

        # Driver Code
if __name__ == '__main__':
    finalAns = ""

    # Construct binary tree
    root = Node('a')
    root.left = Node('c')
    root.left.left = Node('a')
    root.left.right = Node('g')
    root.right = Node('b')
    root.right.left = Node('b')
    root.right.right = Node('x')
    root.right.left.right = Node('a')

    getPalindromePath(root)

    # This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program
// for the above approach
using System;

public class GFG
{
static String finalAns = "";

// Struct binary tree node
class Node
{
    public char data;
    public Node left, right;
};

// Function to create a new node
static Node newNode(char data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to check if the
// String is palindrome or not
static bool checkPalindrome(String s)
{
    int low = 0, high = (int)s.Length - 1;
    while (low < high)
    {
        if (s[low] != s[high])
            return false;
        low++;
        high--;
    }
    return true;
}

// Function to find the lexicographically
// smallest palindromic path in the Binary Tree
static void lexicographicallySmall(Node root, String s)
{

    // Base case
    if (root == null)
        return;

    // Append current node's
    // data to the String
    s += root.data;

    // Check if a node is leaf or not
    if (root.left == null && root.right == null)
    {
        if (checkPalindrome(s))
        {

            // Check for the 1st
            // Palindromic Path
            if (finalAns == "{content}quot;)
                finalAns = s;

            // Store lexicographically the
            // smallest palindromic path
            else
                finalAns = finalAns.CompareTo(s) <= 0 ? finalAns:s;
        }
        return;
    }

    // Recursively traverse left subtree
    lexicographicallySmall(root.left,
                           s);

    // Recursively traverse right subtree
    lexicographicallySmall(root.right,
                           s);
}

// Function to get smallest
// lexographical palindromic
// path
static void getPalindromePath(Node root)
{

    // Variable which stores
    // the readonly result
    finalAns = "{content}quot;;

    // Function call to compute
    // lexicographically smallest
    // palindromic Path
    lexicographicallySmall(root, "");
    if (finalAns == "{content}quot;)
        Console.Write("No Palindromic Path exists");
    else
        Console.Write(finalAns);
}

// Driver Code
public static void Main(String[] args)
{

    // Conbinary tree
    Node root = newNode('a');
    root.left = newNode('c');
    root.left.left = newNode('a');
    root.left.right = newNode('g');
    root.right = newNode('b');
    root.right.left = newNode('b');
    root.right.right = newNode('x');
    root.right.left.right = newNode('a');
    getPalindromePath(root);
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
    // Javascript program for the above approach
    let finalAns="";

    // Struct binary tree node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to create a new node
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // Function to check if the
    // String is palindrome or not
    function checkPalindrome(s)
    {
        let low = 0, high = s.length - 1;
        while (low < high)
        {
            if (s[low] != s[high])
                return false;
            low++;
            high--;
        }
        return true;
    }

    // Function to find the lexicographically
    // smallest palindromic path in the Binary Tree
    function lexicographicallySmall(root, s)
    {

        // Base case
        if (root == null)
            return;

        // Append current node's
        // data to the String
        s += root.data;

        // Check if a node is leaf or not
        if (root.left == null && root.right == null)
        {
            if (checkPalindrome(s))
            {

                // Check for the 1st
                // Palindromic Path
                if (finalAns == "{content}quot;)
                    finalAns = s;

                // Store lexicographically the
                // smallest palindromic path
                else
                    finalAns = finalAns.localeCompare(s) <= 0 ? finalAns:s;
            }
            return;
        }

        // Recursively traverse left subtree
        lexicographicallySmall(root.left, s);

        // Recursively traverse right subtree
        lexicographicallySmall(root.right, s);
    }

    // Function to get smallest
    // lexographical palindromic
    // path
    function getPalindromePath(root)
    {

        // Variable which stores
        // the final result
        finalAns = "{content}quot;;

        // Function call to compute
        // lexicographically smallest
        // palindromic Path
        lexicographicallySmall(root, "");
        if (finalAns == "{content}quot;)
            document.write("No Palindromic Path exists");
        else
            document.write(finalAns);
    }

    // Conbinary tree
    let root = newNode('a');
    root.left = newNode('c');
    root.left.left = newNode('a');
    root.left.right = newNode('g');
    root.right = newNode('b');
    root.right.left = newNode('b');
    root.right.right = newNode('x');
    root.right.left.right = newNode('a');
    getPalindromePath(root);

// This code is contributed by suresh07.
</script>
```

****Output:** 

```
abba
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )***