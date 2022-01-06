# 在二叉树中寻找字典上最小的直径

> 原文:[https://www . geeksforgeeks . org/find-按字典顺序排列的二叉树最小直径/](https://www.geeksforgeeks.org/finding-the-lexicographically-smallest-diameter-in-a-binary-tree/)

给定一个二叉树，其中节点值是小写字母，任务是找到字典上最小的直径。直径是任意两个叶节点之间的最长路径，因此，二叉树中可以有多个直径。任务是打印所有可能直径中字典上最小的直径。

**示例:**

```
Input:          
        a
      /   \
    b       c
  /  \     /  \
 d   e    f    g
Output: Diameter: 5
Lexicographically smallest diameter: d b a c f
Explanation:
Note that there are many other paths 
exist like {d, b, a, c, g}, 
{e, b, a, c, f} and {e, b, a, c, g} 
but {d, b, a, c, f} 
is lexicographically smallest

Input:          
        k
      /   \
    e       s
  /  \       
 g   f    
Output: Diameter: 4
Lexicographically smallest diameter: f e k s
Explanation:
Note that many other paths 
exist like {g, e, k, s} 
{s, k, e, g} and {s, k, e, f} 
but {f, e, k, s} is 
lexicographically smallest

```

**方法:**
方法类似于上一篇文章中讨论的[求径。现在是
打印最大直径和字典最小的最长路径的部分。](https://www.geeksforgeeks.org/diameter-of-a-binary-tree-in-on-a-new-method/)

**步骤:**

*   自定义比较函数返回字典最小向量。
*   维护了六种向量，包括
    *左直径*
    *左直径*右直径
    *节点出现在左高度*
    *节点出现在右高度*
    *节点出现在最大高度*
    *直径向量包括路径出现的节点*
*   其余部分在代码的注释中解释，这里很难用语言解释

下面是上述方法的实现:

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Binary Tree Node
struct node {
    char data;
    node *left, *right;
};

// Utility function to create a new node
node* newNode(char data)
{
    node* c = new node;
    c->data = data;
    c->left = c->right = NULL;
    return c;
}

// Function to compare and return
// lexicographically smallest vector
vector<node*> compare(vector<node*> a, vector<node*> b)
{
    for (int i = 0; i < a.size() && i < b.size(); i++) {
        if (a[i]->data < b[i]->data) {
            return a;
        }
        if (a[i]->data > b[i]->data) {
            return b;
        }
    }

    return a;
}

// Function to find diameter
int diameter(node* root, int& height, vector<node*>& dia,
             vector<node*>& heightv)
{
    // If root is null
    if (!root) {
        height = 0;
        return 0;
    }

    // Left height and right height
    // respectively
    int lh = 0, rh = 0;

    // Left tree diameter and
    // right tree diameter
    int ld, rd;

    vector<node*> leftdia;
    vector<node*> rightdia;
    vector<node*> leftheight;
    vector<node*> rightheight;

    // Left subtree diameter
    ld = diameter(root->left, lh, leftdia, leftheight);

    // Right subtree diameter
    rd = diameter(root->right, rh, rightdia, rightheight);

    // If left height is more
    // than right tree height
    if (lh > rh) {

        // Add current root so lh + 1
        height = lh + 1;

        // Change vector heightv to leftheight
        heightv = leftheight;

        // Insert current root in the path
        heightv.push_back(root);
    }

    // If right height is
    // more than left tree height
    else if (rh > lh) {

        // Add current root so rh + 1
        height = rh + 1;

        // Change vector heightv to rightheight
        heightv = rightheight;

        // Insert current root in the path
        heightv.push_back(root);
    }

    // Both height same compare
    // lexicographically now
    else {

        // Add current root so rh + 1
        height = rh + 1;

        // Lexigcographical comparison between two vectors
        heightv = compare(leftheight, rightheight);

        // Insert current root in the path
        heightv.push_back(root);
    }

    // If distance of one leaf node to another leaf
    // containing the root is more than the left
    // diameter and right diameter
    if (lh + rh + 1 > max(ld, rd)) {

        // Make dia equal to leftheight
        dia = leftheight;

        // Add current root into it
        dia.push_back(root);

        for (int j = rightheight.size() - 1; j >= 0; j--) {
            // Add right tree (right to root) nodes
            dia.push_back(rightheight[j]);
        }
    }

    // If either leftdiameter containing the left
    // subtree and root or rightdiameter containg
    // the right subtree and root is more than
    // above lh+rh+1
    else {

        // If diameter of left tree is
        // greater our answer vector i.e
        // dia is equal to leftdia then
        if (ld > rd) {
            dia = leftdia;
        }

        // If both diameter
        // same check lexicographically
        else if (ld == rd) {
            dia = compare(leftdia, rightdia);
        }

        // If diameter of right tree
        // is greater our answer vector
        // i.e dia is equal to rightdia then
        else {
            dia = rightdia;
        }
    }

    return dia.size();
}

// Driver code
int main()
{
    node* root = newNode('a');
    root->left = newNode('b');
    root->right = newNode('c');
    root->left->left = newNode('d');
    root->left->right = newNode('e');
    root->right->left = newNode('f');
    root->right->right = newNode('g');

    int height = 0;
    vector<node *> dia, heigh;
    cout << "Diameter is: " << diameter(root, height,
                                        dia, heigh)
         << endl;

    // Printing the lexicographically smallest diameter
    cout << "Lexicographically smallest diameter:" << endl;
    for (int j = 0; j < dia.size(); j++) {
        cout << dia[j]->data << " ";
    }

    return 0;
}
```

**Output:**

```
Diameter is: 5
Lexicographically smallest diameter:
d b a c f

```