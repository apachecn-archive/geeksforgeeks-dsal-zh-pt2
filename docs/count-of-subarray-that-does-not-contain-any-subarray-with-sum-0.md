# 不包含任何和为 0 的子阵列的子阵列计数

> 原文:[https://www . geeksforgeeks . org/不包含任何和为 0 的子数组的子数组计数/](https://www.geeksforgeeks.org/count-of-subarray-that-does-not-contain-any-subarray-with-sum-0/)

给定一个数组 **arr** ，任务是找出给定数组中不包含任何元素之和等于零的子数组的子数组总数。所有的数组元素都是**不同的。**
**例:**

> **输入:** arr = {2，4，-6}
> **输出:** 5
> **解释:**
> 有 5 个子阵不包含任何元素和等于零的子阵:[2]，[4]，[-6]，[2，4]，[4，-6]
> **输入:** arr = {10，-10，10}
> **输出:** 3 【T15

**进场:**

1.  首先将数组的所有元素存储为其前一个元素的和。

2.  现在取两个指针，增加第二个指针，并在没有遇到相同元素的情况下将值存储在映射中。

3.  如果遇到一个已经存在于映射中的元素，这意味着在两个元素和等于 0 的指针之间存在一个子数组。

4.  现在增加第一个指针，当两个相同的元素存在时，从地图中移除该元素。

5.  将答案存储在变量中，最后返回。

**以下是上述方法的实施:**

## C++

```
// C++ program to Count the no of subarray
// which do not contain any subarray
// whose sum of elements is equal to zero

#include <bits/stdc++.h>
using namespace std;

// Function that print the number of
// subarrays which do not contain any subarray
// whose elements sum is equal to 0
void numberOfSubarrays(int arr[], int n)
{
    vector<int> v(n + 1);
    v[0] = 0;

    // Storing each element as sum
    // of its previous element
    for (int i = 0; i < n; i++) {
        v[i + 1] = v[i] + arr[i];
    }

    map<int, int> mp;

    int begin = 0, end = 0, answer = 0;

    mp[0] = 1;

    while (begin < n) {

        while (end < n
               && mp.find(v[end + 1])
                      == mp.end()) {
            end++;
            mp[v[end]] = 1;
        }

        // Check if another same element found
        // this means a subarray exist between
        // end and begin whose sum
        // of elements is equal to 0
        answer = answer + end - begin;

        // Erase beginning element from map
        mp.erase(v[begin]);

        // Increase begin
        begin++;
    }

    // Print the result
    cout << answer << endl;
}

// Driver Code
int main()
{

    int arr[] = { 2, 4, -6 };
    int size = sizeof(arr) / sizeof(arr[0]);

    numberOfSubarrays(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count the no of subarray
// which do not contain any subarray
// whose sum of elements is equal to zero
import java.util.*;

class GFG{

// Function that print the number of
// subarrays which do not contain any subarray
// whose elements sum is equal to 0
static void numberOfSubarrays(int arr[], int n)
{
    int []v = new int[n + 1];
    v[0] = 0;

    // Storing each element as sum
    // of its previous element
    for (int i = 0; i < n; i++) {
        v[i + 1] = v[i] + arr[i];
    }

    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    int begin = 0, end = 0, answer = 0;

    mp.put(0, 1);

    while (begin < n) {

        while (end < n
               && !mp.containsKey(v[end + 1])) {
            end++;
            mp.put(v[end],  1);
        }

        // Check if another same element found
        // this means a subarray exist between
        // end and begin whose sum
        // of elements is equal to 0
        answer = answer + end - begin;

        // Erase beginning element from map
        mp.remove(v[begin]);

        // Increase begin
        begin++;
    }

    // Print the result
    System.out.print(answer +"\n");
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 2, 4, -6 };
    int size = arr.length;

    numberOfSubarrays(arr, size);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 program to Count the no of subarray
# which do not contain any subarray
# whose sum of elements is equal to zero

# Function that print the number of
# subarrays which do not contain any subarray
# whose elements sum is equal to 0
def numberOfSubarrays(arr, n):

    v = [0]*(n + 1)

    # Storing each element as sum
    # of its previous element
    for i in range( n):
        v[i + 1] = v[i] + arr[i]

    mp = {}

    begin, end, answer = 0 , 0 , 0

    mp[0] = 1

    while (begin < n):

        while (end < n
            and (v[end + 1]) not in mp):
            end += 1
            mp[v[end]] = 1

        # Check if another same element found
        # this means a subarray exist between
        # end and begin whose sum
        # of elements is equal to 0
        answer = answer + end - begin

        # Erase beginning element from map
        del mp[v[begin]]

        # Increase begin
        begin += 1

    # Print the result
    print(answer)

# Driver Code
if __name__ == "__main__":

    arr = [ 2, 4, -6 ]
    size = len(arr)
    numberOfSubarrays(arr, size)

# This code is contributed by chitranayal
```

## C#

```
// C# program to Count the no of subarray
// which do not contain any subarray
// whose sum of elements is equal to zero
using System;
using System.Collections.Generic;

class GFG{

// Function that print the number of
// subarrays which do not contain any subarray
// whose elements sum is equal to 0
static void numberOfSubarrays(int []arr, int n)
{
    int []v = new int[n + 1];
    v[0] = 0;

    // Storing each element as sum
    // of its previous element
    for (int i = 0; i < n; i++) {
        v[i + 1] = v[i] + arr[i];
    }

    Dictionary<int,int> mp = new Dictionary<int,int>();

    int begin = 0, end = 0, answer = 0;

    mp.Add(0, 1);

    while (begin < n) {

        while (end < n
               && !mp.ContainsKey(v[end + 1])) {
            end++;
            mp.Add(v[end],  1);
        }

        // Check if another same element found
        // this means a subarray exist between
        // end and begin whose sum
        // of elements is equal to 0
        answer = answer + end - begin;

        // Erase beginning element from map
        mp.Remove(v[begin]);

        // Increase begin
        begin++;
    }

    // Print the result
    Console.Write(answer +"\n");
}

// Driver Code
public static void Main(String[] args)
{

    int []arr = { 2, 4, -6 };
    int size = arr.Length;

    numberOfSubarrays(arr, size);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to Count the no of subarray
// which do not contain any subarray
// whose sum of elements is equal to zero

// Function that print the number of
// subarrays which do not contain any subarray
// whose elements sum is equal to 0
function numberOfSubarrays(arr, n)
{
    let v = new Array(n + 1);
    v[0] = 0;

    // Storing each element as sum
    // of its previous element
    for (let i = 0; i < n; i++) {
        v[i + 1] = v[i] + arr[i];
    }

    let mp = new Map();

    let begin = 0, end = 0, answer = 0;

    mp.set(0, 1);

    while (begin < n) {

        while (end < n && !mp.has(v[end + 1])) {
            end++;
            mp.set(v[end], 1);
        }

        // Check if another same element found
        // this means a subarray exist between
        // end and begin whose sum
        // of elements is equal to 0
        answer = answer + end - begin;

        // Erase beginning element from map
        mp.clear();

        // Increase begin
        begin++;
    }

    // Print the result
    document.write(answer + "<br>");
}

// Driver Code

let arr = [ 2, 4, -6 ];
let size = arr.length;

numberOfSubarrays(arr, size);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
5
```