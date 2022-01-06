# 给定范围内的最大前缀和

> 原文:[https://www . geesforgeks . org/maximum-prefix-sum-given-range/](https://www.geeksforgeeks.org/maximum-prefix-sum-given-range/)

给定 n 个整数和 q 个查询的数组，每个查询具有从 l 到 r 的范围。找到范围 l–r 的最大前缀和。
示例:

```
Input: a[] = {-1, 2, 3, -5} 
       q = 2
       l = 0, r = 3
       l = 1, r = 3

Output: 4
        5

Explanation:- The range (0, 3) in the 1st query has
              [-1, 2, 3, -5], since it is prefix, 
              we have to start from -1\. Hence, the 
              max prefix sum will be -1 + 2 + 3 = 4.
              The range (1, 3) in the 2nd query has 
              [2, 3, -5], since it is prefix, we 
              have to start from 2\. Hence, the max
              prefix sum will be 2 + 3 = 5.

Input: a[] = {-2, -3, 4, -1, -2, 1, 5, -3} 
       q = 1
       l = 1 r = 7 

Output: 4

Explanation:- The range (1, 7) in the 1st query has 
              [-3, 4, -1, -2, 1, 5, -3], since it is
              prefix, we have to start from -3\. 
              Hence, the max prefix sum will be 
              -3 + 4 - 1 - 2 + 1 + 5 = 4.
```

**正常方法:**
一个简单的解决方案是运行一个从 l 到 r 的循环，并为每个查询计算从 l 到 r 的最大前缀和。
**时间复杂度**:O(q * n)
**辅助空间** : O(1)
**高效方法:**
一种高效方法是构建一个段树，其中每个节点存储两个值(sum 和 prefix_sum)，并对其进行范围查询以找到最大前缀和。但是为了构建段树，我们必须考虑在树的节点上存储什么。
为了找出最大前缀和，我们需要两件事，一是和，二是前缀和。合并将返回两件事，范围的总和和前缀总和，将 *max(前缀. left，前缀. sum +前缀. right)* 存储在段树中。
如果我们深入研究，任意两个区间组合的最大前缀和，要么是左侧前缀和，要么是左侧前缀和+右侧前缀和，以最大值为准。
**段树的表示:**
1。叶节点是输入数组的元素。
2。每个内部节点代表叶节点的一些合并。对于不同的问题，合并可能会有所不同。对于这个问题，合并是一个节点下的叶子的和。
树的数组表示用于表示段树。对于索引 I 处的每个节点，左子节点位于索引 *2*i+1* ，右子节点位于 *2*i+2* ，父节点位于 *(i-1)/2。*
**从给定数组构建段树:**
我们从段 arr[0]开始。。。n-1]。并且每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，并且对于每个这样的段，我们将总和和前缀总和存储在相应的节点中。
然后我们对段树进行范围查询，找出给定范围的最大前缀和，并输出最大前缀和。
下面是上述方法的 C++实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find
// maximum prefix sum
#include <bits/stdc++.h>
using namespace std;

// struct two store two values in one node
struct Node {
    int sum;
    int prefix;
};

Node tree[4 * 10000];

// function to build the segment tree
void build(int a[], int index, int beg, int end)
{
    if (beg == end) {

        // If there is one element in array,
        // store it in current node of
        // segment tree
        tree[index].sum = a[beg];
        tree[index].prefix = a[beg];
    } else {
        int mid = (beg + end) / 2;

        // If there are more than one elements,
        // then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid);
        build(a, 2 * index + 2, mid + 1, end);

        // adds the sum and stores in the index
        // position of segment tree
        tree[index].sum = tree[2 * index + 1].sum +
                          tree[2 * index + 2].sum;

        // stores the max of prefix-sum either
        // from right or from left.
        tree[index].prefix = max(tree[2 * index + 1].prefix,
                                 tree[2 * index + 1].sum +
                                tree[2 * index + 2].prefix);
    }
}

