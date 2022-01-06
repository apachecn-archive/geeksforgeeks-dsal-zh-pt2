# 节点值从 1 到 N 的二叉树两个节点之间的距离

> 原文:[https://www . geesforgeks . org/二进制树的两个节点之间的距离，节点值从 1 到 n/](https://www.geeksforgeeks.org/distance-between-two-nodes-of-binary-tree-with-node-values-from-1-to-n/)

给定一个二叉树

![1    ](img/f4ab382dc3c22bbb772b2ec216a26c49.png "Rendered by QuickLaTeX.com")

作为它的根和任何父

![i    ](img/01fd03000e431f64f777c8f150885f92.png "Rendered by QuickLaTeX.com")

它的左子将是 **2*i** ，右子将是 **2*i+1** 。任务是找到两个节点 **n1** 和 **n2** 之间的最小距离。

```

               1
            /      \
           2        3
         /  \      / \
        4    5    6   7
      /  \  / \  / \ / \
     .  .  .  . .  .  .  . 
```

**示例** :

```
Input : n1 = 7, n2 = 10
Output : 5

Input : n1 = 6, n2 = 7
Output : 4
```

有很多方法可以找到二叉树两个给定节点之间的最小距离。
这里有一个借助给定节点的二进制表示找到相同的有效方法。对于任何节点，仔细看看它的二进制表示。例如，考虑节点 **9** 。 **9 的二进制表示为 1001** 。因此，要找到从根到节点的路径，请找到该节点的二进制表示，并在该二进制表示中从左向右移动，如果遇到 1，则移动到树中的右子节点，如果遇到 0，则移动到左子节点。

```
Path of 9 as per bit representation
        1
       / \
      2   3
     /\   /\
    4  5 6  7
   /\ 
  8  9.
```

因此，为了找到两个节点之间的最小距离，我们将尝试找到两个节点的二进制表示的公共部分，这实际上是从根到生命周期评价的公共路径。假设两个节点的前 k 位相同。此外，如果二进制形式是 n 位的，那么它表明从根到该节点的路径距离是 n 长度。因此，从上面的陈述我们可以很容易地得出结论:如果 m 和 n 是两个节点的比特长度，并且两个节点的值的 k 个起始比特相同，那么两个节点之间的最小距离将是:**m+n–2 * k**。
**注:**最后一个相似位表示 LCA 在给定二叉树中的位置。
以下是上述方法的实施:

## C++

```
// C++ program to find minimum distance between
// two nodes in binary tree

#include <bits/stdc++.h>
using namespace std;

// Function to get minimum path distance
int minDistance(int n1, int n2)
{
    /** find the 1st dis-similar bit **/
    // count bit length of n1 and n2
    int bitCount1 = floor(log2(n1)) + 1;
    int bitCount2 = floor(log2(n2)) + 1;

    // find bit difference and maxBit
    int bitDiff = abs(bitCount1 - bitCount2);
    int maxBitCount = max(bitCount1, bitCount2);

    if (bitCount1 > bitCount2) {
        n2 = n2 * pow(2, bitDiff);
    }
    else {
        n1 = n1 * pow(2, bitDiff);
    }

    int xorValue = n1 ^ n2;
    int bitCountXorValue;

      if( xorValue == 0)
      bitCountXorValue = 1;
    else
    {
       bitCountXorValue = floor(log2(xorValue)) + 1;
    }
    int disSimilarBitPosition = maxBitCount -
                                     bitCountXorValue;

    // calculate result by formula
    int result = bitCount1 + bitCount2 -
                         2 * disSimilarBitPosition;
    return result;
}

// Driver program
int main()
{
    int n1 = 12, n2 = 5;

    cout << minDistance(n1, n2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum distance between
// two nodes in binary tree
import java.util.*;

class GFG
{
    // Function to get minimum path distance
    static int minDistance(int n1, int n2)
    {
        /** find the 1st dis-similar bit **/
        // count bit length of n1 and n2

        int bitCount1 =(int) Math.floor((Math.log(n1) /
                        Math.log(2))) + 1;
        int bitCount2 = (int)Math.floor((Math.log(n2) /
                        Math.log(2))) + 1;

        // find bit difference and maxBit
        int bitDiff = Math.abs(bitCount1 - bitCount2);
        int maxBitCount = Math.max(bitCount1, bitCount2);

        if (bitCount1 > bitCount2)
        {
            n2 = n2 *(int) Math.pow(2, bitDiff);
        }
        else   
        {
            n1 = n1 *(int) Math.pow(2, bitDiff);
        }

        int xorValue = n1 ^ n2;
        int bitCountXorValue;

        if( xorValue == 0)
          bitCountXorValue = 1;
        else
        {
           bitCountXorValue = (int)Math.floor((Math.log(xorValue) /
                                Math.log(2))) + 1;
        }
        int disSimilarBitPosition = maxBitCount -
                                         bitCountXorValue;

        // calculate result by formula
        int result = bitCount1 + bitCount2 - 2 * disSimilarBitPosition;
        return result;
    }

    // Driver program
    public static void main(String args[])
    {
        int n1 = 12, n2 = 5;
        System.out.println(minDistance(n1, n2));
    }
}

// This code is contributed by
// Sanjit_Prasad
```

## 蟒蛇 3

```
# Python 3 program to find minimum distance
# between two nodes in binary tree
from math import log2

# Function to get minimum path distance
def minDistance(n1, n2):

    # find the 1st dis-similar bit
    # count bit length of n1 and n2
    bitCount1 = int(log2(n1)) + 1
    bitCount2 = int(log2(n2)) + 1

    # find bit difference and maxBit
    bitDiff = abs(bitCount1 - bitCount2)
    maxBitCount = max(bitCount1, bitCount2)

    if (bitCount1 > bitCount2):
        n2 = int(n2 * pow(2, bitDiff))

    else:
        n1 = int(n1 * pow(2, bitDiff))

    xorValue = n1 ^ n2
    if xorValue == 0:
        bitCountXorValue = 1
    else:
        bitCountXorValue = int(log2(xorValue)) + 1
    disSimilarBitPosition = (maxBitCount -
                             bitCountXorValue)

    # calculate result by formula
    result = (bitCount1 + bitCount2 - 2 *
                   disSimilarBitPosition)
    return result

# Driver Code
if __name__ == '__main__':
    n1 = 12
    n2 = 5

    print(minDistance(n1, n2))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find minimum distance between
// two nodes in binary tree
using System;

class GFG
{
    // Function to get minimum path distance
    static int minDistance(int n1, int n2)
    {
        /** find the 1st dis-similar bit **/
        // count bit length of n1 and n2

        int bitCount1 =(int) Math.Floor((Math.Log(n1) /
                        Math.Log(2))) + 1;
        int bitCount2 = (int)Math.Floor((Math.Log(n2) /
                        Math.Log(2))) + 1;

        // find bit difference and maxBit
        int bitDiff = Math.Abs(bitCount1 - bitCount2);
        int maxBitCount = Math.Max(bitCount1, bitCount2);

        if (bitCount1 > bitCount2)
        {
            n2 = n2 *(int) Math.Pow(2, bitDiff);
        }
        else
        {
            n1 = n1 *(int) Math.Pow(2, bitDiff);
        }

        int xorValue = n1 ^ n2;

        int bitCountXorValue;

        if( xorValue == 0)
          bitCountXorValue = 1;
        else
        {
           bitCountXorValue = (int)Math.Floor((Math.Log(xorValue) /
                                Math.Log(2))) + 1;
        }

        int disSimilarBitPosition = maxBitCount - bitCountXorValue;

        // calculate result by formula
        int result = bitCount1 + bitCount2 - 2 * disSimilarBitPosition;
        return result;
    }

    // Driver code
    public static void Main(String []args)
    {
        int n1 = 12, n2 = 5;
        Console.WriteLine(minDistance(n1, n2));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum distance
// between two nodes in binary tree

// Function to get minimum path distance
function minDistance($n1, $n2)
{
    /** find the 1st dis-similar bit **/
    // count bit length of n1 and n2
    $bitCount1 = floor(log($n1, 2)) + 1;
    $bitCount2 = floor(log($n2, 2)) + 1;

    // find bit difference and maxBit
    $bitDiff = abs($bitCount1 - $bitCount2);
    $maxBitCount = max($bitCount1, $bitCount2);

    if ($bitCount1 > $bitCount2)
    {
        $n2 = $n2 * pow(2, $bitDiff);
    }
    else
    {
        $n1 = $n1 * pow(2, $bitDiff);
    }

    $xorValue = $n1 ^ $n2;
    $bitCountXorValue = floor(log($xorValue, 2)) + 1;
    $disSimilarBitPosition = $maxBitCount -
                             $bitCountXorValue;

    // calculate result by formula
    $result = $bitCount1 + $bitCount2 - 2 *
              $disSimilarBitPosition;
    return $result;
}

// Driver Code
$n1 = 12;
$n2 = 5;

echo minDistance($n1, $n2);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum distance between
// two nodes in binary tree

// Function to get minimum path distance
function minDistance(n1, n2)
{
    /** find the 1st dis-similar bit **/
    // count bit length of n1 and n2
    var bitCount1 = Math.floor(Math.log2(n1)) + 1;
    var bitCount2 = Math.floor(Math.log2(n2)) + 1;

    // find bit difference and maxBit
    var bitDiff = Math.abs(bitCount1 - bitCount2);
    var maxBitCount = Math.max(bitCount1, bitCount2);

    if (bitCount1 > bitCount2) {
        n2 = n2 * Math.pow(2, bitDiff);
    }
    else {
        n1 = n1 * Math.pow(2, bitDiff);
    }

    var xorValue = n1 ^ n2;
    var bitCountXorValue;

      if( xorValue == 0)
      bitCountXorValue = 1;
    else
    {
       bitCountXorValue = Math.floor(Math.log2(xorValue)) + 1;
    }
    var disSimilarBitPosition = maxBitCount -
                                     bitCountXorValue;

    // calculate result by formula
    var result = bitCount1 + bitCount2 -
                         2 * disSimilarBitPosition;
    return result;
}

// Driver program
var n1 = 12, n2 = 5;
document.write( minDistance(n1, n2));

</script>
```

**Output:** 

```
5
```