# 段树节点的水平交替 GCD 和 LCM

> 原文:[https://www . geesforgeks . org/level wise-alternating-gcd-LCM-nodes-segment-tree/](https://www.geeksforgeeks.org/levelwise-alternating-gcd-lcm-nodes-segment-tree/)

一个逐级的 GCD/LCM 交替段树是一个段树，这样在每一级操作 GCD 和 LCM 交替。换句话说，在级别 1，左和右子树通过 GCD 操作组合在一起，即父节点=左子 **GCD** 右子，在级别 2，左
和右子树通过 LCM 操作组合在一起，即父节点=左子 **LCM** 右子
这种类型的段树具有以下类型的结构:

操作(GCD)和(LCM)指示执行了哪个操作来合并子节点
给定 N 个叶节点，任务是构建这样的段树并打印根节点。
示例:

```
Input : arr[] = { 5, 4, 8, 10, 6 }
Output : Value at Root Node = 2
Explanation : The image given above shows the 
segment tree corresponding to the given
set leaf nodes.
```

**先决条件:** [段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)
在这个段树中，我们进行两个操作: **GCD 和 LCM** 。
现在，与针对子树递归传递的信息一起，由于这些操作逐级交替，所以关于要在该级执行的操作的信息也被传递。需要注意的是，当父节点调用其左右子节点时，相同的操作信息会传递给这两个子节点，因为它们处于同一级别。
我们分别用 0 和 1 来表示 GCD 和 LCM 这两个操作。然后，如果在第一级执行 GCD 操作，那么在第(i + 1)级将执行 LCM 操作。因此，如果级别 I 有 0 作为操作，那么级别(i + 1)将有 1 作为操作。

```
Operation at Level (i + 1) = ! (Operation at Level i)
where,
Operation at Level i ∊ {0, 1}
```

对图像的仔细分析表明，如果树的高度是偶数，那么根节点是其左右子节点的 LCM 操作的结果，否则是 GCD 操作的结果。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Recursive function to return gcd of a and b
int gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
       return 0;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a-b, b);
    return gcd(a, b-a);
}

// A utility function to get the middle index from
// corner indexes.
int getMid(int s, int e) { return s + (e - s) / 2; }

void STconstructUtill(int arr[], int ss, int se, int* st,
                                          int si, int op)
{
    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se) {
        st[si] = arr[ss];
        return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum of
    // values in this node
    int mid = getMid(ss, se);

    // Build the left and the right subtrees by using
    // the fact that operation at level (i + 1) = !
    // (operation at level i)
    STconstructUtill(arr, ss, mid, st, si * 2 + 1, !op);
    STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, !op);

    // merge the left and right subtrees by checking
    // the operation to be carried. If operation = 1,
    // then do GCD else LCM
    if (op == 1) {
        // GCD operation
        st[si] = __gcd(st[2 * si + 1], st[2 * si + 2]);
    }
    else {
        // LCM operation
        st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
                   (gcd(st[2 * si + 1], st[2 * si + 2]));
    }
}

/* Function to construct segment tree from given array.
This function allocates memory for segment tree and
calls STconstructUtil() to fill the allocated memory */
int* STconstruct(int arr[], int n)
{
    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // allocate memory
    int* st = new int[max_size];

    // operation = 1(GCD) if Height of tree is
    // even else it is 0(LCM) for the root node
    int opAtRoot = (x % 2 == 0 ? 0 : 1);

    // Fill the allocated memory st
    STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot);

    // Return the constructed segment tree
    return st;
}

