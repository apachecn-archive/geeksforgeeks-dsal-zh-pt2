# 数组边界元素可能的最长递增序列

> 原文:[https://www . geeksforgeeks . org/最长递增序列-数组的可能边界元素/](https://www.geeksforgeeks.org/longest-increasing-sequence-possible-by-the-boundary-elements-of-an-array/)

给定一个由正整数**、**组成的长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找到[最长的递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)，它可以由数组两端的元素组成。

**示例:**

> **输入:** N=4 arr[] ={ 1，4，2，3 }
> **输出:** 1 3 4
> **解释:**
> 将 arr[0]追加到序列中。序列= {1}。数组= {4，2，3}。
> 将 arr[2]追加到序列中。序列= {1，3}。数组= {4，2}。
> 将 arr[0]追加到序列中。序列= {1，3，4}。数组= {2}。
> 因此，{1，3，4}是给定数组中最长的递增序列。
> 
> **输入:** N=3 arr[] ={ 4，1，3 }
> T3】输出: 3 4

**进场:**解决这个问题的思路是用[两个指针进场](https://www.geeksforgeeks.org/two-pointers-technique/)。维护一个变量，对严格递增序列中最右边的元素说**最右边的元素，**。保持数组两端有两个指针，分别说 **i** 和 **j** ，执行以下步骤，直到 **i** 超过 **j** 或者两端的元素小于**最右边的 _ 元素**:

*   **If arr[i] > arr[j]:**
    *   **如果 arr[j] >最右侧 _ 元素:**设置**最右侧 _ 元素= arr[j]** 并减量 **j** 。将**arr【j】**添加到序列中。
    *   **如果 arr[i] >最右侧 _ 元素:**设置**最右侧 _ 元素= arr[i]** 并增加 **i** 。将 **arr[i]** 添加到序列中。
*   **If arr[i] < arr[j]:**
    *   **如果 arr[i] >最右 _ 元素**:设置**最右 _ 元素= arr[i]** 并增加 **i** 。将 **arr[i]** 添加到序列中。
    *   **如果 arr[j] >最右 _ 元素**:设置**最右 _ 元素= arr[j]** 并减量 **j** 。将**arr【j】**添加到序列中。
*   **如果 arr[j] = arr[i]:**
    *   **如果 i = j:**
        *   **如果 arr[i] >最右侧 _ 元素**:将 **arr[i]** 添加到序列中。
    *   **否则:**分别检查从两端可以添加的最大元素，分别为 **max_left** 和 **max_right** 。
        *   **If max_left > max_right** :添加所有可以从左端添加的元素。
        *   **否则:**从右侧添加所有可以添加的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
#include <vector>
using namespace std;

// Function to find longest strictly
// increasing sequence using boundary elements
void findMaxLengthSequence(int N, int arr[4])
{
    // Maintains rightmost element
    // in the sequence
    int rightmost_element = -1;

    // Pointer to start of array
    int i = 0;

    // Pointer to end of array
    int j = N - 1;

    // Stores the required sequence
    vector<int> sequence;

    // Traverse the array
    while (i <= j) {

        // If arr[i]>arr[j]
        if (arr[i] > arr[j]) {

            // If arr[j] is greater than
            // rightmost element of the sequence
            if (arr[j] > rightmost_element) {

                // Push arr[j] into the sequence
                sequence.push_back(arr[j]);

                // Update rightmost element
                rightmost_element = arr[j];
                j--;
            }
            else if (arr[i] > rightmost_element) {

                // Push arr[i] into the sequence
                sequence.push_back(arr[i]);

                // Update rightmost element
                rightmost_element = arr[i];
                i++;
            }
            else
                break;
        }

        // If arr[i] < arr[j]
        else if (arr[i] < arr[j]) {

            // If arr[i] > rightmost element
            if (arr[i] > rightmost_element) {

                // Push arr[i] into the sequence
                sequence.push_back(arr[i]);

                // Update rightmost element
                rightmost_element = arr[i];
                i++;
            }

            // If arr[j] > rightmost element
            else if (arr[j] > rightmost_element) {

                // Push arr[j] into the sequence
                sequence.push_back(arr[j]);

                // Update rightmost element
                rightmost_element = arr[j];
                j--;
            }
            else
                break;
        }

        // If arr[i] is equal to arr[j]
        else if (arr[i] == arr[j]) {

            // If i and j are at the same element
            if (i == j) {

                // If arr[i] > rightmostelement
                if (arr[i] > rightmost_element) {

                    // Push arr[j] into the sequence
                    sequence.push_back(arr[i]);

                    // Update rightmost element
                    rightmost_element = arr[i];
                    i++;
                }
                break;
            }
            else {
                sequence.push_back(arr[i]);

                // Traverse array
                // from left to right
                int k = i + 1;

                // Stores the increasing
                // sequence from the left end
                vector<int> max_left;

                // Traverse array from left to right
                while (k < j && arr[k] > arr[k - 1]) {

                    // Push arr[k] to max_left vector
                    max_left.push_back(arr[k]);
                    k++;
                }

                // Traverse the array
                // from right to left
                int l = j - 1;

                // Stores the increasing
                // sequence from the right end
                vector<int> max_right;

                // Traverse array from right to left
                while (l > i && arr[l] > arr[l + 1]) {

                    // Push arr[k] to max_right vector
                    max_right.push_back(arr[l]);
                    l--;
                }

                // If size of max_left is greater
                // than max_right
                if (max_left.size() > max_right.size())
                    for (int element : max_left)

                        // Push max_left elements to
                        // the original sequence
                        sequence.push_back(element);

                // Otherwise
                else
                    for (int element : max_right)

                        // Push max_right elements to
                        // the original sequence
                        sequence.push_back(element);
                break;
            }
        }
    }

    // Print the sequence
    for (int element : sequence)
        printf("%d ", element);
}

// Driver Code
int main()
{
    int N = 4;
    int arr[] = { 1, 3, 2, 1 };

    // Print the longest increasing
    // sequence using boundary elements
    findMaxLengthSequence(N, arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find longest strictly
// increasing sequence using boundary elements
static void findMaxLengthSequence(int N, int[] arr)
{

    // Maintains rightmost element
    // in the sequence
    int rightmost_element = -1;

    // Pointer to start of array
    int i = 0;

    // Pointer to end of array
    int j = N - 1;

    // Stores the required sequence
    Vector<Integer> sequence = new Vector<Integer>();

    // Traverse the array
    while (i <= j)
    {

        // If arr[i]>arr[j]
        if (arr[i] > arr[j])
        {

            // If arr[j] is greater than
            // rightmost element of the sequence
            if (arr[j] > rightmost_element)
            {

                // Push arr[j] into the sequence
                sequence.add(arr[j]);

                // Update rightmost element
                rightmost_element = arr[j];
                j--;
            }
            else if (arr[i] > rightmost_element)
            {

                // Push arr[i] into the sequence
                sequence.add(arr[i]);

                // Update rightmost element
                rightmost_element = arr[i];
                i++;
            }
            else
            break;
        }

        // If arr[i] < arr[j]
        else if (arr[i] < arr[j])
        {

            // If arr[i] > rightmost element
            if (arr[i] > rightmost_element)
            {

                // Push arr[i] into the sequence
                sequence.add(arr[i]);

                // Update rightmost element
                rightmost_element = arr[i];
                i++;
            }

            // If arr[j] > rightmost element
            else if (arr[j] > rightmost_element)
            {

                // Push arr[j] into the sequence
                sequence.add(arr[j]);

                // Update rightmost element
                rightmost_element = arr[j];
                j--;
            }
            else
                break;
        }

        // If arr[i] is equal to arr[j]
        else if (arr[i] == arr[j])
        {

            // If i and j are at the same element
            if (i == j)
            {

                // If arr[i] > rightmostelement
                if (arr[i] > rightmost_element)
                {

                    // Push arr[j] into the sequence
                    sequence.add(arr[i]);

                    // Update rightmost element
                    rightmost_element = arr[i];
                    i++;
                }
                break;
            }
            else
            {
                sequence.add(arr[i]);

                // Traverse array
                // from left to right
                int k = i + 1;

                // Stores the increasing
                // sequence from the left end
                Vector<Integer> max_left = new Vector<Integer>();

                // Traverse array from left to right
                while (k < j && arr[k] > arr[k - 1])
                {

                    // Push arr[k] to max_left vector
                    max_left.add(arr[k]);
                    k++;
                }

                // Traverse the array
                // from right to left
                int l = j - 1;

                // Stores the increasing
                // sequence from the right end
                Vector<Integer> max_right = new Vector<Integer>();

                // Traverse array from right to left
                while (l > i && arr[l] > arr[l + 1])
                {

                    // Push arr[k] to max_right vector
                    max_right.add(arr[l]);
                    l--;
                }

                // If size of max_left is greater
                // than max_right
                if (max_left.size() > max_right.size())
                    for(int element : max_left)

                        // Push max_left elements to
                        // the original sequence
                        sequence.add(element);

                // Otherwise
                else
                    for(int element : max_right)

                        // Push max_right elements to
                        // the original sequence
                        sequence.add(element);

                break;
            }
        }
    }

    // Print the sequence
    for(int element : sequence)
        System.out.print(element + " ");
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;
    int[] arr = { 1, 3, 2, 1 };

    // Print the longest increasing
    // sequence using boundary elements
    findMaxLengthSequence(N, arr);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find longest strictly
# increasing sequence using boundary elements
def findMaxLengthSequence(N, arr):

    # Maintains rightmost element
    # in the sequence
    rightmost_element = -1

    # Pointer to start of array
    i = 0

    # Pointer to end of array
    j = N - 1

    # Stores the required sequence
    sequence = []

    # Traverse the array
    while (i <= j):

        # If arr[i]>arr[j]
        if (arr[i] > arr[j]):

            # If arr[j] is greater than
            # rightmost element of the sequence
            if (arr[j] > rightmost_element):

                # Push arr[j] into the sequence
                sequence.append(arr[j])

                # Update rightmost element
                rightmost_element = arr[j]
                j -= 1

            elif (arr[i] > rightmost_element):

                # Push arr[i] into the sequence
                sequence.append(arr[i])

                # Update rightmost element
                rightmost_element = arr[i]
                i += 1

            else:
                break

        # If arr[i] < arr[j]
        elif (arr[i] < arr[j]):

            # If arr[i] > rightmost element
            if (arr[i] > rightmost_element):

                # Push arr[i] into the sequence
                sequence.append(arr[i])

                # Update rightmost element
                rightmost_element = arr[i]
                i += 1

            # If arr[j] > rightmost element
            elif (arr[j] > rightmost_element):

                # Push arr[j] into the sequence
                sequence.append(arr[j])

                # Update rightmost element
                rightmost_element = arr[j]
                j -= 1

            else:
                break

        # If arr[i] is equal to arr[j]
        elif (arr[i] == arr[j]):

            # If i and j are at the same element
            if (i == j):

                # If arr[i] > rightmostelement
                if (arr[i] > rightmost_element):

                    # Push arr[j] into the sequence
                    sequence.append(arr[i])

                    # Update rightmost element
                    rightmost_element = arr[i]
                    i += 1

                break

            else:
                sequence.append(arr[i])

                # Traverse array
                # from left to right
                k = i + 1

                # Stores the increasing
                # sequence from the left end
                max_left = []

                # Traverse array from left to right
                while (k < j and arr[k] > arr[k - 1]):

                    # Push arr[k] to max_left vector
                    max_left.append(arr[k])
                    k += 1

                # Traverse the array
                # from right to left
                l = j - 1

                # Stores the increasing
                # sequence from the right end
                max_right = []

                # Traverse array from right to left
                while (l > i and arr[l] > arr[l + 1]):

                    # Push arr[k] to max_right vector
                    max_right.append(arr[l])
                    l -= 1

                # If size of max_left is greater
                # than max_right
                if (len(max_left) > len(max_right)):
                    for element in max_left:

                        # Push max_left elements to
                        # the original sequence
                        sequence.append(element)

                # Otherwise
                else:
                    for element in max_right:

                        # Push max_right elements to
                        # the original sequence
                        sequence.append(element)
                break

    # Print the sequence
    for element in sequence:
        print(element, end = " ")

# Driver Code
if __name__ == '__main__':

    N = 4
    arr = [ 1, 3, 2, 1 ]

    # Print the longest increasing
    # sequence using boundary elements
    findMaxLengthSequence(N, arr)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find longest strictly
  // increasing sequence using boundary elements
  static void findMaxLengthSequence(int N, int[] arr)
  {
    // Maintains rightmost element
    // in the sequence
    int rightmost_element = -1;

    // Pointer to start of array
    int i = 0;

    // Pointer to end of array
    int j = N - 1;

    // Stores the required sequence
    List<int> sequence = new List<int>();

    // Traverse the array
    while (i <= j) {

      // If arr[i]>arr[j]
      if (arr[i] > arr[j]) {

        // If arr[j] is greater than
        // rightmost element of the sequence
        if (arr[j] > rightmost_element) {

          // Push arr[j] into the sequence
          sequence.Add(arr[j]);

          // Update rightmost element
          rightmost_element = arr[j];
          j--;
        }
        else if (arr[i] > rightmost_element) {

          // Push arr[i] into the sequence
          sequence.Add(arr[i]);

          // Update rightmost element
          rightmost_element = arr[i];
          i++;
        }
        else
          break;
      }

      // If arr[i] < arr[j]
      else if (arr[i] < arr[j]) {

        // If arr[i] > rightmost element
        if (arr[i] > rightmost_element) {

          // Push arr[i] into the sequence
          sequence.Add(arr[i]);

          // Update rightmost element
          rightmost_element = arr[i];
          i++;
        }

        // If arr[j] > rightmost element
        else if (arr[j] > rightmost_element) {

          // Push arr[j] into the sequence
          sequence.Add(arr[j]);

          // Update rightmost element
          rightmost_element = arr[j];
          j--;
        }
        else
          break;
      }

      // If arr[i] is equal to arr[j]
      else if (arr[i] == arr[j]) {

        // If i and j are at the same element
        if (i == j) {

          // If arr[i] > rightmostelement
          if (arr[i] > rightmost_element) {

            // Push arr[j] into the sequence
            sequence.Add(arr[i]);

            // Update rightmost element
            rightmost_element = arr[i];
            i++;
          }
          break;
        }
        else {
          sequence.Add(arr[i]);

          // Traverse array
          // from left to right
          int k = i + 1;

          // Stores the increasing
          // sequence from the left end
          List<int> max_left = new List<int>();

          // Traverse array from left to right
          while (k < j && arr[k] > arr[k - 1])
          {

            // Push arr[k] to max_left vector
            max_left.Add(arr[k]);
            k++;
          }

          // Traverse the array
          // from right to left
          int l = j - 1;

          // Stores the increasing
          // sequence from the right end
          List<int> max_right = new List<int>();

          // Traverse array from right to left
          while (l > i && arr[l] > arr[l + 1])
          {

            // Push arr[k] to max_right vector
            max_right.Add(arr[l]);
            l--;
          }

          // If size of max_left is greater
          // than max_right
          if (max_left.Count > max_right.Count)
            foreach(int element in max_left)

              // Push max_left elements to
              // the original sequence
              sequence.Add(element);

          // Otherwise
          else
            foreach(int element in max_right)

              // Push max_right elements to
              // the original sequence
              sequence.Add(element);
          break;
        }
      }
    }

    // Print the sequence
    foreach(int element in sequence)
      Console.Write(element + " ");
  }

  // Driver code
  static void Main()
  {

    int N = 4;
    int[] arr = { 1, 3, 2, 1 };

    // Print the longest increasing
    // sequence using boundary elements
    findMaxLengthSequence(N, arr);
  }
}

// This code is contribute by divyesh072019
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find longest strictly
// increasing sequence using boundary elements
function findMaxLengthSequence(N, arr)
{

    // Maintains rightmost element
    // in the sequence
    let rightmost_element = -1;

    // Pointer to start of array
    let i = 0;

    // Pointer to end of array
    let j = N - 1;

    // Stores the required sequence
    let sequence = [];

    // Traverse the array
    while (i <= j)
    {

        // If arr[i]>arr[j]
        if (arr[i] > arr[j])
        {

            // If arr[j] is greater than
            // rightmost element of the sequence
            if (arr[j] > rightmost_element)
            {

                // Push arr[j] into the sequence
                sequence.push(arr[j]);

                // Update rightmost element
                rightmost_element = arr[j];
                j--;
            }
            else if (arr[i] > rightmost_element)
            {

                // Push arr[i] into the sequence
                sequence.push(arr[i]);

                // Update rightmost element
                rightmost_element = arr[i];
                i++;
            }
            else
            break;
        }

        // If arr[i] < arr[j]
        else if (arr[i] < arr[j])
        {

            // If arr[i] > rightmost element
            if (arr[i] > rightmost_element)
            {

                // Push arr[i] into the sequence
                sequence.push(arr[i]);

                // Update rightmost element
                rightmost_element = arr[i];
                i++;
            }

            // If arr[j] > rightmost element
            else if (arr[j] > rightmost_element)
            {

                // Push arr[j] into the sequence
                sequence.push(arr[j]);

                // Update rightmost element
                rightmost_element = arr[j];
                j--;
            }
            else
            break;
        }

        // If arr[i] is equal to arr[j]
        else if (arr[i] == arr[j])
        {

            // If i and j are at the same element
            if (i == j)
            {

                // If arr[i] > rightmostelement
                if (arr[i] > rightmost_element)
                {

                    // Push arr[j] into the sequence
                    sequence.push(arr[i]);

                    // Update rightmost element
                    rightmost_element = arr[i];
                    i++;
                }
                break;
            }
            else
            {
                sequence.push(arr[i]);

                // Traverse array
                // from left to right
                let k = i + 1;

                // Stores the increasing
                // sequence from the left end
                let max_left = [];

                // Traverse array from left to right
                while (k < j && arr[k] > arr[k - 1])
                {

                    // Push arr[k] to max_left vector
                    max_left.push(arr[k]);
                    k++;
                }

                // Traverse the array
                // from right to left
                let l = j - 1;

                // Stores the increasing
                // sequence from the right end
                let max_right = [];

                // Traverse array from right to left
                while (l > i && arr[l] > arr[l + 1])
                {

                    // Push arr[k] to max_right vector
                    max_right.push(arr[l]);
                    l--;
                }

                // If size of max_left is greater
                // than max_right
                if (max_left.length > max_right.length)
                for(let element = 0;
                    element < max_left.length;
                    element++)

                    // Push max_left elements to
                    // the original sequence
                    sequence.push(max_left[element]);

                // Otherwise
                else
                for(let element = 0;
                    element < max_right.length;
                    element++)

                    // Push max_right elements to
                    // the original sequence
                    sequence.push(max_right[element]);
                break;
            }
        }
    }

    // Print the sequence
    for(let element = 0;
        element < sequence.length;
        element++)
        document.write(sequence[element] + " ");
}

// Driver code
let N = 4;
let arr = [ 1, 3, 2, 1 ];

// Print the longest increasing
// sequence using boundary elements
findMaxLengthSequence(N, arr);

// This code is contributed by suresh07

</script>
```

**Output:** 

```
1 2 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)