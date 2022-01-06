# 左右下一个较大的指数的最大乘积

> 原文:[https://www . geeksforgeeks . org/左、右下一个更大索引的最大乘积/](https://www.geeksforgeeks.org/maximum-product-of-indexes-of-next-greater-on-left-and-right/)

给定数组 a[1..N]。对于位置 I 的每个元素(1 <= i <= N)。在哪里

1.  **L(i)** 被定义为最接近的指数 j，使得 j < i 和 a【j】>a【I】。如果不存在这样的 j，那么 **L(i) = 0** 。
2.  **R(i)** 被定义为最接近的指数 k，使得 k > i 和 a【k】>a【I】。如果不存在这样的 k，那么 **R(i) = 0** 。

**LRProduct(i) = L(i)*R(i)** 。
我们需要找到一个 LRProduct 最大的指数

**示例:**

> 输入:1 1 1 0 1 1 1 1 1
> 输出:24
> 对于{1，1，1，1，0，1，1，1，1，1，1}除了 0 之外，所有元素都相同。因此，只有对于零，它们存在更大的元素，而对于其他元素，它将是零。对于零，左边第 4 个元素最接近且大于零，右边第 6 个元素最接近且大于零。所以最大
> 积将是 4*6 = 24。
> 
> 输入:5 4 3 4 5
> 输出:8
> 对于{5，4，3，4，5}，L[] = {0，1，2，1，0}和 R[]
> = {0，5，4，5，0}，
> LRProduct = {0，5，8，5，0}，这里的最大值是 8。

**注:**以起始指数为 1 求 LRproduct。

这个问题基于[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)。
从目前的位置来看，我们需要在它的左右两侧找到最近的大元。
为了找到下一个更大的元素，我们使用了从左到右的堆栈 1。简单地说，我们正在检查哪个元素更大，并将它们的索引存储在指定的位置。
1-如果堆栈为空，则推送当前索引。
2-如果堆栈不为空
…。a)如果当前元素大于顶部元素，则将当前元素的索引存储在顶部元素的索引上。
这样做，一次从左遍历数组元素，一次从右遍历数组元素，形成左右数组，然后，相乘得到最大乘积值。

## C++

