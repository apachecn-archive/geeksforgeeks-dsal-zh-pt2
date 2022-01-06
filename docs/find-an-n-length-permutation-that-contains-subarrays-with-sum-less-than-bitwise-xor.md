# 找到一个 N 长度排列，其中包含和小于按位异或的子阵列

> 原文:[https://www . geeksforgeeks . org/find-an-n-length-replacement-the-contains-subarrays-with-sum-小于-bitwise-xor/](https://www.geeksforgeeks.org/find-an-n-length-permutation-that-contains-subarrays-with-sum-less-than-bitwise-xor/)

给定一个正整数 **N** ，任务是找到长度 **N** 的排列，其任意[子阵列](https://www.geeksforgeeks.org/tag/subarray/)的[位“或”大于或等于](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度。

**示例:**

> **输入:** N = 5
> **输出:** 1 3 5 2 4
> **解释:**
> 从排列{1，3，5，2，$}考虑子阵列{1，3，5}。
> 子阵列的长度= 3
> 子阵列的按位= 1 | 3 | 5 = 7(大于 3)
> 同样，任何长度小于或等于 N 的子阵列都将满足条件。
> 
> **输入:**4
> T3】输出: 4 3 1 2

**方法:**实际上任何长度的排列 **N** 都满足基于以下事实的必要条件:

*   [任意一组数字的按位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)大于或等于该组中存在的最大数字。
*   因为任何子阵列将包含至少一个大于或等于其长度的元素，所以任何排列都满足给定的条件。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <iostream>
using namespace std;

// Function to print the
// required permutation
void findPermutation(int N)
{
   for(int i = 1; i <= N; i++)
     cout << i << " ";

   cout << endl;
}

// Driver code
int main()
{

    int N = 5;

    findPermutation(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Function to print the
// required permutation
static void findPermutation(int N)
{
    for(int i = 1; i <= N; i++)
        System.out.print(i + " ");
}

// Driver Code
public static void main(String[] args)
{
     int N = 5;

    findPermutation(N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to print the
# required permutation
def findPermutation(N):
    for i in range(1, N + 1, 1):
        print(i, end= " ") 
    print("\n", end = "")

# Driver code
if __name__ == '__main__':
    N = 5
    findPermutation(N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG{

// Function to print the
// required permutation
static void findPermutation(int N)
{
    for(int i = 1; i <= N; i++)
        Console.Write(i + " ");
}

// Driver code
public static void Main()
{
    int N = 5;

    findPermutation(N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// javascript implementation of
// the above approach

// Function to print the
// required permutation
function findPermutation(N)
{
   for(var i = 1; i <= N; i++)
     document.write( i + " ");

   document.write("<br>");
}

var N = 5;
findPermutation(N);

//This code in contributed by SoumikMondal
</script>
```

**Output:** 

```
1 2 3 4 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)