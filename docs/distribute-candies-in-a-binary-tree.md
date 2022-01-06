# 在二叉树中分发糖果

> 原文:[https://www . geesforgeks . org/distribute-candes-in-a-a-binary-tree/](https://www.geeksforgeeks.org/distribute-candies-in-a-binary-tree/)

给定一个有 N 个节点的二叉树，其中每个节点值代表该节点上存在的糖果数量，总共有 N 个糖果。在一次移动中，可以选择两个相邻的节点，并将一个糖果从一个节点移动到另一个节点(移动可以是从父节点到子节点，或者从子节点到父节点。)
任务是找到所需的移动次数，使得每个节点都有**正好一个**糖果。

**示例:**

```
Input :      3
           /   \
          0     0 
Output : 2
Explanation: From the root of the tree, we move one 
candy to its left child, and one candy to
its right child.

Input :      0
           /   \
          3     0  
Output :3
Explanation : From the left child of the root, we move 
two candies to the root [taking two moves]. Then, we move 
one candy from the root of the tree to the right child. 
```

**递归求解:**
思路是从叶到根遍历树，连续平衡所有节点。要平衡一个节点，该节点上的糖果数量必须为 1。
可以有两种情况:

1.  如果一个节点需要糖果，如果树的节点有 0 颗糖果(比它需要的多了-1 颗)，那么我们应该把一颗糖果从它的父节点推到这个节点上。
2.  如果节点有 1 个以上的糖果。如果它说，4 个糖果(超过 3 个)，那么我们应该把 3 个糖果从节点推到它的父节点。

因此，从该叶到或从其父代的移动总数是超额=**ABS(num _ candes–1)**。
一旦一个节点平衡了，我们在剩下的计算中就再也不用考虑这个节点了。
以下是上述方法的实施:

## C++

```
// C++ program to distribute candies
// in a Binary Tree

#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Utility function to find the number of
// moves to distribute all of the candies
int distributeCandyUtil(Node* root, int& ans)
{
    // Base Case
    if (root == NULL)
        return 0;

    // Traverse left subtree
    int l = distributeCandyUtil(root->left, ans);

    // Traverse right subtree
    int r = distributeCandyUtil(root->right, ans);

    // Update number of moves
    ans += abs(l) + abs(r);

    // Return number of moves to balance
    // current node
    return root->key + l + r - 1;
}

// Function to find the number of moves to
// distribute all of the candies
int distributeCandy(Node* root)
{
    int ans = 0;

    distributeCandyUtil(root, ans);

    return ans;
}

// Driver program
int main()
{
    /*  3
       / \
      0   0

    Let us create Binary Tree
    shown in above example */

    Node* root = newNode(3);
    root->left = newNode(0);
    root->right = newNode(0);

    cout << distributeCandy(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to distribute candies
// in a Binary Tree
class GfG {

    // Binary Tree Node
    static class Node {
        int key;
        Node left, right;
    }
    static int ans = 0;

    // Utility function to create a new node
    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.key = key;
        temp.left = null;
        temp.right = null;
        return (temp);
    }

    // Utility function to find the number of
    // moves to distribute all of the candies
    static int distributeCandyUtil(Node root)
    {
        // Base Case
        if (root == null)
            return 0;

        // Traverse left subtree
        int l = distributeCandyUtil(root.left);

        // Traverse right subtree
        int r = distributeCandyUtil(root.right);

        // Update number of moves
        ans += Math.abs(l) + Math.abs(r);

        // Return number of moves to balance
        // current node
        return root.key + l + r - 1;
    }

    // Function to find the number of moves to
    // distribute all of the candies
    static int distributeCandy(Node root)
    {
        distributeCandyUtil(root);
        return ans;
    }

    // Driver program
    public static void main(String[] args)
    {
        /* 3
    / \
    0 0

    Let us create Binary Tree
    shown in above example */

        Node root = newNode(3);
        root.left = newNode(0);
        root.right = newNode(0);

        System.out.println(distributeCandy(root));
    }
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python3 program to distribute candies
# in a Binary Tree

# Binary Tree Node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Utility function to create a new node
def newNode(key):

    temp = Node(key)
    return temp

# Utility function to find the number of
# moves to distribute all of the candies
def distributeCandyUtil( root, ans):

    # Base Case
    if (root == None):
        return 0, ans;

    # Traverse left subtree
    l,ans = distributeCandyUtil(root.left, ans);

    # Traverse right subtree
    r,ans = distributeCandyUtil(root.right, ans);

    # Update number of moves
    ans += abs(l) + abs(r);

    # Return number of moves to balance
    # current node
    return root.key + l + r - 1, ans;

# Function to find the number of moves to
# distribute all of the candies
def distributeCandy(root):

    ans = 0;

    tmp, ans = distributeCandyUtil(root, ans);

    return ans;

# Driver program
if __name__=='__main__':

    '''  3
       / \
      0   0

    Let us create Binary Tree
    shown in above example '''

    root = newNode(3);
    root.left = newNode(0);
    root.right = newNode(0);

    print(distributeCandy(root))

# This code is contributed by pratham76
```

## C#

```
// C# program to distribute candies
// in a Binary Tree
using System;

class GFG {

    // Binary Tree Node
    public class Node {
        public int key;
        public Node left, right;
    }
    static int ans = 0;

    // Utility function to create a new node
    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.key = key;
        temp.left = null;
        temp.right = null;
        return (temp);
    }

    // Utility function to find the number of
    // moves to distribute all of the candies
    static int distributeCandyUtil(Node root)
    {
        // Base Case
        if (root == null)
            return 0;

        // Traverse left subtree
        int l = distributeCandyUtil(root.left);

        // Traverse right subtree
        int r = distributeCandyUtil(root.right);

        // Update number of moves
        ans += Math.Abs(l) + Math.Abs(r);

        // Return number of moves to balance
        // current node
        return root.key + l + r - 1;
    }

    // Function to find the number of moves to
    // distribute all of the candies
    static int distributeCandy(Node root)
    {
        distributeCandyUtil(root);
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        /* 3
    / \
    0 0

    Let us create Binary Tree
    shown in above example */

        Node root = newNode(3);
        root.left = newNode(0);
        root.right = newNode(0);

        Console.WriteLine(distributeCandy(root));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to distribute candies in a Binary Tree

    // Binary Tree Node
    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    let ans = 0;

    // Utility function to create a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return (temp);
    }

    // Utility function to find the number of
    // moves to distribute all of the candies
    function distributeCandyUtil(root)
    {
        // Base Case
        if (root == null)
            return 0;

        // Traverse left subtree
        let l = distributeCandyUtil(root.left);

        // Traverse right subtree
        let r = distributeCandyUtil(root.right);

        // Update number of moves
        ans += Math.abs(l) + Math.abs(r);

        // Return number of moves to balance
        // current node
        return root.key + l + r - 1;
    }

    // Function to find the number of moves to
    // distribute all of the candies
    function distributeCandy(root)
    {
        distributeCandyUtil(root);
        return ans;
    }

      /* 3
    / \
    0 0

    Let us create Binary Tree
    shown in above example */

    let root = newNode(3);
    root.left = newNode(0);
    root.right = newNode(0);

    document.write(distributeCandy(root));

</script>
```

**输出**:

```
2
```

**迭代解:**

**进场:**在每个节点，会有一些糖果从左边来，往右边走，或者从右边来，往左边走。在每种情况下，移动都会增加。因此，对于每个节点，我们将计算右边孩子和左边孩子**中所需糖果的数量，即每个孩子的(节点总数–糖果总数)**。有可能是**小于 0** ，但在这种情况下，它也将被视为移动，因为额外的糖果也必须通过根节点。

下面是迭代方法的实现:

## C++

```
// C++ program to distribute
// candies in a Binary Tree

#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to create a new node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

int countinchild(Node* root)
{
    // as node exists.
    if (root == NULL)
        return 0;

    int numberofnodes = 0; // to count total nodes.
    int sum = 0; // to count total candies present.

    queue<Node*> q;
    q.push(root);

    while (q.size() != 0) {
        Node* f = q.front();
        q.pop();

        numberofnodes++;
        sum += f->key;

        if (f->left)
            q.push(f->left);
        if (f->right)
            q.push(f->right);
    }

    // as either less than 0 or greater, it will be counted as
    // move as explained in the approach.

    return abs(numberofnodes - sum);
}

int distributeCandy(Node* root)
{
    // moves will count for total no. of moves.
    int moves = 0;

    // as 0 node and 0 value.
    if (root == NULL)
        return 0;

    // as leaf node don't have to pass any candies.
    if (!root->left && !root->right)
        return 0;

    // queue to iterate on tree .
    queue<Node*> q;
    q.push(root);

    while (q.size() != 0) {
        Node* f = q.front();
        q.pop();

        // total pass from left child
        moves += countinchild(f->left);
        // total pass from right child
        moves += countinchild(f->right);

        if (f->left)
            q.push(f->left);
        if (f->right)
            q.push(f->right);
    }

    return moves;
}

// Driver program
int main()
{
    /*  1
       / \
      0   2

    Let us create Binary Tree 
    shown in above example */

    Node* root = newNode(1);
    root->left = newNode(0);
    root->right = newNode(2);

    cout << distributeCandy(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to distribute candies in a Binary Tree
import java.util.*;
public class GFG
{
    static class Node {

        int key;
        Node left, right;

        Node(int item)
        {
            key = item;
            left = right = null;
        }
    }

    // Root of the Binary Tree
    static Node root;
    public GFG()
    {
        root = null;
    }

    // Utility function to create a new node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return (temp);
    }

    static int countinchild(Node root)
    {
        // as node exists.
        if (root == null)
            return 0;

        int numberofnodes = 0; // to count total nodes.
        int sum = 0; // to count total candies present.

        Queue<Node> q = new LinkedList<>();
        q.add(root);

        while (q.size() != 0) {
            Node f = (Node)q.peek();
            q.remove();

            numberofnodes++;
            sum += f.key;

            if (f.left != null)
                q.add(f.left);
            if (f.right != null)
                q.add(f.right);
        }

        // as either less than 0 or greater, it will be counted as
        // move as explained in the approach.

        return Math.abs(numberofnodes - sum);
    }

    static int distributeCandy(Node root)
    {
        // moves will count for total no. of moves.
        int moves = 0;

        // as 0 node and 0 value.
        if (root == null)
            return 0;

        // as leaf node don't have to pass any candies.
        if (root.left == null && root.right == null)
            return 0;

        // queue to iterate on tree .
        Queue<Node> q = new LinkedList<>();
        q.add(root);

        while (q.size() != 0) {
            Node f = (Node)q.peek();
            q.remove();

            // total pass from left child
            moves += countinchild(f.left);
            // total pass from right child
            moves += countinchild(f.right);

            if (f.left != null)
                q.add(f.left);
            if (f.right != null)
                q.add(f.right);
        }

        return moves;
    }

    public static void main(String[] args) {
            /*  1
           / \
          0   2

        Let us create Binary Tree
        shown in above example */

        GFG tree = new GFG();

        tree.root = newNode(1);
        tree.root.left = newNode(0);
        tree.root.right = newNode(2);

        System.out.println(distributeCandy(tree.root));
    }
}

// This code is contributed by divyeshrabadiyaa07.
```

## 蟒蛇 3

```
# Python3 program to distribute
# candies in a Binary Tree

# Binary Tree Node
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# Utility function to create a new node
def newNode(key):
    temp = Node(key)
    return temp  

def countinchild(root):

    # as node exists.
    if (root == None):
        return 0;
    numberofnodes = 0; # to count total nodes.
    sum = 0; # to count total candies present.

    q = []
    q.append(root);

    while (len(q) != 0):       
        f = q[0];
        q.pop(0);

        numberofnodes += 1
        sum += f.key;

        if (f.left):
            q.append(f.left);
        if (f.right):
            q.append(f.right);

    # as either less than 0 or greater, it will be counted as
    # move as explained in the approach.
    return abs(numberofnodes - sum);

def distributeCandy(root):

    # moves will count for total no. of moves.
    moves = 0;

    # as 0 node and 0 value.
    if (root == None):
        return 0;

    # as leaf node don't have to pass any candies.
    if (not root.left and not root.right):
        return 0;

    # queue to iterate on tree .
    q = []
    q.append(root);

    while (len(q) != 0):       
        f = q[0];
        q.pop(0);

        # total pass from left child
        moves += countinchild(f.left);

        # total pass from right child
        moves += countinchild(f.right);

        if (f.left):
            q.append(f.left);
        if (f.right):
            q.append(f.right);

    return moves;

# Driver program
if __name__=='__main__':

    '''
    /  1
       / \
      0   2

    Let us create Binary Tree 
    shown in above example '''

    root = newNode(1);
    root.left = newNode(0);
    root.right = newNode(2);
    print(distributeCandy(root))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to distribute candies in a Binary Tree
using System;
using System.Collections;
using System.Collections.Generic;

class Node {

    public int key;
    public Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}

public class GFG {

    // Root of the Binary Tree
    Node root;
    public GFG()
    {
        root = null;
    }

    // Utility function to create a new node
    static Node newNode(int key)
    {
        Node temp = new Node(key);
        return (temp);
    }

    static int countinchild(Node root)
    {
        // as node exists.
        if (root == null)
            return 0;

        int numberofnodes = 0; // to count total nodes.
        int sum = 0; // to count total candies present.

        Queue q = new Queue();
        q.Enqueue(root);

        while (q.Count != 0) {
            Node f = (Node)q.Peek();
            q.Dequeue();

            numberofnodes++;
            sum += f.key;

            if (f.left != null)
                q.Enqueue(f.left);
            if (f.right != null)
                q.Enqueue(f.right);
        }

        // as either less than 0 or greater, it will be counted as
        // move as explained in the approach.

        return Math.Abs(numberofnodes - sum);
    }

    static int distributeCandy(Node root)
    {
        // moves will count for total no. of moves.
        int moves = 0;

        // as 0 node and 0 value.
        if (root == null)
            return 0;

        // as leaf node don't have to pass any candies.
        if (root.left == null && root.right == null)
            return 0;

        // queue to iterate on tree .
        Queue q = new Queue();
        q.Enqueue(root);

        while (q.Count != 0) {
            Node f = (Node)q.Peek();
            q.Dequeue();

            // total pass from left child
            moves += countinchild(f.left);
            // total pass from right child
            moves += countinchild(f.right);

            if (f.left != null)
                q.Enqueue(f.left);
            if (f.right != null)
                q.Enqueue(f.right);
        }

        return moves;
    }

  static void Main() {
    /*  1
       / \
      0   2

    Let us create Binary Tree
    shown in above example */

    GFG tree = new GFG();

    tree.root = newNode(1);
    tree.root.left = newNode(0);
    tree.root.right = newNode(2);

    Console.Write(distributeCandy(tree.root));
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>
    // Javascript program to distribute
    // candies in a Binary Tree

    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.key = key;
        }
    }

    // Utility function to create a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return (temp);
    }

    function countinchild(root)
    {
        // as node exists.
        if (root == null)
            return 0;

        let numberofnodes = 0; // to count total nodes.
        let sum = 0; // to count total candies present.

        let q = [];
        q.push(root);

        while (q.length != 0) {
            let f = q[0];
            q.shift();

            numberofnodes++;
            sum += f.key;

            if (f.left)
                q.push(f.left);
            if (f.right)
                q.push(f.right);
        }

        // as either less than 0 or greater, it will be counted as
        // move as explained in the approach.

        return Math.abs(numberofnodes - sum);
    }

    function distributeCandy(root)
    {
        // moves will count for total no. of moves.
        let moves = 0;

        // as 0 node and 0 value.
        if (root == null)
            return 0;

        // as leaf node don't have to pass any candies.
        if (root.left == null && root.right == null)
            return 0;

        // queue to iterate on tree .
        let q = [];
        q.push(root);

        while (q.length != 0) {
            let f = q[0];
            q.shift();

            // total pass from left child
            moves += countinchild(f.left);
            // total pass from right child
            moves += countinchild(f.right);

            if (f.left)
                q.push(f.left);
            if (f.right)
                q.push(f.right);
        }

        return moves;
    }

    /*  1
       / \
      0   2

    Let us create Binary Tree
    shown in above example */

    let root = newNode(1);
    root.left = newNode(0);
    root.right = newNode(2);

    document.write(distributeCandy(root));

</script>
```

**Output**

```
2
```

**时间复杂度:**O(N * N)
T3】辅助空间: O(N)