# 给定高度的 AVL 树中的最小节点数

> 原文:[https://www . geesforgeks . org/给定高度 avl 树中的最小节点数/](https://www.geeksforgeeks.org/minimum-number-of-nodes-in-an-avl-tree-with-given-height/)

给定 AVL 树“h”的高度，任务是找到树可以具有的最小节点数。

**示例:**

```
Input : H = 0
Output : N = 1
Only '1' node is possible if the height 
of the tree is '0' which is the root node.

Input : H = 3
Output : N = 7
```

**递归方法:**在 AVL 树中，我们必须保持高度平衡属性，即对于每个节点，左右子树的高度差不能大于-1、0 或 1。

我们将尝试创建一个递归关系，以找到给定高度 n(h)的最小节点数。

*   对于高度= 0，我们在 AVL 树中只能有一个节点，即 n(0) = 1
*   对于高度= 1，我们可以在 AVL 树中至少有两个节点，即 n(1) = 2
*   现在对于任何高度“h”，根将有两个子树(左和右)。其中一个高度为 h-1，另一个高度为 h-2。[排除根节点]
*   所以， **n(h) = 1 + n(h-1) + n(h-2)** 是 h 所需的递推关系> =2【根节点加 1】

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find
// minimum number of nodes
int AVLnodes(int height)
{
    // Base Conditions
    if (height == 0)
        return 1;
    else if (height == 1)
        return 2;

    // Recursive function call
    // for the recurrence relation
    return (1 + AVLnodes(height - 1) + AVLnodes(height - 2));
}

// Driver Code
int main()
{
    int H = 3;
    cout << AVLnodes(H) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG{

// Function to find
// minimum number of nodes
static int AVLnodes(int height)
{
    // Base Conditions
    if (height == 0)
        return 1;
    else if (height == 1)
        return 2;

    // Recursive function call
    // for the recurrence relation
    return (1 + AVLnodes(height - 1) + AVLnodes(height - 2));
}

// Driver Code
public static void main(String args[])
{
    int H = 3;
    System.out.println(AVLnodes(H));
}
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find minimum
# number of nodes
def AVLnodes(height):

    # Base Conditions
    if (height == 0):
        return 1
    elif (height == 1):
        return 2

    # Recursive function call
    # for the recurrence relation
    return (1 + AVLnodes(height - 1) +
                AVLnodes(height - 2))

# Driver Code
if __name__ == '__main__':
    H = 3
    print(AVLnodes(H))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find
// minimum number of nodes
static int AVLnodes(int height)
{
    // Base Conditions
    if (height == 0)
        return 1;
    else if (height == 1)
        return 2;

    // Recursive function call
    // for the recurrence relation
    return (1 + AVLnodes(height - 1) +
                AVLnodes(height - 2));
}

// Driver Code
public static void Main()
{
    int H = 3;
    Console.Write(AVLnodes(H));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find minimum
// number of nodes
function AVLnodes($height)
{
    // Base Conditions
    if ($height == 0)
        return 1;
    else if ($height == 1)
        return 2;

    // Recursive function call
    // for the recurrence relation
    return (1 + AVLnodes($height - 1) +
                AVLnodes($height - 2));
}

// Driver Code
$H = 3;
echo(AVLnodes($H));

// This code is contributed
// by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find
// minimum number of nodes
function AVLnodes(height)
{

    // Base Conditions
    if (height == 0)
        return 1;
    else if (height == 1)
        return 2;

    // Recursive function call
    // for the recurrence relation
    return (1 + AVLnodes(height - 1) +
                AVLnodes(height - 2));
}

// Driver code
let H = 3;

document.write(AVLnodes(H));

// This code is contributed by decode2207

</script>
```

**Output:** 

```
7
```

**尾部递归方法:**

*   求 n(h)的递归函数(高度为“h”)的 AVL 树中可能的最小节点数为 n(h)= 1+n(h-1)+n(h-2)；h > = 2；n(0)= 1；n(1)= 2；
*   为了创建一个尾部递归函数，我们将维护 1 + n(h-1) + n(h-2)作为函数参数，这样我们就不用计算它，而是直接将其值返回给主函数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return
//minimum number of nodes
int AVLtree(int H, int a = 1, int b = 2)
{
    // Base Conditions
    if (H == 0)
        return 1;
    if (H == 1)
        return b;

    // Tail Recursive Call
    return AVLtree(H - 1, b, a + b + 1);
}

// Driver Code
int main()
{
    int H = 5;
    int answer = AVLtree(H);

    // Output the result
    cout << "n(" << H << ") = "
         << answer << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return
//minimum number of nodes
static int AVLtree(int H, int a, int b)
{
    // Base Conditions
    if (H == 0)
        return 1;
    if (H == 1)
        return b;

    // Tail Recursive Call
    return AVLtree(H - 1, b, a + b + 1);
}

// Driver Code
public static void main(String[] args)
{
    int H = 5;
    int answer = AVLtree(H, 1, 2);

    // Output the result
    System.out.println("n(" + H + ") = " + answer);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return
# minimum number of nodes
def AVLtree(H, a, b):

    # Base Conditions
    if(H == 0):
        return 1;
    if(H == 1):
        return b;

    # Tail Recursive Call
    return AVLtree(H - 1, b, a + b + 1);

# Driver Code
if __name__ == '__main__':
    H = 5;
    answer = AVLtree(H, 1, 2);

    # Output the result
    print("n(", H , ") = "\
        , answer);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return
//minimum number of nodes
static int AVLtree(int H, int a, int b)
{
    // Base Conditions
    if (H == 0)
        return 1;
    if (H == 1)
        return b;

    // Tail Recursive Call
    return AVLtree(H - 1, b, a + b + 1);
}

// Driver Code
public static void Main(String[] args)
{
    int H = 5;
    int answer = AVLtree(H, 1, 2);

    // Output the result
    Console.WriteLine("n(" + H + ") = " + answer);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return
    //minimum number of nodes
    function AVLtree(H, a, b)
    {
        // Base Conditions
        if (H == 0)
            return 1;
        if (H == 1)
            return b;

        // Tail Recursive Call
        return AVLtree(H - 1, b, a + b + 1);
    }

    let H = 5;
    let answer = AVLtree(H, 1, 2);

    // Output the result
    document.write("n(" + H + ") = " + answer);

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
n(5) = 20
```