# 查找数组是否可以通过限制为 k 倍数的交换进行排序

> 原文:[https://www . geesforgeks . org/find-if-array-可通过交换进行排序-限于 k 的倍数/](https://www.geeksforgeeks.org/find-if-array-can-be-sorted-by-swaps-limited-to-multiples-of-k/)

给定一个数组和一个数字 k，任务是检查给定的数组是否可以通过有限的交换操作进行排序。我们只能用 arr[i]或 arr[i + k]或 arr[i + 2*k]或 arr[i + 3*k]等来交换 arr[i]。一般来说，索引 I 处的元素可以与索引 i + j*k 处的元素交换，其中 j = 0，1，2，3，…
注意:可以在数组上执行任意数量的交换。

**示例:**

> **输入:** arr[8] = [1，5，6，9，2，3，5，9]， k = 3
> **输出:**可能排序
> **解释:** 1 5 6 9 2 3 5 9
> 0 1 2 3 4 5 6 7 这里的 k 是 3
> 0 可以用 0 + 3 = (3)交换元素
> 1 可以用 1 + 3 = (4)交换元素
> 2 可以用 2 + 3 = (5)交换元素
> 3 可以用 3 + 3 = (6)交换 元素
> 4 可以与 4 + 3 = (7)元素进行交换
> 我们可以看到索引 0，3，6 处的元素可以相互交换
> 我们可以看到索引 1，4，7 处的元素可以相互交换
> 我们可以看到索引 2，5 处的元素可以相互交换
> 元素 0 永远不能与索引 7，1，4，2，5 进行交换
> 元素在索引(1， 4) 1 2 6 9 5 3 5 9
> 因为 sortarr[1] = 2
> 在索引(2，5) 1 2 3 9 5 6 5 9
> 处交换元素，因为 sortarr[2] = 3
> 在索引(3，6)1 2 3 5 5 6 9
> 处交换元素，因为 sortarr[3] = 5
> 在这种情况下通过交换，我们能够达到 1 2 3 5 6 9
> 
> **输入:** arr=[1，4，2，3]，k = 2
> **输出:**无法排序
> **解释:** 1 4 2 3
> 0 1 2 3 其中 k 为 2
> 0 可以与 0 + 2 = (2)元素互换。
> 1 可以和 1 + 2 = (3)元素互换。
> 我们可以看到，索引 0、2 处的元素可以互相交换。
> 我们可以看到索引 1、3 处元素可以相互交换。
> 不需要交换索引(0，2) 1 4 2 3 处的元素
> 0 1 2 3
> 在排序数组的索引 1 处是 2
> 2 在 1 + j * 2 中不存在，其中 j = {0，1}
> 所以由于 2 永远不能出现在数组的索引 1 处，
> 数组不能排序。
> 数组交换后不排序。
> 
> **输入:**arr[]=【1，4，2，3】，k = 1
> **输出:**可能排序
> **解释:** 1 4 2 3
> 0 1 2 3 其中 k 为 1
> 当 k 为 1 时，总是可能排序
> ，因为交换发生在相邻元素之间。

**方法:**
1)创建排序规则[]作为给定 Arr 的排序版本。
2)将该数组与排序后的数组进行比较。
3)循环迭代，比较索引 i.
4)现在比较索引 I，元素与
索引= i + j * k
比较，其中 j = 0，1，2…..
5)如果对于特定 I 元素，sortArr[i]与 sequence arr[index]匹配，则标志为 1，且
交换 Arr[i]，arr[index]
6)如果没有交换，则标志为 0，这意味着在 sequence 中没有找到元素
7)如果标志为 0，则循环中断并打印不可能
8)否则打印可能

## C++14

