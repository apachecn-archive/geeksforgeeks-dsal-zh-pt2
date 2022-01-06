# 合并数组中所有偶数元素的子数组中的元素

> 原文:[https://www . geesforgeks . org/merge-the-elements-in-subarray-of-all-even-elements-of-the-array/](https://www.geeksforgeeks.org/merge-the-elements-in-subarray-of-all-even-elements-of-the-array/)

给定一个包含 **N** 个数字的数组 **arr[]** ，任务是通过用连续偶数的第一个偶数元素替换该子数组的所有连续偶数来合并该子数组。
**注:**给定数列中至少有三个偶数的数列称为连续的偶数。因此，合并子数组中至少有 3 个连续偶数的元素。
**示例:**

> **输入:** arr[] = {2，2，2，100，5，4，2，9，10，88，24}
> **输出:** 2 5 4 2 9 10
> **解释:**
> 给定序列包含两个连续的偶数子序列。它们是:
> {2，2，2，100}，{10，88，24}。这两个子序列必须合并到子序列中的第一个元素。
> 因此，原系列中{2，2，2，100}替换为 2，{10，88，24}替换为 10。
> **输入:** arr[] = {2，4，5，3，6，8，10，3，4}
> **输出:** 2 4 5 3 6 3 4

**方法:**为了解决这个问题，我们首先需要发现是否存在大小大于 3 的连续偶子序列。因此，我们的想法是遍历给定的数组，检查一个数字是否为偶数。

*   遍历数组。
*   检查元素是否均匀。
*   如果是偶数，会创建一个临时数组来存储下一个连续的偶数，直到下一个数字是奇数。
*   继续添加临时数组中的元素，直到出现奇数。
*   如果此临时数组的大小大于三，则从给定数组中移除这些元素，并用此临时数组的第一个元素替换它们。
*   清空临时数组以计算下一组偶数子序列。

下面是上述方法的实现:

## C++

```
// C++ program to merge the array
// as per the given condition
#include<bits/stdc++.h>
using namespace std;

// Function to merge the array
// as per the given condition
vector<int> merge(vector<int> arr)
{

    // Variable to store the final
    // sequence
    vector<int> ans;

    // Temporary array to store the
    // even numbers while traversing
    vector<int> e;
    int i = 0;
    int j = 0;
    int count = 0;

    // Iterating through the array
    while(i < arr.size())
    {

        // If the element is even
        if(arr[i] % 2 == 0)
        {
            j = i;

            // Iterating till an odd element
            // is found
            while(j < arr.size())
            {

                // Keep appending into the
                // temporary array if the
                // even number is occurred
                if (arr[j] % 2 == 0)
                {
                    e.push_back(arr[j]);
                    count += 1;
                }

                // Break if an odd number
                // has occurred
                else
                    break;

                j += 1;
            }

            // If the series has at least
            // three elements, then merge
            if(count >= 3)
               ans.push_back(e[0]);

            // Else, add all elements to the
            // answer array
            else
            {
                for (auto i: e)
                     ans.push_back(i);
            }

            // Reseting the count and
            // temp array
            count = 0;
            e.clear();
            i = j;
        }

        // If the element is odd, add
        // it to the answer array
        else
        {
            ans.push_back(arr[i]);
            i += 1;
        }
    }

    return ans;
}

// Driver code
int main()
{

    vector<int> arr({ 2, 2, 2, 100, 5, 4,
                      2, 9, 10, 88, 24 });
    vector<int> ans = merge(arr);

    cout << "[";
    for(int i= 0; i < ans.size(); i++)
    {
        if(i == ans.size() - 1)
        cout << ans[i] << "]";
        else
        cout << ans[i] << ", ";
    }

}

// This code is contributed by Samarth
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to merge the array
// as per the given condition
import java.util.*;

class GFG{

// Function to merge the array
// as per the given condition
static Vector<Integer> merge(int []arr)
{

    // Variable to store the final
    // sequence
    Vector<Integer> ans = new Vector<Integer>();

    // Temporary array to store the
    // even numbers while traversing
    Vector<Integer> e = new Vector<Integer>();

    int i = 0;
    int j = 0;
    int count = 0;

    // Iterating through the array
    while (i < arr.length)
    {

        // If the element is even
        if (arr[i] % 2 == 0)
        {
            j = i;

            // Iterating till an odd element
            // is found
            while (j < arr.length)
            {

                // Keep appending into the
                // temporary array if the
                // even number is occurred
                if (arr[j] % 2 == 0)
                {
                    e.add(arr[j]);
                    count += 1;
                }

                // Break if an odd number
                // has occurred
                else
                    break;

                j += 1;
            }

            // If the series has at least
            // three elements, then merge
            if (count >= 3)
               ans.add(e.get(0));

            // Else, add all elements to the
            // answer array
            else
            {
                for(int ii : e)
                     ans.add(ii);
            }

            // Reseting the count and
            // temp array
            count = 0;
            e.clear();
            i = j;
        }

        // If the element is odd, add
        // it to the answer array
        else
        {
            ans.add(arr[i]);
            i += 1;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{

    int []arr = { 2, 2, 2, 100, 5, 4,
                  2, 9, 10, 88, 24 };

    Vector<Integer> ans = merge(arr);

    System.out.print("[");
    for(int i= 0; i < ans.size(); i++)
    {
        if (i == ans.size() - 1)
            System.out.print(ans.get(i) + "]");
        else
            System.out.print(ans.get(i) + ", ");
    }
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to merge the array
# as per the given condition

# Function to merge the array
# as per the given condition
def merge(arr):

    # Variable to store the final
    # sequence
    ans = []

    # Temporary array to store the
    # even numbers while traversing
    e =[]
    i = 0
    j = 0
    count = 0

    # Iterating through the array
    while i<len(arr):

        # If the element is even
        if(arr[i]% 2 == 0):
            j = i

            # Iterating till an odd element
            # is found
            while j<len(arr):

                # Keep appending into the
                # temporary array if the
                # even number is occurred
                if arr[j]% 2 == 0:

                    e.append(arr[j])
                    count+= 1

                # Break if an odd number
                # has occurred
                else:
                    break

                j+= 1

            # If the series has at least
            # three elements, then merge
            if(count>= 3):
                ans.append(e[0])

            # Else, add all elements to the
            # answer array
            else:
                for i in e:
                    ans.append(i)

            # Reseting the count and
            # temp array
            count = 0
            e =[]
            i = j

        # If the element is odd, add
        # it to the answer array
        else:
            ans.append(arr[i])
            i+= 1

    return ans

# Driver code
if __name__ == "__main__":

    arr = [2, 2, 2, 100, 5, 4, 2, 9, 10, 88, 24]

    print(merge(arr))
```

## C#

```
// C# program to merge the array
// as per the given condition
using System;
using System.Collections.Generic;
class GFG{

// Function to merge the array
// as per the given condition
static List<int> merge(int []arr)
{
  // Variable to store the final
  // sequence
  List<int> ans = new List<int>();

  // Temporary array to store the
  // even numbers while traversing
  List<int> e = new List<int>();

  int i = 0;
  int j = 0;
  int count = 0;

  // Iterating through the array
  while (i < arr.Length)
  {
    // If the element is even
    if (arr[i] % 2 == 0)
    {
      j = i;

      // Iterating till an odd element
      // is found
      while (j < arr.Length)
      {
        // Keep appending into the
        // temporary array if the
        // even number is occurred
        if (arr[j] % 2 == 0)
        {
          e.Add(arr[j]);
          count += 1;
        }

        // Break if an odd number
        // has occurred
        else
          break;

        j += 1;
      }

      // If the series has at least
      // three elements, then merge
      if (count >= 3)
        ans.Add(e[0]);

      // Else, add all elements to the
      // answer array
      else
      {
        foreach(int ii in e)
          ans.Add(ii);
      }

      // Reseting the count and
      // temp array
      count = 0;
      e.Clear();
      i = j;
    }

    // If the element is odd, add
    // it to the answer array
    else
    {
      ans.Add(arr[i]);
      i += 1;
    }
  }
  return ans;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {2, 2, 2, 100, 5, 4,
               2, 9, 10, 88, 24};

  List<int> ans = merge(arr);
  Console.Write("[");

  for(int i= 0; i < ans.Count; i++)
  {
    if (i == ans.Count - 1)
      Console.Write(ans[i] + "]");
    else
      Console.Write(ans[i] + ", ");
  }
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
[2, 5, 4, 2, 9, 10]

```

**时间复杂度:** *O(N <sup>2</sup> )* ，其中 N 为阵长。