# 大小为 A 的字典上最小排列，其 B 个整数超过了前面所有的整数

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小大小排列 a-having-b-整数-超过所有先前整数/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-size-a-having-b-integers-exceeding-all-preceeding-integers/)

给定两个正整数 **A** 和 **B** ，任务是生成直到 **A** 的所有整数的字典最小排列，其中恰好 **B** 的整数大于其所有前面的元素。

**示例:**

> **输入:** A = 3，B = 2
> **输出:**【1，3，2】
> **解释:**
> 整数[1，3]的所有可能排列为[(1，2，3)，(1，3，2)，(2，1，3)，(2，3，1)，(3，1)，(3，1，2)，(3，2)，(3，2，1，1)]。在这些排列中，三个排列{(1，3，2)，(2，1，3)，(2，3，1)}满足必要条件。这三个排列中，字典上最小的排列是(1，3，2)。
> 
> **输入:** A = 4，B = 4
> T3】输出:【1，2，3，4】

**方法:**按照以下步骤解决问题:

1.  [使用来自](https://www.geeksforgeeks.org/python-permutation-given-string-using-inbuilt-function/) [**itertools**](https://www.geeksforgeeks.org/python-itertools/) 库的内置函数**排列()** 从**【1，A】**生成整数的所有可能排列。基本上，它返回一个包含所有可能排列的元组。
2.  现在，检查数组的最大元素和元素数量是否应该满足问题的条件计数相等。
3.  如果相等，那么满足条件的元素只有一个可能的列表。从逻辑上讲，它们只是从 1 开始按排序顺序排列的整数的范围。
4.  如果不是，从置换列表中取出每个元组，然后计算元组中存在的整数数量，该数量大于该元组中所有先前的整数。
5.  如果计数等于 **B** ，那么将该元组加载到另一个新列表中。
6.  测试由新列表加载的元素列表，无论它们是否按字典顺序排序，如果没有排序，则手动排列它们并返回最小值。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program for the above approach
from itertools import permutations

# Function to find lexicographically
# smallest permutation of [1, A]
# having B integers greater than
# all the previous elements

def getSmallestArray(A, B):

    # if A and B are equal
    if A == B:
        return list(range(1, A + 1))

    # Initialize pos_list to store list
    # of elements which are satisfying
    # the given conditions
    pos_list = []

    # List to store all possible permutations
    Main_List = list(permutations(range(1, A + 1), A))

    # Check all the permutations for
    # the given condition
    for L in Main_List:

        # Stores the count of elements
        # greater than all the previous
        # elements
        c = 0

        i = 0
        j = 1
        while j <= (len(L)-1):

            if L[j] > L[i]:
                i += 1

            elif i == j:
                c += 1
                j += 1
                i = 0

            else:
                j += 1
                i = 0

        # If count is equal to B
        if (c + 1) == B:

            pos_list.append(list(L))

    # If only one tuple satisfies
    # the given condition
    if len(pos_list) == 1:

        return pos_list[0]

    # Otherwise
    satisfied_list = []
    for i in pos_list:

        array_test = ''.join(map(str, i))
        satisfied_list.append(int(array_test))

        # Evaluate lexicographically smallest tuple
    small = min(satisfied_list)
    str_arr = list(str(small))
    ans = list(map(int, str_arr))

    # Return the answer
    return ans

# Driver Code

A = 3
B = 2

print(getSmallestArray(A, B))
```

**Output:** 

```
[1, 3, 2]
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效方法:**按照以下步骤优化上述方法:

1.  初始化一个数组 **arr[]** ，该数组由第一个 **A** 个自然数依次组成。
2.  创建一个结果数组 **ans[]** ，并从 **arr[]** 中追加第一个**(B–1)**元素。
3.  因此得到的数组具有满足给定条件的**(B–1)**元素。
4.  现在将最大元素从 **arr[]** 插入到结果数组中。移除插入的元素 **arr[]**
5.  因为我们已经有了 **B** 元素，所以结果数组有满足给定条件的 **B** 元素。
6.  现在，将所有剩余元素从 **arr[]** 逐一复制到结果数组中，并打印结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find lexicographically
// smallest permutation of [1, A]
// having B integers greater than
// all the previous elements
vector<int> getSmallestArray(int A, int B)
{

    // Initial array
    vector<int>arr(A);
    for(int i = 0; i < A; i++)
        arr[i] = i + 1;

    // Resultant array
    vector<int>ans(A);

    // Append the first (B-1) elements
    // to the resultant array 
    for(int i = 0; i < B - 1; i++)
        ans[i] = arr[i];

    // Append the maximum from the
    // initial array 
    ans[B - 1] = arr[A - 1];

    // Copy the remaining elements 
    for(int i = B; i < A; i++)
        ans[i] = arr[i - 1];

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int A = 3;
    int B = 2;

    vector<int>ans = getSmallestArray(A, B);

    for(auto i : ans)
        cout << i << " ";
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find lexicographically
// smallest permutation of [1, A]
// having B integers greater than
// all the previous elements
@SuppressWarnings("unchecked")
static void getSmallestArray(int A, int B)
{

    // Initial array
    Vector arr = new Vector();
    for(int i = 0; i < A; i++)
        arr.add(i + 1);

    // Resultant array
    Vector ans = new Vector();

    // Append the first (B-1) elements
    // to the resultant array 
    for(int i = 0; i < B - 1; i++)
        ans.add(arr.get(i));

    // Append the maximum from the
    // initial array 
    ans.add(arr.get(A - 1));

    // Copy the remaining elements 
    for(int i = B; i < A; i++)
        ans.add(arr.get(i - 1));

    // Print the answer
    for(int i = 0; i < ans.size(); i++)
        System.out.print(ans.get(i) + " ");
}

// Driver Code
public static void main(String args[])
{
    int A = 3;
    int B = 2;

    getSmallestArray(A, B);
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find lexicographically
# smallest permutation of [1, A]
# having B integers greater than
# all the previous elements

def getSmallestArray(A, B):

    # Initial array
    arr = (list(range(1, (A + 1))))

    # Resultant array
    ans = []

    # Append the first (B-1) elements
    # to the resultant array
    ans[0:B-1] = arr[0:B-1]

    # Delete the appended elements
    # from the initial array
    del arr[0:B-1]

    # Append the maximum from the
    # initial array
    ans.append(arr[-1])

    # Delete the appended maximum
    del arr[-1]

    # Copy the remaining elements
    ans[B:] = arr[:]

    # Return the answer
    return ans

# Driver Code

A = 3
B = 2

print(getSmallestArray(A, B))
```

## C#

```
// C# program for the above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to find lexicographically
// smallest permutation of [1, A]
// having B integers greater than
// all the previous elements
 static void getSmallestArray(int A, int B)
{

    // Initial array
    List<int> arr = new List<int>();
    for(int i = 0; i < A; i++)
        arr.Add(i + 1);

    // Resultant array
    List<int> ans = new List<int>();

    // Append the first (B-1) elements
    // to the resultant array 
    for(int i = 0; i < B - 1; i++)
        ans.Add(arr[i]);

    // Append the maximum from the
    // initial array 
    ans.Add(arr[A - 1]);

    // Copy the remaining elements 
    for(int i = B; i < A; i++)
        ans.Add(arr[i - 1]);

    // Print the answer
    for(int i = 0; i < A; i++)
        Console.Write(ans[i] + " ");
}

// Driver Code
public static void Main()
{
    int A = 3;
    int B = 2;

    getSmallestArray(A,B);
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find lexicographically
// smallest permutation of [1, A]
// having B integers greater than
// all the previous elements
function getSmallestArray( A, B)
{

    // Initial array
    let arr = [];

    for(let i = 0; i < A; i++)
        arr[i] = i + 1;

    // Resultant array
    let ans = [];
    for(let i = 0;i<A;i++)
        ans.push(0);

    // Append the first (B-1) elements
    // to the resultant array 
    for(let i = 0; i < B - 1; i++)
        ans[i] = arr[i];

    // Append the maximum from the
    // initial array 
    ans[B - 1] = arr[A - 1];

    // Copy the remaining elements 
    for(let i = B; i < A; i++)
        ans[i] = arr[i - 1];
    // Return the answer
    return ans;
}

// Driver Code
let A = 3;
let B = 2;
let ans = getSmallestArray(A, B);
for(let i =0;i<ans.length;i++)
       document.write( ans[i] ," ");

</script>
```

**Output:** 

```
[1, 3, 2]
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)