# 合并不同大小的 K 个排序数组|(分治法)

> 原文:[https://www . geeksforgeeks . org/merge-k-sorted-不同大小的数组-分治法/](https://www.geeksforgeeks.org/merge-k-sorted-arrays-of-different-sizes-divide-and-conquer-approach/)

给定不同长度的 **k** 排序数组，将它们合并成一个数组，这样合并后的数组也被排序。
**例:**

```
Input : {{3, 13}, 
        {8, 10, 11}
        {9, 15}}
Output : {3, 8, 9, 10, 11, 13, 15}

Input : {{1, 5}, 
         {2, 3, 4}}
Output : {1, 2, 3, 4, 5}
```

设 S 为所有数组中元素的总数。
**简单方法**:一个简单的方法就是把数组一个接一个的追加，然后排序。这种情况下的时间复杂度为 **O( S * log(S))** 。
**有效方法**:一个有效的解决方案是在每一步取成对的数组。然后使用[合并两个排序数组](https://www.geeksforgeeks.org/merge-two-sorted-arrays/)的双指针技术合并对。因此，在合并所有对之后，阵列的数量将减少一半。
我们将继续这样做，直到剩余阵列的数量不变成 1。因此，所需步骤的数量将是顺序日志(k)，并且由于在每个步骤中，我们花费 O(S)时间来执行合并操作，因此该方法的总时间复杂度变为 **O(S * log(k))** 。
我们已经讨论过[合并相同大小的 K 个排序数组](https://www.geeksforgeeks.org/merge-k-sorted-arrays-set-3-using-divide-and-conquer-approach/)的方法。
由于在这个问题中数组的大小不同，我们将使用动态数组(例如:C++中的 vector 或 Java 中的 arraylist)，因为它们显著减少了行数和工作量。
以下是上述方法的实施:

## C++

```
// C++ program to merge K sorted arrays of
// different arrays

#include <iostream>
#include <vector>
using namespace std;

// Function to merge two arrays
vector<int> mergeTwoArrays(vector<int> l, vector<int> r)
{
    // array to store the result
    // after merging l and r
    vector<int> ret;

    // variables to store the current
    // pointers for l and r
    int l_in = 0, r_in = 0;

    // loop to merge l and r using two pointer
    while (l_in + r_in < l.size() + r.size()) {
        if (l_in != l.size() && (r_in == r.size() || l[l_in] < r[r_in])) {
            ret.push_back(l[l_in]);
            l_in++;
        }
        else {
            ret.push_back(r[r_in]);
            r_in++;
        }
    }

    return ret;
}

// Function to merge all the arrays
vector<int> mergeArrays(vector<vector<int> > arr)
{
    // 2D-array to store the results of
    // a step temporarily
    vector<vector<int> > arr_s;

    // Loop to make pairs of arrays and merge them
    while (arr.size() != 1) {

        // To clear the data of previous steps
        arr_s.clear();

        for (int i = 0; i < arr.size(); i += 2) {
            if (i == arr.size() - 1)
                arr_s.push_back(arr[i]);

            else
                arr_s.push_back(mergeTwoArrays(arr[i],
                                               arr[i + 1]));
        }

        arr = arr_s;
    }

    // Returning the required output array
    return arr[0];
}

// Driver Code
int main()
{
    // Input arrays
    vector<vector<int> > arr{ { 3, 13 },
                              { 8, 10, 11 },
                              { 9, 15 } };
    // Merged sorted array
    vector<int> output = mergeArrays(arr);

    for (int i = 0; i < output.size(); i++)
        cout << output[i] << " ";

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to merge K sorted
# arrays of different arrays

# Function to merge two arrays
def mergeTwoArrays(l, r):

    # array to store the result
    # after merging l and r
    ret = []

    # variables to store the current
    # pointers for l and r
    l_in, r_in = 0, 0

    # loop to merge l and r using two pointer
    while l_in + r_in < len(l) + len(r):
        if (l_in != len(l) and
           (r_in == len(r) or
            l[l_in] < r[r_in])):

            ret.append(l[l_in])
            l_in += 1

        else:
            ret.append(r[r_in])
            r_in += 1

    return ret

# Function to merge all the arrays
def mergeArrays(arr):

    # 2D-array to store the results
    # of a step temporarily
    arr_s = []

    # Loop to make pairs of arrays
    # and merge them
    while len(arr) != 1:

        # To clear the data of previous steps
        arr_s[:] = []

        for i in range(0, len(arr), 2):
            if i == len(arr) - 1:
                arr_s.append(arr[i])

            else:
                arr_s.append(mergeTwoArrays(arr[i],
                                            arr[i + 1]))

        arr = arr_s[:]

    # Returning the required output array
    return arr[0]

# Driver Code
if __name__ == "__main__":

    # Input arrays
    arr = [[3, 13],
        [8, 10, 11],
        [9, 15]]

    # Merged sorted array
    output = mergeArrays(arr)

    for i in range(0, len(output)):
        print(output[i], end = " ")

# This code is contributed by Rituraj Jain
```

## java 描述语言

```
<script>

// Javascript program to merge K sorted arrays of
// different arrays

// Function to merge two arrays
function mergeTwoArrays(l, r)
{

    // array to store the result
    // after merging l and r
    var ret = [];

    // variables to store the current
    // pointers for l and r
    var l_in = 0, r_in = 0;

    // loop to merge l and r using two pointer
    while (l_in + r_in < l.length + r.length) {
        if (l_in != l.length && (r_in == r.length || l[l_in] < r[r_in])) {
            ret.push(l[l_in]);
            l_in++;
        }
        else {
            ret.push(r[r_in]);
            r_in++;
        }
    }

    return ret;
}

// Function to merge all the arrays
function mergeArrays(arr)
{
    // 2D-array to store the results of
    // a step temporarily
    var arr_s = [];

    // Loop to make pairs of arrays and merge them
    while (arr.length != 1) {

        // To clear the data of previous steps
        arr_s = [];

        for (var i = 0; i < arr.length; i += 2) {
            if (i == arr.length - 1)
                arr_s.push(arr[i]);

            else
                arr_s.push(mergeTwoArrays(arr[i],
                                               arr[i + 1]));
        }

        arr = arr_s;
    }

    // Returning the required output array
    return arr[0];
}

// Driver Code
// Input arrays
var arr = [ [ 3, 13 ],
                          [ 8, 10, 11 ],
                          [ 9, 15 ] ];
// Merged sorted array
var output = mergeArrays(arr);
for (var i = 0; i < output.length; i++)
    document.write(output[i] + " ");

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
3 8 9 10 11 13 15
```

**时间复杂度:**O(S * logK)
T3】辅助空间: O(logK)
注意，存在一个[更好的使用堆(或优先级队列)](https://www.geeksforgeeks.org/merge-k-sorted-arrays-set-2-different-sized-arrays/)的解决方案。基于堆的解决方案的时间复杂度是 O(N Log k)，其中 N 是所有 K 个数组中的元素总数。