```
// C++ program to find the max
// LRproduct[i] among all i
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000

// function to find just next greater
// element in left side
vector<int> nextGreaterInLeft(int a[], int n)
{
    vector<int> left_index(MAX, 0);
    stack<int> s;

    for (int i = n - 1; i >= 0; i--) {

        // checking if current element is greater than top
        while (!s.empty() && a[i] > a[s.top() - 1]) {
            int r = s.top();
            s.pop();

            // on index of top store the current element
            // index which is just greater than top element
            left_index[r - 1] = i + 1;
        }

        // else push the current element in stack
        s.push(i + 1);
    }
    return left_index;
}

// function to find just next greater element
// in right side
vector<int> nextGreaterInRight(int a[], int n)
{
    vector<int> right_index(MAX, 0);
    stack<int> s;
    for (int i = 0; i < n; ++i) {

        // checking if current element is greater than top
        while (!s.empty() && a[i] > a[s.top() - 1]) {
            int r = s.top();
            s.pop();

            // on index of top store the current element
            // index which is just greater than top element
            // stored index should be start with 1
            right_index[r - 1] = i + 1;
        }

        // else push the current element in stack
        s.push(i + 1);
    }
    return right_index;
}

// Function to find maximum LR product
int LRProduct(int arr[], int n)
{
    // for each element storing the index of just
    // greater element in left side
    vector<int> left = nextGreaterInLeft(arr, n);

    // for each element storing the index of just
    // greater element in right side
    vector<int> right = nextGreaterInRight(arr, n);
    int ans = -1;
    for (int i = 1; i <= n; i++) {

        // finding the max index product
        ans = max(ans, left[i] * right[i]);
    }

    return ans;
}

// Drivers code
int main()
{
    int arr[] = { 5, 4, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[1]);

    cout << LRProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// max LRproduct[i] among all i
import java.io.*;
import java.util.*;

class GFG
{
    static int MAX = 1000;

    // function to find just next
    // greater element in left side
    static int[] nextGreaterInLeft(int []a,
                                   int n)
    {
        int []left_index = new int[MAX];
        Stack<Integer> s = new Stack<Integer>();

        for (int i = n - 1; i >= 0; i--)
        {

            // checking if current
            // element is greater than top
            while (s.size() != 0 &&
                     a[i] > a[s.peek() - 1])
            {
                int r = s.peek();
                s.pop();

                // on index of top store
                // the current element
                // index which is just
                // greater than top element
                left_index[r - 1] = i + 1;
            }

            // else push the current
            // element in stack
            s.push(i + 1);
        }
        return left_index;
    }

    // function to find just next
    // greater element in right side
    static int[] nextGreaterInRight(int []a,
                                    int n)
    {
        int []right_index = new int[MAX];
        Stack<Integer> s = new Stack<Integer>();
        for (int i = 0; i < n; ++i) {

            // checking if current element
            // is greater than top
            while (s.size() != 0 &&
                        a[i] > a[s.peek() - 1])
            {
                int r = s.peek();
                s.pop();

                // on index of top store
                // the current element index
                // which is just greater than
                // top element stored index
                // should be start with 1
                right_index[r - 1] = i + 1;
            }

            // else push the current
            // element in stack
            s.push(i + 1);
        }
        return right_index;
    }

    // Function to find
    // maximum LR product
    static int LRProduct(int []arr, int n)
    {

        // for each element storing
        // the index of just greater
        // element in left side
        int []left = nextGreaterInLeft(arr, n);

        // for each element storing
        // the index of just greater
        // element in right side
        int []right = nextGreaterInRight(arr, n);
        int ans = -1;
        for (int i = 1; i <= n; i++)
        {

            // finding the max
            // index product
            ans = Math.max(ans, left[i] *
                                right[i]);
        }

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int []arr = new int[]{ 5, 4, 3, 4, 5 };
        int n = arr.length;

        System.out.print(LRProduct(arr, n));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to find the 
# max LRproduct[i] among all i

# Method to find the next greater
# value in left side
def nextGreaterInLeft(a):

    left_index = [0] * len(a)
    s = []

    for i in range(len(a)):

        # Checking if current
        # element is greater than top
        while len(s) != 0 and a[i] >= a[s[-1]]:

            # Pop the element till we can't
            # get the larger value then
            # the current value
            s.pop()

        if len(s) != 0:
            left_index[i] = s[-1]
        else:
            left_index[i] = 0

        # Else push the element in the stack
        s.append(i)

    return left_index

# Method to find the next
# greater value in right
def nextGreaterInRight(a):

    right_index = [0] * len(a)
    s = []

    for i in range(len(a) - 1, -1, -1):

        # Checking if current element
        # is greater than top
        while len(s) != 0 and a[i] >= a[s[-1]]:

            # Pop the element till we can't
            # get the larger value then
            # the current value
            s.pop()

        if len(s) != 0:
            right_index[i] = s[-1]
        else:
            right_index[i] = 0

        # Else push the element in the stack
        s.append(i)

    return right_index

def LRProduct(arr):

    # For each element storing
    # the index of just greater
    # element in left side
    left = nextGreaterInLeft(arr)

    # For each element storing
    # the index of just greater
    # element in right side
    right = nextGreaterInRight(arr)

    ans = -1

    # As we know the answer will
    # belong to the range from
    # 1st index to second last index.
    # Because for 1st index left
    # will be 0 and for last
    # index right will be 0
    for i in range(1, len(left) - 1):

        if left[i] == 0 or right[i] == 0:

            # Finding the max index product
            ans = max(ans, 0)
        else:
            temp = (left[i] + 1) * (right[i] + 1)

            # Finding the max index product
            ans = max(ans, temp)

    return ans

# Driver Code
arr = [ 5, 4, 3, 4, 5 ]

print(LRProduct(arr))

# This code is contributed by Mohit Pathneja
```

## C#