// function to do the range query in the segment
// tree for the maximum prefix sum
Node query(int index, int beg, int end, int l, int r)
{
    Node result;
    result.sum = result.prefix = -1;

    // If segment of this node is outside the given
    // range, then return the minimum value.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    int mid = (beg + end) / 2;

    // if left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1, end,
                                         l, r);

    // if right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg, mid,
                                       l, r);

    // If a part of this segment overlaps with
    // the given range
    Node left = query(2 * index + 1, beg, mid,
                                        l, r);
    Node right = query(2 * index + 2, mid + 1,
                                   end, l, r);

    // adds the sum of the left and right
    // segment
    result.sum = left.sum + right.sum;

    // stores the max of prefix-sum
    result.prefix = max(left.prefix, left.sum +
                            right.prefix);

    // returns the value
    return result;
}

// driver program to test the program
int main()
{

    int a[] = { -2, -3, 4, -1, -2, 1, 5, -3 };

    // calculates the length of array
    int n = sizeof(a) / sizeof(a[0]);

    // calls the build function to build
    // the segment tree
    build(a, 0, 0, n - 1);

    // find the max prefix-sum between
    // 3rd and 5th index of array
    cout << query(0, 0, n - 1, 3, 5).prefix
         << endl;

    // find the max prefix-sum between
    // 0th and 7th index of array
    cout << query(0, 0, n - 1, 1, 7).prefix
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find
// maximum prefix sum
class GFG
{

// two store two values in one node
static class Node
{
    int sum;
    int prefix;
};

static Node []tree = new Node[4 * 10000];
static
{
    for(int i = 0; i < tree.length; i++)
        tree[i] = new Node();
}

// function to build the segment tree
static void build(int a[], int index, int beg, int end)
{
    if (beg == end)
    {

        // If there is one element in array,
        // store it in current node of
        // segment tree
        tree[index].sum = a[beg];
        tree[index].prefix = a[beg];
    } else {
        int mid = (beg + end) / 2;

        // If there are more than one elements,
        // then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid);
        build(a, 2 * index + 2, mid + 1, end);

        // adds the sum and stores in the index
        // position of segment tree
        tree[index].sum = tree[2 * index + 1].sum +
                        tree[2 * index + 2].sum;

        // stores the max of prefix-sum either
        // from right or from left.
        tree[index].prefix = Math.max(tree[2 * index + 1].prefix,
                                tree[2 * index + 1].sum +
                                tree[2 * index + 2].prefix);
    }
}

// function to do the range query in the segment
// tree for the maximum prefix sum
static Node query(int index, int beg, int end, int l, int r)
{
    Node result = new Node();
    result.sum = result.prefix = -1;

    // If segment of this node is outside the given
    // range, then return the minimum value.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    int mid = (beg + end) / 2;

    // if left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1, end,
                                        l, r);

    // if right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg, mid,
                                    l, r);

    // If a part of this segment overlaps with
    // the given range
    Node left = query(2 * index + 1, beg, mid,
                                        l, r);
    Node right = query(2 * index + 2, mid + 1,
                                end, l, r);

    // adds the sum of the left and right
    // segment
    result.sum = left.sum + right.sum;

    // stores the max of prefix-sum
    result.prefix = Math.max(left.prefix, left.sum +
                            right.prefix);

    // returns the value
    return result;
}

