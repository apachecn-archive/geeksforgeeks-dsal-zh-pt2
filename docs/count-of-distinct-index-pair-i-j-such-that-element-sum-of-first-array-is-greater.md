# 不同索引对(I，j)的计数，使得第一个数组的元素和大于

> 原文:[https://www . geesforgeks . org/count-of-distinct-index-pair-I-j-so-element-sum-first-array-is-better/](https://www.geeksforgeeks.org/count-of-distinct-index-pair-i-j-such-that-element-sum-of-first-array-is-greater/)

给定两个数组 **a[]** 和 **b[]** ，两个数组的大小都是 **N** 。任务是计算不同对的数量，使得**(a[I]+a[j])>(b[I]+b[j])**服从 **(j > i)** 的条件。

**示例:**

> **输入:** N = 5，a[] = {1，2，3，4，5}，b[] = {2，5，6，1，9}
> **输出:** 1
> **解释:**
> 只有一个这样的对存在，那就是(0，3)。
> a[0] = 1，a[3] = 4，a[0] + a[3] = 1 + 4 = 5。
> b[0] = 2，b[3] = 1，b[0] + b[3] = 2 + 1 = 3。
> 显然，5 > 3 和 j > i .因此(0，3)是可能的一对。
> 
> **输入:** N = 5，a[] = {2，4，2，7，8}，b[] = {1，3，6，4，5}
> **输出:** 6

**天真方法:**
最简单的方法是遍历每一个可能的对，如果它满足条件，那么递增计数。然后，返回计数作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above problem
#include <bits/stdc++.h>
using namespace std;

// function to find the number of
// pairs satisfying the given cond.
int count_pairs(int a[],
                int b[], int N)
{

    // variables used for traversal
    int i, j;

    // count variable to store the
    // count of possible pairs
    int count = 0;

    // Nested loop to find out the
    // possible pairs
    for (i = 0; i < (N - 1); i++) {
        for (j = (i + 1); j < N; j++) {

            // Check if the given
            // condition is satisfied
            // or not. If yes then
            // increment the count.
            if ((a[i] + a[j])
                > (b[i] + b[j])) {

                count++;
            }
        }
    }

    // Return the count value
    return count;
}

// Driver Code
int main()
{

    // Size of the arrays
    int N = 5;

    // Initialise the arrays
    int a[N] = { 1, 2, 3, 4, 5 };
    int b[N] = { 2, 5, 6, 1, 9 };

    // function call that returns
    // the count of possible pairs
    cout << count_pairs(a, b, N)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
class GFG{

// function to find the number of
// pairs satisfying the given cond.
static int count_pairs(int []a,
                       int b[], int N)
{

    // variables used for traversal
    int i, j;

    // count variable to store the
    // count of possible pairs
    int count = 0;

    // Nested loop to find out the
    // possible pairs
    for (i = 0; i < (N - 1); i++)
    {
        for (j = (i + 1); j < N; j++)
        {

            // Check if the given
            // condition is satisfied
            // or not. If yes then
            // increment the count.
            if ((a[i] + a[j]) > (b[i] + b[j]))
            {
                count++;
            }
        }
    }

    // Return the count value
    return count;
}

// Driver Code
public static void main(String[] args)
{

    // Size of the arrays
    int N = 5;

    // Initialise the arrays
    int a[] = new int[]{ 1, 2, 3, 4, 5 };

    int b[] = new int[]{ 2, 5, 6, 1, 9 };

    // function call that returns
    // the count of possible pairs
    System.out.println(count_pairs(a, b, N));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above problem

# function to find the number of
# pairs satisfying the given cond.
def count_pairs(a, b, N):

    # count variable to store the
    # count of possible pairs
    count = 0;

    # Nested loop to find out the
    # possible pairs
    for i in range(0, N - 1):
        for j in range(i + 1, N):

            # Check if the given
            # condition is satisfied
            # or not. If yes then
            # increment the count.
            if ((a[i] + a[j]) > (b[i] + b[j])):
                count += 1;

    # Return the count value
    return count;

# Driver Code

# Size of the arrays
N = 5;

# Initialise the arrays
a = [ 1, 2, 3, 4, 5 ];
b = [ 2, 5, 6, 1, 9 ];

# function call that returns
# the count of possible pairs
print(count_pairs(a, b, N)

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above problem
using System;
class GFG{

// function to find the number of
// pairs satisfying the given cond.
static int count_pairs(int []a,
                       int []b, int N)
{

    // variables used for traversal
    int i, j;

    // count variable to store the
    // count of possible pairs
    int count = 0;

    // Nested loop to find out the
    // possible pairs
    for (i = 0; i < (N - 1); i++)
    {
        for (j = (i + 1); j < N; j++)
        {

            // Check if the given
            // condition is satisfied
            // or not. If yes then
            // increment the count.
            if ((a[i] + a[j]) > (b[i] + b[j]))
            {
                count++;
            }
        }
    }

    // Return the count value
    return count;
}

// Driver Code
public static void Main()
{

    // Size of the arrays
    int N = 5;

    // Initialise the arrays
    int []a = new int[]{ 1, 2, 3, 4, 5 };

    int []b = new int[]{ 2, 5, 6, 1, 9 };

    // function call that returns
    // the count of possible pairs
    Console.Write(count_pairs(a, b, N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program for the above problem

// function to find the number of
// pairs satisfying the given cond.
function count_pairs(a, b, N)
{

    // Variables used for traversal
    let i, j;

    // count variable to store the
    // count of possible pairs
    let count = 0;

    // Nested loop to find out the
    // possible pairs
    for(i = 0; i < (N - 1); i++)
    {
        for(j = (i + 1); j < N; j++)
        {

            // Check if the given
            // condition is satisfied
            // or not. If yes then
            // increment the count.
            if ((a[i] + a[j]) >
                (b[i] + b[j]))
            {
                count++;
            }
        }
    }

    // Return the count value
    return count;
}

// Driver code

// Size of the arrays
let N = 5;

// Initialise the arrays
let a = [ 1, 2, 3, 4, 5 ];
let b = [ 2, 5, 6, 1, 9 ];

// Function call that returns
// the count of possible pairs
document.write(count_pairs(a, b, N));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**
按照以下步骤解决问题:

*   将给定的不等式重新排列为:

> = >**a[I]+a[j]>b[I]+b[j]**
> =>**a[I]–b[I]+a[j]–b[j]>0**

*   初始化另一个大小为 **N** 的数组 **c[ ]** ，该数组存储**a[I]–b[I]**的值。
*   排序数组 **c[ ]** 。
*   将**答案**变量初始化为 0。迭代数组 **c[ ]** 。
*   对于数组**c【】**中的每个索引 **i** 执行以下操作:
    1.  如果 **c[i] < = 0** ，继续。
    2.  如果 **c[i] > 0** ，计算最小索引位置并将该值存储在变量 **pos** 中，使得 **c[pos] + c[i] > 0** 。使用 C++ STL 中的**下界**函数可以很容易的找到 **pos** 的值。
    3.  在**答案**中添加**(I–pos)**。

> 插图:
> 
> *   N = 5，a[] = {1，2，3，4，5}，b[] = {2，5，6，1，9}
> *   本例中的数组 c[]将是 c[] = {-1，-3，-3，3，-4}
> *   排序后，数组 c[] = {-4，-3，-3，-1，3}
> *   数组 c[]的第一个也是唯一一个正值位于索引 4 处。
> *   pos =下界(-c[4] + 1) =下界(-2) = 3。
> *   可能的配对数=**I–pos**= 4–3 =**1**。
> 
> **注意:**如果在数组 c【】中找到了多个正数，那么找出 c【】中每个正数的**位置**，并将**I–位置**的值加到计数中。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number
// of pairs.
int numberOfPairs(int* a,
                  int* b, int n)
{

    // Array c[] where
    // c[i] = a[i] - b[i]
    int c[n];

    for (int i = 0; i < n; i++) {
        c[i] = a[i] - b[i];
    }

    // Sort the array c
    sort(c, c + n);

    // Initialise answer as 0
    int answer = 0;

    // Iterate from index
    // 0 to n - 1
    for (int i = 1; i < n; i++) {

        // If c[i] <= 0 then
        // in the sorted array
        // c[i] + c[pos] can never
        // greater than 0
        // where pos < i
        if (c[i] <= 0)
            continue;

        // Find the minimum index
        // such that c[i] + c[j] > 0
        // which is equivalent to
        // c[j] >= - c[i] + 1
        int pos = lower_bound(c, c + n,
                              -c[i] + 1)
                  - c;

        // Add ( i - pos) to answer
        answer += (i - pos);
    }

    // return the answer
    return answer;
}

// Driver code
int32_t main()
{
    // Number of elements
    // in a and b
    int n = 5;

    // array a
    int a[] = { 1, 2, 3, 4, 5 };

    // array b
    int b[] = { 2, 5, 6, 1, 9 };

    cout << numberOfPairs(a, b, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function to find the number
// of pairs.
static int numberOfPairs(int[] a,
                         int[] b, int n)
{

    // Array c[] where
    // c[i] = a[i] - b[i]
    int c[] = new int[n];

    for(int i = 0; i < n; i++)
    {
        c[i] = a[i] - b[i];
    }

    // Sort the array c
    Arrays.sort(c);

    // Initialise answer as 0
    int answer = 0;

    // Iterate from index
    // 0 to n - 1
    for(int i = 1; i < n; i++)
    {

        // If c[i] <= 0 then
        // in the sorted array
        // c[i] + c[pos] can never
        // greater than 0
        // where pos < i
        if (c[i] <= 0)
            continue;

        // Which is equivalent to
        // c[j] >= - c[i] + 1
        int pos = -1;
        for(int j = 0; j < n; j++)
        {
            if (c[i] + c[j] > 0)
            {
                pos = j;
                break;
            }
        }

        // Add (i - pos) to answer
        answer += (i - pos);
    }

    // Return the answer
    return answer;
}

// Driver code   
public static void main (String[] args)
{

    // Number of elements
    // in a and b
    int n = 5;

    // array a
    int a[] = { 1, 2, 3, 4, 5 };

    // array b
    int b[] = { 2, 5, 6, 1, 9 };

    System.out.println(numberOfPairs(a, b, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program of the above approach
from bisect import bisect_left

# Function to find the number
# of pairs.
def numberOfPairs(a, b, n):

    # Array c[] where
    # c[i] = a[i] - b[i]
    c = [0 for i in range(n)]

    for i in range(n):
        c[i] = a[i] - b[i]

    # Sort the array c
    c = sorted(c)

    # Initialise answer as 0
    answer = 0

    # Iterate from index
    # 0 to n - 1
    for i in range(1, n):

        # If c[i] <= 0 then in the
        # sorted array c[i] + c[pos]
        # can never greater than 0
        # where pos < i
        if (c[i] <= 0):
            continue

        # Find the minimum index
        # such that c[i] + c[j] > 0
        # which is equivalent to
        # c[j] >= - c[i] + 1
        pos = bisect_left(c, -c[i] + 1)

        # Add ( i - pos) to answer
        answer += (i - pos)

    # Return the answer
    return answer

# Driver code
if __name__ == '__main__':

    # Number of elements
    # in a and b
    n = 5

    # Array a
    a = [ 1, 2, 3, 4, 5 ]

    # Array b
    b = [ 2, 5, 6, 1, 9 ]

    print(numberOfPairs(a, b, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program of the above approach
using System;

class GFG{

// Function to find the number
// of pairs.
static int numberOfPairs(int[] a,
                         int[] b, int n)
{

    // Array c[] where
    // c[i] = a[i] - b[i]
    int[] c = new int[n];

    for(int i = 0; i < n; i++)
    {
        c[i] = a[i] - b[i];
    }

    // Sort the array c
    Array.Sort(c);

    // Initialise answer as 0
    int answer = 0;

    // Iterate from index
    // 0 to n - 1
    for(int i = 1; i < n; i++)
    {

        // If c[i] <= 0 then
        // in the sorted array
        // c[i] + c[pos] can never
        // greater than 0
        // where pos < i
        if (c[i] <= 0)
            continue;

        // Which is equivalent to
        // c[j] >= - c[i] + 1
        int pos = -1;
        for(int j = 0; j < n; j++)
        {
            if (c[i] + c[j] > 0)
            {
                pos = j;
                break;
            }
        }

        // Add (i - pos) to answer
        answer += (i - pos);
    }

    // Return the answer
    return answer;
}

// Driver Code
static void Main()
{

    // Number of elements
    // in a and b
    int n = 5;

    // Array a
    int[] a = { 1, 2, 3, 4, 5 };

    // Array b
    int[] b = { 2, 5, 6, 1, 9 };

    Console.WriteLine(numberOfPairs(a, b, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript program of the above approach

    // Function to find the number of pairs.
    function numberOfPairs(a, b, n)
    {

        // Array c[] where
        // c[i] = a[i] - b[i]
        let c = new Array(n);

        for(let i = 0; i < n; i++)
        {
            c[i] = a[i] - b[i];
        }

        // Sort the array c
        c.sort(function(a, b){return a - b});

        // Initialise answer as 0
        let answer = 0;

        // Iterate from index
        // 0 to n - 1
        for(let i = 1; i < n; i++)
        {

            // If c[i] <= 0 then
            // in the sorted array
            // c[i] + c[pos] can never
            // greater than 0
            // where pos < i
            if (c[i] <= 0)
                continue;

            // Which is equivalent to
            // c[j] >= - c[i] + 1
            let pos = -1;
            for(let j = 0; j < n; j++)
            {
                if (c[i] + c[j] > 0)
                {
                    pos = j;
                    break;
                }
            }

            // Add (i - pos) to answer
            answer += (i - pos);
        }

        // Return the answer
        return answer;
    }

    // Number of elements
    // in a and b
    let n = 5;

    // Array a
    let a = [ 1, 2, 3, 4, 5 ];

    // Array b
    let b = [ 2, 5, 6, 1, 9 ];

    document.write(numberOfPairs(a, b, n));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O( N * log(N))，其中 **N** 为数组中的元素个数。*
***辅助空间:** O(N)*