```
#include <bits/stdc++.h>
using namespace std;

// CheckSort function
// To check if array can be sorted
void CheckSort(vector<int> arr,int k,int n){

    // sortarr is sorted array of arr
    vector<int> sortarr(arr.begin(),arr.end());

    sort(sortarr.begin(),sortarr.end());

    // if k = 1 then (always possible to sort)
    // swapping can easily give sorted
    // array
    if (k == 1)
        printf("yes");
    else
    {
        int flag = 0;

        // comparing sortarray with array
        for (int i = 0; i < n; i++)
        {
            flag = 0;

            // element at index j
            // must be in j = i + l * k form
            // where i = 0, 1, 2, 3...
            // where l = 0, 1, 2, 3, ..n-1
            for (int j = i; j < n; j += k)
            {

                //if element is present
                //then swapped
                if (sortarr[i] == arr[j]){
                    swap(arr[i], arr[j]);
                    flag = 1;
                    break;
                }
                if (j + k >= n)
                    break;

            }

            // if element of sorted array
            // does not found in its sequence
            // then flag remain zero
            // that means arr can not be
            // sort after swapping
            if (flag == 0)
                break;

            }

        // if flag is 0
        // Not possible
        // else Possible
        if (flag == 0)
            printf("Not possible to sort");
        else
            printf("Possible to sort");
        }
}

// Driver code
int main()
{
    // size of step
    int k = 3;

    // array initialized
    vector<int> arr ={1, 5, 6, 9, 2, 3, 5, 9};

    // length of arr
    int n =arr.size();

    // calling function
    CheckSort(arr, k, n);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

// CheckSort function
// To check if array can be sorted
public static void CheckSort(Vector<Integer> arr,
                             int k, int n)
{

    // sortarr is sorted array of arr
    Vector<Integer> sortarr = new Vector<Integer>();
    for(int i = 0; i < arr.size(); i++)
    {
        sortarr.add(arr.get(i));
    }

    Collections.sort(sortarr);

    // If k = 1 then (always possible to sort)
    // swapping can easily give sorted
    // array
    if (k == 1)
        System.out.println("yes");
    else
    {
        int flag = 0;

        // Comparing sortarray with array
        for(int i = 0; i < n; i++)
        {
            flag = 0;

            // Element at index j
            // must be in j = i + l * k form
            // where i = 0, 1, 2, 3...
            // where l = 0, 1, 2, 3, ..n-1
            for(int j = i; j < n; j += k)
            {

                // If element is present
                //then swapped
                if (sortarr.get(i) == arr.get(j))
                {
                    Collections.swap(arr, i, j);
                    flag = 1;
                    break;
                }
                if (j + k >= n)
                    break;
            }

            // If element of sorted array
            // does not found in its sequence
            // then flag remain zero
            // that means arr can not be
            // sort after swapping
            if (flag == 0)
                break;
        }

        // If flag is 0
        // Not possible
        // else Possible
        if (flag == 0)
            System.out.println("Not possible to sort");
        else
            System.out.println("Possible to sort");
    }
}

// Driver code
public static void main(String[] args)
{

    // Size of step
    int k = 3;

    // Array initialized
    Vector<Integer> arr = new Vector<Integer>();
    arr.add(1);
    arr.add(5);
    arr.add(6);
    arr.add(9);
    arr.add(2);
    arr.add(3);
    arr.add(5);
    arr.add(9);

    // Length of arr
    int n = arr.size();

    // Calling function
    CheckSort(arr, k, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# CheckSort function
# To check if array can be sorted
def CheckSort(arr, k, n):

    # sortarr is sorted array of arr
    sortarr = sorted(arr)

    # if k = 1 then (always possible to sort)
    # swapping can easily give sorted
    # array
    if (k == 1):
        print("yes")
    else:

        # comparing sortarray with array
        for i in range(0, n):
            flag = 0

            # element at index j
            # must be in j = i + l * k form
            # where i = 0, 1, 2, 3...
            # where l = 0, 1, 2, 3, ..n-1
            for j in range(i, n, k):

                # if element is present
                # then swapped
                if (sortarr[i] == arr[j]):
                    arr[i], arr[j] = arr[j], arr[i]
                    flag = 1
                    break
                if (j + k >= n):
                    break

            # if element of sorted array
            # does not found in its sequence
            # then flag remain zero
            # that means arr can not be
            # sort after swapping
            if (flag == 0):
                break

        # if flag is 0
        # Not possible
        # else Possible
        if (flag == 0):
            print("Not possible to sort")
        else:
            print("Possible to sort")

# Driver code
if __name__ == "__main__":
    # size of step
    k = 3

    # array initialized
    arr =[1, 5, 6, 9, 2, 3, 5, 9]

    # length of arr
    n = len(arr)

    # calling function
    CheckSort(arr, k, n)   
```

