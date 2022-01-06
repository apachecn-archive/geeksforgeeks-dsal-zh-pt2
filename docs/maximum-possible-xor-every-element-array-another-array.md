# 一个数组中的每个元素与另一个数组的最大可能异或

> 原文:[https://www . geesforgeks . org/最大可能-xor-ever-element-array-other-array/](https://www.geeksforgeeks.org/maximum-possible-xor-every-element-array-another-array/)

给出了由 N 个元素组成的两个数组 A 和 B。任务是计算数组 A 中的每个元素与数组 b 的最大可能异或。

**示例:**

```
Input :
A : 7 3 9 12
B : 1 3 5 2
Output : 6 6 12 15
Explanation : 1 xor 7 = 6, 5 xor 3 = 6, 5
xor 9 = 12, 3 xor 12 = 15.
```

一种解决这个问题的简单方法是将数组 A 的每个元素与数组 B 的每个其他元素进行检查，并输出最大异或。
时间复杂度:O(n^2)

一个有效的解决方案是使用 T2 特里数据结构。
我们维护数组 b 中所有元素的二进制表示的 Trie。
现在，对于 A 的每个元素，我们在 trie 中找到最大的 [xor。
假设我们的数字 A[i]是{b1，b2…bn}，其中 b1，b2…bn 是二进制位。我们从 b1 开始。
现在，为了使异或最大化，我们将在执行
异或后尝试使最高有效位为 1。所以，如果 b1 是 0，我们需要 1，反之亦然。在 trie 中，我们转到所需的
位端。如果没有有利的选择，我们就去另一边。这样做，我们将得到最大可能的异或。](https://www.geeksforgeeks.org/minimum-xor-value-pair/)

下面是实现

## C++

```
// C++ code to find the maximum possible X-OR of
// every array element with another array
#include<bits/stdc++.h>
using namespace std;

// Structure of Trie DS
struct trie
{
    int value;
    trie *child[2];
};

// Function to initialise a Trie Node
trie * get()
{
    trie * root = new trie;
    root -> value = 0;
    root -> child[0] = NULL;
    root -> child[1] = NULL;
    return root;
}

// Computing max xor
int max_xor(trie * root, int key)
{
    trie * temp = root;

    // Checking for all bits in integer range
    for (int i = 31; i >= 0; i--)
    {
        // Current bit in the number
        bool current_bit = ( key & ( 1 << i) );

        // Traversing Trie for different bit, if found
        if (temp -> child[1 - current_bit] != NULL)
            temp = temp -> child[1 - current_bit];

        // Traversing Trie for same bit
        else
            temp = temp -> child[current_bit];
    }

    // Returning xor value of maximum bit difference
    // value. Thus, we get maximum xor value
    return (key ^ temp -> value);
}

// Inserting B[] in Trie
void insert(trie * root, int key)
{
    trie * temp = root;

    // Storing 31 bits as integer representation
    for (int i = 31; i >= 0; i--)
    {
        // Current bit in the number
        bool current_bit = key & (1 << i);

        // New node required
        if (temp -> child[current_bit] == NULL)       
            temp -> child[current_bit] = get();

        // Traversing in Trie
        temp = temp -> child[current_bit];
    }
    // Assigning value to the leaf Node
    temp -> value = key;
}

int main()
{
    int A[] = {7, 3, 9, 12};
    int B[] = {1, 3, 5, 2};

    int N = sizeof(A)/sizeof(A[0]);

    // Forming Trie for B[]
    trie * root = get();
    for (int i = 0; i < N; i++)
        insert(root, B[i]);

    for (int i = 0; i < N; i++)
        cout << max_xor(root, A[i]) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the maximum possible X-OR of
// every array element with another array
import java.util.*;

class GFG
{

// Structure of Trie DS
static class trie
{
    int value;
    trie []child = new trie[2];
};

// Function to initialise a Trie Node
static trie get()
{
    trie root = new trie();
    root.value = 0;
    root.child[0] = null;
    root.child[1] = null;
    return root;
}

// Computing max xor
static int max_xor(trie root, int key)
{
    trie temp = root;

    // Checking for all bits in integer range
    for (int i = 31; i >= 0; i--)
    {
        // Current bit in the number
        int current_bit = (key & (1 << i));
        if(current_bit > 0)
            current_bit = 1;

        // Traversing Trie for different bit, if found
        if (temp.child[1 - current_bit] != null)
            temp = temp.child[1 - current_bit];

        // Traversing Trie for same bit
        else
            temp = temp.child[current_bit];
    }

    // Returning xor value of maximum bit difference
    // value. Thus, we get maximum xor value
    return (key ^ temp.value);
}

// Inserting B[] in Trie
static void insert(trie root, int key)
{
    trie temp = root;

    // Storing 31 bits as integer representation
    for (int i = 31; i >= 0; i--)
    {
        // Current bit in the number
        int current_bit = key & (1 << i);
        if(current_bit > 0)
            current_bit = 1;

        //System.out.println(current_bit);
        // New node required
        if (temp.child[current_bit] == null)    
            temp.child[current_bit] = get();

        // Traversing in Trie
        temp = temp.child[current_bit];
    }
    // Assigning value to the leaf Node
    temp.value = key;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = {7, 3, 9, 12};
    int B[] = {1, 3, 5, 2};

    int N = A.length;

    // Forming Trie for B[]
    trie root = get();
    for (int i = 0; i < N; i++)
        insert(root, B[i]);

    for (int i = 0; i < N; i++)
        System.out.println(max_xor(root, A[i]));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 code to find the maximum
# possible X-OR of every array
# element with another array

# Structure of Trie DS
class trie:

    def __init__(self, value: int = 0) -> None:

        self.value = value
        self.child = [None] * 2

# Function to initialise a Trie Node
def get() -> trie:

    root = trie()
    root.value = 0
    root.child[0] = None
    root.child[1] = None

    return root

# Computing max xor
def max_xor(root: trie, key: int) -> int:

    temp = root

    # Checking for all bits in integer range
    for i in range(31, -1, -1):

        # Current bit in the number
        current_bit = (key & (1 << i))
        if (current_bit > 0):
            current_bit = 1

        # Traversing Trie for different bit, if found
        if (temp.child[1 - current_bit] != None):
            temp = temp.child[1 - current_bit]

        # Traversing Trie for same bit
        else:
            temp = temp.child[current_bit]

    # Returning xor value of maximum bit difference
    # value. Thus, we get maximum xor value
    return (key ^ temp.value)

# Inserting B[] in Trie
def insert(root: trie, key: int) -> None:

    temp = root

    # Storing 31 bits as integer representation
    for i in range(31, -1, -1):

        # Current bit in the number
        current_bit = key & (1 << i)
        if (current_bit > 0):
            current_bit = 1

        # New node required
        if (temp.child[current_bit] == None):
            temp.child[current_bit] = get()

        # Traversing in Trie
        temp = temp.child[current_bit]

    # Assigning value to the leaf Node
    temp.value = key

# Driver Code
if __name__ == "__main__":

    A = [ 7, 3, 9, 12 ]
    B = [ 1, 3, 5, 2 ]

    N = len(A)

    # Forming Trie for B[]
    root = get()
    for i in range(N):
        insert(root, B[i])

    for i in range(N):
        print(max_xor(root, A[i]))

# This code is contributed by sanjeev2552
```

## C#

```
// C# code to find the maximum possible X-OR of
// every array element with another array
using System;

class GFG
{

// Structure of Trie DS
class trie
{
    public int value;
    public trie []child = new trie[2];
};

// Function to initialise a Trie Node
static trie get()
{
    trie root = new trie();
    root.value = 0;
    root.child[0] = null;
    root.child[1] = null;
    return root;
}

// Computing max xor
static int max_xor(trie root, int key)
{
    trie temp = root;

    // Checking for all bits in integer range
    for (int i = 31; i >= 0; i--)
    {
        // Current bit in the number
        int current_bit = (key & (1 << i));
        if(current_bit > 0)
            current_bit = 1;

        // Traversing Trie for different bit, if found
        if (temp.child[1 - current_bit] != null)
            temp = temp.child[1 - current_bit];

        // Traversing Trie for same bit
        else
            temp = temp.child[current_bit];
    }

    // Returning xor value of maximum bit difference
    // value. Thus, we get maximum xor value
    return (key ^ temp.value);
}

// Inserting B[] in Trie
static void insert(trie root, int key)
{
    trie temp = root;

    // Storing 31 bits as integer representation
    for (int i = 31; i >= 0; i--)
    {
        // Current bit in the number
        int current_bit = key & (1 << i);
        if(current_bit > 0)
            current_bit = 1;

        // System.out.println(current_bit);
        // New node required
        if (temp.child[current_bit] == null)    
            temp.child[current_bit] = get();

        // Traversing in Trie
        temp = temp.child[current_bit];
    }

    // Assigning value to the leaf Node
    temp.value = key;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = {7, 3, 9, 12};
    int []B = {1, 3, 5, 2};

    int N = A.Length;

    // Forming Trie for B[]
    trie root = get();
    for (int i = 0; i < N; i++)
        insert(root, B[i]);

    for (int i = 0; i < N; i++)
        Console.WriteLine(max_xor(root, A[i]));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript code to find the maximum possible X-OR of
// every array element with another array

// Structure of Trie DS
class trie
{
    constructor()
    {
        this.value=0;
        this.child = new Array(2);

    }
}

// Function to initialise a Trie Node   
function get()
{
    let root = new trie();
    root.value = 0;
    root.child[0] = null;
    root.child[1] = null;
    return root;
}

// Computing max xor
function max_xor(root,key)
{
    let temp = root;

    // Checking for all bits in integer range
    for (let i = 31; i >= 0; i--)
    {
        // Current bit in the number
        let current_bit = (key & (1 << i));
        if(current_bit > 0)
            current_bit = 1;

        // Traversing Trie for different bit, if found
        if (temp.child[1 - current_bit] != null)
            temp = temp.child[1 - current_bit];

        // Traversing Trie for same bit
        else
            temp = temp.child[current_bit];
    }

    // Returning xor value of maximum bit difference
    // value. Thus, we get maximum xor value
    return (key ^ temp.value);
}

// Inserting B[] in Trie
function insert(root,key)
{
    let temp = root;

    // Storing 31 bits as integer representation
    for (let i = 31; i >= 0; i--)
    {
        // Current bit in the number
        let current_bit = key & (1 << i);
        if(current_bit > 0)
            current_bit = 1;

        //System.out.println(current_bit);
        // New node required
        if (temp.child[current_bit] == null)   
            temp.child[current_bit] = get();

        // Traversing in Trie
        temp = temp.child[current_bit];
    }
    // Assigning value to the leaf Node
    temp.value = key;
}

// Driver Code
let A=[7, 3, 9, 12];
let B=[1, 3, 5, 2];

let N = A.length;
// Forming Trie for B[]
let root = get();
for (let i = 0; i < N; i++)
    insert(root, B[i]);

for (let i = 0; i < N; i++)
    document.write(max_xor(root, A[i])+"<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
6
6
12
15
```

三元组:O(N×MAX _ BITS)其中 **MAX_BITS** 是数字的二进制表示中的最大位数。
计算最大位差:0(N×MAX _ BITS)

时间复杂度:0(N×MAX _ BITS)

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。