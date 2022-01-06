# 使用给定的运算最大化给定数组的和

> 原文:[https://www . geeksforgeeks . org/使用给定操作最大化给定数组的总和/](https://www.geeksforgeeks.org/maximize-the-sum-of-the-given-array-using-given-operations/)

给定由 **N** 个整数和一个整数 **K** 组成的两个数组 **A[]** 和 **B[]** ，任务是通过以下操作最大化从数组 **A[]** 计算出的和:

*   对于包含 **0** 的**B【】**中的每个指数，A【】中的相应指数被添加到**和**中。
*   对于包含 **1** 的 **B[]** 中的每个指数，将 A[]中相应指数的值加到 atmat**K**这些指数的总和上。对于其余指数，从总和中减去。

**示例:**

> **输入:** A[] = {5，4，6，2，8}，B[] = {1，0，1，0}，K = 2
> **输出:** 21
> **说明:**
> 将 A[1]和 A[4]相加和为 B[1] = B[4] = 0
> 因此和= 4 + 8 = 12。
> 现在，将 A[0]和 A[3]加到总和中，因为可以添加 K 个元素。
> 最后，和减去 2。
> 因此，最大可能和= 12+5+6–2 = 21
> **输入:** A[] = {5，2，1，8，10，5}，B[] = {1，1，1，1，0，0}，K = 3
> **输出:** 29

**进场:**

按照以下步骤解决问题:

*   按降序对数组 A[]进行排序。
*   要最大化总和，首先从排序数组中添加 **B[]** 中的索引包含的 **1** 对应的 **K** 元素。减去剩下的这些元素。
*   将**A【】**中与包含 **0** 的**B【】**中的指数相对应的所有值相加。

下面是上述方法的实现:

## C++

```
// C++ Program to maximize the
// sum of the given array
#include <bits/stdc++.h>
using namespace std;

// Comparator to sort the array
// in ascending order
bool compare(pair<int, int> p1,
             pair<int, int> p2)
{
    return p1.first > p2.first;
}

// Function to maximize the sum of
// the given array
int maximizeScore(int A[], int B[],
                  int K, int N)
{

    // Stores {A[i], B[i]} pairs
    vector<pair<int, int> > pairs(N);
    for (int i = 0; i < N; i++) {
        pairs[i] = make_pair(A[i], B[i]);
    }

    // Sort in descending order of the
    // values in the array A[]
    sort(pairs.begin(), pairs.end(), compare);

    // Stores the maximum sum
    int sum = 0;
    for (int i = 0; i < N; i++) {

        // If B[i] is equal to 0
        if (pairs[i].second == 0) {

            // Simply add A[i] to the sum
            sum += pairs[i].first;
        }

        else if (pairs[i].second == 1) {

            // Add the highest K numbers
            if (K > 0) {
                sum += pairs[i].first;
                K--;
            }

            // Subtract from the sum
            else {
                sum -= pairs[i].first;
            }
        }
    }

    // Return the sum
    return sum;
}

// Driver Code
int main()
{

    int A[] = { 5, 4, 6, 2, 8 };
    int B[] = { 1, 0, 1, 1, 0 };
    int K = 2;
    int N = sizeof(A) / sizeof(int);
    cout << maximizeScore(A, B, K, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximise the
// sum of the given array
import java.util.*;

class Pair implements Comparable<Pair>
{
    int first, second;
    Pair(int x, int y)
    {
        first = x;
        second = y;
    }
    public int compareTo(Pair p)
    {
        return p.first - first;
    }
}

class GFG{

// Function to maximise the sum of
// the given array
static int maximiseScore(int A[], int B[],
                         int K, int N)
{

    // Stores {A[i], B[i]} pairs
    ArrayList<Pair> pairs = new ArrayList<>();
    for(int i = 0; i < N; i++)
    {
        pairs.add(new Pair(A[i], B[i]));
    }

    // Sort in descending order of the
    // values in the array A[]
    Collections.sort(pairs);

    // Stores the maximum sum
    int sum = 0;
    for(int i = 0; i < N; i++)
    {

        // If B[i] is equal to 0
        if (pairs.get(i).second == 0)
        {

            // Simply add A[i] to the sum
            sum += pairs.get(i).first;
        }

        else if (pairs.get(i).second == 1)
        {

            // Add the highest K numbers
            if (K > 0)
            {
                sum += pairs.get(i).first;
                K--;
            }

            // Subtract from the sum
            else
            {
                sum -= pairs.get(i).first;
            }
        }
    }

    // Return the sum
    return sum;
}

// Driver Code
public static void main(String[] args)
{

    int A[] = { 5, 4, 6, 2, 8 };
    int B[] = { 1, 0, 1, 1, 0 };
    int K = 2;
    int N = A.length;

    System.out.print(maximiseScore(A, B, K, N));
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python Program to maximise the
# sum of the given array

# Comparator to sort the array
# in ascending order
def compare(p1, p2):
    return p1[0] > p2[0]

# Function to maximise the sum of
# the given array
def maximiseScore(A, B, K, N):

    # Stores {A[i], B[i]} pairs
    pairs = []
    for i in range(N):
        pairs.append([A[i], B[i]])

    # Sort in descending order of the
    # values in the array A[]
    pairs.sort(key = lambda x:x[0], reverse = True)

    # Stores the maximum sum
    Sum = 0

    for i in range(N):

        # If B[i] is equal to 0
        if(pairs[i][1] == 0):

            # Simply add A[i] to the sum
            Sum += pairs[i][0]
        elif(pairs[i][1] == 1):

            # Add the highest K numbers
            if(K > 0):
                Sum += pairs[i][0]
                K -= 1

            # Subtract from the sum
            else:
                Sum -= pairs[i][0]

    # Return the sum
    return Sum

# Driver Code
A = [5, 4, 6, 2, 8]
B = [1, 0, 1, 1, 0]
K = 2
N = len(A)
print(maximiseScore(A, B, K, N))

# This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
21
```

**时间复杂度:***O(N * log(N))*
T5】辅助空间: *O(N)*