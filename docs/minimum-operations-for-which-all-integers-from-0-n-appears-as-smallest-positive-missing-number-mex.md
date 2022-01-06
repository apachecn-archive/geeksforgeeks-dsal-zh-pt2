# 最小运算，其中来自[0，N]的所有整数显示为最小正缺失数(MEX)

> 原文:[https://www . geesforgeks . org/minimum-operations-for-all-integers-from-0-n-as-minimum-正数-missing-number-mex/](https://www.geeksforgeeks.org/minimum-operations-for-which-all-integers-from-0-n-appears-as-smallest-positive-missing-number-mex/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到数组上的最小操作，以便在每个操作中，数组中的任何元素都可以被选择并按 **1** 递增，这样对于范围**【0，N】**中的所有 **i** 来说， **MEX** 就是 **i** 。如果有**我**如果**墨西哥**不是**我**打印 **-1** 。

**示例:**

> **输入:** arr[] = {3，0，1，0， 3}
> **输出:**
> MEX 为 i = 0 是 2
> MEX 为 i = 1 是 1
> MEX 为 i = 2 是 0
> MEX 为 i = 3 是 4
> MEX 为 i = 4 是 2
> MEX 为 i = 5 是 3
> **解释:**
> 为 MEX = 0
> 在操作 1 中选择索引 1 并将其增加 1
> 在操作 2 中选择索引 3 So 2 操作。
> 对于 MEX =1
> 在操作 1 中，选择索引 2 并将其增加 1，数组变为{3，0，2，0，3} MEX = 1。So 1 操作。
> 对于 MEX = 2，So 0 操作。
> 它已经有了 MEX = 2
> 对于 MEX = 3
> 在操作 1 中选择索引 0 并将其增加 1
> 在操作 2 中选择索引 3 并将其增加 1
> 在操作 3 中选择索引 1 并将其增加 1
> 在操作 3 中选择索引 1 并将其增加 1，数组变成{4，2，1，0，4} MEX = 3 so 4 操作。
> 对于 MEX = 4，5 也一样。
> 
> **输入:** {1，2，3，4}
> **输出:** 0 -1，-1，-1
> MEX 对于 i = 0 是 0
> MEX 对于 i = 1 是-1
> MEX 对于 i = 2 是-1
> MEX 对于 i = 3 是-1
> MEX 对于 i = 4 是-1

**方法:** [哈希](http://www.geeksforgeeks.org/hashing-data-structure/)可以用来解决这个问题，存储元素的[频率，](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[栈](https://www.geeksforgeeks.org/stack-data-structure/)可以用来存储数组中重复的元素。 [Hashmap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 可以用来存储一个 **MEX = i** 的频率如果 **i** 已经存在于 Hashmap 中增加所有的出现并将重复的元素存储在堆栈中否则如果 **i** 的频率是 **0** 它已经是一个 **MEX** 所以 **0** 操作，现在在堆栈中寻找重复的出现并使其成为当前的【t2t 请按照以下步骤解决此问题:

*   [初始化一个**无序映射**](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **freq[]** 来存储数组 **arr[]** 的频率，一个变量**是可能的**来跟踪 **MEX** 的可能性。
*   [遍历数组](https://www.geeksforgeeks.org/range-based-loop-c/) **arr[]** ，并将频率存储在 hashmap freq 中。
*   [初始化**栈**](https://www.geeksforgeeks.org/stack-in-cpp-stl/)**STK【】**和**向量 ops** ，存储 **MEX = i** 、 **prev_cost** 的最小操作，以存储增加重复元素所需的成本。
*   如果**是 _ 可能== 0** ，**墨西哥= i** 是不可能的，那么储存 **-1** 。
*   否则将**频率[i]+ prev_cost** 存储在**操作**中。
    *   如果 **freq[i]** 等于 **0** 检查堆栈中是否有元素，将其弹出并增加到 **i** 并将 **prev_cost** 增加到 **i-j** 并增加 **freq[i]** ，如果堆栈为空，则使 is _ may 为 false。
    *   否则如果 **freq[i] > 1** 将重复推入堆栈 **stk[]** 并递减 **freq[i]** 。
*   现在打印[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **运算**，它包含使 **MEX = i [0，n]** 的最小运算。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum operations
// to make the MEX = i
void find_min_operations(int arr[], int n)
{

    // Initialize an unordered_map
    // to store the frequencies
    unordered_map<int, int> freq;

    // is_possible to store
    // the possibility of MEX = i
    bool is_possible = true;

    // count the frequencies
    // and store into the freq
    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }

    // Initialize stack to store
    // the repeated elements
    stack<int> stk;

    // ops store the minimum
    // operations required for MEX =i
    vector<int> ops;

    // prev_cost to store the
    // cost to increment some
    // repeated element to i-1
    // if MEX initially is i-1 so
    // that  MEX remains i
    int prev_cost = 0;
    for (int i = 0; i <= n; i++) {

        // Push -1 if it is not possible
        if (is_possible == 0)
            ops.push_back(-1);
        else {

            ops.push_back(freq[i] + prev_cost);

            // If frequency of the element is 0
            // then check for repeated element
            // in the stack so that it can be added
            // with i-j operations in next iteration
            // and can be made it to i.
            if (freq[i] == 0) {

                // Check for repeated
                // element in the stack
                if (!stk.empty()) {
                    int j = stk.top();
                    stk.pop();
                    prev_cost += i - j;
                    // Increment the frequency of i since
                    // the repeated element j is made to i

                    freq[i]++;
                }

                // If no repeated element
                // no possibiliy for MEX = i+1
                // so make is_possible=false
                else
                    is_possible = false;
            }

            // If i is already available
            else {

                // Push the repeated elements
                // into the stack
                while (freq[i] > 1) {
                    stk.push(i);
                    freq[i]--;
                }
            }
        }
    }

    for (int i = 0; i < ops.size(); i++) {
        cout << "MEX for i = "
             << i << " is " << ops[i]
             << endl;
    }
}

// Driver Code
int main()
{

    // Initializing array arr[]
    int arr[] = { 3, 0, 1, 0, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    find_min_operations(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque

# Function to find the minimum operations
# to make the MEX = i
def find_min_operations(arr, n):

    # Initialize an unordered_map
    # to store the frequencies
    freq = {}

    # is_possible to store
    # the possibility of MEX = i
    is_possible = True

    # Count the frequencies
    # and store into the freq
    for i in range(0, n):
        if arr[i] in freq:
            freq[arr[i]] += 1
        else:
            freq[arr[i]] = 1

    # Initialize stack to store
    # the repeated elements
    stk = deque()

    # ops store the minimum
    # operations required for MEX =i
    ops = []

    # prev_cost to store the
    # cost to increment some
    # repeated element to i-1
    # if MEX initially is i-1 so
    # that MEX remains i
    prev_cost = 0
    for i in range(0, n + 1):

        # Push -1 if it is not possible
        if (is_possible == 0):
            ops.append(-1)
        else:
            if i in freq:
                ops.append(freq[i] + prev_cost)
            else:
                ops.append(prev_cost)

            # If frequency of the element is 0
            # then check for repeated element
            # in the stack so that it can be added
            # with i-j operations in next iteration
            # and can be made it to i.
            if (not (i in freq)):

                # Check for repeated
                # element in the stack
                if (len(stk) != 0):
                    j = stk.popleft()
                    prev_cost += i - j

                    # Increment the frequency of i since
                    # the repeated element j is made to i
                    freq[i] = freq[i] + 1 if i in freq else 1

                # If no repeated element
                # no possibiliy for MEX = i+1
                # so make is_possible=false
                else:
                    is_possible = False

            # If i is already available
            else:

                # Push the repeated elements
                # into the stack
                while (freq[i] > 1):
                    stk.append(i)
                    freq[i] -= 1

    for i in range(0, len(ops)):
        print(f"MEX for i = {i} is {ops[i]}")

# Driver Code
if __name__ == "__main__":

    # Initializing array arr[]
    arr = [ 3, 0, 1, 0, 3 ]
    n = len(arr)

    # Function call
    find_min_operations(arr, n)

# This code is contributed by rakeshsahni
```

***Output***

```
*MEX for i = 0 is 2*
*MEX for i = 1 is 1*
*MEX for i = 2 is 0*
*MEX for i = 3 is 4*
*MEX for i = 4 is 2*
*MEX for i = 5 is 3*
```

***时间复杂度:** O(N)其中 N 是数组的大小*
T5**辅助空间:** O(N)