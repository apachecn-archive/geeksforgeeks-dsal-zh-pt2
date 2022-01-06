# 给定数组中按位异或大于 K 的计数对

> 原文:[https://www . geesforgeks . org/count-pairs-having-bitwise-xor-大于 k-from-a-给定数组/](https://www.geeksforgeeks.org/count-pairs-having-bitwise-xor-greater-than-k-from-a-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是计算给定数组中的对的数量，使得每对的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)大于 **K** 。

**示例:**

> **输入:** arr = {1，2，3，5}，K = 2
> **输出:** 4
> **解释:**
> 满足给定条件的所有可能对的按位异或为:
> arr[0]^ arr[1]= 1 ^ 2 = 3
> arr[0]^ arr[3]= 1 ^ 5 = 4
> arr[1]^ arr[3]= 2 ^ 5 = 7
> arr[0]^
> 
> **输入:** arr[] = {3，5，6，8}，K = 2
> T3】输出: 6

**天真方法:**解决这个问题最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组的所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，对于每个对，检查对的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)是否大于 **K** 。如果发现为真，则增加**计数，使[按位异或](https://www.geeksforgeeks.org/tag/xor/)大于 **K** 的对**。最后，打印获得的这种对的计数。

***时间复杂度**:O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效途径:**使用[特里](https://www.geeksforgeeks.org/trie-insert-and-search/)可以解决问题。其思想是[迭代给定的数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个数组元素，计算存在于 **Trie** 中的元素数量，其与当前元素的**按位异或**大于 **K** ，并将当前元素的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)插入到 **Trie** 中。最后，打印**位异或**大于 **K** 的对的计数。按照以下步骤解决问题:

*   创建一个 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 有根节点，比如**根**来存储给定数组的每个元素的二进制表示。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，计算与当前元素按位异或大于 K 的 Trie 中存在的元素数量，[插入](https://www.geeksforgeeks.org/trie-insert-and-search/)当前元素的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)。
*   最后，打印满足给定条件的配对数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of Trie
struct TrieNode
{
    // Stores binary representation
    // of numbers
    TrieNode *child[2];

    // Stores count of elements
    // present in a node 
    int cnt;

    // Function to initialize
    // a Trie Node
    TrieNode() {
        child[0] = child[1] = NULL;
        cnt = 0;
    }
};

// Function to insert a number into Trie
void insertTrie(TrieNode *root, int N) {

    // Traverse binary representation of X.
    for (int i = 31; i >= 0; i--) {

        // Stores ith bit of N
        bool x = (N) & (1 << i);

        // Check if an element already
        // present in Trie having ith bit x.
        if(!root->child[x]) {

            // Create a new node of Trie.
            root->child[x] = new TrieNode();
        }

        // Update count of elements
        // whose ith bit is x
        root->child[x]->cnt+= 1;

        // Update root.
        root= root->child[x];
    }
}

// Function to count elements
// in Trie whose XOR with N
// exceeds K
int cntGreater(TrieNode * root,
                int N, int K)
{

    // Stores count of elements
    // whose XOR with N exceeding K
    int cntPairs = 0;

    // Traverse binary representation
    // of N and K in Trie
    for (int i = 31; i >= 0 &&
                     root; i--) {

        // Stores ith bit of N                        
        bool x = N & (1 << i);

        // Stores ith bit of K
        bool y = K & (1 << i);

        // If the ith bit of K is 1
        if (y) {

            // Update root.
            root =
                root->child[1 - x];
        }

        // If the ith bit of K is 0
        else{

            // If an element already
            // present in Trie having
            // ith bit (1 - x)
            if (root->child[1 - x]) {

                // Update cntPairs
                cntPairs +=
                root->child[1 - x]->cnt;
            }

            // Update root.
            root = root->child[x];
        }
    }
    return cntPairs;
}

// Function to count pairs that
// satisfy the given conditions.
int cntGreaterPairs(int arr[], int N,
                             int K) {

    // Create root node of Trie
    TrieNode *root = new TrieNode();

    // Stores count of pairs that
    // satisfy the given conditions
    int cntPairs = 0;

    // Traverse the given array.
    for(int i = 0;i < N; i++){

        // Update cntPairs
        cntPairs += cntGreater(root,
                           arr[i], K);

        // Insert arr[i] into Trie.
        insertTrie(root, arr[i]);
    }
    return cntPairs;
}

//Driver code
int main()
{
    int arr[] = {3, 5, 6, 8};
    int K= 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout<<cntGreaterPairs(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Structure of Trie
static class TrieNode
{
  // Stores binary representation
  // of numbers
  TrieNode []child = new TrieNode[2];

  // Stores count of elements
  // present in a node 
  int cnt;

  // Function to initialize
  // a Trie Node
  TrieNode()
  {
    child[0] = child[1] = null;
    cnt = 0;
  }

};

// Function to insert a number
// into Trie
static void insertTrie(TrieNode root,
                       int N)
{
  // Traverse binary representation
  // of X.
  for (int i = 31; i >= 0; i--)
  {
    // Stores ith bit of N
    int x = (N) & (1 << i);

    // Check if an element already
    // present in Trie having ith
    // bit x.
    if (x < 2 && root.child[x] == null)
    {
      // Create a new node of Trie.
      root.child[x] = new TrieNode();
    }

    // Update count of elements
    // whose ith bit is x
    if(x < 2 && root.child[x] != null)
      root.child[x].cnt += 1;

    // Update root.
    if(x < 2)
      root = root.child[x];
  }
}

// Function to count elements
// in Trie whose XOR with N
// exceeds K
static int cntGreater(TrieNode root,
                      int N, int K)
{
  // Stores count of elements
  // whose XOR with N exceeding K
  int cntPairs = 1;

  // Traverse binary representation
  // of N and K in Trie
  for (int i = 31; i >= 0 &&
           root!=null; i--)
  {
    // Stores ith bit of N
    int x = N & (1 << i);

    // Stores ith bit of K
    int y = K & (1 << i);

    // If the ith bit of K is 1
    if (y == 1)
    {
      // Update root.
      root = root.child[1 - x];
    }

    // If the ith bit of K is 0
    else
    {
      // If an element already
      // present in Trie having
      // ith bit (1 - x)
      if (x < 2 &&
          root.child[1 - x] != null)
      {
        // Update cntPairs
        cntPairs += root.child[1 - x].cnt;
      }

      // Update root.
      if(x < 2)
        root = root.child[x];
    }
  }
  return cntPairs;
}

// Function to count pairs that
// satisfy the given conditions.
static int cntGreaterPairs(int arr[],
                           int N, int K)
{
  // Create root node of Trie
  TrieNode root = new TrieNode();

  // Stores count of pairs that
  // satisfy the given conditions
  int cntPairs = 0;

  // Traverse the given array.
  for (int i = 0; i < N; i++)
  {
    // Update cntPairs
    cntPairs += cntGreater(root,
                           arr[i], K);

    // Insert arr[i] into Trie.
    insertTrie(root, arr[i]);
  }
  return cntPairs;
}

// Driver code
public static void main(String[] args)
{
  int arr[] = {3, 5, 6, 8};
  int K = 2;
  int N = arr.length;
  System.out.print(cntGreaterPairs(arr,
                                   N, K));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Structure of Trie
class TrieNode:

    # Function to initialize
    # a Trie Node
    def __init__(self):

        self.child = [None, None]
        self.cnt = 0

# Function to insert a number into Trie
def insertTrie(root, N):

    # Traverse binary representation of X.
    for i in range(31, -1, -1):

        # Stores ith bit of N
        x = bool((N) & (1 << i))

        # Check if an element already
        # present in Trie having ith bit x.
        if (root.child[x] == None):

            # Create a new node of Trie.
            root.child[x] = TrieNode()

        # Update count of elements
        # whose ith bit is x
        root.child[x].cnt += 1

        # Update root
        root= root.child[x]

# Function to count elements
# in Trie whose XOR with N
# exceeds K
def cntGreater(root, N, K):

    # Stores count of elements
    # whose XOR with N exceeding K
    cntPairs = 0

    # Traverse binary representation
    # of N and K in Trie
    for i in range(31, -1, -1):
        if (root == None):
            break

        # Stores ith bit of N                        
        x = bool(N & (1 << i))

        # Stores ith bit of K
        y = K & (1 << i)

        # If the ith bit of K is 1
        if (y != 0):

            # Update root
            root = root.child[1 - x]

        # If the ith bit of K is 0
        else:

            # If an element already
            # present in Trie having
            # ith bit (1 - x)
            if (root.child[1 - x]):

                # Update cntPairs
                cntPairs += root.child[1 - x].cnt

            # Update root
            root = root.child[x]

    return cntPairs

# Function to count pairs that
# satisfy the given conditions.
def cntGreaterPairs(arr, N, K):

    # Create root node of Trie
    root = TrieNode()

    # Stores count of pairs that
    # satisfy the given conditions
    cntPairs = 0

    # Traverse the given array.
    for i in range(N):

        # Update cntPairs
        cntPairs += cntGreater(root, arr[i], K)

        # Insert arr[i] into Trie.
        insertTrie(root, arr[i])

    return cntPairs

# Driver code
if __name__=='__main__':

    arr = [ 3, 5, 6, 8 ]
    K = 2
    N = len(arr)

    print(cntGreaterPairs(arr, N, K))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Structure of Trie
public class TrieNode
{

  // Stores binary representation
  // of numbers
  public TrieNode []child = new TrieNode[2];

  // Stores count of elements
  // present in a node 
  public int cnt;

  // Function to initialize
  // a Trie Node
  public TrieNode()
  {
    child[0] = child[1] = null;
    cnt = 0;
  }
};

// Function to insert a number
// into Trie
static void insertTrie(TrieNode root,
                       int N)
{

  // Traverse binary representation
  // of X.
  for(int i = 31; i >= 0; i--)
  {

    // Stores ith bit of N
    int x = (N) & (1 << i);

    // Check if an element already
    // present in Trie having ith
    // bit x.
    if (x < 2 && root.child[x] == null)
    {

      // Create a new node of Trie.
      root.child[x] = new TrieNode();
    }

    // Update count of elements
    // whose ith bit is x
    if(x < 2 && root.child[x] != null)
      root.child[x].cnt += 1;

    // Update root.
    if(x < 2)
      root = root.child[x];
  }
}

// Function to count elements
// in Trie whose XOR with N
// exceeds K
static int cntGreater(TrieNode root,
                      int N, int K)
{

  // Stores count of elements
  // whose XOR with N exceeding K
  int cntPairs = 1;

  // Traverse binary representation
  // of N and K in Trie
  for(int i = 31; i >= 0 &&
      root != null; i--)
  {

    // Stores ith bit of N
    int x = N & (1 << i);

    // Stores ith bit of K
    int y = K & (1 << i);

    // If the ith bit of K is 1
    if (y == 1)
    {

      // Update root.
      root = root.child[1 - x];
    }

    // If the ith bit of K is 0
    else
    {

      // If an element already
      // present in Trie having
      // ith bit (1 - x)
      if (x < 2 &&
          root.child[1 - x] != null)
      {

        // Update cntPairs
        cntPairs += root.child[1 - x].cnt;
      }

      // Update root.
      if(x < 2)
        root = root.child[x];
    }
  }
  return cntPairs;
}

// Function to count pairs that
// satisfy the given conditions.
static int cntGreaterPairs(int []arr,
                           int N, int K)
{

  // Create root node of Trie
  TrieNode root = new TrieNode();

  // Stores count of pairs that
  // satisfy the given conditions
  int cntPairs = 0;

  // Traverse the given array.
  for(int i = 0; i < N; i++)
  {

    // Update cntPairs
    cntPairs += cntGreater(root,
                           arr[i], K);

    // Insert arr[i] into Trie.
    insertTrie(root, arr[i]);
  }
  return cntPairs;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = { 3, 5, 6, 8 };
  int K = 2;
  int N = arr.Length;

  Console.Write(cntGreaterPairs(arr,
                                N, K));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Structure of Trie
class TrieNode
{
    constructor()
    {
        this.child = new Array(2);
        this.child[0] = this.child[1] = null;
        this.cnt = 0;
    }
}

// Function to insert a number
// into Trie
function insertTrie(root,N)
{

    // Traverse binary representation
  // of X.
  for (let i = 31; i >= 0; i--)
  {

    // Stores ith bit of N
    let x = (N) & (1 << i);

    // Check if an element already
    // present in Trie having ith
    // bit x.
    if (x < 2 && root.child[x] == null)
    {
      // Create a new node of Trie.
      root.child[x] = new TrieNode();
    }

    // Update count of elements
    // whose ith bit is x
    if(x < 2 && root.child[x] != null)
      root.child[x].cnt += 1;

    // Update root.
    if(x < 2)
      root = root.child[x];
  }
}

// Function to count elements
// in Trie whose XOR with N
// exceeds K
function  cntGreater(root, N, K)
{

    // Stores count of elements
  // whose XOR with N exceeding K
  let cntPairs = 1;

  // Traverse binary representation
  // of N and K in Trie
  for (let i = 31; i >= 0 &&
           root!=null; i--)
  {
    // Stores ith bit of N
    let x = N & (1 << i);

    // Stores ith bit of K
    let y = K & (1 << i);

    // If the ith bit of K is 1
    if (y == 1)
    {

      // Update root.
      root = root.child[1 - x];
    }

    // If the ith bit of K is 0
    else
    {

      // If an element already
      // present in Trie having
      // ith bit (1 - x)
      if (x < 2 &&
          root.child[1 - x] != null)
      {
        // Update cntPairs
        cntPairs += root.child[1 - x].cnt;
      }

      // Update root.
      if(x < 2)
        root = root.child[x];
    }
  }
  return cntPairs;
}

// Function to count pairs that
// satisfy the given conditions.
function cntGreaterPairs(arr,N,K)
{
    // Create root node of Trie
  let root = new TrieNode();

  // Stores count of pairs that
  // satisfy the given conditions
  let cntPairs = 0;

  // Traverse the given array.
  for (let i = 0; i < N; i++)
  {
    // Update cntPairs
    cntPairs += cntGreater(root,
                           arr[i], K);

    // Insert arr[i] into Trie.
    insertTrie(root, arr[i]);
  }
  return cntPairs;
}

// Driver code
let arr=[3, 5, 6, 8];
let K = 2;
let N = arr.length;
document.write(cntGreaterPairs(arr,N, K));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
6
```

***时间复杂度** :O(N * 32)*
***辅助空间:** O(N * 32)*