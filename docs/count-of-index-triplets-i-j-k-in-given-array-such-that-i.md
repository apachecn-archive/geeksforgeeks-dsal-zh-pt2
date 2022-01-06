# 给定数组中索引三元组(I，j，k)的计数，使得 i

> Original:

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算三胞胎的数量，使得 **i < j < k 和 a【j】<a【k】<a【I】**。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** -1
> **说明:**没有所需类型的三元组。
> 
> **输入:** arr[] = {4，1，3，5}
> **输出:** 1
> **说明:**数组 a[]中有一个三元组:{4，1，3 }。
> 
> **输入:** arr[] = {2，1，-3，-2，5}
> **输出:** 2
> **说明:**有两个所需类型的三元组:{2，1，-3}、{1，-3，-2}

**天真方法:**使用三个循环检查**a【】**中所有可能的三胞胎，并计算**arr【】**中的三胞胎数量，使得 i < j < k 和 a【j】<a【k】<a【I】。下面是上述方法的实现。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

int findTriplets(int a[], int n)
{

    // To count desired triplets
    int cnt = 0;

    // Three loops to find triplets
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            for (int k = j + 1; k < n; k++)
            {

                if (a[j] < a[k] && a[k] < a[i])
                    cnt++;
            }
        }
    }

    // Return the number of triplets found
    return cnt;
}

// Driver code
int main()
{
    int a[] = {2, 1, -3, -2, 5};
    int n = sizeof(a) / sizeof(a[0]);

    cout << (findTriplets(a, n));
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.io.*;

class GFG {

    public static int findTriplets(int[] a)
    {

        // To count desired triplets
        int cnt = 0;

        // Three loops to find triplets
        for (int i = 0; i < a.length; i++) {
            for (int j = i + 1; j < a.length; j++) {
                for (int k = j + 1; k < a.length; k++) {

                    if (a[j] < a[k] && a[k] < a[i])
                        cnt++;
                }
            }
        }

        // Return the number of triplets found
        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 1, -3, -2, 5 };

        System.out.println(findTriplets(a));
    }
}
```

## 蟒蛇 3

```
# Python Program for above approach
def findTriplets(a):

  # To count desired triplets
  cnt = 0;

  # Three loops to find triplets
  for i in range(len(a)):
    for j in range(i + 1, len(a)):
      for k in range(j + 1, len(a)):
        if (a[j] < a[k] and a[k] < a[i]):
          cnt += 1

  # Return the number of triplets found
  return cnt;

# Driver code
a = [2, 1, -3, -2, 5];
print(findTriplets(a));

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# Program for above approach
using System;
public class GFG {