int main()
{
    int arr[] = { 5, 4, 8, 10, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree
    int* st = STconstruct(arr, n);

    // 0-based indexing in segment tree
    int rootIndex = 0;

    cout << "Value at Root Node = " << st[rootIndex];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;
class GFG
{

  // Recursive function to return gcd of a and b
  static int gcd(int a, int b)
  {

    // Everything divides 0 
    if (a == 0 || b == 0)
      return 0;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return gcd(a - b, b);
    return gcd(a, b - a);
  }

  // A utility function to get the middle index from
  // corner indexes.
  static int getMid(int s, int e) { return s + (e - s) / 2; }
  static void STconstructUtill(int[] arr, int ss,
                               int se, int[] st, 
                               int si, boolean op)
  {

    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se)
    {
      st[si] = arr[ss];
      return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum of
    // values in this node
    int mid = getMid(ss, se);

    // Build the left and the right subtrees by using
    // the fact that operation at level (i + 1) = !
    // (operation at level i)
    STconstructUtill(arr, ss, mid, st, si * 2 + 1, !op);
    STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, !op);

    // merge the left and right subtrees by checking
    // the operation to be carried. If operation = 1,
    // then do GCD else LCM
    if(op == true)
    {

      // GCD operation
      st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
    }
    else
    {

      // LCM operation
      st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
        (gcd(st[2 * si + 1], st[2 * si + 2]));
    }
  }

  /* Function to construct segment tree from given array.
    This function allocates memory for segment tree and 
    calls STconstructUtil() to fill the allocated memory */
  static int[] STconstruct(int arr[], int n)
  {

    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(Math.ceil((Math.log(n)/Math.log(2))));

    // maximum size of segment tree
    int max_size = 2 * (int)Math.pow(2, x) - 1;

    // allocate memory
    int[] st = new int[max_size];
    boolean opAtRoot;

    // operation = 1(GCD) if Height of tree is
    // even else it is 0(LCM) for the root node
    if(x % 2 == 0)
    {
      opAtRoot = false;
    }
    else
    {
      opAtRoot = true;
    }

    // Fill the allocated memory st
    STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot);

    // Return the constructed segment tree
    return st;
  }

  // Driver code
  public static void main (String[] args)
  {
    int[] arr = { 5, 4, 8, 10, 6 };
    int n = arr.length;

    // Build segment tree
    int[] st=STconstruct(arr, n);

    // 0-based indexing in segment tree
    System.out.println("Value at Root Node = " + st[0]);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
from math import ceil,floor,log

# Recursive function to return gcd of a and b
def gcd(a, b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return gcd(a - b, b)
    return gcd(a, b - a)

# A utility function to get the middle index from
# corner indexes.
def getMid(s, e):
    return s + (e - s) // 2

def STconstructUtill(arr, ss, se, st, si, op):

    # If there is one element in array, store it in
    # current node of segment tree and return
    if (ss == se):
        st[si] = arr[ss]
        return

    # If there are more than one elements, then recur
    # for left and right subtrees and store the sum of
    # values in this node
    mid = getMid(ss, se)

    # Build the left and the right subtrees by using
    # the fact that operation at level (i + 1) = !
    # (operation at level i)
    STconstructUtill(arr, ss, mid, st, si * 2 + 1, not op)
    STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, not op)

    # merge the left and right subtrees by checking
    # the operation to be carried. If operation = 1,
    # then do GCD else LCM
    if (op == 1):

        # GCD operation
        st[si] =gcd(st[2 * si + 1], st[2 * si + 2])
    else :

        # LCM operation
        st[si] = (st[2 * si + 1] * st[2 * si + 2]) //(gcd(st[2 * si + 1], st[2 * si + 2]))
#
# /* Function to construct segment tree from given array.
# This function allocates memory for segment tree and
# calls STconstructUtil() to fill the allocated memory */
def STconstruct(arr, n):
    # Allocate memory for segment tree

    # Height of segment tree
    x = ceil(log(n, 2))

    # maximum size of segment tree
    max_size = 2 *pow(2, x) - 1

    # allocate memory
    st = [0]*max_size

    # operation = 1(GCD) if Height of tree is
    # even else it is 0(LCM) for the root node
    if (x % 2 == 0):
        opAtRoot = 0
    else:
        opAtRoot = 1

    # Fill the allocated memory st
    STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot)

    # Return the constructed segment tree
    return st

# Driver code
if __name__ == '__main__':
    arr = [5, 4, 8, 10, 6]
    n = len(arr)

    # Build segment tree
    st = STconstruct(arr, n)

    # 0-based indexing in segment tree
    rootIndex = 0

    print("Value at Root Node = ",st[rootIndex])

# This code is contributed by mohit kumar 29
```

## C#

```
using System;

class GFG
{

  // Recursive function to return gcd of a and b
  static int gcd(int a, int b)
  {

    // Everything divides 0 
    if (a == 0 || b == 0)
      return 0;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return gcd(a - b, b);
    return gcd(a, b - a);
  }

  // A utility function to get the middle index from
  // corner indexes.
  static int getMid(int s, int e) { return s + (e - s) / 2; }
  static void STconstructUtill(int[] arr, int ss,
                               int se, int[] st,
                               int si, bool op)
  {

    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se)
    {
      st[si] = arr[ss];
      return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum of
    // values in this node
    int mid = getMid(ss, se);

    // Build the left and the right subtrees by using
    // the fact that operation at level (i + 1) = !
    // (operation at level i)
    STconstructUtill(arr, ss, mid, st, si * 2 + 1, !op);
    STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, !op);

    // merge the left and right subtrees by checking
    // the operation to be carried. If operation = 1,
    // then do GCD else LCM
    if(op == true)
    {

      // GCD operation
      st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
    }
    else
    {

      // LCM operation
      st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
        (gcd(st[2 * si + 1], st[2 * si + 2]));
    }
  }

  /* Function to construct segment tree from given array.
    This function allocates memory for segment tree and 
    calls STconstructUtil() to fill the allocated memory */
  static int[] STconstruct(int[] arr, int n)
  {

    // Allocate memory for segment tree
    // Height of segment tree
    int x = (int)(Math.Ceiling((Math.Log(n)/Math.Log(2))));

    // maximum size of segment tree
    int max_size = 2 * (int)Math.Pow(2, x) - 1;

    // allocate memory
    int[] st = new int[max_size];
    bool opAtRoot;

    // operation = 1(GCD) if Height of tree is
    // even else it is 0(LCM) for the root node
    if(x % 2 == 0)
    {
      opAtRoot = false;
    }
    else
    {
      opAtRoot = true;
    }

    // Fill the allocated memory st
    STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot);

    // Return the constructed segment tree
    return st;
  }

  // Driver code
  static public void Main ()
  {
    int[] arr = { 5, 4, 8, 10, 6 };
    int n = arr.Length;

    // Build segment tree
    int[] st=STconstruct(arr, n);

    // 0-based indexing in segment tree
    Console.WriteLine("Value at Root Node = " + st[0]);
  }
}

