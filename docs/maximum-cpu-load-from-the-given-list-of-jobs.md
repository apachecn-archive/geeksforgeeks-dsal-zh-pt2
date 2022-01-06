# 给定作业列表中的最大 CPU 负载

> 原文:[https://www . geesforgeks . org/给定作业列表中的最大 cpu 负载/](https://www.geeksforgeeks.org/maximum-cpu-load-from-the-given-list-of-jobs/)

```
Given an array of jobs with different time requirements, where each job consists of start time, end time and CPU load. The task is to find the maximum CPU load at any time if all jobs are running on the same machine.
```

**示例:**

> **输入:**作业[] = {{1，4，3}，{2，5，4}，{7，9，6}}
> **输出:** 7
> **说明:**
> 在上面给定的作业中，有两个重叠的作业。
> 也就是说，作业[1，4，3]和[2，5，4]在[2，4]
> 中的时间段内重叠。因此，此时的最大 CPU 负载将是最大的(3 + 4 = 7)。
> 
> **输入:**作业[] = {{6，7，10}，{2，4，11}，{8，12，15}}
> **输出:** 15
> **说明:**
> 此后，没有重叠的作业。
> 最大中央处理器负载将为–最大值(10，11，15) = 15

这个问题一般是[合并区间](https://www.geeksforgeeks.org/merging-intervals/)的应用。
**方法:**想法是根据作业的结束时间维持作业的[最小堆](https://www.geeksforgeeks.org/min-heap-in-java/)。然后，对于每个实例，找到已完成的作业，并将其从最小堆中移除。也就是说，检查最小堆中作业的结束时间是否早于当前作业的开始时间。同样，在每个实例中，通过取最小堆中存在的所有作业的总和，找到机器上的最大 CPU 负载。

**例如:**

```
Given Jobs be {{1, 4, 3}, {2, 5, 4}, {7, 9, 6}}
Min-Heap - {}

Instance 1:
The job {1, 4, 3} is inserted into the min-heap
Min-Heap - {{1, 4, 3}},
Total CPU Load  = 3

Instance 2:
The job {2, 5, 4} is inserted into the min-heap.
While the job {1, 4, 3} is still in the CPU, 
because end-time of Job 1 is greater than 
the start time of the new job {2, 5, 4}.
Min-Heap - {{1, 4, 3}, {2, 5, 4}}
Total CPU Load = 4 + 3 = 7

Instance 3:
The job {7, 9, 6} is inserted into the min-heap.
After popping up all the other jobs because their
end time is less than the start time of the new job
Min Heap - {7, 9, 6}
Total CPU Load =  6

Maximum CPU Load = max(3, 7, 6) = 7
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum CPU Load from the given
// lists of the jobs

#include <algorithm>
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

// Blueprint of the job
class Job {
public:
    int start = 0;
    int end = 0;
    int cpuLoad = 0;

    // Constructor function for
    // the CPU Job
    Job(int start, int end, int cpuLoad)
    {
        this->start = start;
        this->end = end;
        this->cpuLoad = cpuLoad;
    }
};

class MaximumCPULoad {

    // Structure to compare two
    // CPU Jobs by their end time
public:
    struct endCompare {
        bool operator()(const Job& x, const Job& y)
        {
            return x.end > y.end;
        }
    };

    // Function to find the maximum
    // CPU Load at any instance of
    // the time for given jobs
    static int findMaxCPULoad(vector<Job>& jobs)
    {
        // Condition when there are
        // no jobs then CPU Load is 0
        if (jobs.empty()) {
            return 0;
        }

        // Sorting all the jobs
        // by their start time
        sort(jobs.begin(), jobs.end(),
             [](const Job& a, const Job& b) {
                 return a.start < b.start;
             });

        int maxCPULoad = 0;
        int currentCPULoad = 0;

        // Min-heap implemented using the
        // help of the priority queue
        priority_queue<Job, vector<Job>, endCompare>
            minHeap;

        // Loop to iterate over all the
        // jobs from the given list
        for (auto job : jobs) {

            // Loop to remove all jobs from
            // the heap which is ended
            while (!minHeap.empty()
                   && job.start > minHeap.top().end) {
                currentCPULoad -= minHeap.top().cpuLoad;
                minHeap.pop();
            }

            // Add the current Job to CPU
            minHeap.push(job);
            currentCPULoad += job.cpuLoad;
            maxCPULoad = max(maxCPULoad, currentCPULoad);
        }
        return maxCPULoad;
    }
};

// Driver Code
int main(int argc, char* argv[])
{
    vector<Job> input
        = { { 1, 4, 3 }, { 7, 9, 6 }, { 2, 5, 4 } };
    cout << "Maximum CPU load at any time: "
         << MaximumCPULoad::findMaxCPULoad(input) << endl;
}
```

## 蟒蛇 3

```
# Python implementation to find the
# maximum CPU Load from the given
# lists of the jobs

from heapq import *

# Blueprint of the job

class job:

    # Constructor of the Job
    def __init__(self, start,
                 end, cpu_load):
        self.start = start
        self.end = end
        self.cpu_load = cpu_load

    # Operator overloading for the
    # Object that is Job
    def __lt__(self, other):

        # min heap based on job.end
        return self.end < other.end

# Function to find the maximum
# CPU Load for the given list of jobs

def find_max_cpu_load(jobs):

    # Sort the jobs by start time
    jobs.sort(key=lambda x: x.start)
    max_cpu_load, current_cpu_load = 0, 0

    # Min-Heap
    min_heap = []

    # Loop to iterate over the list
    # of the jobs given for the CPU
    for j in jobs:

        # Remove all the jobs from
        # the min-heap which ended
        while(len(min_heap) > 0 and
              j.start >= min_heap[0].end):
            current_cpu_load -= min_heap[0].cpu_load
            heappop(min_heap)

        # Add the current job
        # into min_heap
        heappush(min_heap, j)
        current_cpu_load += j.cpu_load
        max_cpu_load = max(max_cpu_load,
                           current_cpu_load)
    return max_cpu_load

# Driver Code
if __name__ == "__main__":
    jobs = [job(1, 4, 3), job(2, 5, 4),
            job(7, 9, 6)]

    print("Maximum CPU load at any time: " +
          str(find_max_cpu_load(jobs)))
```

**Output**

```
Maximum CPU load at any time: 7
```

**性能分析:**

*   **时间复杂度:** O(N*logN)
*   **辅助空间:** O(N)

**进场 2:**

想法很简单。我们假设有 n 个区间，所以我们有 2n 个端点(这里端点是一个区间的终点，它的值是与之相关的时间)。我们可以取一个端点，并将其与关联的负载值和一个标志相结合，该标志表示它是一个区间的起点还是终点。然后，我们可以按照递增的顺序对端点进行排序(如果端点值存在联系，那么我们将通过将在第一位置开始的端点与结束的端点进行比较来打破联系；如果两个端点都开始或结束，那么我们将任意地打破平局)。

排序后，我们将使用 for 循环继续遍历端点。如果我们有一个端点，它是一个区间的起点，那么我们将把与之相关的负载值加到一个变量中，比如说，count。我们还将取计数值的最大值，并将其存储在名为 result 的变量中。

但是当我们得到一个即将结束的端点时，我们将从计数中减少与之相关的负载值。

最后我们将返回结果。

让我们举个例子:假设作业是{1，4，3}、{2，5，4}、{7，9，6}。

我们排序的端点将是 1(开始)、2(开始)、4(结束)、5(结束)、7(开始)、9(结束)。

相应的负载是 3，4，3，4，6，6。

开始移动端点:

所以在遍历第一个端点 1(start)之后，我们有 count+=3(这里 3 是与之相关的负载),所以 count =3。因为 1 是起点，所以我们将更新结果。所以结果=max(结果，计数)所以，结果=3。

遍历 2(开始)后，我们有 count+=4，因此 count=7，result=max(result，count)=7。

在遍历 4(结束)之后，我们有 count-=3(我们减去了，因为它是结束点)，所以 count=4。结果将不会更新，因为我们正在减少计数。

在 ttraveling 5 _ end)之后，我们有 count-=4，因此 count=0。

遍历 7(开始)后，我们有 count+=6，因此 count=6，result=max(result，count)=7。

在 ttraveling 9 _ end)之后，我们有 count-=6，因此 count=0。

我们的成绩是 7 分。

## C++14

```
// C++ implementation to find the
// maximum CPU Load from the given array of jobs

#include <bits/stdc++.h>
using namespace std;

// the job struct will have s(starting time) , e(ending time) , load(cpu load)
struct Job {
    int s, e, load;
};

// endpoint struct will have val(the time associated with the endpoint),
// load(cpu load associated with the endpoint),
// a flag isStart which will tell if the endpoint is starting or ending point of
// an interval
struct Endpoint {
    int val, load;
    bool isStart;
};

// custom comparator function which is used by the c++ sort stl
bool comp(const Endpoint& a, const Endpoint& b) {
    if (a.val != b.val)
        return a.val < b.val;
    return a.isStart == true && b.isStart == false;
}
//function to find maximum cpu load
int maxCpuLoad(vector<Job> v)
{
    int count = 0; // count will contain the count of current loads
      int result = 0; // result will contain maximum of all counts

      // this data array will contain all the endpoints combined with their load values
      // and flags telling whether they are starting or ending point
    vector<Endpoint> data;

    for (int i = 0; i < v.size(); i++) {
        data.emplace_back(Endpoint{ v[i].s, v[i].load, true});
        data.emplace_back(Endpoint{ v[i].e, v[i].load, false});
    }

    sort(data.begin(), data.end(), comp);

    for (int i = 0; i < data.size(); i++) {
        if (data[i].isStart == true) {
            count += data[i].load;
            result = max(result, count);
        }
        else
            count -= data[i].load;

    }

    return result;
}
//Driver code to test maxCpuLoad function
int main() {
    vector<Job> v = {
        {6, 7, 10},
          {2, 4, 11},
          {8, 12, 15}
    };
    cout << maxCpuLoad(v);
    return 0;
}
// this code is contributed by Mohit Puri
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum CPU Load from the given array of jobs

# the job struct will have s(starting time) , e(ending time) , load(cpu load)
class Job:
    def __init__(self,s,e,l) -> None:
        self.s =s; self.e =e; self.load = l

# endpoint will have val(the time associated with the endpoint),
# load(cpu load associated with the endpoint),
# a flag isStart which will tell if the endpois starting or ending poof
# an interval
class Endpoint:
    def __init__(self, v=0, l=0, isStart=False) -> None:
        self.val = v
        self.load = l
        self.isStart = isStart

    def __lt__(self, other):
        if self.val != other.val:
            return self.val < other.val
        return self.isStart == True and other.isStart == False

# function to find maximum cpu load
def maxCpuLoad(v):
    count = 0  # count will contain the count of current loads
    result = 0  # result will contain maximum of all counts

    # this data array will contain all the endpoints combined with their load values
    # and flags telling whether they are starting or ending point
    data = []

    for i in range(len(v)):
        data.append(Endpoint(v[i].s, v[i].load, True))
        data.append(Endpoint(v[i].e, v[i].load, False))

    data.sort()

    for i in range(len(data)):
        if data[i].isStart == True:
            count += data[i].load
            result = max(result, count)

        else:
            count -= data[i].load
    return result

# Driver code to test maxCpuLoad function
if __name__ == "__main__":
    v = [Job(6, 7, 10), Job(2, 4, 11), Job(8, 12, 15)]

    print(maxCpuLoad(v))
```

**Output**

```
15
```

**【时间复杂度】** : O(nlogn)用于对数据数组进行排序。

**空间复杂度** : O(n)即数据数组的大小