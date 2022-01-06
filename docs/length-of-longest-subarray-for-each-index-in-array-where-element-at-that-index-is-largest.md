# 数组中每个索引的最长子数组长度，其中该索引处的元素最大

> 原文:[https://www . geeksforgeeks . org/数组中每个索引的最长子数组长度，其中索引处的元素最大/](https://www.geeksforgeeks.org/length-of-longest-subarray-for-each-index-in-array-where-element-at-that-index-is-largest/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是为 i(0 < =i < N)计算包含 **arr[i]，**的子数组的最大长度，其中 **arr[i]** 是最大元素。

**示例:**

> **输入:** arr[ ] = {62，97，49，59，54，92，21}，N=7
> **输出:**
> 1 7 1 3 1 5 1
> **说明:**第 1 个指标元素最大的子阵最大长度为 1，子阵仅由第 1 个元素组成。
> 对于第二个元素，即 97，子阵列的最大长度= 7。我们可以观察到 97 是数组 a 中的最大元素。
> 对于第三个元素，子数组中只能有 49 个。因此，最大可能长度= 1。
> 对于第四个元素，子阵列[49，59，54]是可能的，其中 59 是最大数量。因此，长度= 3。
> 同样，我们为数组中的每个索引进行计算。
> 
> **输入:** arr[]={1，4，5，2，3}
> **输出:**
> 1 2 5 1 2

**天真方法:**

1.  对于每个索引**‘I’**，遍历数组的两侧，直到找到一个大于**arr【I】**的元素。
2.  计算范围内元素的数量，这将是子阵列的最大长度，其中 **arr[i]** 是最大的元素。

***时间复杂度:** O(N <sup>2</sup> )，*

**高效方法:**想法是使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)数据结构为每个索引计算[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)(一个在左边，一个在右边)。

**例如**

> 设 **arr[]={1，3，1，2，1，5}，**为 **i=3** ，左边下一个较大的元素在**索引 1**
> 处，右边在**索引 5** 处。
> 因此，其中最大的子阵列的长度是 **5-1-1=3** ，即从**索引 2 到 4** 或 **{1，2，1}**

按照以下步骤解决问题:

1.  为每个索引找到下一个较大元素的索引，并使用每个 **i(0 < =i < N)的[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)将其存储在数组中。**
2.  同样，将每个索引的下一个较大的元素存储在数组的左侧。
3.  遍历数组，对于每个索引， **i** ，打印左侧下一个较大元素和右侧下一个较大元素之间的元素数量。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to compute
// next greater element indices on the
// right side on any index
vector<int> rightGreaterElement(int arr[], int n)
{
    // to store the elements of array arr
    // with their index
    vector<pair<int, int> > B(n);
    for (int i = 0; i < n; i++) {
        B[i].first = arr[i];
        B[i].second = i;
    }

    // to store indices of next greater element
    // on the right side
    vector<int> vec(n, -1);

    // to store the pairs
    stack<pair<int, int> > st;
    for (int i = 0; i < n; i++) {

        // if the stack is empty,
        // push the pair
        if (st.empty()) {
            st.push(B[i]);
        }
        else {

            // Pop and assign till
            // the top is smaller
            while (!st.empty()
                   && st.top().first < B[i].first) {
                vec[st.top().second] = B[i].second;
                st.pop();
            }
            st.push(B[i]);
        }
    }

    // assign n to element
    // having no next greater element
    while (!st.empty()) {
        vec[st.top().second] = n;
        st.pop();
    }

    // return the vector
    return vec;
}

// Function to compute next greater element
// indices on the left side on any index
vector<int> leftGreaterElement(int arr[], int n)
{
    // store the elements of array arr
    // with their index
    vector<pair<int, int> > B(n);
    for (int i = 0; i < n; i++) {
        B[i].first = arr[i];
        B[i].second = i;
    }

    // array to store indices of next
    // greater element on the left side
    vector<int> vec(n, -1);

    // stack to store the pairs
    stack<pair<int, int> > st;

    for (int i = n - 1; i >= 0; i--) {

        // if the stack is empty, push the pair
        if (st.empty()) {
            st.push(B[i]);
        }
        else {

            // pop and assign till top is smaller
            while (!st.empty()
                   && st.top().first < B[i].first) {
                vec[st.top().second] = B[i].second;
                st.pop();
            }
            st.push(B[i]);
        }
    }

    // assign -1 to element having
    // no next greater element
    while (!st.empty()) {
        vec[st.top().second] = -1;
        st.pop();
    }

    // returning the vector
    // with indices of next greater
    // elements on the left side.
    return vec;
}

