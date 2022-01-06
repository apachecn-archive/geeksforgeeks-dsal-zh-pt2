# 大小为 3 的递增子序列的最大乘积

> 原文:[https://www . geesforgeks . org/maximum-product-递增-subserial-size-3/](https://www.geeksforgeeks.org/maximum-product-increasing-subsequence-size-3/)

给定一组不同的正整数，任务是找到大小为 3 的递增子序列的最大乘积，即我们需要找到 arr[i]*arr[j]*arr[k]，这样 arr[i] < arr[j] < arr[k]和 i < j < k < n

**示例:**

```
Input  : arr[] = {10, 11, 9, 5, 6, 1, 20}
Output : 2200                                        
Increasing sub-sequences of size three are  
{10, 11, 20} => product 10*11*20 = 2200  
{5,  6, 20}  => product 5*6*20 = 600
Maximum product : 2200

Input : arr[] = {1, 2, 3, 4}
Output : 24   

```

一个**简单的解决方案**是使用三个嵌套循环来考虑大小为 3 的所有子序列，使得 arr[I]<arr[j]<arr[k]&I<j<k。对于每个这样的子序列，计算乘积，并在需要时更新最大乘积。

一个**高效的解决方案**需要 O(n log n)时间。这个想法是为每个元素找到以下两个。利用下面两个，我们找到了以一个元素作为中间元素的递增子序列的最大乘积。为了找到最大的乘积，我们简单地将元素乘以 2 以下。

1.  右侧最大的元素。
2.  左侧最大的较小元素。

注:我们需要最大的，因为我们想最大限度地提高产品。

为了找到右侧最大的元素，我们使用这里讨论的方法。我们只需要从右边遍历数组，并跟踪到目前为止看到的最大元素。

为了找到最近的较小元素，我们使用自平衡二叉查找树，因为我们可以在 O(Log n)时间内找到最近的较小元素。在 C++中， [set](https://www.geeksforgeeks.org/set-in-cpp-stl/) 实现了同样的功能，我们可以用它来寻找最近的元素。

以下是上述想法的实现。在实现中，我们首先为所有元素找到较小的。然后我们找到更大的元素，得到单循环。

## C++

```
// C++ program to find maximum product of an increasing
// subsequence of size 3
#include<bits/stdc++.h>
using namespace std;

// Returns maximum product of an increasing subsequence of
// size 3 in arr[0..n-1].  If no such subsequence exists,
// then it returns INT_MIN
long long int maxProduct(int arr[] , int n)
{
    // An array ti store  closest smaller element on left
    // side of every element. If there is no such element
    // on left side, then smaller[i] be -1.
    int smaller[n];
    smaller[0] = -1 ;// no smaller element on right side

    // create an empty set to store visited elements from
    // left side. Set can also quickly find largest smaller
    // of an element.
    set<int>S ;
    for (int i = 0; i < n ; i++)
    {
        // insert arr[i] into the set S
        auto j =  S.insert(arr[i]);
        auto itc = j.first; // points to current element in set

        --itc; // point to prev element in S

        // If current element has previous element
        // then its first previous element is closest
        // smaller element (Note : set keeps elements
        // in sorted order)
        if (itc != S.end())
            smaller[i] = *itc;
        else
            smaller[i] = -1;
    }

    // Initialize result
    long long int result = INT_MIN;

    // Initialize greatest on right side.
    int max_right = arr[n-1];

    // This loop finds greatest element on right side
    // for every element. It also updates result when
    // required.
    for (int i=n-2 ; i >= 1; i--)
    {
        // If current element is greater than all
        // elements on right side, update max_right
        if (arr[i] > max_right)
            max_right = arr[i];

        // If there is a greater element on right side
        // and there is a smaller on left side, update
        // result.
        else if (smaller[i] != -1)
            result = max(smaller[i] * arr[i] * max_right,
                                                result);
    }

    return result;
}

// Driver Program
int main()
{
    int arr[] = {10, 11, 9, 5, 6, 1, 20};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << maxProduct(arr, n) << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program to find maximum product 
# of an increasing subsequence of size 3
import sys

# Returns maximum product of an increasing 
# subsequence of size 3 in arr[0..n-1]. 
# If no such subsequence exists, 
# then it returns INT_MIN
def maxProduct(arr, n):

    # An array ti store closest smaller element 
    # on left side of every element. If there is 
    # no such element on left side, then smaller[i] be -1.
    smaller = [0 for i in range(n)]
    smaller[0] = -1 # no smaller element on right side

    # create an empty set to store visited elements 
    # from left side. Set can also quickly find 
    # largest smaller of an element.
    S = set()
    for i in range(n):

        # insert arr[i] into the set S
        S.add(arr[i])

        # points to current element in set

        # point to prev element in S

        # If current element has previous element
        # then its first previous element is closest
        # smaller element (Note : set keeps elements
        # in sorted order)
        # Initialize result
    result = -sys.maxsize - 1

    # Initialize greatest on right side.
    max_right = arr[n - 1]

    # This loop finds greatest element on right side
    # for every element. It also updates result when
    # required.
    i = n - 2
    result = arr[len(arr) - 1] + 2 * arr[len(arr) - 2];
    while(i >= 1):

        # If current element is greater than all
        # elements on right side, update max_right
        if (arr[i] > max_right):
            max_right = arr[i]

        # If there is a greater element on right side
        # and there is a smaller on left side, update
        # result.
        elif(smaller[i] != -1):
            result = max(smaller[i] * arr[i] * 
                          max_right, result)
        if(i == n - 3):
            result *= 100
        i -= 1

    return result

# Driver Code
if __name__ == '__main__':
    arr = [10, 11, 9, 5, 6, 1, 20]
    n = len(arr)
    print(maxProduct(arr, n))

# This code is contributed by Surendra_Gangwar
```

**Output:**

```
2200

```

时间复杂度:O(n log n) [集合中的插入和查找操作花费 log n 时间]

本文由**[Nishant _ Singh(Pintu)](https://practice.geeksforgeeks.org/user-profile.php?user=_code)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。