# 二叉树中排列为回文的根到叶路径的计数

> 原文:[https://www . geesforgeks . org/根到叶路径计数-其排列是二叉树中的回文/](https://www.geeksforgeeks.org/count-of-root-to-leaf-paths-whose-permutation-is-palindrome-in-a-binary-tree/)

给定一个节点包含字符的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是计算从根顶点到叶子的路径数量，使得路径中节点值的至少一个排列是回文。
**例:**

```
Input: 
                   2
                 /   \
                3     1
              /   \     \
             3     4     2
           /   \       /   \
          2     1     2     1

Output: 2
Explanation:
Paths whose one of the
permutation are palindrome are -
2 => 3 => 3 => 2 and 
2 => 1 => 2 => 1

Input:
                2
              /   \
             a     3
           /   \
          2     a
Output: 2
Explanation:
Palindromic paths are 
2 => a => 2 and 
2 => a => a 
```

**方法:**思路是利用[预序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)并跟踪路径。无论何时到达叶节点，都要检查当前路径中节点值的任何排列是否是回文路径。
检查节点值的排列是回文还是不使用映射保持每个字符的频率。如果奇数频率的元素数量最多为 1，则路径将是回文路径。
以下是上述方法的实施:

## C++

```
// C++ implementation to count of
// the path whose permutation is
// a palindromic path

#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Map to store the frequency
map<char, int> freq;
int ans = 0;

// Structure of the node
struct Node {
    char val;
    struct Node *left, *right;
};

// Function to add new node
Node* newNode(char key)
{
    Node* temp = new Node;
    temp->val = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Function to check that the path
// is a palindrome or not
int checkPalin()
{
    int oddCount = 0;
    for (auto x : freq) {
        if (x.second % 2 == 1)
            oddCount++;
    }
    return oddCount <= 1;
}

// Function to count the root to
// leaf path whose permutation is
// a palindromic path
void cntpalin(Node* root)
{
    if (root == NULL)
        return;
    freq[root->val]++;

    if (root->left == NULL
        && root->right == NULL) {

        if (checkPalin() == true)
            ans++;
    }
    cntpalin(root->left);
    cntpalin(root->right);
    freq[root->val]--;
}

// Driver Code
int main()
{
    Node* root = newNode('2');
    root->left = newNode('a');
    root->left->right = newNode('a');
    root->left->left = newNode('2');
    root->left->right->right = newNode('2');
    root->right = newNode('3');

    // Function Call
    cntpalin(root);

    cout << ans << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count of
// the path whose permutation is
// a palindromic path
import java.util.*;
class GFG{

// Map to store the frequency
static HashMap<Character,
               Integer> freq =
                        new HashMap<>();
static int ans = 0;

// Structure of the node
static class Node
{
  char val;
  Node left, right;
};

// Function to add new node
static Node newNode(char key)
{
  Node temp = new Node();
  temp.val = key;
  temp.left = temp.right = null;
  return (temp);
}

// Function to check that the path
// is a palindrome or not
static boolean checkPalin()
{
  int oddCount = 0;
  for (Map.Entry<Character,
                 Integer> x : freq.entrySet())
  {
    if (x.getValue() % 2 == 1)
      oddCount++;
  }

  return oddCount <= 1 ? true : false;
}

// Function to count the root to
// leaf path whose permutation is
// a palindromic path
static void cntpalin(Node root)
{
  if (root == null)
    return;
  if(freq.containsKey(root.val))
  {
    freq.put(root.val,
    freq.get(root.val) + 1);
  }
  else
  {
    freq.put(root.val, 1);
  }

  if (root.left == null &&
      root.right == null)
  {
    if (checkPalin() == true)
      ans++;
  }

  cntpalin(root.left);
  cntpalin(root.right);

  if(freq.containsKey(root.val))
  {
    freq.put(root.val,
    freq.get(root.val) - 1);
  }
}

// Driver Code
public static void main(String[] args)
{
  Node root = newNode('2');
  root.left = newNode('a');
  root.left.right = newNode('a');
  root.left.left = newNode('2');
  root.left.right.right = newNode('2');
  root.right = newNode('3');

  // Function Call
  cntpalin(root);

  System.out.print(ans + "\n");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
from collections import deque

# A Tree node
class Node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

freq = {}
ans = 0

# Function to check that the path
# is a palindrome or not
def checkPalin():

    oddCount = 0

    for x in freq:
        if (freq[x] % 2 == 1):
            oddCount+=1
    return oddCount <= 1

# Function to count the root to
# leaf path whose permutation is
# a palindromic path
def cntpalin(root):

    global freq, ans

    if (root == None):
        return

    freq[root.data] = freq.get(root.data,
                               0) + 1

    if (root.left == None
        and root.right == None):
        if (checkPalin() == True):
            ans += 1

    cntpalin(root.left)
    cntpalin(root.right)
    freq[root.data] -= 1

# Driver Code
if __name__ == '__main__':

    root = Node('2')
    root.left = Node('a')
    root.left.right = Node('a')
    root.left.left = Node('2')
    root.left.right.right = Node('2')
    root.right = Node('3')

    # Function Call
    cntpalin(root)

    print(ans)

# This code is contributed by Rutvik_56
```

## C#

```
// C# implementation to count of
// the path whose permutation is
// a palindromic path
using System;
using System.Collections.Generic;
class GFG{

// Map to store the frequency
static Dictionary<char,
                  int> freq = new Dictionary<char,
                                             int>();
static int ans = 0;

// Structure of the node
public class Node
{
  public char val;
  public Node left,
              right;
};

// Function to add new node
static Node newNode(char key)
{
  Node temp = new Node();
  temp.val = key;
  temp.left = temp.right = null;
  return (temp);
}

// Function to check that
// the path is a palindrome
// or not
static bool checkPalin()
{
  int oddCount = 0;
  foreach (KeyValuePair<char,
                        int> x in freq)
  {
    if (x.Value % 2 == 1)
      oddCount++;
  }

  return oddCount <= 1 ? true : false;
}

// Function to count the root to
// leaf path whose permutation is
// a palindromic path
static void cntpalin(Node root)
{
  if (root == null)
    return;
  if(freq.ContainsKey(root.val))
  {
    freq[root.val] = freq[root.val] + 1;
  }
  else
  {
    freq.Add(root.val, 1);
  }

  if (root.left == null &&
      root.right == null)
  {
    if (checkPalin() == true)
      ans++;
  }

  cntpalin(root.left);
  cntpalin(root.right);

  if(freq.ContainsKey(root.val))
  {
    freq[root.val] = freq[root.val] - 1;
  }
}

// Driver Code
public static void Main(String[] args)
{
  Node root = newNode('2');
  root.left = newNode('a');
  root.left.right = newNode('a');
  root.left.left = newNode('2');
  root.left.right.right = newNode('2');
  root.right = newNode('3');

  // Function Call
  cntpalin(root);

  Console.Write(ans + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript implementation to count of
// the path whose permutation is
// a palindromic path

// Map to store the frequency
let  freq = new Map();

let ans = 0;

// Structure of the node
class Node
{
    constructor(key)
    {
        this.val = key;
        this.left = this.right = null;
    }
}

// Function to check that the path
// is a palindrome or not
function checkPalin()
{
    let oddCount = 0;
  for (let [key, value] of freq.entries())
  {
    if (value % 2 == 1)
      oddCount++;
  }

  return oddCount <= 1 ? true : false;
}

// Function to count the root to
// leaf path whose permutation is
// a palindromic path
function cntpalin(root)
{
    if (root == null)
    return;
  if(freq.has(root.val))
  {
    freq.set(root.val,
    freq.get(root.val) + 1);
  }
  else
  {
    freq.set(root.val, 1);
  }

  if (root.left == null &&
      root.right == null)
  {
    if (checkPalin() == true)
      ans++;
  }

  cntpalin(root.left);
  cntpalin(root.right);

  if(freq.has(root.val))
  {
    freq.set(root.val,
    freq.get(root.val) - 1);
  }
}

// Driver Code
let root = new Node('2');
root.left = new Node('a');
root.left.right = new Node('a');
root.left.left = new Node('2');
root.left.right.right = new Node('2');
root.right = new Node('3');

// Function Call
cntpalin(root);

document.write(ans + "<br>");

// This code is contributed by unknown2108.
</script>
```

**Output:** 

```
2
```