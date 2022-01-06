# 二叉树中最低的共同祖先|集合 2(使用父指针)

> 原文:[https://www . geesforgeks . org/最低-二进制树中共同祖先-集合-2-使用父指针/](https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-tree-set-2-using-parent-pointer/)

给定二叉树中两个节点的值，找到最下面的**L****C**ommon**A**ncestor(LCA)。可以假设两个节点都存在于树中。

![BST_LCA](img/84da68a965d0c736f63b82d5c549c244.png "BST_LCA")

例如，考虑图中的二叉树，10 和 14 的 LCA 是 12，8 和 14 的 LCA 是 8。

让 T 成为一棵扎根的树。两个节点 n1 和 n2 之间的最低公共祖先被定义为 T 中同时具有 n1 和 n2 作为后代的最低节点(这里我们允许一个节点是其自身的后代)。来源:[维基百科](http://en.wikipedia.org/wiki/Lowest_common_ancestor)。

我们已经讨论了在第 1 集中寻找生命周期评价的不同方法。当给定父指针时，找到 LCA 变得很容易，因为我们可以很容易地使用父指针找到节点的所有祖先。

以下是寻找生命周期评价的步骤。

1.  创建一个空哈希表。
2.  在哈希表中插入 n1 及其所有祖先。
3.  Check if n2 or any of its ancestors exist in hash table, if yes return the first existing ancestor.

    下面是以上步骤的实现。

    ## C

    ```
    // C++ program to find lowest common ancestor using parent pointer
    #include <bits/stdc++.h>
    using namespace std;

    // A Tree Node
    struct Node
    {
        Node *left, *right, *parent;
        int key;
    };

    // A utility function to create a new BST node
    Node *newNode(int item)
    {
        Node *temp = new Node;
        temp->key = item;
        temp->parent = temp->left = temp->right = NULL;
        return temp;
    }

    /* A utility function to insert a new node with
       given key in Binary Search Tree */
    Node *insert(Node *node, int key)
    {
        /* If the tree is empty, return a new node */
        if (node == NULL) return newNode(key);

        /* Otherwise, recur down the tree */
        if (key < node->key)
        {
            node->left  = insert(node->left, key);
            node->left->parent = node;
        }
        else if (key > node->key)
        {
            node->right = insert(node->right, key);
            node->right->parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }

    // To find LCA of nodes n1 and n2 in Binary Tree
    Node *LCA(Node *n1, Node *n2)
    {
       // Creata a map to store ancestors of n1
       map <Node *, bool> ancestors;

       // Insert n1 and all its ancestors in map
       while (n1 != NULL)
       {
           ancestors[n1] = true;
           n1 = n1->parent;
       }

       // Check if n2 or any of its ancestors is in
       // map.
       while (n2 != NULL)
       {
           if (ancestors.find(n2) != ancestors.end())
               return n2;
           n2 = n2->parent;
       }

       return NULL;
    }

    // Driver method to test above functions
    int main(void)
    {
        Node * root = NULL;

        root = insert(root, 20);
        root = insert(root, 8);
        root = insert(root, 22);
        root = insert(root, 4);
        root = insert(root, 12);
        root = insert(root, 10);
        root = insert(root, 14);

        Node *n1 = root->left->right->left;
        Node *n2 = root->left;
        Node *lca = LCA(n1, n2);

        printf("LCA of %d and %d is %d \n", n1->key, n2->key, lca->key);

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    import java.util.HashMap;
    import java.util.Map;

    // Java program to find lowest common ancestor using parent pointer
    // A tree node
    class Node 
    {
        int key;
        Node left, right, parent;

        Node(int key) 
        {
            this.key = key;
            left = right = parent = null;
        }
    }

    class BinaryTree 
    {
        Node root, n1, n2, lca;

        /* A utility function to insert a new node with
           given key in Binary Search Tree */
        Node insert(Node node, int key) 
        {
            /* If the tree is empty, return a new node */
            if (node == null)
                return new Node(key);

            /* Otherwise, recur down the tree */
            if (key < node.key) 
            {
                node.left = insert(node.left, key);
                node.left.parent = node;
            }
            else if (key > node.key) 
            {
                node.right = insert(node.right, key);
                node.right.parent = node;
            }

            /* return the (unchanged) node pointer */
            return node;
        }

        // To find LCA of nodes n1 and n2 in Binary Tree
        Node LCA(Node n1, Node n2) 
        {
            // Creata a map to store ancestors of n1
            Map<Node, Boolean> ancestors = new HashMap<Node, Boolean>();

            // Insert n1 and all its ancestors in map
            while (n1 != null) 
            {
                ancestors.put(n1, Boolean.TRUE);
                n1 = n1.parent;
            }

            // Check if n2 or any of its ancestors is in
            // map.
            while (n2 != null) 
            {
                if (ancestors.containsKey(n2) != ancestors.isEmpty())
                    return n2;
                n2 = n2.parent;
            }

            return null;
        }

        // Driver method to test above functions
        public static void main(String[] args) 
        {
            BinaryTree tree = new BinaryTree();
            tree.root = tree.insert(tree.root, 20);
            tree.root = tree.insert(tree.root, 8);
            tree.root = tree.insert(tree.root, 22);
            tree.root = tree.insert(tree.root, 4);
            tree.root = tree.insert(tree.root, 12);
            tree.root = tree.insert(tree.root, 10);
            tree.root = tree.insert(tree.root, 14);

            tree.n1 = tree.root.left.right.left;
            tree.n2 = tree.root.left;
            tree.lca = tree.LCA(tree.n1, tree.n2);

            System.out.println("LCA of " + tree.n1.key + " and " + tree.n2.key
                    + " is " + tree.lca.key);
        }
    }

    // This code has been contributed by Mayank Jaiswal(mayank_24)
    ```

    ## C#

    ```
    // C# program to find lowest common ancestor using parent pointer
    // A tree node
    using System;
    using System.Collections;
    using System.Collections.Generic; 

    public class Node 
    {
        public int key;
        public Node left, right, parent;

        public Node(int key) 
        {
            this.key = key;
            left = right = parent = null;
        }
    }

    class BinaryTree 
    {
        Node root, n1, n2, lca;

        /* A utility function to insert a new node with
        given key in Binary Search Tree */
        Node insert(Node node, int key) 
        {
            /* If the tree is empty, return a new node */
            if (node == null)
                return new Node(key);

            /* Otherwise, recur down the tree */
            if (key < node.key) 
            {
                node.left = insert(node.left, key);
                node.left.parent = node;
            }
            else if (key > node.key) 
            {
                node.right = insert(node.right, key);
                node.right.parent = node;
            }

            /* return the (unchanged) node pointer */
            return node;
        }

        // To find LCA of nodes n1 and n2 in Binary Tree
        Node LCA(Node n1, Node n2) 
        {
            // Creata a map to store ancestors of n1
            Dictionary<Node, Boolean> ancestors = new Dictionary<Node, Boolean>();

            // Insert n1 and all its ancestors in map
            while (n1 != null) 
            {
                ancestors.Add(n1,true);
                n1 = n1.parent;
            }

            // Check if n2 or any of its ancestors is in
            // map.
            while (n2 != null) 
            {
                if (ancestors.ContainsKey(n2))
                    return n2;
                n2 = n2.parent;
            }

            return null;
        }

        // Driver code
        public static void Main(String []args) 
        {
            BinaryTree tree = new BinaryTree();
            tree.root = tree.insert(tree.root, 20);
            tree.root = tree.insert(tree.root, 8);
            tree.root = tree.insert(tree.root, 22);
            tree.root = tree.insert(tree.root, 4);
            tree.root = tree.insert(tree.root, 12);
            tree.root = tree.insert(tree.root, 10);
            tree.root = tree.insert(tree.root, 14);

            tree.n1 = tree.root.left.right.left;
            tree.n2 = tree.root.left;
            tree.lca = tree.LCA(tree.n1, tree.n2);

            Console.WriteLine("LCA of " + tree.n1.key + " and " + tree.n2.key
                    + " is " + tree.lca.key);
        }
    }

    // This code is contributed by Arnab Kundu
    ```

    **Output:**

    ```
    LCA of 10 and 8 is 8 
    ```

    注意:上面的实现使用二叉查找树的插入来创建一个二叉树，但是 LCA 函数适用于任何二叉树(不一定是二叉查找树)。

     **时间复杂度:** O(h)其中 h 是二叉树的高度如果我们使用哈希表来实现这个解决方案(注意上面的解决方案使用了需要 O(Log h)时间来插入和查找的 map)。所以上述实现的时间复杂度为 O(h Log h)。

    **辅助空间:** O(h)

    **A O(h)时间和 O(1)额外空间解决方案** :
    上面的解决方案需要额外的空间，因为我们需要使用哈希表来存储访问过的祖先。我们可以使用以下事实来解决 O(1)额外空间中的问题:如果两个节点都在同一级别，并且如果我们使用两个节点的父指针向上遍历，则根路径中的第一个公共节点是 lca。
    思路是找出给定节点的深度，通过深度差向上移动更深的节点指针。一旦两个节点达到相同的级别，遍历它们并返回第一个公共节点。

    感谢神秘心灵提出这个方法。

    ## C++

    ```
    // C++ program to find lowest common ancestor using parent pointer
    #include <bits/stdc++.h>
    using namespace std;

    // A Tree Node
    struct Node
    {
        Node *left, *right, *parent;
        int key;
    };

    // A utility function to create a new BST node
    Node *newNode(int item)
    {
        Node *temp = new Node;
        temp->key = item;
        temp->parent = temp->left = temp->right = NULL;
        return temp;
    }

    /* A utility function to insert a new node with
    given key in Binary Search Tree */
    Node *insert(Node *node, int key)
    {
        /* If the tree is empty, return a new node */
        if (node == NULL) return newNode(key);

        /* Otherwise, recur down the tree */
        if (key < node->key)
        {
            node->left = insert(node->left, key);
            node->left->parent = node;
        }
        else if (key > node->key)
        {
            node->right = insert(node->right, key);
            node->right->parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }

    // A utility function to find depth of a node
    // (distance of it from root)
    int depth(Node *node)
    {
        int d = -1;
        while (node)
        {
            ++d;
            node = node->parent;
        }
        return d;
    }

    // To find LCA of nodes n1 and n2 in Binary Tree
    Node *LCA(Node *n1, Node *n2)
    {
        // Find depths of two nodes and differences
        int d1 = depth(n1), d2 = depth(n2);
        int diff = d1 - d2;

        // If n2 is deeper, swap n1 and n2
        if (diff < 0)
        {
            Node * temp = n1;
            n1 = n2;
            n2 = temp;
            diff = -diff;
        }

        // Move n1 up until it reaches the same level as n2
        while (diff--)
            n1 = n1->parent;

        // Now n1 and n2 are at same levels
        while (n1 && n2)
        {
            if (n1 == n2)
                return n1;
            n1 = n1->parent;
            n2 = n2->parent;
        }

        return NULL;
    }

    // Driver method to test above functions
    int main(void)
    {
        Node * root = NULL;

        root = insert(root, 20);
        root = insert(root, 8);
        root = insert(root, 22);
        root = insert(root, 4);
        root = insert(root, 12);
        root = insert(root, 10);
        root = insert(root, 14);

        Node *n1 = root->left->right->left;
        Node *n2 = root->right;

        Node *lca = LCA(n1, n2);
        printf("LCA of %d and %d is %d \n", n1->key, n2->key, lca->key);

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    import java.util.HashMap;
    import java.util.Map;

    // Java program to find lowest common ancestor using parent pointer

    // A tree node
    class Node 
    {
        int key;
        Node left, right, parent;

        Node(int key) 
        {
            this.key = key;
            left = right = parent = null;
        }
    }

    class BinaryTree 
    {
        Node root, n1, n2, lca;

        /* A utility function to insert a new node with
           given key in Binary Search Tree */
        Node insert(Node node, int key) 
        {
            /* If the tree is empty, return a new node */
            if (node == null)
                return new Node(key);

            /* Otherwise, recur down the tree */
            if (key < node.key) 
            {
                node.left = insert(node.left, key);
                node.left.parent = node;
            } 
            else if (key > node.key) 
            {
                node.right = insert(node.right, key);
                node.right.parent = node;
            }

            /* return the (unchanged) node pointer */
            return node;
        }

        // A utility function to find depth of a node
        // (distance of it from root)
        int depth(Node node) 
        {
            int d = -1;
            while (node != null) 
            {
                ++d;
                node = node.parent;
            }
            return d;
        }

        // To find LCA of nodes n1 and n2 in Binary Tree
        Node LCA(Node n1, Node n2) 
        {
            // Find depths of two nodes and differences
            int d1 = depth(n1), d2 = depth(n2);
            int diff = d1 - d2;

            // If n2 is deeper, swap n1 and n2
            if (diff < 0) 
            {
                Node temp = n1;
                n1 = n2;
                n2 = temp;
                diff = -diff;
            }

            // Move n1 up until it reaches the same level as n2
            while (diff-- != 0)
                n1 = n1.parent;

            // Now n1 and n2 are at same levels
            while (n1 != null && n2 != null) 
            {
                if (n1 == n2)
                    return n1;
                n1 = n1.parent;
                n2 = n2.parent;
            }

            return null;
        }

        // Driver method to test above functions
        public static void main(String[] args) 
        {
            BinaryTree tree = new BinaryTree();
            tree.root = tree.insert(tree.root, 20);
            tree.root = tree.insert(tree.root, 8);
            tree.root = tree.insert(tree.root, 22);
            tree.root = tree.insert(tree.root, 4);
            tree.root = tree.insert(tree.root, 12);
            tree.root = tree.insert(tree.root, 10);
            tree.root = tree.insert(tree.root, 14);

            tree.n1 = tree.root.left.right.left;
            tree.n2 = tree.root.right;
            tree.lca = tree.LCA(tree.n1, tree.n2);

            System.out.println("LCA of " + tree.n1.key + " and " + tree.n2.key
                    + " is " + tree.lca.key);
        }
    }

    // This code has been contributed by Mayank Jaiswal(mayank_24)
    ```

    ## C#

    ```
    // C# program to find lowest common 
    // ancestor using parent pointer 
    using System;

    // A tree node 
    public class Node
    {
        public int key;
        public Node left, right, parent;

        public Node(int key)
        {
            this.key = key;
            left = right = parent = null;
        }
    }

    class GFG
    {
    public Node root, n1, n2, lca;

    /* A utility function to insert a new
     node with given key in Binary Search Tree */
    public virtual Node insert(Node node, int key)
    {
        /* If the tree is empty, return 
           a new node */
        if (node == null)
        {
            return new Node(key);
        }

        /* Otherwise, recur down the tree */
        if (key < node.key)
        {
            node.left = insert(node.left, key);
            node.left.parent = node;
        }
        else if (key > node.key)
        {
            node.right = insert(node.right, key);
            node.right.parent = node;
        }

        /* return the (unchanged) node pointer */
        return node;
    }

    // A utility function to find depth of a 
    // node (distance of it from root) 
    public virtual int depth(Node node)
    {
        int d = -1;
        while (node != null)
        {
            ++d;
            node = node.parent;
        }
        return d;
    }

    // To find LCA of nodes n1 and n2 
    // in Binary Tree 
    public virtual Node LCA(Node n1, Node n2)
    {
        // Find depths of two nodes 
        // and differences 
        int d1 = depth(n1), d2 = depth(n2);
        int diff = d1 - d2;

        // If n2 is deeper, swap n1 and n2 
        if (diff < 0)
        {
            Node temp = n1;
            n1 = n2;
            n2 = temp;
            diff = -diff;
        }

        // Move n1 up until it reaches 
        // the same level as n2 
        while (diff-- != 0)
        {
            n1 = n1.parent;
        }

        // Now n1 and n2 are at same levels 
        while (n1 != null && n2 != null)
        {
            if (n1 == n2)
            {
                return n1;
            }
            n1 = n1.parent;
            n2 = n2.parent;
        }

        return null;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        GFG tree = new GFG();
        tree.root = tree.insert(tree.root, 20);
        tree.root = tree.insert(tree.root, 8);
        tree.root = tree.insert(tree.root, 22);
        tree.root = tree.insert(tree.root, 4);
        tree.root = tree.insert(tree.root, 12);
        tree.root = tree.insert(tree.root, 10);
        tree.root = tree.insert(tree.root, 14);

        tree.n1 = tree.root.left.right.left;
        tree.n2 = tree.root.right;
        tree.lca = tree.LCA(tree.n1, tree.n2);

        Console.WriteLine("LCA of " + tree.n1.key +
                          " and " + tree.n2.key + 
                          " is " + tree.lca.key);
    }
    }

    // This code is contributed by Shrikant13
    ```

    **Output :**

    ```
    LCA of 10 and 22 is 20 
    ```

    你可能也想看下面的文章:

    [二叉树中最低的共同祖先|集合 1](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)

    [二叉查找树的最低共同祖先。](https://www.geeksforgeeks.org/lowest-common-ancestor-in-a-binary-search-tree/)

    [使用 RMQ 在二叉树中找到生命周期评价](https://www.geeksforgeeks.org/find-lca-in-binary-tree-using-rmq/)

    本文由 **Dheeraj Gupta** 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论