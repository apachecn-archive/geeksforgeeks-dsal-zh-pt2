# 使用二分搜索法创建排序数组

> 原文:[https://www . geesforgeks . org/create-a-sorted-array-use-binary-search/](https://www.geeksforgeeks.org/create-a-sorted-array-using-binary-search/)

给定一个数组，任务是根据给定数组的元素以升序创建一个新的排序数组。
**例:**

```
Input : arr[] = {2, 5, 4, 9, 8}
Output : 2 4 5 8 9

Input : arr[] = {10, 45, 98, 35, 45}
Output : 10 35 45 45 98
```

使用二分搜索法可以有效地解决上述问题。我们创建一个新的数组，如果第一个元素是空的，就插入它。现在，对于每个新元素，我们使用二分搜索法找到该元素在新数组中的正确位置，然后在新数组的相应索引处插入该元素。
以下是上述方法的实现:

## C++

```
// C++ program to create a sorted array
// using Binary Search

#include <bits/stdc++.h>
using namespace std;

// Function to create a new sorted array
// using Binary Search
void createSorted(int a[], int n)
{
    // Auxiliary Array
    vector<int> b;

    for (int j = 0; j < n; j++) {
        // if b is empty any element can be at
        // first place
        if (b.empty())
            b.push_back(a[j]);
        else {

            // Perform Binary Search to find the correct
            // position of current element in the
            // new array
            int start = 0, end = b.size() - 1;

            // let the element should be at first index
            int pos = 0;

            while (start <= end) {

                int mid = start + (end - start) / 2;

                // if a[j] is already present in the new array
                if (b[mid] == a[j]) {
                    // add a[j] at mid+1\. you can add it at mid
                    b.emplace(b.begin() + max(0, mid + 1), a[j]);
                    break;
                }
                // if a[j] is lesser than b[mid] go right side
                else if (b[mid] > a[j])
                    // means pos should be between start and mid-1
                    pos = end = mid - 1;
                else
                    // else pos should be between mid+1 and end
                    pos = start = mid + 1;

                // if a[j] is the largest push it at last
                if (start > end) {
                    pos = start;
                    b.emplace(b.begin() + max(0, pos), a[j]);

                    // here max(0, pos) is used because sometimes
                    // pos can be negative as smallest duplicates
                    // can be present in the array
                    break;
                }
            }
        }
    }

    // Print the new generated sorted array
    for (int i = 0; i < n; i++)
        cout << b[i] << " ";
}

// Driver Code
int main()
{
    int a[] = { 2, 5, 4, 9, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    createSorted(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to create a sorted array
// using Binary Search
import java.util.*;

class GFG
{

// Function to create a new sorted array
// using Binary Search
static void createSorted(int a[], int n)
{
    // Auxiliary Array
    Vector<Integer> b = new Vector<>();

    for (int j = 0; j < n; j++)
    {
        // if b is empty any element can be at
        // first place
        if (b.isEmpty())
            b.add(a[j]);
        else
        {

            // Perform Binary Search to find the correct
            // position of current element in the
            // new array
            int start = 0, end = b.size() - 1;

            // let the element should be at first index
            int pos = 0;

            while (start <= end)
            {

                int mid = start + (end - start) / 2;

                // if a[j] is already present in the new array
                if (b.get(mid) == a[j])
                {
                    // add a[j] at mid+1\. you can add it at mid
                    b.add((Math.max(0, mid + 1)), a[j]);
                    break;
                }

                // if a[j] is lesser than b[mid] go right side
                else if (b.get(mid) > a[j])
                    // means pos should be between start and mid-1
                    pos = end = mid - 1;
                else
                    // else pos should be between mid+1 and end
                    pos = start = mid + 1;

                // if a[j] is the largest push it at last
                if (start > end)
                {
                    pos = start;
                    b.add(Math.max(0, pos), a[j]);

                    // here max(0, pos) is used because sometimes
                    // pos can be negative as smallest duplicates
                    // can be present in the array
                    break;
                }
            }
        }
    }

    // Print the new generated sorted array
    for (int i = 0; i < n; i++)
        System.out.print(b.get(i) + " ");
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 2, 5, 4, 9, 8 };
    int n = a.length;

    createSorted(a, n);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python program to create a sorted array
# using Binary Search

# Function to create a new sorted array
# using Binary Search
def createSorted(a: list, n: int):

    # Auxiliary Array
    b = []
    for j in range(n):

        # if b is empty any element can be at
        # first place
        if len(b) == 0:
            b.append(a[j])
        else:

            # Perform Binary Search to find the correct
            # position of current element in the
            # new array
            start = 0
            end = len(b) - 1

            # let the element should be at first index
            pos = 0
            while start <= end:
                mid = start + (end - start) // 2

                # if a[j] is already present in the new array
                if b[mid] == a[j]:

                    # add a[j] at mid+1\. you can add it at mid
                    b.insert(max(0, mid + 1), a[j])
                    break

                # if a[j] is lesser than b[mid] go right side
                elif b[mid] > a[j]:

                    # means pos should be between start and mid-1
                    pos = end = mid - 1
                else:

                    # else pos should be between mid+1 and end
                    pos = start = mid + 1

                # if a[j] is the largest push it at last
                if start > end:
                    pos = start
                    b.insert(max(0, pos), a[j])

                    # here max(0, pos) is used because sometimes
                    # pos can be negative as smallest duplicates
                    # can be present in the array
                    break

    # Print the new generated sorted array
    for i in range(n):
        print(b[i], end=" ")

# Driver Code
if __name__ == "__main__":

    a = [2, 5, 4, 9, 8]
    n = len(a)
    createSorted(a, n)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to create a sorted array
// using Binary Search
using System;
using System.Collections.Generic;

class GFG
{

// Function to create a new sorted array
// using Binary Search
static void createSorted(int []a, int n)
{
    // Auxiliary Array
    List<int> b = new List<int>();

    for (int j = 0; j < n; j++)
    {
        // if b is empty any element can be at
        // first place
        if (b.Count == 0)
            b.Add(a[j]);
        else
        {

            // Perform Binary Search to find the correct
            // position of current element in the
            // new array
            int start = 0, end = b.Count - 1;

            // let the element should be at first index
            int pos = 0;

            while (start <= end)
            {

                int mid = start + (end - start) / 2;

                // if a[j] is already present in the new array
                if (b[mid] == a[j])
                {
                    // add a[j] at mid+1\. you can add it at mid
                    b.Insert((Math.Max(0, mid + 1)), a[j]);
                    break;
                }

                // if a[j] is lesser than b[mid] go right side
                else if (b[mid] > a[j])

                    // means pos should be between start and mid-1
                    pos = end = mid - 1;
                else

                    // else pos should be between mid+1 and end
                    pos = start = mid + 1;

                // if a[j] is the largest push it at last
                if (start > end)
                {
                    pos = start;
                    b.Insert(Math.Max(0, pos), a[j]);

                    // here Max(0, pos) is used because sometimes
                    // pos can be negative as smallest duplicates
                    // can be present in the array
                    break;
                }
            }
        }
    }

    // Print the new generated sorted array
    for (int i = 0; i < n; i++)
        Console.Write(b[i] + " ");
}

// Driver Code
public static void Main(String []args)
{
    int []a = { 2, 5, 4, 9, 8 };
    int n = a.Length;

    createSorted(a, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

      // JavaScript program to create a sorted array
      // using Binary Search

      // Function to create a new sorted array
      // using Binary Search
      function createSorted(a, n) {
        // Auxiliary Array
        var b = [];

        for (var j = 0; j < n; j++) {
          // if b is empty any element can be at
          // first place
          if (b.length == 0) b.push(a[j]);
          else {
            // Perform Binary Search to find the correct
            // position of current element in the
            // new array
            var start = 0,
              end = b.length - 1;

            // let the element should be at first index
            var pos = 0;

            while (start <= end) {
              var mid = start + parseInt((end - start) / 2);

              // if a[j] is already present in the new array
              if (b[mid] === a[j]) {
                // add a[j] at mid+1\. you can add it at mid
                b.insert(Math.max(0, mid + 1), a[j]);

                break;
              }

              // if a[j] is lesser than b[mid] go right side
              else if (b[mid] > a[j])
                // means pos should be between start and mid-1
                pos = end = mid - 1;
              // else pos should be between mid+1 and end
              else pos = start = mid + 1;

              // if a[j] is the largest push it at last
              if (start > end) {
                pos = start;
                b.insert(Math.max(0, pos), a[j]);

                // here Max(0, pos) is used because sometimes
                // pos can be negative as smallest duplicates
                // can be present in the array
                break;
              }
            }
          }
        }

        // Print the new generated sorted array
        for (var i = 0; i < n; i++) document.write(b[i] + " ");
      }

      Array.prototype.insert = function (index, item) {
        this.splice(index, 0, item);
      };
      // Driver Code
      var a = [2, 5, 4, 9, 8];
      var n = a.length;

      createSorted(a, n);

</script>
```

**Output:** 

```
2 4 5 8 9
```

**时间复杂度** : O(N*N)。虽然正在使用二分搜索法，但列表插入调用平均在 0(N)时间内运行
**辅助空间**:0(N)