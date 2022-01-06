# 完整二叉树的最小计数，使得叶子的计数为 N

> 原文:[https://www . geeksforgeeks . org/完整二叉树的最小计数-这样树叶的计数为-n/](https://www.geeksforgeeks.org/minimum-count-of-full-binary-trees-such-that-the-count-of-leaves-is-n/)

给定整数 **N** 和无限数量的不同深度的[全二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，任务是选择最小数量的树，使得每棵树中叶节点的总数为 **N** 。
**例:**

> **输入:** N = 7
> **输出:** 3
> 深度为 2、1、0 的树可摘
> 叶节点数分别为 4、2、1。
> (4 + 2 + 1) = 7
> **输入:** N = 1
> **输出:** 1

**方法:**由于完全二叉树的叶节点数总是 2 的幂。所以，现在问题简化为求 2 的幂，当加在一起时，给出 N，这样求和中的项数最少，这就是所需的答案。
由于 2 的每次方在其二进制表示中只包含一个“1”，因此 **N** 将包含与求和项数相同数量的“1”(假设我们取最小项数)。因此，问题进一步简化为找到 **N** 中的设置位数，这可以使用[这篇](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)文章中使用的方法轻松计算。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the minimum
// count of trees required
int minTrees(int n)
{

    // To store the count of
    // set bits in n
    int count = 0;

    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Driver code
int main()
{
    int n = 7;

    cout << minTrees(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum
// count of trees required
static int minTrees(int n)
{

    // To store the count of
    // set bits in n
    int count = 0;

    while (n > 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int n = 7;

    System.out.print(minTrees(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# count of trees required
def minTrees(n):

    # To store the count of
    # set bits in n
    count = 0;

    while (n):
        n &= (n - 1);
        count += 1;
    return count;

# Driver code
if __name__ == '__main__':
    n = 7;
    print(minTrees(n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum
    // count of trees required
    static int minTrees(int n)
    {

        // To store the count of
        // set bits in n
        int count = 0;

        while (n > 0)
        {
            n &= (n - 1);
            count++;
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 7;

        Console.Write(minTrees(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum
    // count of trees required
    function minTrees(n)
    {

        // To store the count of
        // set bits in n
        let count = 0;

        while (n > 0)
        {
            n &= (n - 1);
            count++;
        }
        return count;
    }

    let n = 7;

      document.write(minTrees(n));

 // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3
```