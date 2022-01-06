# 以子树为素因子的二叉树的节点数

> 原文:[https://www . geesforgeks . org/二叉树中的节点数-谁的子元素是它的素因子/](https://www.geeksforgeeks.org/count-of-nodes-in-a-binary-tree-whose-child-is-its-prime-factors/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印节点的计数，这些节点的任何一个直接子节点都是其[主因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。
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
Output: 3
Explanation: 
Children of 15 (3, 5) 
 are prime factors of 15
Child of 20 (2) 
 is prime factors of 20
Child of 4 (2) 
 is prime factors of 4

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
Children of 70 (2, 5)
 are prime factors of 70
Children of 30 (3, 5)
 are prime factors of 30
```

**进场:**

1.  遍历给定的二叉树，对于每个节点:
    *   检查孩子是否存在。
    *   如果子节点存在，检查每个子节点是否是该节点的[素因子](https://www.geeksforgeeks.org/prime-factor/)。
    *   记录这些节点的数量，并在最后打印出来。

2.  为了检查一个因子是否是素数，我们将使用厄拉多塞的[筛来预计算素数，以做 O(1)中的检查。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

以下是上述方法的实现:

## C++

```
// C++ program for Counting nodes whose
// immediate children are its factors

#include <bits/stdc++.h>
using namespace std;

int N = 1000000;

// To store all prime numbers
vector<int> prime;

void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..N]"
    // and initialize all its entries as true.
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

// Function to check if immediate children
// of a node are its factors or not
bool IsChilrenPrimeFactor(struct Node* parent,
                          struct Node* a)
{
    if (prime[a->key]
        && (parent->key % a->key == 0))
        return true;
    else
        return false;
}

