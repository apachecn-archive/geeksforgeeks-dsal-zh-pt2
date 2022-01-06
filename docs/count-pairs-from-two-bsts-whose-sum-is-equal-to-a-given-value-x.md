# 从两个总和等于给定值 x 的 BST 中计数配对

> 原文:[https://www . geesforgeks . org/count-pairs-from-two-BST-其和等于给定值-x/](https://www.geeksforgeeks.org/count-pairs-from-two-bsts-whose-sum-is-equal-to-a-given-value-x/)

给定两个分别包含 **n1** 和 **n2** 不同节点的 BST。给定值 **x** 。问题是计算两个 BST 中总和等于 **x** 的所有对。

**示例:**

```
Input : BST 1:    5        
                /   \      
               3     7      
              / \   / \    
             2  4  6   8   

        BST 2:    10        
                /   \      
               6     15      
              / \   /  \    
             3  8  11  18
        x = 16

Output : 3
The pairs are:
(5, 11), (6, 10) and (8, 8)
```

**方法 1:** 对于 BST 1 中的每个节点值 **a** ，搜索 BST 2 中的值**(x–a)**。如果找到值，则增加**计数**。要在 BST 中搜索值，请参考[这篇](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)文章。
时间复杂度:O(n1 * h2)，这里 n1 是第一个 BST 中的节点数，h2 是第二个 BST 的高度。

**方法二:**从最小值到节点到最大值遍历 BST 1。这可以通过[迭代遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)来实现。从最大值节点到最小值节点遍历 BST 2。这可以通过反向有序遍历来实现。同时执行这两次遍历。在一个特定的遍历实例中，总结两个 BSt 中相应节点的值。如果总和== x，则增加**计数**。如果 x >相加，则移到 BST 1 当前节点的前一个后继节点，否则移到 BST 2 当前节点的前一个后继节点。执行这些操作，直到两个遍历中的任何一个完成。

## C++

```
// C++ implementation to count pairs from two
// BSTs whose sum is equal to a given  value x
#include <bits/stdc++.h>
using namespace std;

// structure of a node of BST
struct Node {
    int data;
    Node* left, *right;
};

// function to create and return a node of BST
Node* getNode(int data)
{
    // allocate space for the node
    Node* new_node = (Node*)malloc(sizeof(Node));

    // put in the data
    new_node->data = data;
    new_node->left = new_node->right = NULL;
}

// function to count pairs from two BSTs
// whose sum is equal to a given value x
int countPairs(Node* root1, Node* root2, int x)
{
    // if either of the tree is empty
    if (root1 == NULL || root2 == NULL)
        return 0;

    // stack 'st1' used for the inorder
    // traversal of BST 1
    // stack 'st2' used for the reverse
    // inorder traversal of BST 2
    stack<Node*> st1, st2;
    Node* top1, *top2;

    int count = 0;

    // the loop will break when either of two
    // traversals gets completed
    while (1) {

        // to find next node in inorder
        // traversal of BST 1
        while (root1 != NULL) {
            st1.push(root1);
            root1 = root1->left;
        }

        // to find next node in reverse
        // inorder traversal of BST 2
        while (root2 != NULL) {
            st2.push(root2);
            root2 = root2->right;
        }

        // if either gets empty then corresponding
        // tree traversal is completed
        if (st1.empty() || st2.empty())
            break;

        top1 = st1.top();
        top2 = st2.top();

        // if the sum of the node's is equal to 'x'
        if ((top1->data + top2->data) == x) {
            // increment count
            count++;

            // pop nodes from the respective stacks
            st1.pop();
            st2.pop();

            // insert next possible node in the
            // respective stacks
            root1 = top1->right;
            root2 = top2->left;
        }

        // move to next possible node in the
        // inorder traversal of BST 1
        else if ((top1->data + top2->data) < x) {
            st1.pop();
            root1 = top1->right;
        }

        // move to next possible node in the
        // reverse inorder traversal of BST 2
        else {
            st2.pop();
            root2 = top2->left;
        }
    }

    // required count of pairs
    return count;
}

// Driver program to test above
int main()
{
    // formation of BST 1
    Node* root1 = getNode(5); /*             5        */
    root1->left = getNode(3); /*           /   \      */
    root1->right = getNode(7); /*         3     7     */
    root1->left->left = getNode(2); /*    / \   / \    */
    root1->left->right = getNode(4); /*  2  4  6  8    */
    root1->right->left = getNode(6);
    root1->right->right = getNode(8);

    // formation of BST 2
    Node* root2 = getNode(10); /*           10         */
    root2->left = getNode(6); /*           /   \        */
    root2->right = getNode(15); /*        6     15      */
    root2->left->left = getNode(3); /*    / \   /  \     */
    root2->left->right = getNode(8); /*  3  8  11  18    */
    root2->right->left = getNode(11);
    root2->right->right = getNode(18);

    int x = 16;
    cout << "Pairs = "
         << countPairs(root1, root2, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count pairs from two
// BSTs whose sum is equal to a given  value x
import java.util.Stack;
public class GFG {

    // structure of a node of BST
    static class Node {
        int data;
        Node left, right;

        // constructor
        public Node(int data) {
            this.data = data;
            left = null;
            right = null;
        }
    }

    static Node root1;
    static Node root2;
    // function to count pairs from two BSTs
    // whose sum is equal to a given value x
    static int countPairs(Node root1, Node root2,
                                           int x)
    {
        // if either of the tree is empty
        if (root1 == null || root2 == null)
            return 0;

        // stack 'st1' used for the inorder
        // traversal of BST 1
        // stack 'st2' used for the reverse
        // inorder traversal of BST 2
        //stack<Node*> st1, st2;
        Stack<Node> st1 = new Stack<>();
        Stack<Node> st2 = new Stack<>();
        Node top1, top2;

        int count = 0;

        // the loop will break when either of two
        // traversals gets completed
        while (true) {

            // to find next node in inorder
            // traversal of BST 1
            while (root1 != null) {
                st1.push(root1);
                root1 = root1.left;
            }

            // to find next node in reverse
            // inorder traversal of BST 2
            while (root2 != null) {
                st2.push(root2);
                root2 = root2.right;
            }

            // if either gets empty then corresponding
            // tree traversal is completed
            if (st1.empty() || st2.empty())
                break;

            top1 = st1.peek();
            top2 = st2.peek();

            // if the sum of the node's is equal to 'x'
            if ((top1.data + top2.data) == x) {
                // increment count
                count++;

                // pop nodes from the respective stacks
                st1.pop();
                st2.pop();

                // insert next possible node in the
                // respective stacks
                root1 = top1.right;
                root2 = top2.left;
            }

            // move to next possible node in the
            // inorder traversal of BST 1
            else if ((top1.data + top2.data) < x) {
                st1.pop();
                root1 = top1.right;
            }

            // move to next possible node in the
            // reverse inorder traversal of BST 2
            else {
                st2.pop();
                root2 = top2.left;
            }
        }

        // required count of pairs
        return count;
    }

    // Driver program to test above
    public static void main(String args[])
    {
        // formation of BST 1
        root1 = new Node(5);       /*             5        */
        root1.left = new Node(3); /*           /   \      */
        root1.right = new Node(7); /*         3     7     */
        root1.left.left = new Node(2); /*    / \   / \    */
        root1.left.right = new Node(4); /*  2   4 6   8    */
        root1.right.left = new Node(6);
        root1.right.right = new Node(8);

        // formation of BST 2
        root2 = new Node(10);        /*           10         */
        root2.left = new Node(6); /*           /   \        */
        root2.right = new Node(15); /*        6     15      */
        root2.left.left = new Node(3); /*    / \   /  \     */
        root2.left.right = new Node(8); /*  3  8  11  18    */
        root2.right.left = new Node(11);
        root2.right.right = new Node(18);

        int x = 16;
        System.out.println("Pairs = "
             + countPairs(root1, root2, x));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 implementation to count pairs
# from two BSTs whose sum is equal to a
# given  value x

# Structure of a node of BST
class getNode:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function to count pairs from two BSTs
# whose sum is equal to a given value x
def countPairs(root1, root2, x):

    # If either of the tree is empty
    if (root1 == None or root2 == None):
        return 0

    # Stack 'st1' used for the inorder
    # traversal of BST 1
    # stack 'st2' used for the reverse
    # inorder traversal of BST 2
    st1 = []
    st2 = []

    count = 3

    # The loop will break when either
    # of two traversals gets completed
    while (1):

        # To find next node in inorder
        # traversal of BST 1
        while (root1 != None):
            st1.append(root1)
            root1 = root1.left

        # To find next node in reverse
        # inorder traversal of BST 2
        while (root2 != None):
            st2.append(root2)
            root2 = root2.right

        # If either gets empty then corresponding
        # tree traversal is completed
        if (len(st1) or len(st2)):
            break

        top1 = st1[len(st1) - 1]
        top2 = st2[len(st2) - 1]

        # If the sum of the node's is equal to 'x'
        if ((top1.data + top2.data) == x):

            # Increment count
            count += 1

            # Pop nodes from the respective stacks
            st1.remove(st1[len(st1) - 1])
            st2.remove(st2[len(st2) - 1])

            # Insert next possible node in the
            # respective stacks
            root1 = top1.right
            root2 = top2.left

        # Move to next possible node in the
        # inorder traversal of BST 1
        elif ((top1.data + top2.data) < x):
            st1.remove(st1[len(st1) - 1])
            root1 = top1.right

        # Move to next possible node in the
        # reverse inorder traversal of BST 2
        else:
            st2.remove(st2[len(st2) - 1])
            root2 = top2.left

    # Required count of pairs
    return count

# Driver code
if __name__ == '__main__':

    # Formation of BST 1
    '''      5
           /   \ 
          3     7
         / \   / \
        2   4 6   8
    '''
    root1 = getNode(5) 
    root1.left = getNode(3)
    root1.right = getNode(7)
    root1.left.left = getNode(2)
    root1.left.right = getNode(4)
    root1.right.left = getNode(6)
    root1.right.right = getNode(8)

    # Formation of BST 2
    '''    10 
         /   \
        6     15
       / \   /  \ 
      3  8  11  18
    '''
    root2 = getNode(10)
    root2.left = getNode(6)
    root2.right = getNode(15)
    root2.left.left = getNode(3)
    root2.left.right = getNode(8)
    root2.right.left = getNode(11)
    root2.right.right = getNode(18)

    x = 16

    print("Pairs = ", countPairs(root1, root2, x))

# This code is contributed by bgangwar59
```

## C#

```
// C# implementation to count pairs from two
// BSTs whose sum is equal to a given  value x
using System;
using System.Collections.Generic;

// C# implementation to count pairs from two
// BSTs whose sum is equal to a given  value x
public class GFG
{

    // structure of a node of BST
    public class Node
    {
        public int data;
        public Node left, right;

        // constructor
        public Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }

    public static Node root1;
    public static Node root2;
    // function to count pairs from two BSTs
    // whose sum is equal to a given value x
    public static int countPairs(Node root1, Node root2, int x)
    {
        // if either of the tree is empty
        if (root1 == null || root2 == null)
        {
            return 0;
        }

        // stack 'st1' used for the inorder
        // traversal of BST 1
        // stack 'st2' used for the reverse
        // inorder traversal of BST 2
        //stack<Node*> st1, st2;
        Stack<Node> st1 = new Stack<Node>();
        Stack<Node> st2 = new Stack<Node>();
        Node top1, top2;

        int count = 0;

        // the loop will break when either of two
        // traversals gets completed
        while (true)
        {

            // to find next node in inorder
            // traversal of BST 1
            while (root1 != null)
            {
                st1.Push(root1);
                root1 = root1.left;
            }

            // to find next node in reverse
            // inorder traversal of BST 2
            while (root2 != null)
            {
                st2.Push(root2);
                root2 = root2.right;
            }

            // if either gets empty then corresponding
            // tree traversal is completed
            if (st1.Count == 0 || st2.Count == 0)
            {
                break;
            }

            top1 = st1.Peek();
            top2 = st2.Peek();

            // if the sum of the node's is equal to 'x'
            if ((top1.data + top2.data) == x)
            {
                // increment count
                count++;

                // pop nodes from the respective stacks
                st1.Pop();
                st2.Pop();

                // insert next possible node in the
                // respective stacks
                root1 = top1.right;
                root2 = top2.left;
            }

            // move to next possible node in the
            // inorder traversal of BST 1
            else if ((top1.data + top2.data) < x)
            {
                st1.Pop();
                root1 = top1.right;
            }

            // move to next possible node in the
            // reverse inorder traversal of BST 2
            else
            {
                st2.Pop();
                root2 = top2.left;
            }
        }

        // required count of pairs
        return count;
    }

    // Driver program to test above
    public static void Main(string[] args)
    {
        // formation of BST 1
        root1 = new Node(5); //             5
        root1.left = new Node(3); //           /   \
        root1.right = new Node(7); //         3     7
        root1.left.left = new Node(2); //    / \   / \
        root1.left.right = new Node(4); //  2   4 6   8
        root1.right.left = new Node(6);
        root1.right.right = new Node(8);

        // formation of BST 2
        root2 = new Node(10); //           10
        root2.left = new Node(6); //           /   \
        root2.right = new Node(15); //        6     15
        root2.left.left = new Node(3); //    / \   /  \
        root2.left.right = new Node(8); //  3  8  11  18
        root2.right.left = new Node(11);
        root2.right.right = new Node(18);

        int x = 16;
        Console.WriteLine("Pairs = " + countPairs(root1, root2, x));
    }
}

  // This code is contributed by Shrikant13
```

**Output**

```
Pairs = 3
```

**时间复杂度:**O(n1+N2)
T3】辅助空间: O(h1 + h2)其中 h1 为第一棵树的高度，h2 为第二棵树的高度

**方法 3 :**

1.  解决这个问题的递归方法。
2.  遍历 BST1，为每个节点找到 BST2 中的差异(即 x–root 1 . data)，并增加计数。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count pairs from two
// BSTs whose sum is equal to a given  value x
import java.util.Stack;
public class GFG {

    // structure of a node of BST
    static class Node {
        int data;
        Node left, right;

        // constructor
        public Node(int data)
        {
            this.data = data;
            left = null;
            right = null;
        }
    }

    static Node root1;
    static Node root2;

    // function to count pairs from two BSTs
    // whose sum is equal to a given value x
    public static int pairCount = 0;
    public static void traverseTree(Node root1, Node root2,
                                    int sum)
    {
        if (root1 == null || root2 == null) {
            return;
        }
        traverseTree(root1.left, root2, sum);
        traverseTree(root1.right, root2, sum);
        int diff = sum - root1.data;
        findPairs(root2, diff);
    }

    private static void findPairs(Node root2, int diff)
    {
        if (root2 == null) {
            return;
        }
        if (diff > root2.data) {
            findPairs(root2.right, diff);
        }
        else {
            findPairs(root2.left, diff);
        }
        if (root2.data == diff) {
            pairCount++;
        }
    }

    public static int countPairs(Node root1, Node root2,
                                 int sum)
    {
        traverseTree(root1, root2, sum);
        return pairCount;
    }

    // Driver program to test above
    public static void main(String args[])
    {
        // formation of BST 1
        root1 = new Node(5); /*             5        */
        root1.left = new Node(3); /*           /   \      */
        root1.right = new Node(7); /*         3     7     */
        root1.left.left = new Node(2); /*    / \   / \    */
        root1.left.right = new Node(4); /*  2   4 6   8 */
        root1.right.left = new Node(6);
        root1.right.right = new Node(8);

        // formation of BST 2
        root2 = new Node(10); /*           10         */
        root2.left = new Node(6); /*           /   \ */
        root2.right = new Node(15); /*        6     15 */
        root2.left.left = new Node(3); /*    / \   /  \ */
        root2.left.right
            = new Node(8); /*  3  8  11  18    */
        root2.right.left = new Node(11);
        root2.right.right = new Node(18);

        int x = 16;
        System.out.println("Pairs = "
                           + countPairs(root1, root2, x));
    }
}
// This code is contributed by Sujit Panda
```

**Output**

```
Pairs = 3
```

**方法 4:使用 BinarySearch 树迭代器(一种更通用的方法)**

创建两个类，一个作为*迭代器 1* ，另一个作为*迭代器 2* 。这两个类分别对应于*到*和反向*到*的遍历。

每个类都有三种方法–

*   **有下一个**:当遍历尚未完成时将返回真
*   **下一个**:将指针移动到下一个节点
*   **peek** :将返回遍历中的当前节点

在创建了两个这样的类之后，简单地运行迭代器，同时两者都有下一个节点并找到总和。如果 sum == x，递增迭代器 1 和迭代器 2 的下一个指针，如果 sum > x，递增迭代器 2 的下一个指针，否则递增迭代器 1 的下一个指针，即当 sum < x 时。

*下面是 java 中的代码。*

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
class Node{
    int data;
      Node left, right;
       public Node(int data){
        this.data = data;
          this.left = null;
          this.right = null;
    }
}
// inorder successor iterator
class BSTIterator1{
    Stack<Node> s1 = new Stack<>();
    Node root1;
    boolean hasPeeked = false;
    public BSTIterator1(Node root){
        this.root1 = root;
    }
    public boolean hasNext(){
        if(!s1.isEmpty() || root1!=null)
            return true;
        return false;
    }
    public Node peek(){
        if(!hasNext())
            return null;
        while(root1!=null){
            s1.push(root1);
            root1 = root1.left;
            hasPeeked = true;
        }
        return s1.peek();
    }
    public int next(){
        if(!hasNext())
            return -1;
        if(!hasPeeked)
            peek();
        hasPeeked = false;
        root1 = s1.pop();
        Node temp = root1;
        root1 = root1.right;
        return temp.data;
    }
}
// inorder predecessor iterator
class BSTIterator2{
    Stack<Node> s1 = new Stack<>();
    Node root1;
    boolean hasPeeked = false;
    public BSTIterator2(Node root){
        this.root1 = root;
    }
    public boolean hasNext(){
        if(!s1.isEmpty() || root1!=null)
            return true;
        return false;
    }
    public Node peek(){
        if(!hasNext())
            return null;
        while(root1!=null){
            s1.push(root1);
            root1 = root1.right;
            hasPeeked = true;
        }
        return s1.peek();
    }
    public int next(){
        if(!hasNext())
            return -1;
        if(!hasPeeked)
            peek();
        hasPeeked = false;
        root1 = s1.pop();
        Node temp = root1;
        root1 = root1.left;
        return temp.data;
    }
}
class GfG
{  
    public static int countPairs(Node r1, Node r2, int x)
    {

        BSTIterator1 it1 = new BSTIterator1(r1);
        BSTIterator2 it2 = new BSTIterator2(r2);
        int count = 0;
        while(it1.hasNext() && it2.hasNext()){
            Node n1 = it1.peek();
            Node n2 = it2.peek();
            int sum = n1.data+n2.data;
            if(sum == x){
                count++;
                it1.next();
                it2.next();
            }
            else if(sum > x){
                it2.next();
            }else{
                it1.next();
            }
        }
        return count;

    }
   // Driver program to test above
    public static void main(String args[])
    {
        Node root1, root2;
          // formation of BST 1
        root1 = new Node(5); /*                     5        */
        root1.left = new Node(3); /*           /   \      */
        root1.right = new Node(7); /*         3     7     */
        root1.left.left = new Node(2); /*    / \   / \    */
        root1.left.right = new Node(4); /*  2   4 6   8   */
        root1.right.left = new Node(6);
        root1.right.right = new Node(8);

        // formation of BST 2
        root2 = new Node(10); /*                   10      */
        root2.left = new Node(6); /*           /   \    */
        root2.right = new Node(15); /*        6     15  */
        root2.left.left = new Node(3); /*    / \   /  \ */
        root2.left.right
            = new Node(8); /*  3  8  11  18    */
        root2.right.left = new Node(11);
        root2.right.right = new Node(18);

        int x = 16;
        System.out.println("Pairs = "
                           + countPairs(root1, root2, x));
    }
}
```

**Output**

```
Pairs = 3
```

**时间复杂度** : O(n1 + n2)

**辅助空间** : O(h1 + h2)其中 h1 为第一棵树的高度，h2 为第二棵树的高度