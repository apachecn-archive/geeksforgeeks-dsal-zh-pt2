# 根据给定条件缩小数组后找到所有可能的唯一索引

> 原文:[https://www . geeksforgeeks . org/在给定条件下减少数组后查找所有可能的唯一索引/](https://www.geeksforgeeks.org/find-all-possible-unique-indices-after-reducing-the-array-based-on-given-conditions/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr** ，以及一个键数组，这样 arr 中每个元素的键最初等于它在 arr 中的索引。假设可以执行某些移动，其中在一次移动中，选择两个索引 **(i，j)** ，从数组中移除相应的元素，并添加等于移除元素总和的新元素(**arr**【I】+**arr**【j】)，其中一个键等于 arr[i]和 arr[j]中较大元素的键。如果两个元素相等，则可以使用两个元素中的任何一个。任务是当数组只包含一个元素时，在末尾打印所有可能的唯一键。

示例:

> **输入:** N = 3，arr[] = {2，3，4}
> **输出:** 1，2
> **解释:**最初所有元素都有与其索引相等的键。(2- > 0，3- > 1，4- > 2)。
> 案例 1:
> 
> *   取下 2 和 3，用钥匙 1 插入 5。新数组将是(5->1，4->2)
> *   拆下 5 和 4，并用钥匙 1 插入 9。新数组将是(9->1)
> *   对于这些操作，数组中的最终索引将是 1。
> 
> 案例 2:
> 
> *   拆下 2 和 4，并用键 2 插入 6。新数组将是(3->1，6->2)
> *   拆下 6 和 3，并用键 2 插入 9。新数组将是(9->2)
> *   对于这些操作，数组中的最终索引将是 2。
> 
> 所以总共有两个可能的唯一键(1 和 2)。
> 
> **输入:** N = 3，arr[] = {1，1，4}
> **输出:** 2
> **说明:**最后剩下的指数在所有情况下都会是 2。所以总共有 1 个可能的索引。

**方法:**保持一对向量，该向量将为，为每个**arr【I】**存储 **{value，i}** 和一个变量和，该变量和将存储剩余部分的和。我们按照值和的非递减顺序对向量进行排序，从末尾开始遍历。每当数组左边部分的剩余和小于当前元素的值时，这意味着左边部分的所有元素都不能是答案，所以我们从这里开始打破循环，因为左边部分的那些元素将在最后被右边更大元素的键替换。

按照以下步骤作为上述方法的算法:

*   维护一个 [**<u>对向量</u>**](https://www.geeksforgeeks.org/pair-in-cpp-stl/) ，它以 **{value，index}** 的形式存储数组的元素
*   [**<u>按值的非递减顺序排序对向量</u>**](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) 。
*   取一个变量 **sum** ，它将最初存储数组中所有元素的总和。
*   [**<u>在排序后的向量中从右向左迭代</u>**](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) 。
*   如果当前元素的值大于其左侧所有元素的总和，则中断循环，否则，将当前索引作为有效答案相加，将总和减去当前元素的值，并继续处理剩余元素。
*   最后返回答案中所有可能的指数。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// total possible different indexes
// after all possible operations mentioned
int totalFinalIndexes(int A[], int N)
{
    // Variable to calculate possible indexes
    int res = 0;

    // Variable to store the total sum
    int sum = 0;

    // vector to store total possible indexes
    vector<int> ans;
    // Calculat the sum and push them in a
    // pair vector with their indices.

    vector<pair<int, int> > elements;
    for (int i = 0; i < N; i++) {
        sum += A[i];
        elements.push_back(make_pair(A[i], i));
    }

    sort(elements.begin(), elements.end());

    // Iterate from right to left
    // and calculate total possible indexes
    for (int i = N - 1; i >= 0; i--) {
        // increment the current index.
        res++;

        // Decrease the sum
        sum -= elements[i].first;

        // Push the current index
        // in the ans vector
        ans.push_back(elements[i].second);

        // All other indexes
        // cannot be the possible answers
        if (sum < elements[i].first)
            break;
    }

    // Print the indexes of the values
    for (auto x : ans) {
        cout << x << " ";
    }
    return 0;
}

// Driver Code
int main()
{
    int N = 3;
    int A[] = { 2, 3, 4 };
    totalFinalIndexes(A, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
// Function to calculate
// total possible different indexes
// after all possible operations mentioned
static int totalFinalIndexes(int A[], int N)
{

    // Variable to calculate possible indexes
    int res = 0;

    // Variable to store the total sum
    int sum = 0;

    // vector to store total possible indexes
    Vector<Integer> ans = new Vector<Integer>();

    // Calculat the sum and push them in a
    // pair vector with their indices.
    Vector<pair > elements = new Vector<pair>();
    for (int i = 0; i < N; i++) {
        sum += A[i];
        elements.add(new pair(A[i], i));
    }

    Collections.sort(elements,(a,b)->a.first-b.first);

    // Iterate from right to left
    // and calculate total possible indexes
    for (int i = N - 1; i >= 0; i--) {
        // increment the current index.
        res++;

        // Decrease the sum
        sum -= elements.get(i).first;

        // Push the current index
        // in the ans vector
        ans.add(elements.get(i).second);

        // All other indexes
        // cannot be the possible answers
        if (sum < elements.get(i).first)
            break;
    }

    // Print the indexes of the values
    for (int x : ans) {
        System.out.print(x+ " ");
    }
    return 0;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    int A[] = { 2, 3, 4 };
    totalFinalIndexes(A, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# python implementation for the above approach

# Function to calculate
# total possible different indexes
# after all possible operations mentioned
def totalFinalIndexes(A, N):

    # Variable to calculate possible indexes
    res = 0

    # Variable to store the total sum
    sum = 0

    # vector to store total possible indexes
    ans = []

    # Calculat the sum and push them in a
    # pair vector with their indices.
    elements = []
    for i in range(0, N):
        sum += A[i]
        elements.append([A[i], i])

    elements.sort()

    # Iterate from right to left
    # and calculate total possible indexes
    for i in range(N-1, -1, -1):
        # increment the current index.
        res = res + 1

        # Decrease the sum
        sum -= elements[i][0]

        # Push the current index
        # in the ans vector
        ans.append(elements[i][1])

        # All other indexes
        # cannot be the possible answers
        if (sum < elements[i][0]):
            break

    # Print the indexes of the values
    for x in ans:
        print(x, end=" ")

    return 0

# Driver Code
if __name__ == "__main__":

    N = 3
    A = [2, 3, 4]
    totalFinalIndexes(A, N)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;

public class GFG{
    class pair : IComparable<pair>
    {
        public int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
         public int CompareTo(pair p)
         {
             return this.first-p.second;
         }
    }

// Function to calculate
// total possible different indexes
// after all possible operations mentioned
static int totalFinalIndexes(int []A, int N)
{

    // Variable to calculate possible indexes
    int res = 0;

    // Variable to store the total sum
    int sum = 0;

    // vector to store total possible indexes
    List<int> ans = new List<int>();

    // Calculat the sum and push them in a
    // pair vector with their indices.
    List<pair > elements = new List<pair>();
    for (int i = 0; i < N; i++) {
        sum += A[i];
        elements.Add(new pair(A[i], i));
    }

    elements.Sort();
    elements.Reverse();

    // Iterate from right to left
    // and calculate total possible indexes
    for (int i = N - 1; i >= 0; i--)
    {

        // increment the current index.
        res++;

        // Decrease the sum
        sum -= elements[i].first;

        // Push the current index
        // in the ans vector
        ans.Add(elements[i].second);

        // All other indexes
        // cannot be the possible answers
        if (sum < elements[i].first)
            break;
    }

    // Print the indexes of the values
    foreach (int x in ans) {
        Console.Write(x+ " ");
    }
    return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3;
    int []A = { 2, 3, 4 };
    totalFinalIndexes(A, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // JavaScript implementation for the above approach

    // Function to calculate
    // total possible different indexes
    // after all possible operations mentioned
    const totalFinalIndexes = (A, N) => {
        // Variable to calculate possible indexes
        let res = 0;

        // Variable to store the total sum
        let sum = 0;

        // vector to store total possible indexes
        let ans = [];
        // Calculat the sum and push them in a
        // pair vector with their indices.

        let elements = [];
        for (let i = 0; i < N; i++) {
            sum += A[i];
            elements.push([A[i], i]);
        }
        elements.sort((a, b) => a - b);

        // Iterate from right to left
        // and calculate total possible indexes
        for (let i = N - 1; i >= 0; i--) {
            // increment the current index.
            res++;

            // Decrease the sum
            sum -= elements[i][0];

            // Push the current index
            // in the ans vector
            ans.push(elements[i][1]);

            // All other indexes
            // cannot be the possible answers
            if (sum < elements[i][0])
                break;
        }

        // Print the indexes of the values
        for (let x in ans) {
            document.write(`${ans[x]} `);
        }
        return 0;
    }

    // Driver Code
    let N = 3;
    let A = [2, 3, 4];
    totalFinalIndexes(A, N);

    // This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
2 1
```

**时间复杂度:** O(N*log(N))
**辅助空间:** O(N)