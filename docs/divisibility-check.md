# 打印可被至少一个其他元素整除的数组元素

> 原文:[https://www.geeksforgeeks.org/divisibility-check/](https://www.geeksforgeeks.org/divisibility-check/)

给定一个只包含整数的长度为 **N** 的数组，任务是打印数组的特殊数字。这个数组中的一个数被称为**特殊**数，如果它至少能被数组中的另一个数整除。
**例:**

> 输入:1 2 3
> 输出:2 3
> 说明:2 和 3 都可以被 1 整除。
> 输入:2 3 4 6 8 9
> 输出:4 6 8 9
> 说明:2 和 3 不能被任何其他元素整除。元素的其余部分可以被至少一个元素整除。6 能被 2 和 3 整除，4 能被 2 整除，8 能被 2 和 4 整除，9 能被 3 整除。
> 输入:3 5 7 11
> 输出:
> 说明:所有元素都是相对质数，所以没有特殊数字。

一个**简单的解决方案**是遍历所有元素，然后检查每个元素是否可以被任何其他元素整除。这个解决方案的时间复杂度是 O(n<sup>2</sup>)
T5【另一个解决方案，当有很多数值不是很大的元素时效果更好。将所有数组元素存储到哈希中，找出数组中的最大元素，然后向上到最大元素，找出给定数字的倍数，如果数组元素的倍数在哈希中，则该数字可被至少一个数组元素整除。为了删除重复的值，我们将值存储到集合中，因为如果数组有 2、3 和 6，那么只有 6 能被至少一个数组元素整除，2 和 3 都会除以 6，所以 6 将只存储一次。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find special numbers
void divisibilityCheck(int arr[], int n)
{

    // Storing all array elements in a hash
    // and finding maximum element in the array
    unordered_set<int> s;
    int max_ele = INT_MIN;
    for (int i = 0; i < n; i++) {
        s.insert(arr[i]);

        // Update the maximum element of the array
        max_ele = max(max_ele, arr[i]);
    }

    // Traversing the array elements and storing the array
    // multiples that are present in s in res
    unordered_set<int> res;
    for (int i = 0; i < n; i++) {

        // Check for non-zero values only
        if (arr[i] != 0) {

            // Checking the factors of current element
            for (int j = arr[i] * 2; j <= max_ele; j += arr[i]) {

                // If current factor is already part
                // of the array then store it
                if (s.find(j) != s.end())
                    res.insert(j);
            }
        }
    }

    // For non-distinct elmments
    // To store the frequency of elements
    unordered_map<int, int> mp;
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    unordered_map<int, int>::iterator it;
    vector<int> ans;
    for (it = mp.begin(); it != mp.end(); it++) {

        // If frequency is at least 2
        if (it->second >= 2) {
            if (res.find(it->first) == res.end()) {

                // If frequency is greater than 1 and
                // the number is not divisible by
                // any other number
                int val = it->second;

                // Then we push the element number of
                // times it is present in the vector
                while (val--)
                    ans.push_back(it->first);
            }
        }

        // If frequency is greater than 1 and the number
        // is divisible by any other number
        if (res.find(it->first) != res.end()) {
            int val = it->second;

            // Then we push the element number of
            // times it is present in the vector
            while (val--)
                ans.push_back(it->first);
        }
    }

    // Print the elements that are divisible by
    // at least one other element from the array
    for (auto x : ans)
        cout << x << " ";
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 8, 6, 9, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    divisibilityCheck(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find special
// numbers in an array
import java.io.*;
import java.util.*;

class GFG {
    // Function to find
    // special numbers
    static void divisibilityCheck(List<Integer> arr,
                                  int n)
    {
        // Storing all array elements
        // in a hash and finding maximum
        // element in array
        List<Integer> s = new ArrayList<Integer>();
        int max_ele = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            s.add(arr.get(i));

            // finding maximum
            // element of array
            max_ele = Math.max(max_ele,
                               arr.get(i));
        }

        // traversing array element and
        // storing the array multiples
        // that are present in s in res.
        LinkedHashSet<Integer> res = new LinkedHashSet<Integer>();
        for (int i = 0; i < n; i++) {

            // Check for non-zero values only
            if (arr.get(i) != 0)

                // checking the factor
                // of current element
                for (int j = arr.get(i) * 2;
                     j <= max_ele;
                     j += arr.get(i)) {

                    // if factor is already
                    // part of array element
                    // then store it
                    if (s.contains(j))
                        res.add(j);
                }
        }

        // displaying elements that
        // are divisible by at least
        // one other in array
        List<Integer> list = new ArrayList<Integer>(res);
        Collections.reverse(list);

        for (Integer temp : list)
            System.out.print(temp + " ");
    }

    // Driver Code
    public static void main(String args[])
    {
        List<Integer> arr = Arrays.asList(2, 3, 8, 6, 9, 10);
        int n = arr.size();
        divisibilityCheck(arr, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find special numbers
# in an array
import math as mt

# Function to find special numbers
def divisibilityCheck(arr, n):

    # Storing all array elements in a hash
    # and finding maximum element in array
    s = dict()
    max_ele = -10**9
    for i in range(n):
        s[arr[i]] = 1

        # finding maximum element of array
        max_ele = max(max_ele, arr[i])

    # traversing array element and storing
    # the array multiples that are present
    # in s in res.
    res = dict()
    for i in range(n):

        # Check for non-zero values only
        if (arr[i] != 0):

            # checking the factor of current element
            for j in range(arr[i] * 2,
                           max_ele + 1, arr[i]):

                # if factor is already part of
                # array element then store it
                if (j in s.keys()):
                    res[j] = 1

    # displaying elements that are divisible
    # by at least one other in array
    for x in res:
        print(x, end = " ")

# Driver code
arr = [ 2, 3, 8, 6, 9, 10]
n = len(arr)
divisibilityCheck(arr, n)

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// C# program to find special
// numbers in an array
using System;
using System.Linq;
using System.Collections.Generic;

class GFG {
    // Function to find
    // special numbers
    static void divisibilityCheck(List<int> arr,
                                  int n)
    {
        // Storing all array elements
        // in a hash and finding maximum
        // element in array
        List<int> s = new List<int>();
        int max_ele = Int32.MinValue;
        for (int i = 0; i < n; i++) {
            s.Add(arr[i]);

            // finding maximum element of array
            max_ele = Math.Max(max_ele,
                               arr[i]);
        }

        // traversing array element and
        // storing the array multiples
        // that are present in s in res.
        HashSet<int> res = new HashSet<int>();
        for (int i = 0; i < n; i++) {

            // Check for non-zero values only
            if (arr[i] != 0)

                // checking the factor
                // of current element
                for (int j = arr[i] * 2; j <= max_ele;
                     j += arr[i]) {

                    // if factor is already part
                    // of array element then store it
                    if (s.Contains(j))
                        res.Add(j);
                }
        }
        // displaying elements that
        // are divisible by at least
        // one other in array
        foreach(int i in res.Reverse())
            Console.Write(i + " ");
    }

    // Driver Code
    static void Main()
    {
        List<int> arr = new List<int>() { 2, 3, 8,
                                              6, 9, 10 };
        int n = arr.Count;
        divisibilityCheck(arr, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find special numbers
function divisibilityCheck(arr, n) {

    // Storing all array elements in a hash
    // and finding maximum element in the array
    let s = new Set();
    let max_ele = Number.MIN_SAFE_INTEGER;
    for (let i = 0; i < n; i++) {
        s.add(arr[i]);

        // Update the maximum element of the array
        max_ele = Math.max(max_ele, arr[i]);
    }

    // Traversing the array elements and storing the array
    // multiples that are present in s in res
    let res = new Set();
    for (let i = 0; i < n; i++) {

        // Check for non-zero values only
        if (arr[i] != 0) {

            // Checking the factors of current element
            for (let j = arr[i] * 2; j <= max_ele; j += arr[i]) {

                // If current factor is already part
                // of the array then store it
                if (s.has(j))
                    res.add(j);
            }
        }
    }

    // For non-distinct elmments
    // To store the frequency of elements
    let mp = new Map();
    for (let i = 0; i < n; i++) {
        if (mp.has(arr[i])) {
            mp.set(arr[i], mp.get(arr[i]) + 1)
        } else {
            mp.set(arr[i], 1)
        }
    }

    let ans = [];
    for (let it of mp) {

        // If frequency is at least 2
        if (it[1] >= 2) {
            if (res.has(it[0])) {

                // If frequency is greater than 1 and
                // the number is not divisible by
                // any other number
                let val = it[1];

                // Then we push the element number of
                // times it is present in the vector
                while (val--)
                    ans.push(it[0]);
            }
        }

        // If frequency is greater than 1 and the number
        // is divisible by any other number
        if (res.has(it[0])) {
            let val = it[1];

            // Then we push the element number of
            // times it is present in the vector
            while (val--)
                ans.push(it[0]);
        }
    }

    // Print the elements that are divisible by
    // at least one other element from the array
    for (let x of ans.sort((a, b) => a - b))
        document.write(x + " ");
}

// Driver code

let arr = [2, 3, 8, 6, 9, 10];
let n = arr.length

divisibilityCheck(arr, n);

</script>
```

**Output:** 

```
6 8 9 10
```

**注意:**如果需要按排序顺序打印结果，可以用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)代替[无序 _ 设置](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)。