## C#

```
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// CheckSort function
// To check if array can be sorted
static void CheckSort(ArrayList arr, int k, int n)
{

    // sortarr is sorted array of arr
    ArrayList sortarr = new ArrayList(arr);
    sortarr.Sort();

    // If k = 1 then (always possible to sort)
    // swapping can easily give sorted
    // array
    if (k == 1)
        Console.Write("yes");
    else
    {
        int flag = 0;

        // Comparing sortarray with array
        for(int i = 0; i < n; i++)
        {
            flag = 0;

            // Element at index j
            // must be in j = i + l * k form
            // where i = 0, 1, 2, 3...
            // where l = 0, 1, 2, 3, ..n-1
            for(int j = i; j < n; j += k)
            {

                // If element is present
                // then swapped
                if ((int)sortarr[i] == (int)arr[j])
                {
                    int tmp = (int)arr[i];
                    arr[i] = (int)arr[j];
                    arr[j] = tmp;
                    flag = 1;
                    break;
                }

                if (j + k >= n)
                {
                    break;
                }
            }

            // If element of sorted array
            // does not found in its sequence
            // then flag remain zero
            // that means arr can not be
            // sort after swapping
            if (flag == 0)
            {
                break;
            }
        }

        // If flag is 0
        // Not possible
        // else Possible
        if (flag == 0)
            Console.Write("Not possible to sort");
        else
            Console.Write("Possible to sort");
    }
}

// Driver code
public static void Main(string[] args)
{

    // Size of step
    int k = 3;

    // Array initialized
    ArrayList arr = new ArrayList(){ 1, 5, 6, 9,
                                     2, 3, 5, 9 };

    // Length of arr
    int n = arr.Count;

    // Calling function
    CheckSort(arr, k, n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
      // CheckSort function
      // To check if array can be sorted
      function CheckSort(arr, k, n)
      {

        // sortarr is sorted array of arr
        var sortarr = arr.sort((a, b) => a - b);

        // If k = 1 then (always possible to sort)
        // swapping can easily give sorted
        // array
        if (k === 1) document.write("yes");
        else
        {
          var flag = 0;

          // Comparing sortarray with array
          for (var i = 0; i < n; i++) {
            flag = 0;

            // Element at index j
            // must be in j = i + l * k form
            // where i = 0, 1, 2, 3...
            // where l = 0, 1, 2, 3, ..n-1
            for (var j = i; j < n; j += k)
            {

              // If element is present
              // then swapped
              if (sortarr[i] === arr[j])
              {
                var tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;
                flag = 1;
                break;
              }

              if (j + k >= n) {
                break;
              }
            }

            // If element of sorted array
            // does not found in its sequence
            // then flag remain zero
            // that means arr can not be
            // sort after swapping
            if (flag === 0) {
              break;
            }
          }

          // If flag is 0
          // Not possible
          // else Possible
          if (flag === 0) document.write("Not possible to sort");
          else document.write("Possible to sort");
        }
      }

      // Driver code
      // Size of step
      var k = 3;

      // Array initialized
      var arr = [1, 5, 6, 9, 2, 3, 5, 9];

      // Length of arr
      var n = arr.length;

      // Calling function
      CheckSort(arr, k, n);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
Possible to sort
```

**性能分析:**
**时间复杂度:** O(N^2)其中 n 是数组的大小。最差情况
**辅助空间:** O(N)其中 N 为数组大小。