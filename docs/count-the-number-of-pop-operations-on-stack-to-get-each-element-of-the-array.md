# 统计堆栈上弹出操作的次数，得到数组的每个元素

> 原文:[https://www . geesforgeks . org/count-堆栈上的弹出操作数-获取数组的每个元素/](https://www.geeksforgeeks.org/count-the-number-of-pop-operations-on-stack-to-get-each-element-of-the-array/)

**先决条件:** [堆叠](https://www.geeksforgeeks.org/stack-data-structure/)[散列](https://www.geeksforgeeks.org/hashing-data-structure/)
给定一堆 N 个数字和一组数字。计算获取数组每个元素所需的 pop 操作数。一旦一个元素被弹出，它就不会再被推回。假设数组中的所有元素最初都存在于堆栈中。
**示例:**

> 输入:N = 5
> 堆栈:6 4 3 2 1
> 数组:6 3 4 1 2
> 输出:1 2 0 2 0
> 堆栈的第一个元素与数组元素相同。所以要得到 6，需要一个 pop，即堆栈中的 pop 6。为了得到 3，将弹出 2 个元素，即 4 和 3。为了得到 4，4 已经被弹出，因此我们不会弹出更多的元素。同样，为了得到 1，我们将弹出 2 个元素，对于 2，将不添加弹出计数。

**做法:**这个问题用一个栈就可以轻松解决。我们将不断弹出元素，直到找到我们正在搜索的元素。唯一的障碍是，当元素已经弹出并且不在堆栈中时，如何处理这种情况。为此，我们将维护一个哈希映射。当我们从堆栈中弹出一个元素时，我们会将该元素插入到哈希映射中，这样，如果该元素稍后出现在数组中，我们将首先检查它是否出现在哈希映射中，或者换句话说，是否已经从堆栈中弹出。否则，我们将知道它存在于堆栈中，我们将开始弹出元素，直到找到所需的数量。
以下是上述办法的实施:

## C++

```
// C++ program to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count
void countEle(stack<int>& s, int a[], int N)
{
    // Hashmap to store all the elements
    // which are popped once.
    unordered_map<int, bool> mp;
    for (int i = 0; i < N; ++i) {
        int num = a[i];

        // Check if the number is present
        // in the hashmap Or in other words
        // been popped out from the stack before.
        if (mp.find(num) != mp.end())
            cout << "0 ";

        else {
            int cnt = 0;

            // Keep popping the elements
            // while top is not equal to num
            while (s.top() != num) {
                mp[s.top()] = true;
                s.pop();
                cnt++;
            }
            // Pop the top ie. equal to num
            s.pop();
            cnt++;

            // Print the number of elements popped.
            cout << cnt << " ";
        }
    }
}

// Driver code
int main()
{
    int N = 5;

    stack<int> s;
    s.push(1);
    s.push(2);
    s.push(3);
    s.push(4);
    s.push(6);

    int a[] = { 6, 3, 4, 1, 2 };
    countEle(s, a, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement above approach
import java.util.HashMap;
import java.util.Stack;

class GFG
{

    // Function to find the count
    public static void countEle(Stack<Integer> s,
                                int[] a, int N)
    {

        // Hashmap to store all the elements
        // which are popped once.
        HashMap<Integer,
                Boolean> mp = new HashMap<>();
        for (int i = 0; i < N; ++i)
        {
            int num = a[i];

            // Check if the number is present
            // in the hashmap Or in other words
            // been popped out from the stack before.
            if (mp.containsKey(num))
                System.out.print("0 ");
            else
            {
                int cnt = 0;

                // Keep popping the elements
                // while top is not equal to num
                while (s.peek() != num)
                {
                    mp.put(s.peek(), true);
                    s.pop();
                    cnt++;
                }

                // Pop the top ie. equal to num
                s.pop();
                cnt++;

                // Print the number of elements popped.
                System.out.print(cnt + " ");
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 5;

        Stack<Integer> s = new Stack<>();
        s.add(1);
        s.add(2);
        s.add(3);
        s.add(4);
        s.add(6);

        int[] a = { 6, 3, 4, 1, 2 };
        countEle(s, a, N);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to implement above approach

# Function to find the count
def countEle(s, a, N):

    # Hashmap to store all the elements
    # which are popped once.
    mp = {}
    for i in range(0, N): 
        num = a[i]

        # Check if the number is present
        # in the hashmap Or in other words
        # been popped out from the stack before.
        if num in mp:
            print("0", end = " ")

        else:
            cnt = 0

            # Keep popping the elements
            # while top is not equal to num
            while s[-1] != num:
                mp[s.pop()] = True
                cnt += 1

            # Pop the top ie. equal to num
            s.pop()
            cnt += 1

            # Print the number of elements popped.
            print(cnt, end = " ")

# Driver code
if __name__ == "__main__":

    N = 5
    s = []
    s.append(1)
    s.append(2)
    s.append(3)
    s.append(4)
    s.append(6)

    a = [6, 3, 4, 1, 2] 
    countEle(s, a, N)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach:
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the count
    public static void countEle(Stack<int> s,
                                int[] a, int N)
    {

        // Hashmap to store all the elements
        // which are popped once.
        Dictionary<int,
                   bool> mp = new Dictionary<int,
                                             bool>();
        for (int i = 0; i < N; ++i)
        {
            int num = a[i];

            // Check if the number is present
            // in the hashmap Or in other words
            // been popped out from the stack before.
            if (mp.ContainsKey(num))
                Console.Write("0 ");
            else
            {
                int cnt = 0;

                // Keep popping the elements
                // while top is not equal to num
                while (s.Peek() != num)
                {
                    mp.Add(s.Peek(), true);
                    s.Pop();
                    cnt++;
                }

                // Pop the top ie. equal to num
                s.Pop();
                cnt++;

                // Print the number of elements popped.
                Console.Write(cnt + " ");
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int N = 5;

        Stack<int> s = new Stack<int>();
        s.Push(1);
        s.Push(2);
        s.Push(3);
        s.Push(4);
        s.Push(6);

        int[] a = { 6, 3, 4, 1, 2 };
        countEle(s, a, N);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to implement above approach

// Function to find the count
function countEle(s, a, N)
{
    // Hashmap to store all the elements
    // which are popped once.
    var mp = new Map();
    for (var i = 0; i < N; ++i) {
        var num = a[i];

        // Check if the number is present
        // in the hashmap Or in other words
        // been popped out from the stack before.
        if (mp.has(num))
            document.write( "0 ");

        else {
            var cnt = 0;

            // Keep popping the elements
            // while top is not equal to num
            while (s[s.length-1] != num) {
                mp.set(s[s.length-1], true);
                s.pop();
                cnt++;
            }
            // Pop the top ie. equal to num
            s.pop();
            cnt++;

            // Print the number of elements popped.
            document.write( cnt + " ");
        }
    }
}

// Driver code
var N = 5;
var s = [];
s.push(1);
s.push(2);
s.push(3);
s.push(4);
s.push(6);
var a = [6, 3, 4, 1, 2 ];
countEle(s, a, N);

</script>
```

**Output:** 

```
1 2 0 2 0
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)