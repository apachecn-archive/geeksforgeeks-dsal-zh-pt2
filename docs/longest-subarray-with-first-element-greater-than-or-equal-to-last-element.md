# 第一个元素大于或等于最后一个元素的最长子阵列

> 原文:[https://www . geesforgeks . org/第一个元素大于或等于最后一个元素的最长子数组/](https://www.geeksforgeeks.org/longest-subarray-with-first-element-greater-than-or-equal-to-last-element/)

给定数组 arr[0..n-1]的 n 个整数，求最大长度子阵列，使其第一个元素大于或等于子阵列的最后一个元素。

**示例:**

```
Input : arr[] = {-5, -1, 7, 5, 1, -2}
Output : 5
Explanation : Subarray {-1, 7, 5, 1, -2} forms maximum 
length subarray with its first element greater than last.

Input : arr[] = {1, 5, 7}
Output : 1
```

**天真的方法**是对子阵列的每个可能的开始和结束元素使用两个嵌套循环，如果它满足条件，则相应地更新答案。

*时间复杂性–o(n^2)*

更好的方法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。在这种方法中，对于阵列中的每个元素，我们最大化以该元素结束的子阵列的长度。然后我们取所有长度的最大值。

我们将使用另一个数组作为搜索空间来选择的起始元素。当我们遍历数组时，如果元素大于搜索空间中所有前面的元素，我们将继续在其中添加元素。
这里的关键观察是，只有当一个元素大于搜索空间的所有元素时，我们才会将其添加到搜索空间中，因为如果该元素低于任何其他元素，则它永远不能被选择为最大长度子阵列的第一个元素，因为我们会有更好的选择。

由于搜索空间总是以递增的顺序排序，我们只需要将数组的当前元素与搜索空间的最后一个元素进行比较，当且仅当它大于最后一个元素时，我们才将其添加到搜索空间中，否则不会。

下面是上述方法的实现

## C++

```
// CPP program to find length of the longest
// array with first element smaller than or
// equal to last element.
#include <algorithm>
#include <iostream>
using namespace std;

// Search function for searching the first element of the
// subarray which is greater or equal to the last element(num)
int binarySearch(int* searchSpace, int s, int e, int num)
{
    int ans;

    while (s <= e) {
        int mid = (s + e) / 2;

        if (searchSpace[mid] >= num) {
            ans = mid;
            e = mid - 1;
        }
        else
            s = mid + 1;
    }

    return ans;
}

// Returns length of the longest array with first
// element smaller than the last element.
int longestSubArr(int* arr, int n)
{
    // Search space for the potential first elements.
    int searchSpace[n];

    // It will store the Indexes of the elements
    // of search space in the original array.
    int index[n];

    // Initially the search space is empty.
    int j = 0;
    int ans = 0;

    for (int i = 0; i < n; ++i) {

        // We will add an ith element in the search
        // space if the search space is empty or if
        // the ith element is greater than the last
        // element of the search space.
        if (j == 0 or searchSpace[j - 1] < arr[i]) {
            searchSpace[j] = arr[i];
            index[j] = i;
            j++;
        }

        // we will search for the index first element in the
        // search space and we will use it find the
        // index of it in the original array.
        int idx = binarySearch(searchSpace, 0, j - 1, arr[i]);

        // Update the answer if the length of the subarray is
        // greater than the previously calculated lengths.
        ans = max(ans, i - index[idx] + 1);
    }
    return ans;
}

int main(int argc, char const* argv[])
{
    int arr[] = { -5, -1, 7, 5, 1, -2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << longestSubArr(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length
// of the longest array with
// first element smaller than
// or equal to last element.
class GFG
{

// Search function for searching
// the first element of the
// subarray which is greater or
// equal to the last element(num)
static int binarySearch(int []searchSpace, int s,
                        int e, int num)
{
int ans = 0;

while (s <= e)
{
    int mid = (s + e) / 2;

    if (searchSpace[mid] >= num)
    {
        ans = mid;
        e = mid - 1;
    }
    else
        s = mid + 1;
}

return ans;
}

// Returns length of the longest
// array with first element smaller
// than the last element.
static int longestSubArr(int []arr, int n)
{
// Search space for the
// potential first elements.
int []searchSpace = new int[n];

// It will store the Indexes
// of the elements of search
// space in the original array.
int []index = new int[n];

// Initially the search
// space is empty.
int j = 0;
int ans = 0;

for (int i = 0; i < n; ++i)
{

    // We will add an ith element
    // in the search space if the
    // search space is empty or if
    // the ith element is greater
    // than the last element of
    // the search space.
    if (j == 0 || searchSpace[j - 1] < arr[i])
    {
        searchSpace[j] = arr[i];
        index[j] = i;
        j++;
    }

    // we will search for the index
    // first element in the search
    // space and we will use it find
    // the index of it in the original array.
    int idx = binarySearch(searchSpace, 0,
                           j - 1, arr[i]);

    // Update the answer if the
    // length of the subarray is
    // greater than the previously
    // calculated lengths.
    ans = Math.max(ans, i - index[idx] + 1);
}
return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { -5, -1, 7, 5, 1, -2 };
    int n = arr.length;
    System.out.println(longestSubArr(arr, n));
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to find
# length of the longest array
# with first element smaller
# than or equal to last element.

# Search function for searching
# the first element of the
# subarray which is greater or
# equal to the last element(num)
def binarySearch(searchSpace, s, e, num):

    while (s <= e):
        mid = (s + e) // 2

        if searchSpace[mid] >= num :
            ans = mid
            e = mid - 1

        else:
            s = mid + 1

    return ans

# Returns length of the longest
# array with first element
# smaller than the last element.
def longestSubArr(arr, n):

    # Search space for the
    # potential first elements.
    searchSpace = [None] * n

    # It will store the Indexes
    # of the elements of search
    # space in the original array.
    index = [None] * n

    # Initially the search
    # space is empty.
    j = 0
    ans = 0

    for i in range(n):

        # We will add an ith element
        # in the search space if the
        # search space is empty or if
        # the ith element is greater
        # than the last element of
        # the search space.
        if (j == 0 or searchSpace[j - 1] < arr[i]) :
            searchSpace[j] = arr[i]
            index[j] = i
            j += 1

        # we will search for the index
        # first element in the search
        # space and we will use it
        # find the index of it in the
        # original array.
        idx = binarySearch(searchSpace, 0,
                           j - 1, arr[i])

        # Update the answer if the length
        # of the subarray is greater than
        # the previously calculated lengths.
        ans = max(ans, i - index[idx] + 1)

    return ans

if __name__ == "__main__":
    arr = [ -5, -1, 7, 5, 1, -2 ]
    n = len(arr)
    print(longestSubArr(arr, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find length
// of the longest array with
// first element smaller than
// or equal to last element.
using System;

class GFG
{

// Search function for searching
// the first element of the
// subarray which is greater or
// equal to the last element(num)
static int binarySearch(int[] searchSpace,
                        int s, int e, int num)
{
int ans = 0;

while (s <= e)
{
    int mid = (s + e) / 2;

    if (searchSpace[mid] >= num)
    {
        ans = mid;
        e = mid - 1;
    }
    else
        s = mid + 1;
}

return ans;
}

// Returns length of the longest
// array with first element smaller
// than the last element.
static int longestSubArr(int[] arr, int n)
{

// Search space for the
// potential first elements.
int[] searchSpace = new int[n];

// It will store the Indexes
// of the elements of search
// space in the original array.
int[] index = new int[n];

// Initially the search
// space is empty.
int j = 0;
int ans = 0;

for (int i = 0; i < n; ++i)
{

    // We will add an ith element
    // in the search space if the
    // search space is empty or if
    // the ith element is greater
    // than the last element of
    // the search space.
    if (j == 0 || searchSpace[j - 1] < arr[i])
    {
        searchSpace[j] = arr[i];
        index[j] = i;
        j++;
    }

    // we will search for the index
    // first element in the search
    // space and we will use it find the
    // index of it in the original array.
    int idx = binarySearch(searchSpace, 0,
                           j - 1, arr[i]);

    // Update the answer if the
    // length of the subarray is
    // greater than the previously
    // calculated lengths.
    ans = Math.Max(ans, i - index[idx] + 1);
}
return ans;
}

// Driver code
public static void Main()
{
    int[] arr = { -5, -1, 7, 5, 1, -2 };
    int n = arr.Length;
    Console.Write(longestSubArr(arr, n));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length
// of the longest array with
// first element smaller than
// or equal to last element.

// Search function for searching
// the first element of the
// subarray which is greater or
// equal to the last element(num)
function binarySearch($searchSpace,
                      $s, $e, $num)
{
    $ans = 0;
    while ($s <= $e)
    {
        $mid = ($s + $e) / 2;

        if ($searchSpace[$mid] >= $num)
        {
            $ans = $mid;
            $e = $mid - 1;
        }
        else
        {
            $s = $mid + 1;
        }
    }

    return $ans;
}

// Returns length of the longest
// array with first element smaller
// than the last element.
function longestSubArr(&$arr, $n)
{
    // Search space for the
    // potential first elements.

    // It will store the Indexes
    // of the elements of search
    // space in the original array.

    // Initially the search
    // space is empty.
    $j = 0;
    $ans = 0;
    for ($i = 0; $i < $n; ++$i)
    {

        // We will add an ith element
        // in the search space if the
        // search space is empty or if
        // the ith element is greater
        // than the last element of the
        // search space.
        if ($j == 0 or
            $searchSpace[$j - 1] < $arr[$i])
        {
            $searchSpace[$j] = $arr[$i];
            $index[$j] = $i;
            $j++;
        }

        // we will search for the index
        // first element in the search
        // space and we will use it find
        // the index of it in the original
        // array.
        $idx = binarySearch($searchSpace, 0,
                            $j - 1, $arr[$i]);

        // Update the answer if the length
        // of the subarray is greater than
        // the previously calculated lengths.
        $ans = max($ans, $i - $index[$idx] + 1);
    }
    return $ans;
}

// Driver code
$arr = array(-5, -1, 7, 5, 1, -2);
$n = sizeof($arr);
echo (longestSubArr($arr, $n)) ;

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find length
// of the longest array with
// first element smaller than
// or equal to last element.

// Search function for searching
// the first element of the
// subarray which is greater or
// equal to the last element(num)
function binarySearch(searchSpace, s, e, num)
{
    let ans = 0;

    while (s <= e)
    {
        let mid = Math.floor((s + e) / 2);

        if (searchSpace[mid] >= num)
        {
            ans = mid;
            e = mid - 1;
        }
        else
            s = mid + 1;
    }
    return ans;
}

// Returns length of the longest
// array with first element smaller
// than the last element.
function longestSubArr(arr, n)
{

    // Search space for the
    // potential first elements.
    let searchSpace = new Array(n);

    // It will store the Indexes
    // of the elements of search
    // space in the original array.
    let index = new Array(n);

    // Initially the search
    // space is empty.
    let j = 0;
    let ans = 0;

    for(let i = 0; i < n; ++i)
    {

        // We will add an ith element
        // in the search space if the
        // search space is empty or if
        // the ith element is greater
        // than the last element of
        // the search space.
        if (j == 0 || searchSpace[j - 1] < arr[i])
        {
            searchSpace[j] = arr[i];
            index[j] = i;
            j++;
        }

        // We will search for the index
        // first element in the search
        // space and we will use it find
        // the index of it in the original array.
        let idx = binarySearch(searchSpace, 0,
                               j - 1, arr[i]);

        // Update the answer if the
        // length of the subarray is
        // greater than the previously
        // calculated lengths.
        ans = Math.max(ans, i - index[idx] + 1);
    }
    return ans;   
}

// Driver code
let arr = [ -5, -1, 7, 5, 1, -2 ];
let n = arr.length;

document.write(longestSubArr(arr, n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出**

```
5
```

*时间复杂度–( N * log N)*
二分搜索法函数取 Log N 的时间，它将被调用 N 次。