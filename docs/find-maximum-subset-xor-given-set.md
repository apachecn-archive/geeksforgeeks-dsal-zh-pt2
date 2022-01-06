# 求给定集合的最大子集异或

> 原文:[https://www . geesforgeks . org/find-max-subset-xor-给定-set/](https://www.geeksforgeeks.org/find-maximum-subset-xor-given-set/)

给定一组正整数。找出给定集合中的最大异或子集值。预期时间复杂度 O(n)。
**例:**

```
Input: set[] = {2, 4, 5}
Output: 7
The subset {2, 5} has maximum XOR value

Input: set[] = {9, 8, 5}
Output: 13
The subset {8, 5} has maximum XOR value

Input: set[] = {8, 1, 2, 12, 7, 6}
Output: 15
The subset {1, 2, 12} has maximum XOR value

Input: set[] = {4, 6}
Output: 6
The subset {6} has maximum XOR value
```

注意这个问题不同于[最大子阵异或](https://www.geeksforgeeks.org/find-the-maximum-subarray-xor-in-a-given-array/)。这里我们需要找到子集而不是子阵列。

一个**简单的解决方案**是生成给定集合的所有可能子集，求每个子集的异或，返回异或最大的子集。
下面是一个在 O(n)时间内有效的**算法**。
想法基于以下事实:

1.  代表所有元素的位数是固定的，在大多数编译器中整数是 32 位。
2.  如果最大元素在位置 I 具有最高有效位 MSB，则结果至少为 2 <sup>i</sup>

```
1\. Initialize index of chosen elements as 0\. Let this index be 
   'index'
2\. Traverse through all bits starting from most significant bit. 
   Let i be the current bit.
......(a) Find the maximum element with i'th bit set.  If there
          is no element with i'th bit set, continue to smaller 
          bit.  
......(b) Let the element with i'th bit set be maxEle and index
          of this element be maxInd. Place maxEle at 'index' and
          (by swapping set[index] and set[maxInd]) 
......(c) Do XOR of maxEle with all numbers having i'th  bit as set.
......(d) Increment index 
3\. Return XOR of all elements in set[]. Note that set[] is modified
   in step 2.c.
```

下面是这个算法的实现。

## C++

```
// C++ program to find
// maximum XOR subset
#include<bits/stdc++.h>
using namespace std;

// Number of bits to
// represent int
#define INT_BITS 32

// Function to return
// maximum XOR subset
// in set[]
int maxSubarrayXOR(int set[], int n)
{
    // Initialize index of
    // chosen elements
    int index = 0;

    // Traverse through all
    // bits of integer
    // starting from the most
    // significant bit (MSB)
    for (int i = INT_BITS-1; i >= 0; i--)
    {
        // Initialize index of
        // maximum element and
        // the maximum element
        int maxInd = index;
        int maxEle = INT_MIN;
        for (int j = index; j < n; j++)
        {
            // If i'th bit of set[j]
            // is set and set[j] is
            // greater than max so far.
            if ( (set[j] & (1 << i)) != 0
                     && set[j] > maxEle )
                maxEle = set[j], maxInd = j;
        }

        // If there was no
        // element with i'th
        // bit set, move to
        // smaller i
        if (maxEle == INT_MIN)
        continue;

        // Put maximum element
        // with i'th bit set
        // at index 'index'
        swap(set[index], set[maxInd]);

        // Update maxInd and
        // increment index
        maxInd = index;

        // Do XOR of set[maxIndex]
        // with all numbers having
        // i'th bit as set.
        for (int j=0; j<n; j++)
        {
            // XOR set[maxInd] those
            // numbers which have the
            // i'th bit set
            if (j != maxInd &&
               (set[j] & (1 << i)) != 0)
                set[j] = set[j] ^ set[maxInd];
        }

        // Increment index of
        // chosen elements
        index++;
    }

    // Final result is
    // XOR of all elements
    int res = 0;
    for (int i = 0; i < n; i++)
        res ^= set[i];
    return res;
}

// Driver program
int main()
{
    int set[] = {9, 8, 5};
    int n = sizeof(set) / sizeof(set[0]);

    cout << "Max subset XOR is ";
    cout << maxSubarrayXOR(set, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// maximum XOR subset
import java.util.*;

class GFG {

// Number of bits to
// represent int
static final int INT_BITS = 32;

// Function to return
// maximum XOR subset
// in set[]
static int maxSubarrayXOR(int set[], int n)
{
    // Initialize index of
    // chosen elements
    int index = 0;

    // Traverse through all
    // bits of integer
    // starting from the most
    // significant bit (MSB)
    for (int i = INT_BITS - 1; i >= 0; i--)
    {
    // Initialize index of
    // maximum element and
    // the maximum element
    int maxInd = index;
    int maxEle = Integer.MIN_VALUE;
    for (int j = index; j < n; j++) {

        // If i'th bit of set[j]
        // is set and set[j] is
        // greater than max so far.
        if ((set[j] & (1 << i)) != 0 && set[j] > maxEle)
        {
        maxEle = set[j];
        maxInd = j;
        }
    }

    // If there was no
    // element with i'th
    // bit set, move to
    // smaller i
    if (maxEle == -2147483648)
        continue;

    // Put maximum element
    // with i'th bit set
    // at index 'index'
    int temp = set[index];
    set[index] = set[maxInd];
    set[maxInd] = temp;

    // Update maxInd and
    // increment index
    maxInd = index;

    // Do XOR of set[maxIndex]
    // with all numbers having
    // i'th bit as set.
    for (int j = 0; j < n; j++) {

        // XOR set[maxInd] those
        // numbers which have the
        // i'th bit set
        if (j != maxInd && (set[j] & (1 << i)) != 0)
        set[j] = set[j] ^ set[maxInd];
    }

    // Increment index of
    // chosen elements
    index++;
    }

    // Final result is
    // XOR of all elements
    int res = 0;
    for (int i = 0; i < n; i++)
    res ^= set[i];
    return res;
}

// Driver code
public static void main(String arg[]) {
    int set[] = {9, 8, 5};
    int n = set.length;

    System.out.print("Max subset XOR is ");
    System.out.print(maxSubarrayXOR(set, n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# maximum XOR subset

# Number of bits to
# represent int
INT_BITS=32

# Function to return
# maximum XOR subset
# in set[]
def maxSubarrayXOR(set,n):

    # Initialize index of
    # chosen elements
    index = 0

    # Traverse through all
    # bits of integer
    # starting from the most
    # significant bit (MSB)
    for i in range(INT_BITS-1,-1,-1):

        # Initialize index of
        # maximum element and
        # the maximum element
        maxInd = index
        maxEle = -2147483648
        for j in range(index,n):

            # If i'th bit of set[j]
            # is set and set[j] is
            # greater than max so far.
            if ( (set[j] & (1 << i)) != 0
                     and set[j] > maxEle ):

                maxEle = set[j]
                maxInd = j

        # If there was no
        # element with i'th
        # bit set, move to
        # smaller i
        if (maxEle ==-2147483648):
            continue

        # Put maximum element
        # with i'th bit set
        # at index 'index'
        temp=set[index]
        set[index]=set[maxInd]
        set[maxInd]=temp

        # Update maxInd and
        # increment index
        maxInd = index

        # Do XOR of set[maxIndex]
        # with all numbers having
        # i'th bit as set.
        for j in range(n):

            # XOR set[maxInd] those
            # numbers which have the
            # i'th bit set
            if (j != maxInd and
               (set[j] & (1 << i)) != 0):
                set[j] = set[j] ^ set[maxInd]

        # Increment index of
        # chosen elements
        index=index + 1

    # Final result is
    # XOR of all elements
    res = 0
    for i in range(n):
        res =res ^ set[i]
    return res

# Driver code

set= [9, 8, 5]
n =len(set)

print("Max subset XOR is ",end="")
print(maxSubarrayXOR(set, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find
// maximum XOR subset
using System;

class GFG
{

    // Number of bits to
    // represent int
    static int INT_BITS = 32;

    // Function to return
    // maximum XOR subset
    // in set[]
    static int maxSubarrayXOR(int []set,
                              int n)
    {

        // Initialize index of
        // chosen elements
        int index = 0;

        // Traverse through all
        // bits of integer
        // starting from the most
        // significant bit (MSB)
        for (int i = INT_BITS - 1;
                 i >= 0; i--)
        {

        // Initialize index of
        // maximum element and
        // the maximum element
        int maxInd = index;
        int maxEle = int.MinValue;
        for (int j = index; j < n; j++)
        {

            // If i'th bit of set[j]
            // is set and set[j] is
            // greater than max so far.
            if ((set[j] & (1 << i)) != 0 &&
                 set[j] > maxEle)
            {
                maxEle = set[j];
                maxInd = j;
            }
        }

        // If there was no
        // element with i'th
        // bit set, move to
        // smaller i
        if (maxEle == -2147483648)
            continue;

        // Put maximum element
        // with i'th bit set
        // at index 'index'
        int temp = set[index];
        set[index] = set[maxInd];
        set[maxInd] = temp;

        // Update maxInd and
        // increment index
        maxInd = index;

        // Do XOR of set[maxIndex]
        // with all numbers having
        // i'th bit as set.
        for (int j = 0; j < n; j++)
        {

            // XOR set[maxInd] those
            // numbers which have the
            // i'th bit set
            if (j != maxInd && (set[j] &
               (1 << i)) != 0)
            set[j] = set[j] ^ set[maxInd];
    }

        // Increment index of
        // chosen elements
        index++;
    }

    // Final result is
    // XOR of all elements
        int res = 0;
        for (int i = 0; i < n; i++)
        res ^= set[i];
        return res;
    }

    // Driver code
    public static void Main()
    {
        int []set = {9, 8, 5};
        int n = set.Length;

        Console.Write("Max subset XOR is ");
        Console.Write(maxSubarrayXOR(set, n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum XOR subset

// Number of bits to represent int
$INT_BITS = 32;

// Function to return maximum XOR subset
// in set[]
function maxSubarrayXOR(&$set, $n)
{
    global $INT_BITS;

    // Initialize index of chosen elements
    $index = 0;

    // Traverse through all bits of integer
    // starting from the most significant bit (MSB)
    for ($i = $INT_BITS - 1; $i >= 0; $i--)
    {
        // Initialize index of maximum element
        // and the maximum element
        $maxInd = $index;
        $maxEle = 0;
        for ($j = $index; $j < $n; $j++)
        {
            // If i'th bit of set[j]
            // is set and set[j] is
            // greater than max so far.
            if ( ($set[$j] & (1 << $i)) != 0 &&
                  $set[$j] > $maxEle )
            {
                $maxEle = $set[$j];
                $maxInd = $j;
            }
        }

        // If there was no element with i'th
        // bit set, move to smaller i
        if ($maxEle == 0)
        continue;

        // Put maximum element with i'th bit
        // set at index 'index'
        $t = $set[$index];
        $set[$index] = $set[$maxInd];
        $set[$maxInd] = $t;

        // Update maxInd and increment index
        $maxInd = $index;

        // Do XOR of set[maxIndex] with all numbers
        // having i'th bit as set.
        for ($j = 0; $j < $n; $j++)
        {
            // XOR set[maxInd] those numbers which
            // have the i'th bit set
            if ($j != $maxInd &&
               ($set[$j] & (1 << $i)) != 0)
                $set[$j] = $set[$j] ^ $set[$maxInd];
        }

        // Increment index of chosen elements
        $index++;
    }

    // Final result is XOR of all elements
    $res = 0;
    for ($i = 0; $i < $n; $i++)
        $res ^= $set[$i];
    return $res;
}

// Driver Code
$set = array(9, 8, 5);
$n = sizeof($set);
echo "Max subset XOR is ";
echo maxSubarrayXOR($set, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// maximum XOR subset   

    // Number of bits to
    // represent int
    let INT_BITS = 32;

    // Function to return
    // maximum XOR subset
    // in set[]
    function maxSubarrayXOR(set,n)
    {
        // Initialize index of
        // chosen elements
        let index = 0;

        // Traverse through all
        // bits of integer
        // starting from the most
        // significant bit (MSB)

        for (let i = INT_BITS - 1; i >= 0; i--)
        {
            // Initialize index of
            // maximum element and
            // the maximum element
            let maxInd = index;
            let maxEle = Number.MIN_VALUE;
            for (let j = index; j < n; j++) {

                // If i'th bit of set[j]
                // is set and set[j] is
                // greater than max so far.
                if ((set[j] & (1 << i)) != 0 && set[j] > maxEle)
                {
                maxEle = set[j];
                maxInd = j;
                }
            }

            // If there was no
            // element with i'th
            // bit set, move to
            // smaller i
            if (maxEle == Number.MIN_VALUE)
                continue;

            // Put maximum element
            // with i'th bit set
            // at index 'index'
            let temp = set[index];
            set[index] = set[maxInd];
            set[maxInd] = temp;

            // Update maxInd and
            // increment index
            maxInd = index;

            // Do XOR of set[maxIndex]
            // with all numbers having
            // i'th bit as set.
            for (let j = 0; j < n; j++) {

                // XOR set[maxInd] those
                // numbers which have the
                // i'th bit set
                if (j != maxInd && (set[j] & (1 << i)) != 0)
                    set[j] = set[j] ^ set[maxInd];
            }

            // Increment index of
            // chosen elements
            index++;
        }

        // Final result is
        // XOR of all elements
        let res = 0;
        for (let i = 0; i < n; i++)
            res ^= set[i];
        return res;

    }

    // Driver code
    let set=[9, 8, 5];
    let n = set.length;
    document.write("Max subset XOR is ");
    document.write(maxSubarrayXOR(set, n));

    //  This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Max subset XOR is 13
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

**插图:**

```
Let the input set be : {9, 8, 5}

We start from 31st bit [Assuming Integers are 32 bit 
long]. The loop will continue without doing anything till 4'th bit.

The 4th bit is set in set[0] i.e. 9 and this is the maximum
element with 4th bit set. So we choose this element and check
if any other number has the same bit set. If yes, we XOR that 
number with 9\. The element set[1], i.e., 8 also has 4'th bit 
set. Now set[] becomes {9, 1, 5}.  We add 9 to the list of 
chosen elements by incrementing 'index'

We move further and find the maximum number with 3rd bit set
which is set[2] i.e. 5  No other number in the array has 3rd
bit set. 5 is also added to the list of chosen element.

We then iterate for bit 2 (no number for this) and then for 
1 which is 1\. But numbers 9 and 5 have the 1st bit set. Thus
we XOR 9 and 5 with 1 and our set becomes (8, 1, 4)

Finally, we XOR current elements of set and get the result
as 8 ^ 1 ^ 4 = 13.
```

**这是如何工作的？**
我们先来了解一个简单的情况，所有元素在不同位置都有最高有效位(msb)。这个特殊情况下的任务很简单，我们需要对所有元素进行异或运算。
如果输入包含多个具有相同 MSB 的数字，那么不清楚我们应该选择将其中的哪一个包含在异或中。我们所做的是将输入列表简化成一个等价的形式，其中不包含一个以上相同长度的数字。通过取最大元素，我们知道这个的 MSB 会在输出中。让这个 MSB 位于位置 I。如果有更多的元素具有第 I 个集合(或相同的 MSB)，我们将它们与最大数量异或，使得它们中的第 I 位变为 0，问题减少到 i-1 位。
**参考文献:**
[http://math . stackexchange . com/questions/48682/maximization-with-xor-operator](http://math.stackexchange.com/questions/48682/maximization-with-xor-operator)
注:上述方法与高斯消去法类似。考虑一个大小为 32×n 的矩阵，其中 32 是位数，n 是数组中的元素数。
本文由 [Ekta Goel](https://www.linkedin.com/in/ekta-goel-3a612a75?authType=NAME_SEARCH&authToken=n5Y7&locale=en_US&trk=tyah&trkInfo=clickedVertical%3Amynetwork%2CclickedEntityId%3A266060718%2CauthType%3ANAME_SEARCH%2Cidx%3A1-1-1%2CtarId%3A1453641087830%2Ctas%3AEkta%20Go) 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息