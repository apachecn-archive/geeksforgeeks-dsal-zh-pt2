# 排序数组所需的最小次数

> 原文:[https://www . geeksforgeeks . org/最小次数-需要进行数组排序/](https://www.geeksforgeeks.org/minimum-number-of-deques-required-to-make-the-array-sorted/)

给定一个包含唯一整数的 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr** 。任务是计算使数组排序所需的最小次数[德清](https://www.geeksforgeeks.org/deque-cpp-stl/)**。**

****例**:**

> ****输入** : arr[] = {3，6，0，9，5，4}
> **输出** : 2
> **解释** :
> 新建一个德格 d1 = {3}。
> 新建一个 deque d2 = {6}。
> 将 0 推到 d1 前面；d1 = {0，3}
> 将 9 推至 d2 背面；d2 = {6，9}
> 将 5 推到 d2 前面；d2 = {5，6，9}
> 将 4 推到 d2 前面；d2 = {4，5，6，9}
> 因此，至少需要 2 个 deq。**
> 
> ****输入** : arr[] = {50，45，55，60，65，40，70，35，30，75}
> **输出** : 1**

****接近**:以上问题可以通过[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:**

1.  **创建两个数组**正面**和**背面**，存储所有德格的正面和背面元素。**
2.  **迭代数组中的所有元素。对于每个元素**arr【I】**，在下列情况下，当前元素可以被推入预先存在的队列:

    *   存在一个大于**arr【I】**的**战线【j】**，因为这意味着这个**arr【I】**可以被推到这个德格的前面。但是如果在数组 **arr** 中的**arr【I】**和**front【j】**之间存在另一个元素，那么它就不能被推送，因为推送会扰乱 deq 中元素的顺序，使得这些 deq 不能以排序数组的形式排列，甚至不能被单独排序。
    *   同样，使用上述步骤检查阵列**背面**。** 
3.  **如果一个元素不能被推送到下一个元素，那么应该为该元素创建另一个下一个元素。所以把元素放在前面和后面的数组中，因为它是新创建的 deque 的前面和后面。**
4.  **现在，返回[大小阵](https://www.geeksforgeeks.org/arraysize-c-stl/) **正面**(或**背面)**作为这个问题的答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
int minDeques(vector<int> arr)
{
    // Vectors to store the front and back
    // element of all present deques
    vector<int> fronts, backs;

    // Iterate through all array elements
    for (int i = 0; i < arr.size(); i++) {

        // Bool variable to check if the array
        // element has already been pushed or not
        bool hasBeenPushed = false;

        for (int j = 0; j < fronts.size(); j++) {

            // Check for all deques where arr[i]
            // can be pushed in the front
            if (arr[i] < fronts[j]) {
                bool isSafe = true;
                for (int k = 0; k < arr.size(); k++) {
                    if (arr[i] < arr[k]
                        && arr[k] < fronts[j]) {
                        isSafe = false;
                        break;
                    }
                }

                // Push in front of an already
                // existing deque
                if (isSafe) {
                    fronts[j] = arr[i];
                    hasBeenPushed = true;
                    break;
                }
            }

            // Check for all deques where arr[i]
            // can be pushed in the back
            if (arr[i] > backs[j]) {
                bool isSafe = true;
                for (int k = 0; k < arr.size(); k++) {
                    if (arr[i] > arr[k]
                        && arr[k] > backs[j]) {
                        isSafe = false;
                        break;
                    }
                }

                // Push in back of an already
                // existing deque
                if (isSafe) {
                    backs[j] = arr[i];
                    hasBeenPushed = true;
                    break;
                }
            }
        }

        // If arr[i] cannot be pushed to any
        // of the existing deques, then push
        // it in a new deque
        if (!hasBeenPushed) {
            fronts.push_back(arr[i]);
            backs.push_back(arr[i]);
        }
    }

    return fronts.size();
}

// Driver Code
int main()
{
    vector<int> arr = { 3, 6, 0, 9, 5, 4 };
    cout << minDeques(arr);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG{

public static int minDeques(int[] arr)
{
    // Vectors to store the front and back
    // element of all present deques
    ArrayList<Integer> fronts = new ArrayList<Integer>();
    ArrayList<Integer> backs = new ArrayList<Integer>();

    // Iterate through all array elements
    for (int i = 0; i < arr.length; i++) {

        // Bool variable to check if the array
        // element has already been pushed or not
        boolean hasBeenPushed = false;

        for (int j = 0; j < fronts.size(); j++) {

            // Check for all deques where arr[i]
            // can be pushed in the front
            if (arr[i] < fronts.get(j)) {
                boolean isSafe = true;
                for (int k = 0; k < arr.length; k++) {
                    if (arr[i] < arr[k]
                        && arr[k] < fronts.get(j)) {
                        isSafe = false;
                        break;
                    }
                }

                // Push in front of an already
                // existing deque
                if (isSafe) {
                    fronts.set(j, arr[i]);
                    hasBeenPushed = true;
                    break;
                }
            }

            // Check for all deques where arr[i]
            // can be pushed in the back
            if (arr[i] > backs.get(j)) {
                Boolean isSafe = true;
                for (int k = 0; k < arr.length; k++) {
                    if (arr[i] > arr[k]
                        && arr[k] > backs.get(j)) {
                        isSafe = false;
                        break;
                    }
                }

                // Push in back of an already
                // existing deque
                if (isSafe) {
                    backs.set(j, arr[i]);
                    hasBeenPushed = true;
                    break;
                }
            }
        }

        // If arr[i] cannot be pushed to any
        // of the existing deques, then push
        // it in a new deque
        if (!hasBeenPushed) {
            fronts.add(arr[i]);
            backs.add(arr[i]);
        }
    }

    return fronts.size();
}

// Driver Code
public static void main(String args[])
{
    int[] arr = { 3, 6, 0, 9, 5, 4 };
    System.out.println(minDeques(arr));
}
}

// This code is contributed by saurabh_jaiswal..
```

## **蟒蛇 3**

```
# python program for the above approach
def minDeques(arr):

        # Vectors to store the front and back
        # element of all present deques
    fronts = []
    backs = []

    # Iterate through all array elements
    for i in range(0, len(arr)):

                # Bool variable to check if the array
                # element has already been pushed or not
        hasBeenPushed = False

        for j in range(0, len(fronts)):

                        # Check for all deques where arr[i]
                        # can be pushed in the front
            if (arr[i] < fronts[j]):
                isSafe = True
                for k in range(0, len(arr)):
                    if (arr[i] < arr[k] and arr[k] < fronts[j]):
                        isSafe = False
                        break

                        # Push in front of an already
                        # existing deque
                if (isSafe):
                    fronts[j] = arr[i]
                    hasBeenPushed = True
                    break

                    # Check for all deques where arr[i]
                    # can be pushed in the back
            if (arr[i] > backs[j]):
                isSafe = True
                for k in range(0, len(arr)):
                    if (arr[i] > arr[k] and arr[k] > backs[j]):
                        isSafe = False
                        break

                        # Push in back of an already
                        # existing deque
                if (isSafe):
                    backs[j] = arr[i]
                    hasBeenPushed = True
                    break

                # If arr[i] cannot be pushed to any
                # of the existing deques, then push
                # it in a new deque
        if (not hasBeenPushed):
            fronts.append(arr[i])
            backs.append(arr[i])

    return len(fronts)

# Driver Code
if __name__ == "__main__":

    arr = [3, 6, 0, 9, 5, 4]
    print(minDeques(arr))

    # This code is contributed by rakeshsahni
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    static int minDeques(List<int> arr)
    {

        // Vectors to store the front and back
        // element of all present deques
        List<int> fronts = new List<int>();
        List<int> backs = new List<int>();

        // Iterate through all array elements
        for (int i = 0; i < arr.Count; i++) {

            // Bool variable to check if the array
            // element has already been pushed or not
            bool hasBeenPushed = false;

            for (int j = 0; j < fronts.Count; j++) {

                // Check for all deques where arr[i]
                // can be pushed in the front
                if (arr[i] < fronts[j]) {
                    bool isSafe = true;
                    for (int k = 0; k < arr.Count; k++) {
                        if (arr[i] < arr[k]
                            && arr[k] < fronts[j]) {
                            isSafe = false;
                            break;
                        }
                    }

                    // Push in front of an already
                    // existing deque
                    if (isSafe) {
                        fronts[j] = arr[i];
                        hasBeenPushed = true;
                        break;
                    }
                }

                // Check for all deques where arr[i]
                // can be pushed in the back
                if (arr[i] > backs[j]) {
                    bool isSafe = true;
                    for (int k = 0; k < arr.Count; k++) {
                        if (arr[i] > arr[k]
                            && arr[k] > backs[j]) {
                            isSafe = false;
                            break;
                        }
                    }

                    // Push in back of an already
                    // existing deque
                    if (isSafe) {
                        backs[j] = arr[i];
                        hasBeenPushed = true;
                        break;
                    }
                }
            }

            // If arr[i] cannot be pushed to any
            // of the existing deques, then push
            // it in a new deque
            if (!hasBeenPushed) {
                fronts.Add(arr[i]);
                backs.Add(arr[i]);
            }
        }

        return fronts.Count;
    }

    // Driver Code
    public static void Main()
    {
        List<int> arr = new List<int>{ 3, 6, 0, 9, 5, 4 };
        Console.WriteLine(minDeques(arr));
    }
}

// This code is contributed by ukasp.
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach
function minDeques(arr)
{

  // Vectors to store the front and back
  // element of all present deques
  let fronts = [],
    backs = [];

  // Iterate through all array elements
  for (let i = 0; i < arr.length; i++)
  {

    // let variable to check if the array
    // element has already been pushed or not
    let hasBeenPushed = false;

    for (let j = 0; j < fronts.length; j++)
    {

      // Check for all deques where arr[i]
      // can be pushed in the front
      if (arr[i] < fronts[j]) {
        let isSafe = true;
        for (let k = 0; k < arr.length; k++) {
          if (arr[i] < arr[k] && arr[k] < fronts[j]) {
            isSafe = false;
            break;
          }
        }

        // Push in front of an already
        // existing deque
        if (isSafe) {
          fronts[j] = arr[i];
          hasBeenPushed = true;
          break;
        }
      }

      // Check for all deques where arr[i]
      // can be pushed in the back
      if (arr[i] > backs[j]) {
        let isSafe = true;
        for (let k = 0; k < arr.length; k++) {
          if (arr[i] > arr[k] && arr[k] > backs[j]) {
            isSafe = false;
            break;
          }
        }

        // Push in back of an already
        // existing deque
        if (isSafe) {
          backs[j] = arr[i];
          hasBeenPushed = true;
          break;
        }
      }
    }

    // If arr[i] cannot be pushed to any
    // of the existing deques, then push
    // it in a new deque
    if (!hasBeenPushed) {
      fronts.push(arr[i]);
      backs.push(arr[i]);
    }
  }

  return fronts.length;
}

// Driver Code
let arr = [3, 6, 0, 9, 5, 4];
document.write(minDeques(arr));

// This code is contributed by saurabh_jaiswal.
</script>
```

****Output**

```
2
```** 

****时间复杂度:**o(n^3)
T3】辅助空间: O(N)**