# 处理 m 个任务的最小成本，其中切换成本

> 原文:[https://www . geeksforgeeks . org/加工 m-tasks-where-switching-costs/](https://www.geeksforgeeks.org/minimum-cost-to-process-m-tasks-where-switching-costs/)

处理器有 n 个核心。每个核心可以一次处理一个任务。不同的内核可以同时处理不同的任务，而不影响其他任务。假设队列中有 m 个任务，处理器必须处理这 m 个任务。同样，这 m 个任务并不都是相似的类型。任务的类型用数字表示。所以，m 个任务被表示为 m 个连续的数字，相同的数字代表相同类型的任务，像 1 代表类型 1 的任务，2 代表类型 2 的任务等等。

最初，所有内核都是免费的。在一个核心中启动一种类型的任务需要一个单位的成本，该任务当前没有在该核心中运行。在每个核心上开始任务时，将收取一个单位成本。例如，一个核心正在运行类型 3 任务，如果我们在该核心中再次分配类型 3 任务，则此分配的成本将为零。但是，如果我们分配类型 2 的任务，那么这个任务的成本将是一个单位。一个核心一直在处理一个任务，直到下一个任务被分配给该核心。

**示例:**

```
Input : n = 3, m = 6, arr = {1, 2, 1, 3, 4, 1}
Output : 4

Input : n = 2, m = 6, arr = {1, 2, 1, 3, 2, 1}
Output : 4
Explanation : 

Input : n = 3, m = 31, 
arr = {7, 11, 17, 10, 7, 10, 2, 9, 2, 18, 8, 10, 20, 10, 3, 20,
       17, 17, 17, 1, 15, 10, 8, 3, 3, 18, 13, 2, 10, 10, 11}
Output : 18
```

**解释(第一个样本输入/输出):**这里的核心总数是 3。让，A，B 和 c。首先在任何一个核心中分配类型 1 的任务- >花费 1 个单位。状态:A–1，B–无，C–无。在其余 2 个核心中的任何一个核心中分配类型 2 的任务- >花费 1 个单位。状态:A–1，B–2，C–无。然后在类型 1 任务正在进行的核心中分配类型 1 的任务- >花费 0 个单位。状态:A–1，B–2，C–无。
在自由核心分配 3 型任务- >花费 1 单位。状态:A–1、B–2、C–3。

现在，所有核心都在运行一项任务。因此，我们必须在其中一个核心中分配类型 4 的任务。让我们将它加载到核心 B 中，在那里之前类型 2 任务正在进行->成本 1 单位。

状态:A–1、B–4、C–3。现在，在核心 A 中加载类型 1 任务，其中类型 1 任务正在运行->成本 0 单位。状态:A–1、B–4、C–3。因此，总成本= 1 + 1 + 0 + 1 + 1 + 0 = 4 u
单位。

**解释 2(针对第二个样本输入/输出):**内核总数为 2。让 A 和 b .任何一个核心中的第一个类型的处理任务- >花费 1 个单位。状态:A–1，B–无。其余 2 个核心中的任何一个中的类型 2 的处理任务- >花费 1 个单位。状态:A–1，B–2。然后在核心中处理类型 1 任务，其中类型 1 的任务正在进行- >花费 0 单位。状态:A–1，B–2。现在，让我们将类型 3 的任务分配给成本为 1 单位的核心 A - >。状态:A–3，B–2。现在，在核心 B 中分配类型 2 任务，那里已经有类型 2 任务正在进行- >成本 0 单位。状态:A–3，B–2。因此，总成本= 1 + 1 + 0 + 1 + 1 = 4 个单位。最后在任何一个核心中分配类型 1 任务(比如 A) - >花费 1 个单位。状态:A–1，B–2。因此，总成本= 1 + 1 + 0 + 1 + 0 + 1 = 4 个单位。

**方法:**将这个问题分为两种情况:
第一种情况是当同一类型的任务当前在其中一个内核中运行时。然后，只需将即将到来的任务分配给该核心。例如 1，在 i = 3(第三个任务)时，当类型 1 任务到来时，我们可以将该任务分配给先前类型 1 任务所在的核心。这个的成本是 0 单位。

第二种情况是相同类型的任务没有在任何内核中运行。那么，可能有两种可能。子案例 1 是，如果至少有一个空闲核心，那么将即将到来的任务分配给该核心。

子案例 2 是，如果没有空闲的核心，那么我们必须停止处理一种类型的任务，释放一个核心，并在该核心中分配即将到来的任务，以便将来的成本变得最小。为了最大限度地降低成本，我们应该停止一种以后再也不会发生的任务。如果每个正在进行的任务在未来至少重复一次，那么我们应该停止那个将在所有当前正在进行的任务中持续重复的任务(这是一种贪婪的方法，并且会执行任务)。

例如 2:在 i = 4(第四个任务)、类型 3 任务、当前正在进行的类型 1 和类型 2 任务处于两个核心时，我们可以停止任务类型 1 或任务类型 2 来启动任务类型 3。但是我们将停止任务类型 1，因为类型 1 任务在类型 2 任务之后重新出现。

## C++

```
// C++ Program to find out minimum
// cost to process m tasks
#include <bits/stdc++.h>

using namespace std;

// Function to find out the farthest
// position where one of the currently
// ongoing tasks will rehappen.
int find(vector<int> arr, int pos,
         int m, vector<bool> isRunning)
{

    // Iterate form last to current
    // position and find where the
    // task will happen next.
    vector<int> d(m + 1, 0);
    for (int i = m; i > pos; i--)
    {
        if (isRunning[arr[i]])
            d[arr[i]] = i;
    }

    // Find out maximum of all these
    // positions and it is the
    // farthest position.
    int maxipos = 0;
    for (int ele : d)
        maxipos = max(ele, maxipos);

    return maxipos;
}

// Function to find out minimum cost to
// process all the tasks
int mincost(int n, int m, vector<int> arr)
{

    // freqarr[i][j] denotes the frequency
    // of type j task after position i
    // like in array {1, 2, 1, 3, 2, 1}
    // frequency of type 1 task after
    // position 0 is 2\. So, for this
    // array freqarr[0][1] = 2\. Here,
    // i can range in between 0 to m-1 and
    // j can range in between 0 to m(though
    // there is not any type 0 task).
    vector<vector<int> > freqarr(m);

    // Fill up the freqarr vector from
    // last to first. After m-1 th position
    // frequency of all type of tasks will be
    // 0\. Then at m-2 th position only frequency
    // of arr[m-1] type task will be increased
    // by 1\. Again, in m-3 th position only
    // frequency of type arr[m-2] task will
    // be increased by 1 and so on.
    vector<int> newvec(m + 1, 0);
    freqarr[m - 1] = newvec;
    for (int i = m - 2; i >= 0; i--)
    {
        vector<int> nv;
        nv = freqarr[i + 1];
        nv[arr[i + 1]] += 1;
        freqarr[i] = nv;
    }

    // isRunning[i] denotes whether type i
    // task is currently running in one
    // of the cores.
    // At the beginning no tasks are
    // running so all values are false.
    vector<bool> isRunning(m + 1, false);

    // cost denotes total cost to assign tasks
    int cost = 0;

    // truecount denotes number of occupied cores
    int truecount = 0;

    // iterate through each task and find the
    // total cost.
    for (int i = 0; i < m; i++) {

        // ele denotes type of task.
        int ele = arr[i];

        // Case 1: if same type of task is
        // currently running cost for this
        // is 0.
        if (isRunning[ele] == true)
            continue;

        // Case 2: same type of task is not
        // currently running.
        else {

            // Subcase 1: if there is at least
            // one free core then assign this task
            // to that core at a cost of 1 unit.
            if (truecount < n) {
                cost += 1;
                truecount += 1;
                isRunning[ele] = true;
            }

            // Subcase 2: No core is free
            else {

                // here we will first find the minimum
                // frequency among all the ongoing tasks
                // in future.
                // If the minimum frequency is 0 then
                // there is at least one ongoing task
                // which will not occur again. Then we just
                // stop that task.
                // If minimum frequency is >0 then, all the
                // tasks will occur at least once in future.
                // we have to find out which of these will
                // rehappen last among the all ongoing tasks.

                // set minimum frequency to a big number
                int mini = 100000;

                // set index of minimum frequency task to 0.
                int miniind = 0;

                // find the minimum frequency task type(miniind)
                // and frequency(mini).
                for (int j = 1; j <= m; j++) {
                    if (isRunning[j] && mini > freqarr[i][j]) {
                        mini = freqarr[i][j];
                        miniind = j;
                    }
                }

                // If minimum frequency is zero then just stop
                // the task and start the present task in that
                // core. Cost for this is 1 unit.
                if (mini == 0) {
                    isRunning[miniind] = false;
                    isRunning[ele] = true;
                    cost += 1;
                }

                // If minimum frequency is nonzero then find
                // the farthest position where one of the
                // ongoing task will rehappen.
                // Stop that task and start present task
                // in that core.
                else {

                    // find out the farthest position using
                    // find function
                    int farpos = find(arr, i, m, isRunning);
                    isRunning[arr[farpos]] = false;
                    isRunning[ele] = true;
                    cost += 1;
                }
            }
        }
    }
    // return total cost
    return cost;
}

// Driver Program
int main()
{
    // Test case 1
    int n1 = 3;
    int m1 = 6;
    vector<int> arr1{ 1, 2, 1, 3, 4, 1 };
    cout << mincost(n1, m1, arr1) << endl;

    // Test case 2
    int n2 = 2;
    int m2 = 6;
    vector<int> arr2{ 1, 2, 1, 3, 2, 1 };
    cout << mincost(n2, m2, arr2) << endl;

    // Test case 3
    int n3 = 3;
    int m3 = 31;
    vector<int> arr3{ 7, 11, 17, 10, 7, 10, 2, 9,
                      2, 18, 8, 10, 20, 10, 3, 20,
                      17, 17, 17, 1, 15, 10, 8, 3,
                       3, 18, 13, 2, 10, 10, 11 };
    cout << mincost(n3, m3, arr3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find out minimum
// cost to process m tasks
import java.util.*;

class GFG{

// Function to find out the farthest
// position where one of the currently
// ongoing tasks will rehappen.
static int find(int[] arr, int pos, int m,
                boolean[] isRunning)
{

    // Iterate form last to current
    // position and find where the
    // task will happen next.
    int[] d = new int[m + 1];
    for(int i = m - 1; i > pos; i--)
    {
        if (isRunning[arr[i]])
            d[arr[i]] = i;
    }

    // Find out maximum of all these
    // positions and it is the
    // farthest position.
    int maxipos = 0;
    for(int ele : d)
        maxipos = Math.max(ele, maxipos);

    return maxipos;
}

// Function to find out minimum cost to
// process all the tasks
static int mincost(int n, int m, int[] arr)
{

    // freqarr[i][j] denotes the frequency
    // of type j task after position i
    // like in array {1, 2, 1, 3, 2, 1}
    // frequency of type 1 task after
    // position 0 is 2\. So, for this
    // array freqarr[0][1] = 2\. Here,
    // i can range in between 0 to m-1 and
    // j can range in between 0 to m(though
    // there is not any type 0 task).
    @SuppressWarnings("unchecked")
    Vector<Integer>[] freqarr = new Vector[m];
    for(int i = 0; i < freqarr.length; i++)
        freqarr[i] = new Vector<Integer>();

    // Fill up the freqarr vector from
    // last to first. After m-1 th position
    // frequency of all type of tasks will be
    // 0\. Then at m-2 th position only frequency
    // of arr[m-1] type task will be increased
    // by 1\. Again, in m-3 th position only
    // frequency of type arr[m-2] task will
    // be increased by 1 and so on.
    int[] newvec = new int[m + 1];
    for(int i = 0; i < m + 1; i++)
        freqarr[m - 1].add(newvec[i]);

    for(int i = m - 2; i > 0; i--)
    {
        Vector<Integer> nv = new Vector<>();
        nv = freqarr[i + 1];
        nv.insertElementAt(arr[i + 1] + 1,
                           arr[i + 1]);
        freqarr[i] = nv;
    }

    // isRunning[i] denotes whether type i
    // task is currently running in one
    // of the cores.
    // At the beginning no tasks are
    // running so all values are false.
    boolean[] isRunning = new boolean[m + 1];

    // cost denotes total cost to assign tasks
    int cost = 0;

    // truecount denotes number of occupied cores
    int truecount = 0;

    // Iterate through each task and find the
    // total cost.
    for(int i = 0; i < m; i++)
    {

        // ele denotes type of task.
        int ele = arr[i];

        // Case 1: if same type of task is
        // currently running cost for this
        // is 0.
        if (isRunning[ele] == true)
            continue;

        // Case 2: same type of task is not
        // currently running.
        else
        {

            // Subcase 1: if there is at least
            // one free core then assign this task
            // to that core at a cost of 1 unit.
            if (truecount < n)
            {
                cost += 1;
                truecount += 1;
                isRunning[ele] = true;
            }

            // Subcase 2: No core is free
            else
            {

                // Here we will first find the minimum
                // frequency among all the ongoing tasks
                // in future.
                // If the minimum frequency is 0 then
                // there is at least one ongoing task
                // which will not occur again. Then we just
                // stop that task.
                // If minimum frequency is >0 then, all the
                // tasks will occur at least once in future.
                // we have to find out which of these will
                // rehappen last among the all ongoing tasks.

                // Set minimum frequency to a big number
                int mini = 100000;

                // Set index of minimum frequency task to 0.
                int miniind = 0;

                // Find the minimum frequency task
                // type(miniind) and frequency(mini).
                for(int j = 0; j <= m; j++)
                {
                    if (isRunning[j] && mini >
                          freqarr[i].get(j))
                    {
                        mini = freqarr[i].get(j);
                        miniind = j;
                    }
                }

                // If minimum frequency is zero then
                // just stop the task and start the
                // present task in that core. Cost
                // for this is 1 unit.
                if (mini == 0)
                {
                    isRunning[miniind] = false;
                    isRunning[ele] = true;
                    cost += 1;
                }

                // If minimum frequency is nonzero
                // then find the farthest position
                // where one of the ongoing task
                // will rehappen.Stop that task
                // and start present task in that
                // core.
                else
                {

                    // Find out the farthest position
                    // using find function
                    int farpos = find(arr, i, m,
                                      isRunning);
                    isRunning[arr[farpos]] = false;
                    isRunning[ele] = true;
                    cost += 1;
                }
            }
        }
    }

    // Return total cost
    return cost;
}

// Driver code
public static void main(String[] args)
{

    // Test case 1
    int n1 = 3;
    int m1 = 6;
    int[] arr1 = { 1, 2, 1, 3, 4, 1 };
    System.out.print(mincost(n1, m1, arr1) + "\n");

    // Test case 2
    int n2 = 2;
    int m2 = 6;
    int[] arr2 = { 1, 2, 1, 3, 2, 1 };
    System.out.print(mincost(n2, m2, arr2) + "\n");

    // Test case 3
    int n3 = 3;
    int m3 = 31;
    int[] arr3 = { 7, 11, 17, 10, 7, 10,
                   2, 9, 2, 18, 8, 10,
                   20, 10, 3, 20, 17, 17,
                   17, 1, 15, 10, 8, 3,
                   3, 18, 13, 2, 10, 10, 11 };

    System.out.print(mincost(n3, m3 - 8, arr3) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 Program to find out
# minimum cost to process m tasks

# Function to find out the farthest
# position where one of the currently
# ongoing tasks will rehappen.
def find(arr, pos, m, isRunning):

    # Iterate form last to current
    # position and find where the
    # task will happen next.
    d = [0] * (m + 1)
    for i in range(m - 1, pos, -1):

        if isRunning[arr[i]]:
            d[arr[i]] = i

    # Find out maximum of all these positions
    # and it is the farthest position.
    maxipos = 0
    for ele in d:
        maxipos = max(ele, maxipos)

    return maxipos

# Function to find out minimum
# cost to process all the tasks
def mincost(n, m, arr):

    # freqarr[i][j] denotes the frequency
    # of type j task after position i
    # like in array 1, 2, 1, 3, 2, 1
    # frequency of type 1 task after
    # position 0 is 2\. So, for this
    # array freqarr[0][1] = 2\. Here,
    # i can range in between 0 to m-1 and
    # j can range in between 0 to m(though
    # there is not any type 0 task).
    freqarr = [[] for i in range(m)]

    # Fill up the freqarr vector from
    # last to first. After m-1 th position
    # frequency of all type of tasks will be
    # 0\. Then at m-2 th position only frequency
    # of arr[m-1] type task will be increased
    # by 1\. Again, in m-3 th position only
    # frequency of type arr[m-2] task will
    # be increased by 1 and so on.
    newvec = [0] * (m + 1)
    freqarr[m - 1] = newvec[:]
    for i in range(m - 2, -1, -1):

        nv = freqarr[i + 1][:]
        nv[arr[i + 1]] += 1
        freqarr[i] = nv[:]

    # isRunning[i] denotes whether type i
    # task is currently running in one
    # of the cores.
    # At the beginning no tasks are
    # running so all values are false.
    isRunning = [False] * (m + 1)

    # cost denotes total cost to assign tasks
    cost = 0

    # truecount denotes number of occupied cores
    truecount = 0

    # iterate through each task
    # and find the total cost.
    for i in range(0, m):

        # ele denotes type of task.
        ele = arr[i]

        # Case 1: if same type of task is
        # currently running cost for this is 0.
        if isRunning[ele] == True:
            continue

        # Case 2: same type of task
        # is not currently running.
        else:

            # Subcase 1: if there is at least
            # one free core then assign this task
            # to that core at a cost of 1 unit.
            if truecount < n:
                cost += 1
                truecount += 1
                isRunning[ele] = True

            # Subcase 2: No core is free
            else:

                # here we will first find the minimum
                # frequency among all the ongoing tasks
                # in future.
                # If the minimum frequency is 0 then
                # there is at least one ongoing task
                # which will not occur again. Then we just
                # stop that task.
                # If minimum frequency is >0 then, all the
                # tasks will occur at least once in future.
                # we have to find out which of these will
                # rehappen last among the all ongoing tasks.

                # set minimum frequency to a big number
                mini = 100000

                # set index of minimum frequency task to 0.
                miniind = 0

                # find the minimum frequency task
                # type(miniind) and frequency(mini).
                for j in range(1, m + 1):
                    if isRunning[j] and mini > freqarr[i][j]:
                        mini = freqarr[i][j]
                        miniind = j

                # If minimum frequency is zero then just stop
                # the task and start the present task in that
                # core. Cost for this is 1 unit.
                if mini == 0:
                    isRunning[miniind] = False
                    isRunning[ele] = True
                    cost += 1

                # If minimum frequency is nonzero then find
                # the farthest position where one of the
                # ongoing task will rehappen.
                # Stop that task and start present task
                # in that core.
                else:

                    # find out the farthest position
                    # using find function
                    farpos = find(arr, i, m, isRunning)
                    isRunning[arr[farpos]] = False
                    isRunning[ele] = True
                    cost += 1

    # return total cost
    return cost

# Driver Code
if __name__ == "__main__":

    # Test case 1
    n1, m1 = 3, 6
    arr1 = [1, 2, 1, 3, 4, 1]
    print(mincost(n1, m1, arr1))

    # Test case 2
    n2, m2 = 2, 6
    arr2 = [1, 2, 1, 3, 2, 1]
    print(mincost(n2, m2, arr2))

    # Test case 3
    n3, m3 = 3, 31
    arr3 = [7, 11, 17, 10, 7, 10, 2, 9,
            2, 18, 8, 10, 20, 10, 3, 20,
            17, 17, 17, 1, 15, 10, 8, 3,
            3, 18, 13, 2, 10, 10, 11]

    print(mincost(n3, m3, arr3))

# This code is contributed by Rituraj Jain
```

**Output:** 

```
4
4
18
```

**时间复杂度:**o(m^2)
T3】空间复杂度: O(m^2)，(存储频率)