```
// C# program to find the max LRproduct[i]
// among all i
using System;
using System.Collections.Generic;

class GFG {

    static int MAX = 1000;

    // function to find just next greater
    // element in left side
    static int[] nextGreaterInLeft(int []a, int n)
    {
        int []left_index = new int[MAX];
        Stack<int> s = new Stack<int>();

        for (int i = n - 1; i >= 0; i--) {

            // checking if current element is
            // greater than top
            while (s.Count != 0 && a[i] > a[s.Peek() - 1])
            {
                int r = s.Peek();
                s.Pop();

                // on index of top store the current
                // element index which is just greater
                // than top element
                left_index[r - 1] = i + 1;
            }

            // else push the current element in stack
            s.Push(i + 1);
        }
        return left_index;
    }

    // function to find just next greater element
    // in right side
    static int[] nextGreaterInRight(int []a, int n)
    {
        int []right_index = new int[MAX];
        Stack<int> s = new Stack<int>();
        for (int i = 0; i < n; ++i) {

            // checking if current element is
            // greater than top
            while (s.Count != 0 && a[i] > a[s.Peek() - 1])
            {
                int r = s.Peek();
                s.Pop();

                // on index of top store the current
                // element index which is just greater
                // than top element stored index should
                // be start with 1
                right_index[r - 1] = i + 1;
            }

            // else push the current element in stack
            s.Push(i + 1);
        }
        return right_index;
    }

    // Function to find maximum LR product
    static int LRProduct(int []arr, int n)
    {

        // for each element storing the index of just
        // greater element in left side
        int []left = nextGreaterInLeft(arr, n);

        // for each element storing the index of just
        // greater element in right side
        int []right = nextGreaterInRight(arr, n);
        int ans = -1;
        for (int i = 1; i <= n; i++) {

            // finding the max index product
            ans = Math.Max(ans, left[i] * right[i]);
        }

        return ans;
    }

    // Drivers code
    static void Main()
    {
        int []arr = new int[]{ 5, 4, 3, 4, 5 };
        int n = arr.Length;

        Console.Write(LRProduct(arr, n));
    }
}

// This code is contributed by Manish Shaw
```

## java 描述语言

```
<script>
    // Javascript program to find the max LRproduct[i] among all i

    let MAX = 1000;

    // function to find just next greater
    // element in left side
    function nextGreaterInLeft(a, n)
    {
        let left_index = new Array(MAX);
        left_index.fill(0);
        let s = [];

        for (let i = n - 1; i >= 0; i--) {

            // checking if current element is
            // greater than top
            while (s.length != 0 && a[i] > a[s[s.length - 1] - 1])
            {
                let r = s[s.length - 1];
                s.pop();

                // on index of top store the current
                // element index which is just greater
                // than top element
                left_index[r - 1] = i + 1;
            }

            // else push the current element in stack
            s.push(i + 1);
        }
        return left_index;
    }

    // function to find just next greater element
    // in right side
    function nextGreaterInRight(a, n)
    {
        let right_index = new Array(MAX);
        right_index.fill(0);
        let s = [];
        for (let i = 0; i < n; ++i) {

            // checking if current element is
            // greater than top
            while (s.length != 0 && a[i] > a[s[s.length - 1] - 1])
            {
                let r = s[s.length - 1];
                s.pop();

                // on index of top store the current
                // element index which is just greater
                // than top element stored index should
                // be start with 1
                right_index[r - 1] = i + 1;
            }

            // else push the current element in stack
            s.push(i + 1);
        }
        return right_index;
    }

    // Function to find maximum LR product
    function LRProduct(arr, n)
    {

        // for each element storing the index of just
        // greater element in left side
        let left = nextGreaterInLeft(arr, n);

        // for each element storing the index of just
        // greater element in right side
        let right = nextGreaterInRight(arr, n);
        let ans = -1;
        for (let i = 1; i <= n; i++) {

            // finding the max index product
            ans = Math.max(ans, left[i] * right[i]);
        }

        return ans;
    }

    let arr = [ 5, 4, 3, 4, 5 ];
    let n = arr.length;

    document.write(LRProduct(arr, n));

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
8
```

**<u>方法 2:</u>** 通过仅使用一个数组来存储左右最大值，从而减少使用的空间。

**进场:**

先决条件:https://www.geeksforgeeks.org/next-greater-element/

*   为了找到左边的下一个更大的元素，我们使用了从左边开始的堆栈，相同的堆栈用于将右边最大的元素索引乘以左边最大的元素索引。
*   函数 maxProduct()用于通过迭代结果数组返回最大乘积。

## C++