// Function to get the count of full Nodes in
// a binary tree
unsigned int GetCount(struct Node* node)
{
    // If tree is empty
    if (!node)
        return 0;
    queue<Node*> q;

    // Do level order traversal starting
    // from root

    // Initialize count of full nodes having
    // children as their factors
    int count = 0;
    q.push(node);

    while (!q.empty()) {
        struct Node* temp = q.front();
        q.pop();

        // If only right child exist
        if (temp->left == NULL
            && temp->right != NULL) {
            if (IsChilrenPrimeFactor(
                    temp,
                    temp->right))
                count++;
        }
        else {
            // If only left child exist
            if (temp->right == NULL
                && temp->left != NULL) {
                if (IsChilrenPrimeFactor(
                        temp,
                        temp->left))
                    count++;
            }
            else {
                // Both left and right child exist
                if (temp->left != NULL
                    && temp->right != NULL) {
                    if (IsChilrenPrimeFactor(
                            temp,
                            temp->right)
                        && IsChilrenPrimeFactor(
                               temp,
                               temp->left))
                        count++;
                }
            }
        }
        // Check for left child
        if (temp->left != NULL)
            q.push(temp->left);

        // Check for right child
        if (temp->right != NULL)
            q.push(temp->right);
    }
    return count;
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
             2   3 3   14
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
    root->right->right->right = newNode(14);
    root->right->right->right->left = newNode(7);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print Count of all nodes having children
    // as their factors
    cout << GetCount(root) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Counting nodes whose
// immediate children are its factors
import java.util.*;

class GFG{

static int N = 1000000;

// To store all prime numbers
static Vector<Integer> prime = new Vector<Integer>();

static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..N]"
    // and initialize all its entries as true.
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

// Function to check if immediate children
// of a node are its factors or not
static boolean IsChilrenPrimeFactor(Node parent,
                          Node a)
{
    if (prime.get(a.key)>0
        && (parent.key % a.key == 0))
        return true;
    else
        return false;
}

// Function to get the count of full Nodes in
// a binary tree
static int GetCount(Node node)
{
    // If tree is empty
    if (node == null)
        return 0;
    Queue<Node> q = new LinkedList<>();

    // Do level order traversal starting
    // from root

    // Initialize count of full nodes having
    // children as their factors
    int count = 0;
    q.add(node);

    while (!q.isEmpty()) {
        Node temp = q.peek();
        q.remove();

        // If only right child exist
        if (temp.left == null
            && temp.right != null) {
            if (IsChilrenPrimeFactor(
                    temp,
                    temp.right))
                count++;
        }
        else {
            // If only left child exist
            if (temp.right == null
                && temp.left != null) {
                if (IsChilrenPrimeFactor(
                        temp,
                        temp.left))
                    count++;
            }
            else {
                // Both left and right child exist
                if (temp.left != null
                    && temp.right != null) {
                    if (IsChilrenPrimeFactor(
                            temp,
                            temp.right)
                        && IsChilrenPrimeFactor(
                               temp,
                               temp.left))
                        count++;
                }
            }
        }
        // Check for left child
        if (temp.left != null)
            q.add(temp.left);

        // Check for right child
        if (temp.right != null)
            q.add(temp.right);
    }
    return count;
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
             2   3 3   14
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
    root.right.right.right = newNode(14);
    root.right.right.right.left = newNode(7);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print Count of all nodes having children
    // as their factors
    System.out.print(GetCount(root) +"\n");

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program for Counting nodes whose
# immediate children are its factors
from collections import deque
N = 1000000

# To store all prime numbers
prime = []
def SieveOfEratosthenes() -> None:

    # Create a boolean array "prime[0..N]"
    # and initialize all its entries as true.
    # A value in prime[i] will finally
    # be false if i is Not a prime, else true.
    check = [True for _ in range(N + 1)]
    p = 2
    while p * p <= N:

        # If prime[p] is not changed,
        # then it is a prime
        if (check[p]):
            prime.append(p)

            # Update all multiples of p
            # greater than or equal to
            # the square of it
            # numbers which are multiples of p
            # and are less than p^2
            # are already marked.
            for i in range(p * p, N + 1, p):
                check[i] = False
        p += 1

# A Tree node
class Node:
    def __init__(self, key: int) -> None:
        self.key = key
        self.left = None
        self.right = None

# Function to check if immediate children
# of a node are its factors or not
def IsChilrenPrimeFactor(parent: Node, a: Node) -> bool:
    if (prime[a.key] and (parent.key % a.key == 0)):
        return True
    else:
        return False

# Function to get the count of full Nodes in
# a binary tree
def GetCount(node: Node) -> int:

    # If tree is empty
    if (not node):
        return 0
    q = deque()

    # Do level order traversal starting
    # from root

    # Initialize count of full nodes having
    # children as their factors
    count = 0
    q.append(node)

    while q:
        temp = q.popleft()

        # If only right child exist
        if (temp.left == None and temp.right != None):
            if (IsChilrenPrimeFactor(temp, temp.right)):
                count += 1

        else:

            # If only left child exist
            if (temp.right == None and temp.left != None):
                if (IsChilrenPrimeFactor(temp, temp.left)):
                    count += 1

            else:

                # Both left and right child exist
                if (temp.left != None and temp.right != None):
                    if (IsChilrenPrimeFactor(temp, temp.right)
                            and IsChilrenPrimeFactor(temp, temp.left)):
                        count += 1

        # Check for left child
        if (temp.left != None):
            q.append(temp.left)

        # Check for right child
        if (temp.right != None):
            q.append(temp.right)

    return count

# Driver Code
if __name__ == "__main__":
    '''       10
            /   \
           2     5
               /   \
              18    12
              / \   / \
             2   3 3   14
                      /
                     7
    '''

    # Create Binary Tree as shown
    root = Node(10)

    root.left = Node(2)
    root.right = Node(5)

    root.right.left = Node(18)
    root.right.right = Node(12)

    root.right.left.left = Node(2)
    root.right.left.right = Node(3)
    root.right.right.left = Node(3)
    root.right.right.right = Node(14)
    root.right.right.right.left = Node(7)

    # To save all prime numbers
    SieveOfEratosthenes()

    # Print Count of all nodes having children
    # as their factors
    print(GetCount(root))

# This code is contributed by sanjeev2552
```

## C#

```
// C# program for Counting nodes whose
// immediate children are its factors
using System;
using System.Collections.Generic;

public class GFG{

static int N = 1000000;

// To store all prime numbers
static List<int> prime = new List<int>();

static void SieveOfEratosthenes()
{
    // Create a bool array "prime[0..N]"
    // and initialize all its entries as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    bool []check = new bool[N + 1];
    for (int i = 0; i <= N; i += 1)
        check[i] = true;

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

// Function to check if immediate children
// of a node are its factors or not
static bool IsChilrenPrimeFactor(Node parent,
                          Node a)
{
    if (prime[a.key]>0
        && (parent.key % a.key == 0))
        return true;
    else
        return false;
}

// Function to get the count of full Nodes in
// a binary tree
static int GetCount(Node node)
{
    // If tree is empty
    if (node == null)
        return 0;
    List<Node> q = new List<Node>();

    // Do level order traversal starting
    // from root

    // Initialize count of full nodes having
    // children as their factors
    int count = 0;
    q.Add(node);

    while (q.Count!=0) {
        Node temp = q[0];
        q.RemoveAt(0);

        // If only right child exist
        if (temp.left == null
            && temp.right != null) {
            if (IsChilrenPrimeFactor(
                    temp,
                    temp.right))
                count++;
        }
        else {
            // If only left child exist
            if (temp.right == null
                && temp.left != null) {
                if (IsChilrenPrimeFactor(
                        temp,
                        temp.left))
                    count++;
            }
            else {
                // Both left and right child exist
                if (temp.left != null
                    && temp.right != null) {
                    if (IsChilrenPrimeFactor(
                            temp,
                            temp.right)
                        && IsChilrenPrimeFactor(
                               temp,
                               temp.left))
                        count++;
                }
            }
        }
        // Check for left child
        if (temp.left != null)
            q.Add(temp.left);

        // Check for right child
        if (temp.right != null)
            q.Add(temp.right);
    }
    return count;
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
             2   3 3   14
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
    root.right.right.right = newNode(14);
    root.right.right.right.left = newNode(7);

    // To save all prime numbers
    SieveOfEratosthenes();

    // Print Count of all nodes having children
    // as their factors
    Console.Write(GetCount(root) +"\n");

}
}
// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

  // JavaScript program for Counting nodes whose
  // immediate children are its factors

  let N = 1000000;

  // To store all prime numbers
  let prime = [];

  function SieveOfEratosthenes()
  {
      // Create a boolean array "prime[0..N]"
      // and initialize all its entries as true.
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

  // Function to check if immediate children
  // of a node are its factors or not
  function IsChilrenPrimeFactor(parent, a)
  {
      if (prime[a.key]>0
          && (parent.key % a.key == 0))
          return true;
      else
          return false;
  }

  // Function to get the count of full Nodes in
  // a binary tree
  function GetCount(node)
  {
      // If tree is empty
      if (node == null)
          return 0;
      let q = [];

      // Do level order traversal starting
      // from root

      // Initialize count of full nodes having
      // children as their factors
      let count = 0;
      q.push(node);

      while (q.length > 0) {
          let temp = q[0];
          q.shift();

          // If only right child exist
          if (temp.left == null
              && temp.right != null) {
              if (IsChilrenPrimeFactor(
                      temp,
                      temp.right))
                  count++;
          }
          else {
              // If only left child exist
              if (temp.right == null
                  && temp.left != null) {
                  if (IsChilrenPrimeFactor(
                          temp,
                          temp.left))
                      count++;
              }
              else {
                  // Both left and right child exist
                  if (temp.left != null
                      && temp.right != null) {
                      if (IsChilrenPrimeFactor(
                              temp,
                              temp.right)
                          && IsChilrenPrimeFactor(
                                 temp,
                                 temp.left))
                          count++;
                  }
              }
          }
          // Check for left child
          if (temp.left != null)
              q.push(temp.left);

          // Check for right child
          if (temp.right != null)
              q.push(temp.right);
      }
      return count;
  }

  /*       10
            /   \
           2     5
               /   \
              18    12
              / \   / \
             2   3 3   14
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
  root.right.right.right = newNode(14);
  root.right.right.right.left = newNode(7);

  // To save all prime numbers
  SieveOfEratosthenes();

  // Print Count of all nodes having children
  // as their factors
  document.write(GetCount(root) +"</br>");

</script>
```

**Output:** 

```
3
```

**<u>复杂度分析:</u>**

*   **时间复杂度:** O(N)。
    在 dfs 中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于 bfs 而导致的复杂性是 O(N)。此外，为了处理每个节点，使用了 SieveOfEratosthenes()函数，该函数的复杂度也是 O(sqrt(N))，但是由于该函数只执行一次，因此不会影响整体的时间复杂度。因此，时间复杂度为 O(N)。
*   **辅助空间:** O(N)。
    质数数组使用额外空间，因此空间复杂度为 O(N)。