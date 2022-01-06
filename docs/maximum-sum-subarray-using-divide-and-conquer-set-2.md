# 使用分治法的最大和子阵列|集合 2

> 原文:[https://www . geesforgeks . org/max-sum-subarray-使用分治集-2/](https://www.geeksforgeeks.org/maximum-sum-subarray-using-divide-and-conquer-set-2/)

给定一个整数数组 **arr[]** ，任务是在所有可能的子数组中找到最大和子数组。
**例:**

> **输入:** arr[] = {-2，1，-3，4，-1，2，1，-5，4}
> **输出:** 6
> {4，-1，2，1}为所需子数组。
> **输入:** arr[] = {2，2，-2}
> **输出:** 4

**方法:**到目前为止我们只知道[卡丹的算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)，它用动态规划在 O(n)中解决了这个问题。
我们还讨论了 O(N*logN)时间复杂度中最大和子阵的[分治法。
下面的方法使用分治法来解决这个问题，分治法的时间复杂度与 **O(n)相同。**
分而治之的算法一般涉及到把问题分成子问题，分别攻克。对于这个问题，我们维护一个结构(在 cpp 中)或类(在 java 或 python 中)，它存储以下值:](https://www.geeksforgeeks.org/maximum-subarray-sum-using-divide-and-conquer-algorithm/) 

1.  子阵列的总和。
2.  子数组的最大前缀和。
3.  子数组的最大后缀和。
4.  子阵列的总最大和。(这包含子阵列的最大和)。

在递归过程中(除部分)，数组从中间被分成两部分。左节点结构包含数组左部分的所有上述值，右节点结构包含所有上述值。有了这两个节点，现在我们可以通过计算结果节点的所有值来合并这两个节点。
结果节点的最大前缀和将是左节点的最大前缀和或左节点的最大前缀和+右节点的最大前缀和或两个节点的总和中的最大值(这对于具有所有正值的数组是可能的)。
类似地，结果节点的最大后缀和将是右节点的最大后缀和或右节点的最大后缀和+左节点的最大后缀和或两个节点的总和中的最大值(这对于具有所有正值的数组也是可能的)。
结果节点的总和是左节点和右节点总和的总和。
现在，结果节点的最大子阵和将是结果节点的前缀和、结果节点的后缀和、结果节点的总和、左节点的最大和、右节点的最大和、左节点的最大后缀和以及右节点的最大前缀和中的最大值。
这里的征服部分可以在 O(1)时间内完成，结合来自左右节点结构的结果。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

struct Node {

    // To store the maximum sum
    // for a sub-array
    long long _max;

    // To store the maximum prefix
    // sum for a sub-array
    long long _pre;

    // To store the maximum suffix
    // sum for a sub-array
    long long _suf;

    // To store the total sum
    // for a sub-array
    long long _sum;

};

// Function to create a node
Node getNode(long long x){
    Node a;
    a._max = x;
    a._pre = x;
    a._suf = x;
    a._sum = x;
    return a;
}

// Function to merge the 2 nodes left and right
Node merg(const Node &l, const Node &r){

    // Creating node ans
    Node ans ;

    // Initializing all the variables:
    ans._max = ans._pre = ans._suf = ans._sum = 0;

    // The max prefix sum of ans Node is maximum of
    // a) max prefix sum of left Node
    // b) sum of left Node + max prefix sum of right Node
    // c) sum of left Node + sum of right Node
    ans._pre = max({l._pre, l._sum+r._pre, l._sum+r._sum});

    // The max suffix sum of ans Node is maximum of
    // a) max suffix sum of right Node
    // b) sum of right Node + max suffix sum of left Node
    // c) sum of left Node + sum of right Node
    ans._suf = max({r._suf, r._sum+l._suf, l._sum+r._sum});

    // Total sum of ans Node = total sum of left Node + total sum of right Node
    ans._sum = l._sum + r._sum;

    // The max sum of ans Node stores the answer which is the maximum value among:
    // prefix sum of ans Node
    // suffix sum of ans Node
    // maximum value of left Node
    // maximum value of right Node
    // prefix value of right Node + suffix value of left Node
    ans._max = max({ans._pre, ans._suf, ans._sum,l._max, r._max, l._suf+r._pre});

    // Return the ans Node
    return ans;
}

// Function for calculating the
// max_sum_subArray using divide and conquer
Node getMaxSumSubArray(int l, int r, vector<long long> &ar){

    if (l == r) return getNode(ar[l]);

    int mid = (l + r) >> 1;

    // Call method to return left Node:
    Node left = getMaxSumSubArray(l, mid, ar);

    // Call method to return right Node:
    Node right = getMaxSumSubArray(mid+1, r, ar);

    // Return the merged Node:
    return merg(left, right);

}

// Driver code
int main(){

    vector<long long> ar = {-2, -5, 6, -2, -3, 1, 5, -6};
    int n = ar.size();
    Node ans = getMaxSumSubArray(0, n-1, ar);
    cout << "Answer is " << ans._max << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{
static class Node
{

    // To store the maximum sum
    // for a sub-array
    int _max;

    // To store the maximum prefix
    // sum for a sub-array
    int _pre;

    // To store the maximum suffix
    // sum for a sub-array
    int _suf;

    // To store the total sum
    // for a sub-array
    int _sum;

};

// Function to create a node
static Node getNode(int x)
{
    Node a = new Node();
    a._max = x;
    a._pre = x;
    a._suf = x;
    a._sum = x;
    return a;
}

// Function to merge the 2 nodes left and right
static Node merg(Node l, Node r)
{

    // Creating node ans
    Node ans = new Node();

    // Initializing all the variables:
    ans._max = ans._pre = ans._suf = ans._sum = 0;

    // The max prefix sum of ans Node is maximum of
    // a) max prefix sum of left Node
    // b) sum of left Node + max prefix sum of right Node
    // c) sum of left Node + sum of right Node
    ans._pre = Arrays.stream(new int[]{l._pre, l._sum+r._pre,
                                       l._sum+r._sum}).max().getAsInt();

    // The max suffix sum of ans Node is maximum of
    // a) max suffix sum of right Node
    // b) sum of right Node + max suffix sum of left Node
    // c) sum of left Node + sum of right Node
    ans._suf = Arrays.stream(new int[]{r._suf, r._sum+l._suf,
                                       l._sum+r._sum}).max().getAsInt();

    // Total sum of ans Node = total sum of
  // left Node + total sum of right Node
    ans._sum = l._sum + r._sum;

    // The max sum of ans Node stores
    // the answer which is the maximum value among:
    // prefix sum of ans Node
    // suffix sum of ans Node
    // maximum value of left Node
    // maximum value of right Node
    // prefix value of right Node + suffix value of left Node
    ans._max = Arrays.stream(new int[]{ans._pre,
                                       ans._suf,
                                       ans._sum,
                                       l._max, r._max,
                                       l._suf+r._pre}).max().getAsInt();

    // Return the ans Node
    return ans;
}

// Function for calculating the
// max_sum_subArray using divide and conquer
static Node getMaxSumSubArray(int l, int r, int []ar)
{

    if (l == r) return getNode(ar[l]);
    int mid = (l + r) >> 1;

    // Call method to return left Node:
    Node left = getMaxSumSubArray(l, mid, ar);

    // Call method to return right Node:
    Node right = getMaxSumSubArray(mid + 1, r, ar);

    // Return the merged Node:
    return merg(left, right);

}

// Driver code
public static void main(String[] args)
{
    int []ar = {-2, -5, 6, -2, -3, 1, 5, -6};
    int n = ar.length;
    Node ans = getMaxSumSubArray(0, n - 1, ar);
    System.out.print("Answer is " +  ans._max + "\n");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation of the approach

class Node:

    def __init__(self, x):

        # To store the maximum sum for a sub-array
        self._max = x

        # To store the maximum prefix sum for a sub-array
        self._pre = x

        # To store the maximum suffix sum for a sub-array
        self._suf = x

        # To store the total sum for a sub-array
        self._sum = x

# Function to merge the 2 nodes left and right
def merg(l, r):

    # Creating node ans
    ans = Node(0)

    # The max prefix sum of ans Node is maximum of
    # a) max prefix sum of left Node
    # b) sum of left Node + max prefix sum of right Node
    # c) sum of left Node + sum of right Node
    ans._pre = max(l._pre, l._sum+r._pre, l._sum+r._sum)

    # The max suffix sum of ans Node is maximum of
    # a) max suffix sum of right Node
    # b) sum of right Node + max suffix sum of left Node
    # c) sum of left Node + sum of right Node
    ans._suf = max(r._suf, r._sum+l._suf, l._sum+r._sum)

    # Total sum of ans Node = total sum of
    # left Node + total sum of right Node
    ans._sum = l._sum + r._sum

    # The max sum of ans Node stores the answer
    # which is the maximum value among:
    # prefix sum of ans Node
    # suffix sum of ans Node
    # maximum value of left Node
    # maximum value of right Node
    # prefix value of left Node + suffix value of right Node
    ans._max = max(ans._pre, ans._suf, ans._sum,
                    l._max, r._max, l._suf+r._pre)

    # Return the ans Node
    return ans

# Function for calculating the
# max_sum_subArray using divide and conquer
def getMaxSumSubArray(l, r, ar):

    if l == r: return Node(ar[l])

    mid = (l + r) // 2

    # Call method to return left Node:
    left = getMaxSumSubArray(l, mid, ar)

    # Call method to return right Node:
    right = getMaxSumSubArray(mid+1, r, ar)

    # Return the merged Node:
    return merg(left, right)

# Driver code
if __name__ == "__main__":

    ar = [-2, -5, 6, -2, -3, 1, 5, -6]
    n = len(ar)
    ans = getMaxSumSubArray(0, n-1, ar)
    print("Answer is", ans._max)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;
public class GFG
{

class Node
{

    // To store the maximum sum
    // for a sub-array
    public int _max;

    // To store the maximum prefix
    // sum for a sub-array
    public int _pre;

    // To store the maximum suffix
    // sum for a sub-array
    public int _suf;

    // To store the total sum
    // for a sub-array
    public int _sum;
};

// Function to create a node
static Node getNode(int x)
{
    Node a = new Node();
    a._max = x;
    a._pre = x;
    a._suf = x;
    a._sum = x;
    return a;
}

// Function to merge the 2 nodes left and right
static Node merg(Node l, Node r)
{

    // Creating node ans
    Node ans = new Node();

    // Initializing all the variables:
    ans._max = ans._pre = ans._suf = ans._sum = 0;

    // The max prefix sum of ans Node is maximum of
    // a) max prefix sum of left Node
    // b) sum of left Node + max prefix sum of right Node
    // c) sum of left Node + sum of right Node
    ans._pre = (new int[]{l._pre, l._sum+r._pre,
                                       l._sum+r._sum}).Max();

    // The max suffix sum of ans Node is maximum of
    // a) max suffix sum of right Node
    // b) sum of right Node + max suffix sum of left Node
    // c) sum of left Node + sum of right Node
    ans._suf = (new int[]{r._suf, r._sum+l._suf,
                                       l._sum+r._sum}).Max();

    // Total sum of ans Node = total sum of
  // left Node + total sum of right Node
    ans._sum = l._sum + r._sum;

    // The max sum of ans Node stores
    // the answer which is the maximum value among:
    // prefix sum of ans Node
    // suffix sum of ans Node
    // maximum value of left Node
    // maximum value of right Node
    // prefix value of right Node + suffix value of left Node
    ans._max = (new int[]{ans._pre,
                                       ans._suf,
                                       ans._sum,
                                       l._max, r._max,
                                       l._suf+r._pre}).Max();

    // Return the ans Node
    return ans;
}

// Function for calculating the
// max_sum_subArray using divide and conquer
static Node getMaxSumSubArray(int l, int r, int []ar)
{
    if (l == r) return getNode(ar[l]);
    int mid = (l + r) >> 1;

    // Call method to return left Node:
    Node left = getMaxSumSubArray(l, mid, ar);

    // Call method to return right Node:
    Node right = getMaxSumSubArray(mid + 1, r, ar);

    // Return the merged Node:
    return merg(left, right);
}

// Driver code
public static void Main(String[] args)
{
    int []ar = {-2, -5, 6, -2, -3, 1, 5, -6};
    int n = ar.Length;
    Node ans = getMaxSumSubArray(0, n - 1, ar);
    Console.Write("Answer is " +  ans._max + "\n");
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
class Node {

    constructor()
    {
        // To store the maximum sum
        // for a sub-array
        var _max;

        // To store the maximum prefix
        // sum for a sub-array
        var _pre;

        // To store the maximum suffix
        // sum for a sub-array
        var _suf;

        // To store the total sum
        // for a sub-array
        var _sum;
    }

};

// Function to create a node
function getNode(x){
    var a = new Node();
    a._max = x;
    a._pre = x;
    a._suf = x;
    a._sum = x;
    return a;
}

// Function to merge the 2 nodes left and right
function merg(l, r){

    // Creating node ans
    var ans = new Node();

    // Initializing all the variables:
    ans._max = ans._pre = ans._suf = ans._sum = 0;

    // The max prefix sum of ans Node is maximum of
    // a) max prefix sum of left Node
    // b) sum of left Node + max prefix sum of right Node
    // c) sum of left Node + sum of right Node
    ans._pre = Math.max(l._pre, l._sum+r._pre, l._sum+r._sum);

    // The max suffix sum of ans Node is maximum of
    // a) max suffix sum of right Node
    // b) sum of right Node + max suffix sum of left Node
    // c) sum of left Node + sum of right Node
    ans._suf = Math.max(r._suf, r._sum+l._suf, l._sum+r._sum);

    // Total sum of ans Node = total sum of left Node + total sum of right Node
    ans._sum = l._sum + r._sum;

    // The max sum of ans Node stores the answer which is the maximum value among:
    // prefix sum of ans Node
    // suffix sum of ans Node
    // maximum value of left Node
    // maximum value of right Node
    // prefix value of right Node + suffix value of left Node
    ans._max = Math.max(ans._pre, ans._suf, ans._sum,l._max, r._max, l._suf+r._pre);

    // Return the ans Node
    return ans;
}

// Function for calculating the
// max_sum_subArray using divide and conquer
function getMaxSumSubArray(l, r, ar){

    if (l == r) return getNode(ar[l]);

    var mid = (l + r) >> 1;

    // Call method to return left Node:
    var left = getMaxSumSubArray(l, mid, ar);

    // Call method to return right Node:
    var right = getMaxSumSubArray(mid+1, r, ar);

    // Return the merged Node:
    return merg(left, right);

}

// Driver code
var ar = [-2, -5, 6, -2, -3, 1, 5, -6];
var n = ar.length;
var ans = getMaxSumSubArray(0, n-1, ar);
document.write("Answer is " + ans._max + "<br>");

// This code is contributed by rutvik_56.
</script>
```

**输出:**

```
Answer is 7
```

**时间复杂度:**getMaxSumSubArray()递归函数生成以下递归关系。
**T(n) = 2 * T(n / 2) + O(1)** 注意征服部分只需要 O(1)时间。因此，在用 Master 定理求解这个递归时，我们得到了 O(n)的时间复杂度。