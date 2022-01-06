# 根据给定的条件，计算所有整数到 N 的排列，以形成一个非循环图

> 原文:[https://www . geeksforgeeks . org/count-所有整数的排列-up-n-可以基于给定条件形成非循环图/](https://www.geeksforgeeks.org/count-permutations-of-all-integers-upto-n-that-can-form-an-acyclic-graph-based-on-given-conditions/)

给定一个整数 **N，**的任务是从范围**【1，N】**中找出整数的排列数，根据以下条件可以形成一个[非循环图](https://en.wikipedia.org/wiki/Directed_acyclic_graph):

*   对于每一个 **1 ≤ i ≤ N** ，找出最大的 **j** ，使得 **1 ≤ j < i** 和**A【j】>A【I**】，并在节点 **i** 和节点 **j** 之间增加一条[无向边](https://www.geeksforgeeks.org/count-number-edges-undirected-graph/)。
*   对于每一个 **1 ≤ i ≤ N** ，找到最小的 **j** ，使得 **i < j ≤ N** 和**A【j】>A【I】**，在节点 **i** 和节点 **j** 之间增加一条**无向边**。

**示例:**

> **输入:** 3
> **输出:** 4
> **解释:**
> {1，2，3}:可能(图边:{ [1，2]，[2，3] }。因此，不存在循环)
> {1，3，2}:可能(图边:{ [1，3]，[2，3] }。因此，不存在循环)
> {2，1，3}:不可能(图边:{ [2，3]，[1，3]，[1，2] }。因此，循环存在)
> {2，3，1}:可能(图边:{ [2，3]，[1，3] }。因此，不存在循环)
> {3，1，2}:不可能(图边:{ [1，2]，[1，3]，[2，3] }。因此，循环存在)
> {3，2，1}:可能(图边:{ [2，3]，[1，2] }。因此，不存在循环)
> 
> **输入:**4
> T3】输出: 8

**方法:**按照以下步骤解决问题:

*   总共有 **N 个！**可以由范围**【1，N】**的整数排列组成的可能数组。
*   根据给定的条件，如果 **i，j，k (i < j < k)** 是来自数组的索引，那么如果 **A[i] > A[j]** 和 **A[j] < A[k]** ，那么将会有一个由边{**【A[j]、A[i]、【A[j]、A[k]、【A[i]、A[k]}**组成的循环。
*   除去这些排列，还剩下 2 个<sup>(N–1)</sup>可能的排列。
*   剩余的排列只给出范围**【1，N-1】**和 **1** 中整数的两个可能位置 **N** 的可能位置。

> **图解:**
> 对于 N = 3:
> 排列{2，1，3}包含一个循环作为 A[0] > A[1]和 A[1] < A[2]。
> 排列{3，1，2}包含一个循环，如 A[0] > A[1]和 A[1] < A[2]。
> 所有剩余的排列可以生成一个非循环图。
> 因此，有效排列数= 3！–2 = 4 = 2<sup>3–1</sup>

*   因此，打印**2<sup>N–1</sup>**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Find the count of possible graphs
void possibleAcyclicGraph(int N)
{
    cout << pow(2, N - 1);
    return;
}

// Driver Code
int main()
{

    int N = 4;
    possibleAcyclicGraph(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

// Find the count of
// possible graphs
static void possibleAcyclicGraph(int N)
{
  System.out.print((int)Math.pow(2,
                                 N - 1));
  return;
}

// Driver Code
public static void main(String[] args)
{
  int N = 4;
  possibleAcyclicGraph(N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Find the count of possible graphs
def possibleAcyclicGraph(N):

    print(pow(2, N - 1))
    return

# Driver code
if __name__ == '__main__':

    N = 4

    possibleAcyclicGraph(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG{

// Find the count of
// possible graphs
static void possibleAcyclicGraph(int N)
{
    Console.Write((int)Math.Pow(2, N - 1));

    return;
}

// Driver Code
public static void Main()
{
    int N = 4;

    possibleAcyclicGraph(N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Find the count of
// possible graphs
function possibleAcyclicGraph(N)
{
    document.write(Math.pow(2, N - 1));
    return;
}

// Driver Code
let N = 4;

possibleAcyclicGraph(N);

// This code is contributed by target_2

</script>
```

**Output**

```
8
```

***时间复杂度:O(logN)***
***空间复杂度:O(1)***