  public static int findTriplets(int[] a)
  {

    // To count desired triplets
    int cnt = 0;

    // Three loops to find triplets
    for (int i = 0; i < a.Length; i++) {
      for (int j = i + 1; j < a.Length; j++) {
        for (int k = j + 1; k < a.Length; k++) {

          if (a[j] < a[k] && a[k] < a[i])
            cnt++;
        }
      }
    }

    // Return the number of triplets found
    return cnt;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int []a = { 2, 1, -3, -2, 5 };

    Console.WriteLine(findTriplets(a));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Program for above approach
function findTriplets(a) {

  // To count desired triplets
  let cnt = 0;

  // Three loops to find triplets
  for (let i = 0; i < a.length; i++) {
    for (let j = i + 1; j < a.length; j++) {
      for (let k = j + 1; k < a.length; k++) {

        if (a[j] < a[k] && a[k] < a[i])
          cnt++;
      }
    }
  }

  // Return the number of triplets found
  return cnt;
}

// Driver code

let a = [2, 1, -3, -2, 5];

document.write(findTriplets(a));

// This code is contributed by gfgking.
</script>
```

**Output**

```
2
```

**时间复杂度:**O(N<sup>3</sup>)
T5】辅助空间: O(1)

**高效途径:**可以使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)来优化上述解决方案。堆栈将跟踪右侧的下一个较小的和第二个较小的元素。

按照以下步骤解决给定的问题。

*   创建一个**栈**和变量 say**second min****= INT _ MAX**。
*   声明一个变量，比如 **cnt = 0** ，来存储想要的三元组的数量。
*   从数组的末尾**a【】**开始移动。
    *   检查当前元素是否大于 **secondMin** ，如果是，说明找到了需要的三元组，因为****栈**正在跟踪下一个较小的和第二个较小的元素，当前元素满足类型。然后，设置 **cnt = cnt + 1** 。**
    *   **如果不满足以上条件，更新**栈**中的最小值，继续弹出直到**栈**不为空或者当前元素不小于**栈**的顶部。**
    *   **将电流元件推入**堆栈****
*   **最后返回 **cnt** 作为找到的三胞胎数量。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find desired triplets
int findTriplets(vector<int>& a)
{

    // To store the number of triplets found
    int cnt = 0;

    stack<int> st;

    // Keep track of second minimum element
    int secondMin = INT_MAX;

    for (int i = a.size() - 1; i >= 0; i--) {

        // If required triplet is found
        if (a[i] > secondMin)
            cnt++;

        while (!st.empty() && st.top() > a[i]) {

            secondMin = st.top();
            st.pop();
        }
        st.push(a[i]);
    }

    // Return the number of triplets found
    return cnt;
}

// Driver code
int main()
{
    vector<int> a = { 2, 1, -3, -2, 5 };

    // Print the required result
    cout << findTriplets(a);
    return 0;
}

    // This code is contributed by rakeshsahni
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find desired triplets
    public static int findTriplets(int[] a)
    {

        // To store the number of triplets found
        int cnt = 0;

        Stack<Integer> stack = new Stack<>();

        // Keep track of second minimum element
        int secondMin = Integer.MAX_VALUE;

        for (int i = a.length - 1; i >= 0; i--) {

            // If required triplet is found
            if (a[i] > secondMin)
                cnt++;

            while (!stack.isEmpty()
                   && stack.peek() > a[i]) {

                secondMin = stack.pop();
            }
            stack.push(a[i]);
        }

        // Return the number of triplets found
        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 1, -3, -2, 5 };

        // Print the required result
        System.out.println(findTriplets(a));
    }
}
```

## **蟒蛇 3**

```
# Python 3 program for above approach
import sys

# Function to find desired triplets
def findTriplets(a):

    # To store the number of triplets found
    cnt = 0
    st = []

    # Keep track of second minimum element
    secondMin = sys.maxsize
    for i in range(len(a) - 1, -1, -1):

        # If required triplet is found
        if (a[i] > secondMin):
            cnt += 1

        while (not len(st) == 0 and st[-1] > a[i]):

            secondMin = st[-1]
            st.pop()

        st.append(a[i])

    # Return the number of triplets found
    return cnt

# Driver code
if __name__ == "__main__":
    a = [2, 1, -3, -2, 5]

    # Print the required result
    print(findTriplets(a))

    # This code is contributed by ukasp.
```

## **C#**

```
// C# program for above approach

using System;
using System.Collections.Generic;

public class GFG {

    // Function to find desired triplets
    public static int findTriplets(int[] a)
    {

        // To store the number of triplets found
        int cnt = 0;

        Stack<int> stack = new Stack<int>();

        // Keep track of second minimum element
        int secondMin = int.MaxValue;

        for (int i = a.Length - 1; i >= 0; i--) {

            // If required triplet is found
            if (a[i] > secondMin)
                cnt++;

            while (stack.Count!=0
                   && stack.Peek() > a[i]) {

                secondMin = stack.Pop();
            }
            stack.Push(a[i]);
        }

        // Return the number of triplets found
        return cnt;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []a = { 2, 1, -3, -2, 5 };

        // Print the required result
        Console.WriteLine(findTriplets(a));
    }
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>
// javascript program for above approach  
// Function to find desired triplets
    function findTriplets(a)
    {

        // To store the number of triplets found
        var cnt = 0;

        var stack = [];

        // Keep track of second minimum element
        var secondMin = Number.MAX_VALUE;

        for (var i = a.length - 1; i >= 0; i--) {

            // If required triplet is found
            if (a[i] > secondMin)
                cnt++;

            while (stack.length!=0
                   && stack[0] > a[i]) {

                secondMin = stack.pop();
            }
            stack.push(a[i]);
        }

        // Return the number of triplets found
        return cnt;
    }

// Driver code
var a = [ 2, 1, -3, -2, 5 ];

// Print the required result
document.write(findTriplets(a));

// This code is contributed by shikhasingrajput
</script>
```

****Output**

```
2
```** 

****时间复杂度:**O(N)
T3】辅助空间: O(N)**