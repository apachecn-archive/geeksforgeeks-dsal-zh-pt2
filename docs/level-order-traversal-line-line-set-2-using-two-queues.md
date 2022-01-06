# 逐行水平顺序遍历|集合 2(使用两个队列)

> 原文:[https://www . geesforgeks . org/level-order-遍历-line-line-set-2-使用两个队列/](https://www.geeksforgeeks.org/level-order-traversal-line-line-set-2-using-two-queues/)

给定一个二叉树，逐级打印节点，每一级在一个新的行上。

![](img/c8cf26aa3839f4c631be334e5430e6e2.png)

```
Output:
1
2 3
4 5
```

我们在下面的文章中讨论了一个解决方案。
[逐行打印级别顺序遍历| Set 1](https://www.geeksforgeeks.org/print-level-order-traversal-line-line/)
本文讨论了使用两个队列的不同方法。我们可以在第一个队列中插入第一个级别并打印它，当从第一个队列弹出时，将其左右节点插入第二个队列。现在开始打印第二个队列，并在弹出前将其左右子节点插入第一个队列。继续这个过程，直到两个队列都变空。

## C++

```
// C++ program to do level order traversal line by
// line
#include <bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    Node *left, *right;
};

// Prints level order traversal line by line
// using two queues.
void levelOrder(Node *root)
{
    queue<Node *> q1, q2;

    if (root == NULL)
        return;

    // Pushing first level node into first queue
    q1.push(root);

    // Executing loop till both the queues
    // become empty
    while (!q1.empty() || !q2.empty())
    {
        while (!q1.empty())
        {
            // Pushing left child of current node in
            // first queue into second queue
            if (q1.front()->left != NULL)
                q2.push(q1.front()->left);

            // pushing right child of current node
            // in first queue into second queue
            if (q1.front()->right != NULL)
                q2.push(q1.front()->right);

            cout << q1.front()->data << " ";
            q1.pop();
        }

        cout << "\n";

        while (!q2.empty())
        {
            // pushing left child of current node
            // in second queue into first queue
            if (q2.front()->left != NULL)
                q1.push(q2.front()->left);

            // pushing right child of current
            // node in second queue into first queue
            if (q2.front()->right != NULL)
                q1.push(q2.front()->right);

            cout << q2.front()->data << " ";
            q2.pop();
        }

        cout << "\n";
    }
}

// Utility function to create a new tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Driver program to test above functions
int main()
{
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->right = newNode(6);

    levelOrder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to do level order traversal line by
//line
import java.util.LinkedList;
import java.util.Queue;

public class GFG
{
    static class Node
    {
        int data;
        Node left;
        Node right;

        Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }

    // Prints level order traversal line by line
    // using two queues.
    static void levelOrder(Node root)
    {
        Queue<Node> q1 = new LinkedList<Node>();
        Queue<Node> q2 = new LinkedList<Node>();

        if (root == null)
            return;

        // Pushing first level node into first queue
        q1.add(root);

        // Executing loop till both the queues
        // become empty
        while (!q1.isEmpty() || !q2.isEmpty())
        {

            while (!q1.isEmpty())
            {

                // Pushing left child of current node in
                // first queue into second queue
                if (q1.peek().left != null)
                    q2.add(q1.peek().left);

                // pushing right child of current node
                // in first queue into second queue
                if (q1.peek().right != null)
                    q2.add(q1.peek().right);

                System.out.print(q1.peek().data + " ");
                q1.remove();
            }
            System.out.println();

            while (!q2.isEmpty())
            {

                // pushing left child of current node
                // in second queue into first queue
                if (q2.peek().left != null)
                    q1.add(q2.peek().left);

                // pushing right child of current
                // node in second queue into first queue
                if (q2.peek().right != null)
                    q1.add(q2.peek().right);

                System.out.print(q2.peek().data + " ");
                q2.remove();
            }
            System.out.println();
        }
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {

        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.right = new Node(6);

        levelOrder(root);
    }
}
// This code is Contributed by Sumit Ghosh
```

## 计算机编程语言

```
"""
Python program to do level order traversal
line by line using dual queue"""
class GFG:

    """Constructor to create a new tree node"""
    def __init__(self,data):
        self.val = data
        self.left = None
        self.right = None

    """Prints level order traversal line by
    line using two queues."""
    def levelOrder(self,node):
        q1 = [] # Queue 1
        q2 = [] # Queue 2
        q1.append(node)

        """Executing loop till both the
        queues become empty"""
        while(len(q1) > 0 or len(q2) > 0):

            """Empty string to concatenate
            the string for q1"""
            concat_str_q1 = ''
            while(len(q1) > 0):

                """Poped node at the first
                pos in queue 1 i.e q1"""
                poped_node = q1.pop(0)
                concat_str_q1 += poped_node.val +' '

                """Pushing left child of current
                node in first queue into second queue"""
                if poped_node.left:
                    q2.append(poped_node.left)

                """Pushing right child of current node
                in first queue into second queue"""
                if poped_node.right:
                    q2.append(poped_node.right)
            print( str(concat_str_q1))
            concat_str_q1 = ''

            """Empty string to concatenate the
            string for q1"""
            concat_str_q2 = ''
            while (len(q2) > 0):

                """Poped node at the first pos
                in queue 1 i.e q1"""
                poped_node = q2.pop(0)
                concat_str_q2 += poped_node.val + ' '

                """Pushing left child of current node
                in first queue into first queue"""
                if poped_node.left:
                    q1.append(poped_node.left)

                """Pushing right child of current node
                in first queue into first queue"""
                if poped_node.right:
                    q1.append(poped_node.right)
            print(str(concat_str_q2))
            concat_str_q2 = ''

""" Driver program to test above functions"""
node = GFG("1")
node.left = GFG("2")
node.right = GFG("3")
node.left.left = GFG("4")
node.left.right = GFG("5")
node.right.right = GFG("6")
node.levelOrder(node)

# This code is contributed by Vaibhav Kumar 12
```

## C#

```
// C# program to do level order
// traversal line by line
using System;
using System.Collections.Generic;

class GFG
{
    public class Node
    {
        public int data;
        public Node left;
        public Node right;

        public Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }

    // Prints level order traversal
    // line by line using two queues.
    public static void levelOrder(Node root)
    {
        LinkedList<Node> q1 = new LinkedList<Node>();
        LinkedList<Node> q2 = new LinkedList<Node>();

        if (root == null)
        {
            return;
        }

        // Pushing first level node
        // into first queue
        q1.AddLast(root);

        // Executing loop till both the
        // queues become empty
        while (q1.Count > 0 || q2.Count > 0)
        {

            while (q1.Count > 0)
            {

                // Pushing left child of current node
                // in first queue into second queue
                if (q1.First.Value.left != null)
                {
                    q2.AddLast(q1.First.Value.left);
                }

                // pushing right child of current node
                // in first queue into second queue
                if (q1.First.Value.right != null)
                {
                    q2.AddLast(q1.First.Value.right);
                }

                Console.Write(q1.First.Value.data + " ");
                q1.RemoveFirst();
            }
            Console.WriteLine();

            while (q2.Count > 0)
            {

                // pushing left child of current node
                // in second queue into first queue
                if (q2.First.Value.left != null)
                {
                    q1.AddLast(q2.First.Value.left);
                }

                // pushing right child of current
                // node in second queue into first queue
                if (q2.First.Value.right != null)
                {
                    q1.AddLast(q2.First.Value.right);
                }

                Console.Write(q2.First.Value.data + " ");
                q2.RemoveFirst();
            }
            Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.right = new Node(6);

        levelOrder(root);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to do level order
// traversal line by line
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Prints level order traversal
// line by line using two queues.
function levelOrder(root)
{
    var q1 = [];
    var q2 = [];
    if (root == null)
    {
        return;
    }

    // Pushing first level node
    // into first queue
    q1.push(root);

    // Executing loop till both the
    // queues become empty
    while (q1.length > 0 || q2.length > 0)
    {
        while (q1.length > 0)
        {

            // Pushing left child of current node
            // in first queue into second queue
            if (q1[0].left != null)
            {
                q2.push(q1[0].left);
            }

            // Pushing right child of current node
            // in first queue into second queue
            if (q1[0].right != null)
            {
                q2.push(q1[0].right);
            }
            document.write(q1[0].data + " ");
            q1.shift();
        }
        document.write("<br>");
        while (q2.length > 0)
        {

            // Pushing left child of current node
            // in second queue into first queue
            if (q2[0].left != null)
            {
                q1.push(q2[0].left);
            }

            // Pushing right child of current
            // node in second queue into first queue
            if (q2[0].right != null)
            {
                q1.push(q2[0].right);
            }
            document.write(q2[0].data + " ");
            q2.shift();
        }
        document.write("<br>");
    }
}

// Driver Code
var root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.right = new Node(6);

levelOrder(root);

// This code is contributed by noob2000

</script>
```

**输出:**

```
1
2 3
4 5 6
```

**时间复杂度:** O(n)

？list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
本文由 **Geetanjali Gaddam** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。