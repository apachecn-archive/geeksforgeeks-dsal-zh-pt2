# 清空给定数组所需的给定类型的最小操作

> 原文:[https://www . geesforgeks . org/给定类型的最小操作-需要清空给定数组/](https://www.geeksforgeeks.org/minimum-operations-of-given-type-required-to-empty-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算移除所有数组元素所需的操作总数，这样如果数组的第一个元素是[最小的元素](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)，那么移除该元素，否则将第一个元素移动到数组的末尾。

**示例:**

> **输入:** A[] = {8，5，2，3}
> **输出:** 7
> **说明:**最初，A[] = {8，5，2，3}
> 步骤 1: 8 不是最小的。因此，将其移动到数组末尾会将 A[]修改为{5，2，3，8}。
> 第二步:5 不是最小的。因此，将其移动到数组末尾会将 A[]修改为{2，3，8，5}。
> 步骤 3: 2 最小。因此，将其从数组中移除会将 A[]修改为{3，8，5}
> 步骤 4: 3 是最小的。因此，将其从数组中移除会将 A[]修改为 A[] = {5，8}
> 步骤 6: 5 最小。因此，将其从阵列中移除会将 A[]修改为{8}
> 步骤 7: 8 是最小的。因此，将其从数组中删除会将 A[]修改为{}
> 因此，删除整个数组需要 7 次操作。
> 
> **输入:** A[] = {8，6，5，2，7，3，10 }
> T3】输出: 18

**天真法:**解决问题最简单的方法就是反复检查第一个数组元素是否是数组的[最小元素。如果发现为真，则移除该元素并增加计数。否则，将数组的第一个元素移动到数组的末尾，并增加计数。最后，打印获得的总计数。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

**高效方法:**使用[动态规划方法](https://www.geeksforgeeks.org/dynamic-programming/)和[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)可以高效地解决问题。按照以下步骤解决问题:

1.  将数组 **A[]** 的元素及其索引存储成一对[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)**T5，比如向量 **a** 。**
2.  [根据元素的值对向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)进行排序。
3.  初始化数组 **countGreater_right[]** 和 **countGreater_left[]** 以分别存储给定数组中当前元素右侧出现的较大元素的数量和当前元素左侧出现的较大元素的数量，这可以使用[的集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)来完成。
4.  最初，将向量 **a** 的起始元素的索引存储为 **prev = a[0].second.**
5.  用 **prev+1** 初始化**计数**。
6.  现在，遍历向量 **a** 的每个元素，从 **i = 1 到 N-1** 。
7.  对于每个元素，检索其原始索引为 **ind = a[i]。第二个**每个元素的 dp 转变为:

> 如果**找到>前一个**，将**计数**增加**计数大右【前一个】–大右计数**，否则
> 
> 将**计数**增加**计数大 _ 右[前一个] +计数大 _ 左[ind] + 1** 。

8.遍历后，打印**计**为答案。

下面是上述算法的实现:

## C++

```
// C++ program for the above approach

#include
#include
using namespace std;

// Function to find the count of greater
// elements to right of each index
void countGreaterRight(int A[], int len,
                       int* countGreater_right)
{

    // Store elements of array
    // in sorted order
    multiset s;

    // Traverse the array in reverse order
    for (int i = len - 1; i >= 0; i--) {
        auto it = s.lower_bound(A[i]);

        // Stores count of greater elements
        // on the right of i
        countGreater_right[i]
            = distance(it, s.end());

        // Insert current element
        s.insert(A[i]);
    }
}

// Function to find the count of greater
// elements to left of each index
void countGreaterLeft(int A[], int len,
                      int* countGreater_left)
{

    // Stores elements in
    // a sorted order
    multiset s;

    // Traverse the array
    for (int i = 0; i <= len; i++) {
        auto it = s.lower_bound(A[i]);

        // Stores count of greater elements
        // on the left side of i
        countGreater_left[i]
            = distance(it, s.end());

        // Insert current element into multiset
        s.insert(A[i]);
    }
}

// Function to find the count of operations required
// to remove all the array elements such that If
// 1st elements is smallest then remove the element
// otherwise move the element to the end of array
void cntOfOperations(int N, int A[])
{
    int i;

    // Store {A[i], i}
    vector<pair > a;

    // Traverse the array
    for (i = 0; i < N; i++) {

        // Insert {A[i], i}
        a.push_back(make_pair(A[i], i));
    }

    // Sort the vector pair according to
    // elements of the array, A[]
    sort(a.begin(), a.end());

    // countGreater_right[i]: Stores count of
    // greater elements on the right side of i
    int countGreater_right[N];

    // countGreater_left[i]: Stores count of
    // greater elements on the left side of i
    int countGreater_left[N];

    // Function to fill the arrays
    countGreaterRight(A, N, countGreater_right);
    countGreaterLeft(A, N, countGreater_left);

    // Index of smallest element
    // in array A[]
    int prev = a[0].second, ind;

    // Stores count of greater element
    // on left side of index i
    int count = prev + 1;

    // Iterate over remaining elements
    // in of a[][]
    for (i = 1; i  prev) {

            // Update count
            count += countGreater_right[prev]
                     - countGreater_right[ind];
        }

        else {

            // Update count
            count += countGreater_right[prev]
                     + countGreater_left[ind] + 1;
        }

        // Update prev
        prev = ind;
    }

    // Print count as total number
    // of operations
    cout << count;
}

// Driver Code
int main()
{

    // Given array
    int A[] = { 8, 5, 2, 3 };

    // Given size
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    cntOfOperations(N, A);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left, bisect_right

# Function to find the count of greater
# elements to right of each index
def countGreaterRight(A, lenn,countGreater_right):

    # Store elements of array
    # in sorted order
    s = {}

    # Traverse the array in reverse order
    for i in range(lenn-1, -1, -1):
        it = bisect_left(list(s.keys()), A[i])

        # Stores count of greater elements
        # on the right of i
        countGreater_right[i] = it

        # Insert current element
        s[A[i]] = 1
    return countGreater_right

# Function to find the count of greater
# elements to left of each index
def countGreaterLeft(A, lenn,countGreater_left):

    # Store elements of array
    # in sorted order
    s = {}

    # Traverse the array in reverse order
    for i in range(lenn):
        it = bisect_left(list(s.keys()), A[i])

        # Stores count of greater elements
        # on the right of i
        countGreater_left[i] = it

        # Insert current element
        s[A[i]] = 1
    return countGreater_left

# Function to find the count of operations required
# to remove all the array elements such that If
# 1st elements is smallest then remove the element
# otherwise move the element to the end of array
def cntOfOperations(N, A):

    # Store {A[i], i}
    a = []

    # Traverse the array
    for i in range(N):

        # Insert {A[i], i}
        a.append([A[i], i])

    # Sort the vector pair according to
    # elements of the array, A[]
    a = sorted(a)

    # countGreater_right[i]: Stores count of
    # greater elements on the right side of i
    countGreater_right = [0 for i in range(N)]

    # countGreater_left[i]: Stores count of
    # greater elements on the left side of i
    countGreater_left = [0 for i in range(N)]

    # Function to fill the arrays
    countGreater_right = countGreaterRight(A, N,
                                           countGreater_right)
    countGreater_left = countGreaterLeft(A, N,
                                         countGreater_left)

    # Index of smallest element
    # in array A[]
    prev, ind = a[0][1], 0

    # Stores count of greater element
    # on left side of index i
    count = prev

    # Iterate over remaining elements
    # in of a[][]
    for i in range(N):

        # Index of next smaller element
        ind = a[i][1]

        # If ind is greater
        if (ind > prev):

            # Update count
            count += countGreater_right[prev] - countGreater_right[ind]

        else:
            # Update count
            count += countGreater_right[prev] + countGreater_left[ind] + 1

        # Update prev
        prev = ind

    # Prcount as total number
    # of operations
    print (count)

# Driver Code
if __name__ == '__main__':

    # Given array
    A = [8, 5, 2, 3 ]

    # Given size
    N = len(A)

    # Function Call
    cntOfOperations(N, A)

# This code is contributed by mohit kumar 29
```

**Output:** 

```
7
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**注意:**上述方法可以通过使用 [芬威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)在每个索引的左侧和右侧找到更大元素的[计数来优化。](https://www.geeksforgeeks.org/count-smaller-elements-on-right-side-and-greater-elements-on-left-side-using-binary-index-tree/)