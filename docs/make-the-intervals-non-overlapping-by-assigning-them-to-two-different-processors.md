# 通过将间隔分配给两个不同的处理器来使间隔不重叠

> 原文:[https://www . geeksforgeeks . org/通过将间隔分配给两个不同的处理器来使间隔不重叠/](https://www.geeksforgeeks.org/make-the-intervals-non-overlapping-by-assigning-them-to-two-different-processors/)

给定一个区间列表**区间[]** ，其中每个区间包含两个整数 **L** 和 **R** ，任务是将区间分配给两个不同的处理器，使得它们对于每个处理器来说没有重叠的区间。要将间隔[i]分配给第一个处理器，请打印“F”，要将其分配给第二个处理器，请打印“S”。
**注意:**如果没有可能的解决方案打印-1。
**举例:**

> **输入:**间隔[] = {{360，480}、{420，540}、{600，660}}
> **输出:** S，F，S
> T6】说明:
> 分配给处理器的间隔是–
> 第一处理器的间隔{{420，540}}
> 第二处理器的间隔{{360，480}、{600，660}
> **输入:**间隔[] = {{99，150}，{1，100}，{100，301}，{2，5}，{150，250}}
> **输出:** S，F，F，S，S
> **说明:**
> 分配给处理器的间隔是–
> 第一处理器的间隔{{1，100}，{100

**方法:**思路是用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)给处理器分配区间。
如果处理器的最高结束时间小于或等于一个时间间隔的开始时间，那么这个时间间隔可以分配给处理器。否则，检查另一个处理器。如果任何时间间隔不能分配给任何处理器，那么就没有可能的解决方案。
下面是方法步骤的图解:

*   和当前的问题一样，我们必须按照时间间隔的顺序打印。因此，为了保存区间的顺序，请将区间与其索引配对。
*   按开始时间对间隔进行排序。即 **L** 。
*   重复这些间隔，并将这些间隔分配给处理器，如下所示:

```
if (interval[i][0] >= firstProcessorEndTime)
    answer[interval[i]] = "F"
    firstProcessorEndTime = 
        max(firstProcessorEndTime, interval[i][0])
else if (interval[i][0] >= secondProcessorEndTime)
    answer[interval[i]] = "S"
    secondProcessorEndTime = 
        max(secondProcessorEndTime, interval[i][0])
else
    print(-1)
```

以下是上述方法的实现:

## C++

```
// C++ implementation for intervals
// scheduling to two processors such
// that there are no overlapping intervals
#include <bits/stdc++.h>
using namespace std;

// Function to assign the intervals
// to two different processors
void assignIntervals(vector<vector<int> > interval, int n)
{

    //  Loop to pair the interval
    //  with their indices
    for (int i = 0; i < n; i++)
        interval[i].push_back(i);

    // sorting the interval by
    // their start times
    sort(interval.begin(), interval.end());

    int firstEndTime = -1;
    int secondEndTime = -1;
    char fin = ' ';
    bool flag = false;

    // Loop to iterate over the
    // intervals with their start time
    for (int i = 0; i < n; i++) {
        if (interval[i][0] >= firstEndTime) {
            firstEndTime = interval[i][1];
            interval[i].push_back('S');
        }
        else if (interval[i][0] >= secondEndTime) {
            secondEndTime = interval[i][1];
            interval[i].push_back('F');
        }
        else {
            flag = true;
            break;
        }
    }

    // Condition to check if there
    // is a possible solution
    if (flag)
        cout << (-1);
    else {
        vector<char> form(n, ' ');

        for (int i = 0; i < n; i++) {
            int indi = interval[i][2];
            form[indi] = interval[i][3];
        }

        // form = ''.join(form)
        for (int i = 0; i < form.size(); i++)
            cout << form[i] << ",";
    }
}

// Driver Code
int main()
{

    vector<vector<int> > intervals
        = { { 360, 480 }, { 420, 540 }, { 600, 660 } };

    // Function Call
    assignIntervals(intervals, intervals.size());
    return 0;
}
```

## 蟒蛇 3

```
# Python implementation for intervals
# scheduling to two processors such
# that there are no overlapping intervals

# Function to assign the intervals
# to two different processors
def assignIntervals(interval, n):

    # Loop to pair the interval
    # with their indices
    for i in range(n):
        interval[i].append(i)

    # sorting the interval by
    # their startb times
    interval.sort(key = lambda x: x[0])

    firstEndTime = -1
    secondEndTime = -1
    fin = ''
    flag = False

    # Loop to iterate over the
    # intervals with their start time
    for i in range(n):
        if interval[i][0] >= firstEndTime:
            firstEndTime = interval[i][1]
            interval[i].append('S')
        elif interval[i][0] >= secondEndTime:
            secondEndTime = interval[i][1]
            interval[i].append('F')
        else:
            flag = True
            break

    # Condition to check if there
    # is a possible solution
    if flag:
        print(-1)
    else:
        form = ['']*n
        for i in range(n):
            indi = interval[i][2]
            form[indi] = interval[i][3]
        # form = ''.join(form)
        print(form, ", ")

# Driver Code   
if __name__ == "__main__":
    intervals = [[360, 480], [420, 540], [600, 660]]

    # Function Call
    assignIntervals(intervals, len(intervals))
```

**Output:** 

```
['S', 'F', 'S'] ,
```

**时间复杂度:**O(NlogN)
T3】辅助空间: O(N)