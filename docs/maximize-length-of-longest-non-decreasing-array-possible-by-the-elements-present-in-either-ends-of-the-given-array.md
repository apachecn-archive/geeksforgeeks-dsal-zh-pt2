# 通过给定数组两端的元素最大化最长非递减数组的长度

> 原文:[https://www . geesforgeks . org/最大化给定数组两端的元素可能存在的最长非递减数组长度/](https://www.geeksforgeeks.org/maximize-length-of-longest-non-decreasing-array-possible-by-the-elements-present-in-either-ends-of-the-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，任务是通过将元素从给定数组的任一端追加到结果数组的末尾，并逐个移除追加的元素，来找到可以从给定的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)生成的最长非递减数组的最大长度。

**示例:**

> **输入:** A[] = {5，6，8，7}
> **输出:** : 4
> **解释:**
> 如果 resArr[] = { }是新生成的数组，那么
> 将 A[0]插入 resArr[]会修改 A[] = {6，8，7}并将 resArr[] = {5}
> 插入 A[0]到 resArr[]会修改 A[] = {8，7}和 resArr[] = {5，6}
> 插入 7}
> 在 resArr[]中插入 A[0]会修改 A[] = {}和 resArr[] = {5，6，7，8}
> 因此，可以从给定数组生成的最长非递减数组的长度为 4。
> 
> **输入:** {1，1，3，5，4，3，6，2，1}
> 输出 : 7