//  This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Recursive function to return gcd of a and b
    function gcd(a , b) {

        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a - b, b);
        return gcd(a, b - a);
    }

    // A utility function to get the middle index from
    // corner indexes.
    function getMid(s , e) {
        return s + parseInt((e - s) / 2);
    }

    function STconstructUtill(arr , ss , se,  st , si, op) {

        // If there is one element in array, store it in
        // current node of segment tree and return
        if (ss == se) {
            st[si] = arr[ss];
            return;
        }

        // If there are more than one elements, then recur
        // for left and right subtrees and store the sum of
        // values in this node
        var mid = getMid(ss, se);

        // Build the left and the right subtrees by using
        // the fact that operation at level (i + 1) = !
        // (operation at level i)
        STconstructUtill(arr, ss, mid, st, si * 2 + 1, !op);
        STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, !op);

        // merge the left and right subtrees by checking
        // the operation to be carried. If operation = 1,
        // then do GCD else LCM
        if (op == true) {

            // GCD operation
            st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
        } else {

            // LCM operation
            st[si] = (st[2 * si + 1] * st[2 * si + 2]) / (gcd(st[2 * si + 1], st[2 * si + 2]));
        }
    }

    /*
     * Function to construct segment tree from given array. This function allocates
     * memory for segment tree and calls STconstructUtil() to fill the allocated
     * memory
     */
    function STconstruct(arr , n) {

        // Allocate memory for segment tree

        // Height of segment tree
        var x = parseInt( (Math.ceil((Math.log(n) / Math.log(2)))));

        // maximum size of segment tree
        var max_size = 2 * parseInt( Math.pow(2, x) - 1);

        // allocate memory
        var st = Array(max_size).fill(0);
        var opAtRoot;

        // operation = 1(GCD) if Height of tree is
        // even else it is 0(LCM) for the root node
        if (x % 2 == 0) {
            opAtRoot = false;
        } else {
            opAtRoot = true;
        }

        // Fill the allocated memory st
        STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot);

        // Return the constructed segment tree
        return st;
    }

    // Driver code

        var arr = [ 5, 4, 8, 10, 6 ];
        var n = arr.length;

        // Build segment tree
        var st = STconstruct(arr, n);

        // 0-based indexing in segment tree
        document.write("Value at Root Node = " + st[0]);

