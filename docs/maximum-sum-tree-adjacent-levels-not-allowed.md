# 不允许相邻级别的树的最大和

> 原文:[https://www . geesforgeks . org/maximum-sum-tree-邻接权-levels-不允许/](https://www.geeksforgeeks.org/maximum-sum-tree-adjacent-levels-not-allowed/)

给定具有正整数值的二叉树。找到节点的最大和，这样我们就不能选择两个级别来计算和

```
Examples:

Input : Tree
            1
           / \
          2   3
             /
            4
             \
              5
              /
             6

Output :11
Explanation: Total items we can take: {1, 4, 6} 
or {2, 3, 5}. Max sum = 11.

Input : Tree
             1
           /   \
          2     3
        /      /  \
      4       5     6
    /  \     /     /  
   17  18   19    30 
 /     /  \
11    12   13 
Output :89
Explanation: Total items we can take: {2, 3, 17, 18, 
19, 30} or {1, 4, 5, 6, 11, 12, 13}. 
Max sum from first set = 89.
```

**说明**:我们知道需要从交替树级获取物品值。这意味着，如果我们从第 1 级开始选择，下一个选择将从第 3 级开始，然后是第 5 级，依此类推。同样，如果我们从 2 级开始，下一个选秀权将从 4 级开始，然后是 6 级，以此类推。因此，我们实际上需要递归地对一个特定元素的所有子元素求和，因为这些子元素保证处于交替级别。

我们知道，对于树的任何节点，它都有 4 个孙子。

```
    grandchild1 = root.left.left;
    grandchild2 = root.left.right;
    grandchild3 = root.right.left;
    grandchild4 = root.right.right;
```

我们可以递归调用下面程序中的 getSum()方法，来求这些子代和他们孙代的和。最后，我们只需要**返回从 1 级开始到 2 级**开始得到的最大和。

## C++

```
// C++ code for max sum with adjacent levels
// not allowed
#include<bits/stdc++.h>
using namespace std;

    // Tree node class for Binary Tree
    // representation
    struct Node
    {
        int data;
        Node* left, *right;
        Node(int item)
        {
            data = item;
        }
    } ;

    int getSum(Node* root) ;

    // Recursive function to find the maximum
    // sum returned for a root node and its
    // grandchildren
    int getSumAlternate(Node* root)
    {
        if (root == NULL)
            return 0;

        int sum = root->data;
        if (root->left != NULL)
        {
            sum += getSum(root->left->left);
            sum += getSum(root->left->right);
        }

        if (root->right != NULL)
        {
            sum += getSum(root->right->left);
            sum += getSum(root->right->right);
        }
        return sum;
    }

    // Returns maximum sum with adjacent
    // levels not allowed-> This function
    // mainly uses getSumAlternate()
    int getSum(Node* root)
    {
        if (root == NULL)
            return 0;

        // We compute sum of alternate levels
        // starting first level and from second
        // level->
        // And return maximum of two values->
        return max(getSumAlternate(root),
                        (getSumAlternate(root->left) +
                        getSumAlternate(root->right)));
    }

    // Driver function
    int main()
    {
        Node* root = new Node(1);
        root->left = new Node(2);
        root->right = new Node(3);
        root->right->left = new Node(4);
        root->right->left->right = new Node(5);
        root->right->left->right->left = new Node(6);
        cout << (getSum(root));
        return 0;
    }

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for max sum with adjacent levels
// not allowed
import java.util.*;

public class Main {

    // Tree node class for Binary Tree
    // representation
    static class Node {
        int data;
        Node left, right;
        Node(int item)
        {
            data = item;
            left = right = null;
        }
    }

    // Recursive function to find the maximum
    // sum returned for a root node and its
    // grandchildren
    public static int getSumAlternate(Node root)
    {
        if (root == null)
            return 0;

        int sum = root.data;
        if (root.left != null) {
            sum += getSum(root.left.left);
            sum += getSum(root.left.right);
        }

        if (root.right != null) {
            sum += getSum(root.right.left);
            sum += getSum(root.right.right);
        }
        return sum;
    }

    // Returns maximum sum with adjacent
    // levels not allowed. This function
    // mainly uses getSumAlternate()
    public static int getSum(Node root)
    {
        if (root == null)
            return 0;

        // We compute sum of alternate levels
        // starting first level and from second
        // level.
        // And return maximum of two values.
        return Math.max(getSumAlternate(root),
                        (getSumAlternate(root.left) +
                        getSumAlternate(root.right)));
    }

    // Driver function
    public static void main(String[] args)
    {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.right.left = new Node(4);
        root.right.left.right = new Node(5);
        root.right.left.right.left = new Node(6);
        System.out.println(getSum(root));
    }
}
```

## 蟒蛇 3

```
# Python3 code for max sum with adjacent
# levels not allowed
from collections import deque as queue

# A BST node
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Recursive function to find the maximum
# sum returned for a root node and its
# grandchildren
def getSumAlternate(root):

    if (root == None):
        return 0

    sum = root.data

    if (root.left != None):
        sum += getSum(root.left.left)
        sum += getSum(root.left.right)

    if (root.right != None):
        sum += getSum(root.right.left)
        sum += getSum(root.right.right)

    return sum

# Returns maximum sum with adjacent
# levels not allowed. This function
# mainly uses getSumAlternate()
def getSum(root):

    if (root == None):
        return 0

    # We compute sum of alternate levels
    # starting first level and from second
    # level.
    # And return maximum of two values.
    return max(getSumAlternate(root),
              (getSumAlternate(root.left) +
               getSumAlternate(root.right)))

# Driver code
if __name__ == '__main__':

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.right.left = Node(4)
    root.right.left.right = Node(5)
    root.right.left.right.left = Node(6)

    print(getSum(root))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# code for max sum with adjacent levels
// not allowed
using System;

class GFG
{

    // Tree node class for Binary Tree
    // representation
    public class Node
    {
        public int data;
        public Node left, right;
        public Node(int item)
        {
            data = item;
            left = right = null;
        }
    }

    // Recursive function to find the maximum
    // sum returned for a root node and its
    // grandchildren
    public static int getSumAlternate(Node root)
    {
        if (root == null)
            return 0;

        int sum = root.data;
        if (root.left != null)
        {
            sum += getSum(root.left.left);
            sum += getSum(root.left.right);
        }

        if (root.right != null)
        {
            sum += getSum(root.right.left);
            sum += getSum(root.right.right);
        }
        return sum;
    }

    // Returns maximum sum with adjacent
    // levels not allowed. This function
    // mainly uses getSumAlternate()
    public static int getSum(Node root)
    {
        if (root == null)
            return 0;

        // We compute sum of alternate levels
        // starting first level and from second
        // level.
        // And return maximum of two values.
        return Math.Max(getSumAlternate(root),
                        (getSumAlternate(root.left) +
                        getSumAlternate(root.right)));
    }

    // Driver code
    public static void Main()
    {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.right.left = new Node(4);
        root.right.left.right = new Node(5);
        root.right.left.right.left = new Node(6);
        Console.WriteLine(getSum(root));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript code for max sum with
// adjacent levels not allowed

// Tree node class for Binary Tree
// representation
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

// Recursive function to find the maximum
// sum returned for a root node and its
// grandchildren
function getSumAlternate(root)
{
    if (root == null)
        return 0;

    let sum = root.data;
    if (root.left != null)
    {
        sum += getSum(root.left.left);
        sum += getSum(root.left.right);
    }

    if (root.right != null)
    {
        sum += getSum(root.right.left);
        sum += getSum(root.right.right);
    }
    return sum;
}

// Returns maximum sum with adjacent
// levels not allowed. This function
// mainly uses getSumAlternate()
function getSum(root)
{
    if (root == null)
        return 0;

    // We compute sum of alternate levels
    // starting first level and from second
    // level.
    // And return maximum of two values.
    return Math.max(getSumAlternate(root),
                   (getSumAlternate(root.left) +
                    getSumAlternate(root.right)));
}

// Driver code
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.right.left = new Node(4);
root.right.left.right = new Node(5);
root.right.left.right.left = new Node(6);

document.write(getSum(root));

// This code is contributed by patel2127

</script>
```

**输出:**

```
11
```

**时间复杂度:** O(n)

练习:尝试为 n 元树而不是二叉树打印相同的解决方案。诀窍在于树的表现。

本文由 **Ashish Kumar** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。