**逼近**:这个问题可以用[两个指针逼近](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。按照以下步骤解决问题:

*   初始化一个变量，比如 **res = 0** 来存储一个非递减数组的最大长度，该数组可以从给定的数组中生成。
*   初始化两个变量，比如**开始= 0** 和**结束= N–1**来存储开始和结束指针的索引。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件:
    *   如果 **A【开始】< = A【结束】**，则检查 **A【开始】**的值是否大于或等于新数组中先前插入的元素。如果发现为真，则将**开始**和**静止**的值增加 **1** 。
    *   如果 **A【开始】> = A【结束】**，则检查 **A【结束】**的值是否大于或等于新数组中先前插入的元素。如果发现为真，则将**结束**的值减少 **1** ，将**静止**的值增加 **1** 。
*   最后，打印 **res** 的值。

下面是上述方法的实现:

## C++

```
//C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the longest
// non-decreasing array that can be generated
int findLongestNonDecreasing(int A[], int N)
{

    // Stores the length of the longest
    // non-decreasing array that can be
    // generated from the array
    int res = 0; 

    // Stores index of
    // start pointer
    int start = 0;

    // Stores index of
    // end pointer
    int end = N - 1;

    // Stores previously inserted
    // element into the new array
    int prev = -1;

    // Traverse the array
    while (start <= end) {

        // If A[start] is less than
        // or equal to A[end]
        if (A[start] <= A[end]) {

            // If no element inserted into
            // the newly generated array
            if (prev == -1) {

                // Update prev
                prev = A[start];

                // Update res
                res++;

                // Update start
                start++;

            }

            else {

                 // If A[start] is greater
                 // than or equal to prev
                 if (A[start] >= prev) {

                    // Update res
                    res++;

                    // Update prev
                    prev = A[start];

                    // Update start
                    start++;
                 }

                //  If A[end] is greater
                 // than or equal to prev
                 else if (A[end] >= prev) {

                    // Update res
                    res++;

                    // Update prev
                    prev = A[end];

                    // Update end
                    end--;
                 }

                 else {
                     break;
                 }
            }
        }

        // If A[end] is
        // greater than A[start]
        else{

            // If no element inserted into
            // the newly generated array
            if (prev == -1) {

                // Update prev
                prev = A[end];

                // Update res
                res++;

                // Update end
                end--;
            }

            else {

                // If A[end] is greater
                // than or equal to prev
                if (A[end] >= prev) {

                    // Update res
                    res++;

                    //Update prev
                    prev = A[end];

                    // Update end
                    end--;
                }

                // If A[start] is greater
                // than or equal to prev
                else if (A[start] >= prev) {

                    // Update res
                    res++;

                    //Update prev
                    prev = A[start];

                    // Update start
                    start++;
                 }

                 else {
                     break;
                 }
            }
        }
    }

    return res;

}

//Driver Code
int main()
{

    int A[]={ 1, 1, 3, 5, 4, 3, 6, 2, 1 };

    int N = sizeof(A)/sizeof(A[0]);

    //Function call
    cout<< findLongestNonDecreasing(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the length of the longest
// non-decreasing array that can be generated
static int findLongestNonDecreasing(int A[],
                                    int N)
{

    // Stores the length of the longest
    // non-decreasing array that can be
    // generated from the array
    int res = 0; 

    // Stores index of
    // start pointer
    int start = 0;

    // Stores index of
    // end pointer
    int end = N - 1;

    // Stores previously inserted
    // element into the new array
    int prev = -1;

    // Traverse the array
    while (start <= end)
    {

        // If A[start] is less than
        // or equal to A[end]
        if (A[start] <= A[end])
        {

            // If no element inserted into
            // the newly generated array
            if (prev == -1)
            {

                // Update prev
                prev = A[start];

                // Update res
                res++;

                // Update start
                start++;
            }
            else
            {

                // If A[start] is greater
                // than or equal to prev
                if (A[start] >= prev)
                {

                    // Update res
                    res++;

                    // Update prev
                    prev = A[start];

                    // Update start
                    start++;
                }

                //  If A[end] is greater
                // than or equal to prev
                else if (A[end] >= prev)
                {

                    // Update res
                    res++;

                    // Update prev
                    prev = A[end];

                    // Update end
                    end--;
                }
                else
                {
                    break;
                }
            }
        }

        // If A[end] is
        // greater than A[start]
        else
        {

            // If no element inserted into
            // the newly generated array
            if (prev == -1)
            {

                // Update prev
                prev = A[end];

                // Update res
                res++;

                // Update end
                end--;
            }
            else
            {

                // If A[end] is greater
                // than or equal to prev
                if (A[end] >= prev)
                {

                    // Update res
                    res++;

                    //Update prev
                    prev = A[end];

                    // Update end
                    end--;
                }

                // If A[start] is greater
                // than or equal to prev
                else if (A[start] >= prev)
                {

                    // Update res
                    res++;

                    //Update prev
                    prev = A[start];

                    // Update start
                    start++;
                }
                else
                {
                    break;
                }
            }
        }
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 1, 3, 5, 4, 3, 6, 2, 1 };

    int N = A.length;

    // Function call
    System.out.print(findLongestNonDecreasing(A, N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the length of
# the longest non-decreasing array
# that can be generated
def findLongestNonDecreasing(A, N):

    # Stores the length of the longest
    # non-decreasing array that can be
    # generated from the array
    res = 0;

    # Stores index of
    # start pointer
    start = 0;

    # Stores index of
    # end pointer
    end = N - 1;

    # Stores previously inserted
    # element into the new array
    prev = -1;

    # Traverse the array
    while (start <= end):

        # If A[start] is less than
        # or equal to A[end]
        if (A[start] <= A[end]):

            # If no element inserted into
            # the newly generated array
            if (prev == -1):

                # Update prev
                prev = A[start];

                # Update res
                res += 1

                # Update start
                start += 1

            else:

                 # If A[start] is greater
                 # than or equal to prev
                 if (A[start] >= prev):

                    # Update res
                    res += 1

                    # Update prev
                    prev = A[start];

                    # Update start
                    start += 1

                #  If A[end] is greater
                # than or equal to prev
                 elif (A[end] >= prev):

                    # Update res
                    res += 1

                    # Update prev
                    prev = A[end];

                    # Update end
                    end -= 1

                 else:
                     break;

        # If A[end] is
        # greater than A[start]
        else:

            # If no element inserted into
            # the newly generated array
            if (prev == -1):

                # Update prev
                prev = A[end];

                # Update res
                res += 1

                # Update end
                end -= 1

            else:

                # If A[end] is greater
                # than or equal to prev
                if (A[end] >= prev):

                    # Update res
                    res += 1

                    # Update prev
                    prev = A[end];

                    # Update end
                    end -= 1

                # If A[start] is greater
                # than or equal to prev
                elif (A[start] >= prev):

                    # Update res
                    res += 1

                    # Update prev
                    prev = A[start];

                    # Update start
                    start += 1

                else :
                     break;

    return res

# Driver Code
if __name__ == "__main__":

    A = [1, 1, 3, 5,
         4, 3, 6, 2, 1]

    N = len(A)

    # Function call
    print (findLongestNonDecreasing(A, N));

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the length of the longest
// non-decreasing array that can be generated
static int findLongestNonDecreasing(int[] A,
                                    int N)
{

    // Stores the length of the longest
    // non-decreasing array that can be
    // generated from the array
    int res = 0; 

    // Stores index of
    // start pointer
    int start = 0;

    // Stores index of
    // end pointer
    int end = N - 1;

    // Stores previously inserted
    // element into the new array
    int prev = -1;

    // Traverse the array
    while (start <= end)
    {

        // If A[start] is less than
        // or equal to A[end]
        if (A[start] <= A[end])
        {

            // If no element inserted into
            // the newly generated array
            if (prev == -1)
            {

                // Update prev
                prev = A[start];

                // Update res
                res++;

                // Update start
                start++;
            }
            else
            {

                // If A[start] is greater
                // than or equal to prev
                if (A[start] >= prev)
                {

                    // Update res
                    res++;

                    // Update prev
                    prev = A[start];

                    // Update start
                    start++;
                }

                //  If A[end] is greater
                // than or equal to prev
                else if (A[end] >= prev)
                {

                    // Update res
                    res++;

                    // Update prev
                    prev = A[end];

                    // Update end
                    end--;
                }
                else
                {
                    break;
                }
            }
        }

        // If A[end] is
        // greater than A[start]
        else
        {

            // If no element inserted into
            // the newly generated array
            if (prev == -1)
            {

                // Update prev
                prev = A[end];

                // Update res
                res++;

                // Update end
                end--;
            }
            else
            {

                // If A[end] is greater
                // than or equal to prev
                if (A[end] >= prev)
                {

                    // Update res
                    res++;

                    //Update prev
                    prev = A[end];

                    // Update end
                    end--;
                }

                // If A[start] is greater
                // than or equal to prev
                else if (A[start] >= prev)
                {

                    // Update res
                    res++;

                    //Update prev
                    prev = A[start];

                    // Update start
                    start++;
                }
                else
                {
                    break;
                }
            }
        }
    }
    return res;
}

// Driver Code
public static void Main()
{
    int[] A = { 1, 1, 3, 5, 4, 3, 6, 2, 1 };

    int N = A.Length;

    // Function call
    Console.Write(findLongestNonDecreasing(A, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the length of the longest
// non-decreasing array that can be generated
function findLongestNonDecreasing(A, N)
{

    // Stores the length of the longest
    // non-decreasing array that can be
    // generated from the array
    let res = 0;

    // Stores index of
    // start pointer
    let start = 0;

    // Stores index of
    // end pointer
    let end = N - 1;

    // Stores previously inserted
    // element into the new array
    let prev = -1;

    // Traverse the array
    while (start <= end)
    {

        // If A[start] is less than
        // or equal to A[end]
        if (A[start] <= A[end])
        {

            // If no element inserted into
            // the newly generated array
            if (prev == -1)
            {

                // Update prev
                prev = A[start];

                // Update res
                res++;

                // Update start
                start++;
            }
            else
            {

                // If A[start] is greater
                // than or equal to prev
                if (A[start] >= prev)
                {

                    // Update res
                    res++;

                    // Update prev
                    prev = A[start];

                    // Update start
                    start++;
                }

                //  If A[end] is greater
                // than or equal to prev
                else if (A[end] >= prev)
                {

                    // Update res
                    res++;

                    // Update prev
                    prev = A[end];

                    // Update end
                    end--;
                }
                else
                {
                    break;
                }
            }
        }

        // If A[end] is
        // greater than A[start]
        else
        {

            // If no element inserted into
            // the newly generated array
            if (prev == -1)
            {

                // Update prev
                prev = A[end];

                // Update res
                res++;

                // Update end
                end--;
            }
            else
            {

                // If A[end] is greater
                // than or equal to prev
                if (A[end] >= prev)
                {

                    // Update res
                    res++;

                    //Update prev
                    prev = A[end];

                    // Update end
                    end--;
                }

                // If A[start] is greater
                // than or equal to prev
                else if (A[start] >= prev)
                {

                    // Update res
                    res++;

                    //Update prev
                    prev = A[start];

                    // Update start
                    start++;
                }
                else
                {
                    break;
                }
            }
        }
    }
    return res;
}

    // Driver Code

    let A = [ 1, 1, 3, 5, 4, 3, 6, 2, 1 ];

    let N = A.length;

    // Function call
    document.write(findLongestNonDecreasing(A, N));

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*