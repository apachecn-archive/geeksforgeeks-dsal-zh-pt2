# 在二叉树中找到从根到链表的路径方向

> 原文:[https://www . geeksforgeeks . org/find-路径方向-由二叉树中的链表从根跟随/](https://www.geeksforgeeks.org/find-direction-of-path-followed-from-root-by-a-linked-list-in-a-binary-tree/)

给定[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/) **T** 的根和[链表](https://www.geeksforgeeks.org/data-structures/linked-list/) **L** ，任务是找到从根跟随的路径方向，使得存在从根到树的任何叶节点的[路径](https://www.geeksforgeeks.org/given-a-binary-tree-print-all-root-to-leaf-paths/)，使得该路径的值形成链表。如果不存在这样的路径，则打印**-1”**。

**注意:**向左走的路径用 **L** 表示，向右走的路径用 **R** 表示。

**示例**:

> **输入:**LL = 1->2->5->8
> 1
> /\
> 2 3
> /\/\
> 4 5 6 8
> /
> 8
> **输出:** L R L
> **说明:**
> 二叉树中链表的路径如下:
> **1**
> t2t
> 
> **输入:**LL = 1->2->4
> 1
> /\
> 2 2
> /\
> 4 5 6 8
> /
> 8
> **输出:** {L，L}

**方法:**给定的问题可以通过[同时遍历二叉树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)和[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)来解决，如果当前节点与链表的当前节点不匹配，则该路径不正确。否则，检查有效路径的其他顺序。按照以下步骤解决给定的问题:

*   声明一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，说 **findPath(根，头，路径)**，在这个函数中执行以下步骤:
    *   如果根为**空**或者根的值与头的节点值不相同，则返回**假**。
    *   如果当前根节点是叶节点，头节点是最后一个节点，则返回 **true** 。
    *   在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **路径中插入字符**【L】****[递归调用左子树的](https://www.geeksforgeeks.org/recursion/)作为 **findPath(根- >左，头- >下一个，路径)**，如果该函数返回的值为 **true** ，则存在一个路径，并且[从函数](https://www.geeksforgeeks.org/return-statement-in-c-cpp-with-examples/)返回 **true** 。否则，从矢量**路径[]** 弹出最后一个字符。
    *   在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **路径中插入字符**【R】****[递归调用右子树的](https://www.geeksforgeeks.org/recursion/)作为 **findPath(root- > right，head- > next，path)** ，如果该函数返回的值为 **true** ，则存在一个路径，[从函数](https://www.geeksforgeeks.org/return-statement-in-c-cpp-with-examples/)返回 **true** 。否则，从矢量**路径[]** 弹出最后一个字符。
    *   否则，从功能中返回 **false** 。
*   初始化一个向量，比如说**路径[]** ，如果在给定的二叉树中找到链表，则该向量存储方向。
*   调用函数**查找路径(根，头，路径)**。
*   如果向量路径的[大小为 **0** ，则打印 **"-1"** 。否则，打印矢量**路径[]** 中存储的路径。](https://www.geeksforgeeks.org/vectorempty-vectorsize-c-stl/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int data;
    ListNode* next;
    ListNode(int data)
    {
        this->data = data;
        this->next = NULL;
    }
};

struct TreeNode {
    TreeNode* left;
    TreeNode* right;
    int val;

    TreeNode(int x)
        : left(NULL), right(NULL), val(x)
    {
    }
};

// Function to create the Linked list
ListNode* makeList(int arr[], int n)
{
    ListNode* h = NULL;
    ListNode* root;
    for (int i = 0; i < n; i++) {
        int data = arr[i];
        ListNode* node = new ListNode(data);

        if (h == NULL) {
            h = node;
            root = h;
        }
        else {
            root->next = node;
            root = node;
        }
    }
    return h;
}

// utility function to build tree
// from its level order traversal
TreeNode* build_tree(int nodes[], int n)
{
    TreeNode* root = new TreeNode(nodes[0]);
    queue<TreeNode*> q;
    bool is_left = true;
    TreeNode* cur = NULL;
    q.push(root);

    for (int i = 1; i < n; i++) {
        TreeNode* node = NULL;
        if (nodes[i] != '#') {
            node = new TreeNode(nodes[i]);
            q.push(node);
        }

        if (is_left) {
            cur = q.front();
            q.pop();
            cur->left = node;
            is_left = false;
        }
        else {
            cur->right = node;
            is_left = true;
        }
    }

    return root;
}

// Function to find path of linked list
// in binary tree, by traversing the
// tree in pre-order fashion
bool findPath(TreeNode* root, ListNode* head,
              vector<char>& path)
{
    // Base Case
    if (root == NULL) {
        return false;
    }

    // If current tree node is not same
    // as the current LL Node, then
    // return False
    if (root->val != head->data)
        return false;

    // Complete the path of LL is traced
    if (root->left == NULL
        and root->right == NULL
        and head->next == NULL) {
        return true;
    }

    // First go to left
    path.push_back('L');

    // If path found in left subtree
    if (findPath(root->left,
                 head->next, path))
        return true;

    // Pop L because valid path is
    // not traced
    path.pop_back();

    // Go to right
    path.push_back('R');

    // If path found in right subtree
    if (findPath(root->right,
                 head->next, path))
        return true;

    // Pop R because valid path
    // is not traced
    path.pop_back();

    return false;
}

// Function to find the valid path
void find(TreeNode* root, ListNode* head)
{
    vector<char> path;

    // Function call to find the direction
    // of the LL path
    findPath(root, head, path);

    // If there doesn't exists any
    // such paths
    if (path.size() == 0) {
        cout << "-1";
        return;
    }

    // Print the path
    for (int i = 0;
         i < path.size(); i++) {
        cout << path[i] << " ";
    }
}

// Driver Code
int main()
{
    int tree[] = { 1, 2, 3, 4, 5, 6,
                   8, -1, -1, 8 };
    TreeNode* root = build_tree(tree, 10);

    int ll[] = { 1, 2, 5, 8 };
    ListNode* head = makeList(ll, 4);

    find(root, head);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static class ListNode {
    int data;
    ListNode next;
    ListNode(int data)
    {
        this.data = data;
        this.next = null;
    }
};

static class TreeNode {
    TreeNode left;
    TreeNode right;
    int val;

    TreeNode(int x){
        left = null;
        right = null;
        val = x;   
    }
};

// Function to create the Linked list
static ListNode makeList(int arr[], int n)
{
    ListNode h = null;
    ListNode root = new ListNode(0);
    for (int i = 0; i < n; i++) {
        int data = arr[i];
        ListNode node = new ListNode(data);

        if (h == null) {
            h = node;
            root = h;
        }
        else {
            root.next = node;
            root = node;
        }
    }
    return h;
}

// utility function to build tree
// from its level order traversal
static TreeNode build_tree(int nodes[], int n)
{
    TreeNode root = new TreeNode(nodes[0]);
    Queue<TreeNode> q = new LinkedList<>();
    boolean is_left = true;
    TreeNode cur = null;
    q.add(root);

    for (int i = 1; i < n; i++) {
        TreeNode node = null;
        if (nodes[i] != 0) {
            node = new TreeNode(nodes[i]);
            q.add(node);
        }

        if (is_left) {
            cur = q.peek();
            q.remove();
            cur.left = node;
            is_left = false;
        }
        else {
            cur.right = node;
            is_left = true;
        }
    }

    return root;
}

// Function to find path of linked list
// in binary tree, by traversing the
// tree in pre-order fashion
static boolean findPath(TreeNode root, ListNode head,
              Vector<Character> path)
{
    // Base Case
    if (root == null) {
        return false;
    }

    // If current tree node is not same
    // as the current LL Node, then
    // return False
    if (root.val != head.data)
        return false;

    // Complete the path of LL is traced
    if (root.left == null
        && root.right == null
        && head.next == null) {
        return true;
    }

    // First go to left
    path.add('L');

    // If path found in left subtree
    if (findPath(root.left,
                 head.next, path))
        return true;

    // Pop L because valid path is
    // not traced
    path.remove(path.size()-1);

    // Go to right
    path.add('R');

    // If path found in right subtree
    if (findPath(root.right,
                 head.next, path))
        return true;

    // Pop R because valid path
    // is not traced
    path.remove(path.size()-1);

    return false;
}

// Function to find the valid path
static void find(TreeNode root, ListNode head)
{
    Vector<Character> path = new Vector<Character>();

    // Function call to find the direction
    // of the LL path
    findPath(root, head, path);

    // If there doesn't exists any
    // such paths
    if (path.size() == 0) {
        System.out.print("-1");
        return;
    }

    // Print the path
    for (int i = 0;
         i < path.size(); i++) {
        System.out.print(path.get(i)+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int tree[] = { 1, 2, 3, 4, 5, 6,
                   8, -1, -1, 8 };
    TreeNode root = build_tree(tree, 10);

    int ll[] = { 1, 2, 5, 8 };
    ListNode head = makeList(ll, 4);

    find(root, head);

}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

class ListNode {
    public int data;
    public ListNode next;
    public ListNode(int data)
    {
        this.data = data;
        this.next = null;
    }
};

class TreeNode {
    public TreeNode left;
    public TreeNode right;
    public int val;

    public TreeNode(int x){
        left = null;
        right = null;
        val = x;   
    }
};

// Function to create the Linked list
static ListNode makeList(int []arr, int n)
{
    ListNode h = null;
    ListNode root = new ListNode(0);
    for (int i = 0; i < n; i++) {
        int data = arr[i];
        ListNode node = new ListNode(data);

        if (h == null) {
            h = node;
            root = h;
        }
        else {
            root.next = node;
            root = node;
        }
    }
    return h;
}

// utility function to build tree
// from its level order traversal
static TreeNode build_tree(int []nodes, int n)
{
    TreeNode root = new TreeNode(nodes[0]);
    Queue<TreeNode> q = new Queue<TreeNode>();
    bool is_left = true;
    TreeNode cur = null;
    q.Enqueue(root);

    for (int i = 1; i < n; i++) {
        TreeNode node = null;
        if (nodes[i] != 0) {
            node = new TreeNode(nodes[i]);
            q.Enqueue(node);
        }

        if (is_left) {
            cur = q.Peek();
            q.Dequeue();
            cur.left = node;
            is_left = false;
        }
        else {
            cur.right = node;
            is_left = true;
        }
    }

    return root;
}

// Function to find path of linked list
// in binary tree, by traversing the
// tree in pre-order fashion
static bool findPath(TreeNode root, ListNode head,
              List<char> path)
{

    // Base Case
    if (root == null) {
        return false;
    }

    // If current tree node is not same
    // as the current LL Node, then
    // return False
    if (root.val != head.data)
        return false;

    // Complete the path of LL is traced
    if (root.left == null
        && root.right == null
        && head.next == null) {
        return true;
    }

    // First go to left
    path.Add('L');

    // If path found in left subtree
    if (findPath(root.left,
                 head.next, path))
        return true;

    // Pop L because valid path is
    // not traced
    path.RemoveAt(path.Count-1);

    // Go to right
    path.Add('R');

    // If path found in right subtree
    if (findPath(root.right,
                 head.next, path))
        return true;

    // Pop R because valid path
    // is not traced
    path.RemoveAt(path.Count-1);

    return false;
}

// Function to find the valid path
static void find(TreeNode root, ListNode head)
{
    List<char> path = new List<char>();

    // Function call to find the direction
    // of the LL path
    findPath(root, head, path);

    // If there doesn't exists any
    // such paths
    if (path.Count == 0) {
        Console.Write("-1");
        return;
    }

    // Print the path
    for (int i = 0;
         i < path.Count; i++) {
        Console.Write(path[i]+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []tree = { 1, 2, 3, 4, 5, 6,
                   8, -1, -1, 8 };
    TreeNode root = build_tree(tree, 10);

    int []ll = { 1, 2, 5, 8 };
    ListNode head = makeList(ll, 4);

    find(root, head);

}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
L R L
```

***时间复杂度:** O(N + M)，其中 N 为二叉树的节点数，M 为链表* *的* [*长度。*
***辅助空间:** O(H)，其中 H 为*](https://www.geeksforgeeks.org/find-length-of-a-linked-list-iterative-and-recursive/) [*二叉树的高度*](https://www.geeksforgeeks.org/write-a-c-program-to-find-the-maximum-depth-or-height-of-a-tree/) *。*T21】