// Driver code
public static void main(String[] args)
{

    int a[] = { -2, -3, 4, -1, -2, 1, 5, -3 };

    // calculates the length of array
    int n = a.length;

    // calls the build function to build
    // the segment tree
    build(a, 0, 0, n - 1);

    // find the max prefix-sum between
    // 3rd and 5th index of array
    System.out.print(query(0, 0, n - 1, 3, 5).prefix
        +"\n");

    // find the max prefix-sum between
    // 0th and 7th index of array
    System.out.print(query(0, 0, n - 1, 1, 7).prefix
        +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find
// maximum prefix sum
using System;

class GFG
{

// two store two values in one node
class Node
{
    public int sum;
    public int prefix;
};

static Node []tree = new Node[4 * 10000];

// function to build the segment tree
static void build(int []a, int index, int beg, int end)
{
    if (beg == end)
    {

        // If there is one element in array,
        // store it in current node of
        // segment tree
        tree[index].sum = a[beg];
        tree[index].prefix = a[beg];
    } else {
        int mid = (beg + end) / 2;

        // If there are more than one elements,
        // then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid);
        build(a, 2 * index + 2, mid + 1, end);

        // adds the sum and stores in the index
        // position of segment tree
        tree[index].sum = tree[2 * index + 1].sum +
                        tree[2 * index + 2].sum;

        // stores the max of prefix-sum either
        // from right or from left.
        tree[index].prefix = Math.Max(tree[2 * index + 1].prefix,
                                tree[2 * index + 1].sum +
                                tree[2 * index + 2].prefix);
    }
}

// function to do the range query in the segment
// tree for the maximum prefix sum
static Node query(int index, int beg, int end, int l, int r)
{
    Node result = new Node();
    result.sum = result.prefix = -1;

    // If segment of this node is outside the given
    // range, then return the minimum value.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    int mid = (beg + end) / 2;

    // if left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1, end,
                                        l, r);

    // if right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg, mid,
                                    l, r);

    // If a part of this segment overlaps with
    // the given range
    Node left = query(2 * index + 1, beg, mid,
                                        l, r);
    Node right = query(2 * index + 2, mid + 1,
                                end, l, r);

    // adds the sum of the left and right
    // segment
    result.sum = left.sum + right.sum;

    // stores the max of prefix-sum
    result.prefix = Math.Max(left.prefix, left.sum +
                            right.prefix);

    // returns the value
    return result;
}

// Driver code
public static void Main(String[] args)
{

    for(int i = 0; i < tree.Length; i++)
        tree[i] = new Node();
    int []a = { -2, -3, 4, -1, -2, 1, 5, -3 };

    // calculates the length of array
    int n = a.Length;

    // calls the build function to build
    // the segment tree
    build(a, 0, 0, n - 1);

    // find the max prefix-sum between
    // 3rd and 5th index of array
    Console.Write(query(0, 0, n - 1, 3, 5).prefix
        +"\n");

    // find the max prefix-sum between
    // 0th and 7th index of array
    Console.Write(query(0, 0, n - 1, 1, 7).prefix
        +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find
# maximum prefix sum

# struct two store two values in one node

# function to build the segment tree
def build(a, index, beg, end):
    global tree

    if (beg == end):

        # If there is one element in array,
        # store it in current node of
        # segment tree
        tree[index][0] = a[beg]
        tree[index][1] = a[beg]
    else:
        mid = (beg + end) // 2

        # If there are more than one elements,
        # then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid)
        build(a, 2 * index + 2, mid + 1, end)

        # adds the sum and stores in the index
        # position of segment tree
        tree[index][0] = tree[2 * index + 1][0] + tree[2 * index + 2][0]

        # stores the max of prefix-sum either
        # from right or from left.
        tree[index][1] = max(tree[2 * index + 1][1],tree[2 * index + 1][0] + tree[2 * index + 2][1])

# function to do the range query in the segment
# tree for the maximum prefix sum
def query(index, beg, end, l, r):
    global tree
    result = [-1, -1]
    # result[0] = result[1] = -1

    # If segment of this node is outside the given
    # range, then return the minimum value.
    if (beg > r or end < l):
        return result

    # If segment of this node is a part of given
    # range, then return the node of the segment
    if (beg >= l and end <= r):
        return tree[index]

    mid = (beg + end) // 2

    # if left segment of this node falls out of
    # range, then recur in the right side of
    # the tree
    if (l > mid):
        return query(2 * index + 2, mid + 1, end, l, r)

    # if right segment of this node falls out of
    # range, then recur in the left side of
    # the tree
    if (r <= mid):
        return query(2 * index + 1, beg, mid, l, r)

    # If a part of this segment overlaps with
    # the given range
    left = query(2 * index + 1, beg, mid, l, r)
    right = query(2 * index + 2, mid + 1, end, l, r)

    # adds the sum of the left and right
    # segment
    result[0] = left[0] + right[0]

    # stores the max of prefix-sum
    result[1] = max(left[1], left[0] + right[1])

    # returns the value
    return result

# driver program to test the program
if __name__ == '__main__':

    a = [-2, -3, 4, -1, -2, 1, 5, -3 ]

    tree = [[0,0] for i in range(4 * 10000)]

    # calculates the length of array
    n = len(a)

    # calls the build function to build
    # the segment tree
    build(a, 0, 0, n - 1)

    # find the max prefix-sum between
    # 3rd and 5th index of array
    print(query(0, 0, n - 1, 3, 5)[1])

    # find the max prefix-sum between
    # 0th and 7th index of array
    print(query(0, 0, n - 1, 1, 7)[1])

    # This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

// JavaScript program to find
// maximum prefix sum

    // two store two values in one node
    class Node
    {
        constructor()
        {
            let sum,prefix;
        }
    }

    let tree=new Array(4 * 10000);
    for(let i = 0; i < tree.length; i++)
        tree[i] = new Node();

    // function to build the segment tree
    function build(a,index,beg,end)
    {
        if (beg == end)
    {

        // If there is one element in array,
        // store it in current node of
        // segment tree
        tree[index].sum = a[beg];
        tree[index].prefix = a[beg];
    } else {
        let mid = Math.floor((beg + end) / 2);

        // If there are more than one elements,
        // then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid);
        build(a, 2 * index + 2, mid + 1, end);

        // adds the sum and stores in the index
        // position of segment tree
        tree[index].sum = tree[2 * index + 1].sum +
                        tree[2 * index + 2].sum;

        // stores the max of prefix-sum either
        // from right or from left.
        tree[index].prefix =
        Math.max(tree[2 * index + 1].prefix,
        tree[2 * index + 1].sum +
        tree[2 * index + 2].prefix);
    }
    }

    // function to do the range query in the segment
// tree for the maximum prefix sum
    function query(index,beg,end,l,r)
    {
        let result = new Node();
    result.sum = result.prefix = -1;

    // If segment of this node is outside the given
    // range, then return the minimum value.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    let mid = Math.floor((beg + end) / 2);

    // if left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1, end,
                                        l, r);

    // if right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg, mid,
                                    l, r);

    // If a part of this segment overlaps with
    // the given range
    let left = query(2 * index + 1, beg, mid,
                                        l, r);
    let right = query(2 * index + 2, mid + 1,
                                end, l, r);

    // adds the sum of the left and right
    // segment
    result.sum = left.sum + right.sum;

    // stores the max of prefix-sum
    result.prefix = Math.max(left.prefix, left.sum +
                            right.prefix);

    // returns the value
    return result;
    }

    // Driver code
    let a=[-2, -3, 4, -1, -2, 1, 5, -3];
    // calculates the length of array
    let n = a.length;

    // calls the build function to build
    // the segment tree
    build(a, 0, 0, n - 1);

    // find the max prefix-sum between
    // 3rd and 5th index of array
    document.write(query(0, 0, n - 1, 3, 5).prefix
        +"<br>");

    // find the max prefix-sum between
    // 0th and 7th index of array
    document.write(query(0, 0, n - 1, 1, 7).prefix
        +"<br>");

// This code is contributed by patel2127

</script>
```

**输出:**

```
-1
4
```

**时间复杂度:**
树木构建的时间复杂度为 **O(n)** 。总共有 2n-1 个节点，每个节点的值在树构造中只计算一次。
每次查询的时间复杂度为 **O(log n)。**
问题的时间复杂度为 **O(q * log n)**
本文由 **Raja Vikramaditya** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。