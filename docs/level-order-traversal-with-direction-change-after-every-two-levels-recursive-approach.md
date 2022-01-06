# 每两级后方向改变的级序遍历|递归方法

> 原文:[https://www . geesforgeks . org/level-order-遍历-带方向-每两级后改变-递归-方法/](https://www.geeksforgeeks.org/level-order-traversal-with-direction-change-after-every-two-levels-recursive-approach/)

给定一个二叉树，以这样的方式打印级别顺序遍历:前两个级别从左到右打印，后两个级别从右到左打印，然后后两个级别从左到右打印，以此类推。所以，问题是每隔两级就要反转二叉树的级序遍历方向。
**例:**

```
Input: 
            1     
          /   \
        2       3
      /  \     /  \
     4    5    6    7
    / \  / \  / \  / \ 
   8  9 3   1 4  2 7  2
     /     / \    \
    16    17  18   19
Output:
1
2 3
7 6 5 4
2 7 2 4 1 3 9 8
16 17 18 19
In the above example, the first two levels
are printed from left to right, next two
levels are printed from right to left,
and then the last level is printed from 
left to right.
```

**方法:**在之前的[帖子](https://www.geeksforgeeks.org/level-order-traversal-direction-change-every-two-levels/)中，已经使用队列和堆栈进行了级别顺序遍历来打印元素。这里使用了一种**递归**方法来打印每一级的元素。遍历树中的每一层，对于每一层，检查方向。使用一个标志来知道树中遍历的方向。如果**标志**设置为*真*，则在特定级别从右向左打印节点。如果**标志**设置为**假**，从左到右打印该级别的节点。最初，标志设置为假，每两级后，标志将其值更改为真，反之亦然。
以下是上述办法的实施情况。

## C++

```
// C++ program level order traversal
// with direction change
// after every two levels
#include <bits/stdc++.h>
using namespace std;

struct node {
    int data;
    node *left, *right;
} * temp;

// inserts new node
node* newNode(int data)
{
    temp = new node;
    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// function to  print current level
void printCurrLevel(node* root, int level, bool flag)
{
    if (!root)
        return;

    if (level == 1) {
        cout << root->data << " ";
        return;
    }

    else {
        // If the flag is true, we have to print
        // level from RIGHT to LEFT.
        if (flag) {
            printCurrLevel(root->right, level - 1, flag);
            printCurrLevel(root->left, level - 1, flag);
        }

        // If the flag is false, we have to print
        // level from LEFT to RIGHT.
        else {
            printCurrLevel(root->left, level - 1, flag);
            printCurrLevel(root->right, level - 1, flag);
        }
    }
}

// This function returns the height of tree.
int height(node* root)
{
    if (!root)
        return 0;

    // left subtree
    int lh = height(root->left);

    // right subtree
    int rh = height(root->right);

    return 1 + max(lh, rh);
}

// Function to traverse level-wise and
// print nodes
void modifiedLevelOrder(node* root)
{
    int h = height(root);

    // Variable to choose direction.
    bool flag = false;
    for (int i = 1; i <= h; i++) {
        printCurrLevel(root, i, flag);
        cout << endl;

        // change direction after every two levels.
        if (i % 2 == 0)
            flag = !flag;
    }
}

// Driver Code
int main()
{

    // create tree that is given
    // in the example
    node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->left->left->left = newNode(8);
    root->left->left->right = newNode(9);
    root->left->right->left = newNode(3);
    root->left->right->right = newNode(1);
    root->right->left->left = newNode(4);
    root->right->left->right = newNode(2);
    root->right->right->left = newNode(7);
    root->right->right->right = newNode(2);
    root->left->right->left->left = newNode(16);
    root->left->right->left->right = newNode(17);
    root->right->left->right->left = newNode(18);
    root->right->right->left->right = newNode(19);

    modifiedLevelOrder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above idea
import java.util.*;

class GFG
{

static class node
{
    int data;
    node left, right;
}
static node temp;

// inserts new node
static node newNode(int data)
{
    temp = new node();
    temp.data = data;
    temp.left = temp.right = null;

    return temp;
}

// function to print current level
static void printCurrLevel(node root, int level, boolean flag)
{
    if (root == null)
        return;

    if (level == 1)
    {
            System.out.print(root.data + " ");
            return;
    }

    else
    {
        // If the flag is true, we have to print
        // level from RIGHT to LEFT.
        if (flag)
        {
            printCurrLevel(root.right, level - 1, flag);
            printCurrLevel(root.left, level - 1, flag);
        }

        // If the flag is false, we have to print
        // level from LEFT to RIGHT.
        else
        {
            printCurrLevel(root.left, level - 1, flag);
            printCurrLevel(root.right, level - 1, flag);
        }
    }
}

// This function returns the height of tree.
static int height(node root)
{
    if (root == null)
        return 0;

    // left subtree
    int lh = height(root.left);

    // right subtree
    int rh = height(root.right);

    return 1 + Math.max(lh, rh);
}

// Function to traverse level-wise and
// print nodes
static void modifiedLevelOrder(node root)
{
    int h = height(root);

    // Variable to choose direction.
    boolean flag = false;
    for (int i = 1; i <= h; i++)
    {
        printCurrLevel(root, i, flag);
        System.out.println("");

        // change direction after every two levels.
        if (i % 2 == 0)
            flag = !flag;
    }
}

// Driver Code
public static void main(String[] args)
{
    // create tree that is given
    // in the example
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(9);
    root.left.right.left = newNode(3);
    root.left.right.right = newNode(1);
    root.right.left.left = newNode(4);
    root.right.left.right = newNode(2);
    root.right.right.left = newNode(7);
    root.right.right.right = newNode(2);
    root.left.right.left.left = newNode(16);
    root.left.right.left.right = newNode(17);
    root.right.left.right.left = newNode(18);
    root.right.right.left.right = newNode(19);

    modifiedLevelOrder(root);
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program level order traversal with
# direction change after every two levels
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# function to print current level
def printCurrLevel(root, level, flag):

    if root == None:
        return

    if level == 1:
        print(root.data, end = " ")
        return

    else:

        # If the flag is true, we have to
        # print level from RIGHT to LEFT.
        if flag:
            printCurrLevel(root.right,
                           level - 1, flag)
            printCurrLevel(root.left,
                           level - 1, flag)

        # If the flag is false, we have to
        # print level from LEFT to RIGHT.
        else:
            printCurrLevel(root.left,
                           level - 1, flag)
            printCurrLevel(root.right,
                           level - 1, flag)

# This function returns the
# height of tree.
def height(root):

    if root == None:
        return 0

    # left subtree
    lh = height(root.left)

    # right subtree
    rh = height(root.right)

    return 1 + max(lh, rh)

# Function to traverse level-wise
# and print nodes
def modifiedLevelOrder(root):

    h = height(root)

    # Variable to choose direction.
    flag = False
    for i in range(1, h + 1):
        printCurrLevel(root, i, flag)
        print()

        # change direction after every
        # two levels.
        if i % 2 == 0:
            flag = not flag

# Driver Code
if __name__ == "__main__":

    # create tree that is given
    # in the example
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)
    root.left.left.left = Node(8)
    root.left.left.right = Node(9)
    root.left.right.left = Node(3)
    root.left.right.right = Node(1)
    root.right.left.left = Node(4)
    root.right.left.right = Node(2)
    root.right.right.left = Node(7)
    root.right.right.right = Node(2)
    root.left.right.left.left = Node(16)
    root.left.right.left.right = Node(17)
    root.right.left.right.left = Node(18)
    root.right.right.left.right = Node(19)

    modifiedLevelOrder(root)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of above idea
using System;

class GFG
{

public class node
{
    public int data;
    public node left, right;
}
static node temp;

// inserts new node
static node newNode(int data)
{
    temp = new node();
    temp.data = data;
    temp.left = temp.right = null;

    return temp;
}

// function to print current level
static void printCurrLevel(node root, int level, Boolean flag)
{
    if (root == null)
        return;

    if (level == 1)
    {
        Console.Write(root.data + " ");
        return;
    }

    else
    {
        // If the flag is true, we have to print
        // level from RIGHT to LEFT.
        if (flag)
        {
            printCurrLevel(root.right, level - 1, flag);
            printCurrLevel(root.left, level - 1, flag);
        }

        // If the flag is false, we have to print
        // level from LEFT to RIGHT.
        else
        {
            printCurrLevel(root.left, level - 1, flag);
            printCurrLevel(root.right, level - 1, flag);
        }
    }
}

// This function returns the height of tree.
static int height(node root)
{
    if (root == null)
        return 0;

    // left subtree
    int lh = height(root.left);

    // right subtree
    int rh = height(root.right);

    return 1 + Math.Max(lh, rh);
}

// Function to traverse level-wise and
// print nodes
static void modifiedLevelOrder(node root)
{
    int h = height(root);

    // Variable to choose direction.
    Boolean flag = false;
    for (int i = 1; i <= h; i++)
    {
        printCurrLevel(root, i, flag);
        Console.WriteLine("");

        // change direction after every two levels.
        if (i % 2 == 0)
            flag = !flag;
    }
}

// Driver Code
public static void Main(String[] args)
{
    // create tree that is given
    // in the example
    node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(9);
    root.left.right.left = newNode(3);
    root.left.right.right = newNode(1);
    root.right.left.left = newNode(4);
    root.right.left.right = newNode(2);
    root.right.right.left = newNode(7);
    root.right.right.right = newNode(2);
    root.left.right.left.left = newNode(16);
    root.left.right.left.right = newNode(17);
    root.right.left.right.left = newNode(18);
    root.right.right.left.right = newNode(19);

    modifiedLevelOrder(root);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // Javascript implementation of above idea
    class node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let temp;

    // inserts new node
    function newNode(data)
    {
        temp = new node(data);
        return temp;
    }

    // function to print current level
    function printCurrLevel(root, level, flag)
    {
        if (root == null)
            return;

        if (level == 1)
        {
            document.write(root.data + " ");
            return;
        }

        else
        {
            // If the flag is true, we have to print
            // level from RIGHT to LEFT.
            if (flag)
            {
                printCurrLevel(root.right, level - 1, flag);
                printCurrLevel(root.left, level - 1, flag);
            }

            // If the flag is false, we have to print
            // level from LEFT to RIGHT.
            else
            {
                printCurrLevel(root.left, level - 1, flag);
                printCurrLevel(root.right, level - 1, flag);
            }
        }
    }

    // This function returns the height of tree.
    function height(root)
    {
        if (root == null)
            return 0;

        // left subtree
        let lh = height(root.left);

        // right subtree
        let rh = height(root.right);

        return 1 + Math.max(lh, rh);
    }

    // Function to traverse level-wise and
    // print nodes
    function modifiedLevelOrder(root)
    {
        let h = height(root);

        // Variable to choose direction.
        let flag = false;
        for (let i = 1; i <= h; i++)
        {
            printCurrLevel(root, i, flag);
            document.write("</br>");

            // change direction after every two levels.
            if (i % 2 == 0)
                flag = !flag;
        }
    }

    // create tree that is given
    // in the example
    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.left.left.left = newNode(8);
    root.left.left.right = newNode(9);
    root.left.right.left = newNode(3);
    root.left.right.right = newNode(1);
    root.right.left.left = newNode(4);
    root.right.left.right = newNode(2);
    root.right.right.left = newNode(7);
    root.right.right.right = newNode(2);
    root.left.right.left.left = newNode(16);
    root.left.right.left.right = newNode(17);
    root.right.left.right.left = newNode(18);
    root.right.right.left.right = newNode(19);

    modifiedLevelOrder(root);

// This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
1 
2 3 
7 6 5 4 
2 7 2 4 1 3 9 8 
16 17 18 19
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)