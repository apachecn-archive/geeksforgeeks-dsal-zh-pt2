# 将一个数组转换成 1 到 N 的排列的最小运算，用一些 d 的余数代替

> 原文:[https://www . geesforgeks . org/最小运算-通过用某个 d 的余数替换将数组转换为 1 到 n 的排列/](https://www.geeksforgeeks.org/minimum-operations-to-convert-an-array-into-a-permutation-of-1-to-n-by-replacing-with-remainder-from-some-d/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到**最小**运算次数**将**的**数组**转换为**【1，N】**的排列，在每次运算中，一个元素**a【I】**可以被**替换**为**a【I】如果无法打印 **-1** 。**

**示例:**

> ***输入:*** arr[] = {5，4，10，8，1}
> ***输出:*** 2
> ***说明:*** 在第一次运算中选择 d = 7，10 可以被 10 % 7 代替，
> 在第二次运算中 d = 6，8 可以被 8 %6 代替所以两次运算。
> 
> ***输入:*** arr[] = {1，2，3，7}
> ***输出:*** -1

**进场:**使用[贪婪](http://www.geeksforgeeks.org/greedy-algorithms/)进场可以解决任务。这种方法基于这样的事实，即当要获得**余数** r 时，则**a【I】****>****2 * r**即 **r** 位于范围**【0，a【I】-1/2】**之间

> 让我们举个例子:8 代表不同的 d
> 
> 取，8 % 7= 1
> 
>            8%6 = 2
> 
>            8%5 = 3
> 
>           8%4 = 0
> 
>           8%3 = 2
> 
>           8%2 = 0
> 
>           8%1=0
> 
> 所以使用 mod 运算可以得到的最大数是 3，所以当我们想得到一个排列中的数 I 时，这个数应该是 a[i] > 2* i+1

请按照以下步骤解决此问题:

*   初始化一组**s**
*   遍历数组 **arr[]** &将 arr[]的所有元素插入到集合中。
*   初始化变量 **ops = 0**
*   现在从 n 迭代到 1
*   检查 s 是否已经从器械包中取出。
*   否则增加 ops 并检查集合中最大的元素< **2* i +1**
*   如果集合中最大的是< **2* i +1** ，则设定 **ops = -1** 并脱离循环。
*   否则把它从设置中删除，因为我们可以使用 mod 操作来制作它。
*   打印行动

`以下是上述方法的实施情况:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum operations
// to convert the array into a permutation of [1, n]
void minimum_operations(int arr[], int n)
{
    // Initialize the set
    set<int> s;

    // Insert all the elements into the set
    for (int i = 0; i < n; i++) {
        s.insert(arr[i]);
    }

    // Initialize ops to count the operations
    int ops = 0;

    // Traverse from [n to 1]
    for (int i = n; i >= 1; i--) {

        // If we already have i in our
        // array erase it from the set
        if (s.find(i) != s.end()) {
            s.erase(s.find(i));
        }

        // count the ops because there is no element
        else {
            ops++;

            // Check the largest element of the set
            auto it = s.end();
            it--;

            // If it is < 2*i +1 we cant get that i
            // using % operation so there is no way to
            // create a permutation
            if (*it < 2 * i + 1) {
                ops = -1;
                break;
            }

            // Erase it if we have processed
            // it to i by % operation
            s.erase(it);
        }
    }

    // Print the result
    cout << ops << endl;
}

// Driver Code
int main()
{
    // Initialize the value n
    int arr[] = { 5, 4, 10, 8, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    minimum_operations(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

  // Function to find the minimum operations
  // to convert the array into a permutation of [1, n]
  static void minimum_operations(int arr[], int n)
  {
    // Initialize the set
    SortedSet<Integer> s = new TreeSet<Integer>();

    // Insert all the elements into the set
    for (int i = 0; i < n; i++) {
      s.add(arr[i]);
    }

    // Initialize ops to count the operations
    int ops = 0;

    // Traverse from [n to 1]
    for (int i = n; i >= 1; i--) {

      // If we already have i in our
      // array erase it from the set
      if (s.contains(i)) {
        s.remove(i);
      }

      // count the ops because there is no element
      else {
        ops++;

        // Check the largest element of the set
        Integer it = s.last();
        it--;

        // If it is < 2*i +1 we cant get that i
        // using % operation so there is no way to
        // create a permutation
        if (it < 2 * i + 1) {
          ops = -1;
          break;
        }

        // Erase it if we have processed
        // it to i by % operation
        s.remove(it);
      }
    }

    // Print the result
    System.out.print(ops +"\n");
  }

  // Driver Code
  public static void main(String[] args)
  {
    // Initialize the value n
    int arr[] = { 5, 4, 10, 8, 1 };
    int n = arr.length;
    minimum_operations(arr, n);

  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 code for the above approach

# Function to find the minimum operations
# to convert the array into a permutation of [1, n]
def minimum_operations(arr, n):

    # Initialize the set
    s = set([])

    # Insert all the elements into the set
    for i in range(n):
        s.add(arr[i])

    # Initialize ops to count the operations
    ops = 0

    # Traverse from [n to 1]
    for i in range(n, 0, -1):

        # If we already have i in our
        # array erase it from the set
        if (i in s):
            list(s).remove(i)

        # count the ops because there is no element
        else:
            ops += 1

            # Check the largest element of the set
            it = len(s)
            it -= 1

            # If it is < 2*i +1 we cant get that i
            # using % operation so there is no way to
            # create a permutation
            if (list(s)[it] < 2 * i + 1):
                ops = -1
                break

            # Erase it if we have processed
            # it to i by % operation
            list(s).pop(it)

    # Print the result
    print(ops)

# Driver Code
if __name__ == "__main__":

    # Initialize the value n
    arr = [5, 4, 10, 8, 1]
    n = len(arr)
    minimum_operations(arr, n)

    # This code is contributed by ukasp.
```

**Output**

```
2
```

***时间复杂度:**T3】O(nlogn)
T5】T6】辅助空间:T8】O(n)*