```
// C++ program to find max LR product
#include <bits/stdc++.h>
using namespace std;

stack<int> mystack;

// To find greater element to left
void nextGreaterToLeft(int arr[], int res[], int N) {
    mystack.push(0);
    res[0] = 0;

    // iterate through the array
    for(int i = 1; i < N; i++) {
        while(mystack.size() > 0  &&  arr[mystack.top()] <= arr[i])
            mystack.pop();

        // place the index to the left in the resultant array
        res[i] = (mystack.size() == 0) ? 0 : mystack.top()+1;
        mystack.push(i);
    }
}

//// To find greater element to right
void nextGreaterToRight(int arr[], int res[], int N) {
    mystack = stack<int>();

    int n = N;
    mystack.push(n-1);
    res[n-1] *= 0;

    // iterate through the array in the reverse order
    for(int i=n - 2 ; i >= 0; i--) {
        while(mystack.size() > 0  &&  arr[mystack.top()] <= arr[i])
            mystack.pop();

        //multiply the index to the right with the index to the left
        //in the resultant array
        res[i] = (mystack.size() == 0) ? res[i]*0 : res[i]*(mystack.top()+1);
        mystack.push(i);
    }
}

//function to return the max value in the resultant array
int maxProduct(int arr[], int res[], int N) {
    nextGreaterToLeft(arr,res, N);        //to find left max
    nextGreaterToRight(arr,res, N);    //to find right max

    int Max = res[0];
    for(int i = 1; i < N; i++){
        Max = max(Max, res[i]);
    }
    return Max;
}

int main()
{
    int arr[] = {5, 4, 3, 4, 5};
    int N = sizeof(arr) / sizeof(arr[0]);
    int res[N];

    int maxprod = maxProduct(arr, res, N);
    cout << maxprod << endl;

    return 0;
}

// This code is contributed by decode2207.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//java program to find max LR product

import java.util.*;

public class GFG {
    Stack<Integer> mystack = new Stack<>();

    //To find greater element to left
    void nextGreaterToLeft(int[] arr,int[] res) {
        mystack.push(0);
        res[0] = 0;

        //iterate through the array
        for(int i=1;i<arr.length;i++) {
            while(!mystack.isEmpty()  &&  arr[mystack.peek()] <= arr[i])
                mystack.pop();

            //place the index to the left in the resultant array
            res[i] = (mystack.isEmpty()) ? 0 : mystack.peek()+1;
            mystack.push(i);
        }
    }

    ////To find greater element to right
    void nextGreaterToRight(int[] arr,int[] res) {
        mystack.clear();

        int n = arr.length;
        mystack.push(n-1);
        res[n-1] *= 0;

        //iterate through the array in the reverse order
        for(int i=n-2;i>=0;i--) {
            while(!mystack.isEmpty()  &&  arr[mystack.peek()] <= arr[i])
                mystack.pop();

            //multiply the index to the right with the index to the left
            //in the resultant array
            res[i] = (mystack.isEmpty()) ? res[i]*0 : res[i]*(mystack.peek()+1);
            mystack.push(i);
        }
    }

    //function to return the max value in the resultant array
    int maxProduct(int[] arr,int[] res) {
        nextGreaterToLeft(arr,res);        //to find left max
        nextGreaterToRight(arr,res);    //to find right max

        int max = res[0];
        for(int i = 1;i<res.length;i++){
            max = Math.max(max, res[i]);
        }
        return max;
    }

    //Driver function
    public static void main(String args[]) {
        GFG obj = new GFG();
        int arr[] = {5, 4, 3, 4, 5};
        int res[] = new int[arr.length];

        int maxprod = obj.maxProduct(arr, res);
        System.out.println(maxprod);
    }
}

//this method is contributed by Likhita AVL
```

## 蟒蛇 3

```
# Python3 program to find max LR product
mystack = []

# To find greater element to left
def nextGreaterToLeft(arr, res):
    mystack.append(0)
    res[0] = 0

    # iterate through the array
    for i in range(1, len(arr)):
        while(len(mystack) > 0  and arr[mystack[-1]] <= arr[i]):
            mystack.pop()

        # place the index to the left in the resultant array
        if (len(mystack) == 0):
            res[i] = 0
        else:
            res[i] = mystack[-1]+1
        mystack.append(i)

# To find greater element to right
def nextGreaterToRight(arr, res):
    mystack = []

    n = len(arr)
    mystack.append(n-1)
    res[n-1] *= 0

    # iterate through the array in the reverse order
    for i in range(n - 2, -1, -1):
        while(len(mystack) > 0  and arr[mystack[-1]] <= arr[i]):
            mystack.pop()

        # multiply the index to the right with the index to the left
        # in the resultant array
        if (len(mystack) == 0):
            res[i] = res[i]*0
        else :
            res[i] = res[i]*(mystack[-1]+1)
        mystack.append(i)

# function to return the max value in the resultant array
def maxProduct(arr, res):
    nextGreaterToLeft(arr,res)       #to find left max
    nextGreaterToRight(arr,res)      #to find right max

    Max = res[0]
    for i in range(1, len(res)):
        Max = max(Max, res[i])
    return Max

  # Driver code
arr = [5, 4, 3, 4, 5]
res = [0]*(len(arr))

maxprod = maxProduct(arr, res)
print(maxprod)

# This code is contributed by mukesh07.
```