// This code is contributed by umadevi9616
</script>
```

**输出:**

```
Value at Root Node = 2
```

树构建的时间复杂度是 O(n)，因为总共有 2*n-1 个节点，每个节点的值都是一次性计算出来的。
现在执行点更新，即使用给定的索引和值更新值，可以通过遍历树到叶节点并执行更新来完成。
回到根节点，我们再次构建树，类似于 build()函数，传递要在每个级别执行的操作，并存储对其左右子节点的值应用该操作的结果，并将结果存储到该节点中。
执行更新后，考虑下面的分段树，
arr[2] = 7
现在更新后的分段树如下所示:

这里黑色的节点表示它们被更新的事实。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Recursive function to return gcd of a and b
int gcd(int a, int b)
{
    // Everything divides 0
    if (a == 0 || b == 0)
       return 0;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a-b, b);
    return gcd(a, b-a);
}

// A utility function to get the middle index from
// corner indexes.
int getMid(int s, int e) { return s + (e - s) / 2; }

void STconstructUtill(int arr[], int ss, int se, int* st,
                                          int si, int op)
{
    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se) {
        st[si] = arr[ss];
        return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum of
    // values in this node
    int mid = getMid(ss, se);

    // Build the left and the right subtrees by using
    // the fact that operation at level (i + 1) = !
    // (operation at level i)
    STconstructUtill(arr, ss, mid, st, si * 2 + 1, !op);
    STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, !op);

    // merge the left and right subtrees by checking
    // the operation to be carried. If operation = 1,
    // then do GCD else LCM
    if (op == 1) {
        // GCD operation
        st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
    }
    else {
        // LCM operation
        st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
                  (gcd(st[2 * si + 1], st[2 * si + 2]));
    }
}

void updateUtil(int* st, int ss, int se, int ind, int val,
                                            int si, int op)
{
    // Base Case: If the input index lies outside
    // this segment
    if (ind < ss || ind > se)
        return;

    // If the input index is in range of this node,
    // then update the value of the node and its
    // children

    // leaf node
    if (ss == se && ss == ind) {
        st[si] = val;
        return;
    }

    int mid = getMid(ss, se);

    // Update the left and the right subtrees by
    // using the fact that operation at level
    // (i + 1) = ! (operation at level i)
    updateUtil(st, ss, mid, ind, val, 2 * si + 1, !op);
    updateUtil(st, mid + 1, se, ind, val, 2 * si + 2, !op);

    // merge the left and right subtrees by checking
    // the operation to be carried. If operation = 1,
    // then do GCD else LCM
    if (op == 1) {

        // GCD operation
        st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
    }
    else {

        // LCM operation
        st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
                  (gcd(st[2 * si + 1], st[2 * si + 2]));
    }
}

void update(int arr[], int* st, int n, int ind, int val)
{
    // Check for erroneous input index
    if (ind < 0 || ind > n - 1) {
        printf("Invalid Input");
        return;
    }

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // operation = 1(GCD) if Height of tree is
    // even else it is 0(LCM) for the root node
    int opAtRoot = (x % 2 == 0 ? 0 : 1);

    arr[ind] = val;

    // Update the values of nodes in segment tree
    updateUtil(st, 0, n - 1, ind, val, 0, opAtRoot);
}

/* Function to construct segment tree from given array.
This function allocates memory for segment tree and
calls STconstructUtil() to fill the allocated memory */
int* STconstruct(int arr[], int n)
{
    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // allocate memory
    int* st = new int[max_size];

    // operation = 1(GCD) if Height of tree is
    // even else it is 0(LCM) for the root node
    int opAtRoot = (x % 2 == 0 ? 0 : 1);

    // Fill the allocated memory st
    STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot);

    // Return the constructed segment tree
    return st;
}

int main()
{
    int arr[] = { 5, 4, 8, 10, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree
    int* st = STconstruct(arr, n);

    // 0-based indexing in segment tree
    int rootIndex = 0;

    cout << "Old Value at Root Node = " <<
                             st[rootIndex] << endl;

    // perform update arr[2] = 7
    update(arr, st, n, 2, 7);

    cout << "New Value at Root Node = " <<
                             st[rootIndex] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
public class GFG
{
  // Recursive function to return gcd of a and b
  static int gcd(int a, int b)
  {

    // Everything divides 0
    if (a == 0 || b == 0)
      return 0;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return gcd(a - b, b);
    return gcd(a, b - a);
  }

  // A utility function to get the middle index from
  // corner indexes.
  static int getMid(int s, int e)
  {
    return s + (e - s) / 2;
  }

  static void STconstructUtill(int[] arr, int ss, int se, int[] st,
                               int si, int op)
  {
    // If there is one element in array, store it in
    // current node of segment tree and return
    if (ss == se)
    {
      st[si] = arr[ss];
      return;
    }

    // If there are more than one elements, then recur
    // for left and right subtrees and store the sum of
    // values in this node
    int mid = getMid(ss, se);

    // Build the left and the right subtrees by using
    // the fact that operation at level (i + 1) = !
    // (operation at level i)
    if(op != 0)
    {
      STconstructUtill(arr, ss, mid, st,
                       si * 2 + 1, 0);
    }
    else{
      STconstructUtill(arr, ss, mid, st,
                       si * 2 + 1, 1);
    }

    if(op != 0)
    {
      STconstructUtill(arr, mid + 1, se, st,
                       si * 2 + 2, 0);
    }
    else{
      STconstructUtill(arr, mid + 1, se, st,
                       si * 2 + 2, 1);
    }

    // merge the left and right subtrees by checking
    // the operation to be carried. If operation = 1,
    // then do GCD else LCM
    if (op == 1)
    {

      // GCD operation
      st[si] = gcd(st[2 * si + 1],
                   st[2 * si + 2]);
    }
    else {
      // LCM operation
      st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
        (gcd(st[2 * si + 1], st[2 * si + 2]));
    }
  }

  static void updateUtil(int[] st, int ss, int se,
                         int ind, int val,
                         int si, int op)
  {

    // Base Case: If the input index lies outside
    // this segment
    if (ind < ss || ind > se)
      return;

    // If the input index is in range of this node,
    // then update the value of the node and its
    // children

    // leaf node
    if (ss == se && ss == ind)
    {
      st[si] = val;
      return;
    }
    int mid = getMid(ss, se);

    // Update the left and the right subtrees by
    // using the fact that operation at level
    // (i + 1) = ! (operation at level i)
    if(op != 0)
    {
      updateUtil(st, ss, mid, ind,
                 val, 2 * si + 1, 0);
    }
    else{
      updateUtil(st, ss, mid, ind,
                 val, 2 * si + 1, 1);
    }

    if(op != 0)
    {
      updateUtil(st, mid + 1, se, ind,
                 val, 2 * si + 2, 0);
    }
    else{
      updateUtil(st, mid + 1, se, ind,
                 val, 2 * si + 2, 1);
    }

    // merge the left and right subtrees by checking
    // the operation to be carried. If operation = 1,
    // then do GCD else LCM
    if (op == 1) {

      // GCD operation
      st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
    }
    else {

      // LCM operation
      st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
        (gcd(st[2 * si + 1], st[2 * si + 2]));
    }
  }

  static void update(int[] arr, int[] st,
                     int n, int ind, int val)
  {
    // Check for erroneous input index
    if (ind < 0 || ind > n - 1)
    {
      System.out.print("Invalid Input");
      return;
    }

    // Height of segment tree
    int x = (int)(Math.ceil(Math.log(n) / Math.log(2)));

    // operation = 1(GCD) if Height of tree is
    // even else it is 0(LCM) for the root node
    int opAtRoot = (x % 2 == 0 ? 0 : 1);

    arr[ind] = val;

    // Update the values of nodes in segment tree
    updateUtil(st, 0, n - 1, ind, val, 0, opAtRoot);
  }

  /* Function to construct segment tree from given array.
    This function allocates memory for segment tree and
    calls STconstructUtil() to fill the allocated memory */
  static int[] STconstruct(int[] arr, int n)
  {
    // Allocate memory for segment tree

    // Height of segment tree
    int x = (int)(Math.ceil(Math.log(n) / Math.log(2)));

    // maximum size of segment tree
    int max_size = 2 * (int)Math.pow(2, x) - 1;

    // allocate memory
    int[] st = new int[max_size];

    // operation = 1(GCD) if Height of tree is
    // even else it is 0(LCM) for the root node
    int opAtRoot = (x % 2 == 0 ? 0 : 1);

    // Fill the allocated memory st
    STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot);

    // Return the constructed segment tree
    return st;
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] arr = { 5, 4, 8, 10, 6 };
    int n = arr.length;

    // Build segment tree
    int[] st = STconstruct(arr, n);

    // 0-based indexing in segment tree
    int rootIndex = 0;

    System.out.println("Old Value at Root Node = " + st[rootIndex]);

    // perform update arr[2] = 7
    update(arr, st, n, 2, 7);
    System.out.println("New Value at Root Node = " + st[rootIndex]);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
import math

# Recursive function to return gcd of a and b
def gcd(a , b):
    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return gcd(a - b, b)
    return gcd(a, b - a)

# A utility function to get the middle index from
# corner indexes.
def getMid(s , e):
    return s + int((e - s) / 2)

def STconstructUtill(arr , ss , se,  st , si , op):
    # If there is one element in array, store it in
    # current node of segment tree and return
    if (ss == se):
        st[si] = arr[ss]
        return

    # If there are more than one elements, then recur
    # for left and right subtrees and store the sum of
    # values in this node
    mid = getMid(ss, se)

    # Build the left and the right subtrees by using
    # the fact that operation at level (i + 1) = !
    # (operation at level i)
    if (op != 0):
        STconstructUtill(arr, ss, mid, st, si * 2 + 1, 0)
    else:
        STconstructUtill(arr, ss, mid, st, si * 2 + 1, 1)

    if (op != 0):
        STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, 0)
    else:
        STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, 1)

    # merge the left and right subtrees by checking
    # the operation to be carried. If operation = 1,
    # then do GCD else LCM
    if (op == 1):

        # GCD operation
        st[si] = gcd(st[2 * si + 1], st[2 * si + 2])
    else:
        # LCM operation
        st[si] = (st[2 * si + 1] * st[2 * si + 2]) / (gcd(st[2 * si + 1], st[2 * si + 2]))

def updateUtil(st , ss , se , ind , val , si , op):

    # Base Case: If the input index lies outside
    # this segment
    if (ind < ss or ind > se):
        return

    # If the input index is in range of this node,
    # then update the value of the node and its
    # children

    # leaf node
    if (ss == se and ss == ind):
        st[si] = val
        return
    mid = getMid(ss, se)

    # Update the left and the right subtrees by
    # using the fact that operation at level
    # (i + 1) = ! (operation at level i)
    if (op != 0):
        updateUtil(st, ss, mid, ind, val, 2 * si + 1, 0)
    else:
        updateUtil(st, ss, mid, ind, val, 2 * si + 1, 1)

    if (op != 0):
        updateUtil(st, mid + 1, se, ind, val, 2 * si + 2, 0)
    else:
        updateUtil(st, mid + 1, se, ind, val, 2 * si + 2, 1)

    # merge the left and right subtrees by checking
    # the operation to be carried. If operation = 1,
    # then do GCD else LCM
    if (op == 1):
        # GCD operation
        st[si] = gcd(st[2 * si + 1], st[2 * si + 2])
    else:
        # LCM operation
        st[si] = (st[2 * si + 1] * st[2 * si + 2]) / (gcd(st[2 * si + 1], st[2 * si + 2]))

def update(arr,  st , n , ind , val):
    # Check for erroneous input index
    if (ind < 0 and ind > n - 1):
        print("Invalid Input")
        return

    # Height of segment tree
    x = int((math.ceil(math.log(n) / math.log(2))))

    # operation = 1(GCD) if Height of tree is
    # even else it is 0(LCM) for the root node
    if x % 2 == 0:
        opAtRoot = 0
    else:
        opAtRoot = 1

    arr[ind] = val

    # Update the values of nodes in segment tree
    updateUtil(st, 0, n - 1, ind, val, 0, opAtRoot)

"""
 Function to construct segment tree from given array.
 This function allocates memory for
 segment tree and calls STconstructUtil() to
 fill the allocated memory
"""
def STconstruct(arr , n):

    # Allocate memory for segment tree

    # Height of segment tree
    x = int((math.ceil(math.log(n) / math.log(2))))

    # maximum size of segment tree
    max_size = 2 * int(math.pow(2, x) - 1)

    # allocate memory
    st = [0]*(max_size)

    # operation = 1(GCD) if Height of tree is
    # even else it is 0(LCM) for the root node
    if x % 2 == 0:
        opAtRoot = 0
    else:
        opAtRoot = 1

    # Fill the allocated memory st
    STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot)

    # Return the constructed segment tree
    return st

arr = [ 5, 4, 8, 10, 6 ]
n = len(arr)

# Build segment tree
st = STconstruct(arr, n)

# 0-based indexing in segment tree
rootIndex = 0

print("Old Value at Root Node =", int(st[rootIndex]))

# perform update arr[2] = 7
update(arr, st, n, 2, 7)
print("New Value at Root Node =", int(st[rootIndex]))

# This code is contributed by decode2207.
```

