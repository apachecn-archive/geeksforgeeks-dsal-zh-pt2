# 将每个单元的硬币移动到矩阵的任何一个单元所需的最小移动次数

> 原文:[https://www . geeksforgeeks . org/将每个单元的最小移动硬币移动到矩阵的任意一个单元/](https://www.geeksforgeeks.org/minimum-moves-taken-to-move-coin-of-each-cell-to-any-one-cell-of-matrix/)

给定一个奇数 **N** ，它代表一个大小为 **N x N** 的网格，该网格最初由硬币填充，任务是找到所有硬币移动到网格的任何单元所需的最小移动次数，以便在每一步中，网格中间的一些任意硬币可以移动到周围八个单元中的任何一个。

**示例:**

> **输入:** N = 3
> **输出:** 8
> **说明:**
> 一个 3×3 的网格中总共有 9 个单元。假设所有的硬币都必须被带到中央牢房，应该移动 8 枚硬币，步数是 8。
> 
> **输入:**N = 5
> T3】输出: 40

**进场:**只有当所有硬币都移动到格子中心时，才能获得最小步数。因此，想法是将整个网格分成多个层。

*   网格的每一层都需要 K 次移动才能到达中心。那就是:
    1.  第一层的硬币向中心移动一步。
    2.  第二层的硬币分两步移到中间，以此类推。
*   例如，让 N = 5。然后，网格被分成如下层:
*   在上图中，标记为红色的硬币位于第 1 层，标记为蓝色的硬币位于第 2 层。
*   同样，对于 N×N 大小的网格，我们可以将硬币分成 N//2 层。
*   在每层 K 中，存在的硬币数量为(8 * K)。并且，所需的步数为 K，因此，遍历所有图层，总步数为**8 * K<sup>2</sup>T3**

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum number
// of moves taken to move the element of
// each cell to any one cell of the
// square matrix of odd length
#include <iostream>
using namespace std;

// Function to find the minimum number
// of moves taken to move the element 
// of each cell to any one cell of the
// square matrix of odd length
int calculateMoves(int n)
{

    // Initializing count to 0
    int count = 0;

    // Number of layers that are
    // around the centre element
    int layers = n / 2;

    // Iterating over ranger of layers
    for(int k = 1; k < layers + 1; k++)
    {

       // Increase the value of count 
       // by 8 * k * k
       count += 8 * k * k;
    }
    return count;
}

// Driver code
int main()
{
    int N = 5;

    cout << calculateMoves(N);
}

// This code is contributed by coder001
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number
// of moves taken to move the element of
// each cell to any one cell of the
// square matrix of odd length
class GFG{

// Function to find the minimum number
// of moves taken to move the element
// of each cell to any one cell of the
// square matrix of odd length
public static int calculateMoves(int n)
{

    // Initializing count to 0
    int count = 0;

    // Number of layers that are
    // around the centre element
    int layers = n / 2;

    // Iterating over ranger of layers
    for(int k = 1; k < layers + 1; k++)
    {

       // Increase the value of count
       // by 8 * k * k
       count += 8 * k * k;
    }
    return count;
}

// Driver code   
public static void main(String[] args)
{
    int N = 5;

    System.out.println(calculateMoves(N));
}
}

// This code is contributed by divyeshrabadiya07   
```

## 蟒蛇 3

```
# Python3 program to find the minimum number
# of moves taken to move the element of
# each cell to any one cell of the
# square matrix of odd length

# Function to find the minimum number
# of moves taken to move the element of
# each cell to any one cell of the
# square matrix of odd length
def calculateMoves(n):

    # Initializing count to 0
    count = 0

    # Number of layers that are
    # around the centre element
    layers = n//2

    # Iterating over ranger of layers
    for k in range(1, layers + 1):

        # Increase the value of count by
        # 8 * k * k
        count+= 8 * k*k

    return count

# Driver code
if __name__ == "__main__":

    N = 5

    print(calculateMoves(N))
```

## C#

```
// C# program to find the minimum number
// of moves taken to move the element of
// each cell to any one cell of the
// square matrix of odd length
using System;
class GFG{

// Function to find the minimum number
// of moves taken to move the element
// of each cell to any one cell of the
// square matrix of odd length
public static int calculateMoves(int n)
{

    // Initializing count to 0
    int count = 0;

    // Number of layers that are
    // around the centre element
    int layers = n / 2;

    // Iterating over ranger of layers
    for(int k = 1; k < layers + 1; k++)
    {

        // Increase the value of count
        // by 8 * k * k
        count += 8 * k * k;
    }
    return count;
}

// Driver code
public static void Main()
{
    int N = 5;

    Console.Write(calculateMoves(N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to find the minimum number
// of moves taken to move the element of
// each cell to any one cell of the
// square matrix of odd length

// Function to find the minimum number
// of moves taken to move the element
// of each cell to any one cell of the
// square matrix of odd length
function calculateMoves(n)
{

    // Initializing count to 0
    var count = 0;

    // Number of layers that are
    // around the centre element
    var layers = parseInt(n / 2);

    // Iterating over ranger of layers
    for(var k = 1; k < layers + 1; k++)
    {

        // Increase the value of count
        // by 8 * k * k
        count += 8 * k * k;
    }
    return count;
}

// Driver code
var N = 5;

document.write(calculateMoves(N));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
40
```