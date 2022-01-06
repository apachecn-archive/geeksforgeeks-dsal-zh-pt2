# 给定数组中包含偶数或连续元素的对的计数

> 原文:[https://www . geeksforgeeks . org/给定数组中包含偶数或连续元素的对计数/](https://www.geeksforgeeks.org/count-of-pairs-containing-even-or-consecutive-elements-from-given-array/)

给定一个偶数大小的数组 **arr[]** ，任务是在将 **arr[]** 分割成对之后，找到对的计数，这样:

*   **arr[]** 的每个元素恰好属于一对
*   他们两个都是偶数或
*   两者的绝对差为 **1** ，即**| X–Y | = 1**。

***例:***

> ***输入:** arr[] = {11，12，16，14}*
> ***输出:** {11，12}，{16，14}*
> ***说明:** arr[]，可以按以下方式分成对。*
> *对 1 –{ 11，12}，as |11-12| = 1。*
> *对 2 –{ 16，14}，16 和 14 都是偶数。*
> *因此，{11，12}和{16，14}是两对。*
> 
> **在** ***放:** A = {4，7}*
> ***输出:**否*

**进场:**这个问题是观察为主。首先，如果偶数计数和奇数计数不具有相同的奇偶性，那么答案不存在。这意味着如果偶数和奇数的计数都是偶数或奇数。现在左边的例子，当偶数和奇数的频率相等时，有两种情况:

1.  出现的偶数和奇数都是偶数，那么答案总是存在的。
2.  出现偶数和奇数是奇数，然后检查数组中是否有 2 个数字，使它们的绝对差为 1，然后偶数和奇数出现变成，即使如此，答案存在。

按照以下步骤解决给定的问题。

*   创建一个变量**偶数计数= 0** 作为偶数计数，**奇数计数= 0，**作为奇数计数。
*   从 i **ndex = 0 到 n-1** 迭代数组，检查 **arr【索引】%2 == 0** ，递增**偶数 _ 计数**否则递增**奇数 _ 计数。**
*   检查**偶数计数是否=奇数计数**
    *   如果条件为假，输出**否**，因为数组对不能存在。
    *   否则检查数组中是否存在 2 个元素，使得它们的绝对差值为 1。要检查这样的对是否存在，请创建一个数组 temp 并存储数组中每个数字的计数，然后迭代数组并检查连续的元素计数是否大于 1。
    *   如果存在输出**是**。
*   要打印所需的对，请成对打印偶数，然后成对打印奇数，最后一对打印左 2 个元素。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find similar pairs in arr[]
void CheckSimilarPair(int arr[], int n)
{

    // Variable to count
    // Odd and even numbers
    int odd_count = 0;
    int even_count = 0;

    // Count even and odd occurences
    for (int index = 0; index < n; index++) {
        if (arr[index] % 2 == 0)
            even_count++;
        else
            odd_count++;
    }

    // Checking same parity of count of even
    // and odd numbers
    if ((even_count % 2 == 0
         && odd_count % 2 == 1)
        || (even_count % 2 == 1
            && odd_count % 2 == 0)) {
        cout << "-1\n";
    }
    else {
        // Check if there exist 2 numbers
        // with absolute difference is 1

        // Vector to store frequency
        // of elements of the array
        vector<int> temp(1001, 0);

        // Maximum element upto which
        // temp should be checked
        int max_element = 0;

        // Iterate the array and store their counts
        for (int index = 0; index < n; index++) {
            temp[arr[index]]++;
            max_element
                = max(max_element, arr[index]);
        }

        int element1 = -1;
        int element2 = -1;
        bool pair_exist = false;

        // Iterate the temp array
        // upto max_element and check
        // if 2 element exist
        // having 1 abs' difference
        for (int index = 1; index <= max_element; index++) {
            if (temp[index - 1] >= 1
                && temp[index] >= 1) {
                element1 = index - 1;
                element2 = index;
                pair_exist = true;
                break;
            }
        }

        // If pair exist
        if (pair_exist) {
            // Vector storing pairs
            vector<int> res;
            // Even pairs
            for (int index = 0; index < n; index++) {
                if (arr[index] % 2 == 0
                    && arr[index] != element1
                    && arr[index] != element2) {
                    res.push_back(arr[index]);
                }
            }
            // Odd pairs
            for (int index = 0; index < n; index++) {
                if (arr[index] % 2 == 1
                    && arr[index] != element1
                    && arr[index] != element2) {
                    res.push_back(arr[index]);
                }
            }

            // Printing all pairs
            for (int index = 0; index < res.size() - 1; index += 2) {
                cout << "{" << res[index] << ", "
                     << res[index + 1] << "}"
                     << " ";
            }
            cout << "{" << element1 << ", "
                 << element2 << "}";
        }
        else {
            cout << "\nNo";
        }
    }
}

// Driver code
int main()
{
    int arr[4] = { 11, 12, 16, 14 };
    int N = 4;

    CheckSimilarPair(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Function to find similar pairs in arr[]
static void CheckSimilarPair(int arr[], int n)
{

    // Variable to count
    // Odd and even numbers
    int odd_count = 0;
    int even_count = 0;

    // Count even and odd occurences
    for (int index = 0; index < n; index++) {
        if (arr[index] % 2 == 0)
            even_count++;
        else
            odd_count++;
    }

    // Checking same parity of count of even
    // and odd numbers
    if ((even_count % 2 == 0
         && odd_count % 2 == 1)
        || (even_count % 2 == 1
            && odd_count % 2 == 0)) {
        System.out.print("-1\n");
    }
    else {
        // Check if there exist 2 numbers
        // with absolute difference is 1

        // Vector to store frequency
        // of elements of the array
        int []temp = new int[1001];

        // Maximum element upto which
        // temp should be checked
        int max_element = 0;

        // Iterate the array and store their counts
        for (int index = 0; index < n; index++) {
            temp[arr[index]]++;
            max_element
                = Math.max(max_element, arr[index]);
        }

        int element1 = -1;
        int element2 = -1;
        boolean pair_exist = false;

        // Iterate the temp array
        // upto max_element and check
        // if 2 element exist
        // having 1 abs' difference
        for (int index = 1; index <= max_element; index++) {
            if (temp[index - 1] >= 1
                && temp[index] >= 1) {
                element1 = index - 1;
                element2 = index;
                pair_exist = true;
                break;
            }
        }

        // If pair exist
        if (pair_exist)
        {

            // Vector storing pairs
            Vector<Integer> res = new Vector<Integer>();

            // Even pairs
            for (int index = 0; index < n; index++) {
                if (arr[index] % 2 == 0
                    && arr[index] != element1
                    && arr[index] != element2) {
                    res.add(arr[index]);
                }
            }

            // Odd pairs
            for (int index = 0; index < n; index++) {
                if (arr[index] % 2 == 1
                    && arr[index] != element1
                    && arr[index] != element2) {
                    res.add(arr[index]);
                }
            }

            // Printing all pairs
            for (int index = 0; index < res.size() - 1; index += 2) {
                System.out.print("{" +  res.get(index)+ ", "
                     + res.get(index+1)+ "}"
                    + " ");
            }
            System.out.print("{" +  element1+ ", "
                 + element2+ "}");
        }
        else {
            System.out.print("\nNo");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 11, 12, 16, 14 };
    int N = 4;

    CheckSimilarPair(arr, N);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for above approach

# Function to find similar pairs in arr[]
def CheckSimilarPair(arr, n):

    # Variable to count
    # Odd and even numbers
    odd_count = 0
    even_count = 0

    # Count even and odd occurences
    for index in range(n):
        if (arr[index] % 2 == 0):
            even_count += 1
        else:
            odd_count += 1

    # Checking same parity of count of even
    # and odd numbers
    if ((even_count % 2 == 0 and odd_count % 2 == 1) or (even_count % 2 == 1 and odd_count % 2 == 0)):
        print("-1")
    else:

        # Check if there exist 2 numbers
        # with absolute difference is 1

        # Vector to store frequency
        # of elements of the array
        temp = [0] * 1001

        # Maximum element upto which
        # temp should be checked
        max_element = 0

        # Iterate the array and store their counts
        for index in range(n):
            temp[arr[index]] += 1
            max_element = max(max_element, arr[index])

        element1 = -1
        element2 = -1
        pair_exist = False

        # Iterate the temp array
        # upto max_element and check
        # if 2 element exist
        # having 1 abs' difference
        for index in range(max_element + 1):
            if (temp[index - 1] >= 1 and temp[index] >= 1):
                element1 = index - 1
                element2 = index
                pair_exist = True
                break

        # If pair exist
        if (pair_exist):

            # Vector storing pairs
            res = []

            # Even pairs
            for index in range(n):
                if (arr[index] % 2 == 0 and arr[index] != element1 and arr[index] != element2):
                    res.append(arr[index])

            # Odd pairs
            for index in range(n):
                if (arr[index] % 2 == 1 and arr[index] != element1 and arr[index] != element2):
                    res.append(arr[index])

            # Printing all pairs
            for index in range(0, len(res) - 1, 2):
                print("{", end=" ")
                print(f"{res[index]} , {res[index + 1]}", end=" ")
                print("}", end=" ")
            print("{", end=" ")
            print(f"{element1} ,{element2}", end=" ")
            print("}")
        else:
            print('<br>' + "No")

# Driver code
arr = [11, 12, 16, 14]
N = 4

CheckSimilarPair(arr, N)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG{

// Function to find similar pairs in arr[]
static void CheckSimilarPair(int []arr, int n)
{

    // Variable to count
    // Odd and even numbers
    int odd_count = 0;
    int even_count = 0;

    // Count even and odd occurences
    for (int index = 0; index < n; index++) {
        if (arr[index] % 2 == 0)
            even_count++;
        else
            odd_count++;
    }

    // Checking same parity of count of even
    // and odd numbers
    if ((even_count % 2 == 0
         && odd_count % 2 == 1)
        || (even_count % 2 == 1
            && odd_count % 2 == 0)) {
        Console.Write("-1\n");
    }
    else {
        // Check if there exist 2 numbers
        // with absolute difference is 1

        // Vector to store frequency
        // of elements of the array
        int []temp = new int[1001];

        // Maximum element upto which
        // temp should be checked
        int max_element = 0;

        // Iterate the array and store their counts
        for (int index = 0; index < n; index++) {
            temp[arr[index]]++;
            max_element
                = Math.Max(max_element, arr[index]);
        }

        int element1 = -1;
        int element2 = -1;
        bool pair_exist = false;

        // Iterate the temp array
        // upto max_element and check
        // if 2 element exist
        // having 1 abs' difference
        for (int index = 1; index <= max_element; index++) {
            if (temp[index - 1] >= 1
                && temp[index] >= 1) {
                element1 = index - 1;
                element2 = index;
                pair_exist = true;
                break;
            }
        }

        // If pair exist
        if (pair_exist)
        {

            // Vector storing pairs
            ArrayList res = new ArrayList();

            // Even pairs
            for (int index = 0; index < n; index++) {
                if (arr[index] % 2 == 0
                    && arr[index] != element1
                    && arr[index] != element2) {
                    res.Add(arr[index]);
                }
            }

            // Odd pairs
            for (int index = 0; index < n; index++) {
                if (arr[index] % 2 == 1
                    && arr[index] != element1
                    && arr[index] != element2) {
                    res.Add(arr[index]);
                }
            }

            // Printing all pairs
            for (int index = 0; index < res.Count - 1; index += 2) {
                Console.Write("{" +  res[index]+ ", "
                     + res[index+1]+ "}"
                    + " ");
            }
            Console.Write("{" +  element1+ ", "
                 + element2+ "}");
        }
        else {
            Console.Write("\nNo");
        }
    }
}

// Driver Code
public static void Main()
{
    int []arr = { 11, 12, 16, 14 };
    int N = 4;

    CheckSimilarPair(arr, N);
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to find similar pairs in arr[]
function CheckSimilarPair(arr, n)
{

    // Variable to count
    // Odd and even numbers
    let odd_count = 0;
    let even_count = 0;

    // Count even and odd occurences
    for(let index = 0; index < n; index++)
    {
        if (arr[index] % 2 == 0)
            even_count++;
        else
            odd_count++;
    }

    // Checking same parity of count of even
    // and odd numbers
    if ((even_count % 2 == 0 && odd_count % 2 == 1) ||
        (even_count % 2 == 1 && odd_count % 2 == 0))
    {
        cout << "-1\n";
    }
    else
    {

        // Check if there exist 2 numbers
        // with absolute difference is 1

        // Vector to store frequency
        // of elements of the array
        let temp = new Array(1001).fill(0)

        // Maximum element upto which
        // temp should be checked
        let max_element = 0;

        // Iterate the array and store their counts
        for(let index = 0; index < n; index++)
        {
            temp[arr[index]]++;
            max_element = Math.max(max_element,
                                   arr[index]);
        }

        let element1 = -1;
        let element2 = -1;
        let pair_exist = false;

        // Iterate the temp array
        // upto max_element and check
        // if 2 element exist
        // having 1 abs' difference
        for(let index = 1; index <= max_element; index++)
        {
            if (temp[index - 1] >= 1 && temp[index] >= 1)
            {
                element1 = index - 1;
                element2 = index;
                pair_exist = true;
                break;
            }
        }

        // If pair exist
        if (pair_exist)
        {

            // Vector storing pairs
            let res = [];

            // Even pairs
            for(let index = 0; index < n; index++)
            {
                if (arr[index] % 2 == 0 &&
                    arr[index] != element1 &&
                    arr[index] != element2)
                {
                    res.push(arr[index]);
                }
            }

            // Odd pairs
            for(let index = 0; index < n; index++)
            {
                if (arr[index] % 2 == 1 &&
                    arr[index] != element1 &&
                    arr[index] != element2)
                {
                    res.push(arr[index]);
                }
            }

            // Printing all pairs
            for(let index = 0;
                    index < res.length - 1;
                    index += 2)
            {
                document.write("{" + res[index] + ", " +
                                     res[index + 1] + "}" +
                                     " ");
            }
            document.write("{" + element1 + ", " +
                                 element2 + "}");
        }
        else
        {
            document.write('<br>' + "No");
        }
    }
}

// Driver code
let arr = [ 11, 12, 16, 14 ];
let N = 4;

CheckSimilarPair(arr, N);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
{16, 14} {11, 12}
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)