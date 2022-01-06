# 在给定的 1 到 N 的排列数组中找到所有重复和缺失的数字

> 原文:[https://www . geeksforgeeks . org/find-all-replicate-and-missing-numbers-in-给定-array-of-1 到-n/](https://www.geeksforgeeks.org/find-all-duplicate-and-missing-numbers-in-given-permutation-array-of-1-to-n/)

给定一个由第一个自然数**组成的大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到给定数组中**【1，N】**范围内所有重复和缺失的数字。**

****示例:****

> ****输入:** arr[] = {1，1，2，3，3，5}
> **输出:**
> 缺失的数字:【4，6】
> 重复的数字:【1，3】
> **解释:**
> 由于 4 和 6 不在 arr[]，因此它们缺失，1 重复两次，3 重复两次，因此它们是重复的数字。**
> 
> ****输入:** arr[] = {1，2，2，2，4，5，7}
> **输出:**
> 缺少数字:【3，6】
> 重复数字:【2】**

****方法:**给定的问题可以使用本文[中讨论的思想](https://www.geeksforgeeks.org/find-a-repeating-and-a-missing-number/)来解决，其中只有一个元素是重复的，另一个是重复的。按照以下步骤解决给定的问题:**

*   **初始化一个数组，比如说**缺少存储缺少元素的[]** 。**
*   **初始化一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如说**复制**，存储复制的元素。**
*   **[使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:

    *   如果**的值为 arr[i]！= arr[arr[I]–1]**为真，则当前元素不等于从 **1** 到 **N** 的所有数字都存在时的位置。所以交换 **arr[i]** 和**arr[arr[I]–1]**。
    *   否则，意味着相同的元素出现在**arr[arr[I]–1]**处。** 
*   **[使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果 **arr[i]** 的值与 **(i + 1)** 不同，则缺少的元素为 **(i + 1)** ，重复的元素为 **arr[i]** 。**
*   **完成上述步骤后，打印存储在**中的元素缺失[]** 和**重复[]** 作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the duplicate and
// the missing elements over the range
// [1, N]
void findElements(int arr[], int N)
{
    int i = 0;

    // Stores the missing and duplicate
    // numbers in the array arr[]
    vector<int> missing;
    set<int> duplicate;

    // Making an iterator for set
    set<int>::iterator it;

    // Traverse the given array arr[]
    while (i != N) {
        cout << i << " # " ;
        // Check if the current element
        // is not same as the element at
        // index arr[i] - 1, then swap
        if (arr[i] != arr[arr[i] - 1]) {
            swap(arr[i], arr[arr[i] - 1]);
        }

        // Otherwise, increment the index
        else {
            i++;
        }
    }

    // Traverse the array again
    for (i = 0; i < N; i++) {

        // If the element is not at its
        // correct position
        if (arr[i] != i + 1) {

            // Stores the missing and the
            // duplicate elements
            missing.push_back(i + 1);
            duplicate.insert(arr[i]);
        }
    }

    // Print the Missing Number
    cout << "Missing Numbers: ";
    for (auto& it : missing)
        cout << it << ' ';

    // Print the Duplicate Number
    cout << "\nDuplicate Numbers: ";
    for (auto& it : duplicate)
        cout << it << ' ';
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 2, 4, 5, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findElements(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.HashSet;

class GFG {

    // Function to find the duplicate and
    // the missing elements over the range
    // [1, N]
    static void findElements(int arr[], int N) {
        int i = 0;

        // Stores the missing and duplicate
        // numbers in the array arr[]
        ArrayList<Integer> missing = new ArrayList<Integer>();
        HashSet<Integer> duplicate = new HashSet<Integer>();

        // Traverse the given array arr[]
        while (i != N) {
            // Check if the current element
            // is not same as the element at
            // index arr[i] - 1, then swap
            if (arr[i] != arr[arr[i] - 1]) {
                int temp = arr[i];
                arr[i] = arr[arr[i] - 1];
                arr[temp - 1] = temp;
            }

            // Otherwise, increment the index
            else {
                i++;
            }
        }

        // Traverse the array again
        for (i = 0; i < N; i++) {

            // If the element is not at its
            // correct position
            if (arr[i] != i + 1) {

                // Stores the missing and the
                // duplicate elements
                missing.add(i + 1);
                duplicate.add(arr[i]);
            }
        }

        // Print the Missing Number
        System.out.print("Missing Numbers: ");
        for (Integer itr : missing)
            System.out.print(itr + " ");

        // Print the Duplicate Number
        System.out.print("\nDuplicate Numbers: ");
        for (Integer itr : duplicate)
            System.out.print(itr + " ");
    }

    // Driver code
    public static void main(String args[]) {
        int arr[] = { 1, 2, 2, 2, 4, 5, 7 };
        int N = arr.length;
        findElements(arr, N);
    }

}

// This code is contributed by gfgking.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the duplicate and
# the missing elements over the range
# [1, N]
def findElements(arr, N) :
    i = 0;

    # Stores the missing and duplicate
    # numbers in the array arr[]
    missing = [];
    duplicate = set();

    # Traverse the given array arr[]
    while (i != N) :

        # Check if the current element
        # is not same as the element at
        # index arr[i] - 1, then swap
        if (arr[i] != arr[arr[i] - 1]) :

            t = arr[i]
            arr[i] = arr[arr[i] - 1]
            arr[t - 1]  = t

        # Otherwise, increment the index
        else :
            i += 1;

    # Traverse the array again
    for i in range(N) :

        # If the element is not at its
        # correct position
        if (arr[i] != i + 1) :

            # Stores the missing and the
            # duplicate elements
            missing.append(i + 1);
            duplicate.add(arr[i]);

    # Print the Missing Number
    print("Missing Numbers: ",end="");

    for it in missing:
        print(it,end=" ");

    # Print the Duplicate Number
    print("\nDuplicate Numbers: ",end="");

    for it in list(duplicate) :
        print(it, end=' ');

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 2, 2, 4, 5, 7 ];
    N = len(arr);
    findElements(arr, N);

    # This code is contributed by AnkThon
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to find the duplicate and
// the missing elements over the range
// [1, N]
function findElements(arr, N) {
  let i = 0;

  // Stores the missing and duplicate
  // numbers in the array arr[]
  let missing = [];
  let duplicate = new Set();

  // Traverse the given array arr[]
  while (i != N)
  {

    // Check if the current element
    // is not same as the element at
    // index arr[i] - 1, then swap
    if (arr[i] != arr[arr[i] - 1]) {
      t = arr[i];
      arr[i] = arr[arr[i] - 1];
      arr[t - 1] = t;
    }

    // Otherwise, increment the index
    else {
      i += 1;
    }
  }

  // Traverse the array again
  for (let i = 0; i < N; i++)
  {

    // If the element is not at its
    // correct position
    if (arr[i] != i + 1)
    {

      // Stores the missing and the
      // duplicate elements
      missing.push(i + 1);
      duplicate.add(arr[i]);
    }
  }

  // Print the Missing Number
  document.write("Missing Numbers: ");

  for (it of missing) document.write(it + " ");

  // Print the Duplicate Number
  document.write("<br>Duplicate Numbers: ");

  for (let it of [...duplicate]) document.write(it + " ");
}

// Driver code

let arr = [1, 2, 2, 2, 4, 5, 7];
let N = arr.length;
findElements(arr, N);

// This code is contributed by _saurabh_jaiswal

</script>
```

****Output:** 

```
Missing Numbers: 3 6 
Duplicate Numbers: 2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**