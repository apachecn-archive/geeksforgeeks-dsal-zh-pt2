# 二叉树中偶数和奇数节点的和之差

> 原文:[https://www . geeksforgeeks . org/二叉树中奇偶值节点和之差/](https://www.geeksforgeeks.org/difference-between-sum-of-even-and-odd-valued-nodes-in-a-binary-tree/)

给定一棵二叉树，任务是找出二叉树中偶值节点和奇值节点之间的**绝对差**。

**示例:**

```
Input:
      5
    /   \
   2     6
 /  \     \  
1    4     8
    /     / \ 
   3     7   9
Output: 5
Explanation:
Sum of the odd value nodes is:
5 + 1 + 3 + 7 + 9 = 25 
Sum of the even value nodes is:
2 + 6 + 4 + 8 = 20 
Absolute difference = (25 – 20) = 5.

Input:
      4
    /   \
   1     4
 /  \     \  
7    2     6
Output: 8
```

**方法:**
按照以下步骤解决问题:

*   遍历树中的每个节点，检查该节点的值是**奇数**还是**偶数。**
*   访问每个节点后，相应更新 **oddSum** 和**event sum**。
*   完成树的遍历后，打印 **oddSum** 和**event sum**的绝对差值。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

int oddsum = 0;
int evensum = 0;
int ans = 0;

struct node {
    int data;
    struct node* left;
    struct node* right;
};

struct node* newnode(int data)
{
    node* temp = new node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Function calculate the sum of
// odd and even value node
void OddEvenDifference(struct node*
                           root)
{
    // If root is NULL
    if (root == NULL) {
        return;
    }
    else {
        // Check if current root
        // is odd or even
        if (root->data % 2 == 0) {
            evensum += root->data;
        }
        else {
            oddsum += root->data;
        }
        // Call on the left subtree
        OddEvenDifference(root->left);

        // Call on the right subtree
        OddEvenDifference(root->right);
    }
}

// Driver Code
int main()
{
    node* root = newnode(5);
    root->left = newnode(2);
    root->right = newnode(6);
    root->left->left = newnode(1);
    root->left->right = newnode(4);
    root->left->right->left
        = newnode(3);
    root->right->right = newnode(8);
    root->right->right->right
        = newnode(9);
    root->right->right->left
        = newnode(7);

    OddEvenDifference(root);

    cout << abs(oddsum - evensum)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
class GFG{

static int oddsum = 0;
static int evensum = 0;
static int ans = 0;

static class node
{
    int data;
    node left;
    node right;
};

static node newnode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function calculate the sum of
// odd and even value node
static void OddEvenDifference(node root)
{

    // If root is null
    if (root == null)
    {
        return;
    }
    else
    {

        // Check if current root
        // is odd or even
        if (root.data % 2 == 0)
        {
            evensum += root.data;
        }
        else
        {
            oddsum += root.data;
        }

        // Call on the left subtree
        OddEvenDifference(root.left);

        // Call on the right subtree
        OddEvenDifference(root.right);
    }
}

// Driver Code
public static void main(String[] args)
{
    node root = newnode(5);
    root.left = newnode(2);
    root.right = newnode(6);
    root.left.left = newnode(1);
    root.left.right = newnode(4);
    root.left.right.left = newnode(3);
    root.right.right = newnode(8);
    root.right.right.right = newnode(9);
    root.right.right.left = newnode(7);

    OddEvenDifference(root);

    System.out.print(Math.abs(
        oddsum - evensum) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
oddsum = 0
evensum = 0

class Node:

    def __init__(self, data):

        self.left = None
        self.right = None
        self.data = data

def newnode(data):

    temp = Node(data)

    return temp

# Function calculate the sum of
# odd and even value node
def OddEvenDifference(root):

    global evensum, oddsum

    # If root is NULL
    if (root == None):
        return

    else:

        # Check if current root
        # is odd or even
        if (root.data % 2 == 0):
            evensum += root.data
        else:
            oddsum += root.data

        # Call on the left subtree
        OddEvenDifference(root.left)

        # Call on the right subtree
        OddEvenDifference(root.right)

# Driver code
if __name__=="__main__":

    root = newnode(5)
    root.left = newnode(2)
    root.right = newnode(6)
    root.left.left = newnode(1)
    root.left.right = newnode(4)
    root.left.right.left= newnode(3)
    root.right.right = newnode(8)
    root.right.right.right= newnode(9)
    root.right.right.left= newnode(7)

    OddEvenDifference(root)

    print(abs(oddsum - evensum))

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG{

static int oddsum = 0;
static int evensum = 0;
//static int ans = 0;

class node
{
    public int data;
    public node left;
    public node right;
};

static node newnode(int data)
{
    node temp = new node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function calculate the sum of
// odd and even value node
static void OddEvenDifference(node root)
{

    // If root is null
    if (root == null)
    {
        return;
    }
    else
    {

        // Check if current root
        // is odd or even
        if (root.data % 2 == 0)
        {
            evensum += root.data;
        }
        else
        {
            oddsum += root.data;
        }

        // Call on the left subtree
        OddEvenDifference(root.left);

        // Call on the right subtree
        OddEvenDifference(root.right);
    }
}

// Driver Code
public static void Main(String[] args)
{
    node root = newnode(5);
    root.left = newnode(2);
    root.right = newnode(6);
    root.left.left = newnode(1);
    root.left.right = newnode(4);
    root.left.right.left = newnode(3);
    root.right.right = newnode(8);
    root.right.right.right = newnode(9);
    root.right.right.left = newnode(7);

    OddEvenDifference(root);

    Console.Write(Math.Abs(
        oddsum - evensum) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    let oddsum = 0;
    let evensum = 0;
    let ans = 0;

    class node
    {
        constructor(data) {
           this.data = data;
           this.left = this.right = null;
        }
    }

    function newnode(data)
    {
        let temp = new node(data);
        return temp;
    }

    // Function calculate the sum of
    // odd and even value node
    function OddEvenDifference(root)
    {

        // If root is null
        if (root == null)
        {
            return;
        }
        else
        {

            // Check if current root
            // is odd or even
            if (root.data % 2 == 0)
            {
                evensum += root.data;
            }
            else
            {
                oddsum += root.data;
            }

            // Call on the left subtree
            OddEvenDifference(root.left);

            // Call on the right subtree
            OddEvenDifference(root.right);
        }
    }

    let root = newnode(5);
    root.left = newnode(2);
    root.right = newnode(6);
    root.left.left = newnode(1);
    root.left.right = newnode(4);
    root.left.right.left = newnode(3);
    root.right.right = newnode(8);
    root.right.right.right = newnode(9);
    root.right.right.left = newnode(7);

    OddEvenDifference(root);

    document.write(Math.abs(oddsum - evensum) + "</br>");

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*