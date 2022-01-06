# 在两个二叉树中找到第一个不匹配的叶子

> 原文:[https://www . geeksforgeeks . org/find-first-非匹配-leads-two-二叉树/](https://www.geeksforgeeks.org/find-first-non-matching-leaves-two-binary-trees/)

给定两个二叉树，找出不匹配的两棵树的第一片叶子。如果没有不匹配的叶子，什么都不打印。
**例:**

```
Input : First Tree
          5
        /   \
       2     7
     /   \
   10     11

      Second Tree   
          6
       /    \
     10     15

Output : 11 15
If we consider leaves of two trees in order,
we can see that 11 and 15 are the first leaves 
that do not match.
```

**方法 1(简单):**
依次遍历两棵树，将两棵树的叶子存储在两个不同的列表中。最后，找出两个列表中不同的第一个值。时间复杂度为 O(n1 + n2)，其中 n1 和 n2 是两棵树中的节点数。辅助空间要求为 O(n1 + n2)。
**方法 2(高效)**
该解决方案将辅助空间需求表示为 O(h1 + h2)，其中 h1 和 h2 是树的高度。我们使用堆栈同时对两个树进行[迭代前序遍历](https://www.geeksforgeeks.org/iterative-preorder-traversal/)。我们为每棵树维护一个堆栈。对于每棵树，继续推进堆栈中的节点，直到顶部节点是叶节点。比较两个堆栈的顶部节点。如果它们相等，做进一步的遍历否则返回。

## C++

```
// C++ program to find first leaves that are
// not same.
#include<bits/stdc++.h>
using namespace std;

// Tree node
struct Node
{
    int data;
    Node *left,  *right;
};

// Utility method to create a new node
Node *newNode(int x)
{
    Node * temp = new Node;
    temp->data = x;
    temp->left = temp->right = NULL;
    return temp;
}

bool isLeaf(Node * t)
{
    return ((t->left == NULL) && (t->right == NULL));
}

// Prints the first non-matching leaf node in
// two trees if it exists, else prints nothing.
void findFirstUnmatch(Node *root1, Node *root2)
{
    // If any of the tree is empty
    if (root1 == NULL || root2 == NULL)
      return;

    // Create two stacks for preorder traversals
    stack<Node*> s1, s2;
    s1.push(root1);
    s2.push(root2);

    while (!s1.empty() || !s2.empty())
    {
        // If traversal of one tree is over
        // and other tree still has nodes.
        if (s1.empty() || s2.empty() )
           return;

        // Do iterative traversal of first tree
        // and find first lead node in it as "temp1"
        Node *temp1 = s1.top();
        s1.pop();
        while (temp1 && !isLeaf(temp1))
        {
            // pushing right childfirst so that
            // left child comes first while popping.
            s1.push(temp1->right);
            s1.push(temp1->left);
            temp1 = s1.top();
            s1.pop();
        }

        // Do iterative traversal of second tree
        // and find first lead node in it as "temp2"
        Node * temp2 = s2.top();
        s2.pop();
        while (temp2 && !isLeaf(temp2))
        {
            s2.push(temp2->right);
            s2.push(temp2->left);
            temp2 = s2.top();
            s2.pop();
        }

        // If we found leaves in both trees
        if (temp1 != NULL && temp2 != NULL )
        {
            if (temp1->data != temp2->data )
            {
                cout << "First non matching leaves : "
                     << temp1->data <<"  "<< temp2->data
                     << endl;
                return;
            }
        }
    }
}

// Driver code
int main()
{
    struct Node *root1 = newNode(5);
    root1->left = newNode(2);
    root1->right = newNode(7);
    root1->left->left = newNode(10);
    root1->left->right = newNode(11);

    struct Node * root2 = newNode(6);
    root2->left = newNode(10);
    root2->right = newNode(15);

    findFirstUnmatch(root1,root2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first leaves that are
// not same.
import java.util.*;
class GfG {

// Tree node
static class Node
{
    int data;
    Node left, right;
}

// Utility method to create a new node
static Node newNode(int x)
{
    Node temp = new Node();
    temp.data = x;
    temp.left = null;
    temp.right = null;
    return temp;
}

static boolean isLeaf(Node t)
{
    return ((t.left == null) && (t.right == null));
}

// Prints the first non-matching leaf node in
// two trees if it exists, else prints nothing.
static void findFirstUnmatch(Node root1, Node root2)
{
    // If any of the tree is empty
    if (root1 == null || root2 == null)
    return;

    // Create two stacks for preorder traversals
    Stack<Node> s1 = new Stack<Node> ();
    Stack<Node> s2 = new Stack<Node> ();
    s1.push(root1);
    s2.push(root2);

    while (!s1.isEmpty() || !s2.isEmpty())
    {
        // If traversal of one tree is over
        // and other tree still has nodes.
        if (s1.isEmpty() || s2.isEmpty() )
        return;

        // Do iterative traversal of first tree
        // and find first lead node in it as "temp1"
        Node temp1 = s1.peek();
        s1.pop();
        while (temp1 != null && isLeaf(temp1) != true)
        {
            // pushing right childfirst so that
            // left child comes first while popping.
            s1.push(temp1.right);
            s1.push(temp1.left);
            temp1 = s1.peek();
            s1.pop();
        }

        // Do iterative traversal of second tree
        // and find first lead node in it as "temp2"
        Node temp2 = s2.peek();
        s2.pop();
        while (temp2 != null && isLeaf(temp2) != true)
        {
            s2.push(temp2.right);
            s2.push(temp2.left);
            temp2 = s2.peek();
            s2.pop();
        }

        // If we found leaves in both trees
        if (temp1 != null && temp2 != null )
        {
            if (temp1.data != temp2.data )
            {
                System.out.println(temp1.data+" "+temp2.data);
                return;
            }
        }
    }
}

// Driver code
public static void main(String[] args)
{
    Node root1 = newNode(5);
    root1.left = newNode(2);
    root1.right = newNode(7);
    root1.left.left = newNode(10);
    root1.left.right = newNode(11);

    Node root2 = newNode(6);
    root2.left = newNode(10);
    root2.right = newNode(15);

    findFirstUnmatch(root1,root2);

}
}
```

## 蟒蛇 3

```
# Python3 program to find first leaves
# that are not same.

# Tree Node
# Utility function to create a
# new tree Node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

def isLeaf(t):

    return ((t.left == None) and
            (t.right == None))

# Prints the first non-matching leaf node in
# two trees if it exists, else prints nothing.
def findFirstUnmatch(root1, root2) :

    # If any of the tree is empty
    if (root1 == None or root2 == None) :
        return

    # Create two stacks for preorder
    # traversals
    s1 = []
    s2 = []
    s1.insert(0, root1)
    s2.insert(0, root2)

    while (len(s1) or len(s2)) :

        # If traversal of one tree is over
        # and other tree still has nodes.
        if (len(s1) == 0 or len(s2) == 0) :
            return

        # Do iterative traversal of first
        # tree and find first lead node
        # in it as "temp1"
        temp1 = s1[0]
        s1.pop(0)
        while (temp1 and not isLeaf(temp1)) :

            # pushing right childfirst so that
            # left child comes first while popping.
            s1.insert(0, temp1.right)
            s1.insert(0, temp1.left)
            temp1 = s1[0]
            s1.pop(0)

        # Do iterative traversal of second tree
        # and find first lead node in it as "temp2"
        temp2 = s2[0]
        s2.pop(0)
        while (temp2 and not isLeaf(temp2)) :

            s2.insert(0, temp2.right)
            s2.insert(0, temp2.left)
            temp2 = s2[0]
            s2.pop(0)

        # If we found leaves in both trees
        if (temp1 != None and temp2 != None ) :

            if (temp1.data != temp2.data ) :

                print("First non matching leaves :",
                        temp1.data, "", temp2.data )
                return

# Driver Code
if __name__ == '__main__':
    root1 = newNode(5)
    root1.left = newNode(2)
    root1.right = newNode(7)
    root1.left.left = newNode(10)
    root1.left.right = newNode(11)

    root2 = newNode(6)
    root2.left = newNode(10)
    root2.right = newNode(15)

    findFirstUnmatch(root1,root2)

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# program to find first leaves that are
// not same.
using System;
using System.Collections.Generic;

class GfG
{

    // Tree node
    public class Node
    {
        public int data;
        public Node left, right;
    }

    // Utility method to create a new node
    static Node newNode(int x)
    {
        Node temp = new Node();
        temp.data = x;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    static bool isLeaf(Node t)
    {
        return ((t.left == null) && (t.right == null));
    }

    // Prints the first non-matching leaf node in
    // two trees if it exists, else prints nothing.
    static void findFirstUnmatch(Node root1, Node root2)
    {
        // If any of the tree is empty
        if (root1 == null || root2 == null)
        return;

        // Create two stacks for preorder traversals
        Stack<Node> s1 = new Stack<Node> ();
        Stack<Node> s2 = new Stack<Node> ();
        s1.Push(root1);
        s2.Push(root2);

        while (s1.Count != 0 || s2.Count != 0)
        {
            // If traversal of one tree is over
            // and other tree still has nodes.
            if (s1.Count == 0 || s2.Count == 0 )
            return;

            // Do iterative traversal of first tree
            // and find first lead node in it as "temp1"
            Node temp1 = s1.Peek();
            s1.Pop();
            while (temp1 != null && isLeaf(temp1) != true)
            {
                // pushing right childfirst so that
                // left child comes first while popping.
                s1.Push(temp1.right);
                s1.Push(temp1.left);
                temp1 = s1.Peek();
                s1.Pop();
            }

            // Do iterative traversal of second tree
            // and find first lead node in it as "temp2"
            Node temp2 = s2.Peek();
            s2.Pop();
            while (temp2 != null && isLeaf(temp2) != true)
            {
                s2.Push(temp2.right);
                s2.Push(temp2.left);
                temp2 = s2.Peek();
                s2.Pop();
            }

            // If we found leaves in both trees
            if (temp1 != null && temp2 != null )
            {
                if (temp1.data != temp2.data )
                {
                    Console.WriteLine(temp1.data + " " + temp2.data);
                    return;
                }
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root1 = newNode(5);
        root1.left = newNode(2);
        root1.right = newNode(7);
        root1.left.left = newNode(10);
        root1.left.right = newNode(11);

        Node root2 = newNode(6);
        root2.left = newNode(10);
        root2.right = newNode(15);

        findFirstUnmatch(root1,root2);

    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find first leaves that are
// not same.
// Tree node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}
// Utility method to create a new node
function newNode(x)
{
    var temp = new Node();
    temp.data = x;
    temp.left = null;
    temp.right = null;
    return temp;
}
function isLeaf(t)
{
    return ((t.left == null) && (t.right == null));
}
// Prints the first non-matching leaf node in
// two trees if it exists, else prints nothing.
function findFirstUnmatch(root1, root2)
{
    // If any of the tree is empty
    if (root1 == null || root2 == null)
    return;
    // Create two stacks for preorder traversals
    var s1 = [];
    var s2 = [];
    s1.push(root1);
    s2.push(root2);
    while (s1.length != 0 || s2.length != 0)
    {
        // If traversal of one tree is over
        // and other tree still has nodes.
        if (s1.length == 0 || s2.length == 0 )
        return;
        // Do iterative traversal of first tree
        // and find first lead node in it as "temp1"
        var temp1 = s1[s1.length-1];
        s1.pop();
        while (temp1 != null && isLeaf(temp1) != true)
        {
            // pushing right childfirst so that
            // left child comes first while popping.
            s1.push(temp1.right);
            s1.push(temp1.left);
            temp1 = s1[s1.length-1];
            s1.pop();
        }
        // Do iterative traversal of second tree
        // and find first lead node in it as "temp2"
        var temp2 = s2[s2.length-1];
        s2.pop();
        while (temp2 != null && isLeaf(temp2) != true)
        {
            s2.push(temp2.right);
            s2.push(temp2.left);
            temp2 = s2[s2.length-1];
            s2.pop();
        }
        // If we found leaves in both trees
        if (temp1 != null && temp2 != null )
        {
            if (temp1.data != temp2.data )
            {
                document.write("First non matching leaves : " +
                temp1.data + " " + temp2.data);
                return;
            }
        }
    }
}
// Driver code
var root1 = newNode(5);
root1.left = newNode(2);
root1.right = newNode(7);
root1.left.left = newNode(10);
root1.left.right = newNode(11);
var root2 = newNode(6);
root2.left = newNode(10);
root2.right = newNode(15);
findFirstUnmatch(root1,root2);

</script>
```

**输出:**

```
First non matching leaves : 11  15
```

**参考文献:**

*   [https://www . geesforgeks . org/Amazon-interview-experience-set-337-SDE-1/](https://www.geeksforgeeks.org/amazon-interview-experience-set-337-sde-1/)
*   [https://www.careercup.com/question?id=5673248478986240](https://www.careercup.com/question?id=5673248478986240)

本文由 **Ekta Goel** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。