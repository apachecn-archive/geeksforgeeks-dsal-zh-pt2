# 最大化获得巧克力的人数

> 原文:[https://www . geesforgeks . org/最大化收到巧克力的人数/](https://www.geeksforgeeks.org/maximize-count-of-persons-receiving-a-chocolate/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**，由 **N** 个整数组成，**B【】**由 **M** 块巧克力的口味值和一个整数 **X** 组成，任务是在一个人只能吃一块巧克力且口味值在**【A[I]–X，A[I]+X】**范围内的条件下，找出能收到一块巧克力的最大人数。
***注:**巧克力一旦给了一个人，就不能再给其他任何人了。*

***例:***

> **输入:** A[] = {90，49，20，39，60}，B[] = {14，24，82}，X = 15
> **输出:** 3
> **说明:**
> 第 1 个人可以挑选第 3 块巧克力，因为第 3 块巧克力的价值(= 82)在[75(= 90–15)，105 ( = 90 + 15)]的范围内。
> 第二个人不能挑选任何巧克力，因为没有价值在[34(= 49–15)、64 ( = 49 + 15)范围内的巧克力。
> 第三个人可以挑选第一块巧克力，因为第一块巧克力的价值在[5(= 20–15)、35(= 20–15)]的范围内。
> 第四个人可以挑选第二块巧克力，因为第二块巧克力的价值在[24(= 39–15)和 54(= 39–15)]的范围内。
> 第 5 个人不能挑选任何巧克力，因为没有价值在[45(= 60–15)、75(= 60–15)]范围内的巧克力。
> 因此，领取一块巧克力的总人数为 3 人，这是最大可能。
> 
> ***输入:*** A[] = {2，4，6，40，50}，B[] = {38，36}，X = 13
> *T6】输出: 2*

**方法:**这个问题可以用[贪心法/a>](https://www.geeksforgeeks.org/greedy-algorithms/)和[搜索](https://www.geeksforgeeks.org/searching-algorithms/)解决。这里的关键观察是对于任何第 **i <sup>个</sup>人**，如果可能的话，分配范围内最小可能值的巧克力。否则，将此人排除在结果之外。请遵循以下步骤:

*   [按非递减顺序对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **A[]** 和 **B[]** 排序。
*   初始化一个[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)来存储数组 **B[]** 的元素。
*   初始化变量**计数= 0** ，以存储收到巧克力的人数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) A【】，使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)或[下界()](https://www.geeksforgeeks.org/lower_bound-in-cpp/)找到可以分配给每个 i <sup>第</sup>人的最小可能巧克力值。检查该值是否在范围**【a<sub>I</sub>–X，a<sub>I</sub>+X】**内。
*   如果发现是真的，则增加**计数**，并从**多集**中移除该巧克力的值。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number
// of persons receiving a chocolate
int countMaxPersons(int* A, int n, int* B,
                    int m, int x)
{

    // Initialize count as 0
    int count = 0;

    // Sort the given arrays
    sort(A, A + n);
    sort(B, B + m);

    // Initialize a multiset
    multiset<int> s;

    // Insert B[] array values into
    // the multiset
    for (int i = 0; i < m; i++)
        s.insert(B[i]);

    // Traverse elements in array A[]
    for (int i = 0; i < n; i++) {
        int val = A[i] - x;

        // Search for the lowest value in B[]
        auto it = s.lower_bound(val);

        // If found, increment count,
        // and delete from set
        if (it != s.end()
            && *it <= A[i] + x) {
            count++;
            s.erase(it);
        }
    }

    // Return the number of people
    return count;
}

// Driver Code
int main()
{
    int A[] = { 90, 49, 20, 39, 49 };
    int B[] = { 14, 24, 82 };
    int X = 15;
    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    // Function Call
    cout << countMaxPersons(A, N, B, M, X);
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left

# Function to count the maximum number
# of persons receiving a chocolate
def countMaxPersons(A, n, B, m, x):

    # Initialize count as 0
    count = 0

    # Sort the given arrays
    A = sorted(A)
    B = sorted(B)

    # Initialize a multiset
    s = []

    # Insert B[] array values into
    # the multiset
    for i in range(m):
        s.append(B[i])

    # Traverse elements in array A[]
    for i in range(n):
        val = A[i] - x

        # Search for the lowest value in B[]
        it = bisect_left(s,val)

        # If found, increment count,
        # and delete from set
        if (it != len(s) and it <= A[i] + x):
            count += 1
            del s[it]

    # Return the number of people
    return count

# Driver Code
if __name__ == '__main__':

    A = [90, 49, 20, 39, 49]
    B = [14, 24, 82]
    X = 15
    N = len(A)
    M = len(B)

    # Function Call
    print(countMaxPersons(A, N, B, M, X))

    # This code is contributed by mohit kumar 29
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(M)*