# 两个直接子节点都是其主要因子的节点数

> 原文:[https://www . geeksforgeeks . org/其两个直系子女都是其主要因素的节点数/](https://www.geeksforgeeks.org/count-of-nodes-whose-both-immediate-children-are-its-prime-factors/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印同时拥有两个子节点的节点数，并且这两个子节点都是它的主要因素。
**例:**

```
Input: 
                  1
                /   \ 
              15     20
             /  \   /  \ 
            3    5 4     2 
                    \    / 
                     2  3  
Output: 1
Explanation: 
Children of 15 (3, 5) are prime factors of 15

Input:
                  7
                /  \ 
              210   14 
             /  \      \
            70   14     30
           / \         / \
          2   5       3   5
                      /
                     23 
Output: 2
Explanation: 
Children of 70 (2, 5) are prime factors of 70
Children of 30 (3, 5) are prime factors of 30
```

**进场:**

1.  遍历给定的二叉树，对于每个节点，检查两个子节点是否存在。
2.  如果两个子节点都存在，检查每个子节点是否是该节点的主要因素。
3.  记录这些节点的数量，并在最后打印出来。
4.  为了检查一个因子是否是质数，我们将使用 screen 来预计算质数，以便在 O(1)中进行检查。

下面是上述方法的实现。

## C++

```
// C++ program for Counting nodes
// whose immediate children are its factors

#include <bits/stdc++.h>
using namespace std;

int N = 1000000;

// To store all prime numbers
vector<int> prime;

void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..N]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    bool check[N + 1];
    memset(check, true, sizeof(check));

    for (int p = 2; p * p <= N; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (check[p] == true) {

            prime.push_back(p);

            // Update all multiples of p
            // greater than or equal to
            // the square of it
            // numbers which are multiples of p
            // and are less than p^2
            // are already marked.
            for (int i = p * p; i <= N; i += p)
                check[i] = false;
        }
    }
}

// A Tree node
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

// function to check and print if
// immediate children of a node
// are its factors or not
bool areChilrenPrimeFactors(struct Node* parent,
                            struct Node* a,
                            struct Node* b)
{
    if (prime[a->key] && prime[b->key]
        && (parent->key % a->key == 0
            && parent->key % b->key == 0))
        return true;
    else
        return false;
}

// Function to get the count of full Nodes in
// a binary tree
unsigned int getCount(struct Node* node)
{
    // If tree is empty
    if (!node)
        return 0;
    queue<Node*> q;

    // Initialize count of ful/l nodes
    // having children as their factors
    int count = 0;

    // Do level order traversal
    // starting from root
    q.push(node);
    while (!q.empty()) {
        struct Node* temp = q.front();
        q.pop();

        if (temp->left && temp->right) {
            if (areChilrenPrimeFactors(
                    temp, temp->left,
                    temp->right))
                count++;
        }

        if (temp->left != NULL)
            q.push(temp->left);
        if (temp->right != NULL)
            q.push(temp->right);
    }
    return count;
}

// Function to find total no of nodes
// In a given binary tree
int findSize(struct Node* node)
{
    // Base condition
    if (node == NULL)
        return 0;

    return 1
           + findSize(node->left)
           + findSize(node->right);
}

// Driver Code
int main()
{
    /*       10
            /   \
           2     5
               /   \
              18    12
              / \   / \
             2   3 3   2
                      /
                     7
    */

    // Create Binary Tree as shown
    Node* root = newNode(10);

    root->left = newNode(2);
    root->right = newNode(5);

    root->right->left = newNode(18);
    root->right->right = newNode(12);

    root->right->left->left = newNode(2);
    root->right->left->right = newNode(3);
    root->right->right->left = newNode(3);
    root->right->right->right = newNode(2);
    root->right->right->right->left = newNode(7);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print all nodes having
    // children as their factors
    cout << getCount(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Counting nodes
// whose immediate children are its factors
import java.util.*;

class GFG{

static int N = 1000000;

// To store all prime numbers
static Vector<Integer> prime = new Vector<Integer>();

static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..N]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    boolean []check = new boolean[N + 1];
    Arrays.fill(check, true);

    for (int p = 2; p * p <= N; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (check[p] == true) {

            prime.add(p);

            // Update all multiples of p
            // greater than or equal to
            // the square of it
            // numbers which are multiples of p
            // and are less than p^2
            // are already marked.
            for (int i = p * p; i <= N; i += p)
                check[i] = false;
        }
    }
}

// A Tree node
static class Node {
    int key;
    Node left, right;
};

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// function to check and print if
// immediate children of a node
// are its factors or not
static boolean areChilrenPrimeFactors(Node parent,
                            Node a,
                            Node b)
{
    if (prime.get(a.key) != null && prime.get(b.key) != null
        && (parent.key % a.key == 0
            && parent.key % b.key == 0))
        return true;
    else
        return false;
}

// Function to get the count of full Nodes in
// a binary tree
static int getCount(Node node)
{
    // If tree is empty
    if (node == null)
        return 0;
    Queue<Node> q = new LinkedList<>();

    // Initialize count of ful/l nodes
    // having children as their factors
    int count = 0;

    // Do level order traversal
    // starting from root
    q.add(node);
    while (!q.isEmpty()) {
        Node temp = q.peek();
        q.remove();

        if (temp.left!=null && temp.right != null) {
            if (areChilrenPrimeFactors(
                    temp, temp.left,
                    temp.right))
                count++;
        }

        if (temp.left != null)
            q.add(temp.left);
        if (temp.right != null)
            q.add(temp.right);
    }
    return count;
}

// Function to find total no of nodes
// In a given binary tree
static int findSize(Node node)
{
    // Base condition
    if (node == null)
        return 0;

    return 1
           + findSize(node.left)
           + findSize(node.right);
}

// Driver Code
public static void main(String[] args)
{
    /*       10
            /   \
           2     5
               /   \
              18    12
              / \   / \
             2   3 3   2
                      /
                     7
    */

    // Create Binary Tree as shown
    Node root = newNode(10);

    root.left = newNode(2);
    root.right = newNode(5);

    root.right.left = newNode(18);
    root.right.right = newNode(12);

    root.right.left.left = newNode(2);
    root.right.left.right = newNode(3);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(2);
    root.right.right.right.left = newNode(7);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print all nodes having
    // children as their factors
    System.out.print(getCount(root) +"\n");

}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program for Counting nodes
// whose immediate children are its factors
using System;
using System.Collections.Generic;

class GFG{

static int N = 1000000;

// To store all prime numbers
static List<int> prime = new List<int>();

static void SieveOfEratosthenes()
{
    // Create a bool array "prime[0..N]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    bool []check = new bool[N + 1];
    for (int i = 0; i <= N; i += 1){
        check[i] = true;
    }

    for (int p = 2; p * p <= N; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (check[p] == true) {

            prime.Add(p);

            // Update all multiples of p
            // greater than or equal to
            // the square of it
            // numbers which are multiples of p
            // and are less than p^2
            // are already marked.
            for (int i = p * p; i <= N; i += p)
                check[i] = false;
        }
    }
}

// A Tree node
class Node {
    public int key;
    public Node left, right;
};

// Utility function to create a new node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// function to check and print if
// immediate children of a node
// are its factors or not
static bool areChilrenPrimeFactors(Node parent,
                            Node a,
                            Node b)
{
    if (prime.Contains(a.key)&& prime.Contains(b.key)
        && (parent.key % a.key == 0
            && parent.key % b.key == 0))
        return true;
    else
        return false;
}

// Function to get the count of full Nodes in
// a binary tree
static int getCount(Node node)
{
    // If tree is empty
    if (node == null)
        return 0;
    List<Node> q = new List<Node>();

    // Initialize count of ful/l nodes
    // having children as their factors
    int count = 0;

    // Do level order traversal
    // starting from root
    q.Add(node);
    while (q.Count!=0) {
        Node temp = q[0];
        q.RemoveAt(0);

        if (temp.left!=null && temp.right != null) {
            if (areChilrenPrimeFactors(
                    temp, temp.left,
                    temp.right))
                count++;
        }

        if (temp.left != null)
            q.Add(temp.left);
        if (temp.right != null)
            q.Add(temp.right);
    }
    return count;
}

// Function to find total no of nodes
// In a given binary tree
static int findSize(Node node)
{
    // Base condition
    if (node == null)
        return 0;

    return 1
           + findSize(node.left)
           + findSize(node.right);
}

// Driver Code
public static void Main(String[] args)
{
    /*       10
            /   \
           2     5
               /   \
              18    12
              / \   / \
             2   3 3   2
                      /
                     7
    */

    // Create Binary Tree as shown
    Node root = newNode(10);

    root.left = newNode(2);
    root.right = newNode(5);

    root.right.left = newNode(18);
    root.right.right = newNode(12);

    root.right.left.left = newNode(2);
    root.right.left.right = newNode(3);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(2);
    root.right.right.right.left = newNode(7);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print all nodes having
    // children as their factors
    Console.Write(getCount(root) +"\n");

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program for Counting nodes
    // whose immediate children are its factors

    let N = 1000000;

    // To store all prime numbers
    let prime = [];

    function SieveOfEratosthenes()
    {
        // Create a boolean array "prime[0..N]"
        // and initialize all entries it as true.
        // A value in prime[i] will finally
        // be false if i is Not a prime, else true.
        let check = new Array(N + 1);
        check.fill(true);

        for (let p = 2; p * p <= N; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (check[p] == true) {

                prime.push(p);

                // Update all multiples of p
                // greater than or equal to
                // the square of it
                // numbers which are multiples of p
                // and are less than p^2
                // are already marked.
                for (let i = p * p; i <= N; i += p)
                    check[i] = false;
            }
        }
    }

    // A Tree node
    class Node {
        constructor(key)
        {
            this.key = key;
            this.left = null;
            this.right = null;
        }
    }

    // Utility function to create a new node
    function newNode(key)
    {
        let temp = new Node(key);
        return (temp);
    }

    // function to check and print if
    // immediate children of a node
    // are its factors or not
    function areChilrenPrimeFactors(parent, a, b)
    {
        if (prime[a.key] != null && prime[b.key] != null
            && (parent.key % a.key == 0
                && parent.key % b.key == 0))
            return true;
        else
            return false;
    }

    // Function to get the count of full Nodes in
    // a binary tree
    function getCount(node)
    {
        // If tree is empty
        if (node == null)
            return 0;
        let q = [];

        // Initialize count of ful/l nodes
        // having children as their factors
        let count = 0;

        // Do level order traversal
        // starting from root
        q.push(node);
        while (q.length > 0) {
            let temp = q[0];
            q.shift();

            if (temp.left!=null && temp.right != null) {
                if (areChilrenPrimeFactors(
                        temp, temp.left,
                        temp.right))
                    count++;
            }

            if (temp.left != null)
                q.push(temp.left);
            if (temp.right != null)
                q.push(temp.right);
        }
        return count;
    }

    // Function to find total no of nodes
    // In a given binary tree
    function findSize(node)
    {
        // Base condition
        if (node == null)
            return 0;

        return 1
               + findSize(node.left)
               + findSize(node.right);
    }

    /*       10
            /   \
           2     5
               /   \
              18    12
              / \   / \
             2   3 3   2
                      /
                     7
    */

    // Create Binary Tree as shown
    let root = newNode(10);

    root.left = newNode(2);
    root.right = newNode(5);

    root.right.left = newNode(18);
    root.right.right = newNode(12);

    root.right.left.left = newNode(2);
    root.right.left.right = newNode(3);
    root.right.right.left = newNode(3);
    root.right.right.right = newNode(2);
    root.right.right.right.left = newNode(7);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print all nodes having
    // children as their factors
    document.write(getCount(root) +"</br>");

</script>
```

**Output:** 

```
3
```