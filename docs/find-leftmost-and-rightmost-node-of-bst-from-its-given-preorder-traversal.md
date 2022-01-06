# 从给定的前序遍历中找到 BST 最左边和最右边的节点

> 原文:[https://www . geesforgeks . org/find-从其给定的前序遍历中查找 bst 的最左和最右节点/](https://www.geeksforgeeks.org/find-leftmost-and-rightmost-node-of-bst-from-its-given-preorder-traversal/)

给定 **N** 个节点的二叉查找树的预序序列。任务是找到它最左边和最右边的节点。

**示例:**

```
Input : N = 5, preorder[]={ 3, 2, 1, 5, 4 }
Output : Leftmost = 1, Rightmost = 5
The BST constructed from this 
preorder sequence would be:
         3
       /   \
      2     5
     /     /
    1     4
Leftmost Node of this tree is equal to 1
Rightmost Node of this tree is equal to 5

Input : N = 3 preorder[]={ 2, 1, 3}
Output : Leftmost = 1, Rightmost = 3 
```

**朴素方法:**
从给定的前序序列构建 BST。参见[这篇](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/)文章，了解从给定的预订单构建 bst 的代码。构造好 BST 后，从根到最左节点遍历，从根到最右节点遍历，找到最左和最右节点。
**时间复杂度:** O(N)
**空间复杂度:** O(N)

**高效方法:**
不用构造树，而是利用 BST 的属性。BST 中最左边的节点总是具有最小值，而 BST 中最右边的节点总是具有最大值。
所以，从给定的数组中我们只需要找到最左边节点的最小值和最右边节点的最大值。

下面是上述方法的实现:

## C++

```
// C++ program to find leftmost and
// rightmost node from given preorder sequence
#include <bits/stdc++.h>
using namespace std;

// Function to return the leftmost and
// rightmost nodes of the BST whose
// preorder traversal is given
void LeftRightNode(int preorder[], int n)
{
    // Variables for finding minimum
    // and maximum values of the array
    int min = INT_MAX, max = INT_MIN;

    for (int i = 0; i < n; i++) {

        // Update the minimum
        if (min > preorder[i])
            min = preorder[i];

        // Update the maximum
        if (max < preorder[i])
            max = preorder[i];
    }

    // Print the values
    cout << "Leftmost node is " << min << "\n";
    cout << "Rightmost node is " << max;
}

// Driver Code
int main()
{
    int preorder[] = { 3, 2, 1, 5, 4 };
    int n = 5;

    LeftRightNode(preorder, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find leftmost and
// rightmost node from given preorder sequence
class GFG
{

// Function to return the leftmost and
// rightmost nodes of the BST whose
// preorder traversal is given
static void LeftRightNode(int preorder[], int n)
{
    // Variables for finding minimum
    // and maximum values of the array
    int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;

    for (int i = 0; i < n; i++)
    {

        // Update the minimum
        if (min > preorder[i])
            min = preorder[i];

        // Update the maximum
        if (max < preorder[i])
            max = preorder[i];
    }
    // Print the values
    System.out.println("Leftmost node is " + min);
    System.out.println("Rightmost node is " + max);
}

// Driver Code
public static void main(String[] args)
{
        int preorder[] = { 3, 2, 1, 5, 4 };
        int n = 5;
        LeftRightNode(preorder, n);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find leftmost and
# rightmost node from given preorder sequence

# Function to return the leftmost and
# rightmost nodes of the BST whose
# preorder traversal is given
def LeftRightNode(preorder, n):
    # Variables for finding minimum
    # and maximum values of the array
    min = 10**9
    max = -10**9

    for i in range(n):

        # Update the minimum
        if (min > preorder[i]):
            min = preorder[i]

        # Update the maximum
        if (max < preorder[i]):
            max = preorder[i]

    # Print the values
    print("Leftmost node is ",min)
    print("Rightmost node is ",max)

# Driver Code

preorder = [3, 2, 1, 5, 4]
n =len(preorder)

LeftRightNode(preorder, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find leftmost and
// rightmost node from given preorder sequence
using System;

class GFG
{

// Function to return the leftmost and
// rightmost nodes of the BST whose
// preorder traversal is given
static void LeftRightNode(int []preorder, int n)
{
    // Variables for finding minimum
    // and maximum values of the array
    int min = int.MaxValue, max = int.MinValue;

    for (int i = 0; i < n; i++)
    {

        // Update the minimum
        if (min > preorder[i])
            min = preorder[i];

        // Update the maximum
        if (max < preorder[i])
            max = preorder[i];
    }
    // Print the values
    Console.WriteLine("Leftmost node is " + min);
    Console.WriteLine("Rightmost node is " + max);
}

// Driver Code
public static void Main(String[] args)
{
        int []preorder = { 3, 2, 1, 5, 4 };
        int n = 5;
        LeftRightNode(preorder, n);

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find leftmost and
// rightmost node from given preorder sequence

// Function to return the leftmost and
// rightmost nodes of the BST whose
// preorder traversal is given
function LeftRightNode(preorder, n)
{
    // Variables for finding minimum
    // and maximum values of the array
    var min = 1000000000, max = -1000000000;

    for (var i = 0; i < n; i++) {

        // Update the minimum
        if (min > preorder[i])
            min = preorder[i];

        // Update the maximum
        if (max < preorder[i])
            max = preorder[i];
    }

    // Print the values
    document.write( "Leftmost node is " + min + "<br>");
    document.write( "Rightmost node is " + max);
}

// Driver Code
var preorder = [3, 2, 1, 5, 4];
var n = 5;
LeftRightNode(preorder, n);

</script>
```

**Output:** 

```
Leftmost node is 1
Rightmost node is 5
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)