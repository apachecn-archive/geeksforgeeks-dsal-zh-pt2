# 数组中两个数的最大异或|集合 2

> 原文:[https://www . geeksforgeeks . org/数组集 2 中两个数的最大异或/](https://www.geeksforgeeks.org/maximum-xor-of-two-numbers-in-an-array-set-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是从给定数组中所有可能的对中找到最大值[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> ***输入:** arr[] = {25，10，2，8，5，3}*
> ***输出:** 28*
> ***解释:***
> *最大的结果是 5^25 = 28。*
> 
> ***输入:** arr[] = {1，2，3，4，5，6，7}*
> ***输出:** 7*
> ***解释:***
> *最大的结果是 1^6 = 7。*

**天真法:**参考文章[一个数组中两个数的最大异或](https://www.geeksforgeeks.org/maximum-xor-of-two-numbers-in-an-array/)最简单的解题方法是[生成给定数组的所有对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)并计算每对的异或，找出其中的最大值。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**位屏蔽方法:**参考文章[数组中两个数的最大异或](https://www.geeksforgeeks.org/maximum-xor-of-two-numbers-in-an-array/)使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)解决问题。

***时间复杂度:** O(N*log M)，其中 M 是数组*
***中出现的***最大*数辅助空间: O(N)*

**有效方法:**上述方法可以通过在数组**arr【】**中插入数字[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)来使用 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 来解决。现在迭代数组 **arr[]** 中所有元素的二进制表示，如果当前位为 **0** ，则在 **Trie** 中找到值为 **1** 的路径，反之亦然，以获得**按位异或**的最大值。更新每个数字的最大值。以下是步骤:

1.  将**最大值**初始化为 **0** 。
2.  在树中给定数组**arr【】**中插入所有数字的[二进制表示。在 trie 中插入当前位 **0** 时，在左边创建一个节点，否则在当前头节点的右边创建一个节点。](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)
3.  现在，[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对每个元素执行以下操作:
    *   将**电流或**值初始化为 0。
    *   遍历当前数字的二进制表示。
    *   如果 **i <sup>第</sup>位**为 **1** 和**节点- >左侧**存在，则更新**current sor 为 current sor+pow(2，i)** 并将节点更新为**节点- >左侧**。否则更新**节点=节点- >右**。
    *   如果 **i <sup>第</sup>位为 0** ，且**节点- >右侧**存在，则更新**current sor 为 current sor+pow(2，i)** 并将节点更新为**节点- >右侧**。否则更新**节点=节点- >左侧**。
4.  对于上述步骤中的每个数组元素，如果**最大值**大于**当前值**，则更新**最大值**值。
5.  完成上述步骤后，打印**最大值**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of Trie
class node {
public:
    node* left;
    node* right;
};

// Function to insert binary
// representation of element x
// in the Trie
void insert(int x, node* head)
{
    // Store the head
    node* curr = head;

    for (int i = 30; i >= 0; i--) {

        // Find the i-th bit
        int val = (x >> i) & 1;

        if (val == 0) {

            // If curr->left is NULL
            if (!curr->left)
                curr->left = new node();

            // Update curr to curr->left
            curr = curr->left;
        }
        else {

            // If curr->right is NULL
            if (!curr->right)
                curr->right = new node();

            // Update curr to curr->right
            curr = curr->right;
        }
    }
}

// Function that finds the maximum
// Bitwise XOR value for all such pairs
int findMaximumXOR(int arr[], int n)
{
    // head Node of Trie
    node* head = new node();

    // Insert each element in trie
    for (int i = 0; i < n; i++) {
        insert(arr[i], head);
    }

    // Stores the maximum XOR value
    int ans = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // Stores the XOR with current
        // value arr[i]
        int curr_xor = 0;

        int M = pow(2, 30);

        node* curr = head;

        for (int j = 30; j >= 0; j--) {

            // Finding ith bit
            int val = (arr[i] >> j) & 1;

            // Check if the bit is 0
            if (val == 0) {

                // If right node exists
                if (curr->right) {

                    // Update the currentXOR
                    curr_xor += M;
                    curr = curr->right;
                }

                else {
                    curr = curr->left;
                }
            }

            else {

                // Check if left node exists
                if (curr->left) {

                    // Update the currentXOR
                    curr_xor += M;
                    curr = curr->left;
                }
                else {
                    curr = curr->right;
                }
            }

            // Update M to M/2 for next set bit
            M /= 2;
        }

        // Update the maximum XOR
        ans = max(ans, curr_xor);
    }

    // Return the maximum XOR found
    return ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << findMaximumXOR(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Structure of Trie
static class node
{
    node left;
    node right;
};

// Function to insert binary
// representation of element x
// in the Trie
static void insert(int x, node head)
{

    // Store the head
    node curr = head;

    for(int i = 30; i >= 0; i--)
    {

        // Find the i-th bit
        int val = (x >> i) & 1;

        if (val == 0)
        {

            // If curr.left is null
            if (curr.left == null)
                curr.left = new node();

            // Update curr to curr.left
            curr = curr.left;
        }
        else
        {

            // If curr.right is null
            if (curr.right == null)
                curr.right = new node();

            // Update curr to curr.right
            curr = curr.right;
        }
    }
}

// Function that finds the maximum
// Bitwise XOR value for all such pairs
static int findMaximumXOR(int arr[], int n)
{

    // head Node of Trie
    node head = new node();

    // Insert each element in trie
    for(int i = 0; i < n; i++)
    {
        insert(arr[i], head);
    }

    // Stores the maximum XOR value
    int ans = 0;

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // Stores the XOR with current
        // value arr[i]
        int curr_xor = 0;

        int M = (int)Math.pow(2, 30);

        node curr = head;

        for(int j = 30; j >= 0; j--)
        {

            // Finding ith bit
            int val = (arr[i] >> j) & 1;

            // Check if the bit is 0
            if (val == 0)
            {

                // If right node exists
                if (curr.right != null)
                {

                    // Update the currentXOR
                    curr_xor += M;
                    curr = curr.right;
                }
                else
                {
                    curr = curr.left;
                }
            }

            else
            {

                // Check if left node exists
                if (curr.left != null)
                {

                    // Update the currentXOR
                    curr_xor += M;
                    curr = curr.left;
                }
                else
                {
                    curr = curr.right;
                }
            }

            // Update M to M/2 for next set bit
            M /= 2;
        }

        // Update the maximum XOR
        ans = Math.max(ans, curr_xor);
    }

    // Return the maximum XOR found
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };

    int N = arr.length;

    // Function call
    System.out.print(findMaximumXOR(arr, N));
}
}

// This code is contributed by Amit Katiyar
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Structure of Tree
public class node
{
  public node left;
  public node right;
};

// Function to insert binary
// representation of element
// x in the Tree
static void insert(int x,
                   node head)
{
  // Store the head
  node curr = head;

  for(int i = 30; i >= 0; i--)
  {
    // Find the i-th bit
    int val = (x >> i) & 1;

    if (val == 0)
    {
      // If curr.left is null
      if (curr.left == null)
        curr.left = new node();

      // Update curr to curr.left
      curr = curr.left;
    }
    else
    {
      // If curr.right is null
      if (curr.right == null)
        curr.right = new node();

      // Update curr to curr.right
      curr = curr.right;
    }
  }
}

// Function that finds the maximum
// Bitwise XOR value for all
// such pairs
static int findMaximumXOR(int []arr,
                          int n)
{   
  // Head Node of Tree
  node head = new node();

  // Insert each element in tree
  for(int i = 0; i < n; i++)
  {
    insert(arr[i], head);
  }

  // Stores the maximum XOR value
  int ans = 0;

  // Traverse the given array
  for(int i = 0; i < n; i++)
  {
    // Stores the XOR with
    // current value arr[i]
    int curr_xor = 0;

    int M = (int)Math.Pow(2, 30);
    node curr = head;

    for(int j = 30; j >= 0; j--)
    {
      // Finding ith bit
      int val = (arr[i] >> j) & 1;

      // Check if the bit is 0
      if (val == 0)
      {
        // If right node exists
        if (curr.right != null)
        {
          // Update the currentXOR
          curr_xor += M;
          curr = curr.right;
        }
        else
        {
          curr = curr.left;
        }
      }

      else
      {
        // Check if left node exists
        if (curr.left != null)
        {
          // Update the currentXOR
          curr_xor += M;
          curr = curr.left;
        }
        else
        {
          curr = curr.right;
        }
      }

      // Update M to M/2
      // for next set bit
      M /= 2;
    }

    // Update the maximum XOR
    ans = Math.Max(ans, curr_xor);
  }

  // Return the maximum
  // XOR found
  return ans;
}

// Driver Code
public static void Main(String[] args)
{   
  // Given array []arr
  int []arr = {1, 2, 3, 4};

  int N = arr.Length;

  // Function call
  Console.Write(findMaximumXOR(arr, N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Structure of Trie
     class node {
         constructor() {

                this.left = null;
                this.right = null;
            }
     }
    // Function to insert binary
    // representation of element x
    // in the Trie
    function insert(x,  head) {

        // Store the head
        var curr = head;

        for (i = 30; i >= 0; i--) {

            // Find the i-th bit
            var val = (x >> i) & 1;

            if (val == 0) {

                // If curr.left is null
                if (curr.left == null)
                    curr.left = new node();

                // Update curr to curr.left
                curr = curr.left;
            } else {

                // If curr.right is null
                if (curr.right == null)
                    curr.right = new node();

                // Update curr to curr.right
                curr = curr.right;
            }
        }
    }

    // Function that finds the maximum
    // Bitwise XOR value for all such pairs
    function findMaximumXOR(arr , n) {

        // head Node of Trie
        var head = new node();

        // Insert each element in trie
        for (var i = 0; i < n; i++) {
            insert(arr[i], head);
        }

        // Stores the maximum XOR value
        var ans = 0;

        // Traverse the given array
        for (i = 0; i < n; i++) {

            // Stores the XOR with current
            // value arr[i]
            var curr_xor = 0;

            var M = parseInt( Math.pow(2, 30));

            var curr = head;

            for (j = 30; j >= 0; j--) {

                // Finding ith bit
                var val = (arr[i] >> j) & 1;

                // Check if the bit is 0
                if (val == 0) {

                    // If right node exists
                    if (curr.right != null) {

                        // Update the currentXOR
                        curr_xor += M;
                        curr = curr.right;
                    } else {
                        curr = curr.left;
                    }
                }

                else {

                    // Check if left node exists
                    if (curr.left != null) {

                        // Update the currentXOR
                        curr_xor += M;
                        curr = curr.left;
                    } else {
                        curr = curr.right;
                    }
                }

                // Update M to M/2 for next set bit
                M = parseInt(M/2);
            }

            // Update the maximum XOR
            ans = Math.max(ans, curr_xor);
        }

        // Return the maximum XOR found
        return ans;
    }

    // Driver Code

        // Given array arr
        var arr = [ 1, 2, 3, 4 ];

        var N = arr.length;

        // Function call
        document.write(findMaximumXOR(arr, N));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(32*N)*
***辅助空间:** O(32*N)*