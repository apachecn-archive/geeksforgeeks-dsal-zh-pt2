# 返回主文件夹所需的最小操作次数

> 原文:[https://www . geesforgeks . org/返回主文件夹所需的最小操作数/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-return-to-the-main-folder/)

给定一个由[字符串](https://www.geeksforgeeks.org/string-data-structure/)**arr【】**组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)，表示在文件系统上执行的已更改文件夹操作(Unix 风格)。最初，文件系统在主文件夹中打开。任务是找到返回主文件夹的以下三种操作的最小计数:

*   **”../:**移动到当前文件夹的父文件夹。(如果当前文件夹是主文件夹，它将保持在同一文件夹中)。
*   **”。/:**保留在同一个文件夹中。
*   **“F/”:**移动到名为 F 的子文件夹

**示例:**

> **输入:**arr[]= {“F1/”、“F2/”、“”。/，“F3/”../，“F31/”}
> T3】输出: 3
> **解释:**
> arr[0]=“F1/”。移动到名为 F1 的子文件夹。因此，当前目录的路径是/F1。
> arr[1]=“F2/”。移动到名为 F2 的子文件夹。因此，当前目录的路径是/F1/F2
> arr[2] =”。/" .保留在当前文件夹中。因此，当前目录的路径为/F1/F2
> arr[3]=“F3/”。移动到孩子的文件夹，命名为 F3。因此，当前目录的路径是/F1/F2/F3
> arr[4] =”../".移动到 F3 的父文件夹。因此，当前目录的路径为/F1/F2
> arr[5]“F31/”。移动到孩子的文件夹，命名为 F31。因此，当前目录的路径是/F1/F2/F31
> 现在，该“../"操作需要执行三次才能返回主文件夹。
> 因此，要求输出为 3。
> 
> **输入:** arr[] = {"F1/"，"../", "../}
> **输出:** 0
> **解释:**
> arr[0]=“F1/”。因此，当前目录的路径是/F1。
> arr[1] = "../".因此，当前目录的路径是/
> arr[2] =”../".因此，当前目录的路径是/
> 由于目录的当前路径已经在主文件夹中，因此不需要任何操作。因此，所需的输出为 0。

**方法:**使用[栈](https://www.geeksforgeeks.org/stack-in-cpp-stl/)可以解决问题。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntOp** 来存储返回主文件夹所需的最小操作数。
*   创建一个[栈](https://www.geeksforgeeks.org/stack-in-cpp-stl/)，比如 **st** 来存储当前文件夹的路径
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件:
    *   如果 **arr[i] ==”../**然后弹出栈顶元素。
    *   如果**arr[I]= =“F/”**那么将 **arr[i]** 的值推至栈顶。
*   最后，打印堆栈上剩余的元素数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of
// operations to go back to main folder
int minOperations(vector<string>& arr,
                               int N)
{
    // Stores path of
    // the current folder
    stack<string> st;

    for (int i = 0; i < N; i++) {

        // If stack is not empty and
        // the value of arr[i] is "../"
        if (arr[i] == "../" &&
                      !st.empty()) {

            // Pop top element of
            // the stack             
            st.pop();
        }

        // If the value of arr[i]
        // is like "F/"
        else if (arr[i] != "./") {

            // Push arr[i] on top element
            // of the stack              
            st.push(arr[i]);
        }
    }

    // Return count of elements left
    // into the stack
    return st.size();
}

// Driver Code
int main()
{
    vector<string> arr
        = { "F1/", "F2/", "./",
          "F3/", "../", "F31/" };
    int N = arr.size();
    cout << minOperations(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find minimum number of
// operations to go back to main folder
static int minOperations(String []arr, int N)
{

    // Stores path of
    // the current folder
    Stack<String> st = new Stack<>();

    for(int i = 0; i < N; i++)
    {

        // If stack is not empty and
        // the value of arr[i] is "../"
        if (arr[i] == "../" && !st.empty())
        {

            // Pop top element of
            // the stack             
            st.pop();
        }

        // If the value of arr[i]
        // is like "F/"
        else if (arr[i] != "./")
        {

            // Push arr[i] on top element
            // of the stack              
            st.push(arr[i]);
        }
    }

    // Return count of elements left
    // into the stack
    return st.size();
}

// Driver Code
public static void main(String args[])
{
    String []arr = { "F1/", "F2/", "./",
                     "F3/", "../", "F31/" };

    int N = arr.length;

    System.out.print(minOperations(arr, N));
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find minimum number of
# operations to go back to main folder
def minOperations(arr, N):

    # Stores path of
    # the current folder
    st = []

    for i in range(N):

        # If stack is not empty and
        # the value of arr[i] is "../"
        if (arr[i] == "../" and len(st) != 0):

            # Pop top element of
            # the stack
            st.pop(-1)

        # If the value of arr[i]
        # is like "F/"
        elif (arr[i] != "./"):

            # Push arr[i] on top element
            # of the stack
            st.append(arr[i])

    # Return count of elements left
    # into the stack
    return len(st)

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [ "F1/", "F2/", "./",
            "F3/", "../", "F31/" ]

    # Size of the array
    N = len(arr)

    # Function Call
    print(minOperations(arr, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find minimum
// number of operations to
// go back to main folder
static int minOperations(String []arr,
                         int N)
{   
  // Stores path of
  // the current folder
  Stack<String> st =
        new Stack<String>();

  for(int i = 0; i < N; i++)
  {
    // If stack is not empty
    // and the value of arr[i]
    // is "../"
    if (arr[i] == "../" &&
        st.Count != 0)
    {
      // Pop top element of
      // the stack             
      st.Pop();
    }

    // If the value of arr[i]
    // is like "F/"
    else if (arr[i] != "./")
    {

      // Push arr[i] on top
      // element of the stack              
      st.Push(arr[i]);
    }
  }

  // Return count of elements
  // left into the stack
  return st.Count;
}

// Driver Code
public static void Main(String []args)
{
  String []arr = {"F1/", "F2/", "./",
                  "F3/", "../", "F31/"};
  int N = arr.Length;
  Console.Write(minOperations(arr, N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
//Javascript  program to implement
// the above approach

// Function to find minimum number of
// operations to go back to main folder
function minOperations(arr, N)
{
    // Stores path of
    // the current folder
    st = [];

    for (var i = 0; i < N; i++) {

        // If stack is not empty and
        // the value of arr[i] is "../"
        if (arr[i] == "../" && (st.length-1) !== 0) {

            // Pop top element of
            // the stack             
            st.pop();
        }

        // If the value of arr[i]
        // is like "F/"
        else if (arr[i] != "./") {

            // Push arr[i] on top element
            // of the stack              
            st.push(arr[i]);
        }
    }

    // Return count of elements left
    // into the stack
    return st.length;
}

var arr = [ "F1/", "F2/", "./", "F3/", "../", "F31/" ];
var N = arr.length;
document.write( minOperations(arr, N));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)