## C#

```
// C# program to find max LR product
using System;
using System.Collections;
class GFG {

    static Stack mystack = new Stack();

    //To find greater element to left
    static void nextGreaterToLeft(int[] arr,int[] res) {
        mystack.Push(0);
        res[0] = 0;

        //iterate through the array
        for(int i=1;i<arr.Length;i++) {
            while(mystack.Count > 0  &&  arr[(int)mystack.Peek()] <= arr[i])
                mystack.Pop();

            //place the index to the left in the resultant array
            res[i] = (mystack.Count == 0) ? 0 : (int)mystack.Peek()+1;
            mystack.Push(i);
        }
    }

    ////To find greater element to right
    static void nextGreaterToRight(int[] arr,int[] res) {
        mystack = new Stack();

        int n = arr.Length;
        mystack.Push(n-1);
        res[n-1] *= 0;

        //iterate through the array in the reverse order
        for(int i = n - 2; i >= 0; i--) {
            while(mystack.Count == 0  &&  arr[(int)mystack.Peek()] <= arr[i])
                mystack.Pop();

            //multiply the index to the right with the index to the left
            //in the resultant array
            res[i] = (mystack.Count == 0) ? res[i]*0 : res[i]*((int)mystack.Peek()+1);
            mystack.Push(i);
        }
    }

    //function to return the max value in the resultant array
    static int maxProduct(int[] arr,int[] res) {
        nextGreaterToLeft(arr, res);        //to find left max
        nextGreaterToRight(arr, res);    //to find right max

        int max = res[0];
        for(int i = 1; i < res.Length; i++){
            max = Math.Max(max, res[i]);
        }
        return max;
    }

  static void Main() {
    int[] arr = {5, 4, 3, 4, 5};
    int[] res = new int[arr.Length];

    int maxprod = maxProduct(arr, res);
    Console.WriteLine(maxprod);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program to find max LR product

    let mystack = [];

    // To find greater element to left
    function nextGreaterToLeft(arr, res) {
        mystack.push(0);
        res[0] = 0;

        // iterate through the array
        for(let i = 1; i < arr.length; i++) {
            while(mystack.length > 0  &&  arr[mystack[mystack.length - 1]] <= arr[i])
                mystack.pop();

            // place the index to the left in the resultant array
            res[i] = (mystack.length == 0) ? 0 : mystack[mystack.length - 1]+1;
            mystack.push(i);
        }
    }

    //// To find greater element to right
    function nextGreaterToRight(arr, res) {
        mystack = [];

        let n = arr.length;
        mystack.push(n-1);
        res[n-1] *= 0;

        // iterate through the array in the reverse order
        for(let i = n - 2; i >= 0; i--) {
            while(mystack.length > 0  &&  arr[mystack[mystack.length - 1]] <= arr[i])
                mystack.pop();

            // multiply the index to the right with the index to the left
            // in the resultant array
            res[i] = (mystack.length == 0) ? res[i]*0 : res[i]*(mystack[mystack.length - 1]+1);
            mystack.push(i);
        }
    }

    // function to return the max value in the resultant array
    function maxProduct(arr, res) {
        nextGreaterToLeft(arr,res);        //to find left max
        nextGreaterToRight(arr,res);    //to find right max

        let max = res[0];
        for(let i = 1;i<res.length;i++){
            max = Math.max(max, res[i]);
        }
        return max;
    }

    let arr = [5, 4, 3, 4, 5];
    let res = new Array(arr.length);

    let maxprod = maxProduct(arr, res);
    document.write(maxprod);

    // This code is contributed by divyesh072019.
</script>
```

**Output**

```
8
```

**时间复杂度:** O(n)