## C#

```
using System;
class GFG
{

    // Recursive function to return gcd of a and b
    static int gcd(int a, int b)
    {

        // Everything divides 0
        if (a == 0 || b == 0)
           return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a - b, b);
        return gcd(a, b - a);
    }

    // A utility function to get the middle index from
    // corner indexes.
    static int getMid(int s, int e)
    {
        return s + (e - s) / 2;
    }

    static void STconstructUtill(int[] arr, int ss, int se, int[] st,
                                              int si, int op)
    {
        // If there is one element in array, store it in
        // current node of segment tree and return
        if (ss == se)
        {
            st[si] = arr[ss];
            return;
        }

        // If there are more than one elements, then recur
        // for left and right subtrees and store the sum of
        // values in this node
        int mid = getMid(ss, se);

        // Build the left and the right subtrees by using
        // the fact that operation at level (i + 1) = !
        // (operation at level i)
        if(op != 0)
        {
            STconstructUtill(arr, ss, mid, st,
                             si * 2 + 1, 0);
        }
        else{
            STconstructUtill(arr, ss, mid, st,
                             si * 2 + 1, 1);
        }

        if(op != 0)
        {
            STconstructUtill(arr, mid + 1, se, st,
                             si * 2 + 2, 0);
        }
        else{
            STconstructUtill(arr, mid + 1, se, st,
                             si * 2 + 2, 1);
        }

        // merge the left and right subtrees by checking
        // the operation to be carried. If operation = 1,
        // then do GCD else LCM
        if (op == 1)
        {

            // GCD operation
            st[si] = gcd(st[2 * si + 1],
                         st[2 * si + 2]);
        }
        else {
            // LCM operation
            st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
                      (gcd(st[2 * si + 1], st[2 * si + 2]));
        }
    }

    static void updateUtil(int[] st, int ss, int se,
                           int ind, int val,
                           int si, int op)
    {

        // Base Case: If the input index lies outside
        // this segment
        if (ind < ss || ind > se)
            return;

        // If the input index is in range of this node,
        // then update the value of the node and its
        // children

        // leaf node
        if (ss == se && ss == ind)
        {
            st[si] = val;
            return;
        }
        int mid = getMid(ss, se);

        // Update the left and the right subtrees by
        // using the fact that operation at level
        // (i + 1) = ! (operation at level i)
        if(op != 0)
        {
            updateUtil(st, ss, mid, ind,
                       val, 2 * si + 1, 0);
        }
        else{
            updateUtil(st, ss, mid, ind,
                       val, 2 * si + 1, 1);
        }

        if(op != 0)
        {
            updateUtil(st, mid + 1, se, ind,
                       val, 2 * si + 2, 0);
        }
        else{
            updateUtil(st, mid + 1, se, ind,
                       val, 2 * si + 2, 1);
        }

        // merge the left and right subtrees by checking
        // the operation to be carried. If operation = 1,
        // then do GCD else LCM
        if (op == 1) {

            // GCD operation
            st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
        }
        else {

            // LCM operation
            st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
                      (gcd(st[2 * si + 1], st[2 * si + 2]));
        }
    }

    static void update(int[] arr, int[] st,
                       int n, int ind, int val)
    {
        // Check for erroneous input index
        if (ind < 0 || ind > n - 1)
        {
            Console.Write("Invalid Input");
            return;
        }

        // Height of segment tree
        int x = (int)(Math.Ceiling(Math.Log(n, 2)));

        // operation = 1(GCD) if Height of tree is
        // even else it is 0(LCM) for the root node
        int opAtRoot = (x % 2 == 0 ? 0 : 1);

        arr[ind] = val;

        // Update the values of nodes in segment tree
        updateUtil(st, 0, n - 1, ind, val, 0, opAtRoot);
    }

    /* Function to construct segment tree from given array.
    This function allocates memory for segment tree and
    calls STconstructUtil() to fill the allocated memory */
    static int[] STconstruct(int[] arr, int n)
    {
        // Allocate memory for segment tree

        // Height of segment tree
        int x = (int)(Math.Ceiling(Math.Log(n, 2)));

        // maximum size of segment tree
        int max_size = 2 * (int)Math.Pow(2, x) - 1;

        // allocate memory
        int[] st = new int[max_size];

        // operation = 1(GCD) if Height of tree is
        // even else it is 0(LCM) for the root node
        int opAtRoot = (x % 2 == 0 ? 0 : 1);

        // Fill the allocated memory st
        STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot);

        // Return the constructed segment tree
        return st;
    }

  // Driver code
  static void Main()
  {
    int[] arr = { 5, 4, 8, 10, 6 };
    int n = arr.Length;

    // Build segment tree
    int[] st = STconstruct(arr, n);

    // 0-based indexing in segment tree
    int rootIndex = 0;

    Console.WriteLine("Old Value at Root Node = " + st[rootIndex]);

    // perform update arr[2] = 7
    update(arr, st, n, 2, 7);
    Console.WriteLine("New Value at Root Node = " + st[rootIndex]);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

    // Recursive function to return gcd of a and b
    function gcd(a , b) {

        // Everything divides 0
        if (a == 0 || b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a - b, b);
        return gcd(a, b - a);
    }

    // A utility function to get the middle index from
    // corner indexes.
    function getMid(s , e) {
        return s + parseInt((e - s) / 2);
    }

    function STconstructUtill(arr , ss , se,  st , si , op) {
        // If there is one element in array, store it in
        // current node of segment tree and return
        if (ss == se) {
            st[si] = arr[ss];
            return;
        }

        // If there are more than one elements, then recur
        // for left and right subtrees and store the sum of
        // values in this node
        var mid = getMid(ss, se);

        // Build the left and the right subtrees by using
        // the fact that operation at level (i + 1) = !
        // (operation at level i)
        if (op != 0) {
            STconstructUtill(arr, ss, mid, st, si * 2 + 1, 0);
        } else {
            STconstructUtill(arr, ss, mid, st, si * 2 + 1, 1);
        }

        if (op != 0) {
            STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, 0);
        } else {
            STconstructUtill(arr, mid + 1, se, st, si * 2 + 2, 1);
        }

        // merge the left and right subtrees by checking
        // the operation to be carried. If operation = 1,
        // then do GCD else LCM
        if (op == 1) {

            // GCD operation
            st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
        } else {
            // LCM operation
            st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
            (gcd(st[2 * si + 1], st[2 * si + 2]));
        }
    }

    function updateUtil(st , ss , se , ind , val , si , op) {

        // Base Case: If the input index lies outside
        // this segment
        if (ind < ss || ind > se)
            return;

        // If the input index is in range of this node,
        // then update the value of the node and its
        // children

        // leaf node
        if (ss == se && ss == ind) {
            st[si] = val;
            return;
        }
        var mid = getMid(ss, se);

        // Update the left and the right subtrees by
        // using the fact that operation at level
        // (i + 1) = ! (operation at level i)
        if (op != 0) {
            updateUtil(st, ss, mid, ind, val, 2 * si + 1, 0);
        } else {
            updateUtil(st, ss, mid, ind, val, 2 * si + 1, 1);
        }

        if (op != 0) {
            updateUtil(st, mid + 1, se, ind, val, 2 * si + 2, 0);
        } else {
            updateUtil(st, mid + 1, se, ind, val, 2 * si + 2, 1);
        }

        // merge the left and right subtrees by checking
        // the operation to be carried. If operation = 1,
        // then do GCD else LCM
        if (op == 1) {

            // GCD operation
            st[si] = gcd(st[2 * si + 1], st[2 * si + 2]);
        } else {

            // LCM operation
            st[si] = (st[2 * si + 1] * st[2 * si + 2]) /
            (gcd(st[2 * si + 1], st[2 * si + 2]));
        }
    }

    function update(arr,  st , n , ind , val) {
        // Check for erroneous input index
        if (ind < 0 || ind > n - 1) {
            document.write("Invalid Input");
            return;
        }

        // Height of segment tree
        var x = parseInt( (Math.ceil(Math.log(n) / Math.log(2))));

        // operation = 1(GCD) if Height of tree is
        // even else it is 0(LCM) for the root node
        var opAtRoot = (x % 2 == 0 ? 0 : 1);

        arr[ind] = val;

        // Update the values of nodes in segment tree
        updateUtil(st, 0, n - 1, ind, val, 0, opAtRoot);
    }

    /*
     Function to construct segment tree from given array.
     This function allocates memory for
     segment tree and calls STconstructUtil() to
     fill the allocated memory
     */
    function STconstruct(arr , n) {
        // Allocate memory for segment tree

        // Height of segment tree
        var x = parseInt( (Math.ceil(Math.log(n) / Math.log(2))));

        // maximum size of segment tree
        var max_size = 2 * parseInt( Math.pow(2, x) - 1);

        // allocate memory
        var st = Array(max_size).fill(0);

        // operation = 1(GCD) if Height of tree is
        // even else it is 0(LCM) for the root node
        var opAtRoot = (x % 2 == 0 ? 0 : 1);

        // Fill the allocated memory st
        STconstructUtill(arr, 0, n - 1, st, 0, opAtRoot);

        // Return the constructed segment tree
        return st;
    }

    // Driver code

        var arr = [ 5, 4, 8, 10, 6 ];
        var n = arr.length;

        // Build segment tree
        var st = STconstruct(arr, n);

        // 0-based indexing in segment tree
        var rootIndex = 0;

        document.write("Old Value at Root Node = " + st[rootIndex]);

        // perform update arr[2] = 7
        update(arr, st, n, 2, 7);
        document.write("<br/>New Value at Root Node = " + st[rootIndex]);

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
Old Value at Root Node = 2
New Value at Root Node = 1
```

更新的时间复杂度也是 O(Logn)。要更新叶值，每个级别处理一个节点，级别数为 0(Logn)。