// Function to print the maximum
// length of subarrays for all
// indices where A[i] is the
// maximum element in the subarray
void maximumSubarrayLength(int arr[], int N)
{
    // array having index of next
    // greater element on the right side.
    vector<int> right = rightGreaterElement(arr, N);

    // array having index of next
    // greater element on the left side.
    vector<int> left = leftGreaterElement(arr, N);

    // print the range between the
    // next greater elements on both the sides.
    for (int i = 0; i < N; i++) {
        int l = left[i];
        int r = right[i];
        cout << r - l - 1 << " ";
    }
}

// Driver code
int main()
{
    // Input
    int arr[] = { 62, 97, 49, 59, 54, 92, 21 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    maximumSubarrayLength(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;
import java.awt.Point;
public class Main
{
    // Function to compute
    // next greater element indices on the
    // right side on any index
    static int[] rightGreaterElement(int[] arr, int n)
    {

        // to store the elements of array arr
        // with their index
        int[][] B = new int[n][2];
        for (int i = 0; i < n; i++) {
            B[i][0] = arr[i];
            B[i][1] = i;
        }

        // to store indices of next greater element
        // on the right side
        int[] vec = new int[n];
        Arrays.fill(vec, -1);

        // to store the pairs
        Stack<Point> st = new Stack<Point>();
        for (int i = 0; i < n; i++) {

            // if the stack is empty,
            // push the pair
            if (st.size() == 0) {
                st.push(new Point(B[i][0], B[i][1]));
            }
            else {

                // Pop and assign till
                // the top is smaller
                while (st.size() > 0 && (st.peek()).x < B[i][0]) {
                    vec[(st.peek()).y] = B[i][1];
                    st.pop();
                }
                st.push(new Point(B[i][0], B[i][1]));
            }
        }

        // assign n to element
        // having no next greater element
        while (st.size() > 0) {
            vec[(st.peek()).y] = n;
            st.pop();
        }

        // return the vector
        return vec;
    }

    // Function to compute next greater element
    // indices on the left side on any index
    static int[] leftGreaterElement(int[] arr, int n)
    {
        // store the elements of array arr
        // with their index
        int[][] B = new int[n][2];
        for (int i = 0; i < n; i++) {
            B[i][0] = arr[i];
            B[i][1] = i;
        }

        // array to store indices of next
        // greater element on the left side
        int[] vec = new int[n];
        Arrays.fill(vec, -1);

        // stack to store the pairs
        Stack<Point> st = new Stack<Point>();

        for (int i = n - 1; i >= 0; i--) {

            // if the stack is empty, push the pair
            if (st.size() == 0) {
                st.push(new Point(B[i][0], B[i][1]));
            }
            else {

                // pop and assign till top is smaller
                while (st.size() > 0 && (st.peek()).x < B[i][0]) {
                    vec[(st.peek()).y] = B[i][1];
                    st.pop();
                }
                st.push(new Point(B[i][0], B[i][1]));
            }
        }

        // assign -1 to element having
        // no next greater element
        while (st.size() > 0) {
            vec[(st.peek()).y] = -1;
            st.pop();
        }

        // returning the vector
        // with indices of next greater
        // elements on the left side.
        return vec;
    }

    // Function to print the maximum
    // length of subarrays for all
    // indices where A[i] is the
    // maximum element in the subarray
    static void maximumSubarrayLength(int[] arr, int N)
    {
        // array having index of next
        // greater element on the right side.
        int[] right = rightGreaterElement(arr, N);

        // array having index of next
        // greater element on the left side.
        int[] left = leftGreaterElement(arr, N);

        // print the range between the
        // next greater elements on both the sides.
        for (int i = 0; i < N; i++) {
            int l = left[i];
            int r = right[i];
            System.out.print((r - l - 1) + " ");
        }
    }

    public static void main(String[] args) {
        // Input
        int[] arr = { 62, 97, 49, 59, 54, 92, 21 };
        int N = arr.length;

        // Function call
        maximumSubarrayLength(arr, N);
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to compute next greater
# element indices on the right side
# on any index
def rightGreaterElement(arr, n):

    # To store the elements of array arr
    # with their index
    B = [[0, 0] for i in range(n)]

    for i in range(n):
        B[i][0] = arr[i]
        B[i][1] = i

    # To store indices of next greater element
    # on the right side
    vec = [-1 for i in range(n)]

    # To store the pairs
    st = []
    for i in range(n):

        # If the stack is empty,
        # push the pair
        if (len(st) == 0):
            st.append(B[i])
        else:

            # Pop and assign till
            # the top is smaller
            while (len(st) > 0 and st[-1][0] < B[i][0]):
                vec[st[-1][1]] = B[i][1]
                st.pop()

            st.append(B[i])

    # Assign n to element
    # having no next greater element
    while (len(st) > 0):
        vec[st[-1][1]] = n
        st.pop()

    # Return the vector
    return vec

# Function to compute next greater element
# indices on the left side on any index
def leftGreaterElement(arr, n):

    # Store the elements of array arr
    # with their index
    B = [[0,0] for i in range(n)]
    for i in range(n):
        B[i][0] = arr[i]
        B[i][1] = i

    # Array to store indices of next
    # greater element on the left side
    vec = [-1 for i in range(n)]

    # Stack to store the pairs
    st = []

    i = n - 1

    while(i >= 0):

        # If the stack is empty, push the pair
        if (len(st) == 0):
            st.append(B[i])
        else:

            # Pop and assign till top is smaller
            while (len(st) > 0 and st[-1][0] < B[i][0]):
                vec[st[-1][1]] = B[i][1]
                st.pop()

            st.append(B[i])

        i -= 1

    # Assign -1 to element having
    # no next greater element
    while (len(st) > 0):
        vec[st[-1][1]] = -1
        st.pop()

    # Returning the vector
    # with indices of next greater
    # elements on the left side.
    return vec

# Function to print the maximum
# length of subarrays for all
# indices where A[i] is the
# maximum element in the subarray
def maximumSubarrayLength(arr, N):

    # Array having index of next
    # greater element on the right side.
    right = rightGreaterElement(arr, N)

    # Array having index of next
    # greater element on the left side.
    left = leftGreaterElement(arr, N)

    # Print the range between the
    # next greater elements on both the sides.
    for i in range(N):
        l = left[i]
        r = right[i]
        print(r - l - 1, end = " ")

# Driver code
if __name__ == '__main__':

    # Input
    arr = [ 62, 97, 49, 59, 54, 92, 21 ]
    N = len(arr)

    # Function call
    maximumSubarrayLength(arr, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# code for the above approach
using System;
using System.Collections;
class GFG {

    // Function to compute
    // next greater element indices on the
    // right side on any index
    static int[] rightGreaterElement(int[] arr, int n)
    {
        // to store the elements of array arr
        // with their index
        int[,] B = new int[n,2];
        for (int i = 0; i < n; i++) {
            B[i,0] = arr[i];
            B[i,1] = i;
        }

        // to store indices of next greater element
        // on the right side
        int[] vec = new int[n];
        Array.Fill(vec, -1);

        // to store the pairs
        Stack st = new Stack();
        for (int i = 0; i < n; i++) {

            // if the stack is empty,
            // push the pair
            if (st.Count == 0) {
                st.Push(new Tuple<int,int>(B[i,0], B[i,1]));
            }
            else {

                // Pop and assign till
                // the top is smaller
                while (st.Count > 0
                       && ((Tuple<int,int>)st.Peek()).Item1 < B[i,0]) {
                    vec[((Tuple<int,int>)st.Peek()).Item2] = B[i,1];
                    st.Pop();
                }
                st.Push(new Tuple<int,int>(B[i,0], B[i,1]));
            }
        }

        // assign n to element
        // having no next greater element
        while (st.Count > 0) {
            vec[((Tuple<int,int>)st.Peek()).Item2] = n;
            st.Pop();
        }

        // return the vector
        return vec;
    }

    // Function to compute next greater element
    // indices on the left side on any index
    static int[] leftGreaterElement(int[] arr, int n)
    {
        // store the elements of array arr
        // with their index
        int[,] B = new int[n,2];
        for (int i = 0; i < n; i++) {
            B[i,0] = arr[i];
            B[i,1] = i;
        }

        // array to store indices of next
        // greater element on the left side
        int[] vec = new int[n];
        Array.Fill(vec, -1);

        // stack to store the pairs
        Stack st = new Stack();

        for (int i = n - 1; i >= 0; i--) {

            // if the stack is empty, push the pair
            if (st.Count == 0) {
                st.Push(new Tuple<int,int>(B[i,0], B[i,1]));
            }
            else {

                // pop and assign till top is smaller
                while (st.Count > 0
                       && ((Tuple<int,int>)st.Peek()).Item1 < B[i,0]) {
                    vec[((Tuple<int,int>)st.Peek()).Item2] = B[i,1];
                    st.Pop();
                }
                st.Push(new Tuple<int,int>(B[i,0], B[i,1]));
            }
        }

        // assign -1 to element having
        // no next greater element
        while (st.Count > 0) {
            vec[((Tuple<int,int>)st.Peek()).Item2] = -1;
            st.Pop();
        }

        // returning the vector
        // with indices of next greater
        // elements on the left side.
        return vec;
    }

    // Function to print the maximum
    // length of subarrays for all
    // indices where A[i] is the
    // maximum element in the subarray
    static void maximumSubarrayLength(int[] arr, int N)
    {
        // array having index of next
        // greater element on the right side.
        int[] right = rightGreaterElement(arr, N);

        // array having index of next
        // greater element on the left side.
        int[] left = leftGreaterElement(arr, N);

        // print the range between the
        // next greater elements on both the sides.
        for (int i = 0; i < N; i++) {
            int l = left[i];
            int r = right[i];
            Console.Write((r - l - 1) + " ");
        }
    }

  static void Main()
  {

    // Input
    int[] arr = { 62, 97, 49, 59, 54, 92, 21 };
    int N = arr.Length;

    // Function call
    maximumSubarrayLength(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to compute
// next greater element indices on the
// right side on any index
function rightGreaterElement(arr, n) {
    // to store the elements of array arr
    // with their index
    let B = new Array(n).fill(0).map(() => new Array(2).fill(0));
    for (let i = 0; i < n; i++) {
        B[i][0] = arr[i];
        B[i][1] = i;
    }

    // to store indices of next greater element
    // on the right side
    let vec = new Array(n).fill(-1);

    // to store the pairs
    let st = [];
    for (let i = 0; i < n; i++) {

        // if the stack is empty,
        // push the pair
        if (st.length == 0) {
            st.push(B[i]);
        }
        else {

            // Pop and assign till
            // the top is smaller
            while (st.length > 0
                && st[st.length - 1][0] < B[i][0]) {
                vec[st[st.length - 1][1]] = B[i][1];
                st.pop();
            }
            st.push(B[i]);
        }
    }

    // assign n to element
    // having no next greater element
    while (st.length > 0) {
        vec[st[st.length - 1][1]] = n;
        st.pop();
    }

    // return the vector
    return vec;
}

// Function to compute next greater element
// indices on the left side on any index
function leftGreaterElement(arr, n) {
    // store the elements of array arr
    // with their index
    let B = new Array(n).fill(0).map(() => new Array(2));
    for (let i = 0; i < n; i++) {
        B[i][0] = arr[i];
        B[i][1] = i;
    }

    // array to store indices of next
    // greater element on the left side
    let vec = new Array(n).fill(-1);

    // stack to store the pairs
    let st = [];

    for (let i = n - 1; i >= 0; i--) {

        // if the stack is empty, push the pair
        if (st.length == 0) {
            st.push(B[i]);
        }
        else {

            // pop and assign till top is smaller
            while (st.length > 0
                && st[st.length - 1][0] < B[i][0]) {
                vec[st[st.length - 1][1]] = B[i][1];
                st.pop();
            }
            st.push(B[i]);
        }
    }

    // assign -1 to element having
    // no next greater element
    while (st.length > 0) {
        vec[st[st.length - 1][1]] = -1;
        st.pop();
    }

    // returning the vector
    // with indices of next greater
    // elements on the left side.
    return vec;
}

// Function to print the maximum
// length of subarrays for all
// indices where A[i] is the
// maximum element in the subarray
function maximumSubarrayLength(arr, N)
{

    // array having index of next
    // greater element on the right side.
    let right = rightGreaterElement(arr, N);

    // array having index of next
    // greater element on the left side.
    let left = leftGreaterElement(arr, N);

    // print the range between the
    // next greater elements on both the sides.
    for (let i = 0; i < N; i++) {
        let l = left[i];
        let r = right[i];
        document.write(r - l - 1 + " ");
    }
}

// Driver code

// Input
let arr = [62, 97, 49, 59, 54, 92, 21];
let N = arr.length;

// Function call
maximumSubarrayLength(arr, N);

// This code is contributed by _saurabh_jaiswal.

</script>
```

**Output**

```
1 7 1 3 1 5 1 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)