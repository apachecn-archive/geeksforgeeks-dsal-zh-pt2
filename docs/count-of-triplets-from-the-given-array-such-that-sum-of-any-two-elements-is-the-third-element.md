# 给定数组中三元组的计数，任何两个元素的和就是第三个元素

> 原文:[https://www . geesforgeks . org/从给定数组中计算三元组，这样任何两个元素的和就是第三个元素/](https://www.geeksforgeeks.org/count-of-triplets-from-the-given-array-such-that-sum-of-any-two-elements-is-the-third-element/)

给定一个未排序的数组 **arr** ，任务是找到不同三元组的计数，其中任意两个元素的和是第三个元素。

**示例:**

> **输入:** arr[] = {1，3，4，15，19}
> **输出:** 2
> **解释:**
> 在给定的数组中有两个三元组，这样两个元素的和等于第三个元素:{{1，3，4}，{4，15，19}}
> 
> **输入:** arr[] = {7，2，5，4，3，6，1，9，10，12 }
> T3】输出: 18

**进场:**

*   给定数组排序
*   为数组创建一个[散列图](https://www.geeksforgeeks.org/hashing-data-structure/)，以检查特定元素是否存在。
*   使用两个[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)迭代数组，以选择不同位置的任意两个元素，并检查这两个元素的总和是否在 O(1)时间内出现在哈希映射中。
*   如果哈希映射中存在这两个元素的总和，则增加三元组的计数。

下面是上述方法的实现:

## C++

```
// C++ Implementation to find the
// Count the triplets in which sum
// of two elements is the third element
#include <bits/stdc++.h>

using namespace std;

// Function to find the count
// the triplets in which sum
// of two elements is the third element
int triplets(vector<int>arr)
{

    // Dictionary to check a element is
    // present or not in array
    map<int, int> k;
    map<pair<int, int>, int> mpp;

    // List to check for
    // duplicates of Triplets
    vector<vector<int >> ssd;

    // Set initial count to zero
    int count = 0;

    // Sort the array
    sort(arr.begin(),arr.end());

    int i = 0;
    while (i < arr.size())
    {

        // Add all the values as key
        // value pairs to the dictionary
        if (k.find(arr[i]) == k.end())
            k[arr[i]] = 1;

        i += 1;
    }

    // Loop to choose two elements
    int j = 0;
    while (j < arr.size() - 1)
    {

        int q = j + 1;
        while (q < arr.size())
        {

            // Check for the sum and duplicate
            if ( k.find(arr[j] + arr[q]) != k.end() and
                mpp[{arr[j], arr[q]}] != arr[j] + arr[q])
            {

                count += 1;

                ssd.push_back({arr[j], arr[q], arr[j] + arr[q]});
                mpp[{arr[j], arr[q]}] = arr[j] + arr[q];
            }

            q += 1;
        }
        j += 1;
    }
    return count;
}

// Driver Code
int main()
{
    vector<int>arr = {7, 2, 5, 4, 3, 6, 1, 9, 10, 12};
    int count = triplets(arr);
    printf("%d",count);
    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Count the triplets in which sum
// of two elements is the third element
import java.io.*;
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;

class GFG{

// Function to find the count the triplets
// in which sum of two elements is the third element
public static int triplets(ArrayList<Integer> arr)
{

      // Dictionary to check a element is
       // present or not in array
    HashSet<Integer> k = new HashSet<>();

      // List to check for
    // duplicates of Triplets
    HashSet<ArrayList<Integer>> ssd = new HashSet<>();

      // Set initial count to zero
    int count = 0;

    // Sort the array
    Collections.sort(arr);

    int i = 0;

      // Add all the values as key
    // value pairs to the dictionary
    while (i < arr.size())
    {
        if (!k.contains(arr.get(i)))
        {
            k.add(arr.get(i));
        }
        i += 1;
    }
    int j = 0;

    // Loop to choose two elements
    while (j < arr.size() - 1)
    {
        int q = j + 1;

          // Check for the sum and duplicate
        while (q < arr.size())
        {
            ArrayList<Integer> trip = new ArrayList<>();
            trip.add(arr.get(j));
            trip.add(arr.get(q));
            trip.add(arr.get(j) + arr.get(q));

            if (k.contains(arr.get(j) + arr.get(q)) &&
                !ssd.contains(trip))
            {
                count += 1;
                ArrayList<Integer> nums = new ArrayList<>();
                nums.add(arr.get(j));
                nums.add(arr.get(q));
                nums.add(arr.get(j) + arr.get(q));
                ssd.add(nums);
            }
            q += 1;
        }
        j += 1;
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    ArrayList<Integer> arr = new ArrayList<>();
    arr.add(7);
    arr.add(2);
    arr.add(5);
    arr.add(4);
    arr.add(3);
    arr.add(6);
    arr.add(1);
    arr.add(9);
    arr.add(10);
    arr.add(12);

    int count = triplets(arr);

    System.out.println(count);
}
}

// This code is contributed by aditya7409
```

## 蟒蛇 3

```
# Python3 Implementation to find the
# Count the triplets in which sum
# of two elements is the third element

# Function to find the count
# the triplets in which sum
# of two elements is the third element
def triplets(arr):

    # Dictionary to check a element is
    # present or not in array
    k = set()

    # List to check for
    # duplicates of Triplets
    ssd = []

    # Set initial count to zero
    count = 0

    # Sort the array
    arr.sort()

    i = 0
    while i < len(arr):

        # Add all the values as key
        # value pairs to the dictionary
        if arr[i] not in k:
            k.add(arr[i])

        i += 1

    # Loop to choose two elements
    j = 0
    while j < len(arr) - 1:

        q = j + 1
        while q < len(arr):

            # Check for the sum and duplicate
            if arr[j] + arr[q] in k and\
               [arr[j], arr[q], arr[j] + arr[q]] not in ssd:

                count += 1

                ssd.append([arr[j], arr[q], arr[j] + arr[q]])

            q += 1
        j += 1

    return count

# Driver Code
if __name__ == "__main__":
    arr = [7, 2, 5, 4, 3, 6, 1, 9, 10, 12]
    count = triplets(arr)
    print(count)
```

## C#

```
// C# Implementation to find the
// Count the triplets in which sum
// of two elements is the third element
using System;
using System.Collections.Generic;
class GFG {

  // Function to find the count
  // the triplets in which sum
  // of two elements is the third element
  static int triplets(List<int> arr)
  {

    // Dictionary to check a element is
    // present or not in array
    Dictionary<int, int> k = new Dictionary<int, int>();
    Dictionary<Tuple<int, int>, int> mpp = new Dictionary<Tuple<int, int>, int>();

    // List to check for
    // duplicates of Triplets
    List<List<int>> ssd = new List<List<int>>();

    // Set initial count to zero
    int count = 0;

    // Sort the array
    arr.Sort();

    int i = 0;
    while (i < arr.Count)
    {

      // Add all the values as key
      // value pairs to the dictionary
      if (!k.ContainsKey(arr[i]))
        k[arr[i]] = 1;

      i += 1;
    }

    // Loop to choose two elements
    int j = 0;
    while (j < arr.Count - 1)
    {
      int q = j + 1;
      while (q < arr.Count)
      {

        // Check for the sum and duplicate
        if(!k.ContainsKey(arr[j] + arr[q]))
        {
          q += 1;
          continue;
        }
        if (mpp.ContainsKey(new Tuple<int,int>(arr[j], arr[q])) &&
            mpp[new Tuple<int,int>(arr[j], arr[q])] != (arr[j] + arr[q]))
        {
          count += 1;   
          ssd.Add(new List<int>(new int[]{arr[j], arr[q], arr[j] + arr[q]}));
          mpp[new Tuple<int,int>(arr[j], arr[q])] = arr[j] + arr[q];
        }
        else{
          count += 1;
          ssd.Add(new List<int>(new int[]{arr[j], arr[q], arr[j] + arr[q]}));
          mpp[new Tuple<int,int>(arr[j], arr[q])] = arr[j] + arr[q];
        }    
        q += 1;
      }
      j += 1;
    }
    return count;
  }

  // Driver code
  static void Main()
  {
    List<int> arr = new List<int>(new int[]{7, 2, 5, 4, 3, 6, 1, 9, 10, 12});
    int count = triplets(arr);
    Console.Write(count);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// Count the triplets in which sum
// of two elements is the third element

// Function to find the count the triplets
// in which sum of two elements is the third element
function triplets(arr)
{

    // Dictionary to check a element is
    // present or not in array
    let k = new Set();

    // List to check for
    // duplicates of Triplets
    let ssd = new Set();

    // Set initial count to zero
    let count = 0;

    // Sort the array
    arr.sort((a, b) => a - b);

    let i = 0;

      // Add all the values as key
    // value pairs to the dictionary
    while (i < arr.length)
    {
        if (!k.has(arr[i]))
        {
            k.add(arr[i]);
        }
        i += 1;
    }
    let j = 0;

    // Loop to choose two elements
    while (j < arr.length - 1)
    {
        let q = j + 1;

        // Check for the sum and duplicate
        while (q < arr.length)
        {
            let trip = new Array();
            trip.push(arr[j]);
            trip.push(arr[q]);
            trip.push(arr[j] + arr[q]);

            if (k.has(arr[j] + arr[q]) &&
                !ssd.has(trip))
            {
                count += 1;
                let nums = new Array();
                nums.push(arr[j]);
                nums.push(arr[q]);
                nums.push(arr[j] + arr[q]);
                ssd.add(nums);
            }
            q += 1;
        }
        j += 1;
    }
    return count;
}

// Driver Code

    let arr = new Array();
    arr.push(7);
    arr.push(2);
    arr.push(5);
    arr.push(4);
    arr.push(3);
    arr.push(6);
    arr.push(1);
    arr.push(9);
    arr.push(10);
    arr.push(12);

    let count = triplets(arr);

    document.write(count);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
18
```

**时间复杂度:** O(N <sup>2</sup> *logN)

**辅助空间:** O(3*N <sup>2</sup> )